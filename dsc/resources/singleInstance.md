---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Psaní jednorázové instance prostředku DSC (osvědčený postup)
ms.openlocfilehash: 9494964b1b13eaa082ad5cbc279b4586bb7211cc
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403852"
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a><span data-ttu-id="1b623-103">Psaní jednorázové instance prostředku DSC (osvědčený postup)</span><span class="sxs-lookup"><span data-stu-id="1b623-103">Writing a single-instance DSC resource (best practice)</span></span>

><span data-ttu-id="1b623-104">**Poznámka:** Toto téma popisuje nejvhodnějším postupem pro definování prostředek DSC, která umožňuje jenom jednu instanci v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1b623-104">**Note:** This topic describes a best practice for defining a DSC resource that allows only a single instance in a configuration.</span></span> <span data-ttu-id="1b623-105">V současné době neexistuje žádný integrovanou funkci DSC k tomu.</span><span class="sxs-lookup"><span data-stu-id="1b623-105">Currently, there is no built-in DSC feature to do this.</span></span> <span data-ttu-id="1b623-106">Který může v budoucnu změnit.</span><span class="sxs-lookup"><span data-stu-id="1b623-106">That might change in the future.</span></span>

<span data-ttu-id="1b623-107">Existují situace, kdy nechcete povolit prostředek, který se má použít více než jednou v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1b623-107">There are situations where you don't want to allow a resource to be used multiple times in a configuration.</span></span> <span data-ttu-id="1b623-108">Například v předchozích implementacích služby [xTimeZone](https://github.com/PowerShell/xTimeZone) prostředků, konfigurace lze zavolat prostředku více než jednou, nastavení časového pásma na jiné nastavení v každém bloku prostředků:</span><span class="sxs-lookup"><span data-stu-id="1b623-108">For example, in a previous implementation of the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource, a configuration could call the resource multiple times, setting the time zone to a different setting in each resource block:</span></span>

```powershell
Configuration SetTimeZone
{
    Param
    (
        [String[]]$NodeName = $env:COMPUTERNAME

    )

    Import-DSCResource -ModuleName xTimeZone


    Node $NodeName
    {
         xTimeZone TimeZoneExample
         {

            TimeZone = 'Eastern Standard Time'
         }

         xTimeZone TimeZoneExample2
         {

            TimeZone = 'Pacific Standard Time'

         }

    }
}
```

<span data-ttu-id="1b623-109">Toto je vzhledem ke způsobu klíče prostředku DSC fungovat.</span><span class="sxs-lookup"><span data-stu-id="1b623-109">This is because of the way DSC resource keys work.</span></span> <span data-ttu-id="1b623-110">Prostředek musí mít alespoň jednu klíčovou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1b623-110">A resource must have at least one key property.</span></span> <span data-ttu-id="1b623-111">Instance prostředku se považuje za jedinečné, pokud je jedinečná kombinace hodnot všech vlastností klíče.</span><span class="sxs-lookup"><span data-stu-id="1b623-111">A resource instance is considered unique if the combination of the values of all of its key properties is unique.</span></span> <span data-ttu-id="1b623-112">V předchozích implementacích [xTimeZone](https://github.com/PowerShell/xTimeZone) prostředku měli jenom jednu vlastnost –**časové pásmo**, které se musí být klíč.</span><span class="sxs-lookup"><span data-stu-id="1b623-112">In its previous implementation, the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource had only one property--**TimeZone**, which was required to be a key.</span></span> <span data-ttu-id="1b623-113">Z tohoto důvodu by konfigurace, jako je například nad kompilace a spuštění bez předchozího upozornění.</span><span class="sxs-lookup"><span data-stu-id="1b623-113">Because of this, a configuration such as the one above would compile and run without warning.</span></span> <span data-ttu-id="1b623-114">Každá z **xTimeZone** bloky prostředků je považován za jedinečný.</span><span class="sxs-lookup"><span data-stu-id="1b623-114">Each of the **xTimeZone** resource blocks is considered unique.</span></span> <span data-ttu-id="1b623-115">To by způsobilo konfiguraci tak, aby opakovaně použít pro uzel cyklí časové pásmo vpřed a zpět.</span><span class="sxs-lookup"><span data-stu-id="1b623-115">This would cause the configuration to be repeatedly applied to the node, cycling the timezone back and forth.</span></span>

<span data-ttu-id="1b623-116">K zajištění, že konfigurace nastavit časové pásmo pro cílový uzel pouze jednou, byl aktualizován, přidejte druhý vlastnost prostředku **IsSingleInstance**, který začal být klíčová vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1b623-116">To ensure that a configuration could set the time zone for a target node only once, the resource was updated to add a second property, **IsSingleInstance**, that became the key property.</span></span>
<span data-ttu-id="1b623-117">**IsSingleInstance** byla omezena na jednu hodnotu "Ano" pomocí **chybu**.</span><span class="sxs-lookup"><span data-stu-id="1b623-117">The **IsSingleInstance** was limited to a single value, "Yes" by using a **ValueMap**.</span></span> <span data-ttu-id="1b623-118">Bylo staré schéma MOF pro prostředek:</span><span class="sxs-lookup"><span data-stu-id="1b623-118">The old MOF schema for the resource was:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="1b623-119">Aktualizované schéma MOF pro prostředek je:</span><span class="sxs-lookup"><span data-stu-id="1b623-119">The updated MOF schema for the resource is:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="1b623-120">Skript prostředků bylo aktualizováno také používat nový parametr.</span><span class="sxs-lookup"><span data-stu-id="1b623-120">The resource script was also updated to use the new parameter.</span></span> <span data-ttu-id="1b623-121">Tady je původní skript prostředků:</span><span class="sxs-lookup"><span data-stu-id="1b623-121">Here is the old resource script:</span></span>

```powershell
function Get-TargetResource
{
    [CmdletBinding()]
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Get the current TimeZone
    $CurrentTimeZone = Get-TimeZone

    $returnValue = @{
        TimeZone = $CurrentTimeZone
        IsSingleInstance = 'Yes'
    }

    #Output the target resource
    $returnValue
}


function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output the result of Get-TargetResource function.
    $CurrentTimeZone = Get-TimeZone

    if($PSCmdlet.ShouldProcess("'$TimeZone'","Replace the System Time Zone"))
    {
        try
        {
            if($CurrentTimeZone -ne $TimeZone)
            {
                Write-Verbose -Verbose "Setting the TimeZone"
                Set-TimeZone -TimeZone $TimeZone}
            else
            {
                Write-Verbose -Verbose "TimeZone already set to $TimeZone"
            }
        }
        catch
        {
            $ErrorMsg = $_.Exception.Message
            Write-Verbose -Verbose $ErrorMsg
        }
    }
}


function Test-TargetResource
{
    [CmdletBinding()]
    [OutputType([Boolean])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output from Get-TargetResource
    $CurrentTimeZone = Get-TimeZone

    if($TimeZone -eq $CurrentTimeZone)
    {
        return $true
    }
    else
    {
        return $false
    }
}

Function Get-TimeZone {
    [CmdletBinding()]
    param()

    & tzutil.exe /g
}

Function Set-TimeZone {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [System.String]
        $TimeZone
    )

    try
    {
        & tzutil.exe /s $TimeZone
    }
    catch
    {
        $ErrorMsg = $_.Exception.Message
        Write-Verbose $ErrorMsg
    }
}

Export-ModuleMember -Function *-TargetResource
```

<span data-ttu-id="1b623-122">Všimněte si, že **časové pásmo** vlastnost už není klíč.</span><span class="sxs-lookup"><span data-stu-id="1b623-122">Notice that the **TimeZone** property is no longer a key.</span></span> <span data-ttu-id="1b623-123">Když teď aplikaci filled konfiguraci, pokusí se nastavit časové pásmo dvakrát (s použitím dva různé **xTimeZone** bloky s různými **časové pásmo** hodnoty), při pokusu o kompilaci konfigurace způsobí chybu:</span><span class="sxs-lookup"><span data-stu-id="1b623-123">Now, if a configuration attempts to set the time zone twice (by using two different **xTimeZone** blocks with different **TimeZone** values), attempting to compile the configuration will cause an error:</span></span>

```powershell
Test-ConflictingResources : A conflict was detected between resources '[xTimeZone]TimeZoneExample (::15::10::xTimeZone)' and
'[xTimeZone]TimeZoneExample2 (::22::10::xTimeZone)' in node 'CONTOSO-CLIENT'. Resources have identical key properties but there are differences in the
following non-key properties: 'TimeZone'. Values 'Eastern Standard Time' don't match values 'Pacific Standard Time'. Please update these property
values so that they are identical in both cases.
At line:271 char:9
+         Test-ConflictingResources $keywordName $canonicalizedValue $k ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : ConflictingDuplicateResource,Test-ConflictingResources
Errors occurred while processing configuration 'SetTimeZone'.
At C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:3705 char:5
+     throw $ErrorRecord
+     ~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (SetTimeZone:String) [], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessConfiguration
```
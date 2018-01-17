---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Zápis prostředek DSC jedné instance (doporučený postup)"
ms.openlocfilehash: 4510bec5b4600334b845831ec6700da01e1a110c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a><span data-ttu-id="3954e-103">Zápis prostředek DSC jedné instance (doporučený postup)</span><span class="sxs-lookup"><span data-stu-id="3954e-103">Writing a single-instance DSC resource (best practice)</span></span>

><span data-ttu-id="3954e-104">**Poznámka:** Toto téma popisuje osvědčený postup pro definování prostředek DSC, který umožňuje pouze jednu instanci v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="3954e-104">**Note:** This topic describes a best practice for defining a DSC resource that allows only a single instance in a configuration.</span></span> <span data-ttu-id="3954e-105">V současné době není k dispozici žádné předdefinované funkce DSC k tomu.</span><span class="sxs-lookup"><span data-stu-id="3954e-105">Currently, there is no built-in DSC feature to do this.</span></span> <span data-ttu-id="3954e-106">Může v budoucnu změnit.</span><span class="sxs-lookup"><span data-stu-id="3954e-106">That might change in the future.</span></span>

<span data-ttu-id="3954e-107">Existují situace, kdy nechcete povolit prostředků, který se má použít více než jednou. v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="3954e-107">There are situations where you don't want to allow a resource to be used multiple times in a configuration.</span></span> <span data-ttu-id="3954e-108">Například v předchozích implementacích služby [xTimeZone](https://github.com/PowerShell/xTimeZone) prostředků, konfigurace může volat prostředek vícekrát, nastavení časového pásma na jiné nastavení v každém bloku prostředků:</span><span class="sxs-lookup"><span data-stu-id="3954e-108">For example, in a previous implementation of the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource, a configuration could call the resource multiple times, setting the time zone to a different setting in each resource block:</span></span>

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

<span data-ttu-id="3954e-109">To je kvůli způsob, jakým klíče prostředků DSC fungovat.</span><span class="sxs-lookup"><span data-stu-id="3954e-109">This is because of the way DSC resource keys work.</span></span> <span data-ttu-id="3954e-110">Prostředek musí mít alespoň jednu klíčovou vlastnost.</span><span class="sxs-lookup"><span data-stu-id="3954e-110">A resource must have at least one key property.</span></span> <span data-ttu-id="3954e-111">Instance prostředků je považován za jedinečný, pokud je kombinace hodnot všech jeho klíčové vlastnosti jedinečná.</span><span class="sxs-lookup"><span data-stu-id="3954e-111">A resource instance is considered unique if the combination of the values of all of its key properties is unique.</span></span> <span data-ttu-id="3954e-112">V předchozích implementacích [xTimeZone](https://github.com/PowerShell/xTimeZone) prostředků měl pouze jednu vlastnost--**časové pásmo**, které se musí být klíč.</span><span class="sxs-lookup"><span data-stu-id="3954e-112">In its previous implementation, the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource had only one property--**TimeZone**, which was required to be a key.</span></span> <span data-ttu-id="3954e-113">Z tohoto důvodu by konfigurace, jako je třeba výše zkompilování a spuštění bez upozornění.</span><span class="sxs-lookup"><span data-stu-id="3954e-113">Because of this, a configuration such as the one above would compile and run without warning.</span></span> <span data-ttu-id="3954e-114">Každý z **xTimeZone** bloky prostředků se považuje za jedinečný.</span><span class="sxs-lookup"><span data-stu-id="3954e-114">Each of the **xTimeZone** resource blocks is considered unique.</span></span> <span data-ttu-id="3954e-115">To by způsobilo konfigurace opakovaně použít k uzlu, prosté časové pásmo a zpět.</span><span class="sxs-lookup"><span data-stu-id="3954e-115">This would cause the configuration to be repeatedly applied to the node, cycling the timezone back and forth.</span></span>

<span data-ttu-id="3954e-116">K zajištění, že konfigurace může nastavit časové pásmo pro cílový uzel pouze jednou, byl aktualizován přidáním druhou vlastností prostředku **IsSingleInstance**, která se aktivovala vlastnost klíče.</span><span class="sxs-lookup"><span data-stu-id="3954e-116">To ensure that a configuration could set the time zone for a target node only once, the resource was updated to add a second property, **IsSingleInstance**, that became the key property.</span></span> <span data-ttu-id="3954e-117">**IsSingleInstance** byla omezena na jednu hodnotu "Ano" pomocí **chybu**.</span><span class="sxs-lookup"><span data-stu-id="3954e-117">The **IsSingleInstance** was limited to a single value, "Yes" by using a **ValueMap**.</span></span> <span data-ttu-id="3954e-118">Byl původní MOF schématu pro prostředek:</span><span class="sxs-lookup"><span data-stu-id="3954e-118">The old MOF schema for the resource was:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="3954e-119">Aktualizované schéma MOF pro prostředek je:</span><span class="sxs-lookup"><span data-stu-id="3954e-119">The updated MOF schema for the resource is:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="3954e-120">Skript prostředků bylo aktualizováno také používat nový parametr.</span><span class="sxs-lookup"><span data-stu-id="3954e-120">The resource script was also updated to use the new parameter.</span></span> <span data-ttu-id="3954e-121">Tady je starý skriptu prostředků:</span><span class="sxs-lookup"><span data-stu-id="3954e-121">Here is the old resource script:</span></span>

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

<span data-ttu-id="3954e-122">Všimněte si, že **časové pásmo** vlastnost je už klíč.</span><span class="sxs-lookup"><span data-stu-id="3954e-122">Notice that the **TimeZone** property is no longer a key.</span></span> <span data-ttu-id="3954e-123">Nyní, pokud konfigurace pokusí se nastavit časové pásmo dvakrát (pomocí dva různé **xTimeZone** bloky jiné **časové pásmo** hodnoty), pokus o zkompilování konfigurace dojde k chybě:</span><span class="sxs-lookup"><span data-stu-id="3954e-123">Now, if a configuration attempts to set the time zone twice (by using two different **xTimeZone** blocks with different **TimeZone** values), attempting to compile the configuration will cause an error:</span></span>

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
   

---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Pomocí nástroje Návrhář prostředků
ms.openlocfilehash: 3fd2f06cf46602ee30dd34f8e7bd77d3c92b808f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403722"
---
# <a name="using-the-resource-designer-tool"></a><span data-ttu-id="123ee-103">Pomocí nástroje Návrhář prostředků</span><span class="sxs-lookup"><span data-stu-id="123ee-103">Using the Resource Designer tool</span></span>

> <span data-ttu-id="123ee-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="123ee-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="123ee-105">Nástroj Návrhář prostředků je sada rutin, které jsou vystavené **xDscResourceDesigner** modul, který usnadnit vytváření prostředků Windows PowerShell Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="123ee-105">The Resource Designer tool is a set of cmdlets exposed by the **xDscResourceDesigner** module that make creating Windows PowerShell Desired State Configuration (DSC) resources easier.</span></span> <span data-ttu-id="123ee-106">Rutiny v tomto prostředku pomoci vytvořit schéma MOF, modul skriptu a strukturu adresářů pro nový prostředek.</span><span class="sxs-lookup"><span data-stu-id="123ee-106">The cmdlets in this resource help create the MOF schema, the script module, and the directory structure for your new resource.</span></span> <span data-ttu-id="123ee-107">Další informace o prostředcích DSC najdete v tématu [vytvářet vlastní Windows PowerShell Desired State Configuration prostředky](authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="123ee-107">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md).</span></span>
<span data-ttu-id="123ee-108">V tomto tématu vytvoříme prostředek DSC, který slouží ke správě uživatelů služby Active Directory.</span><span class="sxs-lookup"><span data-stu-id="123ee-108">In this topic, we will create a DSC resource that manages Active Directory users.</span></span>
<span data-ttu-id="123ee-109">Použití [Install-Module](/powershell/module/PowershellGet/Install-Module) rutinu instalace **xDscResourceDesigner** modulu.</span><span class="sxs-lookup"><span data-stu-id="123ee-109">Use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xDscResourceDesigner** module.</span></span>

><span data-ttu-id="123ee-110">**Poznámka:**: **Install-Module** je součástí **PowerShellGet** modulu, která je obsažena v Powershellu 5.0.</span><span class="sxs-lookup"><span data-stu-id="123ee-110">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="123ee-111">Můžete stáhnout **PowerShellGet** modulu pro PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="123ee-111">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>

## <a name="creating-resource-properties"></a><span data-ttu-id="123ee-112">Vytvoření vlastností prostředku</span><span class="sxs-lookup"><span data-stu-id="123ee-112">Creating resource properties</span></span>
<span data-ttu-id="123ee-113">První věc, kterou budeme muset udělat se při rozhodování o vlastnosti, které odhalují prostředku.</span><span class="sxs-lookup"><span data-stu-id="123ee-113">The first thing we need to do is decide on properties that the resource will expose.</span></span> <span data-ttu-id="123ee-114">V tomto příkladu jsme budou definovat uživatele služby Active Directory s následujícími vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="123ee-114">For this example, we will define an Active Directory user with the following properties.</span></span>

<span data-ttu-id="123ee-115">Název parametru popis</span><span class="sxs-lookup"><span data-stu-id="123ee-115">Parameter name  Description</span></span>
* <span data-ttu-id="123ee-116">**Uživatelské jméno**: Klíčová vlastnost, která jednoznačně identifikuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="123ee-116">**UserName**: Key property that uniquely identifies a user.</span></span>
* <span data-ttu-id="123ee-117">**Zajištění**: Určuje, zda by měl být uživatelský účet k dispozici nebo chybí.</span><span class="sxs-lookup"><span data-stu-id="123ee-117">**Ensure**: Specifies whether the user account should be Present or Absent.</span></span> <span data-ttu-id="123ee-118">Tento parametr budou mít pouze dva možné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="123ee-118">This parameter will have only two possible values.</span></span>
* <span data-ttu-id="123ee-119">**DomainCredential**: Heslo domény pro daného uživatele.</span><span class="sxs-lookup"><span data-stu-id="123ee-119">**DomainCredential**: The domain password for the user.</span></span>
* <span data-ttu-id="123ee-120">**Heslo**: Požadované heslo pro uživatele povolit konfiguraci, kterou chcete změnit heslo uživatele v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="123ee-120">**Password**: The desired password for the user to allow a configuration to change the user password if necessary.</span></span>

<span data-ttu-id="123ee-121">K vytvoření vlastnosti, použijeme **New-xDscResourceProperty** rutiny.</span><span class="sxs-lookup"><span data-stu-id="123ee-121">To create the properties, we use the **New-xDscResourceProperty** cmdlet.</span></span> <span data-ttu-id="123ee-122">Následující příkazy prostředí PowerShell vytvoří vlastností popsaných výše.</span><span class="sxs-lookup"><span data-stu-id="123ee-122">The following PowerShell commands create the properties described above.</span></span>

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a><span data-ttu-id="123ee-123">Vytvoření prostředku</span><span class="sxs-lookup"><span data-stu-id="123ee-123">Create the resource</span></span>

<span data-ttu-id="123ee-124">Teď, když byly vytvořeny vlastnosti prostředku, budeme volat **New-xDscResource** rutina pro vytvoření prostředku.</span><span class="sxs-lookup"><span data-stu-id="123ee-124">Now that the resource properties have been created, we can call the **New-xDscResource** cmdlet to create the resource.</span></span> <span data-ttu-id="123ee-125">**New-xDscResource** rutiny přebírá seznam vlastností, které jako parametry.</span><span class="sxs-lookup"><span data-stu-id="123ee-125">The **New-xDscResource** cmdlet takes the list of properties as parameters.</span></span> <span data-ttu-id="123ee-126">Přijímá také cestu, kde by měl být vytvořen modulu, název nového prostředku a název modulu, ve kterém je obsažená.</span><span class="sxs-lookup"><span data-stu-id="123ee-126">It also takes the path where the module should be created, the name of the new resource, and the name of the module in which it is contained.</span></span> <span data-ttu-id="123ee-127">Následující příkaz Powershellu vytvoří prostředek.</span><span class="sxs-lookup"><span data-stu-id="123ee-127">The following PowerShell command creates the resource.</span></span>

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

<span data-ttu-id="123ee-128">**New-xDscResource** rutina vytvoří schéma MOF, skript kostru prostředků, vyžaduje adresářovou strukturu pro nový prostředek a manifest pro modul, který zpřístupňuje nový prostředek.</span><span class="sxs-lookup"><span data-stu-id="123ee-128">The **New-xDscResource** cmdlet creates the MOF schema, a skeleton resource script, the required directory structure for your new resource, and a manifest for the module that exposes the new resource.</span></span>

<span data-ttu-id="123ee-129">Je v schématu soubor MOF **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, a jeho obsah následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="123ee-129">The MOF schema file is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, and its contents are as follows.</span></span>

```
[ClassVersion("1.0.0.0"), FriendlyName("Demo_ADUser")]
class Demo_ADUser : OMI_BaseResource
{
  [Key] string UserName;
  [Write, ValueMap{"Present","Absent"}, Values{"Present","Absent"}] string Ensure;
  [Write, EmbeddedInstance("MSFT_Credential")] String DomainCredential;
  [Write, EmbeddedInstance("MSFT_Credential")] String Password;
};
```

<span data-ttu-id="123ee-130">Skript prostředků je na **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span><span class="sxs-lookup"><span data-stu-id="123ee-130">The resource script is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span></span> <span data-ttu-id="123ee-131">Nezahrnuje skutečné logiku pro implementaci prostředku, který je nutné přidat sami.</span><span class="sxs-lookup"><span data-stu-id="123ee-131">It does not include the actual logic to implement the resource, which you must add yourself.</span></span> <span data-ttu-id="123ee-132">Obsah kostru skriptu jsou následující.</span><span class="sxs-lookup"><span data-stu-id="123ee-132">The contents of the skeleton script are as follows.</span></span>

```powershell
function Get-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Collections.Hashtable])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $returnValue = @{
  UserName = [System.String]
  Ensure = [System.String]
  DomainAdminCredential = [System.Management.Automation.PSCredential]
  Password = [System.Management.Automation.PSCredential]
  }

  $returnValue
  #>
}


function Set-TargetResource
{
  [CmdletBinding()]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  #Include this line if the resource requires a system reboot.
  #$global:DSCMachineStatus = 1


}


function Test-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Boolean])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $result = [System.Boolean]

  $result
  #>
}


Export-ModuleMember -Function *-TargetResource
```

## <a name="updating-the-resource"></a><span data-ttu-id="123ee-133">Aktualizuje se prostředek</span><span class="sxs-lookup"><span data-stu-id="123ee-133">Updating the resource</span></span>

<span data-ttu-id="123ee-134">Pokud potřebujete přidat nebo upravit seznam parametrů prostředku, můžete volat **aktualizace xDscResource** rutiny.</span><span class="sxs-lookup"><span data-stu-id="123ee-134">If you need to add or modify the parameter list of the resource, you can call the **Update-xDscResource** cmdlet.</span></span> <span data-ttu-id="123ee-135">Rutina aktualizace prostředku se nový seznam parametrů.</span><span class="sxs-lookup"><span data-stu-id="123ee-135">The cmdlet updates the resource with a new parameter list.</span></span> <span data-ttu-id="123ee-136">Pokud jste už přidali logiky ve vašem skriptu prostředků, je ponechán beze změny.</span><span class="sxs-lookup"><span data-stu-id="123ee-136">If you have already added logic in your resource script, it is left intact.</span></span>

<span data-ttu-id="123ee-137">Předpokládejme například, že chcete poslední protokolu zahrnout v čase pro uživatele v naší prostředku.</span><span class="sxs-lookup"><span data-stu-id="123ee-137">For example, suppose you want to include the last log in time for the user in our resource.</span></span> <span data-ttu-id="123ee-138">Místo psaní znovu zcela prostředek, můžete volat **New-xDscResourceProperty** vytvořit novou vlastnost a poté zavolejte **aktualizace xDscResource** a přidat nové vlastnosti do seznam vlastností.</span><span class="sxs-lookup"><span data-stu-id="123ee-138">Rather than writing the resource again completely, you can call the **New-xDscResourceProperty** to create the new property, and then call **Update-xDscResource** and add your new property to the properties list.</span></span>

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a><span data-ttu-id="123ee-139">Testování schématu zdroje</span><span class="sxs-lookup"><span data-stu-id="123ee-139">Testing a resource schema</span></span>

<span data-ttu-id="123ee-140">Nástroj Návrhář prostředků zpřístupňuje jeden další rutiny, které můžete použít k testování platnosti schématu MOF, který jste napsali ručně.</span><span class="sxs-lookup"><span data-stu-id="123ee-140">The Resource Designer tool exposes one more cmdlet that can be used to test the validity of a MOF schema that you have written manually.</span></span> <span data-ttu-id="123ee-141">Volání **testovací xDscSchema** předáním cesty prostředku schématu MOF jako parametr rutiny.</span><span class="sxs-lookup"><span data-stu-id="123ee-141">Call the **Test-xDscSchema** cmdlet, passing the path of a MOF resource schema as a parameter.</span></span> <span data-ttu-id="123ee-142">Rutina vydá všechny chyby ve schématu.</span><span class="sxs-lookup"><span data-stu-id="123ee-142">The cmdlet will output any errors in the schema.</span></span>

### <a name="see-also"></a><span data-ttu-id="123ee-143">Viz také</span><span class="sxs-lookup"><span data-stu-id="123ee-143">See Also</span></span>

#### <a name="concepts"></a><span data-ttu-id="123ee-144">Koncepty</span><span class="sxs-lookup"><span data-stu-id="123ee-144">Concepts</span></span>
[<span data-ttu-id="123ee-145">Vlastní Windows PowerShell Desired State Configuration prostředky sestavení</span><span class="sxs-lookup"><span data-stu-id="123ee-145">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

#### <a name="other-resources"></a><span data-ttu-id="123ee-146">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="123ee-146">Other Resources</span></span>
[<span data-ttu-id="123ee-147">xDscResourceDesigner modulu</span><span class="sxs-lookup"><span data-stu-id="123ee-147">xDscResourceDesigner Module</span></span>](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0)

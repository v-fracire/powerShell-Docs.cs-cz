---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "V nástroji Návrhář prostředků"
ms.openlocfilehash: c39b48f67d3874ee3cd2f2704aeb7390fa186fe4
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="using-the-resource-designer-tool"></a><span data-ttu-id="abed4-103">V nástroji Návrhář prostředků</span><span class="sxs-lookup"><span data-stu-id="abed4-103">Using the Resource Designer tool</span></span>

> <span data-ttu-id="abed4-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="abed4-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="abed4-105">Nástroj Návrhář prostředků je sada rutin, které jsou zveřejněné **xDscResourceDesigner** modul, který usnadnění vytváření prostředků požadovaného stavu aplikace Windows PowerShell (DSC).</span><span class="sxs-lookup"><span data-stu-id="abed4-105">The Resource Designer tool is a set of cmdlets exposed by the **xDscResourceDesigner** module that make creating Windows PowerShell Desired State Configuration (DSC) resources easier.</span></span> <span data-ttu-id="abed4-106">Rutiny v tento prostředek pomoci vytvořit schéma MOF, modulu skriptu a strukturu adresáře pro nový prostředek.</span><span class="sxs-lookup"><span data-stu-id="abed4-106">The cmdlets in this resource help create the MOF schema, the script module, and the directory structure for your new resource.</span></span> <span data-ttu-id="abed4-107">Další informace o prostředcích DSC najdete v tématu [sestavení vlastní Windows PowerShell požadovaného stavu konfigurace prostředků](authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="abed4-107">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md).</span></span>
<span data-ttu-id="abed4-108">V tomto tématu vytvoříme prostředek DSC, která spravuje uživatelů služby Active Directory.</span><span class="sxs-lookup"><span data-stu-id="abed4-108">In this topic, we will create a DSC resource that manages Active Directory users.</span></span>
<span data-ttu-id="abed4-109">Použití [instalace modulu](https://technet.microsoft.com/library/dn807162.aspx) k instalaci **xDscResourceDesigner** modulu.</span><span class="sxs-lookup"><span data-stu-id="abed4-109">Use the [Install-Module](https://technet.microsoft.com/library/dn807162.aspx) cmdlet to install the **xDscResourceDesigner** module.</span></span>

><span data-ttu-id="abed4-110">**Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="abed4-110">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="abed4-111">Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="abed4-111">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>

## <a name="creating-resource-properties"></a><span data-ttu-id="abed4-112">Vytvoření vlastností prostředku</span><span class="sxs-lookup"><span data-stu-id="abed4-112">Creating resource properties</span></span>
<span data-ttu-id="abed4-113">První věc, kterou je potřeba udělat je, vyberte vlastnosti, které se zveřejňují prostředku.</span><span class="sxs-lookup"><span data-stu-id="abed4-113">The first thing we need to do is decide on properties that the resource will expose.</span></span> <span data-ttu-id="abed4-114">V tomto příkladu jsme bude definovat uživatele služby Active Directory s následujícími vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="abed4-114">For this example, we will define an Active Directory user with the following properties.</span></span>
 
<span data-ttu-id="abed4-115">Název parametru popis</span><span class="sxs-lookup"><span data-stu-id="abed4-115">Parameter name  Description</span></span>
* <span data-ttu-id="abed4-116">**Uživatelské jméno**: klíčové vlastnosti, která jednoznačně identifikuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="abed4-116">**UserName**: Key property that uniquely identifies a user.</span></span>
* <span data-ttu-id="abed4-117">**Ujistěte se,**: Určuje, zda uživatelský účet, musí být přítomen nebo chybí.</span><span class="sxs-lookup"><span data-stu-id="abed4-117">**Ensure**: Specifies whether the user account should be Present or Absent.</span></span> <span data-ttu-id="abed4-118">Tento parametr bude obsahovat pouze dvě možné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="abed4-118">This parameter will have only two possible values.</span></span>
* <span data-ttu-id="abed4-119">**DomainCredential**: heslo domény pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="abed4-119">**DomainCredential**: The domain password for the user.</span></span>
* <span data-ttu-id="abed4-120">**Heslo**: požadované heslo pro uživatele pro povolení konfiguraci, kterou chcete změnit heslo uživatele v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="abed4-120">**Password**: The desired password for the user to allow a configuration to change the user password if necessary.</span></span>

<span data-ttu-id="abed4-121">Pokud chcete vytvořit vlastnosti, používáme **New-xDscResourceProperty** rutiny.</span><span class="sxs-lookup"><span data-stu-id="abed4-121">To create the properties, we use the **New-xDscResourceProperty** cmdlet.</span></span> <span data-ttu-id="abed4-122">Následující příkazy prostředí PowerShell vytvořit pomocí vlastností popsaných výše.</span><span class="sxs-lookup"><span data-stu-id="abed4-122">The following PowerShell commands create the properties described above.</span></span>

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential-Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a><span data-ttu-id="abed4-123">Vytvořit prostředek</span><span class="sxs-lookup"><span data-stu-id="abed4-123">Create the resource</span></span>

<span data-ttu-id="abed4-124">Teď, když byly vytvořeny vlastnosti prostředku, jsme volání **New-xDscResource** vytvořte prostředek.</span><span class="sxs-lookup"><span data-stu-id="abed4-124">Now that the resource properties have been created, we can call the **New-xDscResource** cmdlet to create the resource.</span></span> <span data-ttu-id="abed4-125">**New-xDscResource** rutiny přebírá seznam vlastností, jako parametry.</span><span class="sxs-lookup"><span data-stu-id="abed4-125">The **New-xDscResource** cmdlet takes the list of properties as parameters.</span></span> <span data-ttu-id="abed4-126">Také trvá cestu, kde by se měl vytvořit modul, název nového prostředku a název modulu, ve kterém se nachází.</span><span class="sxs-lookup"><span data-stu-id="abed4-126">It also takes the path where the module should be created, the name of the new resource, and the name of the module in which it is contained.</span></span> <span data-ttu-id="abed4-127">Následující příkaz prostředí PowerShell vytvoří prostředek.</span><span class="sxs-lookup"><span data-stu-id="abed4-127">The following PowerShell command creates the resource.</span></span>

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

<span data-ttu-id="abed4-128">**New-xDscResource** rutina vytvoří schéma MOF, skript kostru prostředků, strukturu požadované adresáře pro nový prostředek a manifestu pro modul, který zveřejňuje nový prostředek.</span><span class="sxs-lookup"><span data-stu-id="abed4-128">The **New-xDscResource** cmdlet creates the MOF schema, a skeleton resource script, the required directory structure for your new resource, and a manifest for the module that exposes the new resource.</span></span>

<span data-ttu-id="abed4-129">Schéma soubor MOF, který je na **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, a jeho obsah následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="abed4-129">The MOF schema file is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, and its contents are as follows.</span></span>

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

<span data-ttu-id="abed4-130">Je skript prostředků v **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span><span class="sxs-lookup"><span data-stu-id="abed4-130">The resource script is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span></span> <span data-ttu-id="abed4-131">Neobsahuje skutečné logiku pro provádění prostředku, který je nutné přidat sami.</span><span class="sxs-lookup"><span data-stu-id="abed4-131">It does not include the actual logic to implement the resource, which you must add yourself.</span></span> <span data-ttu-id="abed4-132">Obsah kostru skriptu jsou následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="abed4-132">The contents of the skeleton script are as follows.</span></span>

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

## <a name="updating-the-resource"></a><span data-ttu-id="abed4-133">Aktualizuje prostředek</span><span class="sxs-lookup"><span data-stu-id="abed4-133">Updating the resource</span></span>

<span data-ttu-id="abed4-134">Pokud potřebujete přidat nebo upravit seznam parametrů prostředku, můžete zavolat **aktualizace xDscResource** rutiny.</span><span class="sxs-lookup"><span data-stu-id="abed4-134">If you need to add or modify the parameter list of the resource, you can call the **Update-xDscResource** cmdlet.</span></span> <span data-ttu-id="abed4-135">Rutina aktualizuje prostředek nový seznam parametrů.</span><span class="sxs-lookup"><span data-stu-id="abed4-135">The cmdlet updates the resource with a new parameter list.</span></span> <span data-ttu-id="abed4-136">Pokud jste již přidali logiku ve vašem skriptu prostředků, je ponechán beze změny.</span><span class="sxs-lookup"><span data-stu-id="abed4-136">If you have already added logic in your resource script, it is left intact.</span></span>

<span data-ttu-id="abed4-137">Například předpokládejme, že chcete zahrnout poslední protokolu v čase pro uživatele v našem prostředku.</span><span class="sxs-lookup"><span data-stu-id="abed4-137">For example, suppose you want to include the last log in time for the user in our resource.</span></span> <span data-ttu-id="abed4-138">Místo psaní znovu zcela prostředek, můžete volat **New-xDscResourceProperty** k vytvoření nové vlastnosti a pak zavolají **aktualizace xDscResource** a přidejte do vaší nové vlastnosti seznam vlastností.</span><span class="sxs-lookup"><span data-stu-id="abed4-138">Rather than writing the resource again completely, you can call the **New-xDscResourceProperty** to create the new property, and then call **Update-xDscResource** and add your new property to the properties list.</span></span>

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a><span data-ttu-id="abed4-139">Testování schéma prostředků</span><span class="sxs-lookup"><span data-stu-id="abed4-139">Testing a resource schema</span></span>

<span data-ttu-id="abed4-140">Nástroj Návrhář prostředků zpřístupní jeden další rutiny, která můžete použít k testování platnosti schématu MOF, který jste napsali ručně.</span><span class="sxs-lookup"><span data-stu-id="abed4-140">The Resource Designer tool exposes one more cmdlet that can be used to test the validity of a MOF schema that you have written manually.</span></span> <span data-ttu-id="abed4-141">Volání **Test xDscSchema** předávání cestu schéma MOF prostředků jako parametr rutiny.</span><span class="sxs-lookup"><span data-stu-id="abed4-141">Call the **Test-xDscSchema** cmdlet, passing the path of a MOF resource schema as a parameter.</span></span> <span data-ttu-id="abed4-142">Rutina výstup všechny chyby ve schématu.</span><span class="sxs-lookup"><span data-stu-id="abed4-142">The cmdlet will output any errors in the schema.</span></span>

### <a name="see-also"></a><span data-ttu-id="abed4-143">Viz také</span><span class="sxs-lookup"><span data-stu-id="abed4-143">See Also</span></span>

#### <a name="concepts"></a><span data-ttu-id="abed4-144">Koncepty</span><span class="sxs-lookup"><span data-stu-id="abed4-144">Concepts</span></span>
[<span data-ttu-id="abed4-145">Sestavení vlastní Windows PowerShell Desired State Configuration prostředky</span><span class="sxs-lookup"><span data-stu-id="abed4-145">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

#### <a name="other-resources"></a><span data-ttu-id="abed4-146">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="abed4-146">Other Resources</span></span>
[<span data-ttu-id="abed4-147">xDscResourceDesigner modulu</span><span class="sxs-lookup"><span data-stu-id="abed4-147">xDscResourceDesigner Module</span></span>](https://powershellgallery.com/packages/xDscResourceDesigner)
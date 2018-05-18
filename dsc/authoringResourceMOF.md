---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Psaní vlastních prostředků DSC s MOF
ms.openlocfilehash: 50b5f2eddbac4571f5351b32648d45c54ded167e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a><span data-ttu-id="53fef-103">Psaní vlastních prostředků DSC s MOF</span><span class="sxs-lookup"><span data-stu-id="53fef-103">Writing a custom DSC resource with MOF</span></span>

> <span data-ttu-id="53fef-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="53fef-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="53fef-105">V tomto tématu jsme bude definovat schéma pro vlastní prostředek požadovaného stavu aplikace Windows PowerShell (DSC) v souboru MOF a implementovat prostředku v souboru skriptu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53fef-105">In this topic, we will define the schema for a Windows PowerShell Desired State Configuration (DSC) custom resource in a MOF file, and implement the resource in a Windows PowerShell script file.</span></span> <span data-ttu-id="53fef-106">Tento vlastní prostředek je pro vytváření a údržbu webu.</span><span class="sxs-lookup"><span data-stu-id="53fef-106">This custom resource is for creating and maintaining a web site.</span></span>

## <a name="creating-the-mof-schema"></a><span data-ttu-id="53fef-107">Vytvoření schématu MOF</span><span class="sxs-lookup"><span data-stu-id="53fef-107">Creating the MOF schema</span></span>

<span data-ttu-id="53fef-108">Schéma definuje vlastnosti prostředku nakonfigurovaný pomocí skriptu, který konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="53fef-108">The schema defines the properties of your resource that can be configured by a DSC configuration script.</span></span>

### <a name="folder-structure-for-a-mof-resource"></a><span data-ttu-id="53fef-109">Struktura složek pro prostředek MOF</span><span class="sxs-lookup"><span data-stu-id="53fef-109">Folder structure for a MOF resource</span></span>

<span data-ttu-id="53fef-110">Chcete-li implementovat vlastní prostředek DSC se schématem, MOF, vytvořte následující strukturu složek.</span><span class="sxs-lookup"><span data-stu-id="53fef-110">To implement a DSC custom resource with a MOF schema, create the following folder structure.</span></span> <span data-ttu-id="53fef-111">Schéma MOF je definována v souboru Demo_IISWebsite.schema.mof a skriptu prostředků je definována v Demo_IISWebsite.psm1.</span><span class="sxs-lookup"><span data-stu-id="53fef-111">The MOF schema is defined in the file Demo_IISWebsite.schema.mof, and the resource script is defined in Demo_IISWebsite.psm1.</span></span> <span data-ttu-id="53fef-112">Volitelně můžete vytvořit soubor manifestu (psd1) modulu.</span><span class="sxs-lookup"><span data-stu-id="53fef-112">Optionally, you can create a module manifest (psd1) file.</span></span>

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

<span data-ttu-id="53fef-113">Všimněte si, že je potřeba vytvořit složku s názvem DSCResources ve složce nejvyšší úrovně a že složka pro každý prostředek, musí mít stejný název jako prostředek.</span><span class="sxs-lookup"><span data-stu-id="53fef-113">Note that it is necessary to create a folder named DSCResources under the top-level folder, and that the folder for each resource must have the same name as the resource.</span></span>

### <a name="the-contents-of-the-mof-file"></a><span data-ttu-id="53fef-114">Obsah souboru MOF</span><span class="sxs-lookup"><span data-stu-id="53fef-114">The contents of the MOF file</span></span>

<span data-ttu-id="53fef-115">Následuje příklad MOF souboru, který lze použít pro prostředek vlastní web.</span><span class="sxs-lookup"><span data-stu-id="53fef-115">Following is an example MOF file that can be used for a custom website resource.</span></span> <span data-ttu-id="53fef-116">Postup popsaný v tomto příkladu, uložit toto schéma do souboru a volání soubor *Demo_IISWebsite.schema.mof*.</span><span class="sxs-lookup"><span data-stu-id="53fef-116">To follow this example, save this schema to a file, and call the file *Demo_IISWebsite.schema.mof*.</span></span>

```
[ClassVersion("1.0.0"), FriendlyName("Website")]
class Demo_IISWebsite : OMI_BaseResource
{
  [Key] string Name;
  [Required] string PhysicalPath;
  [write,ValueMap{"Present", "Absent"},Values{"Present", "Absent"}] string Ensure;
  [write,ValueMap{"Started","Stopped"},Values{"Started", "Stopped"}] string State;
  [write] string Protocol[];
  [write] string BindingInfo[];
  [write] string ApplicationPool;
  [read] string ID;
};
```

<span data-ttu-id="53fef-117">Vezměte na vědomí následující skutečnosti související předchozí kód:</span><span class="sxs-lookup"><span data-stu-id="53fef-117">Note the following about the previous code:</span></span>

* <span data-ttu-id="53fef-118">`FriendlyName` Definuje název, který slouží k odkazování na tento vlastní prostředek DSC konfigurační skripty.</span><span class="sxs-lookup"><span data-stu-id="53fef-118">`FriendlyName` defines the name you can use to refer to this custom resource in DSC configuration scripts.</span></span> <span data-ttu-id="53fef-119">V tomto příkladu `Website` je ekvivalentní popisný název `Archive` pro předdefinované prostředek archivu.</span><span class="sxs-lookup"><span data-stu-id="53fef-119">In this example, `Website` is equivalent to the friendly name `Archive` for the built-in Archive resource.</span></span>
* <span data-ttu-id="53fef-120">Třída definujete pro vlastní prostředek musí být odvozeny od `OMI_BaseResource`.</span><span class="sxs-lookup"><span data-stu-id="53fef-120">The class you define for your custom resource must derive from `OMI_BaseResource`.</span></span>
* <span data-ttu-id="53fef-121">Kvalifikátor typu `[Key]`na vlastnost značí, že tato vlastnost jednoznačné identifikaci instance prostředku.</span><span class="sxs-lookup"><span data-stu-id="53fef-121">The type qualifier, `[Key]`, on a property indicates that this property will uniquely identify the resource instance.</span></span> <span data-ttu-id="53fef-122">Alespoň jeden `[Key]` vlastnost je povinná.</span><span class="sxs-lookup"><span data-stu-id="53fef-122">At least one `[Key]` property is required.</span></span>
* <span data-ttu-id="53fef-123">`[Required]` Kvalifikátor označuje, že tato vlastnost je vyžadovaná (musí být zadaná hodnota v konfigurační skript, který používá tento prostředek).</span><span class="sxs-lookup"><span data-stu-id="53fef-123">The `[Required]` qualifier indicates that the property is required (a value must be specified in any configuration script that uses this resource).</span></span>
* <span data-ttu-id="53fef-124">`[write]` Kvalifikátor označuje, že tato vlastnost je volitelná, při použití vlastního prostředku v konfigurační skript.</span><span class="sxs-lookup"><span data-stu-id="53fef-124">The `[write]` qualifier indicates that this property is optional when using the custom resource in a configuration script.</span></span> <span data-ttu-id="53fef-125">`[read]` Kvalifikátor označuje, že vlastnost nelze nastavit konfigurace a je pouze pro účely vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="53fef-125">The `[read]` qualifier indicates that a property cannot be set by a configuration, and is for reporting purposes only.</span></span>
* <span data-ttu-id="53fef-126">`Values` omezuje hodnoty, které lze přiřadit k vlastnosti do seznamu hodnot definovaných v `ValueMap`.</span><span class="sxs-lookup"><span data-stu-id="53fef-126">`Values` restricts the values that can be assigned to the property to the list of values defined in `ValueMap`.</span></span> <span data-ttu-id="53fef-127">Další informace najdete v tématu [chybu a hodnota kvalifikátory](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).</span><span class="sxs-lookup"><span data-stu-id="53fef-127">For more information, see [ValueMap and Value Qualifiers](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).</span></span>
* <span data-ttu-id="53fef-128">Včetně vlastnost volá `Ensure` s hodnotami `Present` a `Absent` v prostředku se doporučuje jako způsob, jak udržovat konzistentní styl s integrovanou prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="53fef-128">Including a property called `Ensure` with values `Present` and `Absent` in your resource is recommended as a way to maintain a consistent style with built-in DSC resources.</span></span>
* <span data-ttu-id="53fef-129">Název souboru schématu pro vlastní prostředek následujícím způsobem: `classname.schema.mof`, kde `classname` je identifikátor, který následuje `class` – klíčové slovo v vaší definice schématu.</span><span class="sxs-lookup"><span data-stu-id="53fef-129">Name the schema file for your custom resource as follows: `classname.schema.mof`, where `classname` is the identifier that follows the `class` keyword in your schema definition.</span></span>

### <a name="writing-the-resource-script"></a><span data-ttu-id="53fef-130">Psaní skriptu prostředků</span><span class="sxs-lookup"><span data-stu-id="53fef-130">Writing the resource script</span></span>

<span data-ttu-id="53fef-131">Skript prostředků implementuje logiku prostředku.</span><span class="sxs-lookup"><span data-stu-id="53fef-131">The resource script implements the logic of the resource.</span></span> <span data-ttu-id="53fef-132">V tomto modulu musí obsahovat tři funkce volané **Get-TargetResource**, **Set-TargetResource**, a **Test TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="53fef-132">In this module, you must include three functions called **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource**.</span></span> <span data-ttu-id="53fef-133">Všechny tři funkce vyžaduje sadu parametrů, který je stejný jako sada vlastností, definovaná ve schématu MOF, který jste vytvořili pro prostředek.</span><span class="sxs-lookup"><span data-stu-id="53fef-133">All three functions must take a parameter set that is identical to the set of properties defined in the MOF schema that you created for your resource.</span></span> <span data-ttu-id="53fef-134">V tomto dokumentu tato sada vlastností se označuje jako "vlastností prostředku."</span><span class="sxs-lookup"><span data-stu-id="53fef-134">In this document, this set of properties is referred to as the “resource properties.”</span></span> <span data-ttu-id="53fef-135">Úložiště volá tyto tři funkce v souboru <ResourceName>.psm1.</span><span class="sxs-lookup"><span data-stu-id="53fef-135">Store these three functions in a file called <ResourceName>.psm1.</span></span> <span data-ttu-id="53fef-136">V následujícím příkladu funkce jsou uloženy v souboru s názvem Demo_IISWebsite.psm1.</span><span class="sxs-lookup"><span data-stu-id="53fef-136">In the following example, the functions are stored in a file called Demo_IISWebsite.psm1.</span></span>

> <span data-ttu-id="53fef-137">**Poznámka:**: Když spustíte stejný konfigurační skript na prostředku více než jednou, mělo by se zobrazit žádné chyby a prostředek by měla zůstat v stejného stavu jako jednou spouštění skriptu.</span><span class="sxs-lookup"><span data-stu-id="53fef-137">**Note**: When you run the same configuration script on your resource more than once, you should receive no errors and the resource should remain in the same state as running the script once.</span></span> <span data-ttu-id="53fef-138">K tomu, ujistěte se, že vaše **Get-TargetResource** a **Test TargetResource** funkce nechte beze změny prostředek a že vyvolání **Set-TargetResource**více než jednou v sekvenci s parametrem stejné hodnoty se vždy rovná ho po vyvolání funkce.</span><span class="sxs-lookup"><span data-stu-id="53fef-138">To accomplish this, ensure that your **Get-TargetResource** and **Test-TargetResource** functions leave the resource unchanged, and that invoking the **Set-TargetResource** function more than once in a sequence with the same parameter values is always equivalent to invoking it once.</span></span>

<span data-ttu-id="53fef-139">V **Get-TargetResource** funkce implementace, použijte vlastnost hodnoty klíče prostředků, které jsou k dispozici jako parametry a zkontrolujte stav instance zadaný prostředek.</span><span class="sxs-lookup"><span data-stu-id="53fef-139">In the **Get-TargetResource** function implementation, use the key resource property values that are provided as parameters to check the status of the specified resource instance.</span></span> <span data-ttu-id="53fef-140">Tato funkce musí vracet zatřiďovací tabulka, která jsou uvedeny vlastnosti prostředků jako klíče a skutečné hodnoty těchto vlastností jako odpovídající hodnoty.</span><span class="sxs-lookup"><span data-stu-id="53fef-140">This function must return a hash table that lists all the resource properties as keys and the actual values of these properties as the corresponding values.</span></span> <span data-ttu-id="53fef-141">Následující kód představuje příklad.</span><span class="sxs-lookup"><span data-stu-id="53fef-141">The following code provides an example.</span></span>

```powershell
# DSC uses the Get-TargetResource function to fetch the status of the resource instance specified in the parameters for the target machine
function Get-TargetResource
{
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

        $getTargetResourceResult = $null;

        <# Insert logic that uses the mandatory parameter values to get the website and assign it to a variable called $Website #>
        <# Set $ensureResult to "Present" if the requested website exists and to "Absent" otherwise #>

        # Add all Website properties to the hash table
        # This simple example assumes that $Website is not null
        $getTargetResourceResult = @{
                                      Name = $Website.Name;
                                        Ensure = $ensureResult;
                                        PhysicalPath = $Website.physicalPath;
                                        State = $Website.state;
                                        ID = $Website.id;
                                        ApplicationPool = $Website.applicationPool;
                                        Protocol = $Website.bindings.Collection.protocol;
                                        Binding = $Website.bindings.Collection.bindingInformation;
                                    }

        $getTargetResourceResult;
}
```

<span data-ttu-id="53fef-142">V závislosti na hodnoty, které jsou určené pro vlastnosti prostředku v konfigurační skript **Set-TargetResource** musíte udělat jednu z následujících akcí:</span><span class="sxs-lookup"><span data-stu-id="53fef-142">Depending on the values that are specified for the resource properties in the configuration script, the **Set-TargetResource** must do one of the following:</span></span>

* <span data-ttu-id="53fef-143">Vytvoření nového webu</span><span class="sxs-lookup"><span data-stu-id="53fef-143">Create a new website</span></span>
* <span data-ttu-id="53fef-144">Aktualizovat existující web</span><span class="sxs-lookup"><span data-stu-id="53fef-144">Update an existing website</span></span>
* <span data-ttu-id="53fef-145">Odstraňte existující web</span><span class="sxs-lookup"><span data-stu-id="53fef-145">Delete an existing website</span></span>

<span data-ttu-id="53fef-146">Následující příklad znázorňuje to.</span><span class="sxs-lookup"><span data-stu-id="53fef-146">The following example illustrates this.</span></span>

```powershell
# The Set-TargetResource function is used to create, delete or configure a website on the target machine.
function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

    <# If Ensure is set to "Present" and the website specified in the mandatory input parameters does not exist, then create it using the specified parameter values #>
    <# Else, if Ensure is set to "Present" and the website does exist, then update its properties to match the values provided in the non-mandatory parameter values #>
    <# Else, if Ensure is set to "Absent" and the website does not exist, then do nothing #>
    <# Else, if Ensure is set to "Absent" and the website does exist, then delete the website #>
}
```

<span data-ttu-id="53fef-147">Nakonec **Test TargetResource** funkce vyžaduje parametr stejné nastavení jako **Get-TargetResource** a **Set-TargetResource**.</span><span class="sxs-lookup"><span data-stu-id="53fef-147">Finally, the **Test-TargetResource** function must take the same parameter set as **Get-TargetResource** and **Set-TargetResource**.</span></span> <span data-ttu-id="53fef-148">V implementaci **Test TargetResource**, zkontrolujte stav instance prostředku, který je uveden v parametrech klíče.</span><span class="sxs-lookup"><span data-stu-id="53fef-148">In your implementation of **Test-TargetResource**, check the status of the resource instance that is specified in the key parameters.</span></span> <span data-ttu-id="53fef-149">Pokud skutečný stav instance prostředku neodpovídá hodnot zadaných v sadě parametrů, vrátí **$false**.</span><span class="sxs-lookup"><span data-stu-id="53fef-149">If the actual status of the resource instance does not match the values specified in the parameter set, return **$false**.</span></span> <span data-ttu-id="53fef-150">V opačném vraťte **$true**.</span><span class="sxs-lookup"><span data-stu-id="53fef-150">Otherwise, return **$true**.</span></span>

<span data-ttu-id="53fef-151">Následující kód implementuje **Test TargetResource** funkce.</span><span class="sxs-lookup"><span data-stu-id="53fef-151">The following code implements the **Test-TargetResource** function.</span></span>

```powershell
function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[parameter(Mandatory = $true)]
[System.String]
$Name,

[parameter(Mandatory = $true)]
[System.String]
$PhysicalPath,

[ValidateSet("Started","Stopped")]
[System.String]
$State,

[System.String[]]
$Protocol,

[System.String[]]
$BindingData,

[System.String]
$ApplicationPool
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


#Include logic to
$result = [System.Boolean]
#Add logic to test whether the website is present and its status mathes the supplied parameter values. If it does, return true. If it does not, return false.
$result
}
```

<span data-ttu-id="53fef-152">**Poznámka:**: pro snazší ladění, použijte **Write-Verbose** rutiny v implementaci předchozí tři funkce.</span><span class="sxs-lookup"><span data-stu-id="53fef-152">**Note**: For easier debugging, use the **Write-Verbose** cmdlet in your implementation of the previous three functions.</span></span>
><span data-ttu-id="53fef-153">Tato rutina zapíše text do proudu podrobnou zprávu.</span><span class="sxs-lookup"><span data-stu-id="53fef-153">This cmdlet writes text to the verbose message stream.</span></span>
><span data-ttu-id="53fef-154">Ve výchozím nastavení, se nezobrazí datový proud podrobné zprávy, ale můžete ji zobrazit tak, že změníte hodnotu **$VerbosePreference** proměnné nebo pomocí **podrobné** parametr rutiny DSC = nový.</span><span class="sxs-lookup"><span data-stu-id="53fef-154">By default, the verbose message stream is not displayed, but you can display it by changing the value of the **$VerbosePreference** variable or by using the **Verbose** parameter in the DSC cmdlets = new.</span></span>

### <a name="creating-the-module-manifest"></a><span data-ttu-id="53fef-155">Vytvoření manifestu modulu</span><span class="sxs-lookup"><span data-stu-id="53fef-155">Creating the module manifest</span></span>

<span data-ttu-id="53fef-156">Nakonec použijte **New-ModuleManifest** rutiny k definování <ResourceName>.psd1 soubor pro vaše vlastní prostředek modul.</span><span class="sxs-lookup"><span data-stu-id="53fef-156">Finally, use the **New-ModuleManifest** cmdlet to define a <ResourceName>.psd1 file for your custom resource module.</span></span> <span data-ttu-id="53fef-157">Při vyvolání této rutiny, odkazovat na soubor skriptu (.psm1) modul popsané v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="53fef-157">When you invoke this cmdlet, reference the script module (.psm1) file described in the previous section.</span></span> <span data-ttu-id="53fef-158">Zahrnout **Get-TargetResource**, **Set-TargetResource**, a **Test TargetResource** v seznamu funkcí pro export.</span><span class="sxs-lookup"><span data-stu-id="53fef-158">Include **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** in the list of functions to export.</span></span> <span data-ttu-id="53fef-159">Následuje příklad souboru manifestu.</span><span class="sxs-lookup"><span data-stu-id="53fef-159">Following is an example manifest file.</span></span>

```powershell
# Module manifest for module 'Demo.IIS.Website'
#
# Generated on: 1/10/2013
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '6AB5ED33-E923-41d8-A3A4-5ADDA2B301DE'

# Author of this module
Author = 'Contoso'

# Company or vendor of this module
CompanyName = 'Contoso'

# Copyright statement for this module
Copyright = 'Contoso. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This Module is used to support the creation and configuration of IIS Websites through Get, Set and Test API on the DSC managed nodes.'

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '4.0'

# Minimum version of the common language runtime (CLR) required by this module
CLRVersion = '4.0'

# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @("WebAdministration")

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @("Demo_IISWebsite.psm1")

# Functions to export from this module
FunctionsToExport = @("Get-TargetResource", "Set-TargetResource", "Test-TargetResource")

# Cmdlets to export from this module
#CmdletsToExport = '*'

# HelpInfo URI of this module
# HelpInfoURI = ''
}
```

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="53fef-160">Podpora PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="53fef-160">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="53fef-161">**Poznámka:** **PsDscRunAsCredential** je podporována v prostředí PowerShell 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="53fef-161">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="53fef-162">**PsDscRunAsCredential** vlastnost lze použít v [konfigurace DSC](configurations.md) prostředků bloku určí prostředek by měl být spuštění pod zadanou sadu přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="53fef-162">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="53fef-163">Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="53fef-163">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

<span data-ttu-id="53fef-164">Pro přístup k kontext uživatele z v rámci vlastní prostředek, můžete použít automatické proměnné `$PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="53fef-164">To access the user context from within a custom resource, you can use the automatic variable `$PsDscContext`.</span></span>

<span data-ttu-id="53fef-165">Například následující kód zapíše kontextu uživatele, pod kterým běží prostředku do datového proudu podrobný výstup:</span><span class="sxs-lookup"><span data-stu-id="53fef-165">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```
---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředky DSC
ms.openlocfilehash: 1f77b5e6630a2e3de6e1d1a05638f94d2df039ae
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046687"
---
# <a name="dsc-resources"></a><span data-ttu-id="936e0-103">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="936e0-103">DSC Resources</span></span>

><span data-ttu-id="936e0-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="936e0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="936e0-105">Desired State Configuration (DSC) prostředky poskytují stavební bloky pro konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="936e0-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="936e0-106">Prostředek zveřejňuje vlastnosti, které může být nakonfigurovaný (schéma) a obsahuje funkce skript Powershellu, která volá místní Configuration Manageru (LCM) aby ",".</span><span class="sxs-lookup"><span data-stu-id="936e0-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="936e0-107">Zdroj lze modelovat něco jako obecné jako soubor, nebo co nastavení serveru služby IIS.</span><span class="sxs-lookup"><span data-stu-id="936e0-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="936e0-108">Skupiny jako prostředky jsou zkombinované v modulu DSC, která slouží k uspořádání všechny požadované soubory v strukturu, která je přenosná a zahrnuje jejich metadata k určení, jak jsou prostředky určena pro použití.</span><span class="sxs-lookup"><span data-stu-id="936e0-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>

<span data-ttu-id="936e0-109">Každý prostředek má \* schéma, které určuje nutné k využití prostředků v syntaxi [konfigurace](../configurations/configurations.md).</span><span class="sxs-lookup"><span data-stu-id="936e0-109">Each resource has a \*schema that determines the syntax needed to use the resource in a [Configuration](../configurations/configurations.md).</span></span> <span data-ttu-id="936e0-110">Schéma zdroje lze definovat takto:</span><span class="sxs-lookup"><span data-stu-id="936e0-110">A resource's schema can be defined in the following ways:</span></span>

- <span data-ttu-id="936e0-111">**"Schema.Mof"** souboru: Definujte většinu prostředků jejich *schématu* v "schema.mof soubor, pomocí [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).</span><span class="sxs-lookup"><span data-stu-id="936e0-111">**'Schema.Mof'** file: Most resources define their *schema* in a 'schema.mof' file, using [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).</span></span>
- <span data-ttu-id="936e0-112">**"\<Název prostředku\>. schema.psm1"** souboru: [Složené prostředky](../configurations/compositeConfigs.md) definovat jejich *schématu* v "<ResourceName>. schema.psm1" soubor pomocí [bloku parametrů](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).</span><span class="sxs-lookup"><span data-stu-id="936e0-112">**'\<Resource Name\>.schema.psm1'** file: [Composite Resources](../configurations/compositeConfigs.md) define their *schema* in a '<ResourceName>.schema.psm1' file using a [Parameter Block](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).</span></span>
- <span data-ttu-id="936e0-113">**"\<Název prostředku\>.psm1"** souboru: Třídy založené na prostředky DSC definovat jejich *schématu* v definici třídy.</span><span class="sxs-lookup"><span data-stu-id="936e0-113">**'\<Resource Name\>.psm1'** file: Class based DSC resources define their *schema* in the class definition.</span></span> <span data-ttu-id="936e0-114">Syntaxe položky jsou označené jako vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="936e0-114">Syntax items are denoted as Class properties.</span></span> <span data-ttu-id="936e0-115">Další informace najdete v tématu [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).</span><span class="sxs-lookup"><span data-stu-id="936e0-115">For more information, see [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).</span></span>

<span data-ttu-id="936e0-116">Pokud chcete načíst syntaxe pro prostředek DSC, použijte [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) rutinu s `-Syntax` parametru.</span><span class="sxs-lookup"><span data-stu-id="936e0-116">To retrieve the syntax for a DSC resource, use the [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet with the `-Syntax` parameter.</span></span> <span data-ttu-id="936e0-117">Toto použití je podobný používání [Get-Command](/powershell/module/microsoft.powershell.core/get-command) s `-Syntax` parametr zobrazíte Syntaxe rutin.</span><span class="sxs-lookup"><span data-stu-id="936e0-117">This usage is similar to using [Get-Command](/powershell/module/microsoft.powershell.core/get-command) with the `-Syntax` parameter to get cmdlet syntax.</span></span> <span data-ttu-id="936e0-118">Šablona použitá pro blok prostředků pro prostředek, který zadáte se zobrazí výstup, který se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="936e0-118">The output you see will show the template used for a resource block for the resource you specify.</span></span>

```powershell
Get-DscResource -Syntax Service
```

<span data-ttu-id="936e0-119">Který se zobrazí výstup by měl vypadat přibližně ve výstupu níže, i když tento prostředek syntaxe může v budoucnu změnit.</span><span class="sxs-lookup"><span data-stu-id="936e0-119">The output you see should be similar to the output below, though this resource's syntax could change in the future.</span></span> <span data-ttu-id="936e0-120">Syntaxe rutin, jako jsou *klíče* viděli v hranatých závorkách jsou volitelné.</span><span class="sxs-lookup"><span data-stu-id="936e0-120">Like cmdlet syntax, the *keys* seen in square brackets, are optional.</span></span> <span data-ttu-id="936e0-121">Typy určete typ dat, který očekává, že každý klíč.</span><span class="sxs-lookup"><span data-stu-id="936e0-121">The types specify the type of data each key expects.</span></span>

> [!NOTE]
> <span data-ttu-id="936e0-122">**Ujistěte se, že** klíč je volitelný, protože výchozí hodnota "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="936e0-122">The **Ensure** key is optional because it defaults to "Present".</span></span>

```output
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

<span data-ttu-id="936e0-123">V konfiguraci **služby** prostředků bloku může vypadat třeba takto k **Ujistěte se, že** , na kterém běží služba zařazování tisku.</span><span class="sxs-lookup"><span data-stu-id="936e0-123">Inside a Configuration, a **Service** resource block might look like this to **Ensure** that the Spooler service is running.</span></span>

> [!NOTE]
> <span data-ttu-id="936e0-124">Před použitím zdroje v konfiguraci, je nutné naimportovat pomocí [Import-DSCResource](../configurations/import-dscresource.md).</span><span class="sxs-lookup"><span data-stu-id="936e0-124">Before using a resource in a Configuration, you must import it using [Import-DSCResource](../configurations/import-dscresource.md).</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }
    }
}
```

<span data-ttu-id="936e0-125">Konfigurace může obsahovat více instancí stejného typu prostředku.</span><span class="sxs-lookup"><span data-stu-id="936e0-125">Configurations can contain multiple instances of the same resource type.</span></span> <span data-ttu-id="936e0-126">Každá instance musí mít jedinečné názvy.</span><span class="sxs-lookup"><span data-stu-id="936e0-126">Each instance must be uniquely named.</span></span> <span data-ttu-id="936e0-127">V následujícím příkladu druhý **služby** prostředků bloku se přidá do konfigurace služby "DHCP".</span><span class="sxs-lookup"><span data-stu-id="936e0-127">In the following example, a second **Service** resource block is added to configure the "DHCP" service.</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }

        # To configure a second service resource block, add another Service resource block and use a unique name.
        Service "DHCP:Running"
        {
            Name = "DHCP"
            State = "Running"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="936e0-128">Od v Powershellu 5.0, byl přidán technologie intellisense pro DSC.</span><span class="sxs-lookup"><span data-stu-id="936e0-128">Beginning in PowerShell 5.0, intellisense was added for DSC.</span></span> <span data-ttu-id="936e0-129">Tato nová funkce umožňuje používat \<kartu\> a \<kombinace kláves Ctrl + mezerník\> pro automatické dokončování názvů klíčů.</span><span class="sxs-lookup"><span data-stu-id="936e0-129">This new feature allows you to use \<TAB\> and \<Ctrl+Space\> to auto-complete key names.</span></span>

![Prostředek Tab k dokončování příkazů](../media/resource-tabcompletion.png)

## <a name="built-in-resources"></a><span data-ttu-id="936e0-131">Integrované prostředky</span><span class="sxs-lookup"><span data-stu-id="936e0-131">Built-in resources</span></span>

<span data-ttu-id="936e0-132">Kromě komunitní zdroje jsou integrované prostředky pro Windows, prostředky pro Linux a prostředky pro závislost mezi uzly.</span><span class="sxs-lookup"><span data-stu-id="936e0-132">In addition to community resources, there are built-in resources for Windows, resources for Linux, and resources for cross-node dependency.</span></span> <span data-ttu-id="936e0-133">Výše uvedené kroky můžete použít k určení syntaxe těchto prostředků a jejich použití.</span><span class="sxs-lookup"><span data-stu-id="936e0-133">You can use the steps above to determine the syntax of these resources and how to use them.</span></span> <span data-ttu-id="936e0-134">Na stránkách, které slouží tyto prostředky byly archivovány v rámci **odkaz**.</span><span class="sxs-lookup"><span data-stu-id="936e0-134">The pages that serve these resources have been archived under **Reference**.</span></span>

<span data-ttu-id="936e0-135">Integrované prostředky pro Windows</span><span class="sxs-lookup"><span data-stu-id="936e0-135">Windows built-in resources</span></span>

* [<span data-ttu-id="936e0-136">Prostředek Archive</span><span class="sxs-lookup"><span data-stu-id="936e0-136">Archive Resource</span></span>](../reference/resources/windows/archiveResource.md)
* [<span data-ttu-id="936e0-137">Prostředek Environment</span><span class="sxs-lookup"><span data-stu-id="936e0-137">Environment Resource</span></span>](../reference/resources/windows/environmentResource.md)
* [<span data-ttu-id="936e0-138">Prostředek File</span><span class="sxs-lookup"><span data-stu-id="936e0-138">File Resource</span></span>](../reference/resources/windows/fileResource.md)
* [<span data-ttu-id="936e0-139">Prostředek Group</span><span class="sxs-lookup"><span data-stu-id="936e0-139">Group Resource</span></span>](../reference/resources/windows/groupResource.md)
* [<span data-ttu-id="936e0-140">Prostředek GroupSet</span><span class="sxs-lookup"><span data-stu-id="936e0-140">GroupSet Resource</span></span>](../reference/resources/windows/groupSetResource.md)
* [<span data-ttu-id="936e0-141">Prostředek Log</span><span class="sxs-lookup"><span data-stu-id="936e0-141">Log Resource</span></span>](../reference/resources/windows/logResource.md)
* [<span data-ttu-id="936e0-142">Prostředek Package</span><span class="sxs-lookup"><span data-stu-id="936e0-142">Package Resource</span></span>](../reference/resources/windows/packageResource.md)
* [<span data-ttu-id="936e0-143">Prostředek ProcessSet</span><span class="sxs-lookup"><span data-stu-id="936e0-143">ProcessSet Resource</span></span>](../reference/resources/windows/ProcessSetResource.md)
* [<span data-ttu-id="936e0-144">Prostředek Registry</span><span class="sxs-lookup"><span data-stu-id="936e0-144">Registry Resource</span></span>](../reference/resources/windows/registryResource.md)
* [<span data-ttu-id="936e0-145">Prostředek Script</span><span class="sxs-lookup"><span data-stu-id="936e0-145">Script Resource</span></span>](../reference/resources/windows/scriptResource.md)
* [<span data-ttu-id="936e0-146">Prostředek Service</span><span class="sxs-lookup"><span data-stu-id="936e0-146">Service Resource</span></span>](../reference/resources/windows/serviceResource.md)
* [<span data-ttu-id="936e0-147">Prostředek ServiceSet</span><span class="sxs-lookup"><span data-stu-id="936e0-147">ServiceSet Resource</span></span>](../reference/resources/windows/serviceSetResource.md)
* [<span data-ttu-id="936e0-148">Prostředek User</span><span class="sxs-lookup"><span data-stu-id="936e0-148">User Resource</span></span>](../reference/resources/windows/userResource.md)
* [<span data-ttu-id="936e0-149">Prostředek WindowsFeature</span><span class="sxs-lookup"><span data-stu-id="936e0-149">WindowsFeature Resource</span></span>](../reference/resources/windows/windowsFeatureResource.md)
* [<span data-ttu-id="936e0-150">Prostředek WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="936e0-150">WindowsFeatureSet Resource</span></span>](../reference/resources/windows/windowsFeatureSetResource.md)
* [<span data-ttu-id="936e0-151">Prostředek WindowsOptionalFeature</span><span class="sxs-lookup"><span data-stu-id="936e0-151">WindowsOptionalFeature Resource</span></span>](../reference/resources/windows/windowsOptionalFeatureResource.md)
* [<span data-ttu-id="936e0-152">Prostředek WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="936e0-152">WindowsOptionalFeatureSet Resource</span></span>](../reference/resources/windows/windowsOptionalFeatureSetResource.md)
* [<span data-ttu-id="936e0-153">WindowsPackageCabResource prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-153">WindowsPackageCabResource Resource</span></span>](../reference/resources/windows/windowsPackageCabResource.md)
* [<span data-ttu-id="936e0-154">Prostředek WindowsProcess</span><span class="sxs-lookup"><span data-stu-id="936e0-154">WindowsProcess Resource</span></span>](../reference/resources/windows/windowsProcessResource.md)

<span data-ttu-id="936e0-155">[Závislost mezi uzly](../configurations/crossNodeDependencies.md) prostředky</span><span class="sxs-lookup"><span data-stu-id="936e0-155">[Cross-Node dependency](../configurations/crossNodeDependencies.md) resources</span></span>

* [<span data-ttu-id="936e0-156">WaitForAll prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-156">WaitForAll Resource</span></span>](../reference/resources/windows/waitForAllResource.md)
* [<span data-ttu-id="936e0-157">WaitForSome prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-157">WaitForSome Resource</span></span>](../reference/resources/windows/waitForSomeResource.md)
* [<span data-ttu-id="936e0-158">WaitForAny prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-158">WaitForAny Resource</span></span>](../reference/resources/windows/waitForAnyResource.md)

<span data-ttu-id="936e0-159">Balíček správy prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-159">Package Management resources</span></span>

* [<span data-ttu-id="936e0-160">PackageManagement prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-160">PackageManagement Resource</span></span>](../reference/resources/packagemanagement/PackageManagementDscResource.md)
* [<span data-ttu-id="936e0-161">PackageManagementSource prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-161">PackageManagementSource Resource</span></span>](../reference/resources/packagemanagement/PackageManagementSourceDscResource.md)

<span data-ttu-id="936e0-162">Prostředky pro Linux</span><span class="sxs-lookup"><span data-stu-id="936e0-162">Linux resources</span></span>

* [<span data-ttu-id="936e0-163">Prostředek Linux Archive</span><span class="sxs-lookup"><span data-stu-id="936e0-163">Linux Archive Resource</span></span>](../reference/resources/linux/lnxArchiveResource.md)
* [<span data-ttu-id="936e0-164">Zdroje prostředí Linux</span><span class="sxs-lookup"><span data-stu-id="936e0-164">Linux Environment Resource</span></span>](../reference/resources/linux/lnxEnvironmentResource.md)
* [<span data-ttu-id="936e0-165">Linux FileLine prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-165">Linux FileLine Resource</span></span>](../reference/resources/linux/lnxFileLineResource.md)
* [<span data-ttu-id="936e0-166">Linuxový soubor prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-166">Linux File Resource</span></span>](../reference/resources/linux/lnxFileResource.md)
* [<span data-ttu-id="936e0-167">Linuxové skupiny prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-167">Linux Group Resource</span></span>](../reference/resources/linux/lnxGroupResource.md)
* [<span data-ttu-id="936e0-168">Prostředek Linux Package</span><span class="sxs-lookup"><span data-stu-id="936e0-168">Linux Package Resource</span></span>](../reference/resources/linux/lnxPackageResource.md)
* [<span data-ttu-id="936e0-169">Prostředek Linux Script</span><span class="sxs-lookup"><span data-stu-id="936e0-169">Linux Script Resource</span></span>](../reference/resources/linux/lnxScriptResource.md)
* [<span data-ttu-id="936e0-170">Prostředek služby Linux</span><span class="sxs-lookup"><span data-stu-id="936e0-170">Linux Service Resource</span></span>](../reference/resources/linux/lnxServiceResource.md)
* [<span data-ttu-id="936e0-171">Linux SshAuthorizedKeys prostředků</span><span class="sxs-lookup"><span data-stu-id="936e0-171">Linux SshAuthorizedKeys Resource</span></span>](../reference/resources/linux/lnxSshAuthorizedKeysResource.md)
* [<span data-ttu-id="936e0-172">Prostředek uživatele Linuxu</span><span class="sxs-lookup"><span data-stu-id="936e0-172">Linux User Resource</span></span>](../reference/resources/linux/lnxUserResource.md)

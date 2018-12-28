---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Pomocí Import-DSCResource
ms.openlocfilehash: 6bc3c1aa1d34a05e3188666da825322235c0672e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403779"
---
# <a name="using-import-dscresource"></a><span data-ttu-id="19b08-103">Pomocí Import-DSCResource</span><span class="sxs-lookup"><span data-stu-id="19b08-103">Using Import-DSCResource</span></span>

<span data-ttu-id="19b08-104">`Import-DScResource` je dynamické klíčové slovo, které jde použít jenom uvnitř bloku skriptu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="19b08-104">`Import-DScResource` is a dynamic keyword, which can only be used inside a Configuration script block.</span></span> <span data-ttu-id="19b08-105">`Import-DSCResource` – Klíčové slovo import všechny prostředky potřebné v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="19b08-105">The `Import-DSCResource` keyword to import any resources needed in your Configuration.</span></span> <span data-ttu-id="19b08-106">Prostředky v rámci `$phsome` jsou importovány automaticky, ale přesto považuje osvědčeným postupem je explicitně importují všechny prostředky používané v vaše [konfigurace](Configurations.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-106">Resources under `$phsome` are imported automatically, but it is still considered best practice to explicitly import all resources used in your [Configuration](Configurations.md).</span></span>

<span data-ttu-id="19b08-107">Syntaxe pro `Import-DSCResource` je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="19b08-107">The syntax for `Import-DSCResource` is shown below.</span></span>

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>]
```

|<span data-ttu-id="19b08-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="19b08-108">Parameter</span></span>  |<span data-ttu-id="19b08-109">Popis</span><span class="sxs-lookup"><span data-stu-id="19b08-109">Description</span></span>  |
|---------|---------|
|`-Name`|<span data-ttu-id="19b08-110">Názvy prostředků DSC, která je nutné naimportovat.</span><span class="sxs-lookup"><span data-stu-id="19b08-110">The DSC resource name(s) that you must import.</span></span> <span data-ttu-id="19b08-111">Pokud není zadán název modulu, tento příkaz vyhledá pro tyto prostředky DSC v rámci tohoto modulu; v opačném případě příkaz vyhledá prostředky DSC v všechny cesty prostředku DSC.</span><span class="sxs-lookup"><span data-stu-id="19b08-111">If the module name is specified, the command searches for these DSC resources within this module; otherwise the command searches the DSC resources in all DSC resource paths.</span></span> <span data-ttu-id="19b08-112">Jsou podporovány zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="19b08-112">Wildcards are supported.</span></span>|
|`-ModuleName`|<span data-ttu-id="19b08-113">Názvy kontejnerů modulu nebo modul byly.</span><span class="sxs-lookup"><span data-stu-id="19b08-113">The container module name(s), or module specification(s).</span></span>  <span data-ttu-id="19b08-114">Pokud chcete zadat prostředky pro import z modulu, příkaz se pokusí importovat pouze tyto prostředky.</span><span class="sxs-lookup"><span data-stu-id="19b08-114">If you specify resources to import from a module, the command will try to import only those resources.</span></span> <span data-ttu-id="19b08-115">Pokud zadáte pouze modulu, tento příkaz importuje všechny prostředky DSC v modulu.</span><span class="sxs-lookup"><span data-stu-id="19b08-115">If you specify the module only, the command imports all the DSC resources in the module.</span></span>|

<span data-ttu-id="19b08-116">Můžete použít zástupné znaky `-Name` parametr při použití `Import-DSCResource`.</span><span class="sxs-lookup"><span data-stu-id="19b08-116">You can use wildcards with the `-Name` parameter when using `Import-DSCResource`.</span></span>

```powershell
Import-DscResource -Name * -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a><span data-ttu-id="19b08-117">Příklad: Použití Import-DSCResource v rámci konfigurace</span><span class="sxs-lookup"><span data-stu-id="19b08-117">Example: Use Import-DSCResource within a configuration</span></span>

```powershell
Configuration MSDSCConfiguration
{
    # Search for and imports Service, File, and Registry from the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName MS_DSC1 -name Service, File, Registry

    # Search for and import Resource1 from the module that defines it.
    # If only –Name parameter is used then resources can belong to different PowerShell modules as well.
    # TimeZone resource is from the ComputerManagementDSC module which is not installed by default.
    Import-DSCResource -Name File, TimeZone

    # Search for and import all DSC resources inside the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration
...
```

> [!NOTE]
> <span data-ttu-id="19b08-118">Zadání více hodnot pro názvy prostředků a moduly ve stejném příkazu se nepodporují.</span><span class="sxs-lookup"><span data-stu-id="19b08-118">Specifying multiple values for Resource names and modules names in same command are not supported.</span></span> <span data-ttu-id="19b08-119">Může mít nedeterministické chování, o který prostředek se má načíst z modulu, který v případě, že stejný prostředek existuje v několika modulů.</span><span class="sxs-lookup"><span data-stu-id="19b08-119">It can have non-deterministic behavior about which resource to load from which module in case same resource exists in multiple modules.</span></span> <span data-ttu-id="19b08-120">Následující příkaz způsobí chyby během kompilace.</span><span class="sxs-lookup"><span data-stu-id="19b08-120">Below command will result in error during compilation.</span></span>
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

<span data-ttu-id="19b08-121">Co je třeba zvážit při použití pouze název parametru:</span><span class="sxs-lookup"><span data-stu-id="19b08-121">Things to consider when using only the Name parameter:</span></span>

- <span data-ttu-id="19b08-122">Je náročná operace v závislosti na počet modulů na počítači nainstalovaný.</span><span class="sxs-lookup"><span data-stu-id="19b08-122">It is a resource-intensive operation depending on the number of modules installed on machine.</span></span>
- <span data-ttu-id="19b08-123">Načte první prostředek nenašel se zadaným názvem.</span><span class="sxs-lookup"><span data-stu-id="19b08-123">It will load the first resource found with the given name.</span></span> <span data-ttu-id="19b08-124">V případě níž se nachází více než jeden prostředek se stejným názvem nainstalovaná, může načtení nesprávné prostředků.</span><span class="sxs-lookup"><span data-stu-id="19b08-124">In the case where there is more than one resource with same name installed, it could load the wrong resource.</span></span>

<span data-ttu-id="19b08-125">Doporučuje se určit `–ModuleName` s `-Name` parametru, jak je popsáno níže.</span><span class="sxs-lookup"><span data-stu-id="19b08-125">The recommended usage is to specify `–ModuleName` with the `-Name` parameter, as described below.</span></span>

<span data-ttu-id="19b08-126">Toto použití má následující výhody:</span><span class="sxs-lookup"><span data-stu-id="19b08-126">This usage has the following benefits:</span></span>

- <span data-ttu-id="19b08-127">Snižuje dopad na výkon tím, že omezíte rozsah vyhledávání pro zadaný prostředek.</span><span class="sxs-lookup"><span data-stu-id="19b08-127">It reduces the performance impact by limiting the search scope for the specified resource.</span></span>
- <span data-ttu-id="19b08-128">Definuje explicitně modulu definice prostředků, zajistit, že je načten správný zdroj.</span><span class="sxs-lookup"><span data-stu-id="19b08-128">It explicitly defines the module defining the resource, ensuring the correct resource is loaded.</span></span>

> [!NOTE]
> <span data-ttu-id="19b08-129">V Powershellu 5.0 prostředky DSC můžete mít více verzí a verzí lze nainstalovat počítač-souběžně.</span><span class="sxs-lookup"><span data-stu-id="19b08-129">In PowerShell 5.0, DSC resources can have multiple versions, and versions can be installed on a computer side-by-side.</span></span> <span data-ttu-id="19b08-130">Toto je implementováno s více verzí modulu prostředků, které jsou obsaženy ve stejné složce modulu.</span><span class="sxs-lookup"><span data-stu-id="19b08-130">This is implemented by having multiple versions of a resource module that are contained in the same module folder.</span></span>
> <span data-ttu-id="19b08-131">Další informace najdete v tématu [pomocí různých verzí prostředků](sxsresource.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-131">For more information, see [Using resources with multiple versions](sxsresource.md).</span></span>

## <a name="intellisense-with-import-dscresource"></a><span data-ttu-id="19b08-132">Technologie IntelliSense s Import-DSCResource</span><span class="sxs-lookup"><span data-stu-id="19b08-132">Intellisense with Import-DSCResource</span></span>

<span data-ttu-id="19b08-133">Při vytváření konfigurace DSC v prostředí ISE Powershellu zajišťující IntelliSence prostředků a vlastnosti prostředků.</span><span class="sxs-lookup"><span data-stu-id="19b08-133">When authoring the DSC configuration in ISE, PowerShell provides IntelliSence for resources and resource properties.</span></span> <span data-ttu-id="19b08-134">Definice prostředků v rámci `$pshome` cesta modulu jsou načteny automaticky.</span><span class="sxs-lookup"><span data-stu-id="19b08-134">Resource definitions under the `$pshome` module path are loaded automatically.</span></span> <span data-ttu-id="19b08-135">Při importu prostředků pomocí `Import-DSCResource` – klíčové slovo, se přidají definice zadaný prostředek a technologie Intellisense je rozbalený se zahrnout schéma importovaných zdrojů.</span><span class="sxs-lookup"><span data-stu-id="19b08-135">When you import resources using the `Import-DSCResource` keyword, the specified resource definitions are added and Intellisense is expanded to include the imported resource's schema.</span></span>

![Technologie Intellisense prostředků](/media/resource-intellisense.png)

> [!NOTE]
> <span data-ttu-id="19b08-137">Od v Powershellu 5.0, tab k dokončování příkazů byl přidán do ISE pro prostředky DSC a jejich vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="19b08-137">Beginning in PowerShell 5.0, tab completion was added to the ISE for DSC resources and their properties.</span></span> <span data-ttu-id="19b08-138">Další informace najdete v tématu [prostředky](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-138">For more information, see [Resources](../resources/resources.md).</span></span>

<span data-ttu-id="19b08-139">Při kompilaci konfigurace Powershellu definice importovaných zdrojů používá k ověření všechny bloky prostředků v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="19b08-139">When compiling the Configuration, PowerShell uses the imported resource definitions to validate all resource blocks in the configuration.</span></span>
<span data-ttu-id="19b08-140">Každý blok prostředků se ověří pomocí prostředku schématu definice pro následující pravidla.</span><span class="sxs-lookup"><span data-stu-id="19b08-140">Each resource block is validated, using the resource's schema definition, for the following rules.</span></span>

- <span data-ttu-id="19b08-141">Pouze vlastnosti definované ve schématu se používají.</span><span class="sxs-lookup"><span data-stu-id="19b08-141">Only properties defined in schema are used.</span></span>
- <span data-ttu-id="19b08-142">Datové typy pro každou vlastnost jsou správné.</span><span class="sxs-lookup"><span data-stu-id="19b08-142">The data types for each property are correct.</span></span>
- <span data-ttu-id="19b08-143">Nejsou zadány vlastnosti klíče.</span><span class="sxs-lookup"><span data-stu-id="19b08-143">Keys properties are specified.</span></span>
- <span data-ttu-id="19b08-144">Žádná vlastnost jen pro čtení se používá.</span><span class="sxs-lookup"><span data-stu-id="19b08-144">No read-only property is used.</span></span>
- <span data-ttu-id="19b08-145">Ověřování na hodnotě mapuje typy.</span><span class="sxs-lookup"><span data-stu-id="19b08-145">Validation on value maps types.</span></span>

<span data-ttu-id="19b08-146">Vezměte v úvahu následující konfiguraci:</span><span class="sxs-lookup"><span data-stu-id="19b08-146">Consider the following configuration:</span></span>

```powershell
Configuration SchemaValidationInCorrectEnumValue
{
    # It is best practice to explicitly import all resources used in your Configuration.
    # This includes resources that are imported automatically, like WindowsFeature.
    Import-DSCResource -Name WindowsFeature
    Node localhost
    {
        WindowsFeature ROLE1
        {
            Name = “Telnet-Client”
            Ensure = “Invalid”
        }
    }
}
```

<span data-ttu-id="19b08-147">Tato konfigurace způsobí chybu kompilace.</span><span class="sxs-lookup"><span data-stu-id="19b08-147">Compiling this Configuration results in an error.</span></span>

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

<span data-ttu-id="19b08-148">Technologie IntelliSense a schéma ověřování umožňuje zachytit další chyby při analýze a kompilaci zabránit komplikacím v době běhu.</span><span class="sxs-lookup"><span data-stu-id="19b08-148">Intellisense and schema validation allow you to catch more errors during parse and compilation time, avoiding complications at run time.</span></span>

> [!NOTE]
> <span data-ttu-id="19b08-149">Jednotlivé prostředky DSC můžete mít název a **FriendlyName** definovaná pomocí schématu prostředku.</span><span class="sxs-lookup"><span data-stu-id="19b08-149">Each DSC resource can have a name, and a **FriendlyName** defined by the resource's schema.</span></span> <span data-ttu-id="19b08-150">Níže jsou první dva řádky "MSFT_ServiceResource.shema.mof".</span><span class="sxs-lookup"><span data-stu-id="19b08-150">Below are the first two lines of "MSFT_ServiceResource.shema.mof".</span></span>
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> <span data-ttu-id="19b08-151">Při použití tohoto prostředku v konfiguraci, můžete zadat **MSFT_ServiceResource** nebo **služby**.</span><span class="sxs-lookup"><span data-stu-id="19b08-151">When using this resource in a Configuration, you can specify **MSFT_ServiceResource** or **Service**.</span></span>

## <a name="powershell-v4-and-v5-differences"></a><span data-ttu-id="19b08-152">Rozdíly v4, tak i v5 prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="19b08-152">PowerShell v4 and v5 differences</span></span>

<span data-ttu-id="19b08-153">Existuje několik rozdílů, které se zobrazí při vytváření konfigurace v Powershellu 4.0 vs. PowerShell 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="19b08-153">There are multiple differences you see when authoring Configurations in PowerShell 4.0 vs. PowerShell 5.0 and later.</span></span> <span data-ttu-id="19b08-154">V této části budou zvýrazněny rozdíly, že se zobrazí relevantní k tomuto článku.</span><span class="sxs-lookup"><span data-stu-id="19b08-154">This section will highlight the differences that you see relevant to this article.</span></span>

### <a name="multiple-resource-versions"></a><span data-ttu-id="19b08-155">Více verzí prostředků</span><span class="sxs-lookup"><span data-stu-id="19b08-155">Multiple Resource Versions</span></span>

<span data-ttu-id="19b08-156">Instalace a použití více verzí prostředků vedle sebe nebyla podporovaná v Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="19b08-156">Installing and using multiple versions of resources side by side was not supported in PowerShell 4.0.</span></span> <span data-ttu-id="19b08-157">Pokud si všimnete problémů při importu zdrojů do vaší konfigurace, ujistěte se, že máte jenom jedna verze prostředku nainstalované.</span><span class="sxs-lookup"><span data-stu-id="19b08-157">If you notice issues importing resources into your Configuration, ensure that you only have one version of the resource installed.</span></span>

<span data-ttu-id="19b08-158">Na obrázku níže, dvě verze **xPSDesiredStateConfiguration** modulu jsou nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="19b08-158">In the image below, two versions of the **xPSDesiredStateConfiguration** module are installed.</span></span>

![Více verzí prostředků opraveno](/media/multiple-resource-versions-broken.md)

<span data-ttu-id="19b08-160">Na nejvyšší úrovni adresáře modulů zkopírujte obsah vaší verze požadovaný modul.</span><span class="sxs-lookup"><span data-stu-id="19b08-160">Copy the contents of your desired module version to the top level of the module directory.</span></span>

![Více verzí prostředků opraveno](/media/multiple-resource-versions-fixed.md)

### <a name="resource-location"></a><span data-ttu-id="19b08-162">Umístění prostředku</span><span class="sxs-lookup"><span data-stu-id="19b08-162">Resource location</span></span>

<span data-ttu-id="19b08-163">Při vytváření obsahu a kompilace konfigurací, vaše prostředky mohou být uloženy v libovolném adresáři určeném vaše [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path).</span><span class="sxs-lookup"><span data-stu-id="19b08-163">When authoring and compiling Configurations, your resources can be stored in any directory specified by your [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path).</span></span> <span data-ttu-id="19b08-164">LCM v Powershellu 4.0, vyžaduje všechny moduly prostředků DSC mají být uloženy v části "Program Files\WindowsPowerShell\Modules" nebo `$pshome\Modules`.</span><span class="sxs-lookup"><span data-stu-id="19b08-164">In PowerShell 4.0, the LCM requires all DSC resource modules to be stored under "Program Files\WindowsPowerShell\Modules" or `$pshome\Modules`.</span></span> <span data-ttu-id="19b08-165">Od v Powershellu 5.0, byl odebrán tento požadavek a moduly prostředků mohou být uloženy v libovolném adresáři určeném `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="19b08-165">Beginning in PowerShell 5.0, this requirement was removed, and resource modules can be stored in any directory specified by `PSModulePath`.</span></span>

## <a name="see-also"></a><span data-ttu-id="19b08-166">Viz taky</span><span class="sxs-lookup"><span data-stu-id="19b08-166">See also</span></span>

- [<span data-ttu-id="19b08-167">Prostředky</span><span class="sxs-lookup"><span data-stu-id="19b08-167">Resources</span></span>](../resources/resources.md)

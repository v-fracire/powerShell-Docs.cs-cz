---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace DSC
ms.openlocfilehash: 6af27f442de3080facd65892c713c989d0e388c5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403731"
---
# <a name="dsc-configurations"></a><span data-ttu-id="a48de-103">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="a48de-103">DSC Configurations</span></span>

> <span data-ttu-id="a48de-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a48de-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="a48de-105">Konfigurace DSC se skripty Powershellu, které definují speciální typ funkce.</span><span class="sxs-lookup"><span data-stu-id="a48de-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span>
<span data-ttu-id="a48de-106">K definování konfigurace, použijte prostředí PowerShell – klíčové slovo **konfigurace**.</span><span class="sxs-lookup"><span data-stu-id="a48de-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

```powershell
Configuration MyDscConfiguration {
    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration
```

<span data-ttu-id="a48de-107">Uložte skript pod názvem `.ps1` souboru.</span><span class="sxs-lookup"><span data-stu-id="a48de-107">Save the script as a `.ps1` file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="a48de-108">Konfigurace syntaxe</span><span class="sxs-lookup"><span data-stu-id="a48de-108">Configuration syntax</span></span>

<span data-ttu-id="a48de-109">Skript konfigurace se skládá z následujících částí:</span><span class="sxs-lookup"><span data-stu-id="a48de-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="a48de-110">**Konfigurace** bloku.</span><span class="sxs-lookup"><span data-stu-id="a48de-110">The **Configuration** block.</span></span> <span data-ttu-id="a48de-111">Toto je skript vnějšího bloku.</span><span class="sxs-lookup"><span data-stu-id="a48de-111">This is the outermost script block.</span></span> <span data-ttu-id="a48de-112">Definovat pomocí **konfigurace** – klíčové slovo a poskytnutí názvu.</span><span class="sxs-lookup"><span data-stu-id="a48de-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="a48de-113">Název konfigurace je v tomto případě "MyDscConfiguration".</span><span class="sxs-lookup"><span data-stu-id="a48de-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="a48de-114">Jeden nebo více **uzel** bloky.</span><span class="sxs-lookup"><span data-stu-id="a48de-114">One or more **Node** blocks.</span></span> <span data-ttu-id="a48de-115">Tyto zásady určují uzly (virtuální počítače nebo počítače), které konfigurujete.</span><span class="sxs-lookup"><span data-stu-id="a48de-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="a48de-116">V konfiguraci uvedené výš, existuje **uzel** blok, který cílí na počítač s názvem "TEST-PC1".</span><span class="sxs-lookup"><span data-stu-id="a48de-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span> <span data-ttu-id="a48de-117">Objekt uzlu může přijmout více názvů počítačů.</span><span class="sxs-lookup"><span data-stu-id="a48de-117">The Node block can accept multiple computer names.</span></span>
- <span data-ttu-id="a48de-118">Jeden nebo více prostředků bloky.</span><span class="sxs-lookup"><span data-stu-id="a48de-118">One or more resource blocks.</span></span> <span data-ttu-id="a48de-119">To je, kde konfiguraci nastaví vlastnosti pro prostředky, které je konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a48de-119">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="a48de-120">V tomto případě existují dva prostředků bloky, z nichž každý prostředek "WindowsFeature" volání.</span><span class="sxs-lookup"><span data-stu-id="a48de-120">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="a48de-121">V rámci **konfigurace** blok, můžete provést cokoli, co můžete normálně ve funkci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a48de-121">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="a48de-122">Například v předchozím příkladu, pokud nechcete pevně kódu název cílového počítače v konfiguraci, můžete přidat parametr pro název uzlu:</span><span class="sxs-lookup"><span data-stu-id="a48de-122">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

<span data-ttu-id="a48de-123">V tomto příkladu zadáte předáním jako název uzlu **ComputerName** parametr při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a48de-123">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuration.</span></span> <span data-ttu-id="a48de-124">Výchozí název "localhost".</span><span class="sxs-lookup"><span data-stu-id="a48de-124">The name defaults to "localhost".</span></span>

```powershell
Configuration MyDscConfiguration
{
    param
    (
        [string[]]$ComputerName='localhost'
    )

    Node $ComputerName
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

<span data-ttu-id="a48de-125">**Uzel** blok můžete také přijmout více názvů počítačů.</span><span class="sxs-lookup"><span data-stu-id="a48de-125">The **Node** block can also accept multiple computer names.</span></span> <span data-ttu-id="a48de-126">V příkladu výše, můžete použít `-ComputerName` parametr nebo pass čárkou oddělený seznam počítačů přímo k **uzel** bloku.</span><span class="sxs-lookup"><span data-stu-id="a48de-126">In the above example, you can either use the `-ComputerName` parameter, or pass a comma-separated list of computers directly to the **Node** block.</span></span>

```powershell
MyDscConfiguration -ComputerName "localhost", "Server01"
```

<span data-ttu-id="a48de-127">Při zadávání seznamu počítačů a **uzlu** bloku, z v rámci konfigurace, je třeba použít notaci pole.</span><span class="sxs-lookup"><span data-stu-id="a48de-127">When specifying a list of computers to the **Node** block, from within a Configuration, you need to use array-notation.</span></span>

```powershell
Configuration MyDscConfiguration
{
    Node @('localhost', 'Server01')
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

## <a name="compiling-the-configuration"></a><span data-ttu-id="a48de-128">Kompilace konfigurace</span><span class="sxs-lookup"><span data-stu-id="a48de-128">Compiling the configuration</span></span>

<span data-ttu-id="a48de-129">Předtím, než může přijmout konfiguraci, budete muset zkompilovat ji do dokument MOF.</span><span class="sxs-lookup"><span data-stu-id="a48de-129">Before you can enact a configuration, you have to compile it into a MOF document.</span></span>
<span data-ttu-id="a48de-130">To provedete voláním konfigurace, jako by volání funkce prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a48de-130">You do this by calling the configuration like you would call a PowerShell function.</span></span>
<span data-ttu-id="a48de-131">Poslední řádek v příkladu obsahující název konfigurace, volá konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a48de-131">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="a48de-132">Volání na konfiguraci, musí být funkce v globálním oboru (stejně jako u jakékoli jiné funkce Powershellu).</span><span class="sxs-lookup"><span data-stu-id="a48de-132">To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span>
> <span data-ttu-id="a48de-133">Můžete provést toto možné buď pomocí "dot-sourcing" skript, nebo spuštěním skriptu konfigurace pomocí klávesy F5 nebo kliknutím na **spustit skript** tlačítko v prostředí ISE.</span><span class="sxs-lookup"><span data-stu-id="a48de-133">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span>
> <span data-ttu-id="a48de-134">Dot-source skriptu, spusťte příkaz `. .\myConfig.ps1` kde `myConfig.ps1` je název souboru skriptu, který obsahuje vaši konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a48de-134">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="a48de-135">Při volání v konfiguraci ji:</span><span class="sxs-lookup"><span data-stu-id="a48de-135">When you call the configuration, it:</span></span>

- <span data-ttu-id="a48de-136">Přeloží všechny proměnné</span><span class="sxs-lookup"><span data-stu-id="a48de-136">Resolves all variables</span></span>
- <span data-ttu-id="a48de-137">Vytvoří složku v aktuálním adresáři se stejným názvem jako konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a48de-137">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="a48de-138">Vytvoří soubor s názvem _NodeName_MOF v novém adresáři, ve kterém _NodeName_ je název uzlu cílové konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a48de-138">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span>
  <span data-ttu-id="a48de-139">Pokud existuje více než jeden uzel, vytvoří se soubor MOF pro každý uzel.</span><span class="sxs-lookup"><span data-stu-id="a48de-139">If there is more than one node, a MOF file will be created for each node.</span></span>

> [!NOTE]
> <span data-ttu-id="a48de-140">Soubor MOF obsahoval všechny informace o konfiguraci pro cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="a48de-140">The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="a48de-141">Z toho důvodu je důležité, abyste zajistili jeho zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="a48de-141">Because of this, it’s important to keep it secure.</span></span>
> <span data-ttu-id="a48de-142">Další informace najdete v tématu [zabezpečení souboru MOF](../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="a48de-142">For more information, see [Securing the MOF file](../pull-server/secureMOF.md).</span></span>

<span data-ttu-id="a48de-143">Kompilování první konfigurace nad výsledky ve struktuře následující složky:</span><span class="sxs-lookup"><span data-stu-id="a48de-143">Compiling the first configuration above results in the following folder structure:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 localhost.mof
```

<span data-ttu-id="a48de-144">Pokud má parametr, viz druhý příklad konfigurace, který má být k dispozici v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="a48de-144">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="a48de-145">Tady je způsob, který by vypadalo:</span><span class="sxs-lookup"><span data-stu-id="a48de-145">Here's how that would look:</span></span>

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration -ComputerName 'MyTestNode'
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="a48de-146">Pomocí nových prostředků v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="a48de-146">Using new resources in Your configuration</span></span>

<span data-ttu-id="a48de-147">Pokud jste spustili v předchozích příkladech, jste si možná všimli, že se upozornění, které jste používali prostředku bez explicitně importu.</span><span class="sxs-lookup"><span data-stu-id="a48de-147">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="a48de-148">V současné době DSC se dodává s 12 prostředků jako součást modulu PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="a48de-148">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span>

<span data-ttu-id="a48de-149">Rutiny [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), je možné určit, jaké prostředky jsou nainstalovaná v systému a k dispozici pro použití podle LCM.</span><span class="sxs-lookup"><span data-stu-id="a48de-149">The cmdlet, [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span>
<span data-ttu-id="a48de-150">Jakmile tyto moduly byly umístěny do `$env:PSModulePath` a jsou správně rozpoznány modulem [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), stále potřebují být načteny v rámci vaší konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a48de-150">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), they still need to be loaded within your configuration.</span></span>

<span data-ttu-id="a48de-151">**Import-DscResource** je dynamické klíčové slovo, který může být rozpoznán pouze v rámci **konfigurace** bloku není rutina.</span><span class="sxs-lookup"><span data-stu-id="a48de-151">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block, it is not a cmdlet.</span></span>
<span data-ttu-id="a48de-152">**Import-DscResource** podporuje dva parametry:</span><span class="sxs-lookup"><span data-stu-id="a48de-152">**Import-DscResource** supports two parameters:</span></span>

- <span data-ttu-id="a48de-153">**Název modulu** je doporučený způsob použití **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="a48de-153">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="a48de-154">Přijímá název modulu, který obsahuje prostředky, které se mají naimportovat (stejně jako pole řetězců názvů modulů).</span><span class="sxs-lookup"><span data-stu-id="a48de-154">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span>
- <span data-ttu-id="a48de-155">**Název** je název prostředku, který chcete importovat.</span><span class="sxs-lookup"><span data-stu-id="a48de-155">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="a48de-156">Nejedná se o popisný název vrácený jako "Name" [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), ale název třídy používá při definování schématu prostředků (vrácena jako **elementu ResourceType** podle [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).</span><span class="sxs-lookup"><span data-stu-id="a48de-156">This is not the friendly name returned as "Name" by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).</span></span>

<span data-ttu-id="a48de-157">Další informace o používání `Import-DSCResource`, naleznete v tématu [pomocí Import-DSCResource](import-dscresource.md)</span><span class="sxs-lookup"><span data-stu-id="a48de-157">For more information on using `Import-DSCResource`, see [Using Import-DSCResource](import-dscresource.md)</span></span>

## <a name="powershell-v4-and-v5-differences"></a><span data-ttu-id="a48de-158">Rozdíly v4, tak i v5 prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="a48de-158">PowerShell v4 and v5 differences</span></span>

<span data-ttu-id="a48de-159">Existují rozdíly v kdy je potřeba prostředky DSC uložené v Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="a48de-159">There are differences in where DSC resources need to be stored in PowerShell 4.0.</span></span> <span data-ttu-id="a48de-160">Další informace najdete v tématu [umístění prostředku](import-dscresource.md#resource-location).</span><span class="sxs-lookup"><span data-stu-id="a48de-160">For more information, see [Resource location](import-dscresource.md#resource-location).</span></span>

## <a name="see-also"></a><span data-ttu-id="a48de-161">Viz také</span><span class="sxs-lookup"><span data-stu-id="a48de-161">See Also</span></span>

- [<span data-ttu-id="a48de-162">Prostředí Windows PowerShell Desired State Configuration – přehled</span><span class="sxs-lookup"><span data-stu-id="a48de-162">Windows PowerShell Desired State Configuration Overview</span></span>](../overview/overview.md)
- [<span data-ttu-id="a48de-163">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="a48de-163">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="a48de-164">Konfigurace Local Configuration Manageru</span><span class="sxs-lookup"><span data-stu-id="a48de-164">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)

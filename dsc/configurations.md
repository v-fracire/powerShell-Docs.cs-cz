---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace DSC
ms.openlocfilehash: 171068acb51f44e31c81e63f6640222ef71bee38
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093690"
---
# <a name="dsc-configurations"></a><span data-ttu-id="94297-103">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="94297-103">DSC Configurations</span></span>

> <span data-ttu-id="94297-104">Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="94297-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="94297-105">Konfigurace DSC se skripty Powershellu, které definují speciální typ funkce.</span><span class="sxs-lookup"><span data-stu-id="94297-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span>
<span data-ttu-id="94297-106">K definování konfigurace, použijte prostředí PowerShell – klíčové slovo **konfigurace**.</span><span class="sxs-lookup"><span data-stu-id="94297-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

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

<span data-ttu-id="94297-107">Uložte skript jako soubor .ps1.</span><span class="sxs-lookup"><span data-stu-id="94297-107">Save the script as a .ps1 file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="94297-108">Konfigurace syntaxe</span><span class="sxs-lookup"><span data-stu-id="94297-108">Configuration syntax</span></span>

<span data-ttu-id="94297-109">Skript konfigurace se skládá z následujících částí:</span><span class="sxs-lookup"><span data-stu-id="94297-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="94297-110">**Konfigurace** bloku.</span><span class="sxs-lookup"><span data-stu-id="94297-110">The **Configuration** block.</span></span> <span data-ttu-id="94297-111">Toto je skript vnějšího bloku.</span><span class="sxs-lookup"><span data-stu-id="94297-111">This is the outermost script block.</span></span> <span data-ttu-id="94297-112">Definovat pomocí **konfigurace** – klíčové slovo a poskytnutí názvu.</span><span class="sxs-lookup"><span data-stu-id="94297-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="94297-113">Název konfigurace je v tomto případě "MyDscConfiguration".</span><span class="sxs-lookup"><span data-stu-id="94297-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="94297-114">Jeden nebo více **uzel** bloky.</span><span class="sxs-lookup"><span data-stu-id="94297-114">One or more **Node** blocks.</span></span> <span data-ttu-id="94297-115">Tyto zásady určují uzly (virtuální počítače nebo počítače), které konfigurujete.</span><span class="sxs-lookup"><span data-stu-id="94297-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="94297-116">V konfiguraci uvedené výš, existuje **uzel** blok, který cílí na počítač s názvem "TEST-PC1".</span><span class="sxs-lookup"><span data-stu-id="94297-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span>
- <span data-ttu-id="94297-117">Jeden nebo více prostředků bloky.</span><span class="sxs-lookup"><span data-stu-id="94297-117">One or more resource blocks.</span></span> <span data-ttu-id="94297-118">To je, kde konfiguraci nastaví vlastnosti pro prostředky, které je konfigurace.</span><span class="sxs-lookup"><span data-stu-id="94297-118">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="94297-119">V tomto případě existují dva prostředků bloky, z nichž každý prostředek "WindowsFeature" volání.</span><span class="sxs-lookup"><span data-stu-id="94297-119">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="94297-120">V rámci **konfigurace** blok, můžete provést cokoli, co můžete normálně ve funkci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94297-120">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="94297-121">Například v předchozím příkladu, pokud nechcete pevně kódu název cílového počítače v konfiguraci, můžete přidat parametr pro název uzlu:</span><span class="sxs-lookup"><span data-stu-id="94297-121">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

```powershell
Configuration MyDscConfiguration {
    param(
        [string[]]$ComputerName='localhost'
    )
    Node $ComputerName {
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
MyDscConfiguration -ComputerName $ComputerName
```

<span data-ttu-id="94297-122">V tomto příkladu zadáte předáním jako název uzlu **ComputerName** parametr při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="94297-122">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuration.</span></span> <span data-ttu-id="94297-123">Výchozí název "localhost".</span><span class="sxs-lookup"><span data-stu-id="94297-123">The name defaults to "localhost".</span></span>

## <a name="compiling-the-configuration"></a><span data-ttu-id="94297-124">Kompilace konfigurace</span><span class="sxs-lookup"><span data-stu-id="94297-124">Compiling the configuration</span></span>

<span data-ttu-id="94297-125">Předtím, než může přijmout konfiguraci, budete muset zkompilovat ji do dokument MOF.</span><span class="sxs-lookup"><span data-stu-id="94297-125">Before you can enact a configuration, you have to compile it into a MOF document.</span></span>
<span data-ttu-id="94297-126">To provedete voláním konfigurace, jako by volání funkce prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94297-126">You do this by calling the configuration like you would call a PowerShell function.</span></span>
<span data-ttu-id="94297-127">Poslední řádek v příkladu obsahující název konfigurace, volá konfigurace.</span><span class="sxs-lookup"><span data-stu-id="94297-127">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="94297-128">Volání na konfiguraci, musí být funkce v globálním oboru (stejně jako u jakékoli jiné funkce Powershellu).</span><span class="sxs-lookup"><span data-stu-id="94297-128">To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span>
> <span data-ttu-id="94297-129">Můžete provést toto možné buď pomocí "dot-sourcing" skript, nebo spuštěním skriptu konfigurace pomocí klávesy F5 nebo kliknutím na **spustit skript** tlačítko v prostředí ISE.</span><span class="sxs-lookup"><span data-stu-id="94297-129">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span>
> <span data-ttu-id="94297-130">Dot-source skriptu, spusťte příkaz `. .\myConfig.ps1` kde `myConfig.ps1` je název souboru skriptu, který obsahuje vaši konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="94297-130">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="94297-131">Při volání v konfiguraci ji:</span><span class="sxs-lookup"><span data-stu-id="94297-131">When you call the configuration, it:</span></span>

- <span data-ttu-id="94297-132">Přeloží všechny proměnné</span><span class="sxs-lookup"><span data-stu-id="94297-132">Resolves all variables</span></span>
- <span data-ttu-id="94297-133">Vytvoří složku v aktuálním adresáři se stejným názvem jako konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="94297-133">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="94297-134">Vytvoří soubor s názvem _NodeName_MOF v novém adresáři, ve kterém _NodeName_ je název uzlu cílové konfigurace.</span><span class="sxs-lookup"><span data-stu-id="94297-134">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span>
  <span data-ttu-id="94297-135">Pokud existuje více uzlů, vytvoří se soubor MOF pro každý uzel.</span><span class="sxs-lookup"><span data-stu-id="94297-135">If there are more than one nodes, a MOF file will be created for each node.</span></span>

> [!NOTE]
> <span data-ttu-id="94297-136">Soubor MOF obsahoval všechny informace o konfiguraci pro cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="94297-136">The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="94297-137">Z toho důvodu je důležité, abyste zajistili jeho zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="94297-137">Because of this, it’s important to keep it secure.</span></span>
> <span data-ttu-id="94297-138">Další informace najdete v tématu [zabezpečení souboru MOF](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="94297-138">For more information, see [Securing the MOF file](secureMOF.md).</span></span>

<span data-ttu-id="94297-139">Kompilování první konfigurace nad výsledky ve struktuře následující složky:</span><span class="sxs-lookup"><span data-stu-id="94297-139">Compiling the first configuration above results in the following folder structure:</span></span>

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

<span data-ttu-id="94297-140">Pokud má parametr, viz druhý příklad konfigurace, který má být k dispozici v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="94297-140">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="94297-141">Tady je způsob, který by vypadalo:</span><span class="sxs-lookup"><span data-stu-id="94297-141">Here's how that would look:</span></span>

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

## <a name="using-dependson"></a><span data-ttu-id="94297-142">Pomocí DependsOn</span><span class="sxs-lookup"><span data-stu-id="94297-142">Using DependsOn</span></span>

<span data-ttu-id="94297-143">Je užitečné DSC – klíčové slovo **DependsOn**.</span><span class="sxs-lookup"><span data-stu-id="94297-143">A useful DSC keyword is **DependsOn**.</span></span> <span data-ttu-id="94297-144">Obvykle (i když není vždy), platí prostředky v pořadí, ve kterém se zobrazují v rámci konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="94297-144">Typically (though not necessarily always), DSC applies the resources in the order that they appear within the configuration.</span></span>
<span data-ttu-id="94297-145">Ale **DependsOn** Určuje, které prostředky jsou závislé na jiných prostředcích a LCM se zajistí, že se použijí ve správném pořadí, bez ohledu na pořadí, ve které prostředky jsou definovány instancí.</span><span class="sxs-lookup"><span data-stu-id="94297-145">However, **DependsOn** specifies which resources depend on other resources, and the LCM ensures that they are applied in the correct order, regardless of the order in which resource instances are defined.</span></span>
<span data-ttu-id="94297-146">Konfigurace například můžou určit, že instance **uživatele** prostředků závisí na existenci **skupiny** instance:</span><span class="sxs-lookup"><span data-stu-id="94297-146">For example, a configuration might specify that an instance of the **User** resource depends on the existence of a **Group** instance:</span></span>

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = 'Present'
            GroupName = 'TestGroup'
        }

        User UserExample {
            Ensure = 'Present'
            UserName = 'TestUser'
            FullName = 'TestUser'
            DependsOn = '[Group]GroupExample'
        }
    }
}
```

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="94297-147">Pomocí nových prostředků v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="94297-147">Using new resources in Your configuration</span></span>

<span data-ttu-id="94297-148">Pokud jste spustili v předchozích příkladech, jste si možná všimli, že se upozornění, které jste používali prostředku bez explicitně importu.</span><span class="sxs-lookup"><span data-stu-id="94297-148">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="94297-149">V současné době DSC se dodává s 12 prostředků jako součást modulu PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="94297-149">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span>
<span data-ttu-id="94297-150">Ostatní prostředky v externích modulech musí být umístěn v `$env:PSModulePath` aby bylo možné je nerozpoznají LCM.</span><span class="sxs-lookup"><span data-stu-id="94297-150">Other resources in external modules must be placed in `$env:PSModulePath` in order to be recognized by the LCM.</span></span>
<span data-ttu-id="94297-151">Nová rutina [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), je možné určit, jaké prostředky jsou nainstalovaná v systému a k dispozici pro použití podle LCM.</span><span class="sxs-lookup"><span data-stu-id="94297-151">A new cmdlet, [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span>
<span data-ttu-id="94297-152">Jakmile tyto moduly byly umístěny do `$env:PSModulePath` a jsou správně rozpoznány modulem [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), stále potřebují být načteny v rámci vaší konfigurace.</span><span class="sxs-lookup"><span data-stu-id="94297-152">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), they still need to be loaded within your configuration.</span></span>
<span data-ttu-id="94297-153">**Import-DscResource** je dynamické klíčové slovo, který může být rozpoznán pouze v rámci **konfigurace** blok (tedy není rutina).</span><span class="sxs-lookup"><span data-stu-id="94297-153">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block (i.e. it is not a cmdlet).</span></span>
<span data-ttu-id="94297-154">**Import-DscResource** podporuje dva parametry:</span><span class="sxs-lookup"><span data-stu-id="94297-154">**Import-DscResource** supports two parameters:</span></span>

- <span data-ttu-id="94297-155">**Název modulu** je doporučený způsob použití **Import-DscResource**.</span><span class="sxs-lookup"><span data-stu-id="94297-155">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="94297-156">Přijímá název modulu, který obsahuje prostředky, které se mají naimportovat (stejně jako pole řetězců názvů modulů).</span><span class="sxs-lookup"><span data-stu-id="94297-156">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span>
- <span data-ttu-id="94297-157">**Název** je název prostředku, který chcete importovat.</span><span class="sxs-lookup"><span data-stu-id="94297-157">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="94297-158">Nejedná se o popisný název vrácený jako "Name" [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), ale název třídy používá při definování schématu prostředků (vrácena jako **elementu ResourceType** podle [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).</span><span class="sxs-lookup"><span data-stu-id="94297-158">This is not the friendly name returned as "Name" by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).</span></span>

## <a name="see-also"></a><span data-ttu-id="94297-159">Viz také</span><span class="sxs-lookup"><span data-stu-id="94297-159">See Also</span></span>

- [<span data-ttu-id="94297-160">Prostředí Windows PowerShell Desired State Configuration – přehled</span><span class="sxs-lookup"><span data-stu-id="94297-160">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="94297-161">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="94297-161">DSC Resources</span></span>](resources.md)
- [<span data-ttu-id="94297-162">Konfigurace Local Configuration Manageru</span><span class="sxs-lookup"><span data-stu-id="94297-162">Configuring The Local Configuration Manager</span></span>](metaConfig.md)
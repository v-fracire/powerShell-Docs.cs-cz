---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: Konfigurace DSC
ms.openlocfilehash: eeee18e6a4bd09cc22d1ac4ed5cbfaea02346170
ms.sourcegitcommit: 60f06a06c2fce63024f3f4cbd7657b1dfe7fcb1a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/03/2018
---
# <a name="dsc-configurations"></a><span data-ttu-id="cb0a6-103">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="cb0a6-103">DSC Configurations</span></span>

><span data-ttu-id="cb0a6-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="cb0a6-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="cb0a6-105">Konfigurace DSC jsou skripty prostředí PowerShell, které definují speciální typ funkce.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-105">DSC configurations are PowerShell scripts that define a special type of function.</span></span> <span data-ttu-id="cb0a6-106">K definování konfigurace, použijte klíčové slovo prostředí PowerShell **konfigurace**.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-106">To define a configuration, you use the PowerShell keyword **Configuration**.</span></span>

```powershell
Configuration MyDscConfiguration {

    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration

```

<span data-ttu-id="cb0a6-107">Uložte skript jako souboru s příponou .ps1.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-107">Save the script as a .ps1 file.</span></span>

## <a name="configuration-syntax"></a><span data-ttu-id="cb0a6-108">Konfigurace syntaxe</span><span class="sxs-lookup"><span data-stu-id="cb0a6-108">Configuration syntax</span></span>

<span data-ttu-id="cb0a6-109">Konfigurační skript se skládá z následujících částí:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-109">A configuration script consists of the following parts:</span></span>

- <span data-ttu-id="cb0a6-110">**Konfigurace** bloku.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-110">The **Configuration** block.</span></span> <span data-ttu-id="cb0a6-111">Toto je blok nejkrajnější skriptu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-111">This is the outermost script block.</span></span> <span data-ttu-id="cb0a6-112">Můžete definovat pomocí **konfigurace** – klíčové slovo a poskytnutí názvu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-112">You define it by using the **Configuration** keyword and providing a name.</span></span> <span data-ttu-id="cb0a6-113">Název konfigurace je v tomto případě "MyDscConfiguration".</span><span class="sxs-lookup"><span data-stu-id="cb0a6-113">In this case, the name of the configuration is "MyDscConfiguration".</span></span>
- <span data-ttu-id="cb0a6-114">Jeden nebo více **uzlu** bloky.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-114">One or more **Node** blocks.</span></span> <span data-ttu-id="cb0a6-115">Tyto zásady určují uzly (počítačů nebo virtuální počítače), které konfigurujete.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-115">These define the nodes (computers or VMs) that you are configuring.</span></span> <span data-ttu-id="cb0a6-116">Ve výše uvedené konfiguraci je jeden **uzlu** bloku, která je cílena počítači s názvem "TEST-PC1".</span><span class="sxs-lookup"><span data-stu-id="cb0a6-116">In the above configuration, there is one **Node** block that targets a computer named "TEST-PC1".</span></span>
- <span data-ttu-id="cb0a6-117">Jeden nebo více prostředků bloky.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-117">One or more resource blocks.</span></span> <span data-ttu-id="cb0a6-118">Toto je, kde konfigurace nastaví vlastnosti pro prostředky, které je konfigurace.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-118">This is where the configuration sets the properties for the resources that it is configuring.</span></span> <span data-ttu-id="cb0a6-119">V takovém případě existují dva bloky prostředků, z nichž každý volání prostředků "WindowsFeature".</span><span class="sxs-lookup"><span data-stu-id="cb0a6-119">In this case, there are two resource blocks, each of which call the "WindowsFeature" resource.</span></span>

<span data-ttu-id="cb0a6-120">V rámci **konfigurace** blok, můžete provést všechno, co se za normálních okolností může ve funkci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-120">Within a **Configuration** block, you can do anything that you normally could in a PowerShell function.</span></span> <span data-ttu-id="cb0a6-121">Například v předchozím příkladu, pokud nebyla chcete pevného code název cílového počítače v konfiguraci, můžete přidat parametr pro název uzlu:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-121">For example, in the previous example, if you didn't want to hard code the name of the target computer in the configuration, you could add a parameter for the node name:</span></span>

```powershell
Configuration MyDscConfiguration {

    param(
        [string[]]$ComputerName="localhost"
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration

```

<span data-ttu-id="cb0a6-122">V tomto příkladu zadejte název uzlu předáním jej jako **ComputerName** parametr při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-122">In this example, you specify the name of the node by passing it as the **ComputerName** parameter when you compile the configuration.</span></span> <span data-ttu-id="cb0a6-123">Výchozí název "localhost".</span><span class="sxs-lookup"><span data-stu-id="cb0a6-123">The name defaults to "localhost".</span></span>

## <a name="compiling-the-configuration"></a><span data-ttu-id="cb0a6-124">Kompilování konfigurace</span><span class="sxs-lookup"><span data-stu-id="cb0a6-124">Compiling the configuration</span></span>

<span data-ttu-id="cb0a6-125">Před konfigurací můžete uplatní, budete muset kompilována MOF dokumentu.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-125">Before you can enact a configuration, you have to compile it into a MOF document.</span></span> <span data-ttu-id="cb0a6-126">To provedete pomocí volání konfigurace jako funkce prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-126">You do this by calling the configuration like you would a PowerShell function.</span></span>  
<span data-ttu-id="cb0a6-127">Poslední řádek v příkladu obsahující pouze název konfigurace, zavolá konfigurace.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-127">The last line of the example containing only the name of the configuration, calls the configuration.</span></span>

><span data-ttu-id="cb0a6-128">**Poznámka:** volat konfigurace, musí být funkce v globálním oboru (stejně jako u jakékoli jiné funkce prostředí PowerShell).</span><span class="sxs-lookup"><span data-stu-id="cb0a6-128">**Note:** To call a configuration, the function must be in global scope (as with any other PowerShell function).</span></span> 
><span data-ttu-id="cb0a6-129">Můžete použít tento dojít buď pomocí "dot-sourcing" skriptu, nebo spuštěním skriptu konfigurace pomocí F5 nebo kliknutím na **spustit skript** tlačítko (ISE) v.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-129">You can make this happen either by "dot-sourcing" the script, or by running the configuration script by using F5 or clicking on the **Run Script** button in the ISE.</span></span> 
><span data-ttu-id="cb0a6-130">Zdroj tečkou skriptu, spusťte příkaz `. .\myConfig.ps1` kde `myConfig.ps1` je název souboru skriptu, který obsahuje konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-130">To dot-source the script, run the command `. .\myConfig.ps1` where `myConfig.ps1` is the name of the script file that contains your configuration.</span></span>

<span data-ttu-id="cb0a6-131">Při volání v konfiguraci ji:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-131">When you call the configuration, it:</span></span>

- <span data-ttu-id="cb0a6-132">Přeloží všechny proměnné</span><span class="sxs-lookup"><span data-stu-id="cb0a6-132">Resolves all variables</span></span> 
- <span data-ttu-id="cb0a6-133">Vytvoří složku v aktuálním adresáři se stejným názvem jako konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-133">Creates a folder in the current directory with the same name as the configuration.</span></span>
- <span data-ttu-id="cb0a6-134">Vytvoří soubor s názvem _NodeName_MOF do nového adresáře, kde _NodeName_ je název cílový uzel konfigurace.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-134">Creates a file named _NodeName_.mof in the new directory, where _NodeName_ is the name of the target node of the configuration.</span></span> 
    <span data-ttu-id="cb0a6-135">Pokud je více než jeden uzlů, vytvoří se soubor MOF pro každý uzel.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-135">If there are more than one nodes, a MOF file will be created for each node.</span></span>

><span data-ttu-id="cb0a6-136">**Poznámka:**: soubor MOF obsahuje všechny informace o konfiguraci pro cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-136">**Note**: The MOF file contains all of the configuration information for the target node.</span></span> <span data-ttu-id="cb0a6-137">Z toho důvodu je důležité k lepšímu zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-137">Because of this, it’s important to keep it secure.</span></span> 
><span data-ttu-id="cb0a6-138">Další informace najdete v tématu [zabezpečení souboru MOF](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="cb0a6-138">For more information, see [Securing the MOF file](secureMOF.md).</span></span>

<span data-ttu-id="cb0a6-139">Kompilování první konfiguraci výše má za následek následující strukturu složek:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-139">Compiling the first configuration above results in the following folder structure:</span></span>

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

<span data-ttu-id="cb0a6-140">Pokud konfigurace přebírá parametr, jako v druhém příkladu, který je třeba zadat v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-140">If the configuration takes a parameter, as in the second example, that has to be provided at compile time.</span></span> <span data-ttu-id="cb0a6-141">Zde je, který vzhledu:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-141">Here's how that would look:</span></span>

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

## <a name="using-dependson"></a><span data-ttu-id="cb0a6-142">Pomocí DependsOn</span><span class="sxs-lookup"><span data-stu-id="cb0a6-142">Using DependsOn</span></span>

<span data-ttu-id="cb0a6-143">Je užitečné DSC – klíčové slovo **DependsOn**.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-143">A useful DSC keyword is **DependsOn**.</span></span> <span data-ttu-id="cb0a6-144">Obvykle (i když není vždy), platí prostředky v pořadí, ve kterém se zobrazují v rámci konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-144">Typically (though not necessarily always), DSC applies the resources in the order that they appear within the configuration.</span></span> <span data-ttu-id="cb0a6-145">Ale **DependsOn** Určuje, které prostředky závisí na jiné prostředky, a LCM zajistí, že jejich použití ve správném pořadí, bez ohledu na pořadí, ve které prostředků jsou definovány instancí.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-145">However, **DependsOn** specifies which resources depend on other resources, and the LCM ensures that they are applied in the correct order, regardless of the order in which resource instances are defined.</span></span> <span data-ttu-id="cb0a6-146">Například, konfigurace může určit, že instance **uživatele** prostředků závisí na existenci **skupiny** instance:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-146">For example, a configuration might specify that an instance of the **User** resource depends on the existence of a **Group** instance:</span></span>

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = "Present"
            GroupName = "TestGroup"
        }

        User UserExample {
            Ensure = "Present"
            UserName = "TestUser"
            FullName = "TestUser"
            DependsOn = "[Group]GroupExample"
        }
    }
}

```

## <a name="using-new-resources-in-your-configuration"></a><span data-ttu-id="cb0a6-147">Pomocí nové prostředky ve vaší konfiguraci</span><span class="sxs-lookup"><span data-stu-id="cb0a6-147">Using new resources in Your configuration</span></span>

<span data-ttu-id="cb0a6-148">Pokud jste spustili v předchozích příkladech, budete možná jste si všimli, že byly varování, že jste používali prostředku bez explicitně jeho import.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-148">If you ran the previous examples, you might have noticed that you were warned that you were using a resource without explicitly importing it.</span></span>
<span data-ttu-id="cb0a6-149">V současné době DSC se dodává s 12 prostředky jako součást modulu PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-149">Today, DSC ships with 12 resources as part of the PSDesiredStateConfiguration module.</span></span> <span data-ttu-id="cb0a6-150">Další prostředky v externích moduly musí být umístěny v `$env:PSModulePath` aby rozpoznala LCM.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-150">Other resources in external modules must be placed in `$env:PSModulePath` in order to be recognized by the LCM.</span></span> <span data-ttu-id="cb0a6-151">Nové rutiny [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), můžete použít k určení, jaké prostředky jsou nainstalovaná v systému a k dispozici pro použití LCM.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-151">A new cmdlet, [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), can be used to determine what resources are installed on the system and available for use by the LCM.</span></span> <span data-ttu-id="cb0a6-152">Jakmile tyto moduly byly umístěny do `$env:PSModulePath` a jsou správně rozpoznáno [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), ještě musí být načíst v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-152">Once these modules have been placed in `$env:PSModulePath` and are properly recognized by [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), they still need to be loaded within your configuration.</span></span> 
<span data-ttu-id="cb0a6-153">**Import DscResource** je dynamické klíčové slovo, které může být rozeznána pouze v rámci **konfigurace** bloku (tj. není rutina).</span><span class="sxs-lookup"><span data-stu-id="cb0a6-153">**Import-DscResource** is a dynamic keyword that can only be recognized within a **Configuration** block (i.e. it is not a cmdlet).</span></span> 
<span data-ttu-id="cb0a6-154">**Import DscResource** podporuje dva parametry:</span><span class="sxs-lookup"><span data-stu-id="cb0a6-154">**Import-DscResource** supports two parameters:</span></span>
- <span data-ttu-id="cb0a6-155">**Název modulu** je doporučený způsob použití **Import DscResource**.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-155">**ModuleName** is the recommended way of using **Import-DscResource**.</span></span> <span data-ttu-id="cb0a6-156">Přijímá název modul, který obsahuje prostředky, které mají být importované (i pole řetězců názvů modulu).</span><span class="sxs-lookup"><span data-stu-id="cb0a6-156">It accepts the name of the module that contains the resources to be imported (as well as a string array of module names).</span></span> 
- <span data-ttu-id="cb0a6-157">**Název** je název prostředku pro import.</span><span class="sxs-lookup"><span data-stu-id="cb0a6-157">**Name** is the name of the resource to import.</span></span> <span data-ttu-id="cb0a6-158">Nejedná se o popisný název vrácené jako "Název" [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), ale název třídy, které se používá při definování schématu zdroje (vrátí jako **ResourceType** podle [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)).</span><span class="sxs-lookup"><span data-stu-id="cb0a6-158">This is not the friendly name returned as "Name" by [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), but the class name used when defining the resource schema (returned as **ResourceType** by [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)).</span></span> 

## <a name="see-also"></a><span data-ttu-id="cb0a6-159">Viz také</span><span class="sxs-lookup"><span data-stu-id="cb0a6-159">See Also</span></span>
* [<span data-ttu-id="cb0a6-160">Přehled stavu konfigurace požadovaného prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb0a6-160">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
* [<span data-ttu-id="cb0a6-161">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="cb0a6-161">DSC Resources</span></span>](resources.md)
* [<span data-ttu-id="cb0a6-162">Konfigurace správce místní konfigurace</span><span class="sxs-lookup"><span data-stu-id="cb0a6-162">Configuring The Local Configuration Manager</span></span>](metaConfig.md)


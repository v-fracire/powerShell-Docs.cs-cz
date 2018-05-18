---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Začínáme s prostředím PowerShell konfigurace požadovaného stavu
ms.openlocfilehash: a449382c979e680ea311c887c86cb675ba6162b7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="getting-started-with-powershell-desired-state-configuration"></a><span data-ttu-id="99c1f-103">Začínáme s prostředím PowerShell konfigurace požadovaného stavu</span><span class="sxs-lookup"><span data-stu-id="99c1f-103">Getting Started with PowerShell Desired State Configuration</span></span> #

<span data-ttu-id="99c1f-104">Tato příručka popisuje, jak začít vytvářet dokumenty konfigurace požadovaného stavu prostředí PowerShell a použít je k počítačům.</span><span class="sxs-lookup"><span data-stu-id="99c1f-104">This guide describes how to begin creating PowerShell Desired State Configuration documents and apply them to machines.</span></span> <span data-ttu-id="99c1f-105">Předpokládá základní znalost rutiny prostředí PowerShell, moduly a funkce.</span><span class="sxs-lookup"><span data-stu-id="99c1f-105">It assumes basic familiarity with PowerShell cmdlets, modules, and functions.</span></span>


## <a name="create-a-configuration"></a><span data-ttu-id="99c1f-106">Vytvoření konfigurace</span><span class="sxs-lookup"><span data-stu-id="99c1f-106">Create a Configuration</span></span> ##

<span data-ttu-id="99c1f-107">[**Konfigurace** ](https://msdn.microsoft.com/powershell/dsc/configurations) jsou dokumenty, které popisují prostředí.</span><span class="sxs-lookup"><span data-stu-id="99c1f-107">[**Configurations**](https://msdn.microsoft.com/powershell/dsc/configurations) are documents that describe an environment.</span></span> <span data-ttu-id="99c1f-108">Prostředí obsahovat "**uzly**", které jsou běžně virtuálních nebo fyzických počítačích.</span><span class="sxs-lookup"><span data-stu-id="99c1f-108">Environments consist of "**nodes**", which are commonly virtual or physical machines.</span></span>

<span data-ttu-id="99c1f-109">Konfigurace můžou mít v různých formách.</span><span class="sxs-lookup"><span data-stu-id="99c1f-109">Configurations can come in a variety of forms.</span></span> <span data-ttu-id="99c1f-110">Nejjednodušší způsob, jak vytvořit novou konfiguraci je vytvoření souboru s příponou .ps1 (skript prostředí PowerShell).</span><span class="sxs-lookup"><span data-stu-id="99c1f-110">The easiest way to create a new configuration is to create a .ps1 (PowerShell script) file.</span></span> <span data-ttu-id="99c1f-111">K tomuto účelu otevřete váš editor výběru.</span><span class="sxs-lookup"><span data-stu-id="99c1f-111">To do this, open your editor of choice.</span></span> <span data-ttu-id="99c1f-112">Prostředí PowerShell ISE je dobrá volba, vzhledem k tomu, že nativně rozumí DSC.</span><span class="sxs-lookup"><span data-stu-id="99c1f-112">The PowerShell ISE is a good choice, since it understands DSC natively.</span></span> <span data-ttu-id="99c1f-113">Uložte jako PS1 následující:</span><span class="sxs-lookup"><span data-stu-id="99c1f-113">Save the following as a PS1:</span></span>

```powershell
configuration MyFirstConfiguration
{
    Import-DscResource -Name WindowsFeature

    Node localhost
    {
        WindowsFeature IIS
        {
            Name = "IIS"

        }

    }

}
```
## <a name="parts-of-a-configuration"></a><span data-ttu-id="99c1f-114">Součástí konfigurace</span><span class="sxs-lookup"><span data-stu-id="99c1f-114">Parts of a Configuration</span></span> ##
<span data-ttu-id="99c1f-115">**Konfigurace** je klíčové slovo, který byl přidán do prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="99c1f-115">**Configuration** is a keyword that has been added to PowerShell 4.0.</span></span> <span data-ttu-id="99c1f-116">Označuje je zvláštní druh funkce prostředí PowerShell používané konfigurace požadovaného stavu.</span><span class="sxs-lookup"><span data-stu-id="99c1f-116">It signifies a special kind of PowerShell function used by Desired State Configuration.</span></span> <span data-ttu-id="99c1f-117">V tomto příkladu je funkce s názvem myFirstConfiguration.</span><span class="sxs-lookup"><span data-stu-id="99c1f-117">In this example, the function is named myFirstConfiguration.</span></span>

<span data-ttu-id="99c1f-118">Na další řádek je příkaz import, podobně jako Import modulu.</span><span class="sxs-lookup"><span data-stu-id="99c1f-118">The next line is an import statement, similar to importing a module.</span></span> <span data-ttu-id="99c1f-119">Bude probírat později.</span><span class="sxs-lookup"><span data-stu-id="99c1f-119">It will be discussed later on.</span></span>

<span data-ttu-id="99c1f-120">"Uzel" definuje název počítače, které tato konfigurace bude fungovat na.</span><span class="sxs-lookup"><span data-stu-id="99c1f-120">"Node" defines the machine name this configuration will act on.</span></span> <span data-ttu-id="99c1f-121">I když tato konfigurace je upravovat místně, můžete konfigurace přístup ke vzdálené uzly a nakonfigurovat.</span><span class="sxs-lookup"><span data-stu-id="99c1f-121">Although this configuration is edited locally, configurations can reach out to remote nodes and configure them.</span></span>

<span data-ttu-id="99c1f-122">Uzly mohou být názvy počítačů nebo IP adresy.</span><span class="sxs-lookup"><span data-stu-id="99c1f-122">Nodes can be machine names or IP addresses.</span></span> <span data-ttu-id="99c1f-123">Může mít více uzlů v jedné konfiguraci dokumentu.</span><span class="sxs-lookup"><span data-stu-id="99c1f-123">You can have multiple nodes in a single configuration document.</span></span> <span data-ttu-id="99c1f-124">Pomocí [konfigurační data](https://msdn.microsoft.com/powershell/dsc/configdata), můžete mít také stejnou konfiguraci použít na víc uzlů.</span><span class="sxs-lookup"><span data-stu-id="99c1f-124">Using [configuration data](https://msdn.microsoft.com/powershell/dsc/configdata), you can also have the same configuration apply to multiple nodes.</span></span> <span data-ttu-id="99c1f-125">V takovém případě uzlu je "localhost" – to znamená místního počítače.</span><span class="sxs-lookup"><span data-stu-id="99c1f-125">In this case, the node is "localhost" - which means the local computer.</span></span>

<span data-ttu-id="99c1f-126">Další položka [ **prostředků**](https://msdn.microsoft.com/powershell/dsc/resources).</span><span class="sxs-lookup"><span data-stu-id="99c1f-126">The next item is a [**resource**](https://msdn.microsoft.com/powershell/dsc/resources).</span></span> <span data-ttu-id="99c1f-127">Prostředky jsou stavební bloky konfigurací.</span><span class="sxs-lookup"><span data-stu-id="99c1f-127">Resources are building blocks of configurations.</span></span> <span data-ttu-id="99c1f-128">Každý prostředek, je modul, který definuje logiku implementace jeden aspekt počítače.</span><span class="sxs-lookup"><span data-stu-id="99c1f-128">Each resource is a module that defines the implementation logic of a single aspect of a machine.</span></span> <span data-ttu-id="99c1f-129">Každý prostředek na počítači můžete zobrazit spuštěním **Get-DscResource** v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99c1f-129">You can view every resource on your machine by running **Get-DscResource** in PowerShell.</span></span> <span data-ttu-id="99c1f-130">Prostředky musí být na místním počítači a importovat před použitím v konfiguraci s **Import DscResource** tedy na druhém řádku této konfigurace.</span><span class="sxs-lookup"><span data-stu-id="99c1f-130">Resources must be present on the local machine and imported before they can be used in a configuration with **Import-DscResource** which is on the second line of this configuration.</span></span>

<span data-ttu-id="99c1f-131">**Přijetí konfigurace**</span><span class="sxs-lookup"><span data-stu-id="99c1f-131">**Enacting a Configuration**</span></span>

<span data-ttu-id="99c1f-132">Skript výše je uložena a spustíte, bude možné vytvořit žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="99c1f-132">If the script above is saved and run, no output will be produced.</span></span> <span data-ttu-id="99c1f-133">Toto je vzhledem k tomu, že konfigurace je právě funkce a skript výše má definované funkce, ale ještě není ji spustit.</span><span class="sxs-lookup"><span data-stu-id="99c1f-133">This is because a configuration is just a function, and the script above has defined the function but not yet run it.</span></span> <span data-ttu-id="99c1f-134">Jakmile je definována funkce, musí být volána:</span><span class="sxs-lookup"><span data-stu-id="99c1f-134">After the function is defined, it must be invoked:</span></span>
```powershell
myFirstConfiguration
```

<span data-ttu-id="99c1f-135">Po provedení konfigurace funkcí je ověření konfigurace je neplatná.</span><span class="sxs-lookup"><span data-stu-id="99c1f-135">When executed, configuration functions validate the configuration is valid.</span></span> <span data-ttu-id="99c1f-136">Měl by mít žádné chyby syntaxe, prostředky by měly mít všechny povinné parametry definované a všechny prostředky by měly být naimportovány před spuštěním.</span><span class="sxs-lookup"><span data-stu-id="99c1f-136">It should have no syntax errors, resources should have all mandatory parameters defined, and all resources should be imported before execution.</span></span>

<span data-ttu-id="99c1f-137">Po konfiguraci se spustí, vytvoří složku s názvem konfigurace obsahující **. Soubor MOF** pro každý uzel v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="99c1f-137">Once the configuration is executed, it creates a folder with the name of the configuration containing a **.MOF file** for every node in the configuration.</span></span> <span data-ttu-id="99c1f-138">Na. Soubor MOF je formátu založených na standardech správy, který je používán DSC prostředí PowerShell pro komunikaci přes síť.</span><span class="sxs-lookup"><span data-stu-id="99c1f-138">The .MOF file is a standards-based management format which is used by PowerShell DSC to communicate over the network.</span></span>

<span data-ttu-id="99c1f-139">Chcete-li uplatní konfigurace:</span><span class="sxs-lookup"><span data-stu-id="99c1f-139">To enact the configuration:</span></span>
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration
```
<span data-ttu-id="99c1f-140">Tím se vytvoří úlohu prostředí PowerShell, která dosáhne pro uzly v konfiguraci a nakonfiguruje je.</span><span class="sxs-lookup"><span data-stu-id="99c1f-140">This creates a PowerShell job that reaches out to the nodes in the configuration and configures them.</span></span> <span data-ttu-id="99c1f-141">Pokud chcete zobrazit výstup úlohy, použijte - čekání.</span><span class="sxs-lookup"><span data-stu-id="99c1f-141">To see the output of the job, use -Wait.</span></span>
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration -Wait
```
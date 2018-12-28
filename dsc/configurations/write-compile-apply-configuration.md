---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, služby, instalační program
title: Psaní, kompilace a použití konfigurace
ms.openlocfilehash: fa4d98fd12202439ba7025fd8af3fa398653ca05
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403673"
---
> <span data-ttu-id="f0c8f-103">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f0c8f-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="write-compile-and-apply-a-configuration"></a><span data-ttu-id="f0c8f-104">Psaní, kompilace a použití konfigurace</span><span class="sxs-lookup"><span data-stu-id="f0c8f-104">Write, Compile, and Apply a Configuration</span></span>

<span data-ttu-id="f0c8f-105">V tomto cvičení vás provedou vytvořením a aplikování konfigurace Desired State Configuration (DSC) od začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="f0c8f-106">V následujícím příkladu se dozvíte, jak napsat a použít velmi jednoduchou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-106">In the following example, you will learn how to write and apply a very simple Configuration.</span></span> <span data-ttu-id="f0c8f-107">Konfigurace se ujistěte se, že "HelloWorld.txt" soubor existuje na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-107">The Configuration will ensure a "HelloWorld.txt" file exists on your local machine.</span></span> <span data-ttu-id="f0c8f-108">Při odstranění souboru, DSC se jej znovu vytvořit při příštím aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-108">If you delete the file, DSC will recreate it the next time it updates.</span></span>

<span data-ttu-id="f0c8f-109">Přehled o novinkách DSC a jak to funguje, najdete v části [Desired State Configuration přehled pro vývojáře](../overview/overview.md).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-109">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Developers](../overview/overview.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="f0c8f-110">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f0c8f-110">Requirements</span></span>

<span data-ttu-id="f0c8f-111">Chcete-li spustit tento příklad, musíte počítač se systémem Powershellu 4.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-111">To run this example, you will need a computer running PowerShell 4.0 or later.</span></span>

## <a name="write-the-configuration"></a><span data-ttu-id="f0c8f-112">Zapsat konfiguraci</span><span class="sxs-lookup"><span data-stu-id="f0c8f-112">Write the configuration</span></span>

<span data-ttu-id="f0c8f-113">DSC [konfigurace](configurations.md) je speciální funkce prostředí PowerShell, který definuje, jak chcete nakonfigurovat jeden nebo více cílových počítačů (uzlů).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-113">A DSC [Configuration](configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (Nodes).</span></span>

<span data-ttu-id="f0c8f-114">V prostředí PowerShell ISE, nebo jiném editoru prostředí PowerShell zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="f0c8f-114">In the PowerShell ISE, or other PowerShell editor, type the following:</span></span>

```powershell
Configuration HelloWorld {

    # Import the module that contains the File resource.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets to compile MOF files for, when this configuration is executed.
    Node 'localhost' {

        # The File resource can ensure the state of files, or copy them from a source to a destination with persistent updates.
        File HelloWorld {
            DestinationPath = "C:\Temp\HelloWorld.txt"
            Ensure = "Present"
            Contents   = "Hello World from DSC!"
        }
    }
}
```

<span data-ttu-id="f0c8f-115">Uložte soubor jako "HelloWorld.ps1".</span><span class="sxs-lookup"><span data-stu-id="f0c8f-115">Save the file as "HelloWorld.ps1".</span></span>

<span data-ttu-id="f0c8f-116">Definování konfigurace je stejná jako definice funkce.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-116">Defining a Configuration is like defining a Function.</span></span> <span data-ttu-id="f0c8f-117">**Uzel** bloku Určuje cílový uzel nakonfigurovat, v tomto případě `localhost`.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-117">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="f0c8f-118">Konfigurace volá jedno [prostředky](../resources/resources.md), `File` prostředků.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-118">The configuration calls one [resources](../resources/resources.md), the `File` resource.</span></span> <span data-ttu-id="f0c8f-119">Prostředky vykonávají práci třeba zajistit, který cílový uzel je ve stavu, které jsou definované v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-119">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="f0c8f-120">Kompilace konfigurace</span><span class="sxs-lookup"><span data-stu-id="f0c8f-120">Compile the configuration</span></span>

<span data-ttu-id="f0c8f-121">Pro konfiguraci DSC, kterou chcete použít pro uzel je nutné nejprve být zkompilován do souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-121">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="f0c8f-122">Spouštění konfigurace, jako je funkce, zkompiluje jeden soubor "MOF" pro každý uzel určené `Node` bloku.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-122">Running the configuration, like a function, will compile one ".mof" file for every Node defined by the `Node` block.</span></span>
<span data-ttu-id="f0c8f-123">Pokud chcete spustit konfiguraci, je potřeba *tečkou zdroj* "HelloWorld.ps1" skript do aktuálního oboru.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-123">In order to run the configuration, you need to *dot source* your "HelloWorld.ps1" script into the current scope.</span></span>
<span data-ttu-id="f0c8f-124">Další informace najdete v tématu [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-124">For more information, see [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).</span></span>

<span data-ttu-id="f0c8f-125">*Zdroj tečkou* skriptu "HelloWorld.ps1" tak, že zadáte cestu, kam jste uložili, ho po `. ` (tečka, místo).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-125">*Dot source* your "HelloWorld.ps1" script by typing in the path where you stored it, after the `. ` (dot, space).</span></span> <span data-ttu-id="f0c8f-126">Potom můžete spustit konfiguraci voláním jako funkce.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-126">You may then, run your configuration by calling it like a Function.</span></span>

```powershell
. C:\Scripts\WebsiteTest.ps1
HelloWolrd
```

<span data-ttu-id="f0c8f-127">Tím se vygeneruje následující výstup:</span><span class="sxs-lookup"><span data-stu-id="f0c8f-127">This generates the following output:</span></span>

```output
Directory: C:\Scripts\HelloWorld


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

## <a name="apply-the-configuration"></a><span data-ttu-id="f0c8f-128">Použít konfiguraci</span><span class="sxs-lookup"><span data-stu-id="f0c8f-128">Apply the configuration</span></span>

<span data-ttu-id="f0c8f-129">Teď, když máte zkompilovaný soubor MOF, můžete provést konfiguraci na cílový uzel (v tomto případě místní počítač) pomocí volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-129">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

<span data-ttu-id="f0c8f-130">`Start-DscConfiguration` Říká rutiny [místní Configuration Manageru (LCM)](../managing-nodes/metaConfig.md), modulu DSC, chcete-li použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-130">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md), the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="f0c8f-131">LCM provádí volání prostředky DSC můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-131">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="f0c8f-132">Použít níže uvedený kód ke spuštění `Start-DSCConfiguration` rutiny.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-132">Use the code below to execute the `Start-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="f0c8f-133">Zadejte vaše "localhost.mof" se mají ukládat do cesta k adresáři `-Path` parametru.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-133">Specify the directory path where your "localhost.mof" is stored to the `-Path` parameter.</span></span> <span data-ttu-id="f0c8f-134">`Start-DSCConfiguration` Rutiny prohlédne do adresáře určeného pro všechny "\<computername\>.mof" soubory.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-134">The `Start-DSCConfiguration` cmdlet looks through the directory specified for any "\<computername\>.mof" files.</span></span> <span data-ttu-id="f0c8f-135">`Start-DSCConfiguration` Rutina se pokusí použít každý soubor "MOF", které nalezne na název určený název souboru ("localhost", "server01", "dc-02" atd.).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-135">The `Start-DSCConfiguration` cmdlet attempts to apply each ".mof" file it finds to the computername specified by the filename ("localhost", "server01", "dc-02", etc.).</span></span>

> [!NOTE]
> <span data-ttu-id="f0c8f-136">Pokud `-Wait` parametr není zadán, `Start-DSCConfiguration` vytvoří úlohu na pozadí k provedení této operace.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-136">If the `-Wait` parameter is not specified, `Start-DSCConfiguration` creates a background job to perform the operation.</span></span> <span data-ttu-id="f0c8f-137">Zadání `-Verbose` parametr umožňuje sledovat **Verbose** výstupní operace.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-137">Specifying the `-Verbose` parameter allows you to watch the **Verbose** output of the operation.</span></span> <span data-ttu-id="f0c8f-138">`-Wait`, a `-Verbose` jsou obě volitelné parametry.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-138">`-Wait`, and `-Verbose` are both optional parameters.</span></span>

```powershell
Start-DscConfiguration -Path C:\Scripts\HelloWorld -Verbose -Wait
```

## <a name="test-the-configuration"></a><span data-ttu-id="f0c8f-139">Otestujte konfiguraci</span><span class="sxs-lookup"><span data-stu-id="f0c8f-139">Test the configuration</span></span>

<span data-ttu-id="f0c8f-140">Jakmile `Start-DSCConfiguration` dokončení rutiny, měli byste vidět soubor "HelloWorld.txt" v zadaném umístění.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-140">Once the `Start-DSCConfiguration` cmdlet is complete, you should see a "HelloWorld.txt" file in the location you specified.</span></span> <span data-ttu-id="f0c8f-141">Můžete ověřit obsah s [Get-Content](/powershell/module/microsoft.powershell.management/get-content) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-141">You can verify the contents with the [Get-Content](/powershell/module/microsoft.powershell.management/get-content) cmdlet.</span></span>

<span data-ttu-id="f0c8f-142">Můžete také *testování* aktuální stav pomocí [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-142">You can also *test* the current status using [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span></span>

<span data-ttu-id="f0c8f-143">Výstup by měl "True", pokud uzel je nyní kompatibilní s použité konfigurace.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-143">The output should be "True" if the Node is currently compliant with the applied Configuration.</span></span>

```powershell
Test-DSCConfiguration
```

```output
True
```

```powershell
Get-Content -Path C:\Temp\HelloWorld.txt
```

```output
Hello World from DSC!
```

## <a name="re-applying-the-configuration"></a><span data-ttu-id="f0c8f-144">Opětovné použití konfigurace</span><span class="sxs-lookup"><span data-stu-id="f0c8f-144">Re-applying the configuration</span></span>

<span data-ttu-id="f0c8f-145">Zobrazit konfiguraci znovu použije, můžete odebrat textový soubor vytvořil konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-145">To see your configuration get applied again, you can remove the text file created by your Configuration.</span></span> <span data-ttu-id="f0c8f-146">Použití `Start-DSCConfiguration` rutinu s `-UseExisting` parametru.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-146">The use the `Start-DSCConfiguration` cmdlet with the `-UseExisting` parameter.</span></span> <span data-ttu-id="f0c8f-147">`-UseExisting` Nastaví parametr `Start-DSCConfiguration` znovu použít soubor "current.mof", která představuje naposledy úspěšně použili konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f0c8f-147">The `-UseExisting` parameter instructs `Start-DSCConfiguration` to re-apply the "current.mof" file, which represents the most recently successfully applied configuration.</span></span>

```powershell
Remove-Item -Path C:\Temp\HelloWorld.txt
```

## <a name="next-steps"></a><span data-ttu-id="f0c8f-148">Další kroky</span><span class="sxs-lookup"><span data-stu-id="f0c8f-148">Next steps</span></span>

- <span data-ttu-id="f0c8f-149">Další informace o konfiguracích DSC na [konfigurací DSC](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-149">Find out more about DSC configurations at [DSC configurations](configurations.md).</span></span>
- <span data-ttu-id="f0c8f-150">Podívejte se, jaké prostředky DSC jsou k dispozici a jak vytvořit vlastní prostředky DSC na [prostředky DSC](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-150">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](../resources/resources.md).</span></span>
- <span data-ttu-id="f0c8f-151">Najděte prostředky v a konfigurace DSC [Galerie prostředí PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="f0c8f-151">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>

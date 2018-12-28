---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Rychlý start – vytvoření webu s DSC
ms.openlocfilehash: c62e2d8af46bf74c4dd13069ddff6cc39763a209
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403634"
---
> <span data-ttu-id="7e743-103">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7e743-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="quickstart---create-a-website-with-dsc"></a><span data-ttu-id="7e743-104">Rychlý start – vytvoření webu s DSC</span><span class="sxs-lookup"><span data-stu-id="7e743-104">Quickstart - Create a website with DSC</span></span>

<span data-ttu-id="7e743-105">V tomto cvičení vás provedou vytvořením a aplikování konfigurace Desired State Configuration (DSC) od začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="7e743-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="7e743-106">Příklad použijeme zajistí, že je na serveru `Web-Server` povolena funkce (služby IIS), a je k dispozici v obsahu pro jednoduchý web "Hello World" `intepub\wwwroot` adresáře tohoto serveru.</span><span class="sxs-lookup"><span data-stu-id="7e743-106">The example we'll use ensures that a server has the `Web-Server` (IIS) feature enabled, and that the content for a simple "Hello World" website is present in the `intepub\wwwroot` directory of that server.</span></span>

<span data-ttu-id="7e743-107">Přehled o novinkách DSC a jak to funguje, najdete v části [Desired State Configuration přehled pro pracovníky s rozhodovací pravomocí](../overview/decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="7e743-107">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Decision Makers](../overview/decisionMaker.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="7e743-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="7e743-108">Requirements</span></span>

<span data-ttu-id="7e743-109">Chcete-li spustit tento příklad, musíte počítač se systémem Windows Server 2012 nebo novější a prostředí PowerShell 4.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="7e743-109">To run this example, you will need a computer running Windows Server 2012 or later and PowerShell 4.0 or later.</span></span>

## <a name="write-and-place-the-indexhtm-file"></a><span data-ttu-id="7e743-110">Zápis a umístěte soubor index.htm</span><span class="sxs-lookup"><span data-stu-id="7e743-110">Write and place the index.htm file</span></span>

<span data-ttu-id="7e743-111">Nejprve vytvoříme soubor HTML, který budeme používat jako obsah webu.</span><span class="sxs-lookup"><span data-stu-id="7e743-111">First, we'll create the HTML file that we will use as the website content.</span></span>

<span data-ttu-id="7e743-112">V kořenové složce vytvořte složku s názvem `test`.</span><span class="sxs-lookup"><span data-stu-id="7e743-112">In your root folder, create a folder named `test`.</span></span>

<span data-ttu-id="7e743-113">V textovém editoru zadejte následující text:</span><span class="sxs-lookup"><span data-stu-id="7e743-113">In a text editor, type the following text:</span></span>

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

<span data-ttu-id="7e743-114">Uložit jako `index.htm` v `test` složky, které jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="7e743-114">Save this as `index.htm` in the `test` folder you created earlier.</span></span>

## <a name="write-the-configuration"></a><span data-ttu-id="7e743-115">Zapsat konfiguraci</span><span class="sxs-lookup"><span data-stu-id="7e743-115">Write the configuration</span></span>

<span data-ttu-id="7e743-116">A [konfigurace DSC](../configurations/configurations.md) je speciální funkce prostředí PowerShell, který definuje, jak chcete nakonfigurovat jeden nebo více cílových počítačů (uzlů).</span><span class="sxs-lookup"><span data-stu-id="7e743-116">A [DSC configuration](../configurations/configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (nodes).</span></span>

<span data-ttu-id="7e743-117">V prostředí PowerShell ISE zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="7e743-117">In the PowerShell ISE, type the following:</span></span>

```powershell
Configuration WebsiteTest {

    # Import the module that contains the resources we're using.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets this configuration will be applied to.
    Node 'localhost' {

        # The first resource block ensures that the Web-Server (IIS) feature is enabled.
        WindowsFeature WebServer {
            Ensure = "Present"
            Name   = "Web-Server"
        }

        # The second resource block ensures that the website content copied to the website root folder.
        File WebsiteContent {
            Ensure = 'Present'
            SourcePath = 'c:\test\index.htm'
            DestinationPath = 'c:\inetpub\wwwroot'
        }
    }
}
```

<span data-ttu-id="7e743-118">Uložte soubor jako `WebsiteTest.ps1`.</span><span class="sxs-lookup"><span data-stu-id="7e743-118">Save the file as `WebsiteTest.ps1`.</span></span>

<span data-ttu-id="7e743-119">Uvidíte, že to vypadá funkce prostředí PowerShell, a uveďte klíčového slova **konfigurace** nepoužili název funkce.</span><span class="sxs-lookup"><span data-stu-id="7e743-119">You can see that it looks like a PowerShell function, with the addition of the keyword **Configuration** used before the name of the function.</span></span>

<span data-ttu-id="7e743-120">**Uzel** bloku Určuje cílový uzel nakonfigurovat, v tomto případě `localhost`.</span><span class="sxs-lookup"><span data-stu-id="7e743-120">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="7e743-121">Konfigurace vyžaduje dvě [prostředky](../resources/resources.md), **WindowsFeature** a **souboru**.</span><span class="sxs-lookup"><span data-stu-id="7e743-121">The configuration calls two [resources](../resources/resources.md), **WindowsFeature** and **File**.</span></span>
<span data-ttu-id="7e743-122">Prostředky vykonávají práci třeba zajistit, který cílový uzel je ve stavu, které jsou definované v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="7e743-122">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="7e743-123">Kompilace konfigurace</span><span class="sxs-lookup"><span data-stu-id="7e743-123">Compile the configuration</span></span>

<span data-ttu-id="7e743-124">Pro konfiguraci DSC, kterou chcete použít pro uzel je nutné nejprve být zkompilován do souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="7e743-124">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="7e743-125">K tomuto účelu spustit konfiguraci jako funkce.</span><span class="sxs-lookup"><span data-stu-id="7e743-125">To do this, you run the configuration like a function.</span></span>
<span data-ttu-id="7e743-126">V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkazy ke kompilaci konfigurace do souboru MOF:</span><span class="sxs-lookup"><span data-stu-id="7e743-126">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following commands to compile the configuration into a MOF file:</span></span>

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

<span data-ttu-id="7e743-127">Tím se vygeneruje následující výstup:</span><span class="sxs-lookup"><span data-stu-id="7e743-127">This generates the following output:</span></span>

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

<span data-ttu-id="7e743-128">První řádek provede konfiguraci funkce dostupné v konzole.</span><span class="sxs-lookup"><span data-stu-id="7e743-128">The first line makes the configuration function available in the console.</span></span>
<span data-ttu-id="7e743-129">Druhý řádek se spustí v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="7e743-129">The second line runs the configuration.</span></span>
<span data-ttu-id="7e743-130">Výsledkem je, že novou složku s názvem `WebsiteTest` je vytvořen jako podsložky do aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="7e743-130">The result is that a new folder, named `WebsiteTest` is created as a subfolder of the current folder.</span></span>
<span data-ttu-id="7e743-131">`WebsiteTest` Složka obsahuje soubor s názvem `localhost.mof`.</span><span class="sxs-lookup"><span data-stu-id="7e743-131">The `WebsiteTest` folder contains a file named `localhost.mof`.</span></span>
<span data-ttu-id="7e743-132">Je tento soubor, který lze následně použít na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="7e743-132">It is this file that can then be applied to the target node.</span></span>

## <a name="apply-the-configuration"></a><span data-ttu-id="7e743-133">Použít konfiguraci</span><span class="sxs-lookup"><span data-stu-id="7e743-133">Apply the configuration</span></span>

<span data-ttu-id="7e743-134">Teď, když máte zkompilovaný soubor MOF, můžete provést konfiguraci na cílový uzel (v tomto případě místní počítač) pomocí volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="7e743-134">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

<span data-ttu-id="7e743-135">`Start-DscConfiguration` Říká rutiny [místní Configuration Manageru (LCM)](../managing-nodes/metaConfig.md), což je modul DSC, chcete-li použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="7e743-135">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md), which is the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="7e743-136">LCM provádí volání prostředky DSC můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="7e743-136">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="7e743-137">V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="7e743-137">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following command:</span></span>

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a><span data-ttu-id="7e743-138">Otestujte konfiguraci</span><span class="sxs-lookup"><span data-stu-id="7e743-138">Test the configuration</span></span>

<span data-ttu-id="7e743-139">Můžete volat [Get-DscConfigurationStatus](/powershell/module/psdesiredstateconfiguration/get-dscconfigurationstatus) rutiny zobrazíte, jestli konfigurace proběhla úspěšně.</span><span class="sxs-lookup"><span data-stu-id="7e743-139">You can call the [Get-DscConfigurationStatus](/powershell/module/psdesiredstateconfiguration/get-dscconfigurationstatus) cmdlet to see whether the configuration succeeded.</span></span>

<span data-ttu-id="7e743-140">Můžete také otestovat výsledky přímo, v tomto případě tak, že přejdete do `http://localhost/` ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="7e743-140">You can also test the results directly, in this case by browsing to `http://localhost/` in a web browser.</span></span>
<span data-ttu-id="7e743-141">Jako první krok v tomto příkladu byste měli vidět "Hello World" HTML stránka, kterou jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="7e743-141">You should see the "Hello World" HTML page you created as the first step in this example.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e743-142">Další kroky</span><span class="sxs-lookup"><span data-stu-id="7e743-142">Next steps</span></span>

- <span data-ttu-id="7e743-143">Další informace o konfiguracích DSC na [konfigurací DSC](../configurations/configurations.md).</span><span class="sxs-lookup"><span data-stu-id="7e743-143">Find out more about DSC configurations at [DSC configurations](../configurations/configurations.md).</span></span>
- <span data-ttu-id="7e743-144">Podívejte se, jaké prostředky DSC jsou k dispozici a jak vytvořit vlastní prostředky DSC na [prostředky DSC](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="7e743-144">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](../resources/resources.md).</span></span>
- <span data-ttu-id="7e743-145">Najděte prostředky v a konfigurace DSC [Galerie prostředí PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="7e743-145">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>

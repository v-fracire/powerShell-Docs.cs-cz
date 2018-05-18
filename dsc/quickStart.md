---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Desired State Configuration rychlý Start
ms.openlocfilehash: eb7572f39f7a2710c82f132f42c3502b15c48d0f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
> <span data-ttu-id="60cd1-103">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="60cd1-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="desired-state-configuration-quick-start"></a><span data-ttu-id="60cd1-104">Desired State Configuration rychlý Start</span><span class="sxs-lookup"><span data-stu-id="60cd1-104">Desired State Configuration Quick Start</span></span>

<span data-ttu-id="60cd1-105">Tento postup vás provede vytvořením a použitím konfiguraci konfigurace požadovaného stavu (DSC) od začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="60cd1-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="60cd1-106">V příkladu použijeme zajistí, že má server `Web-Server` povolena funkce (IIS) a která je k dispozici v obsahu pro jednoduchý web "Hello World" `intepub\wwwroot` adresáři z tohoto serveru.</span><span class="sxs-lookup"><span data-stu-id="60cd1-106">The example we'll use ensures that a server has the `Web-Server` (IIS) feature enabled, and that the content for a simple "Hello World" website is present in the `intepub\wwwroot` directory of that server.</span></span>

<span data-ttu-id="60cd1-107">Přehled DSC a jak to funguje, najdete v tématu [potřeby přehled stavu konfigurace pro rozhodují](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="60cd1-107">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="60cd1-108">Požadavky</span><span class="sxs-lookup"><span data-stu-id="60cd1-108">Requirements</span></span>

<span data-ttu-id="60cd1-109">Pokud chcete spustit tento příklad, budete potřebovat počítač se systémem Windows Server 2012 nebo novější a prostředí PowerShell 4.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="60cd1-109">To run this example, you will need a computer running Windows Server 2012 or later and PowerShell 4.0 or later.</span></span>

## <a name="write-and-place-the-indexhtm-file"></a><span data-ttu-id="60cd1-110">Zápis a umístěte soubor index.htm</span><span class="sxs-lookup"><span data-stu-id="60cd1-110">Write and place the index.htm file</span></span>

<span data-ttu-id="60cd1-111">Nejdříve vytvoříme soubor HTML, který budeme používat jako obsah webu.</span><span class="sxs-lookup"><span data-stu-id="60cd1-111">First, we'll create the HTML file that we will use as the website content.</span></span>

<span data-ttu-id="60cd1-112">V kořenové složce, vytvořte složku s názvem `test`.</span><span class="sxs-lookup"><span data-stu-id="60cd1-112">In your root folder, create a folder named `test`.</span></span>

<span data-ttu-id="60cd1-113">V textovém editoru zadejte následující text:</span><span class="sxs-lookup"><span data-stu-id="60cd1-113">In a text editor, type the following text:</span></span>

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

<span data-ttu-id="60cd1-114">Uložit jako `index.htm` v `test` složky, které jste vytvořili dříve.</span><span class="sxs-lookup"><span data-stu-id="60cd1-114">Save this as `index.htm` in the `test` folder you created earlier.</span></span>

## <a name="write-the-configuration"></a><span data-ttu-id="60cd1-115">Zápis konfigurace</span><span class="sxs-lookup"><span data-stu-id="60cd1-115">Write the configuration</span></span>

<span data-ttu-id="60cd1-116">A [konfigurace DSC](configurations.md) je speciální funkce prostředí PowerShell, která definuje, jak chcete nakonfigurovat jeden nebo více cílových počítačů (uzlů).</span><span class="sxs-lookup"><span data-stu-id="60cd1-116">A [DSC configuration](configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (nodes).</span></span>

<span data-ttu-id="60cd1-117">V integrovaném Skriptovacím prostředí PowerShell zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="60cd1-117">In the PowerShell ISE, type the following:</span></span>

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

<span data-ttu-id="60cd1-118">Uložte soubor jako `WebsiteTest.ps1`.</span><span class="sxs-lookup"><span data-stu-id="60cd1-118">Save the file as `WebsiteTest.ps1`.</span></span>

<span data-ttu-id="60cd1-119">Uvidíte, že to vypadá funkce prostředí PowerShell, a uveďte klíčové slovo **konfigurace** používali před název funkce.</span><span class="sxs-lookup"><span data-stu-id="60cd1-119">You can see that it looks like a PowerShell function, with the addition of the keyword **Configuration** used before the name of the function.</span></span>

<span data-ttu-id="60cd1-120">**Uzlu** bloku Určuje cílový uzel potřeba nakonfigurovat v tomto případě `localhost`.</span><span class="sxs-lookup"><span data-stu-id="60cd1-120">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="60cd1-121">Konfigurace volá dva [prostředky](resources.md), [WindowsFeature](windowsFeatureResource.md) a [soubor](fileResource.md).</span><span class="sxs-lookup"><span data-stu-id="60cd1-121">The configuration calls two [resources](resources.md), [WindowsFeature](windowsFeatureResource.md) and [File](fileResource.md).</span></span>
<span data-ttu-id="60cd1-122">Prostředky udělají tuto práci zajistit, který cílový uzel je ve stavu definované v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="60cd1-122">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="60cd1-123">Konfigurace kompilace</span><span class="sxs-lookup"><span data-stu-id="60cd1-123">Compile the configuration</span></span>

<span data-ttu-id="60cd1-124">Pro konfiguraci DSC, kterou chcete použít k uzlu je nutné nejprve být zkompilován do souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="60cd1-124">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="60cd1-125">K tomu spusťte konfigurace jako funkce.</span><span class="sxs-lookup"><span data-stu-id="60cd1-125">To do this, you run the configuration like a function.</span></span>
<span data-ttu-id="60cd1-126">V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkazy ke kompilaci konfigurace do souboru MOF:</span><span class="sxs-lookup"><span data-stu-id="60cd1-126">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following commands to compile the configuration into a MOF file:</span></span>

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

<span data-ttu-id="60cd1-127">To vygeneruje následující výstup:</span><span class="sxs-lookup"><span data-stu-id="60cd1-127">This generates the following output:</span></span>

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

<span data-ttu-id="60cd1-128">První řádek zpřístupní funkce konfigurace v konzole.</span><span class="sxs-lookup"><span data-stu-id="60cd1-128">The first line makes the configuration function available in the console.</span></span>
<span data-ttu-id="60cd1-129">Druhý řádek se spustí v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="60cd1-129">The second line runs the configuration.</span></span>
<span data-ttu-id="60cd1-130">Výsledkem je, že novou složku s názvem `WebsiteTest` je vytvořen jako podsložkou aktuální složky.</span><span class="sxs-lookup"><span data-stu-id="60cd1-130">The result is that a new folder, named `WebsiteTest` is created as a subfolder of the current folder.</span></span>
<span data-ttu-id="60cd1-131">`WebsiteTest` Složka obsahuje soubor s názvem `localhost.mof`.</span><span class="sxs-lookup"><span data-stu-id="60cd1-131">The `WebsiteTest` folder contains a file named `localhost.mof`.</span></span>
<span data-ttu-id="60cd1-132">Je tento soubor, který lze použít na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="60cd1-132">It is this file that can then be applied to the target node.</span></span>

## <a name="apply-the-configuration"></a><span data-ttu-id="60cd1-133">Použít konfiguraci</span><span class="sxs-lookup"><span data-stu-id="60cd1-133">Apply the configuration</span></span>

<span data-ttu-id="60cd1-134">Teď, když máte kompilované MOF, můžete použít konfiguraci na cílovém uzlu (v tomto případě místní počítač) pomocí volání [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="60cd1-134">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) cmdlet.</span></span>

<span data-ttu-id="60cd1-135">`Start-DscConfiguration` Rutiny informuje [místní Configuration Manager (LCM)](metaConfig.md), což je modul DSC, můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="60cd1-135">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](metaConfig.md), which is the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="60cd1-136">LCM funguje volání prostředky DSC můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="60cd1-136">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="60cd1-137">V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="60cd1-137">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following command:</span></span>

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a><span data-ttu-id="60cd1-138">Otestujte konfiguraci</span><span class="sxs-lookup"><span data-stu-id="60cd1-138">Test the configuration</span></span>

<span data-ttu-id="60cd1-139">Můžete volat [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) rutiny zobrazíte, jestli konfigurace byla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="60cd1-139">You can call the [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) cmdlet to see whether the configuration succeeded.</span></span>

<span data-ttu-id="60cd1-140">Můžete také otestovat výsledky přímo, v takovém případě procházením `http://localhost/` ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="60cd1-140">You can also test the results directly, in this case by browsing to `http://localhost/` in a web browser.</span></span>
<span data-ttu-id="60cd1-141">Měli byste vidět "Hello, World" HTML stránka, kterou jste vytvořili jako první krok v tomto příkladu.</span><span class="sxs-lookup"><span data-stu-id="60cd1-141">You should see the "Hello World" HTML page you created as the first step in this example.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60cd1-142">Další kroky</span><span class="sxs-lookup"><span data-stu-id="60cd1-142">Next steps</span></span>

- <span data-ttu-id="60cd1-143">Další informace o konfiguracích DSC v [konfigurace DSC](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="60cd1-143">Find out more about DSC configurations at [DSC configurations](configurations.md).</span></span>
- <span data-ttu-id="60cd1-144">Jaké prostředky DSC jsou k dispozici a jak vytvořit vlastní prostředky DSC v [prostředky DSC](resources.md).</span><span class="sxs-lookup"><span data-stu-id="60cd1-144">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](resources.md).</span></span>
- <span data-ttu-id="60cd1-145">Najít konfigurace DSC a prostředky v [Galerie prostředí PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="60cd1-145">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
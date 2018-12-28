---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Vytváření procesních toků pro průběžnou integraci a průběžné nasazování s DSC
ms.openlocfilehash: c305d9bc7e0f8c659129b5a20d0b7e8b34d09ba8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403824"
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a><span data-ttu-id="1bfc1-103">Vytváření procesních toků pro průběžnou integraci a průběžné nasazování s DSC</span><span class="sxs-lookup"><span data-stu-id="1bfc1-103">Building a Continuous Integration and Continuous Deployment pipeline with DSC</span></span>

<span data-ttu-id="1bfc1-104">Tento příklad ukazuje, jak vytvořit kanál průběžné integrace a průběžného nasazování (CI/CD) s použitím prostředí PowerShell, DSC, Pester a Visual Studio Team Foundation Server (TFS).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-104">This example demonstrates how to build a Continuous Integration/Continuous Deployment (CI/CD) pipeline by using PowerShell, DSC, Pester, and Visual Studio Team Foundation Server (TFS).</span></span>

<span data-ttu-id="1bfc1-105">Po vytvoření kanálu a nakonfigurované, můžete použít plně nasazení, testování a konfigurace serveru DNS a související záznamy hostitele.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-105">After the pipeline is built and configured, you can use it to fully deploy, configure and test a DNS server and associated host records.</span></span>
<span data-ttu-id="1bfc1-106">Tento proces simuluje první část kanál, který se použije ve vývojovém prostředí.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-106">This process simulates the first part of a pipeline that would be used in a development environment.</span></span>

<span data-ttu-id="1bfc1-107">Automatizovaný kanál CI/CD vám pomůže aktualizovat software rychleji a spolehlivěji, zajištění, že je testován veškerý kód, a zda je aktuální sestavení kódu vždy k dispozici.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-107">An automated CI/CD pipeline helps you update software faster and more reliably, ensuring that all code is tested, and that a current build of your code is available at all times.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bfc1-108">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="1bfc1-108">Prerequisites</span></span>

<span data-ttu-id="1bfc1-109">Chcete-li použít tento příklad, měli seznámit s následujícími možnostmi:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-109">To use this example, you should be familiar with the following:</span></span>

- <span data-ttu-id="1bfc1-110">Koncepty CI-CD.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-110">CI-CD concepts.</span></span> <span data-ttu-id="1bfc1-111">Najdete vhodné reference na [The Model kanálu verze](http://aka.ms/thereleasepipelinemodelpdf).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-111">A good reference can be found at [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf).</span></span>
- <span data-ttu-id="1bfc1-112">[Git](https://git-scm.com/) správy zdrojového kódu</span><span class="sxs-lookup"><span data-stu-id="1bfc1-112">[Git](https://git-scm.com/) source control</span></span>
- <span data-ttu-id="1bfc1-113">[Pester](https://github.com/pester/Pester) testování</span><span class="sxs-lookup"><span data-stu-id="1bfc1-113">The [Pester](https://github.com/pester/Pester) testing framework</span></span>
- [<span data-ttu-id="1bfc1-114">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="1bfc1-114">Team Foundation Server</span></span>](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a><span data-ttu-id="1bfc1-115">Co budete potřebovat</span><span class="sxs-lookup"><span data-stu-id="1bfc1-115">What you will need</span></span>

<span data-ttu-id="1bfc1-116">Sestavit a spustit tento příklad, musíte v prostředí s několika počítačích nebo virtuálních počítačů.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-116">To build and run this example, you will need an environment with several computers and/or virtual machines.</span></span>

### <a name="client"></a><span data-ttu-id="1bfc1-117">Client</span><span class="sxs-lookup"><span data-stu-id="1bfc1-117">Client</span></span>

<span data-ttu-id="1bfc1-118">Toto je počítač, kde budete používat všechnu práci, nastavení a spuštění příkladu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-118">This is the computer where you'll do all of the work setting up and running the example.</span></span>

<span data-ttu-id="1bfc1-119">Klientský počítač musí být počítač Windows s nainstalované tyto položky:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-119">The client computer must be a Windows computer with the following installed:</span></span>

- [<span data-ttu-id="1bfc1-120">Git</span><span class="sxs-lookup"><span data-stu-id="1bfc1-120">Git</span></span>](https://git-scm.com/)
- <span data-ttu-id="1bfc1-121">naklonovat místního úložiště git z https://github.com/PowerShell/Demo_CI</span><span class="sxs-lookup"><span data-stu-id="1bfc1-121">a local git repo cloned from https://github.com/PowerShell/Demo_CI</span></span>
- <span data-ttu-id="1bfc1-122">textový editor, například [Visual Studio Code](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="1bfc1-122">a text editor, such as [Visual Studio Code](https://code.visualstudio.com/)</span></span>

### <a name="tfssrv1"></a><span data-ttu-id="1bfc1-123">TFSSrv1</span><span class="sxs-lookup"><span data-stu-id="1bfc1-123">TFSSrv1</span></span>

<span data-ttu-id="1bfc1-124">Počítač, který je hostitelem serveru TFS, kde bude definici sestavení a vydání.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-124">The computer that hosts the TFS server where you will define your build and release.</span></span>
<span data-ttu-id="1bfc1-125">Tento počítač musí mít [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) nainstalované.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-125">This computer must have [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) installed.</span></span>

### <a name="buildagent"></a><span data-ttu-id="1bfc1-126">BuildAgent</span><span class="sxs-lookup"><span data-stu-id="1bfc1-126">BuildAgent</span></span>

<span data-ttu-id="1bfc1-127">Počítač, na kterém běží Windows agenta sestavení, sestavení projektu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-127">The computer that runs the Windows build agent that builds the project.</span></span>
<span data-ttu-id="1bfc1-128">Tento počítač musí mít Windows nainstalovaný a spuštěný agent sestavení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-128">This computer must have a Windows build agent installed and running.</span></span>
<span data-ttu-id="1bfc1-129">Zobrazit [nasazení agenta ve Windows](/azure/devops/pipelines/agents/v2-windows) pro agenta sestavení pokyny o tom, jak nainstalovat a spustit Windows.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-129">See [Deploy an agent on Windows](/azure/devops/pipelines/agents/v2-windows) for instructions on how to install and run a Windows build agent.</span></span>

<span data-ttu-id="1bfc1-130">Budete také muset nainstalovat i `xDnsServer` a `xNetworking` moduly DSC na tomto počítači.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-130">You also need to install both the `xDnsServer` and `xNetworking` DSC modules on this computer.</span></span>

### <a name="testagent1"></a><span data-ttu-id="1bfc1-131">TestAgent1</span><span class="sxs-lookup"><span data-stu-id="1bfc1-131">TestAgent1</span></span>

<span data-ttu-id="1bfc1-132">To je počítač, který je nakonfigurovaný jako DNS server konfigurací DSC v tomto příkladu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-132">This is the computer that is configured as a DNS server by the DSC configuration in this example.</span></span>
<span data-ttu-id="1bfc1-133">Počítači musí běžet [Windows serveru 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-133">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

### <a name="testagent2"></a><span data-ttu-id="1bfc1-134">TestAgent2</span><span class="sxs-lookup"><span data-stu-id="1bfc1-134">TestAgent2</span></span>

<span data-ttu-id="1bfc1-135">Toto je počítač, který je hostitelem webu, který tento příklad konfiguruje.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-135">This is the computer that hosts the website this example configures.</span></span>
<span data-ttu-id="1bfc1-136">Počítači musí běžet [Windows serveru 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-136">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

## <a name="add-the-code-to-tfs"></a><span data-ttu-id="1bfc1-137">Přidejte kód do TFS</span><span class="sxs-lookup"><span data-stu-id="1bfc1-137">Add the code to TFS</span></span>

<span data-ttu-id="1bfc1-138">Začneme vytváření úložiště Git v sadě TFS a import kód ze svého místního úložiště na klientském počítači.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-138">We'll start out by creating a Git repository in TFS, and importing the code from your local repository on the client computer.</span></span>
<span data-ttu-id="1bfc1-139">Pokud nebyly již naklonované úložiště Demo_CI na klientském počítači, proveďte to teď spuštěním následujícího příkazu git:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-139">If you have not already cloned the Demo_CI repository to your client computer, do so now by running the following git command:</span></span>

`git clone https://github.com/PowerShell/Demo_CI`

1. <span data-ttu-id="1bfc1-140">Na klientském počítači přejděte na server TFS ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-140">On your client computer, navigate to your TFS server in a web browser.</span></span>
1. <span data-ttu-id="1bfc1-141">V sadě TFS [vytvořte nový týmový projekt](/azure/devops/organizations/projects/create-project) s názvem Demo_CI.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-141">In TFS, [Create a new team project](/azure/devops/organizations/projects/create-project) named Demo_CI.</span></span>

   <span data-ttu-id="1bfc1-142">Ujistěte se, že **verzí** je nastavena na **Git**.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-142">Make sure that **Version control** is set to **Git**.</span></span>
1. <span data-ttu-id="1bfc1-143">Na klientském počítači přidejte vzdálené úložiště, které jste právě vytvořili na serveru TFS pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-143">On your client computer, add a remote to the repository you just created in TFS with the following command:</span></span>

   `git remote add tfs <YourTFSRepoURL>`

   <span data-ttu-id="1bfc1-144">Kde `<YourTFSRepoURL>` je adresa URL klonování k TFS úložiště, kterou jste vytvořili v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-144">Where `<YourTFSRepoURL>` is the clone URL to the TFS repository you created in the previous step.</span></span>

   <span data-ttu-id="1bfc1-145">Pokud si nejste jisti, kde najít tuto adresu URL, najdete v článku [Naklonovat existující úložiště Git](/azure/devops/repos/git/clone).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-145">If you don't know where to find this URL, see [Clone an existing Git repo](/azure/devops/repos/git/clone).</span></span>
1. <span data-ttu-id="1bfc1-146">Vložit kód ze svého místního úložiště do vašeho úložiště TFS pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-146">Push the code from your local repository to your TFS repository with the following command:</span></span>

   `git push tfs --all`
1. <span data-ttu-id="1bfc1-147">Úložiště TFS naplní Demo_CI kódu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-147">The TFS repository will be populated with the Demo_CI code.</span></span>

> [!NOTE]
> <span data-ttu-id="1bfc1-148">V tomto příkladu kódu v `ci-cd-example` větve úložiště Git.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-148">This example uses the code in the `ci-cd-example` branch of the Git repo.</span></span>
> <span data-ttu-id="1bfc1-149">Nezapomeňte zadat tuto větev jako výchozí větev ve vašem projektu TFS a pro aktivační události CI/CD, který vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-149">Be sure to specify this branch as the default branch in your TFS project, and for the CI/CD triggers you create.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="1bfc1-150">Porozumění kódu</span><span class="sxs-lookup"><span data-stu-id="1bfc1-150">Understanding the code</span></span>

<span data-ttu-id="1bfc1-151">Než vytvoříme kanály sestavení a nasazení, Pojďme se podívat na některé z kódu pochopit, co se děje.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-151">Before we create the build and deployment pipelines, let's look at some of the code to understand what is going on.</span></span>
<span data-ttu-id="1bfc1-152">Na klientském počítači otevřete oblíbený textový editor a přejděte do kořenového adresáře úložiště Demo_CI Git.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-152">On your client computer, open your favorite text editor and navigate to the root of your Demo_CI Git repository.</span></span>

### <a name="the-dsc-configuration"></a><span data-ttu-id="1bfc1-153">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="1bfc1-153">The DSC configuration</span></span>

<span data-ttu-id="1bfc1-154">Otevřete soubor `DNSServer.ps1` (z kořenového adresáře místního úložiště Demo_CI `./InfraDNS/Configs/DNSServer.ps1`).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-154">Open the file `DNSServer.ps1` (from the root of the local Demo_CI repository, `./InfraDNS/Configs/DNSServer.ps1`).</span></span>

<span data-ttu-id="1bfc1-155">Tento soubor obsahuje konfiguraci DSC, která slouží k nastavení serveru DNS.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-155">This file contains the DSC configuration that sets up the DNS server.</span></span> <span data-ttu-id="1bfc1-156">Tady je v celém rozsahu:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-156">Here it is in its entirety:</span></span>

```powershell
configuration DNSServer
{
    Import-DscResource -module 'xDnsServer','xNetworking', 'PSDesiredStateConfiguration'

    Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
    {
        WindowsFeature DNS
        {
            Ensure  = 'Present'
            Name    = 'DNS'
        }

        xDnsServerPrimaryZone $Node.zone
        {
            Ensure    = 'Present'
            Name      = $Node.Zone
            DependsOn = '[WindowsFeature]DNS'
        }

        foreach ($ARec in $Node.ARecords.keys) {
            xDnsRecord $ARec
            {
                Ensure    = 'Present'
                Name      = $ARec
                Zone      = $Node.Zone
                Type      = 'ARecord'
                Target    = $Node.ARecords[$ARec]
                DependsOn = '[WindowsFeature]DNS'
            }
        }

        foreach ($CName in $Node.CNameRecords.keys) {
            xDnsRecord $CName
            {
                Ensure    = 'Present'
                Name      = $CName
                Zone      = $Node.Zone
                Type      = 'CName'
                Target    = $Node.CNameRecords[$CName]
                DependsOn = '[WindowsFeature]DNS'
            }
        }
    }
}
```

<span data-ttu-id="1bfc1-157">Všimněte si, že `Node` – příkaz:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-157">Notice the `Node` statement:</span></span>

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

<span data-ttu-id="1bfc1-158">To najde všechny uzly, které byly definovány jako s rolí `DNSServer` v [konfigurační data](../configurations/configData.md), který je vytvořen `DevEnv.ps1` skriptu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-158">This finds any nodes that were defined as having a role of `DNSServer` in the [configuration data](../configurations/configData.md), which is created by the `DevEnv.ps1` script.</span></span>

<span data-ttu-id="1bfc1-159">Další informace o `Where` metoda [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span><span class="sxs-lookup"><span data-stu-id="1bfc1-159">You can read more about the `Where` method in [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span></span>

<span data-ttu-id="1bfc1-160">Definování uzly pomocí konfiguračních dat je důležité při provádění položky konfigurace, protože informace o uzlu se pravděpodobně změní mezi prostředími a pomocí konfigurační data můžete snadno změnit informace o uzlu beze změny kódu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-160">Using configuration data to define nodes is important when doing CI because node information will likely change between environments, and using configuration data allows you to easily make changes to node information without changing the configuration code.</span></span>

<span data-ttu-id="1bfc1-161">V prvním bloku prostředek konfigurace volá **WindowsFeature** zajistit, že je povolena funkce DNS.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-161">In the first resource block, the configuration calls the **WindowsFeature** to ensure that the DNS feature is enabled.</span></span>
<span data-ttu-id="1bfc1-162">Bloky prostředků, které následují volání zdroje z [xDnsServer](https://github.com/PowerShell/xDnsServer) modulu, který chcete konfigurovat zóny a záznamy DNS.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-162">The resource blocks that follow call resources from the [xDnsServer](https://github.com/PowerShell/xDnsServer) module to configure the primary zone and DNS records.</span></span>

<span data-ttu-id="1bfc1-163">Všimněte si, že dva `xDnsRecord` bloky jsou zabaleny v `foreach` smyček, které iteraci přes pole v konfiguračních datech.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-163">Notice that the two `xDnsRecord` blocks are wrapped in `foreach` loops that iterate through arrays in the configuration data.</span></span>
<span data-ttu-id="1bfc1-164">Znovu vytvoří konfigurační data `DevEnv.ps1` skript, který se podíváme na další.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-164">Again, the configuration data is created by the `DevEnv.ps1` script, which we'll look at next.</span></span>

### <a name="configuration-data"></a><span data-ttu-id="1bfc1-165">Konfigurační data</span><span class="sxs-lookup"><span data-stu-id="1bfc1-165">Configuration data</span></span>

<span data-ttu-id="1bfc1-166">`DevEnv.ps1` Souboru (z kořenového adresáře místního úložiště Demo_CI `./InfraDNS/DevEnv.ps1`) určuje specifických pro prostředí konfigurační data v zatřiďovací tabulku a pak předá tento zatřiďovací tabulky na volání `New-DscConfigurationDataDocument` funkce, která je definována v `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-166">The `DevEnv.ps1` file (from the root of the local Demo_CI repository, `./InfraDNS/DevEnv.ps1`) specifies the environment-specific configuration data in a hashtable, and then passes that hashtable to a call to the `New-DscConfigurationDataDocument` function, which is defined in `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span></span>

<span data-ttu-id="1bfc1-167">`DevEnv.ps1` Souboru:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-167">The `DevEnv.ps1` file:</span></span>

```powershell
param(
    [parameter(Mandatory=$true)]
    [string]
    $OutputPath
)

Import-Module $PSScriptRoot\..\Assets\DscPipelineTools\DscPipelineTools.psd1 -Force

# Define Unit Test Environment
$DevEnvironment = @{
    Name                        = 'DevEnv';
    Roles = @(
        @{  Role                = 'DNSServer';
            VMName              = 'TestAgent1';
            Zone                = 'Contoso.com';
            ARecords            = @{'TFSSrv1'= '10.0.0.10';'Client'='10.0.0.15';'BuildAgent'='10.0.0.30';'TestAgent1'='10.0.0.40';'TestAgent2'='10.0.0.50'};
            CNameRecords        = @{'DNS' = 'TestAgent1.contoso.com'};
        }
    )
}

Return New-DscConfigurationDataDocument -RawEnvData $DevEnvironment -OutputPath $OutputPath
```

<span data-ttu-id="1bfc1-168">`New-DscConfigurationDataDocument` – Funkce (definované v `\Assets\DscPipelineTools\DscPipelineTools.psm1`) prostřednictvím kódu programu vytvoří konfigurační data dokumentu z zatřiďovací tabulky (data uzlu) a pole (data bez uzlu), které jsou předány jako `RawEnvData` a `OtherEnvData` parametry.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-168">The `New-DscConfigurationDataDocument` function (defined in `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programmatically creates a configuration data document from the hashtable (node data) and array (non-node data) that are passed as the `RawEnvData` and `OtherEnvData` parameters.</span></span>

<span data-ttu-id="1bfc1-169">V našem případě pouze `RawEnvData` parametr se používá.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-169">In our case, only the `RawEnvData` parameter is used.</span></span>

### <a name="the-psake-build-script"></a><span data-ttu-id="1bfc1-170">Skript sestavení psake</span><span class="sxs-lookup"><span data-stu-id="1bfc1-170">The psake build script</span></span>

<span data-ttu-id="1bfc1-171">[Psake](https://github.com/psake/psake) skript definovaný v sestavení `Build.ps1` (z kořenového adresáře úložiště Demo_CI `./InfraDNS/Build.ps1`) definuje úlohy, které jsou součástí sestavení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-171">The [psake](https://github.com/psake/psake) build script defined in `Build.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Build.ps1`) defines tasks that are part of the build.</span></span>
<span data-ttu-id="1bfc1-172">Definuje také další úlohy, které každý úkol závisí.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-172">It also defines which other tasks each task depends on.</span></span>
<span data-ttu-id="1bfc1-173">Po vyvolání skriptu psake zajišťuje, že zadanou úlohu (nebo úloha s názvem `Default` Pokud není zadaný žádný) běží a že všechny závislosti také spustit (to je rekurzivní, tak, aby závislosti závislosti spouštět, a tak dále).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-173">When invoked, the psake script ensures that the specified task (or the task named `Default` if none is specified) runs, and that all dependencies also run (this is recursive, so that dependencies of dependencies run, and so on).</span></span>

<span data-ttu-id="1bfc1-174">V tomto příkladu `Default` úkolu je definován jako:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-174">In this example, the `Default` task is defined as:</span></span>

```powershell
Task Default -depends UnitTests
```

<span data-ttu-id="1bfc1-175">`Default` Úloha nemá žádnou implementaci samotný, ale má závislost na `CompileConfigs` úloh.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-175">The `Default` task has no implementation itself, but has a dependency on the `CompileConfigs` task.</span></span>
<span data-ttu-id="1bfc1-176">Výsledný řetězec závislostí zajistí, že jsou spuštěny všechny úlohy ve skriptu buildu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-176">The resulting chain of task dependencies ensures that all tasks in the build script are run.</span></span>

<span data-ttu-id="1bfc1-177">V tomto příkladu je skript psake vyvolána voláním `Invoke-PSake` v `Initiate.ps1` soubor (umístěný v kořenovém adresáři úložiště Demo_CI):</span><span class="sxs-lookup"><span data-stu-id="1bfc1-177">In this example, the psake script is invoked by a call to `Invoke-PSake` in the `Initiate.ps1` file (located at the root of the Demo_CI repository):</span></span>

```powershell
param(
    [parameter()]
    [ValidateSet('Build','Deploy')]
    [string]
    $fileName
)

#$Error.Clear()

Invoke-PSake $PSScriptRoot\InfraDNS\$fileName.ps1

<#if($Error.count)
{
    Throw "$fileName script failed. Check logs for failure details."
}
#>
```

<span data-ttu-id="1bfc1-178">Když jsme v našem příkladu na serveru TFS vytvořte definici sestavení, jsme poskytne naše psake soubor skriptu jako `fileName` parametr pro tento skript.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-178">When we create the build definition for our example in TFS, we will supply our psake script file as the `fileName` parameter for this script.</span></span>

<span data-ttu-id="1bfc1-179">Skript sestavení definuje následující úlohy:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-179">The build script defines the following tasks:</span></span>

#### <a name="generateenvironmentfiles"></a><span data-ttu-id="1bfc1-180">GenerateEnvironmentFiles</span><span class="sxs-lookup"><span data-stu-id="1bfc1-180">GenerateEnvironmentFiles</span></span>

<span data-ttu-id="1bfc1-181">Spuštění `DevEnv.ps1`, který generuje soubor konfiguračních dat.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-181">Runs `DevEnv.ps1`, which generates the configuration data file.</span></span>

#### <a name="installmodules"></a><span data-ttu-id="1bfc1-182">InstallModules</span><span class="sxs-lookup"><span data-stu-id="1bfc1-182">InstallModules</span></span>

<span data-ttu-id="1bfc1-183">Nainstaluje moduly potřebnými konfigurace `DNSServer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-183">Installs the modules required by the configuration `DNSServer.ps1`.</span></span>

#### <a name="scriptanalysis"></a><span data-ttu-id="1bfc1-184">ScriptAnalysis</span><span class="sxs-lookup"><span data-stu-id="1bfc1-184">ScriptAnalysis</span></span>

<span data-ttu-id="1bfc1-185">Volání [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-185">Calls the [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span></span>

#### <a name="unittests"></a><span data-ttu-id="1bfc1-186">UnitTests</span><span class="sxs-lookup"><span data-stu-id="1bfc1-186">UnitTests</span></span>

<span data-ttu-id="1bfc1-187">Spuštění [Pester](https://github.com/pester/Pester/wiki) testování částí.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-187">Runs the [Pester](https://github.com/pester/Pester/wiki) unit tests.</span></span>

#### <a name="compileconfigs"></a><span data-ttu-id="1bfc1-188">CompileConfigs</span><span class="sxs-lookup"><span data-stu-id="1bfc1-188">CompileConfigs</span></span>

<span data-ttu-id="1bfc1-189">Zkompiluje konfiguraci (`DNSServer.ps1`) do souboru MOF pomocí konfiguračních dat generovaných `GenerateEnvironmentFiles` úloh.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-189">Compiles the configuration (`DNSServer.ps1`) into a MOF file, using the configuration data generated by the `GenerateEnvironmentFiles` task.</span></span>

#### <a name="clean"></a><span data-ttu-id="1bfc1-190">Clean</span><span class="sxs-lookup"><span data-stu-id="1bfc1-190">Clean</span></span>

<span data-ttu-id="1bfc1-191">Vytvoří složek používaných pro příklad a odebere všechny výsledky testů, soubory konfiguračních dat a moduly z předchozích spuštění.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-191">Creates the folders used for the example, and removes any test results, configuration data files, and modules from previous runs.</span></span>

### <a name="the-psake-deploy-script"></a><span data-ttu-id="1bfc1-192">Skript nasadit psake</span><span class="sxs-lookup"><span data-stu-id="1bfc1-192">The psake deploy script</span></span>

<span data-ttu-id="1bfc1-193">[Psake](https://github.com/psake/psake) skript nasazení, které jsou definovány v `Deploy.ps1` (z kořenového adresáře úložiště Demo_CI `./InfraDNS/Deploy.ps1`) definuje úlohy, které nasadit a spustit konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-193">The [psake](https://github.com/psake/psake) deployment script defined in `Deploy.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Deploy.ps1`) defines tasks that deploy and run the configuration.</span></span>

<span data-ttu-id="1bfc1-194">`Deploy.ps1` definuje následující úlohy:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-194">`Deploy.ps1` defines the following tasks:</span></span>

#### <a name="deploymodules"></a><span data-ttu-id="1bfc1-195">DeployModules</span><span class="sxs-lookup"><span data-stu-id="1bfc1-195">DeployModules</span></span>

<span data-ttu-id="1bfc1-196">Spustí relaci prostředí PowerShell na `TestAgent1` a nainstaluje moduly obsahují prostředky DSC vyžadované pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-196">Starts a PowerShell session on `TestAgent1` and installs the modules containing the DSC resources required for the configuration.</span></span>

#### <a name="deployconfigs"></a><span data-ttu-id="1bfc1-197">DeployConfigs</span><span class="sxs-lookup"><span data-stu-id="1bfc1-197">DeployConfigs</span></span>

<span data-ttu-id="1bfc1-198">Volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny spustit konfiguraci v `TestAgent1`.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-198">Calls the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet to run the configuration on `TestAgent1`.</span></span>

#### <a name="integrationtests"></a><span data-ttu-id="1bfc1-199">IntegrationTests</span><span class="sxs-lookup"><span data-stu-id="1bfc1-199">IntegrationTests</span></span>

<span data-ttu-id="1bfc1-200">Spuštění [Pester](https://github.com/pester/Pester/wiki) integrační testy.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-200">Runs the [Pester](https://github.com/pester/Pester/wiki) integration tests.</span></span>

#### <a name="acceptancetests"></a><span data-ttu-id="1bfc1-201">AcceptanceTests</span><span class="sxs-lookup"><span data-stu-id="1bfc1-201">AcceptanceTests</span></span>

<span data-ttu-id="1bfc1-202">Spuštění [Pester](https://github.com/pester/Pester/wiki) předávací testy.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-202">Runs the [Pester](https://github.com/pester/Pester/wiki) acceptance tests.</span></span>

#### <a name="clean"></a><span data-ttu-id="1bfc1-203">Clean</span><span class="sxs-lookup"><span data-stu-id="1bfc1-203">Clean</span></span>

<span data-ttu-id="1bfc1-204">Odebere všechny moduly nainstalované v předchozí běhy a zajistí, že existuje složka výsledků testu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-204">Removes any modules installed in previous runs, and ensures that the test result folder exists.</span></span>

### <a name="test-scripts"></a><span data-ttu-id="1bfc1-205">Testování skriptů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-205">Test scripts</span></span>

<span data-ttu-id="1bfc1-206">Přijetí, integrace a testy jednotek, které jsou definovány ve skriptech v `Tests` složky (z kořenového adresáře úložiště Demo_CI `./InfraDNS/Tests`), každá do souborů s názvem `DNSServer.tests.ps1` v jejich příslušné složky.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-206">Acceptance, Integration, and Unit tests are defined in scripts in the `Tests` folder (from the root of the Demo_CI repository, `./InfraDNS/Tests`), each in files named `DNSServer.tests.ps1` in their respective folders.</span></span>

<span data-ttu-id="1bfc1-207">Testovací skripty použití [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-207">The test scripts use [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="unit-tests"></a><span data-ttu-id="1bfc1-208">Testy jednotek</span><span class="sxs-lookup"><span data-stu-id="1bfc1-208">Unit tests</span></span>

<span data-ttu-id="1bfc1-209">Konfigurace testů DSC samy o sobě Ujistěte se, že konfigurace provedete, co se očekává při spuštění testování částí.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-209">The unit tests test the DSC configurations themselves to ensure that the configurations will do what is expected when they run.</span></span>
<span data-ttu-id="1bfc1-210">Skript používá test jednotky [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-210">The unit test script uses [Pester](https://github.com/pester/Pester/wiki).</span></span>

#### <a name="integration-tests"></a><span data-ttu-id="1bfc1-211">Integrační testy</span><span class="sxs-lookup"><span data-stu-id="1bfc1-211">Integration tests</span></span>

<span data-ttu-id="1bfc1-212">Integrační testy otestovat konfiguraci systému a zajistit tak, že při integraci s ostatními součástmi, systém je nakonfigurován podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-212">The integration tests test the configuration of the system to ensure that when integrated with other components, the system is configured as expected.</span></span> <span data-ttu-id="1bfc1-213">Tyto testy se spouštějí na cílovém uzlu po dokončení konfigurace pomocí DSC.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-213">These tests run on the target node after it has been configured with DSC.</span></span>
<span data-ttu-id="1bfc1-214">Tento skript test integrace využívá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-214">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="acceptance-tests"></a><span data-ttu-id="1bfc1-215">Předávací testy</span><span class="sxs-lookup"><span data-stu-id="1bfc1-215">Acceptance tests</span></span>

<span data-ttu-id="1bfc1-216">Akceptační testy otestovat systém a ujistěte se, že se chová podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-216">Acceptance tests test the system to ensure that it behaves as expected.</span></span>
<span data-ttu-id="1bfc1-217">Například testy k zajištění, že se že vrátí správné informace při dotazu na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-217">For example, it tests to ensure a web page returns the right information when queried.</span></span>
<span data-ttu-id="1bfc1-218">Tyto testy vzdáleně spouštět z cílového uzlu účely otestování scénářů reálného světa.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-218">These tests run remotely from the target node in order to test real world scenarios.</span></span>
<span data-ttu-id="1bfc1-219">Tento skript test integrace využívá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-219">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

## <a name="define-the-build"></a><span data-ttu-id="1bfc1-220">Definice sestavení</span><span class="sxs-lookup"><span data-stu-id="1bfc1-220">Define the build</span></span>

<span data-ttu-id="1bfc1-221">Teď, když jsme na server TFS odeslána našeho kódu a prohlédli jste si ho nemá, nadefinujeme našich sestavení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-221">Now that we've uploaded our code to TFS and looked at what it does, let's define our build.</span></span>

<span data-ttu-id="1bfc1-222">Tady zaměříme jenom kroky sestavení, které přidáte do sestavení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-222">Here, we'll cover only the build steps that you'll add to the build.</span></span> <span data-ttu-id="1bfc1-223">Pokyny o tom, jak vytvořit definici sestavení v TFS naleznete v tématu [Create a queue definici sestavení](/azure/devops/pipelines/get-started-designer).</span><span class="sxs-lookup"><span data-stu-id="1bfc1-223">For instructions on how to create a build definition in TFS, see [Create and queue a build definition](/azure/devops/pipelines/get-started-designer).</span></span>

<span data-ttu-id="1bfc1-224">Vytvoření nové definice sestavení (vyberte **prázdný** šablony) s názvem "InfraDNS".</span><span class="sxs-lookup"><span data-stu-id="1bfc1-224">Create a new build definition (select the **Empty** template) named "InfraDNS".</span></span>
<span data-ttu-id="1bfc1-225">Přidáte že následující kroky vám definice sestavení:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-225">Add the following steps to you build definition:</span></span>

- <span data-ttu-id="1bfc1-226">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bfc1-226">PowerShell Script</span></span>
- <span data-ttu-id="1bfc1-227">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-227">Publish Test Results</span></span>
- <span data-ttu-id="1bfc1-228">Kopírování souborů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-228">Copy Files</span></span>
- <span data-ttu-id="1bfc1-229">Publikování artefaktů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-229">Publish Artifact</span></span>

<span data-ttu-id="1bfc1-230">Po přidání tyto kroky sestavení, upravte vlastnosti každého kroku následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-230">After adding these build steps, edit the properties of each step as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="1bfc1-231">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bfc1-231">PowerShell Script</span></span>

1. <span data-ttu-id="1bfc1-232">Nastavte **typ** vlastnost `File Path`.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-232">Set the **Type** property to `File Path`.</span></span>
1. <span data-ttu-id="1bfc1-233">Nastavte **cesta ke skriptu** vlastnost `initiate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-233">Set the **Script Path** property to `initiate.ps1`.</span></span>
1. <span data-ttu-id="1bfc1-234">Přidat `-fileName build` k **argumenty** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-234">Add `-fileName build` to the **Arguments** property.</span></span>

<span data-ttu-id="1bfc1-235">Tento krok sestavení běží `initiate.ps1` soubor, který volá psake skript sestavení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-235">This build step runs the `initiate.ps1` file, which calls the psake build script.</span></span>

### <a name="publish-test-results"></a><span data-ttu-id="1bfc1-236">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-236">Publish Test Results</span></span>

1. <span data-ttu-id="1bfc1-237">Nastavte **testování výsledku formátu** do `NUnit`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-237">Set **Test Result Format** to `NUnit`</span></span>
1. <span data-ttu-id="1bfc1-238">Nastavte **soubory výsledků testu** do `InfraDNS/Tests/Results/*.xml`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-238">Set **Test Results Files** to `InfraDNS/Tests/Results/*.xml`</span></span>
1. <span data-ttu-id="1bfc1-239">Nastavte **název testovacího běhu** k `Unit`.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-239">Set **Test Run Title** to `Unit`.</span></span>
1. <span data-ttu-id="1bfc1-240">Ujistěte se, že **možnosti ovládání** **povoleno** a **vždycky spouštět** jsou oba zaškrtnuto.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-240">Make sure **Control Options** **Enabled** and **Always run** are both selected.</span></span>

<span data-ttu-id="1bfc1-241">Tento krok sestavení spustí testy jednotek ve skriptu Pester jsme se podívali na dříve a ukládá výsledky `InfraDNS/Tests/Results/*.xml` složky.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-241">This build step runs the unit tests in the Pester script we looked at earlier, and stores the results in the `InfraDNS/Tests/Results/*.xml` folder.</span></span>

### <a name="copy-files"></a><span data-ttu-id="1bfc1-242">Kopírování souborů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-242">Copy Files</span></span>

1. <span data-ttu-id="1bfc1-243">Přidejte následující řádky do **obsah**:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-243">Add each of the following lines to **Contents**:</span></span>

   ```
   initiate.ps1
   **\deploy.ps1
   **\Acceptance\**
   **\Integration\**
   ```

1. <span data-ttu-id="1bfc1-244">Nastavte **TargetFolder** do `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-244">Set **TargetFolder** to `$(Build.ArtifactStagingDirectory)\`</span></span>

<span data-ttu-id="1bfc1-245">Zkopíruje tento krok sestavení a testovací skripty do pracovního adresáře tak, lze publikovat, protože artefaktů sestavení na další krok.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-245">This step copies the build and test scripts to the staging directory so that the can be published as build artifacts by the next step.</span></span>

### <a name="publish-artifact"></a><span data-ttu-id="1bfc1-246">Publikování artefaktů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-246">Publish Artifact</span></span>

1. <span data-ttu-id="1bfc1-247">Nastavte **cesta k publikování** do `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-247">Set **Path to Publish** to `$(Build.ArtifactStagingDirectory)\`</span></span>
1. <span data-ttu-id="1bfc1-248">Nastavte **název artefaktu** do `Deploy`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-248">Set **Artifact Name** to `Deploy`</span></span>
1. <span data-ttu-id="1bfc1-249">Nastavte **Typ artefaktu** do `Server`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-249">Set **Artifact Type** to `Server`</span></span>
1. <span data-ttu-id="1bfc1-250">Vyberte `Enabled` v **možnosti ovládání**</span><span class="sxs-lookup"><span data-stu-id="1bfc1-250">Select `Enabled` in **Control Options**</span></span>

## <a name="enable-continuous-integration"></a><span data-ttu-id="1bfc1-251">Povolit průběžnou integraci</span><span class="sxs-lookup"><span data-stu-id="1bfc1-251">Enable continuous integration</span></span>

<span data-ttu-id="1bfc1-252">Teď nastavíme triggeru, který způsobí, že projekt k sestavení kdykoli změnu se změnami do `ci-cd-example` větve úložiště git.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-252">Now we'll set up a trigger that causes the project to build any time a change is checked in to the `ci-cd-example` branch of the git repository.</span></span>

1. <span data-ttu-id="1bfc1-253">V sadě TFS, klikněte na tlačítko **sestavení a vydání** kartu</span><span class="sxs-lookup"><span data-stu-id="1bfc1-253">In TFS, click the **Build & Release** tab</span></span>
1. <span data-ttu-id="1bfc1-254">Vyberte `DNS Infra` definice sestavení a klikněte na tlačítko **upravit**</span><span class="sxs-lookup"><span data-stu-id="1bfc1-254">Select the `DNS Infra` build definition, and click **Edit**</span></span>
1. <span data-ttu-id="1bfc1-255">Klikněte na tlačítko **triggery** kartu</span><span class="sxs-lookup"><span data-stu-id="1bfc1-255">Click the **Triggers** tab</span></span>
1. <span data-ttu-id="1bfc1-256">Vyberte **kontinuální integrace (CI)** a vyberte `refs/heads/ci-cd-example` v rozevíracím seznamu větve</span><span class="sxs-lookup"><span data-stu-id="1bfc1-256">Select **Continuous integration (CI)**, and select `refs/heads/ci-cd-example` in the branch drop-down list</span></span>
1. <span data-ttu-id="1bfc1-257">Klikněte na tlačítko **Uložit** a potom **OK**</span><span class="sxs-lookup"><span data-stu-id="1bfc1-257">Click **Save** and then **OK**</span></span>

<span data-ttu-id="1bfc1-258">Nyní jakékoli změny v aktivační události git úložiště TFS automatické sestavení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-258">Now any change in the TFS git repository triggers an automated build.</span></span>

## <a name="create-the-release-definition"></a><span data-ttu-id="1bfc1-259">Vytvoření definice verze</span><span class="sxs-lookup"><span data-stu-id="1bfc1-259">Create the release definition</span></span>

<span data-ttu-id="1bfc1-260">Pojďme vytvořit definici vydané verze, tak, že projekt je nasazen do vývojového prostředí s každou kód vrácení se změnami.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-260">Let's create a release definition so that the project is deployed to the development environment with every code check-in.</span></span>

<span data-ttu-id="1bfc1-261">Provedete to tak, přidejte novou definici verze přidružené k `InfraDNS` jste předtím vytvořili definice sestavení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-261">To do this, add a new release definition associated with the `InfraDNS` build definition you created previously.</span></span>
<span data-ttu-id="1bfc1-262">Je potřeba vybrat možnost **průběžné nasazování** tak, aby se nová verze se aktivuje vždy nového sestavení se dokončí.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-262">Be sure to select **Continuous deployment** so that a new release will be triggered any time a new build is completed.</span></span>
<span data-ttu-id="1bfc1-263">([Jak: Práce s definic vydané verze](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) a nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-263">([How to: Work with release definitions](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) and configure it as follows:</span></span>

<span data-ttu-id="1bfc1-264">Přidejte do definice vydané verze následující kroky:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-264">Add the following steps to the release definition:</span></span>

- <span data-ttu-id="1bfc1-265">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bfc1-265">PowerShell Script</span></span>
- <span data-ttu-id="1bfc1-266">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-266">Publish Test Results</span></span>
- <span data-ttu-id="1bfc1-267">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-267">Publish Test Results</span></span>

<span data-ttu-id="1bfc1-268">Postup úpravy následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1bfc1-268">Edit the steps as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="1bfc1-269">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bfc1-269">PowerShell Script</span></span>

1. <span data-ttu-id="1bfc1-270">Nastavte **cesta ke skriptu** pole `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-270">Set the **Script Path** field to `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span></span>
1. <span data-ttu-id="1bfc1-271">Nastavte **argumenty** pole `-fileName Deploy`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-271">Set the **Arguments** field to `-fileName Deploy`</span></span>

### <a name="first-publish-test-results"></a><span data-ttu-id="1bfc1-272">Nejprve publikovat výsledky testů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-272">First Publish Test Results</span></span>

1. <span data-ttu-id="1bfc1-273">Vyberte `NUnit` pro **formát výsledku testu** pole</span><span class="sxs-lookup"><span data-stu-id="1bfc1-273">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="1bfc1-274">Nastavte **soubory s výsledky testu** pole `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-274">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span></span>
1. <span data-ttu-id="1bfc1-275">Nastavte **název testovacího běhu** do `Integration`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-275">Set the **Test Run Title** to `Integration`</span></span>
1. <span data-ttu-id="1bfc1-276">V části **možnosti ovládání**, zkontrolujte **vždycky spouštět**</span><span class="sxs-lookup"><span data-stu-id="1bfc1-276">Under **Control Options**, check **Always run**</span></span>

### <a name="second-publish-test-results"></a><span data-ttu-id="1bfc1-277">Za druhé publikovat výsledky testů</span><span class="sxs-lookup"><span data-stu-id="1bfc1-277">Second Publish Test Results</span></span>

1. <span data-ttu-id="1bfc1-278">Vyberte `NUnit` pro **formát výsledku testu** pole</span><span class="sxs-lookup"><span data-stu-id="1bfc1-278">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="1bfc1-279">Nastavte **soubory s výsledky testu** pole `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-279">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span></span>
1. <span data-ttu-id="1bfc1-280">Nastavte **název testovacího běhu** do `Acceptance`</span><span class="sxs-lookup"><span data-stu-id="1bfc1-280">Set the **Test Run Title** to `Acceptance`</span></span>
1. <span data-ttu-id="1bfc1-281">V části **možnosti ovládání**, zkontrolujte **vždycky spouštět**</span><span class="sxs-lookup"><span data-stu-id="1bfc1-281">Under **Control Options**, check **Always run**</span></span>

## <a name="verify-your-results"></a><span data-ttu-id="1bfc1-282">Zkontrolujte výsledky</span><span class="sxs-lookup"><span data-stu-id="1bfc1-282">Verify your results</span></span>

<span data-ttu-id="1bfc1-283">Teď, když odešlete změny `ci-cd-example` větve na server TFS, nové sestavení spustí.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-283">Now, any time you push changes in the `ci-cd-example` branch to TFS, a new build will start.</span></span>
<span data-ttu-id="1bfc1-284">Pokud se sestavení úspěšně dokončí, se aktivuje nové nasazení.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-284">If the build completes successfully, a new deployment is triggered.</span></span>

<span data-ttu-id="1bfc1-285">Výsledek nasazení můžete zkontrolovat otevřením prohlížeče v klientském počítači a přejdete na `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-285">You can check the result of the deployment by opening a browser on the client machine and navigating to `www.contoso.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bfc1-286">Další kroky</span><span class="sxs-lookup"><span data-stu-id="1bfc1-286">Next steps</span></span>

<span data-ttu-id="1bfc1-287">Tento příklad konfiguruje DNS server `TestAgent1` tak, aby adresa URL `www.contoso.com` přeloží na `TestAgent2`, ale ve skutečnosti Nenasazuje webu.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-287">This example configures the DNS server `TestAgent1` so that the URL `www.contoso.com` resolves to `TestAgent2`, but it does not actually deploy a website.</span></span>
<span data-ttu-id="1bfc1-288">Kostru to udělat najdete v úložišti v rámci `WebApp` složky.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-288">The skeleton for doing so is provided in the repo under the `WebApp` folder.</span></span>
<span data-ttu-id="1bfc1-289">Můžete použít zástupné procedury, chcete-li vytvořit skripty psake Pester testy a konfigurace DSC k dispozici pro nasazení svůj vlastní web.</span><span class="sxs-lookup"><span data-stu-id="1bfc1-289">You can use the stubs provided to create psake scripts, Pester tests, and DSC configurations to deploy your own website.</span></span>

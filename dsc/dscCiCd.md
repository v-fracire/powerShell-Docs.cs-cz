---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Vytváření kanál průběžnou integraci a průběžné nasazování pomocí DSC
ms.openlocfilehash: faeef5022cbd984cab0620b69db19de8b84cca0e
ms.sourcegitcommit: 68093cc12a7a22c53d11ce7d33c18622921a0dd1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/26/2018
ms.locfileid: "36940340"
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a><span data-ttu-id="149e7-103">Vytváření kanál průběžnou integraci a průběžné nasazování pomocí DSC</span><span class="sxs-lookup"><span data-stu-id="149e7-103">Building a Continuous Integration and Continuous Deployment pipeline with DSC</span></span>

<span data-ttu-id="149e7-104">Tento příklad ukazuje, jak vytvořit kanál průběžné nasazování integrace/souvislý (CI/CD) pomocí prostředí PowerShell, DSC, Pester a Visual Studio Team Foundation Server (TFS).</span><span class="sxs-lookup"><span data-stu-id="149e7-104">This example demonstrates how to build a Continuous Integration/Continuous Deployment (CI/CD) pipeline by using PowerShell, DSC, Pester, and Visual Studio Team Foundation Server (TFS).</span></span>

<span data-ttu-id="149e7-105">Po vytvoření kanálu a nakonfigurovaný, můžete použít pro plně nasazení, konfiguraci a testování serveru DNS a přidružené záznamy hostitele.</span><span class="sxs-lookup"><span data-stu-id="149e7-105">After the pipeline is built and configured, you can use it to fully deploy, configure and test a DNS server and associated host records.</span></span>
<span data-ttu-id="149e7-106">Tento proces simuluje první část kanál, který se použije ve vývojovém prostředí.</span><span class="sxs-lookup"><span data-stu-id="149e7-106">This process simulates the first part of a pipeline that would be used in a development environment.</span></span>

<span data-ttu-id="149e7-107">Kanál automatizované CI/CD umožňuje rychlejší aktualizace softwaru a spolehlivěji, zajistíte, že veškerý kód je testován a že je aktuální sestavení kódu vždy k dispozici.</span><span class="sxs-lookup"><span data-stu-id="149e7-107">An automated CI/CD pipeline helps you update software faster and more reliably, ensuring that all code is tested, and that a current build of your code is available at all times.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="149e7-108">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="149e7-108">Prerequisites</span></span>

<span data-ttu-id="149e7-109">Pokud chcete použít v tomto příkladu, byste měli seznámit s následujícími službami:</span><span class="sxs-lookup"><span data-stu-id="149e7-109">To use this example, you should be familiar with the following:</span></span>

- <span data-ttu-id="149e7-110">Koncepty CI CD.</span><span class="sxs-lookup"><span data-stu-id="149e7-110">CI-CD concepts.</span></span> <span data-ttu-id="149e7-111">Odkaz na dobrý najdete na [modelu kanálu verze](http://aka.ms/thereleasepipelinemodelpdf).</span><span class="sxs-lookup"><span data-stu-id="149e7-111">A good reference can be found at [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf).</span></span>
- <span data-ttu-id="149e7-112">[Git](https://git-scm.com/) zdroj ovládacího prvku</span><span class="sxs-lookup"><span data-stu-id="149e7-112">[Git](https://git-scm.com/) source control</span></span>
- <span data-ttu-id="149e7-113">[Pester](https://github.com/pester/Pester) testování framework</span><span class="sxs-lookup"><span data-stu-id="149e7-113">The [Pester](https://github.com/pester/Pester) testing framework</span></span>
- [<span data-ttu-id="149e7-114">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="149e7-114">Team Foundation Server</span></span>](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a><span data-ttu-id="149e7-115">Co budete potřebovat</span><span class="sxs-lookup"><span data-stu-id="149e7-115">What you will need</span></span>

<span data-ttu-id="149e7-116">Pro sestavení a spuštění tohoto příkladu, budete potřebovat v prostředí s několika počítačích nebo virtuálních počítačů.</span><span class="sxs-lookup"><span data-stu-id="149e7-116">To build and run this example, you will need an environment with several computers and/or virtual machines.</span></span>

### <a name="client"></a><span data-ttu-id="149e7-117">Client</span><span class="sxs-lookup"><span data-stu-id="149e7-117">Client</span></span>

<span data-ttu-id="149e7-118">Toto je počítač, kde, můžete to udělat všechny pracovní nastavení a spuštění v příkladu.</span><span class="sxs-lookup"><span data-stu-id="149e7-118">This is the computer where you'll do all of the work setting up and running the example.</span></span>

<span data-ttu-id="149e7-119">Klientský počítač musí být počítač se systémem Windows s nainstalované tyto položky:</span><span class="sxs-lookup"><span data-stu-id="149e7-119">The client computer must be a Windows computer with the following installed:</span></span>

- [<span data-ttu-id="149e7-120">Git</span><span class="sxs-lookup"><span data-stu-id="149e7-120">Git</span></span>](https://git-scm.com/)
- <span data-ttu-id="149e7-121">klonovat úložiště místní git z https://github.com/PowerShell/Demo_CI</span><span class="sxs-lookup"><span data-stu-id="149e7-121">a local git repo cloned from https://github.com/PowerShell/Demo_CI</span></span>
- <span data-ttu-id="149e7-122">textový editor, například [Visual Studio Code](https://code.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="149e7-122">a text editor, such as [Visual Studio Code](https://code.visualstudio.com/)</span></span>

### <a name="tfssrv1"></a><span data-ttu-id="149e7-123">TFSSrv1</span><span class="sxs-lookup"><span data-stu-id="149e7-123">TFSSrv1</span></span>

<span data-ttu-id="149e7-124">Počítač, který je hostitelem serveru TFS, kde můžete definovat vaše sestavení a verze.</span><span class="sxs-lookup"><span data-stu-id="149e7-124">The computer that hosts the TFS server where you will define your build and release.</span></span>
<span data-ttu-id="149e7-125">Tento počítač musí mít [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) nainstalována.</span><span class="sxs-lookup"><span data-stu-id="149e7-125">This computer must have [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) installed.</span></span>

### <a name="buildagent"></a><span data-ttu-id="149e7-126">BuildAgent</span><span class="sxs-lookup"><span data-stu-id="149e7-126">BuildAgent</span></span>

<span data-ttu-id="149e7-127">Počítač, který spouští Windows sestavení agenta, který sestaví projekt.</span><span class="sxs-lookup"><span data-stu-id="149e7-127">The computer that runs the Windows build agent that builds the project.</span></span>
<span data-ttu-id="149e7-128">Tento počítač musí mít Windows sestavení agent nainstalován a spuštěn.</span><span class="sxs-lookup"><span data-stu-id="149e7-128">This computer must have a Windows build agent installed and running.</span></span>
<span data-ttu-id="149e7-129">V tématu [nasadit agenta v systému Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) pro pokyny, jak nainstalovat a spustit Windows sestavení agenta.</span><span class="sxs-lookup"><span data-stu-id="149e7-129">See [Deploy an agent on Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) for instructions on how to install and run a Windows build agent.</span></span>

<span data-ttu-id="149e7-130">Musíte taky nainstalovat obě `xDnsServer` a `xNetworking` moduly DSC v tomto počítači.</span><span class="sxs-lookup"><span data-stu-id="149e7-130">You also need to install both the `xDnsServer` and `xNetworking` DSC modules on this computer.</span></span>

### <a name="testagent1"></a><span data-ttu-id="149e7-131">TestAgent1</span><span class="sxs-lookup"><span data-stu-id="149e7-131">TestAgent1</span></span>

<span data-ttu-id="149e7-132">Toto je počítač, který je nakonfigurovaný jako DNS server v tomto příkladu konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="149e7-132">This is the computer that is configured as a DNS server by the DSC configuration in this example.</span></span>
<span data-ttu-id="149e7-133">V počítači musí být spuštěn [systému Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="149e7-133">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

### <a name="testagent2"></a><span data-ttu-id="149e7-134">TestAgent2</span><span class="sxs-lookup"><span data-stu-id="149e7-134">TestAgent2</span></span>

<span data-ttu-id="149e7-135">Toto je počítač, který je hostitelem webu, který tento příklad konfiguruje.</span><span class="sxs-lookup"><span data-stu-id="149e7-135">This is the computer that hosts the website this example configures.</span></span>
<span data-ttu-id="149e7-136">V počítači musí být spuštěn [systému Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="149e7-136">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

## <a name="add-the-code-to-tfs"></a><span data-ttu-id="149e7-137">Přidejte kód do sady TFS</span><span class="sxs-lookup"><span data-stu-id="149e7-137">Add the code to TFS</span></span>

<span data-ttu-id="149e7-138">Začneme vytvoření úložiště Git v sadě TFS a importováním kód z místního úložiště v klientském počítači.</span><span class="sxs-lookup"><span data-stu-id="149e7-138">We'll start out by creating a Git repository in TFS, and importing the code from your local repository on the client computer.</span></span>
<span data-ttu-id="149e7-139">Pokud se úložiště Demo_CI nebyly již klonovat na klientském počítači, postupujte tak teď spuštěním následujícího příkazu git:</span><span class="sxs-lookup"><span data-stu-id="149e7-139">If you have not already cloned the Demo_CI repository to your client computer, do so now by running the following git command:</span></span>

`git clone https://github.com/PowerShell/Demo_CI`

1. <span data-ttu-id="149e7-140">Na klientském počítači přejděte na server TFS ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="149e7-140">On your client computer, navigate to your TFS server in a web browser.</span></span>
1. <span data-ttu-id="149e7-141">V sadě TFS [vytvoření nového týmového projektu](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) s názvem Demo_CI.</span><span class="sxs-lookup"><span data-stu-id="149e7-141">In TFS, [Create a new team project](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) named Demo_CI.</span></span>

   <span data-ttu-id="149e7-142">Ujistěte se, že **verzí** je nastaven na **Git**.</span><span class="sxs-lookup"><span data-stu-id="149e7-142">Make sure that **Version control** is set to **Git**.</span></span>
1. <span data-ttu-id="149e7-143">Na klientském počítači přidejte vzdálené úložiště, které jste právě vytvořili v sadě TFS pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="149e7-143">On your client computer, add a remote to the repository you just created in TFS with the following command:</span></span>

   `git remote add tfs <YourTFSRepoURL>`

   <span data-ttu-id="149e7-144">Kde `<YourTFSRepoURL>` je adresa URL klonování k úložišti sady TFS, který jste vytvořili v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="149e7-144">Where `<YourTFSRepoURL>` is the clone URL to the TFS repository you created in the previous step.</span></span>

   <span data-ttu-id="149e7-145">Pokud si nejste jisti, kde se tato adresa URL, najdete v části [klonovat existující úložiště Git](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).</span><span class="sxs-lookup"><span data-stu-id="149e7-145">If you don't know where to find this URL, see [Clone an existing Git repo](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).</span></span>
1. <span data-ttu-id="149e7-146">Push kód z místního úložiště do úložiště TFS pomocí následujícího příkazu:</span><span class="sxs-lookup"><span data-stu-id="149e7-146">Push the code from your local repository to your TFS repository with the following command:</span></span>

   `git push tfs --all`
1. <span data-ttu-id="149e7-147">Úložiště TFS vyplní kódem Demo_CI.</span><span class="sxs-lookup"><span data-stu-id="149e7-147">The TFS repository will be populated with the Demo_CI code.</span></span>

> [!NOTE]
> <span data-ttu-id="149e7-148">Kód v tomto příkladu používá `ci-cd-example` větve úložiště Git.</span><span class="sxs-lookup"><span data-stu-id="149e7-148">This example uses the code in the `ci-cd-example` branch of the Git repo.</span></span>
> <span data-ttu-id="149e7-149">Nezapomeňte zadat tuto větev jako výchozí větev ve vašem projektu sady TFS a aktivačních událostí CI/CD vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="149e7-149">Be sure to specify this branch as the default branch in your TFS project, and for the CI/CD triggers you create.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="149e7-150">Pochopení kódu</span><span class="sxs-lookup"><span data-stu-id="149e7-150">Understanding the code</span></span>

<span data-ttu-id="149e7-151">Předtím, než vytvoříme kanály sestavení a nasazení, podíváme se na kód, abyste pochopili, co se děje.</span><span class="sxs-lookup"><span data-stu-id="149e7-151">Before we create the build and deployment pipelines, let's look at some of the code to understand what is going on.</span></span>
<span data-ttu-id="149e7-152">Na klientském počítači otevřete svém oblíbeném textovém editoru a přejděte do kořenového úložiště Demo_CI Git.</span><span class="sxs-lookup"><span data-stu-id="149e7-152">On your client computer, open your favorite text editor and navigate to the root of your Demo_CI Git repository.</span></span>

### <a name="the-dsc-configuration"></a><span data-ttu-id="149e7-153">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="149e7-153">The DSC configuration</span></span>

<span data-ttu-id="149e7-154">Otevřete soubor `DNSServer.ps1` (z kořene místní úložiště Demo_CI `./InfraDNS/Configs/DNSServer.ps1`).</span><span class="sxs-lookup"><span data-stu-id="149e7-154">Open the file `DNSServer.ps1` (from the root of the local Demo_CI repository, `./InfraDNS/Configs/DNSServer.ps1`).</span></span>

<span data-ttu-id="149e7-155">Tento soubor obsahuje konfigurace DSC, který slouží k nastavení serveru DNS.</span><span class="sxs-lookup"><span data-stu-id="149e7-155">This file contains the DSC configuration that sets up the DNS server.</span></span> <span data-ttu-id="149e7-156">Tady je v celé jeho šíři:</span><span class="sxs-lookup"><span data-stu-id="149e7-156">Here it is in its entirety:</span></span>

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

<span data-ttu-id="149e7-157">Upozornění `Node` příkaz:</span><span class="sxs-lookup"><span data-stu-id="149e7-157">Notice the `Node` statement:</span></span>

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

<span data-ttu-id="149e7-158">To vyhledá všechny uzly, které byly definovány tak, že má role `DNSServer` v [konfigurační data](configData.md), který je vytvořen `DevEnv.ps1` skriptu.</span><span class="sxs-lookup"><span data-stu-id="149e7-158">This finds any nodes that were defined as having a role of `DNSServer` in the [configuration data](configData.md), which is created by the `DevEnv.ps1` script.</span></span>

<span data-ttu-id="149e7-159">Další informace o `Where` metoda v [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span><span class="sxs-lookup"><span data-stu-id="149e7-159">You can read more about the `Where` method in [about_arrays](/powershell/reference/3.0/Microsoft.PowerShell.Core/About/about_Arrays.md)</span></span>

<span data-ttu-id="149e7-160">Definování uzly pomocí konfiguračních dat je důležité, pokud to položek konfigurace, protože uzel informace změní pravděpodobně mezi prostředími, a pomocí konfigurační data můžete snadno provádět změny uzlu informace beze změny kódu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="149e7-160">Using configuration data to define nodes is important when doing CI because node information will likely change between environments, and using configuration data allows you to easily make changes to node information without changing the configuration code.</span></span>

<span data-ttu-id="149e7-161">V prvním bloku prostředků, konfigurace volá [WindowsFeature](windowsFeatureResource.md) zajistit, že je povolena funkce DNS.</span><span class="sxs-lookup"><span data-stu-id="149e7-161">In the first resource block, the configuration calls the [WindowsFeature](windowsFeatureResource.md) to ensure that the DNS feature is enabled.</span></span>
<span data-ttu-id="149e7-162">Bloky prostředků, které podle volání prostředky z [xDnsServer](https://github.com/PowerShell/xDnsServer) modulu Konfigurace primární zóna a záznamy DNS.</span><span class="sxs-lookup"><span data-stu-id="149e7-162">The resource blocks that follow call resources from the [xDnsServer](https://github.com/PowerShell/xDnsServer) module to configure the primary zone and DNS records.</span></span>

<span data-ttu-id="149e7-163">Všimněte si, že dva `xDnsRecord` bloky jsou uzavřen do `foreach` cykly, které iteraci v rámci pole v konfigurační data.</span><span class="sxs-lookup"><span data-stu-id="149e7-163">Notice that the two `xDnsRecord` blocks are wrapped in `foreach` loops that iterate through arrays in the configuration data.</span></span>
<span data-ttu-id="149e7-164">Znovu vytvoří konfigurační data `DevEnv.ps1` skript, který podíváme Další.</span><span class="sxs-lookup"><span data-stu-id="149e7-164">Again, the configuration data is created by the `DevEnv.ps1` script, which we'll look at next.</span></span>

### <a name="configuration-data"></a><span data-ttu-id="149e7-165">Konfigurační data</span><span class="sxs-lookup"><span data-stu-id="149e7-165">Configuration data</span></span>

<span data-ttu-id="149e7-166">`DevEnv.ps1` Souboru (z kořene místní úložiště Demo_CI `./InfraDNS/DevEnv.ps1`) určuje konkrétní prostředí konfigurační data v zatřiďovací tabulky a pak předá tento zatřiďovací tabulky na volání `New-DscConfigurationDataDocument` funkce, která je definována v `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span><span class="sxs-lookup"><span data-stu-id="149e7-166">The `DevEnv.ps1` file (from the root of the local Demo_CI repository, `./InfraDNS/DevEnv.ps1`) specifies the environment-specific configuration data in a hashtable, and then passes that hashtable to a call to the `New-DscConfigurationDataDocument` function, which is defined in `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span></span>

<span data-ttu-id="149e7-167">`DevEnv.ps1` Souboru:</span><span class="sxs-lookup"><span data-stu-id="149e7-167">The `DevEnv.ps1` file:</span></span>

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

<span data-ttu-id="149e7-168">`New-DscConfigurationDataDocument` – Funkce (definované v `\Assets\DscPipelineTools\DscPipelineTools.psm1`) prostřednictvím kódu programu vytvoří dokument data konfigurace z zatřiďovací tabulky (data uzlu) a pole (bez uzlu data), které se předávají jako `RawEnvData` a `OtherEnvData` parametry.</span><span class="sxs-lookup"><span data-stu-id="149e7-168">The `New-DscConfigurationDataDocument` function (defined in `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programmatically creates a configuration data document from the hashtable (node data) and array (non-node data) that are passed as the `RawEnvData` and `OtherEnvData` parameters.</span></span>

<span data-ttu-id="149e7-169">V našem případě pouze `RawEnvData` parametr se používá.</span><span class="sxs-lookup"><span data-stu-id="149e7-169">In our case, only the `RawEnvData` parameter is used.</span></span>

### <a name="the-psake-build-script"></a><span data-ttu-id="149e7-170">Skript psake sestavení</span><span class="sxs-lookup"><span data-stu-id="149e7-170">The psake build script</span></span>

<span data-ttu-id="149e7-171">[Psake](https://github.com/psake/psake) skriptu definovaný v sestavení `Build.ps1` (z kořenového úložiště Demo_CI `./InfraDNS/Build.ps1`) definuje úlohy, které jsou součástí sestavení.</span><span class="sxs-lookup"><span data-stu-id="149e7-171">The [psake](https://github.com/psake/psake) build script defined in `Build.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Build.ps1`) defines tasks that are part of the build.</span></span>
<span data-ttu-id="149e7-172">Také definuje, jaké úkoly, které každý úkol závisí na.</span><span class="sxs-lookup"><span data-stu-id="149e7-172">It also defines which other tasks each task depends on.</span></span>
<span data-ttu-id="149e7-173">Po vyvolání skriptu psake zajistí, že zadané úloze (nebo úloha s názvem `Default` Pokud není zadaný žádný) běží a že všechny závislosti také spustit (to je rekurzivní, takže závislosti závislosti spustit, a tak dále).</span><span class="sxs-lookup"><span data-stu-id="149e7-173">When invoked, the psake script ensures that the specified task (or the task named `Default` if none is specified) runs, and that all dependencies also run (this is recursive, so that dependencies of dependencies run, and so on).</span></span>

<span data-ttu-id="149e7-174">V tomto příkladu `Default` úloh je definován jako:</span><span class="sxs-lookup"><span data-stu-id="149e7-174">In this example, the `Default` task is defined as:</span></span>

```powershell
Task Default -depends UnitTests
```

<span data-ttu-id="149e7-175">`Default` Úloha nemá žádnou implementaci sám sebe, ale má závislost na `CompileConfigs` úloh.</span><span class="sxs-lookup"><span data-stu-id="149e7-175">The `Default` task has no implementation itself, but has a dependency on the `CompileConfigs` task.</span></span>
<span data-ttu-id="149e7-176">Výsledný řetězec závislostí zajistí, že jsou všechny úlohy ve skriptu buildu použít.</span><span class="sxs-lookup"><span data-stu-id="149e7-176">The resulting chain of task dependencies ensures that all tasks in the build script are run.</span></span>

<span data-ttu-id="149e7-177">V tomto příkladu je skript psake vyvolat volání `Invoke-PSake` v `Initiate.ps1` soubor (umístěný v kořenovém úložišti Demo_CI):</span><span class="sxs-lookup"><span data-stu-id="149e7-177">In this example, the psake script is invoked by a call to `Invoke-PSake` in the `Initiate.ps1` file (located at the root of the Demo_CI repository):</span></span>

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

<span data-ttu-id="149e7-178">Při vytváření definice sestavení pro náš příklad v sadě TFS, jsme se zadat soubor skriptu naše psake jako `fileName` parametr pro tento skript.</span><span class="sxs-lookup"><span data-stu-id="149e7-178">When we create the build definition for our example in TFS, we will supply our psake script file as the `fileName` parameter for this script.</span></span>

<span data-ttu-id="149e7-179">Skript sestavení definuje následující úlohy:</span><span class="sxs-lookup"><span data-stu-id="149e7-179">The build script defines the following tasks:</span></span>

#### <a name="generateenvironmentfiles"></a><span data-ttu-id="149e7-180">GenerateEnvironmentFiles</span><span class="sxs-lookup"><span data-stu-id="149e7-180">GenerateEnvironmentFiles</span></span>

<span data-ttu-id="149e7-181">Spustí `DevEnv.ps1`, který generuje datový soubor konfigurace.</span><span class="sxs-lookup"><span data-stu-id="149e7-181">Runs `DevEnv.ps1`, which generates the configuration data file.</span></span>

#### <a name="installmodules"></a><span data-ttu-id="149e7-182">InstallModules</span><span class="sxs-lookup"><span data-stu-id="149e7-182">InstallModules</span></span>

<span data-ttu-id="149e7-183">Nainstaluje moduly potřebnými konfigurace `DNSServer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="149e7-183">Installs the modules required by the configuration `DNSServer.ps1`.</span></span>

#### <a name="scriptanalysis"></a><span data-ttu-id="149e7-184">ScriptAnalysis</span><span class="sxs-lookup"><span data-stu-id="149e7-184">ScriptAnalysis</span></span>

<span data-ttu-id="149e7-185">Volání [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="149e7-185">Calls the [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span></span>

#### <a name="unittests"></a><span data-ttu-id="149e7-186">UnitTests</span><span class="sxs-lookup"><span data-stu-id="149e7-186">UnitTests</span></span>

<span data-ttu-id="149e7-187">Spustí [Pester](https://github.com/pester/Pester/wiki) testování částí.</span><span class="sxs-lookup"><span data-stu-id="149e7-187">Runs the [Pester](https://github.com/pester/Pester/wiki) unit tests.</span></span>

#### <a name="compileconfigs"></a><span data-ttu-id="149e7-188">CompileConfigs</span><span class="sxs-lookup"><span data-stu-id="149e7-188">CompileConfigs</span></span>

<span data-ttu-id="149e7-189">Zkompiluje konfigurace (`DNSServer.ps1`) do souboru MOF, pomocí konfiguračních dat vygenerovaných `GenerateEnvironmentFiles` úloh.</span><span class="sxs-lookup"><span data-stu-id="149e7-189">Compiles the configuration (`DNSServer.ps1`) into a MOF file, using the configuration data generated by the `GenerateEnvironmentFiles` task.</span></span>

#### <a name="clean"></a><span data-ttu-id="149e7-190">Clean</span><span class="sxs-lookup"><span data-stu-id="149e7-190">Clean</span></span>

<span data-ttu-id="149e7-191">Vytvoří složek používaných pro tento příklad a odebere z předchozích spuštění žádné výsledky testů, souborů konfiguračních dat a modulů.</span><span class="sxs-lookup"><span data-stu-id="149e7-191">Creates the folders used for the example, and removes any test results, configuration data files, and modules from previous runs.</span></span>

### <a name="the-psake-deploy-script"></a><span data-ttu-id="149e7-192">Skript nasadit psake</span><span class="sxs-lookup"><span data-stu-id="149e7-192">The psake deploy script</span></span>

<span data-ttu-id="149e7-193">[Psake](https://github.com/psake/psake) skript nasazení, které jsou definované v `Deploy.ps1` (z kořenového úložiště Demo_CI `./InfraDNS/Deploy.ps1`) definuje úlohy, které nasazení a spuštění konfigurace.</span><span class="sxs-lookup"><span data-stu-id="149e7-193">The [psake](https://github.com/psake/psake) deployment script defined in `Deploy.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Deploy.ps1`) defines tasks that deploy and run the configuration.</span></span>

<span data-ttu-id="149e7-194">`Deploy.ps1` definuje následující úlohy:</span><span class="sxs-lookup"><span data-stu-id="149e7-194">`Deploy.ps1` defines the following tasks:</span></span>

#### <a name="deploymodules"></a><span data-ttu-id="149e7-195">DeployModules</span><span class="sxs-lookup"><span data-stu-id="149e7-195">DeployModules</span></span>

<span data-ttu-id="149e7-196">Spustí relaci prostředí PowerShell na `TestAgent1` a nainstaluje moduly obsahující prostředky DSC potřebné pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="149e7-196">Starts a PowerShell session on `TestAgent1` and installs the modules containing the DSC resources required for the configuration.</span></span>

#### <a name="deployconfigs"></a><span data-ttu-id="149e7-197">DeployConfigs</span><span class="sxs-lookup"><span data-stu-id="149e7-197">DeployConfigs</span></span>

<span data-ttu-id="149e7-198">Volání [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) můžete spustit konfiguraci `TestAgent1`.</span><span class="sxs-lookup"><span data-stu-id="149e7-198">Calls the [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) cmdlet to run the configuration on `TestAgent1`.</span></span>

#### <a name="integrationtests"></a><span data-ttu-id="149e7-199">IntegrationTests</span><span class="sxs-lookup"><span data-stu-id="149e7-199">IntegrationTests</span></span>

<span data-ttu-id="149e7-200">Spustí [Pester](https://github.com/pester/Pester/wiki) integrace testy.</span><span class="sxs-lookup"><span data-stu-id="149e7-200">Runs the [Pester](https://github.com/pester/Pester/wiki) integration tests.</span></span>

#### <a name="acceptancetests"></a><span data-ttu-id="149e7-201">AcceptanceTests</span><span class="sxs-lookup"><span data-stu-id="149e7-201">AcceptanceTests</span></span>

<span data-ttu-id="149e7-202">Spustí [Pester](https://github.com/pester/Pester/wiki) přijetí testy.</span><span class="sxs-lookup"><span data-stu-id="149e7-202">Runs the [Pester](https://github.com/pester/Pester/wiki) acceptance tests.</span></span>

#### <a name="clean"></a><span data-ttu-id="149e7-203">Clean</span><span class="sxs-lookup"><span data-stu-id="149e7-203">Clean</span></span>

<span data-ttu-id="149e7-204">Odebere všechny moduly nainstalované v předchozích spuštění a zajišťuje, že složka výsledků testu existuje.</span><span class="sxs-lookup"><span data-stu-id="149e7-204">Removes any modules installed in previous runs, and ensures that the test result folder exists.</span></span>

### <a name="test-scripts"></a><span data-ttu-id="149e7-205">Testování skriptů</span><span class="sxs-lookup"><span data-stu-id="149e7-205">Test scripts</span></span>

<span data-ttu-id="149e7-206">Přijetí, integrace a jednotky testů jsou definovány v skripty v `Tests` složky (z kořenového úložiště Demo_CI `./InfraDNS/Tests`), každou v souborech s názvem `DNSServer.tests.ps1` v jejich příslušné složky.</span><span class="sxs-lookup"><span data-stu-id="149e7-206">Acceptance, Integration, and Unit tests are defined in scripts in the `Tests` folder (from the root of the Demo_CI repository, `./InfraDNS/Tests`), each in files named `DNSServer.tests.ps1` in their respective folders.</span></span>

<span data-ttu-id="149e7-207">Použití skriptů test [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="149e7-207">The test scripts use [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="unit-tests"></a><span data-ttu-id="149e7-208">Testy jednotek</span><span class="sxs-lookup"><span data-stu-id="149e7-208">Unit tests</span></span>

<span data-ttu-id="149e7-209">Jednotka testy konfigurací testů DSC, se ujistěte, že konfigurace bude provádět očekávané při spuštění.</span><span class="sxs-lookup"><span data-stu-id="149e7-209">The unit tests test the DSC configurations themselves to ensure that the configurations will do what is expected when they run.</span></span>
<span data-ttu-id="149e7-210">Jednotka testování skript používá [Pester](https://github.com/pester/Pester/wiki).</span><span class="sxs-lookup"><span data-stu-id="149e7-210">The unit test script uses [Pester](https://github.com/pester/Pester/wiki).</span></span>

#### <a name="integration-tests"></a><span data-ttu-id="149e7-211">Integrace testů</span><span class="sxs-lookup"><span data-stu-id="149e7-211">Integration tests</span></span>

<span data-ttu-id="149e7-212">Testy integrace otestovat konfiguraci systému a zajistit, že při integraci s ostatními součástmi, systém je nastaven podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="149e7-212">The integration tests test the configuration of the system to ensure that when integrated with other components, the system is configured as expected.</span></span> <span data-ttu-id="149e7-213">Tyto testy se spouštějí na cílovém uzlu po byl nakonfigurován s DSC.</span><span class="sxs-lookup"><span data-stu-id="149e7-213">These tests run on the target node after it has been configured with DSC.</span></span>
<span data-ttu-id="149e7-214">Integrace zkušební skript používá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="149e7-214">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="acceptance-tests"></a><span data-ttu-id="149e7-215">Přijetí testů</span><span class="sxs-lookup"><span data-stu-id="149e7-215">Acceptance tests</span></span>

<span data-ttu-id="149e7-216">Přijetí testy testovací systém tak, aby se chová podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="149e7-216">Acceptance tests test the system to ensure that it behaves as expected.</span></span>
<span data-ttu-id="149e7-217">Například testy k zajištění, že vrací náležité informace, které při dotazu na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="149e7-217">For example, it tests to ensure a web page returns the right information when queried.</span></span>
<span data-ttu-id="149e7-218">Tyto testy spustit z cílový uzel pro otestování skutečných scénářích vzdáleně.</span><span class="sxs-lookup"><span data-stu-id="149e7-218">These tests run remotely from the target node in order to test real world scenarios.</span></span>
<span data-ttu-id="149e7-219">Integrace zkušební skript používá kombinaci [Pester](https://github.com/pester/Pester/wiki) a [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntaxe.</span><span class="sxs-lookup"><span data-stu-id="149e7-219">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

## <a name="define-the-build"></a><span data-ttu-id="149e7-220">Zadejte sestavení</span><span class="sxs-lookup"><span data-stu-id="149e7-220">Define the build</span></span>

<span data-ttu-id="149e7-221">Teď, když jsme nahrán kódu do sady TFS a podívat, jak funguje, nastavíme naše sestavení.</span><span class="sxs-lookup"><span data-stu-id="149e7-221">Now that we've uploaded our code to TFS and looked at what it does, let's define our build.</span></span>

<span data-ttu-id="149e7-222">Zde jsme zaměříme pouze kroky sestavení, které přidáte do sestavení.</span><span class="sxs-lookup"><span data-stu-id="149e7-222">Here, we'll cover only the build steps that you'll add to the build.</span></span> <span data-ttu-id="149e7-223">Pokyny k vytvoření definice sestavení v sadě TFS najdete v tématu [vytvořit a fronty pro definici buildu](https://www.visualstudio.com/en-us/docs/build/define/create).</span><span class="sxs-lookup"><span data-stu-id="149e7-223">For instructions on how to create a build definition in TFS, see [Create and queue a build definition](https://www.visualstudio.com/en-us/docs/build/define/create).</span></span>

<span data-ttu-id="149e7-224">Vytvořte novou definici sestavení (vyberte **prázdný** šablony) s názvem "InfraDNS".</span><span class="sxs-lookup"><span data-stu-id="149e7-224">Create a new build definition (select the **Empty** template) named "InfraDNS".</span></span>
<span data-ttu-id="149e7-225">Přidáte že následující kroky vám sestavení definice:</span><span class="sxs-lookup"><span data-stu-id="149e7-225">Add the following steps to you build definition:</span></span>

- <span data-ttu-id="149e7-226">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="149e7-226">PowerShell Script</span></span>
- <span data-ttu-id="149e7-227">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="149e7-227">Publish Test Results</span></span>
- <span data-ttu-id="149e7-228">Kopírování souborů</span><span class="sxs-lookup"><span data-stu-id="149e7-228">Copy Files</span></span>
- <span data-ttu-id="149e7-229">Publikování artefaktů</span><span class="sxs-lookup"><span data-stu-id="149e7-229">Publish Artifact</span></span>

<span data-ttu-id="149e7-230">Po přidání tyto kroky sestavení, upravit vlastnosti každého kroku následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="149e7-230">After adding these build steps, edit the properties of each step as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="149e7-231">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="149e7-231">PowerShell Script</span></span>

1. <span data-ttu-id="149e7-232">Nastavte **typ** vlastnost `File Path`.</span><span class="sxs-lookup"><span data-stu-id="149e7-232">Set the **Type** property to `File Path`.</span></span>
1. <span data-ttu-id="149e7-233">Nastavte **cestu ke skriptu** vlastnost `initiate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="149e7-233">Set the **Script Path** property to `initiate.ps1`.</span></span>
1. <span data-ttu-id="149e7-234">Přidat `-fileName build` k **argumenty** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="149e7-234">Add `-fileName build` to the **Arguments** property.</span></span>

<span data-ttu-id="149e7-235">Tento krok sestavení běží `initiate.ps1` souboru, který volá psake skriptu buildu.</span><span class="sxs-lookup"><span data-stu-id="149e7-235">This build step runs the `initiate.ps1` file, which calls the psake build script.</span></span>

### <a name="publish-test-results"></a><span data-ttu-id="149e7-236">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="149e7-236">Publish Test Results</span></span>

1. <span data-ttu-id="149e7-237">Nastavit **testování výsledný formát** na `NUnit`</span><span class="sxs-lookup"><span data-stu-id="149e7-237">Set **Test Result Format** to `NUnit`</span></span>
1. <span data-ttu-id="149e7-238">Nastavit **výsledky testu soubory** do `InfraDNS/Tests/Results/*.xml`</span><span class="sxs-lookup"><span data-stu-id="149e7-238">Set **Test Results Files** to `InfraDNS/Tests/Results/*.xml`</span></span>
1. <span data-ttu-id="149e7-239">Nastavit **testování název běhu** k `Unit`.</span><span class="sxs-lookup"><span data-stu-id="149e7-239">Set **Test Run Title** to `Unit`.</span></span>
1. <span data-ttu-id="149e7-240">Zajistěte, aby **možnosti řízení** **povoleno** a **vždy spustit** jsou obě vybrané.</span><span class="sxs-lookup"><span data-stu-id="149e7-240">Make sure **Control Options** **Enabled** and **Always run** are both selected.</span></span>

<span data-ttu-id="149e7-241">Tento krok sestavení spustí testy jednotek ve skriptu Pester jsme se podívali na dříve a ukládá výsledky do `InfraDNS/Tests/Results/*.xml` složky.</span><span class="sxs-lookup"><span data-stu-id="149e7-241">This build step runs the unit tests in the Pester script we looked at earlier, and stores the results in the `InfraDNS/Tests/Results/*.xml` folder.</span></span>

### <a name="copy-files"></a><span data-ttu-id="149e7-242">Kopírování souborů</span><span class="sxs-lookup"><span data-stu-id="149e7-242">Copy Files</span></span>

1. <span data-ttu-id="149e7-243">Přidejte všechny následující řádky, které se **obsah**:</span><span class="sxs-lookup"><span data-stu-id="149e7-243">Add each of the following lines to **Contents**:</span></span>

   ```
   initiate.ps1
   **\deploy.ps1
   **\Acceptance\**
   **\Integration\**
   ```

1. <span data-ttu-id="149e7-244">Nastavit **TargetFolder** na `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="149e7-244">Set **TargetFolder** to `$(Build.ArtifactStagingDirectory)\`</span></span>

<span data-ttu-id="149e7-245">Tento krok zkopíruje sestavení a testů skriptů do pracovního adresáře, který lze publikovat, protože sestavení artefaktů dalším krokem.</span><span class="sxs-lookup"><span data-stu-id="149e7-245">This step copies the build and test scripts to the staging directory so that the can be published as build artifacts by the next step.</span></span>

### <a name="publish-artifact"></a><span data-ttu-id="149e7-246">Publikování artefaktů</span><span class="sxs-lookup"><span data-stu-id="149e7-246">Publish Artifact</span></span>

1. <span data-ttu-id="149e7-247">Nastavit **cestu k publikování** na `$(Build.ArtifactStagingDirectory)\`</span><span class="sxs-lookup"><span data-stu-id="149e7-247">Set **Path to Publish** to `$(Build.ArtifactStagingDirectory)\`</span></span>
1. <span data-ttu-id="149e7-248">Nastavit **artefaktů název** na `Deploy`</span><span class="sxs-lookup"><span data-stu-id="149e7-248">Set **Artifact Name** to `Deploy`</span></span>
1. <span data-ttu-id="149e7-249">Nastavit **typu artefaktu** na `Server`</span><span class="sxs-lookup"><span data-stu-id="149e7-249">Set **Artifact Type** to `Server`</span></span>
1. <span data-ttu-id="149e7-250">Vyberte `Enabled` v **řízení možností**</span><span class="sxs-lookup"><span data-stu-id="149e7-250">Select `Enabled` in **Control Options**</span></span>

## <a name="enable-continuous-integration"></a><span data-ttu-id="149e7-251">Povolit průběžnou integraci</span><span class="sxs-lookup"><span data-stu-id="149e7-251">Enable continuous integration</span></span>

<span data-ttu-id="149e7-252">Nyní nastavíme aktivační událost, která způsobí, že projekt sestavení kdykoli změnu se změnami do `ci-cd-example` větve úložiště git.</span><span class="sxs-lookup"><span data-stu-id="149e7-252">Now we'll set up a trigger that causes the project to build any time a change is checked in to the `ci-cd-example` branch of the git repository.</span></span>

1. <span data-ttu-id="149e7-253">V sadě TFS, klikněte **sestavení a verze** karta</span><span class="sxs-lookup"><span data-stu-id="149e7-253">In TFS, click the **Build & Release** tab</span></span>
1. <span data-ttu-id="149e7-254">Vyberte `DNS Infra` definice sestavení a klikněte na tlačítko **upravit**</span><span class="sxs-lookup"><span data-stu-id="149e7-254">Select the `DNS Infra` build definition, and click **Edit**</span></span>
1. <span data-ttu-id="149e7-255">Klikněte **aktivační události** karta</span><span class="sxs-lookup"><span data-stu-id="149e7-255">Click the **Triggers** tab</span></span>
1. <span data-ttu-id="149e7-256">Vyberte **průběžnou integraci (CI)** a vyberte `refs/heads/ci-cd-example` v rozevíracím seznamu firemní pobočky</span><span class="sxs-lookup"><span data-stu-id="149e7-256">Select **Continuous integration (CI)**, and select `refs/heads/ci-cd-example` in the branch drop-down list</span></span>
1. <span data-ttu-id="149e7-257">Klikněte na tlačítko **Uložit** a potom **OK**</span><span class="sxs-lookup"><span data-stu-id="149e7-257">Click **Save** and then **OK**</span></span>

<span data-ttu-id="149e7-258">Nyní každé změně aktivačních událostí úložišti git sady TFS automatizované sestavení.</span><span class="sxs-lookup"><span data-stu-id="149e7-258">Now any change in the TFS git repository triggers an automated build.</span></span>

## <a name="create-the-release-definition"></a><span data-ttu-id="149e7-259">Vytvořit definici verze</span><span class="sxs-lookup"><span data-stu-id="149e7-259">Create the release definition</span></span>

<span data-ttu-id="149e7-260">Umožňuje vytvořit definici verze tak, aby nasazení projektu do vývojového prostředí s každou změnami kódu.</span><span class="sxs-lookup"><span data-stu-id="149e7-260">Let's create a release definition so that the project is deployed to the development environment with every code check-in.</span></span>

<span data-ttu-id="149e7-261">K tomuto účelu přidání nové verze definice přidružené `InfraDNS` sestavení definice, které jste předtím vytvořili.</span><span class="sxs-lookup"><span data-stu-id="149e7-261">To do this, add a new release definition associated with the `InfraDNS` build definition you created previously.</span></span>
<span data-ttu-id="149e7-262">Je nutné vybrat **průběžné nasazování** tak, aby nové verze aktivuje vždy, když je dokončena nové sestavení.</span><span class="sxs-lookup"><span data-stu-id="149e7-262">Be sure to select **Continuous deployment** so that a new release will be triggered any time a new build is completed.</span></span>
<span data-ttu-id="149e7-263">([Postupy: práce s verzí definice](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) a nakonfigurovat následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="149e7-263">([How to: Work with release definitions](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) and configure it as follows:</span></span>

<span data-ttu-id="149e7-264">Přidáte následující kroky k definici verze:</span><span class="sxs-lookup"><span data-stu-id="149e7-264">Add the following steps to the release definition:</span></span>

- <span data-ttu-id="149e7-265">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="149e7-265">PowerShell Script</span></span>
- <span data-ttu-id="149e7-266">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="149e7-266">Publish Test Results</span></span>
- <span data-ttu-id="149e7-267">Publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="149e7-267">Publish Test Results</span></span>

<span data-ttu-id="149e7-268">Postup úpravy následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="149e7-268">Edit the steps as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="149e7-269">Skript prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="149e7-269">PowerShell Script</span></span>

1. <span data-ttu-id="149e7-270">Nastavte **cestu ke skriptu** do `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span><span class="sxs-lookup"><span data-stu-id="149e7-270">Set the **Script Path** field to `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span></span>
1. <span data-ttu-id="149e7-271">Nastavte **argumenty** do `-fileName Deploy`</span><span class="sxs-lookup"><span data-stu-id="149e7-271">Set the **Arguments** field to `-fileName Deploy`</span></span>

### <a name="first-publish-test-results"></a><span data-ttu-id="149e7-272">Nejprve publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="149e7-272">First Publish Test Results</span></span>

1. <span data-ttu-id="149e7-273">Vyberte `NUnit` pro **testovací výsledný formát** pole</span><span class="sxs-lookup"><span data-stu-id="149e7-273">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="149e7-274">Nastavte **testovací soubory výsledek** do `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span><span class="sxs-lookup"><span data-stu-id="149e7-274">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span></span>
1. <span data-ttu-id="149e7-275">Nastavte **testování název běhu** na `Integration`</span><span class="sxs-lookup"><span data-stu-id="149e7-275">Set the **Test Run Title** to `Integration`</span></span>
1. <span data-ttu-id="149e7-276">V části **možnosti řízení**, zkontrolujte **vždy spustit.**</span><span class="sxs-lookup"><span data-stu-id="149e7-276">Under **Control Options**, check **Always run**</span></span>

### <a name="second-publish-test-results"></a><span data-ttu-id="149e7-277">Druhý publikování výsledků testů</span><span class="sxs-lookup"><span data-stu-id="149e7-277">Second Publish Test Results</span></span>

1. <span data-ttu-id="149e7-278">Vyberte `NUnit` pro **testovací výsledný formát** pole</span><span class="sxs-lookup"><span data-stu-id="149e7-278">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="149e7-279">Nastavte **testovací soubory výsledek** do `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span><span class="sxs-lookup"><span data-stu-id="149e7-279">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span></span>
1. <span data-ttu-id="149e7-280">Nastavte **testování název běhu** na `Acceptance`</span><span class="sxs-lookup"><span data-stu-id="149e7-280">Set the **Test Run Title** to `Acceptance`</span></span>
1. <span data-ttu-id="149e7-281">V části **možnosti řízení**, zkontrolujte **vždy spustit.**</span><span class="sxs-lookup"><span data-stu-id="149e7-281">Under **Control Options**, check **Always run**</span></span>

## <a name="verify-your-results"></a><span data-ttu-id="149e7-282">Zkontrolujte výsledky</span><span class="sxs-lookup"><span data-stu-id="149e7-282">Verify your results</span></span>

<span data-ttu-id="149e7-283">Nyní, kdykoli nabízené změny `ci-cd-example` spustí větev do sady TFS, nové sestavení.</span><span class="sxs-lookup"><span data-stu-id="149e7-283">Now, any time you push changes in the `ci-cd-example` branch to TFS, a new build will start.</span></span>
<span data-ttu-id="149e7-284">Sestavení se dokončí úspěšně, aktivuje se nové nasazení.</span><span class="sxs-lookup"><span data-stu-id="149e7-284">If the build completes successfully, a new deployment is triggered.</span></span>

<span data-ttu-id="149e7-285">Výsledek nasazení můžete zkontrolovat otevřením prohlížeče v klientském počítači a přejdete na `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="149e7-285">You can check the result of the deployment by opening a browser on the client machine and navigating to `www.contoso.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="149e7-286">Další kroky</span><span class="sxs-lookup"><span data-stu-id="149e7-286">Next steps</span></span>

<span data-ttu-id="149e7-287">Tento příklad konfiguruje DNS server `TestAgent1` tak, aby adresa URL `www.contoso.com` přeloží na `TestAgent2`, ale ve skutečnosti Nenasazuje webu.</span><span class="sxs-lookup"><span data-stu-id="149e7-287">This example configures the DNS server `TestAgent1` so that the URL `www.contoso.com` resolves to `TestAgent2`, but it does not actually deploy a website.</span></span>
<span data-ttu-id="149e7-288">Kostru jak to udělat najdete v úložišti v části `WebApp` složky.</span><span class="sxs-lookup"><span data-stu-id="149e7-288">The skeleton for doing so is provided in the repo under the `WebApp` folder.</span></span>
<span data-ttu-id="149e7-289">Zástupných procedur zadaná k vytvoření psake skripty, Pester testy a konfigurace DSC můžete použít k nasazení vlastního webu.</span><span class="sxs-lookup"><span data-stu-id="149e7-289">You can use the stubs provided to create psake scripts, Pester tests, and DSC configurations to deploy your own website.</span></span>
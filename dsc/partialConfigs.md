---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Částečné konfigurace prostředí PowerShell Desired State Configuration
ms.openlocfilehash: 1f5ec5bd5055ccc3d83a60712aebe635f2548828
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892997"
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a><span data-ttu-id="080e2-103">Částečné konfigurace prostředí PowerShell Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="080e2-103">PowerShell Desired State Configuration partial configurations</span></span>

> <span data-ttu-id="080e2-104">Platí pro: Windows PowerShell 5.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="080e2-104">Applies To: Windows PowerShell 5.0 and later.</span></span>

<span data-ttu-id="080e2-105">Desired State Configuration (DSC) v Powershellu 5.0 umožňuje konfigurace, které se dodávají v fragmentů a z více zdrojů.</span><span class="sxs-lookup"><span data-stu-id="080e2-105">In PowerShell 5.0, Desired State Configuration (DSC) allows configurations to be delivered in fragments and from multiple sources.</span></span> <span data-ttu-id="080e2-106">Tyto fragmenty místní Configuration Manageru (LCM) na cílovém uzlu společně vloží před jejich použitím jako jediné konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="080e2-106">The Local Configuration Manager (LCM) on the target node puts the fragments together before applying them as a single configuration.</span></span> <span data-ttu-id="080e2-107">Tato možnost umožňuje kontrolu nad konfigurací mezi týmy nebo jednotlivce, pro sdílení obsahu.</span><span class="sxs-lookup"><span data-stu-id="080e2-107">This capability allows sharing control of configuration between teams or individuals.</span></span>
<span data-ttu-id="080e2-108">Například pokud dva nebo více týmů vývojářů spolupracují na službě, může každý chtějí vytvořit konfigurace pro správu jejich součástí služby.</span><span class="sxs-lookup"><span data-stu-id="080e2-108">For example, if two or more teams of developers are collaborating on a service, they might each want to create configurations to manage their part of the service.</span></span> <span data-ttu-id="080e2-109">Každá z těchto konfigurací může získaných z různých o přijetí změn servery a může být přidán v různých fázích vývoje.</span><span class="sxs-lookup"><span data-stu-id="080e2-109">Each of these configurations could be pulled from different pull servers, and they could be added at different stages of development.</span></span> <span data-ttu-id="080e2-110">Částečné konfigurace také povolit různí jednotlivci nebo týmy ovládat různé aspekty konfigurace uzlů bez nutnosti ke koordinaci úpravy dokumentu jediné konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="080e2-110">Partial configurations also allow different individuals or teams to control different aspects of configuring nodes without having to coordinate the editing of a single configuration document.</span></span> <span data-ttu-id="080e2-111">Například může být jeden tým odpovědného za nasazení virtuálního počítače a operačního systému, zatímco jiný tým může nasadit další aplikace a služby na tomto virtuálním počítači.</span><span class="sxs-lookup"><span data-stu-id="080e2-111">For example, one team might be responsible for deploying a VM and operating system, while another team might deploy other applications and services on that VM.</span></span> <span data-ttu-id="080e2-112">Konfigurací částečného každý tým může vytvořit své vlastní konfigurace bez některou z nich se zbytečně složité.</span><span class="sxs-lookup"><span data-stu-id="080e2-112">With partial configurations, each team can create its own configuration, without either of them being unnecessarily complicated.</span></span>

<span data-ttu-id="080e2-113">Můžete použít částečné konfigurace v režimu nabízení, režimu o přijetí změn nebo kombinaci obojího.</span><span class="sxs-lookup"><span data-stu-id="080e2-113">You can use partial configurations in push mode, pull mode, or a combination of the two.</span></span>

## <a name="partial-configurations-in-push-mode"></a><span data-ttu-id="080e2-114">Částečné konfigurace v režimu nabízení</span><span class="sxs-lookup"><span data-stu-id="080e2-114">Partial configurations in push mode</span></span>

<span data-ttu-id="080e2-115">Částečné konfigurace v režimu nabízení, můžete nakonfigurovat LCM na cílovém uzlu přijímat částečné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="080e2-115">To use partial configurations in push mode, you configure the LCM on the target node to receive the partial configurations.</span></span> <span data-ttu-id="080e2-116">Každá částečné konfigurace musí doručit bez vyžádání do cíle pomocí `Publish-DSCConfiguration` rutiny.</span><span class="sxs-lookup"><span data-stu-id="080e2-116">Each partial configuration must be pushed to the target by using the `Publish-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="080e2-117">Cílový uzel pak kombinuje částečné konfigurace do jediné konfiguraci a můžete provést konfiguraci pomocí volání [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="080e2-117">The target node then combines the partial configuration into a single configuration, and you can apply the configuration by calling the [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) cmdlet.</span></span>

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a><span data-ttu-id="080e2-118">Konfigurace LCM pro režimu nabízení částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="080e2-118">Configuring the LCM for push-mode partial configurations</span></span>

<span data-ttu-id="080e2-119">Konfigurace LCM pro částečné konfigurace v režimu nabízení, vytvoříte **DSCLocalConfigurationManager** konfiguraci s jednou **PartialConfiguration** blok pro každou částečné konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="080e2-119">To configure the LCM for partial configurations in push mode, you create a **DSCLocalConfigurationManager** configuration with one **PartialConfiguration** block for each partial configuration.</span></span> <span data-ttu-id="080e2-120">Další informace týkající se konfigurace LCM v tématu [Windows konfigurace Local Configuration Manageru](/powershell/dsc/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="080e2-120">For more information about configuring the LCM, see [Windows Configuring the Local Configuration Manager](/powershell/dsc/metaConfig).</span></span>
<span data-ttu-id="080e2-121">Následující příklad ukazuje LCM konfigurace, který očekává, že dvě částečné konfigurace – ten, který se nasadí operační systém a jednu, která nasazuje a konfiguruje službu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="080e2-121">The following example shows an LCM configuration that expects two partial configurations—one that deploys the OS, and one that deploys and configures SharePoint.</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {

        PartialConfiguration ServiceAccountConfig
        {
            Description = 'Configuration to add the SharePoint service account to the Administrators group.'
            RefreshMode = 'Push'
        }
           PartialConfiguration SharePointConfig
        {
            Description = 'Configuration for the SharePoint server'
            RefreshMode = 'Push'
        }
    }
}

PartialConfigDemo
```

<span data-ttu-id="080e2-122">**RefreshMode** pro každou konfiguraci částečné je nastaven na hodnotu "Push".</span><span class="sxs-lookup"><span data-stu-id="080e2-122">The **RefreshMode** for each partial configuration is set to "Push".</span></span> <span data-ttu-id="080e2-123">Názvy **PartialConfiguration** bloky (v tomto případě "ServiceAccountConfig" a "SharePointConfig") musí odpovídat přesně názvy konfigurace, které se odesílají na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="080e2-123">The names of the **PartialConfiguration** blocks (in this case, "ServiceAccountConfig" and "SharePointConfig") must match exactly the names of the configurations that are pushed to the target node.</span></span>

> [!Note]
> <span data-ttu-id="080e2-124">Pojmenované jednotlivých **PartialConfiguration** bloku musí odpovídat skutečný název konfigurace, protože je zadán v konfigurační skript, nikoli název souboru MOF, který by měl být název cílový uzel nebo `localhost`.</span><span class="sxs-lookup"><span data-stu-id="080e2-124">The named of each **PartialConfiguration** block must match the actual name of the configuration as it is specified in the configuration script, not the name of the MOF file, which should be either the name of the target node or `localhost`.</span></span>

### <a name="publishing-and-starting-push-mode-partial-configurations"></a><span data-ttu-id="080e2-125">Publikování a spuštění režimu nabízení částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="080e2-125">Publishing and starting push-mode partial configurations</span></span>

<span data-ttu-id="080e2-126">Poté je zapotřebí zavolat [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) pro každou konfiguraci předávání složky, která obsahují dokumenty konfigurace jako **cesta** parametry.</span><span class="sxs-lookup"><span data-stu-id="080e2-126">You then call [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) for each configuration, passing the folders that contain the configuration documents as the **Path** parameters.</span></span> <span data-ttu-id="080e2-127">`Publish-DSCConfiguration`umístí konfigurační soubory MOF a cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="080e2-127">`Publish-DSCConfiguration`places the configuration MOF files to the target nodes.</span></span> <span data-ttu-id="080e2-128">Po publikování obě konfigurace, můžete volat `Start-DSCConfiguration –UseExisting` na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="080e2-128">After publishing both configurations, you can call `Start-DSCConfiguration –UseExisting` on the target node.</span></span>

<span data-ttu-id="080e2-129">Například, pokud jste zkompilovali následující dokumenty MOF konfigurace uzlu pro vytváření obsahu:</span><span class="sxs-lookup"><span data-stu-id="080e2-129">For example, if you have compiled the following configuration MOF documents on the authoring node:</span></span>

```powershell
Get-ChildItem -Recurse
```

```output
    Directory: C:\PartialConfigTest

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        8/11/2016   1:55 PM                ServiceAccountConfig
d-----       11/17/2016   4:14 PM                SharePointConfig

    Directory: C:\PartialConfigTest\ServiceAccountConfig

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        8/11/2016   2:02 PM           2034 TestVM.mof

    Directory: C:\DscTests\SharePointConfig

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       11/17/2016   4:14 PM           1930 TestVM.mof
```

<span data-ttu-id="080e2-130">By publikovat a spustit konfiguraci následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="080e2-130">You would publish and run the configurations as follows:</span></span>

```powershell
Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
Start-DscConfiguration -UseExisting -ComputerName 'TestVM'
```

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

> [!Note]
> <span data-ttu-id="080e2-131">Uživatel, který spustil [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) rutina musí mít oprávnění správce na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="080e2-131">The user running the [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) cmdlet must have administrator privileges on the target node.</span></span>

## <a name="partial-configurations-in-pull-mode"></a><span data-ttu-id="080e2-132">Částečné konfigurace v režimu o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="080e2-132">Partial configurations in pull mode</span></span>

<span data-ttu-id="080e2-133">Částečné konfigurace můžete načíst z jednoho nebo více serverů o přijetí změn (Další informace o serverech o přijetí změn najdete v tématu [Windows PowerShell Desired State Configuration o přijetí změn servery](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="080e2-133">Partial configurations can be pulled from one or more pull servers (for more information about pull servers, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="080e2-134">Chcete-li to provést, musíte nakonfigurovat LCM na cílový uzel k vyžádání částečné konfigurace a název a vyhledejte dokumenty konfigurace správně na serverech o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="080e2-134">To do this, you have to configure the LCM on the target node to pull the partial configurations, and name and locate the configuration documents properly on the pull servers.</span></span>

### <a name="configuring-the-lcm-for-pull-node-configurations"></a><span data-ttu-id="080e2-135">Konfigurace LCM pro o přijetí změn konfigurace uzlu</span><span class="sxs-lookup"><span data-stu-id="080e2-135">Configuring the LCM for pull node configurations</span></span>

<span data-ttu-id="080e2-136">Konfigurace LCM přetahování částečné konfigurace ze serveru vyžádané replikace, definujete v jednom serveru vyžádané replikace **ConfigurationRepositoryWeb** (pro vyžádání obsahu server HTTP) nebo **ConfigurationRepositoryShare** () pro serveru vyžádané replikace SMB) bloku.</span><span class="sxs-lookup"><span data-stu-id="080e2-136">To configure the LCM to pull partial configurations from a pull server, you define the pull server in either a **ConfigurationRepositoryWeb** (for an HTTP pull server) or **ConfigurationRepositoryShare** (for an SMB pull server) block.</span></span> <span data-ttu-id="080e2-137">Pak vytvoříte **PartialConfiguration** bloky, které odkazují na serveru vyžádané replikace s použitím **ConfigurationSource** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="080e2-137">You then create **PartialConfiguration** blocks that refer to the pull server by using the **ConfigurationSource** property.</span></span> <span data-ttu-id="080e2-138">Je také potřeba vytvořit **nastavení** bloku k určení, že LCM používá režim o přijetí změn a k určení **ConfigurationNames** nebo **ConfigurationID** , který serveru vyžádané replikace a Cílový uzel použijte k identifikaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="080e2-138">You also need to create a **Settings** block to specify that the LCM uses pull mode, and to specify the **ConfigurationNames** or **ConfigurationID** that the pull server and target node use to identify the configurations.</span></span> <span data-ttu-id="080e2-139">Definuje následující meta konfigurace serveru HTTP o přijetí změn s názvem CONTOSO-PullSrv a dvě částečné konfigurace, které používají, které server vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="080e2-139">The following meta-configuration defines an HTTP pull server named CONTOSO-PullSrv and two partial configurations that use that pull server.</span></span>

<span data-ttu-id="080e2-140">Další informace o konfiguraci pomocí LCM **ConfigurationNames**, naleznete v tématu [nastavení načítacího klienta použití konfiguračních názvů](pullClientConfigNames.md).</span><span class="sxs-lookup"><span data-stu-id="080e2-140">For more information about configuring the LCM using **ConfigurationNames**, see [Setting up a pull client using configuration names](pullClientConfigNames.md).</span></span>
<span data-ttu-id="080e2-141">Informace o konfiguraci pomocí LCM **ConfigurationID**, naleznete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="080e2-141">For information about configuring the LCM using **ConfigurationID**, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a><span data-ttu-id="080e2-142">Konfigurace LCM pro použití konfiguračních názvů konfigurace režimu o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="080e2-142">Configuring the LCM for pull mode configurations using configuration names</span></span>

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               ="ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
        }
}
```

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a><span data-ttu-id="080e2-143">Konfigurace LCM pro vyžádání obsahu režim konfigurace pomocí ConfigurationID</span><span class="sxs-lookup"><span data-stu-id="080e2-143">Configuring the LCM for pull mode configurations using ConfigurationID</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemoConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode                     = 'Pull'
            ConfigurationID                 = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins            = 30
            RebootNodeIfNeeded              = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description                     = 'Configuration for the Base OS'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode                     = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description                     = 'Configuration for the Sharepoint Server'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Pull'
        }
    }
}
PartialConfigDemo
```

<span data-ttu-id="080e2-144">Částečné konfigurace z více než jednom serveru o přijetí změn si můžete vyžádat – stačí je třeba definovat každého serveru vyžádané replikace, a přečtěte si informace na server příslušné o přijetí změn v každém **PartialConfiguration** bloku.</span><span class="sxs-lookup"><span data-stu-id="080e2-144">You can pull partial configurations from more than one pull server—you would just need to define each pull server, and then refer to the appropriate pull server in each **PartialConfiguration** block.</span></span>

<span data-ttu-id="080e2-145">Po vytvoření meta konfigurace, musíte spustit vytvořit dokument konfigurace (soubor MOF), a poté zavolejte [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) konfigurace LCM.</span><span class="sxs-lookup"><span data-stu-id="080e2-145">After creating the meta-configuration, you must run it to create a configuration document (a MOF file), and then call [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) to configure the LCM.</span></span>

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a><span data-ttu-id="080e2-146">Názvy a umístění konfigurace dokumentů na serveru vyžádané replikace (ConfigurationNames)</span><span class="sxs-lookup"><span data-stu-id="080e2-146">Naming and placing the configuration documents on the pull server (ConfigurationNames)</span></span>

<span data-ttu-id="080e2-147">Částečné konfigurace dokumenty musí být umístěné ve složce určené jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="080e2-147">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span>

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a><span data-ttu-id="080e2-148">Pojmenování konfigurace dokumentů na serveru vyžádané replikace v prostředí PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="080e2-148">Naming configuration documents on the pull server in PowerShell 5.1</span></span>

<span data-ttu-id="080e2-149">Pokud se souhrnné informace pouze jedna částečná konfigurace z jednotlivých načítacího serveru, dokument konfigurace může mít libovolný název.</span><span class="sxs-lookup"><span data-stu-id="080e2-149">If you are pulling only one partial configuration from an individual pull server, the configuration document can have any name.</span></span>
<span data-ttu-id="080e2-150">Pokud se stahování více než jedna částečná konfigurace ze serveru vyžádané replikace, dokument konfigurace může mít název buď `<ConfigurationName>.mof`, kde *ConfigurationName* je název částečné konfigurace nebo `<ConfigurationName>.<NodeName>.mof`, kde  *ConfigurationName* je název částečné konfigurace a *NodeName* je název cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="080e2-150">If you are pulling more than one partial configuration from a pull server, the configuration document can be named either `<ConfigurationName>.mof`, where *ConfigurationName* is the name of the partial configuration, or `<ConfigurationName>.<NodeName>.mof`, where  *ConfigurationName* is the name of the partial configuration, and *NodeName* is the name of the target node.</span></span>
<span data-ttu-id="080e2-151">To vám umožní o přijetí změn konfigurace z načítacího serveru Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="080e2-151">This allows you to pull configurations from Azure Automation DSC pull server.</span></span>

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a><span data-ttu-id="080e2-152">Pojmenování konfigurace dokumentů na serveru vyžádané replikace v Powershellu 5.0</span><span class="sxs-lookup"><span data-stu-id="080e2-152">Naming configuration documents on the pull server in PowerShell 5.0</span></span>

<span data-ttu-id="080e2-153">Konfigurace dokumenty musí mít název takto: `ConfigurationName.mof`, kde *ConfigurationName* je název částečné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="080e2-153">The configuration documents must be named as follows: `ConfigurationName.mof`, where *ConfigurationName* is the name of the partial configuration.</span></span> <span data-ttu-id="080e2-154">V našem příkladu by měl být pojmenován dokumenty konfigurace následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="080e2-154">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a><span data-ttu-id="080e2-155">Názvy a umístění konfigurace dokumentů na serveru vyžádané replikace (ConfigurationID)</span><span class="sxs-lookup"><span data-stu-id="080e2-155">Naming and placing the configuration documents on the pull server (ConfigurationID)</span></span>

<span data-ttu-id="080e2-156">Částečné konfigurace dokumenty musí být umístěné ve složce určené jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="080e2-156">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span> <span data-ttu-id="080e2-157">Konfigurace dokumenty musí mít název takto: *ConfigurationName*.</span><span class="sxs-lookup"><span data-stu-id="080e2-157">The configuration documents must be named as follows: *ConfigurationName*.</span></span> <span data-ttu-id="080e2-158">\* ConfigurationID8`.mof`, kde *ConfigurationName* je název částečné konfigurace a *ConfigurationID* je podle ID konfigurace LCM na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="080e2-158">\*ConfigurationID8`.mof`, where *ConfigurationName* is the name of the partial configuration and *ConfigurationID* is the configuration ID defined in the LCM on the target node.</span></span> <span data-ttu-id="080e2-159">V našem příkladu by měl být pojmenován dokumenty konfigurace následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="080e2-159">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```

### <a name="running-partial-configurations-from-a-pull-server"></a><span data-ttu-id="080e2-160">Částečné konfigurace spuštěných serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="080e2-160">Running partial configurations from a pull server</span></span>

<span data-ttu-id="080e2-161">Po LCM na cílový uzel byl nakonfigurován a konfigurace dokumenty byly vytvořeny a správně s názvem na serveru vyžádané replikace cílový uzel přetáhne částečné konfigurace, je zkombinovat a použít výslednou konfiguraci podle běžného intervaly podle specifikace **RefreshFrequencyMins** vlastnost LCM.</span><span class="sxs-lookup"><span data-stu-id="080e2-161">After the LCM on the target node has been configured, and the configuration documents have been created and properly named on the pull server, the target node will pull the partial configurations, combine them, and apply the resulting configuration at regular intervals as specified by the **RefreshFrequencyMins** property of the LCM.</span></span> <span data-ttu-id="080e2-162">Pokud chcete vynutit aktualizaci, můžete volat [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) rutiny, o přijetí změn konfigurace a potom `Start-DSCConfiguration –UseExisting` jejich použití.</span><span class="sxs-lookup"><span data-stu-id="080e2-162">If you want to force a refresh, you can call the [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) cmdlet, to pull the configurations, and then `Start-DSCConfiguration –UseExisting` to apply them.</span></span>

## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a><span data-ttu-id="080e2-163">Částečné konfigurace ve smíšené režimech nabízení a vyžadování</span><span class="sxs-lookup"><span data-stu-id="080e2-163">Partial configurations in mixed push and pull modes</span></span>

<span data-ttu-id="080e2-164">Můžete také kombinovat push a pull režimy pro částečné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="080e2-164">You can also mix push and pull modes for partial configurations.</span></span> <span data-ttu-id="080e2-165">To znamená může mít jednu konfiguraci částečné, které pocházejí ze serveru vyžádané replikace, zatímco je jinou konfiguraci částečné vloženo.</span><span class="sxs-lookup"><span data-stu-id="080e2-165">That is, you could have one partial configuration that is pulled from a pull server, while another partial configuration is pushed.</span></span> <span data-ttu-id="080e2-166">Režim aktualizace pro každou konfiguraci částečné zadejte, jak je popsáno v předchozích částech.</span><span class="sxs-lookup"><span data-stu-id="080e2-166">Specify the refresh mode for each partial configuration as described in the previous sections.</span></span>
<span data-ttu-id="080e2-167">Například následující meta konfigurace popisuje stejný příklad s `ServiceAccountConfig` částečné konfigurace v režimu o přijetí změn a `SharePointConfig` částečné konfigurace v režimu nabízení.</span><span class="sxs-lookup"><span data-stu-id="080e2-167">For example, the following meta-configuration describes the same example, with the `ServiceAccountConfig` partial configuration in pull mode and the `SharePointConfig` partial configuration in push mode.</span></span>

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a><span data-ttu-id="080e2-168">Smíšené režimech nabízení a vyžadování pomocí ConfigurationNames</span><span class="sxs-lookup"><span data-stu-id="080e2-168">Mixed push and pull modes using ConfigurationNames</span></span>

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               = "ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            RefreshMode                     = 'Pull'
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Push'
        }

}
```

### <a name="mixed-push-and-pull-modes-using-configurationid"></a><span data-ttu-id="080e2-169">Smíšené režimech nabízení a vyžadování pomocí ConfigurationID</span><span class="sxs-lookup"><span data-stu-id="080e2-169">Mixed push and pull modes using ConfigurationID</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {
        Settings
        {
            RefreshMode             = 'Pull'
            ConfigurationID         = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins    = 30
            RebootNodeIfNeeded      = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL               = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description             = 'Configuration for the Base OS'
            ConfigurationSource     = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode             = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description             = 'Configuration for the Sharepoint Server'
            DependsOn               = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode             = 'Push'
        }
    }
}
PartialConfigDemo
```

<span data-ttu-id="080e2-170">Všimněte si, že **RefreshMode** zadaný v bloku nastavení je "Pull", ale **RefreshMode** pro `SharePointConfig` částečné konfigurace je "Push".</span><span class="sxs-lookup"><span data-stu-id="080e2-170">Note that the **RefreshMode** specified in the Settings block is "Pull", but the **RefreshMode** for the `SharePointConfig` partial configuration is "Push".</span></span>

<span data-ttu-id="080e2-171">Zadejte název a vyhledejte konfigurační soubory MOF, jak je popsáno výše pro režimy jejich příslušné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="080e2-171">Name and locate the configuration MOF files as described above for their respective refresh modes.</span></span> <span data-ttu-id="080e2-172">Volání `Publish-DSCConfiguration` publikovat `SharePointConfig` částečné konfigurace a buď počkejte `ServiceAccountConfig` konfigurace načíst ze serveru vyžádané replikace, nebo vynutit aktualizaci voláním [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).</span><span class="sxs-lookup"><span data-stu-id="080e2-172">Call `Publish-DSCConfiguration` to publish the `SharePointConfig` partial configuration, and either wait for the `ServiceAccountConfig` configuration to be pulled from the pull server, or force a refresh by calling [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).</span></span>

## <a name="example-serviceaccountconfig-partial-configuration"></a><span data-ttu-id="080e2-173">Příklad ServiceAccountConfig částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="080e2-173">Example ServiceAccountConfig Partial Configuration</span></span>

```powershell
Configuration ServiceAccountConfig
{
    Param (
        [Parameter(Mandatory,
                   HelpMessage="Domain credentials required to add domain\sharepoint_svc to the local Administrators group.")]
        [ValidateNotNullOrEmpty()]
        [pscredential]$Credential
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration


    Node localhost
    {
        Group LocalAdmins
        {
            GroupName           = 'Administrators'
            MembersToInclude    = 'domain\sharepoint_svc',
                                  'admins@example.domain'
            Ensure              = 'Present'
            Credential          = $Credential

        }

        WindowsFeature Telnet
        {
            Name                = 'Telnet-Server'
            Ensure              = 'Absent'
        }
    }
}
ServiceAccountConfig

```

## <a name="example-sharepointconfig-partial-configuration"></a><span data-ttu-id="080e2-174">Příklad SharePointConfig částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="080e2-174">Example SharePointConfig Partial Configuration</span></span>

```powershell
Configuration SharePointConfig
{
    Param (
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [pscredential]$ProductKey
    )

    Import-DscResource -ModuleName xSharePoint

    Node localhost
    {
        xSPInstall SharePointDefault
        {
            Ensure      = 'Present'
            BinaryDir   = '\\FileServer\Installers\Sharepoint\'
            ProductKey  = $ProductKey
        }
    }
}
SharePointConfig
```

## <a name="see-also"></a><span data-ttu-id="080e2-175">Viz také</span><span class="sxs-lookup"><span data-stu-id="080e2-175">See Also</span></span>

[<span data-ttu-id="080e2-176">Prostředí Windows PowerShell Desired State Configuration servery o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="080e2-176">Windows PowerShell Desired State Configuration Pull Servers</span></span>](pullServer.md)

[<span data-ttu-id="080e2-177">Konfigurace Local Configuration Manageru Windows</span><span class="sxs-lookup"><span data-stu-id="080e2-177">Windows Configuring the Local Configuration Manager</span></span>](/powershell/dsc/metaConfig)
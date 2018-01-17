---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Konfigurace požadovaného stavu prostředí PowerShell částečné konfigurace"
ms.openlocfilehash: 66791bb7b14898d292b9da38dd27ba45b7c75d88
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a><span data-ttu-id="2e978-103">Konfigurace požadovaného stavu prostředí PowerShell částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="2e978-103">PowerShell Desired State Configuration partial configurations</span></span>

><span data-ttu-id="2e978-104">Platí pro: Prostředí Windows PowerShell 5.0 a novější.</span><span class="sxs-lookup"><span data-stu-id="2e978-104">Applies To: Windows PowerShell 5.0 and later.</span></span>

<span data-ttu-id="2e978-105">Konfigurace požadovaného stavu (DSC) v prostředí PowerShell 5.0 umožňuje konfigurace, který bude doručen v fragmenty a z více zdrojů.</span><span class="sxs-lookup"><span data-stu-id="2e978-105">In PowerShell 5.0, Desired State Configuration (DSC) allows configurations to be delivered in fragments and from multiple sources.</span></span> <span data-ttu-id="2e978-106">Místní Configuration Manager (LCM) na cílovém uzlu fragmenty umístí společně před jejich použití jako jedna konfigurační.</span><span class="sxs-lookup"><span data-stu-id="2e978-106">The Local Configuration Manager (LCM) on the target node puts the fragments together before applying them as a single configuration.</span></span> <span data-ttu-id="2e978-107">Tato možnost umožňuje sdílení kontrolu nad konfiguraci mezi týmy nebo jednotlivce.</span><span class="sxs-lookup"><span data-stu-id="2e978-107">This capability allows sharing control of configuration between teams or individuals.</span></span> <span data-ttu-id="2e978-108">Například pokud dva nebo více týmy vývojářů spolupracují na službě, může každý chtějí vytvořit konfigurace ke správě jejich součástí služby.</span><span class="sxs-lookup"><span data-stu-id="2e978-108">For example, if two or more teams of developers are collaborating on a service, they might each want to create configurations to manage their part of the service.</span></span> <span data-ttu-id="2e978-109">Každý z těchto konfigurací může vyžádat ze serverů různých vyžádání obsahu a nebylo možné přidat v různých fázích vývoje.</span><span class="sxs-lookup"><span data-stu-id="2e978-109">Each of these configurations could be pulled from different pull servers, and they could be added at different stages of development.</span></span> <span data-ttu-id="2e978-110">Různí jednotlivci nebo týmy ovládat různé aspekty konfigurace uzlů bez nutnosti ke koordinaci úpravy dokumentu jedna konfigurační také umožňuje částečné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2e978-110">Partial configurations also allow different individuals or teams to control different aspects of configuring nodes without having to coordinate the editing of a single configuration document.</span></span> <span data-ttu-id="2e978-111">Například může být jeden tým odpovědný pro nasazení virtuálního počítače a operačního systému, může jiného týmu nasazení dalších aplikací a služeb na tento virtuální počítač.</span><span class="sxs-lookup"><span data-stu-id="2e978-111">For example, one team might be responsible for deploying a VM and operating system, while another team might deploy other applications and services on that VM.</span></span> <span data-ttu-id="2e978-112">S konfigurací částečné každý tým můžete vytvořit vlastní konfiguraci, bez buď z nich se zbytečně komplikovanější.</span><span class="sxs-lookup"><span data-stu-id="2e978-112">With partial configurations, each team can create its own configuration, without either of them being unnecessarily complicated.</span></span>

<span data-ttu-id="2e978-113">Můžete použít částečný konfigurace v režimu push, pull režimu nebo kombinaci těchto dvou.</span><span class="sxs-lookup"><span data-stu-id="2e978-113">You can use partial configurations in push mode, pull mode, or a combination of the two.</span></span>

## <a name="partial-configurations-in-push-mode"></a><span data-ttu-id="2e978-114">Částečné konfigurace v režimu nabízení</span><span class="sxs-lookup"><span data-stu-id="2e978-114">Partial configurations in push mode</span></span>
<span data-ttu-id="2e978-115">V režimu nabízená použít částečný konfigurace, nakonfigurujte LCM na cílový uzel pro příjem částečné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2e978-115">To use partial configurations in push mode, you configure the LCM on the target node to receive the partial configurations.</span></span> <span data-ttu-id="2e978-116">Každá částečné konfigurace musí nabídnutých k cíli pomocí rutiny DSCConfiguration publikovat.</span><span class="sxs-lookup"><span data-stu-id="2e978-116">Each partial configuration must be pushed to the target by using the Publish-DSCConfiguration cmdlet.</span></span> <span data-ttu-id="2e978-117">Cílový uzel pak kombinuje částečné konfigurace do jedné konfigurace a konfigurace můžete použít při volání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="2e978-117">The target node then combines the partial configuration into a single configuration, and you can apply the configuration by calling the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span>

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a><span data-ttu-id="2e978-118">Konfigurace LCM pro částečné konfigurace nabízené režimu</span><span class="sxs-lookup"><span data-stu-id="2e978-118">Configuring the LCM for push-mode partial configurations</span></span>
<span data-ttu-id="2e978-119">Ke konfiguraci LCM pro částečné konfigurace v nabízené režimu, vytvoříte **DSCLocalConfigurationManager** konfigurace s jedním **PartialConfiguration** blok pro každé částečné konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="2e978-119">To configure the LCM for partial configurations in push mode, you create a **DSCLocalConfigurationManager** configuration with one **PartialConfiguration** block for each partial configuration.</span></span> <span data-ttu-id="2e978-120">Další informace o konfiguraci LCM najdete v tématu [Windows konfigurace správce místní konfigurace](https://technet.microsoft.com/en-us/library/mt421188.aspx).</span><span class="sxs-lookup"><span data-stu-id="2e978-120">For more information about configuring the LCM, see [Windows Configuring the Local Configuration Manager](https://technet.microsoft.com/en-us/library/mt421188.aspx).</span></span> <span data-ttu-id="2e978-121">Následující příklad ukazuje konfigurace aplikace LCM, která očekává dvě konfigurace částečné – jednu, která nasazuje operační systém a ten, který nasadí a nakonfiguruje služby SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2e978-121">The following example shows an LCM configuration that expects two partial configurations—one that deploys the OS, and one that deploys and configures SharePoint.</span></span>

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

<span data-ttu-id="2e978-122">**RefreshMode** pro každý částečné konfigurace je nastavena na "Push".</span><span class="sxs-lookup"><span data-stu-id="2e978-122">The **RefreshMode** for each partial configuration is set to "Push".</span></span> <span data-ttu-id="2e978-123">Názvy **PartialConfiguration** bloky (v tomto případě "ServiceAccountConfig" a "SharePointConfig") musí odpovídat přesně názvy konfigurace, které odesílají na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="2e978-123">The names of the **PartialConfiguration** blocks (in this case, "ServiceAccountConfig" and "SharePointConfig") must match exactly the names of the configurations that are pushed to the target node.</span></span>

><span data-ttu-id="2e978-124">**Poznámka:** pojmenované jednotlivých **PartialConfiguration** bloku musí odpovídat skutečný název konfigurace, jako jsou zadány v konfigurační skript, nikoli název souboru MOF, který musí být buď název Cílový uzel nebo `localhost`.</span><span class="sxs-lookup"><span data-stu-id="2e978-124">**Note:** The named of each **PartialConfiguration** block must match the actual name of the configuration as it is specified in the configuration script, not the name of the MOF file, which should be either the name of the target node or `localhost`.</span></span>

### <a name="publishing-and-starting-push-mode-partial-configurations"></a><span data-ttu-id="2e978-125">Publikování a počáteční konfigurace částečné nabízené režimu</span><span class="sxs-lookup"><span data-stu-id="2e978-125">Publishing and starting push-mode partial configurations</span></span>

<span data-ttu-id="2e978-126">Potom zavolejte [publikovat DSCConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) pro každou konfiguraci předávání složky, které obsahují dokumenty konfigurace jako **cesta** parametry.</span><span class="sxs-lookup"><span data-stu-id="2e978-126">You then call [Publish-DSCConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) for each configuration, passing the folders that contain the configuration documents as the **Path** parameters.</span></span> <span data-ttu-id="2e978-127">`Publish-DSCConfiguration`umístí konfigurační soubory MOF a cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="2e978-127">`Publish-DSCConfiguration`places the configuration MOF files to the target nodes.</span></span> <span data-ttu-id="2e978-128">Po publikování obě konfigurace, můžete volat `Start-DSCConfiguration –UseExisting` na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="2e978-128">After publishing both configurations, you can call `Start-DSCConfiguration –UseExisting` on the target node.</span></span>

<span data-ttu-id="2e978-129">Například, pokud jste sestavili v následujících dokumentech MOF konfigurace na uzlu pro vytváření obsahu:</span><span class="sxs-lookup"><span data-stu-id="2e978-129">For example, if you have compiled the following configuration MOF documents on the authoring node:</span></span>

```powershell
PS C:\PartialConfigTest> Get-ChildItem -Recurse


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

<span data-ttu-id="2e978-130">By publikování a spusťte konfigurace následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2e978-130">You would publish and run the configurations as follows:</span></span>

```powershell
PS C:\PartialConfigTest> Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Start-DscConfiguration -UseExisting -ComputerName 'TestVM'

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command                  
--     ----            -------------   -----         -----------     --------             -------                  
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

><span data-ttu-id="2e978-131">**Poznámka:** uživatel, který spouští [publikovat DSCConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) rutinu musí mít oprávnění správce na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="2e978-131">**Note:** The user running the [Publish-DSCConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) cmdlet must have administrator privileges on the target node.</span></span>

## <a name="partial-configurations-in-pull-mode"></a><span data-ttu-id="2e978-132">Částečné konfigurace v režimu pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="2e978-132">Partial configurations in pull mode</span></span>

<span data-ttu-id="2e978-133">Je mohly vyžádat částečné konfigurací z jednoho nebo více serverů pro vyžádání obsahu (Další informace o přijetí změn serverech najdete v tématu [Windows PowerShell požadovaného stavu konfigurace vyžadování servery](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="2e978-133">Partial configurations can be pulled from one or more pull servers (for more information about pull servers, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="2e978-134">K tomuto účelu, budete muset nakonfigurovat LCM na cílovém uzlu částečné konfigurace pro vyžádání obsahu a název a najít dokumenty konfigurace správně na serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="2e978-134">To do this, you have to configure the LCM on the target node to pull the partial configurations, and name and locate the configuration documents properly on the pull servers.</span></span>

### <a name="configuring-the-lcm-for-pull-node-configurations"></a><span data-ttu-id="2e978-135">Konfigurace LCM pro vyžádání obsahu konfigurace uzlu</span><span class="sxs-lookup"><span data-stu-id="2e978-135">Configuring the LCM for pull node configurations</span></span>

<span data-ttu-id="2e978-136">Ke konfiguraci LCM vyžádání částečné konfigurace z načítacího serveru, definujete načítacího serveru buď **ConfigurationRepositoryWeb** (pro vyžádání obsahu server HTTP) nebo **ConfigurationRepositoryShare** () pro vyžádání obsahu server protokolu SMB) bloku.</span><span class="sxs-lookup"><span data-stu-id="2e978-136">To configure the LCM to pull partial configurations from a pull server, you define the pull server in either a **ConfigurationRepositoryWeb** (for an HTTP pull server) or **ConfigurationRepositoryShare** (for an SMB pull server) block.</span></span> <span data-ttu-id="2e978-137">Potom můžete vytvářet **PartialConfiguration** bloky, které odkazují na vyžádání obsahu server pomocí **ConfigurationSource** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="2e978-137">You then create **PartialConfiguration** blocks that refer to the pull server by using the **ConfigurationSource** property.</span></span> <span data-ttu-id="2e978-138">Je také nutné vytvořit **nastavení** blok, můžete určit, že LCM používá režim vyžádání obsahu a zadejte **ConfigurationNames** nebo **ConfigurationID** , načítacího serveru a Cílový uzel použijte k identifikaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2e978-138">You also need to create a **Settings** block to specify that the LCM uses pull mode, and to specify the **ConfigurationNames** or **ConfigurationID** that the pull server and target node use to identify the configurations.</span></span> <span data-ttu-id="2e978-139">Definuje následující meta konfigurace serveru pro vyžádání obsahu HTTP s názvem CONTOSO-PullSrv a dvě částečné konfigurace, které používají, které server vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="2e978-139">The following meta-configuration defines an HTTP pull server named CONTOSO-PullSrv and two partial configurations that use that pull server.</span></span>

<span data-ttu-id="2e978-140">Další informace o konfiguraci pomocí LCM **ConfigurationNames**, najdete v části [nastavení vyžadování klienta pomocí názvy konfigurace](pullClientConfigNames.md).</span><span class="sxs-lookup"><span data-stu-id="2e978-140">For more information about configuring the LCM using **ConfigurationNames**, see [Setting up a pull client using configuration names](pullClientConfigNames.md).</span></span> <span data-ttu-id="2e978-141">Informace o konfiguraci pomocí LCM **ConfigurationID**, najdete v části [nastavení vyžadování klienta pomocí ID konfigurace](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="2e978-141">For information about configuring the LCM using **ConfigurationID**, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a><span data-ttu-id="2e978-142">Konfigurace LCM pro vyžádání obsahu režimu konfigurace pomocí názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="2e978-142">Configuring the LCM for pull mode configurations using configuration names</span></span>

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

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a><span data-ttu-id="2e978-143">Konfigurace LCM pro vyžádání obsahu režimu konfigurace pomocí ConfigurationID</span><span class="sxs-lookup"><span data-stu-id="2e978-143">Configuring the LCM for pull mode configurations using ConfigurationID</span></span>

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

<span data-ttu-id="2e978-144">Částečné konfigurace z více než jeden server pro vyžádání obsahu můžete načítat – potřebovali byste právě definovat každý server pro vyžádání obsahu, a potom se podívejte na příslušné vyžádání obsahu server v každé **PartialConfiguration** bloku.</span><span class="sxs-lookup"><span data-stu-id="2e978-144">You can pull partial configurations from more than one pull server—you would just need to define each pull server, and then refer to the appropriate pull server in each **PartialConfiguration** block.</span></span>

<span data-ttu-id="2e978-145">Po vytvoření meta konfigurace, je nutné jej vytvořit dokument konfigurace (soubor MOF) a pak zavolají spustit [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621(v=wps.630).aspx) nakonfigurovat LCM.</span><span class="sxs-lookup"><span data-stu-id="2e978-145">After creating the meta-configuration, you must run it to create a configuration document (a MOF file), and then call [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621(v=wps.630).aspx) to configure the LCM.</span></span>

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a><span data-ttu-id="2e978-146">Názvy a umístění konfigurace dokumenty na serveru vyžádané replikace (ConfigurationNames)</span><span class="sxs-lookup"><span data-stu-id="2e978-146">Naming and placing the configuration documents on the pull server (ConfigurationNames)</span></span>

<span data-ttu-id="2e978-147">Dokumentů částečné konfigurace musí být umístěny ve složce zadané jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="2e978-147">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span> 

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a><span data-ttu-id="2e978-148">Pojmenování konfigurace dokumentů na serveru vyžádané replikace v prostředí PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="2e978-148">Naming configuration documents on the pull server in PowerShell 5.1</span></span>

<span data-ttu-id="2e978-149">Pokud jsou stahování částečné konfiguraci pouze jednoho z jednotlivých vyžádání obsahu serveru, konfigurace dokument může mít libovolný název.</span><span class="sxs-lookup"><span data-stu-id="2e978-149">If you are pulling only one partial configuration from an individual pull server, the configuration document can have any name.</span></span> <span data-ttu-id="2e978-150">Pokud jsou stahování více než jeden částečné konfigurace z načítacího serveru, konfigurace dokument může mít název buď `<ConfigurationName>.mof`, kde _ConfigurationName_ je název částečné konfigurace nebo `<ConfigurationName>.<NodeName>.mof`, kde  _ConfigurationName_ je název částečné konfigurace a _NodeName_ je název cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="2e978-150">If you are pulling more than one partial configuration from a pull server, the configuration document can be named either `<ConfigurationName>.mof`, where _ConfigurationName_ is the name of the partial configuration, or `<ConfigurationName>.<NodeName>.mof`, where  _ConfigurationName_ is the name of the partial configuration, and _NodeName_ is the name of the target node.</span></span> <span data-ttu-id="2e978-151">To vám umožní pro vyžádání obsahu konfigurace z načítacího serveru Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="2e978-151">This allows you to pull configurations from Azure Automation DSC pull server.</span></span>


#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a><span data-ttu-id="2e978-152">Pojmenování konfigurace dokumentů na serveru vyžádané replikace v prostředí PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="2e978-152">Naming configuration documents on the pull server in PowerShell 5.0</span></span>

<span data-ttu-id="2e978-153">Konfigurace dokumenty musí mít název následujícím způsobem: `ConfigurationName.mof`, kde _ConfigurationName_ je název částečné konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2e978-153">The configuration documents must be named as follows: `ConfigurationName.mof`, where _ConfigurationName_ is the name of the partial configuration.</span></span> <span data-ttu-id="2e978-154">Pro náš příklad konfigurace dokumenty nazván následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2e978-154">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a><span data-ttu-id="2e978-155">Názvy a umístění konfigurace dokumenty na serveru vyžádané replikace (ConfigurationID)</span><span class="sxs-lookup"><span data-stu-id="2e978-155">Naming and placing the configuration documents on the pull server (ConfigurationID)</span></span>

<span data-ttu-id="2e978-156">Dokumentů částečné konfigurace musí být umístěny ve složce zadané jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span><span class="sxs-lookup"><span data-stu-id="2e978-156">The partial configuration documents must be placed in the folder specified as the **ConfigurationPath** in the `web.config` file for the pull server (typically `C:\Program Files\WindowsPowerShell\DscService\Configuration`).</span></span> <span data-ttu-id="2e978-157">Konfigurace dokumenty musí mít název následujícím způsobem: _ConfigurationName_.</span><span class="sxs-lookup"><span data-stu-id="2e978-157">The configuration documents must be named as follows: _ConfigurationName_.</span></span> <span data-ttu-id="2e978-158">_ConfigurationID_`.mof`, kde _ConfigurationName_ je název částečné konfigurace a _ConfigurationID_ ID konfigurace musí být definován v LCM Cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="2e978-158">_ConfigurationID_`.mof`, where _ConfigurationName_ is the name of the partial configuration and _ConfigurationID_ is the configuration ID defined in the LCM on the target node.</span></span> <span data-ttu-id="2e978-159">Pro náš příklad konfigurace dokumenty nazván následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="2e978-159">For our example, the configuration documents should be named as follows:</span></span>

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```


### <a name="running-partial-configurations-from-a-pull-server"></a><span data-ttu-id="2e978-160">Spuštění částečné konfigurace z načítacího serveru</span><span class="sxs-lookup"><span data-stu-id="2e978-160">Running partial configurations from a pull server</span></span>

<span data-ttu-id="2e978-161">Po LCM na cílový uzel byl nakonfigurován a dokumenty konfigurace byly vytvořeny a správně s názvem na tomto serveru, cílový uzel částečné konfigurace pro vyžádání obsahu, je kombinovat a použít Výsledná konfigurace podle běžného intervaly podle specifikace **RefreshFrequencyMins** vlastnost LCM.</span><span class="sxs-lookup"><span data-stu-id="2e978-161">After the LCM on the target node has been configured, and the configuration documents have been created and properly named on the pull server, the target node will pull the partial configurations, combine them, and apply the resulting configuration at regular intervals as specified by the **RefreshFrequencyMins** property of the LCM.</span></span> <span data-ttu-id="2e978-162">Pokud chcete vynutit aktualizaci, můžete zavolat [aktualizace DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx) rutiny načítat konfigurace a potom `Start-DSCConfiguration –UseExisting` jejich použití.</span><span class="sxs-lookup"><span data-stu-id="2e978-162">If you want to force a refresh, you can call the [Update-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx) cmdlet, to pull the configurations, and then `Start-DSCConfiguration –UseExisting` to apply them.</span></span>


## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a><span data-ttu-id="2e978-163">Částečné konfigurace ve smíšeném režimech nabízení a vyžadování</span><span class="sxs-lookup"><span data-stu-id="2e978-163">Partial configurations in mixed push and pull modes</span></span>

<span data-ttu-id="2e978-164">Můžete také kombinovat nabízené a režimy pro částečné konfigurace pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="2e978-164">You can also mix push and pull modes for partial configurations.</span></span> <span data-ttu-id="2e978-165">To znamená můžete mít jeden částečné konfigurace, které pocházejí z načítacího serveru, zatímco jiné částečné konfigurace se instaluje.</span><span class="sxs-lookup"><span data-stu-id="2e978-165">That is, you could have one partial configuration that is pulled from a pull server, while another partial configuration is pushed.</span></span> <span data-ttu-id="2e978-166">Zadejte režim aktualizace pro každý částečné konfigurace, jak je popsáno v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="2e978-166">Specify the refresh mode for each partial configuration as described in the previous sections.</span></span> <span data-ttu-id="2e978-167">Například následující meta konfigurace popisuje tomto příkladě se `ServiceAccountConfig` částečné konfigurace v režimu pro vyžádání obsahu a `SharePointConfig` částečné konfigurace v režimu nabízení.</span><span class="sxs-lookup"><span data-stu-id="2e978-167">For example, the following meta-configuration describes the same example, with the `ServiceAccountConfig` partial configuration in pull mode and the `SharePointConfig` partial configuration in push mode.</span></span>

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a><span data-ttu-id="2e978-168">Smíšená režimech nabízení a vyžadování pomocí ConfigurationNames</span><span class="sxs-lookup"><span data-stu-id="2e978-168">Mixed push and pull modes using ConfigurationNames</span></span>

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

### <a name="mixed-push-and-pull-modes-using-configurationid"></a><span data-ttu-id="2e978-169">Smíšená režimech nabízení a vyžadování pomocí ConfigurationID</span><span class="sxs-lookup"><span data-stu-id="2e978-169">Mixed push and pull modes using ConfigurationID</span></span>

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

<span data-ttu-id="2e978-170">Všimněte si, že **RefreshMode** zadaný v bloku nastavení je "Pro vyžádání obsahu", ale **RefreshMode** pro `SharePointConfig` částečné konfigurace je "Push".</span><span class="sxs-lookup"><span data-stu-id="2e978-170">Note that the **RefreshMode** specified in the Settings block is "Pull", but the **RefreshMode** for the `SharePointConfig` partial configuration is "Push".</span></span>

<span data-ttu-id="2e978-171">Název a vyhledejte konfigurační soubory MOF, jak je popsáno výše pro režimy jejich příslušné aktualizace.</span><span class="sxs-lookup"><span data-stu-id="2e978-171">Name and locate the configuration MOF files as described above for their respective refresh modes.</span></span> <span data-ttu-id="2e978-172">Volání **publikovat DSCConfiguration** publikovat `SharePointConfig` částečné konfigurace a buď počkejte `ServiceAccountConfig` konfigurace být vyžádány z načítacího serveru nebo vynutit aktualizaci voláním [ Aktualizace DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541(v=wps.630).aspx).</span><span class="sxs-lookup"><span data-stu-id="2e978-172">Call **Publish-DSCConfiguration** to publish the `SharePointConfig` partial configuration, and either wait for the `ServiceAccountConfig` configuration to be pulled from the pull server, or force a refresh by calling [Update-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541(v=wps.630).aspx).</span></span>

## <a name="example-serviceaccountconfig-partial-configuration"></a><span data-ttu-id="2e978-173">Příklad ServiceAccountConfig Partial konfigurace</span><span class="sxs-lookup"><span data-stu-id="2e978-173">Example ServiceAccountConfig Partial Configuration</span></span>

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
## <a name="example-sharepointconfig-partial-configuration"></a><span data-ttu-id="2e978-174">Příklad SharePointConfig Partial konfigurace</span><span class="sxs-lookup"><span data-stu-id="2e978-174">Example SharePointConfig Partial Configuration</span></span>
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
##<a name="see-also"></a><span data-ttu-id="2e978-175">Viz také</span><span class="sxs-lookup"><span data-stu-id="2e978-175">See Also</span></span> 

<span data-ttu-id="2e978-176">**Koncepty**
[požadovaného stavu konfigurační servery z vlastního prostředí Windows PowerShell](pullServer.md)</span><span class="sxs-lookup"><span data-stu-id="2e978-176">**Concepts**
[Windows PowerShell Desired State Configuration Pull Servers](pullServer.md)</span></span> 

[<span data-ttu-id="2e978-177">Konfigurace správce místní konfigurace systému Windows</span><span class="sxs-lookup"><span data-stu-id="2e978-177">Windows Configuring the Local Configuration Manager</span></span>](https://technet.microsoft.com/en-us/library/mt421188.aspx) 


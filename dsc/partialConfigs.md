---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Konfigurace požadovaného stavu prostředí PowerShell částečné konfigurace"
ms.openlocfilehash: 2c5f29ee2940f4b7955219e97275ffa2695f9dee
ms.sourcegitcommit: aa6890031dad3f2981b24c58893d134bdf4e8655
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/08/2017
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a>Konfigurace požadovaného stavu prostředí PowerShell částečné konfigurace

>Platí pro: Prostředí Windows PowerShell 5.0 a novější.

Konfigurace požadovaného stavu (DSC) v prostředí PowerShell 5.0 umožňuje konfigurace, který bude doručen v fragmenty a z více zdrojů. Místní Configuration Manager (LCM) na cílovém uzlu fragmenty umístí společně před jejich použití jako jedna konfigurační. Tato možnost umožňuje sdílení kontrolu nad konfiguraci mezi týmy nebo jednotlivce. Například pokud dva nebo více týmy vývojářů spolupracují na službě, může každý chtějí vytvořit konfigurace ke správě jejich součástí služby. Každý z těchto konfigurací může vyžádat ze serverů různých vyžádání obsahu a nebylo možné přidat v různých fázích vývoje. Různí jednotlivci nebo týmy ovládat různé aspekty konfigurace uzlů bez nutnosti ke koordinaci úpravy dokumentu jedna konfigurační také umožňuje částečné konfigurace. Například může být jeden tým odpovědný pro nasazení virtuálního počítače a operačního systému, může jiného týmu nasazení dalších aplikací a služeb na tento virtuální počítač. S konfigurací částečné každý tým můžete vytvořit vlastní konfiguraci, bez buď z nich se zbytečně komplikovanější.

Můžete použít částečný konfigurace v režimu push, pull režimu nebo kombinaci těchto dvou.

## <a name="partial-configurations-in-push-mode"></a>Částečné konfigurace v režimu nabízení
V režimu nabízená použít částečný konfigurace, nakonfigurujte LCM na cílový uzel pro příjem částečné konfigurace. Každá částečné konfigurace musí nabídnutých k cíli pomocí rutiny DSCConfiguration publikovat. Cílový uzel pak kombinuje částečné konfigurace do jedné konfigurace a konfigurace můžete použít při volání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny.

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a>Konfigurace LCM pro částečné konfigurace nabízené režimu
Ke konfiguraci LCM pro částečné konfigurace v nabízené režimu, vytvoříte **DSCLocalConfigurationManager** konfigurace s jedním **PartialConfiguration** blok pro každé částečné konfiguraci. Další informace o konfiguraci LCM najdete v tématu [Windows konfigurace správce místní konfigurace](https://technet.microsoft.com/en-us/library/mt421188.aspx). Následující příklad ukazuje konfigurace aplikace LCM, která očekává dvě konfigurace částečné – jednu, která nasazuje operační systém a ten, který nasadí a nakonfiguruje služby SharePoint.

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

**RefreshMode** pro každý částečné konfigurace je nastavena na "Push". Názvy **PartialConfiguration** bloky (v tomto případě "ServiceAccountConfig" a "SharePointConfig") musí odpovídat přesně názvy konfigurace, které odesílají na cílovém uzlu.

>**Poznámka:** pojmenované jednotlivých **PartialConfiguration** bloku musí odpovídat skutečný název konfigurace, jako jsou zadány v konfigurační skript, nikoli název souboru MOF, který musí být buď název Cílový uzel nebo `localhost`.

### <a name="publishing-and-starting-push-mode-partial-configurations"></a>Publikování a počáteční konfigurace částečné nabízené režimu

Potom zavolejte [publikovat DSCConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) pro každou konfiguraci předávání složky, které obsahují dokumenty konfigurace jako **cesta** parametry. `Publish-DSCConfiguration`umístí konfigurační soubory MOF a cílové uzly. Po publikování obě konfigurace, můžete volat `Start-DSCConfiguration –UseExisting` na cílovém uzlu.

Například, pokud jste sestavili v následujících dokumentech MOF konfigurace na uzlu pro vytváření obsahu:

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

By publikování a spusťte konfigurace následujícím způsobem:

```powershell
PS C:\PartialConfigTest> Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Start-DscConfiguration -UseExisting -ComputerName 'TestVM'

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command                  
--     ----            -------------   -----         -----------     --------             -------                  
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

>**Poznámka:** uživatel, který spouští [publikovat DSCConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) rutinu musí mít oprávnění správce na cílovém uzlu.

## <a name="partial-configurations-in-pull-mode"></a>Částečné konfigurace v režimu pro vyžádání obsahu

Je mohly vyžádat částečné konfigurací z jednoho nebo více serverů pro vyžádání obsahu (Další informace o přijetí změn serverech najdete v tématu [Windows PowerShell požadovaného stavu konfigurace vyžadování servery](pullServer.md). K tomuto účelu, budete muset nakonfigurovat LCM na cílovém uzlu částečné konfigurace pro vyžádání obsahu a název a najít dokumenty konfigurace správně na serveru vyžádané replikace.

### <a name="configuring-the-lcm-for-pull-node-configurations"></a>Konfigurace LCM pro vyžádání obsahu konfigurace uzlu

Ke konfiguraci LCM vyžádání částečné konfigurace z načítacího serveru, definujete načítacího serveru buď **ConfigurationRepositoryWeb** (pro vyžádání obsahu server HTTP) nebo **ConfigurationRepositoryShare** () pro vyžádání obsahu server protokolu SMB) bloku. Potom můžete vytvářet **PartialConfiguration** bloky, které odkazují na vyžádání obsahu server pomocí **ConfigurationSource** vlastnost. Je také nutné vytvořit **nastavení** blok, můžete určit, že LCM používá režim vyžádání obsahu a zadejte **ConfigurationNames** nebo **ConfigurationID** , načítacího serveru a Cílový uzel použijte k identifikaci konfigurace. Definuje následující meta konfigurace serveru pro vyžádání obsahu HTTP s názvem CONTOSO-PullSrv a dvě částečné konfigurace, které používají, které server vyžádané replikace.

Další informace o konfiguraci pomocí LCM **ConfigurationNames**, najdete v části [nastavení vyžadování klienta pomocí názvy konfigurace](pullClientConfigNames.md). Informace o konfiguraci pomocí LCM **ConfigurationID**, najdete v části [nastavení vyžadování klienta pomocí ID konfigurace](pullClientConfigID.md).

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a>Konfigurace LCM pro vyžádání obsahu režimu konfigurace pomocí názvy konfigurace

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

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a>Konfigurace LCM pro vyžádání obsahu režimu konfigurace pomocí ConfigurationID

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

Částečné konfigurace z více než jeden server pro vyžádání obsahu můžete načítat – potřebovali byste právě definovat každý server pro vyžádání obsahu, a potom se podívejte na příslušné vyžádání obsahu server v každé **PartialConfiguration** bloku.

Po vytvoření meta konfigurace, je nutné jej vytvořit dokument konfigurace (soubor MOF) a pak zavolají spustit [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621(v=wps.630).aspx) nakonfigurovat LCM.

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a>Názvy a umístění konfigurace dokumenty na serveru vyžádané replikace (ConfigurationNames)

Dokumentů částečné konfigurace musí být umístěny ve složce zadané jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program Files\WindowsPowerShell\DscService\Configuration`). 

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a>Pojmenování konfigurace dokumentů na serveru vyžádané replikace v prostředí PowerShell 5.1

Pokud jsou stahování částečné konfiguraci pouze jednoho z jednotlivých vyžádání obsahu serveru, konfigurace dokument může mít libovolný název. Pokud jsou stahování více než jeden částečné konfigurace z načítacího serveru, konfigurace dokument může mít název buď `<ConfigurationName>.mof`, kde _ConfigurationName_ je název částečné konfigurace nebo `<ConfigurationName>.<NodeName>.mof`, kde  _ConfigurationName_ je název částečné konfigurace a _NodeName_ je název cílový uzel. To vám umožní pro vyžádání obsahu konfigurace z načítacího serveru Azure Automation DSC.


#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a>Pojmenování konfigurace dokumentů na serveru vyžádané replikace v prostředí PowerShell 5.0

Konfigurace dokumenty musí mít název následujícím způsobem: `ConfigurationName.mof`, kde _ConfigurationName_ je název částečné konfigurace. Pro náš příklad konfigurace dokumenty nazván následujícím způsobem:

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a>Názvy a umístění konfigurace dokumenty na serveru vyžádané replikace (ConfigurationID)

Dokumentů částečné konfigurace musí být umístěny ve složce zadané jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program Files\WindowsPowerShell\DscService\Configuration`). Konfigurace dokumenty musí mít název následujícím způsobem: _ConfigurationName_. _ConfigurationID_`.mof`, kde _ConfigurationName_ je název částečné konfigurace a _ConfigurationID_ ID konfigurace musí být definován v LCM Cílový uzel. Pro náš příklad konfigurace dokumenty nazván následujícím způsobem:

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```


### <a name="running-partial-configurations-from-a-pull-server"></a>Spuštění částečné konfigurace z načítacího serveru

Po LCM na cílový uzel byl nakonfigurován a dokumenty konfigurace byly vytvořeny a správně s názvem na tomto serveru, cílový uzel částečné konfigurace pro vyžádání obsahu, je kombinovat a použít Výsledná konfigurace podle běžného intervaly podle specifikace **RefreshFrequencyMins** vlastnost LCM. Pokud chcete vynutit aktualizaci, můžete zavolat [aktualizace DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx) rutiny načítat konfigurace a potom `Start-DSCConfiguration –UseExisting` jejich použití.


## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a>Částečné konfigurace ve smíšeném režimech nabízení a vyžadování

Můžete také kombinovat nabízené a režimy pro částečné konfigurace pro vyžádání obsahu. To znamená můžete mít jeden částečné konfigurace, které pocházejí z načítacího serveru, zatímco jiné částečné konfigurace se instaluje. Zadejte režim aktualizace pro každý částečné konfigurace, jak je popsáno v předchozí části. Například následující meta konfigurace popisuje tomto příkladě se `ServiceAccountConfig` částečné konfigurace v režimu pro vyžádání obsahu a `SharePointConfig` částečné konfigurace v režimu nabízení.

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a>Smíšená režimech nabízení a vyžadování pomocí ConfigurationNames

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

### <a name="mixed-push-and-pull-modes-using-configurationid"></a>Smíšená režimech nabízení a vyžadování pomocí ConfigurationID

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

Všimněte si, že **RefreshMode** zadaný v bloku nastavení je "Pro vyžádání obsahu", ale **RefreshMode** pro `SharePointConfig` částečné konfigurace je "Push".

Název a vyhledejte konfigurační soubory MOF, jak je popsáno výše pro režimy jejich příslušné aktualizace. Volání **publikovat DSCConfiguration** publikovat `SharePointConfig` částečné konfigurace a buď počkejte `ServiceAccountConfig` konfigurace být vyžádány z načítacího serveru nebo vynutit aktualizaci voláním [ Aktualizace DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541(v=wps.630).aspx).

## <a name="example-serviceaccountconfig-partial-configuration"></a>Příklad ServiceAccountConfig Partial konfigurace

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
## <a name="example-sharepointconfig-partial-configuration"></a>Příklad SharePointConfig Partial konfigurace
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
##<a name="see-also"></a>Viz také 

**Koncepty**
[požadovaného stavu konfigurační servery z vlastního prostředí Windows PowerShell](pullServer.md) 

[Konfigurace správce místní konfigurace systému Windows](https://technet.microsoft.com/en-us/library/mt421188.aspx) 


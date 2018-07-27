---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Částečné konfigurace prostředí PowerShell Desired State Configuration
ms.openlocfilehash: 1b9ff8534f4c11d6859587830a04075be55a7d54
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268377"
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a>Částečné konfigurace prostředí PowerShell Desired State Configuration

_Platí pro: Windows PowerShell 5.0 nebo novější._

Desired State Configuration (DSC) v Powershellu 5.0 umožňuje konfigurace, které se dodávají v fragmentů a z více zdrojů. Tyto fragmenty místní Configuration Manageru (LCM) na cílovém uzlu společně vloží před jejich použitím jako jediné konfiguraci. Tato možnost umožňuje kontrolu nad konfigurací mezi týmy nebo jednotlivce, pro sdílení obsahu. Například pokud dva nebo více týmů vývojářů spolupracují na službě, může každý chtějí vytvořit konfigurace pro správu jejich součástí služby. Každá z těchto konfigurací může získaných z různých o přijetí změn servery a může být přidán v různých fázích vývoje. Částečné konfigurace také povolit různí jednotlivci nebo týmy ovládat různé aspekty konfigurace uzlů bez nutnosti ke koordinaci úpravy dokumentu jediné konfiguraci. Například může být jeden tým odpovědného za nasazení virtuálního počítače a operačního systému, zatímco jiný tým může nasadit další aplikace a služby na tomto virtuálním počítači. Konfigurací částečného každý tým může vytvořit své vlastní konfigurace bez některou z nich se zbytečně složité.

Můžete použít částečné konfigurace v režimu nabízení, režimu o přijetí změn nebo kombinaci obojího.

## <a name="partial-configurations-in-push-mode"></a>Částečné konfigurace v režimu nabízení

Částečné konfigurace v režimu nabízení, můžete nakonfigurovat LCM na cílovém uzlu přijímat částečné konfigurace. Každá částečné konfigurace musí doručit bez vyžádání do cíle pomocí `Publish-DSCConfiguration` rutiny. Cílový uzel pak kombinuje částečné konfigurace do jediné konfiguraci a můžete provést konfiguraci pomocí volání [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny.

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a>Konfigurace LCM pro režimu nabízení částečné konfigurace

Konfigurace LCM pro částečné konfigurace v režimu nabízení, vytvoříte **DSCLocalConfigurationManager** konfiguraci s jednou **PartialConfiguration** blok pro každou částečné konfiguraci. Další informace týkající se konfigurace LCM v tématu [Windows konfigurace Local Configuration Manageru](/powershell/dsc/metaConfig). Následující příklad ukazuje LCM konfigurace, který očekává, že dvě částečné konfigurace – ten, který se nasadí operační systém a jednu, která nasazuje a konfiguruje službu SharePoint.

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

**RefreshMode** pro každou konfiguraci částečné je nastaven na hodnotu "Push". Názvy **PartialConfiguration** bloky (v tomto případě "ServiceAccountConfig" a "SharePointConfig") musí odpovídat přesně názvy konfigurace, které se odesílají na cílový uzel.

> [!Note]
> Pojmenované jednotlivých **PartialConfiguration** bloku musí odpovídat skutečný název konfigurace, protože je zadán v konfigurační skript, nikoli název souboru MOF, který by měl být název cílový uzel nebo `localhost`.

### <a name="publishing-and-starting-push-mode-partial-configurations"></a>Publikování a spuštění režimu nabízení částečné konfigurace

Poté je zapotřebí zavolat [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) pro každou konfiguraci předávání složky, která obsahují dokumenty konfigurace jako **cesta** parametry. `Publish-DSCConfiguration`umístí konfigurační soubory MOF a cílové uzly. Po publikování obě konfigurace, můžete volat `Start-DSCConfiguration –UseExisting` na cílovém uzlu.

Například, pokud jste zkompilovali následující dokumenty MOF konfigurace uzlu pro vytváření obsahu:

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

By publikovat a spustit konfiguraci následujícím způsobem:

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
> Uživatel, který spustil [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) rutina musí mít oprávnění správce na cílovém uzlu.

## <a name="partial-configurations-in-pull-mode"></a>Částečné konfigurace v režimu o přijetí změn

Částečné konfigurace můžete načíst z jednoho nebo více serverů o přijetí změn (Další informace o serverech o přijetí změn najdete v tématu [Windows PowerShell Desired State Configuration o přijetí změn servery](pullServer.md). Chcete-li to provést, musíte nakonfigurovat LCM na cílový uzel k vyžádání částečné konfigurace a název a vyhledejte dokumenty konfigurace správně na serverech o přijetí změn.

### <a name="configuring-the-lcm-for-pull-node-configurations"></a>Konfigurace LCM pro o přijetí změn konfigurace uzlu

Konfigurace LCM přetahování částečné konfigurace ze serveru vyžádané replikace, definujete v jednom serveru vyžádané replikace **ConfigurationRepositoryWeb** (pro vyžádání obsahu server HTTP) nebo **ConfigurationRepositoryShare** () pro serveru vyžádané replikace SMB) bloku. Pak vytvoříte **PartialConfiguration** bloky, které odkazují na serveru vyžádané replikace s použitím **ConfigurationSource** vlastnost. Je také potřeba vytvořit **nastavení** bloku k určení, že LCM používá režim o přijetí změn a k určení **ConfigurationNames** nebo **ConfigurationID** , který serveru vyžádané replikace a Cílový uzel použijte k identifikaci konfigurace. Definuje následující meta konfigurace serveru HTTP o přijetí změn s názvem CONTOSO-PullSrv a dvě částečné konfigurace, které používají, které server vyžádané replikace.

Další informace o konfiguraci pomocí LCM **ConfigurationNames**, naleznete v tématu [nastavení načítacího klienta použití konfiguračních názvů](pullClientConfigNames.md). Informace o konfiguraci pomocí LCM **ConfigurationID**, naleznete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů](pullClientConfigID.md).

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a>Konfigurace LCM pro použití konfiguračních názvů konfigurace režimu o přijetí změn

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

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a>Konfigurace LCM pro vyžádání obsahu režim konfigurace pomocí ConfigurationID

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

Částečné konfigurace z více než jednom serveru o přijetí změn si můžete vyžádat – stačí je třeba definovat každého serveru vyžádané replikace, a přečtěte si informace na server příslušné o přijetí změn v každém **PartialConfiguration** bloku.

Po vytvoření meta konfigurace, musíte spustit vytvořit dokument konfigurace (soubor MOF), a poté zavolejte [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) konfigurace LCM.

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a>Názvy a umístění konfigurace dokumentů na serveru vyžádané replikace (ConfigurationNames)

Částečné konfigurace dokumenty musí být umístěné ve složce určené jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program
Files\WindowsPowerShell\DscService\Configuration`).

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a>Pojmenování konfigurace dokumentů na serveru vyžádané replikace v prostředí PowerShell 5.1

Pokud se souhrnné informace pouze jedna částečná konfigurace z jednotlivých načítacího serveru, dokument konfigurace může mít libovolný název. Pokud se stahování více než jedna částečná konfigurace ze serveru vyžádané replikace, dokument konfigurace může mít název buď `<ConfigurationName>.mof`, kde *ConfigurationName* je název částečné konfigurace nebo `<ConfigurationName>.<NodeName>.mof`, kde *ConfigurationName* je název částečné konfigurace a *NodeName* je název cílový uzel. To vám umožní o přijetí změn konfigurace z načítacího serveru Azure Automation DSC.

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a>Pojmenování konfigurace dokumentů na serveru vyžádané replikace v Powershellu 5.0

Konfigurace dokumenty musí mít název takto: `ConfigurationName.mof`, kde *ConfigurationName* je název částečné konfigurace. V našem příkladu by měl být pojmenován dokumenty konfigurace následujícím způsobem:

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a>Názvy a umístění konfigurace dokumentů na serveru vyžádané replikace (ConfigurationID)

Částečné konfigurace dokumenty musí být umístěné ve složce určené jako **ConfigurationPath** v `web.config` soubor pro vyžádání obsahu server (obvykle `C:\Program Files\WindowsPowerShell\DscService\Configuration`). Konfigurace dokumenty musí mít název takto: `<ConfigurationName>.<ConfigurationID>.mof`, kde _ConfigurationName_ je název částečné konfigurace a _ConfigurationID_ je konfigurace podle ID LCM na cílovém uzlu. V našem příkladu by měl být pojmenován dokumenty konfigurace následujícím způsobem:

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```

### <a name="running-partial-configurations-from-a-pull-server"></a>Částečné konfigurace spuštěných serveru vyžádané replikace

Po LCM na cílový uzel byl nakonfigurován a konfigurace dokumenty byly vytvořeny a správně s názvem na serveru vyžádané replikace cílový uzel přetáhne částečné konfigurace, je zkombinovat a použít výslednou konfiguraci podle běžného intervaly podle specifikace **RefreshFrequencyMins** vlastnost LCM. Pokud chcete vynutit aktualizaci, můžete volat [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) rutiny, o přijetí změn konfigurace a potom `Start-DSCConfiguration –UseExisting` jejich použití.

## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a>Částečné konfigurace ve smíšené režimech nabízení a vyžadování

Můžete také kombinovat push a pull režimy pro částečné konfigurace. To znamená může mít jednu konfiguraci částečné, které pocházejí ze serveru vyžádané replikace, zatímco je jinou konfiguraci částečné vloženo. Režim aktualizace pro každou konfiguraci částečné zadejte, jak je popsáno v předchozích částech. Například následující meta konfigurace popisuje stejný příklad s `ServiceAccountConfig` částečné konfigurace v režimu o přijetí změn a `SharePointConfig` částečné konfigurace v režimu nabízení.

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a>Smíšené režimech nabízení a vyžadování pomocí ConfigurationNames

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

### <a name="mixed-push-and-pull-modes-using-configurationid"></a>Smíšené režimech nabízení a vyžadování pomocí ConfigurationID

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

Všimněte si, že **RefreshMode** zadaný v bloku nastavení je "Pull", ale **RefreshMode** pro `SharePointConfig` částečné konfigurace je "Push".

Zadejte název a vyhledejte konfigurační soubory MOF, jak je popsáno výše pro režimy jejich příslušné aktualizace.
Volání `Publish-DSCConfiguration` publikovat `SharePointConfig` částečné konfigurace a buď počkejte `ServiceAccountConfig` konfigurace načíst ze serveru vyžádané replikace, nebo vynutit aktualizaci voláním [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).

## <a name="example-serviceaccountconfig-partial-configuration"></a>Příklad ServiceAccountConfig částečné konfigurace

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

## <a name="example-sharepointconfig-partial-configuration"></a>Příklad SharePointConfig částečné konfigurace

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

## <a name="see-also"></a>Viz také

[Prostředí Windows PowerShell Desired State Configuration servery o přijetí změn](pullServer.md)

[Konfigurace Local Configuration Manageru Windows](metaConfig.md)
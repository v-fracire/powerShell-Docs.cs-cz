---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Nastavení vyžadování klienta pomocí ID konfigurace"
ms.openlocfilehash: bb14bff95c626b65e2d0d0072c39e4c571cea4b0
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a>Nastavení vyžadování klienta pomocí ID konfigurace

> Platí pro: Prostředí Windows PowerShell 5.0

Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadána adresa URL, kde může kontaktovat načítací server za účelem získání konfigurace. K tomuto účelu, budete muset nakonfigurovat místní Configuration Manager (LCM) nezbytné informace. Pokud chcete nakonfigurovat LCM, vytvoříte speciální typ konfigurace, označených pomocí **DSCLocalConfigurationManager** atribut. Další informace o konfiguraci LCM najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md).

> **Poznámka:**: Toto téma se týká PowerShell 5.0. Informace o nastavení klienta přijetí změn v prostředí PowerShell 4.0 najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0](pullClientConfigID4.md)

Následující skript nakonfiguruje LCM přijetí změn konfigurace ze serveru s názvem "CONTOSO-PullSrv".

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }      
    }
}
PullClientConfigID
```

Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace. **ServerURL**

Po spuštění tohoto skriptu vytvoří nový výstupní složky s názvem **PullClientConfigID** a vloží soubor MOF metakonfiguraci existuje. V takovém případě bude mít název souboru MOF metakonfiguraci `localhost.meta.mof`.

Chcete-li použít konfiguraci, volejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavte na umístění souboru MOF metakonfiguraci. Příklad: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`

## <a name="configuration-id"></a>ID konfigurace

Nastaví skript **ConfigurationID** vlastnost LCM na identifikátor GUID, který byl dříve vytvořili pro tento účel (identifikátor GUID můžete vytvořit pomocí **nový Guid** rutiny). **ConfigurationID** je co LCM používá k nalezení odpovídající konfiguraci na tomto serveru. Konfigurační soubor MOF na tomto serveru musí mít název _ConfigurationID_MOF, kde _ConfigurationID_ je hodnota **ConfigurationID** vlastnost cíle LCM uzlu.

## <a name="smb-pull-server"></a>Vyžádání serveru SMB

Nastavení klienta pro vyžádání obsahu konfigurace ze serveru SMB, použijte **ConfigurationRepositoryShare** bloku. V **ConfigurationRepositoryShare** bloku, musíte zadat cestu k serveru nastavením **SourcePath** vlastnost. Následující metakonfiguraci nakonfiguruje cílový uzel načítat z serveru SMB vyžádání obsahu s názvem **SMBPullServer**.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryShare SMBPullServer
        {
            SourcePath = '\\SMBPullServer\PullSource'
            
        }     
    }
}
PullClientConfigID
```

## <a name="resource-and-report-servers"></a>Servery prostředků a sestavy

Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat ve vaší konfiguraci LCM (jako v předchozím příkladu), klient pro vyžádání obsahu načte prostředky z Zadaný server, ale nebude odesílat zprávy do něj. Jeden načítacího serveru můžete použít pro konfigurace, prostředky a vytváření sestav, ale je nutné vytvořit **ReportRepositoryWeb** blok k nastavení vytváření sestav. 

Následující příklad ukazuje metakonfiguraci, který nastaví kolekci klienta k přijetí změn konfigurace a prostředky a odesílat data, pro vytváření sestav k jedné z vlastního serveru.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
        
        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

Můžete také zadat servery různých vyžádání obsahu pro prostředky a vytváření sestav. K určení serveru prostředků, můžete buď použít **ResourceRepositoryWeb** (pro webový server pro vyžádání obsahu) nebo **ResourceRepositoryShare** blok (pro vyžádání obsahu serveru SMB).
Chcete-li zadat server sestav, je použít **ReportRepositoryWeb** bloku. Server sestav nemůže být serveru SMB.
Následující metakonfiguraci nakonfiguruje klienta vyžádání obsahu k získání jeho konfigurace z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**a k odeslání zprávy o stavu do  **CONTOSO-ReportSrv**:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30 
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            
        }
        
        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

## <a name="see-also"></a>Viz také

* [Nastavení klienta vyžádání obsahu s názvy konfigurace](pullClientConfigNames.md)


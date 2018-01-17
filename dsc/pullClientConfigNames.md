---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Nastavení vyžadování klienta pomocí názvy konfigurace"
ms.openlocfilehash: 11de53fc349ce0ebacf0d4855d82fa8a22d55c99
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a>Nastavení vyžadování klienta pomocí názvy konfigurace

> Platí pro: Prostředí Windows PowerShell 5.0

Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadána adresa URL, kde může kontaktovat načítací server za účelem získání konfigurace.
K tomuto účelu, budete muset nakonfigurovat místní Configuration Manager (LCM) nezbytné informace.
Pokud chcete nakonfigurovat LCM, vytvoříte speciální typ konfigurace, označených pomocí **DSCLocalConfigurationManager** atribut.
Další informace o konfiguraci LCM najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md).

> **Poznámka:**: Toto téma se týká PowerShell 5.0.
Informace o nastavení klienta přijetí změn v prostředí PowerShell 4.0 najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0](pullClientConfigID4.md)

Následující skript nakonfiguruje LCM pro vyžádání obsahu konfigurace ze serveru s názvem "CONTOSO-PullSrv":

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }
    }
}
PullClientConfigNames
```

Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace.
**ServerURL** vlastnost určuje koncový bod pro vyžádání obsahu serveru.

**RegistrationKey** vlastnost je sdílený klíč mezi všechny uzly klienta pro vyžádání obsahu server a tento server pro vyžádání obsahu.
Stejné hodnota je uložena v souboru na tomto serveru.

**ConfigurationNames** vlastnost je pole, které určuje názvy konfigurace určené pro klientský uzel.
Na tomto serveru, MOF konfigurační soubor pro tento uzel klienta musí mít název *ConfigurationNames*MOF, kde *ConfigurationNames* odpovídá hodnotě **ConfigurationNames**  sadu v této metakonfiguraci vlastností.

>**Poznámka:** Pokud zadáte více než jednu hodnotu v **ConfigurationNames**, musíte zadat také **PartialConfiguration** bloků v konfiguraci.
Informace o částečné konfiguracích najdete v tématu [konfigurace požadovaného stavu prostředí PowerShell částečné konfigurace](partialConfigs.md).

Po spuštění tohoto skriptu vytvoří nový výstupní složky s názvem **PullClientConfigNames** a vloží soubor MOF metakonfiguraci existuje.
V takovém případě bude mít název souboru MOF metakonfiguraci `localhost.meta.mof`.

Chcete-li použít konfiguraci, volejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavte na umístění souboru MOF metakonfiguraci.

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> **Poznámka:**: registrační kódy pracovat pouze s webovými servery vyžádání obsahu.
Je nutné použít **ConfigurationID** se serverem SMB vyžádání obsahu.
Informace o konfiguraci serveru vyžádané replikace pomocí **ConfigurationID**, najdete v části [nastavení vyžadování klienta pomocí ID konfigurace](PullClientConfigNames.md)

## <a name="resource-and-report-servers"></a>Servery prostředků a sestavy

Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat ve vaší konfiguraci LCM (jako v předchozím příkladu), klient pro vyžádání obsahu načte prostředky z Zadaný server, ale nebude odesílat zprávy do něj.
Jeden načítacího serveru můžete použít pro konfigurace, prostředky a vytváření sestav, ale je nutné vytvořit **ReportRepositoryWeb** blok k nastavení vytváření sestav.
Následující příklad ukazuje metakonfiguraci, který nastaví kolekci klienta k přijetí změn konfigurace a prostředky a odesílat data, pro vytváření sestav k jedné z vlastního serveru.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigNames
```

Můžete také zadat servery různých vyžádání obsahu pro prostředky a vytváření sestav.
K určení serveru prostředků, můžete buď použít **ResourceRepositoryWeb** (pro webový server pro vyžádání obsahu) nebo **ResourceRepositoryShare** blok (pro vyžádání obsahu serveru SMB).
Chcete-li zadat server sestav, je použít **ReportRepositoryWeb** bloku.
Server sestav nemůže být serveru SMB.
Následující metakonfiguraci nakonfiguruje klienta vyžádání obsahu k získání jeho konfigurace z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**a k odeslání zprávy o stavu do  **CONTOSO-ReportSrv**:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-ResourceSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '30ef9bd8-9acf-4e01-8374-4dc35710fc90'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-ReportSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '6b392c6a-818c-4b24-bf38-47124f1e2f14'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a>Viz také

* [Nastavení vyžadování klienta s ID konfigurace](PullClientConfigNames.md)
* [Nastavení webového serveru vyžádané replikace DSC](pullServer.md)


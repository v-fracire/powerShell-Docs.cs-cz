---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Nastavení klienta o přijetí změn se názvy konfigurací v Powershellu 5.0 a novější
ms.openlocfilehash: fd038a105da7a83ecad9b571e611b65c8ec847b3
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403844"
---
# <a name="set-up-a-pull-client-using-configuration-names-in-powershell-50-and-later"></a>Nastavení klienta o přijetí změn se názvy konfigurací v Powershellu 5.0 a novější

> Platí pro: Windows PowerShell 5.0

> [!IMPORTANT]
> Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce. Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).

Před nastavení načítacího klienta, byste měli nastavit serveru vyžádané replikace. I když toto pořadí není vyžadována, pomáhá při řešení potíží a vám pomůže zajistit, že registrace byla úspěšná. Nastavení serveru vyžádané replikace, můžete použít následující příručky:

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)

Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav. Následující části ukazují, jak nakonfigurovat klienta o přijetí změn s sdílenou složku protokolu SMB nebo protokolu HTTP serveru vyžádané replikace DSC. Při aktualizaci uzlu LCM se vás bude kontaktovat do nakonfigurovaného umístění ke stažení všechny přiřazené konfigurace. Pokud všechny požadované prostředky neexistuje na uzlu, se bude automaticky si je stáhnout z nakonfigurovaných umístění. Pokud uzel je nakonfigurované [serveru sestav](reportServer.md), potom oznámí stav operace.

> **Poznámka:**: Toto téma platí pro PowerShell 5.0.
Informace o nastavení načítacího klienta v Powershellu 4.0 najdete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů v Powershellu 4.0](pullClientConfigID4.md)

## <a name="configure-the-pull-client-lcm"></a>Konfigurace LCM klienta o přijetí změn

Provádění některý z níže uvedených příkladech vytvoří nový výstupní složka s názvem **PullClientConfigName** a umístí soubor MOF metaconfiguration existuje. V takovém případě bude mít název souboru MOF metaconfiguration `localhost.meta.mof`.

Chcete-li použít konfiguraci, zavolejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavit umístění souboru MOF metaconfiguration. Příklad:

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigName –Verbose.
```

## <a name="configuration-name"></a>Název konfigurace

V příkladech níže sad **ConfigurationName** vlastnost LCM název předtím zkompilovanou konfiguraci, vytvořený k tomuto účelu. **ConfigurationName** je co LCM používá k nalezení odpovídající konfigurace na serveru vyžádané replikace. Musí mít název konfiguračního souboru MOF na serveru vyžádané replikace `<ConfigurationName>.mof`, v tomto případě "ClientConfig.mof". Další informace najdete v tématu [publikovat konfigurace serveru vyžádaných replikací s (v4/v5)](publishConfigs.md).

## <a name="set-up-a-pull-client-to-download-configurations"></a>Při nastavování klienta o přijetí změn ke stažení konfigurace

Každý klient musí být nakonfigurovaný v **o přijetí změn** režimu a adresu url serveru o přijetí změn jeho konfigurace se mají ukládat. K tomuto účelu, budete muset nakonfigurovat místní Configuration Manageru (LCM) potřebné informace. Konfigurace LCM, vytvoříte speciální typ konfigurace dekorován **DSCLocalConfigurationManager** atribut. Další informace týkající se konfigurace LCM v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md).

Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze serveru s názvem "CONTOSO-PullSrv".

- Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace. **ServerURL** vlastnost určuje koncový bod pro vyžádání obsahu server.

- **RegistrationKey** vlastnost se sdílený klíč mezi všechny uzly klienta pro server na vyžádání a tohoto serveru vyžádané replikace. Stejná hodnota uložená v souboru na tomto serveru.
  > **Poznámka:**: Registrační kódy fungovat jenom s **webové** o přijetí změn servery. Je nutné použít **ConfigurationID** s **SMB** serveru vyžádané replikace.
  > Informace o konfiguraci serveru vyžádané replikace s použitím **ConfigurationID**, naleznete v tématu [nastavení načítacího klienta pomocí ID konfigurace](pullClientConfigId.md)

- **ConfigurationNames** vlastnost je pole, které určuje názvy konfigurace určené pro uzel klienta.
  >**Poznámka:** Pokud zadáte více než jednu hodnotu v **ConfigurationNames**, musíte zadat také **PartialConfiguration** blokuje v konfiguraci.
  >Informace o částečné konfigurace najdete v tématu [částečné konfigurace prostředí PowerShell Desired State Configuration](partialConfigs.md).

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

## <a name="set-up-a-pull-client-to-download-resources"></a>Chcete-li stáhnout prostředky při nastavování klienta o přijetí změn

Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat v konfiguraci LCM (jako v předchozím příkladu), načítacího klienta přetáhne prostředky ze stejné umístění, kde jsou uložené soubory ".mof". Můžete také zadat různá umístění, ve kterém klienti mohli stahovat prostředky. K určení prostředků serveru, můžete použít buď **ResourceRepositoryWeb** (pro webový server se o přijetí změn) nebo **ResourceRepositoryShare** blok (pro serveru vyžádané replikace SMB).

Následující příklad ukazuje metaconfiguration, který nastaví kolekci klienta ke stažení konfigurace ze serveru vyžádaných replikací s a zdroje ze sdílené složce SMB.

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

        ResourceRepositoryShare SMBResources
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigNames
```

## <a name="set-up-a-pull-client-to-report-status"></a>Při nastavování klienta o přijetí změn do sestav stavu

Jeden načítacího serveru můžete použít pro konfigurace, prostředků a vytváření sestav. Vytváření sestav není nakonfigurován pro klienty ve výchozím nastavení. Abyste mohli nakonfigurovat klienta k hlášení stavu, je nutné vytvořit **ReportRepositoryWeb** bloku. Následující příklad ukazuje metaconfiguration, který nastaví klienta o přijetí změn konfigurace, prostředků a odeslat data, pro generování sestav o přijetí změn jeden server.

> [!NOTE]
> Server sestav nemůže být sdílené složce SMB.

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
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a>Viz také

* [Nastavení načítacího klienta s ID konfigurace](PullClientConfigNames.md)
* [Nastavení webového serveru vyžádané replikace DSC](pullServer.md)

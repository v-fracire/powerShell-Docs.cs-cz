---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Při nastavování klienta o přijetí změn pomocí ID konfigurace v Powershellu 5.0 a novější
ms.openlocfilehash: 8d8cf478f9127e1b7005d1b9e832e84b11612c9c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403782"
---
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-50-and-later"></a>Při nastavování klienta o přijetí změn pomocí ID konfigurace v Powershellu 5.0 a novější

> Platí pro: Windows PowerShell 5.0

> [!IMPORTANT]
> Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce. Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).

Před nastavení načítacího klienta, byste měli nastavit serveru vyžádané replikace. I když toto pořadí není vyžadována, pomáhá při řešení potíží a vám pomůže zajistit, že registrace byla úspěšná. Nastavení serveru vyžádané replikace, můžete použít následující příručky:

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)

Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav. Následující části ukazují, jak nakonfigurovat klienta o přijetí změn s sdílenou složku protokolu SMB nebo protokolu HTTP serveru vyžádané replikace DSC. Při aktualizaci uzlu LCM se vás bude kontaktovat do nakonfigurovaného umístění ke stažení všechny přiřazené konfigurace. Pokud všechny požadované prostředky neexistuje na uzlu, se bude automaticky si je stáhnout z nakonfigurovaných umístění. Pokud uzel je nakonfigurované [serveru sestav](reportServer.md), potom oznámí stav operace.

> **Poznámka:**: Toto téma platí pro PowerShell 5.0. Informace o nastavení načítacího klienta v Powershellu 4.0 najdete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů v Powershellu 4.0](pullClientConfigID4.md)

## <a name="configure-the-pull-client-lcm"></a>Konfigurace LCM klienta o přijetí změn

Provádění některý z níže uvedených příkladech vytvoří nový výstupní složka s názvem **PullClientConfigID** a umístí soubor MOF metaconfiguration existuje. V takovém případě bude mít název souboru MOF metaconfiguration `localhost.meta.mof`.

Chcete-li použít konfiguraci, zavolejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavit umístění souboru MOF metaconfiguration. Příklad:

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a>ID konfigurace

V příkladech níže sad **ConfigurationID** vlastnost funkce LCM se **Guid** , který byl dříve vytvořili pro tento účel. **ConfigurationID** je co LCM používá k nalezení odpovídající konfigurace na serveru vyžádané replikace. Musí mít název konfiguračního souboru MOF na serveru vyžádané replikace `ConfigurationID.mof`, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel. Další informace najdete v části [publikovat konfigurace serveru vyžádaných replikací s (v4/v5)](publishConfigs.md).

Můžete vytvořit náhodnou **Guid** pomocí příkladu níže nebo pomocí [nový identifikátor Guid](/powershell/module/microsoft.powershell.utility/new-guid) rutiny.

```powershell
[System.Guid]::NewGuid()
```

Další informace o používání **GUID** ve vašem prostředí, najdete v článku [plánování GUID](/powershell/dsc/secureserver#guids).

## <a name="set-up-a-pull-client-to-download-configurations"></a>Při nastavování klienta o přijetí změn ke stažení konfigurace

Každý klient musí být nakonfigurovaný v **o přijetí změn** režimu a adresu url serveru o přijetí změn jeho konfigurace se mají ukládat. K tomuto účelu, budete muset nakonfigurovat místní Configuration Manageru (LCM) potřebné informace. Konfigurace LCM, vytvoříte speciální typ konfigurace dekorován **DSCLocalConfigurationManager** atribut. Další informace týkající se konfigurace LCM v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md).

### <a name="http-dsc-pull-server"></a>HTTP Server s DSC o přijetí změn

Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze serveru s názvem "CONTOSO-PullSrv".

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

Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace. **ServerUrl** Určuje adresu url DSC o přijetí změn

### <a name="smb-share"></a>Sdílené složky SMB

Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze sdílené složky SMB `\\SMBPullServer\Pull`.

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
            SourcePath = '\\SMBPullServer\Pull'
        }
    }
}
PullClientConfigID
```

Ve skriptu **ConfigurationRepositoryShare** bloku definuje serveru vyžádané replikace, který v tomto případě je právě do sdílené složky SMB.

## <a name="set-up-a-pull-client-to-download-resources"></a>Chcete-li stáhnout prostředky při nastavování klienta o přijetí změn

Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat v konfiguraci LCM (podobně jako v předchozích příkladech), načítacího klienta přetáhne prostředky ze stejného umístění, načte její konfigurace. Můžete také zadat samostatné umístění pro prostředky. Pokud chcete zadat umístění prostředků jako samostatný server, použijte **ResourceRepositoryWeb** bloku. Pokud chcete zadat umístění prostředku jako sdílenou složku protokolu SMB, použijte **ResourceRepositoryShare** bloku.

> [!NOTE]
> Můžete kombinovat **ConfigurationRepositoryWeb** s **ResourceRepositoryShare** nebo **ConfigurationRepositoryShare** s **ResourceRepositoryWeb** . Příklady nejsou zobrazeny níže.

### <a name="http-dsc-pull-server"></a>HTTP Server s DSC o přijetí změn

Následující metaconfiguration nakonfiguruje klienta o přijetí změn zobrazíte jeho konfiguraci z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**.

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
    }
}
PullClientConfigID
```

### <a name="smb-share"></a>Sdílené složky SMB

Následující příklad ukazuje metaconfiguration, který nastaví klienta o přijetí změn konfigurace ze sdílené složky SMB `\\SMBPullServer\Configurations`a prostředky ze sdílené složky SMB `\\SMBPullServer\Resources`.

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
            SourcePath = '\\SMBPullServer\Configurations'
        }

        ResourceRepositoryShare SMBResourceServer
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigID
```

#### <a name="automatically-download-resources-in-push-mode"></a>Automaticky stahovat prostředků v režimu Push

Od v Powershellu 5.0, klienty o přijetí změn můžete stáhnout moduly ze sdílené složky SMB, i když jsou nakonfigurované pro **Push** režimu. To je zvláště užitečná v situacích, kdy nechcete k nastavení serveru vyžádané replikace. **ResourceRepositoryShare** bloku lze použít bez zadání **ConfigurationRepositoryShare**. Následující příklad ukazuje metaconfiguration, který nastaví kolekci klienta o přijetí změn prostředků ze sdílené složce SMB `\\SMBPullServer\Resources`. Pokud je uzel **PUSHED** konfigurace, se automaticky stáhne všechny požadované prostředky ze sdílené složky zadané.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Push'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
        }

        ResourceRepositoryShare SMBResourceServer
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigID
```

## <a name="set-up-a-pull-client-to-report-status"></a>Při nastavování klienta o přijetí změn do sestav stavu

Ve výchozím nastavení nebude uzly odesílat sestavy do nakonfigurovaného serveru vyžádané replikace. Jeden načítacího serveru můžete použít pro konfigurace, prostředků a vytváření sestav, ale je nutné vytvořit **ReportRepositoryWeb** bloku k nastavení vytváření sestav.

### <a name="http-dsc-pull-server"></a>HTTP Server s DSC o přijetí změn

Následující příklad ukazuje metaconfiguration, který nastaví klienta o přijetí změn konfigurace, prostředků a odeslat data, pro generování sestav o přijetí změn jeden server.

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

K určení serveru sestav, můžete použít **ReportRepositoryWeb** bloku. Server sestav nemůže být serveru SMB.
Následující metaconfiguration nakonfiguruje klienta o přijetí změn zobrazíte jeho konfiguraci z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**a k odeslání zprávy o stavu  **CONTOSO-ReportSrv**:

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

### <a name="smb-share"></a>Sdílené složky SMB

Server sestav nemůže být sdílené složce SMB.

## <a name="next-steps"></a>Další kroky

Po načítacího klienta nakonfigurovaný, můžete provést další kroky následující příručky:

- [Publikování na serveru vyžádané replikace (v4 nebo verze 5) konfigurace](publishConfigs.md)
- [Balíček a prostředky nahrávání na serveru vyžádané replikace (v4)](package-upload-resources.md)

## <a name="see-also"></a>Viz také

* [Nastavení načítacího klienta s názvy konfigurace](pullClientConfigNames.md)

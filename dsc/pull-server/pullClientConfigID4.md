---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Při nastavování klienta o přijetí změn pomocí ID konfigurace v Powershellu 4.0
ms.openlocfilehash: 9adc767e91ff19d373c122a0d493e7b8703d5476
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403834"
---
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-40"></a>Při nastavování klienta o přijetí změn pomocí ID konfigurace v Powershellu 4.0

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

> [!IMPORTANT]
> Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce. Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).

Před nastavení načítacího klienta, byste měli nastavit serveru vyžádané replikace. I když toto pořadí není vyžadována, pomáhá při řešení potíží a vám pomůže zajistit, že registrace byla úspěšná. Nastavení serveru vyžádané replikace, můžete použít následující příručky:

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)

Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav. Následující části ukazují, jak nakonfigurovat klienta o přijetí změn s sdílenou složku protokolu SMB nebo protokolu HTTP serveru vyžádané replikace DSC. Při aktualizaci uzlu LCM se vás bude kontaktovat do nakonfigurovaného umístění ke stažení všechny přiřazené konfigurace. Pokud všechny požadované prostředky neexistuje na uzlu, se bude automaticky si je stáhnout z nakonfigurovaných umístění. Pokud uzel je nakonfigurované [serveru sestav](reportServer.md), potom oznámí stav operace.

## <a name="configure-the-pull-client-lcm"></a>Konfigurace LCM klienta o přijetí změn

Provádění některý z níže uvedených příkladech vytvoří nový výstupní složka s názvem **PullClientConfigID** a umístí soubor MOF metaconfiguration existuje. V takovém případě bude mít název souboru MOF metaconfiguration `localhost.meta.mof`.

Chcete-li použít konfiguraci, zavolejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavit umístění souboru MOF metaconfiguration. Příklad:

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a>ID konfigurace

V příkladech níže sada **ConfigurationID** vlastnost funkce LCM se **Guid** , který byl dříve vytvořili pro tento účel. **ConfigurationID** je co LCM používá k nalezení odpovídající konfigurace na serveru vyžádané replikace. Musí mít název konfiguračního souboru MOF na serveru vyžádané replikace `ConfigurationID.mof`, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel. Další informace najdete v tématu [publikovat konfigurace serveru vyžádaných replikací s (v4/v5)](publishConfigs.md).

Můžete vytvořit náhodnou **Guid** pomocí příkladu níže.

```powershell
[System.Guid]::NewGuid()
```

## <a name="set-up-a-pull-client-to-download-configurations"></a>Při nastavování klienta o přijetí změn ke stažení konfigurace

Každý klient musí být nakonfigurovaný v **o přijetí změn** režimu a adresu url serveru o přijetí změn jeho konfigurace se mají ukládat. K tomuto účelu, budete muset nakonfigurovat místní Configuration Manageru (LCM) potřebné informace. Konfigurace LCM, vytvoříte speciální typ konfigurace, s **LocalConfigurationManager** bloku. Další informace týkající se konfigurace LCM v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig4.md).

## <a name="http-dsc-pull-server"></a>HTTP Server s DSC o přijetí změn

Pokud serveru vyžádané replikace je nastaven jako webovou službu, můžete nastavit **DownloadManagerName** k **WebDownloadManager**. **WebDownloadManager** potřeba zadat **ServerUrl** k **DownloadManagerCustomData** klíč. Můžete také zadat hodnotu pro **AllowUnsecureConnection**, jako v následujícím příkladu. Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze serveru s názvem "PullServer".

```powershell
Configuration PullClientConfigId
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "WebDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "http://PullServer:8080/PSDSCPullServer/PSDSCPullServer.svc"; AllowUnsecureConnection = “TRUE”}
    }
}
PullClientConfigId -Output "."
```

## <a name="smb-share"></a>Sdílené složky SMB

Pokud serveru vyžádané replikace je nastaven jako sdílené složky SMB, nikoli webovou službu, můžete nastavit **DownloadManagerName** k **DscFileDownloadManager** místo **WebDownLoadManager**. **DscFileDownloadManager** potřeba zadat **SourcePath** vlastnost **DownloadManagerCustomData**. Následující skript nakonfiguruje funkce LCM se o přijetí změn konfigurace ze sdílené složce SMB na serveru s názvem "CONTOSO-SERVER" s názvem "SmbDscShare".

```powershell
Configuration PullClientConfigId
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "DscFileDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "\\CONTOSO-SERVER\SmbDscShare"}
    }
}
PullClientConfigId -Output "."
```

## <a name="next-steps"></a>Další kroky

Po načítacího klienta nakonfigurovaný, můžete provést další kroky následující příručky:

- [Publikování na serveru vyžádané replikace (v4 nebo verze 5) konfigurace](publishConfigs.md)
- [Balíček a prostředky nahrávání na serveru vyžádané replikace (v4)](package-upload-resources.md)

## <a name="see-also"></a>Viz také

- [Nastavení webového serveru vyžádané replikace DSC](pullServer.md)
- [Nastavení serveru vyžádané replikace SMB pro DSC](pullServerSMB.md)

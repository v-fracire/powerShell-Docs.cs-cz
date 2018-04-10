---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0
ms.openlocfilehash: 7074d842b7b99ef3fb6498b6dbc1e561b14caf16
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="setting-up-a-pull-client-using-configuration-id-in-powershell-40"></a>Nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadána adresa URL, kde může kontaktovat načítací server za účelem získání konfigurace. K tomuto účelu, budete muset nakonfigurovat místní Configuration Manager (LCM) nezbytné informace. Pokud chcete nakonfigurovat LCM, vytvoříte speciální typ konfigurace označuje jako "metakonfiguraci". Další informace o konfiguraci LCM najdete v tématu [Windows PowerShell 4.0 požadovaného stavu konfigurace místní Configuration Manager](metaConfig4.md)

Následující skript nakonfiguruje LCM pro vyžádání obsahu konfigurace ze serveru s názvem "PullServer":

```powershell
Configuration SimpleMetaConfigurationForPull
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
SimpleMetaConfigurationForPull -Output "."
```

Ve skriptu **DownloadManagerCustomData** předává adresu URL serveru pro vyžádání obsahu a (pro tento příklad) umožňuje nezabezpečené připojení.

Po spuštění tohoto skriptu, vytvoří novou výstupní složku s názvem **SimpleMetaConfigurationForPull** a vloží soubor MOF metakonfiguraci existuje.

Chcete-li použít konfiguraci, použijte **Set-DscLocalConfigurationManager** s parametry, **ComputerName** (použijte "localhost") a **cesta** (cestu k umístění cíl souboru localhost.meta.mof uzlu). Příklad:
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## <a name="configuration-id"></a>ID konfigurace
Nastaví skript **ConfigurationID** vlastnost LCM na identifikátor GUID, který byl dříve vytvořili pro tento účel (identifikátor GUID můžete vytvořit pomocí **nový Guid** rutiny). **ConfigurationID** je co LCM používá k nalezení odpovídající konfiguraci na tomto serveru. Konfigurační soubor MOF na tomto serveru musí mít název `ConfigurationID.mof`, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel.

## <a name="pulling-from-an-smb-server"></a>Vyžádání ze serveru SMB

Pokud server vyžádané replikace je nastavený jako sdílené složky SMB, nikoli webové služby, zadejte **DscFileDownloadManager** místo **WebDownLoadManager**.
**DscFileDownloadManager** trvá **SourcePath** vlastnost místo **ServerUrl**. Následující skript nakonfiguruje LCM načítat konfigurace ze složky SMB s názvem "SmbDscShare" na serveru s názvem "Serveru CONTOSO":

```powershell
Configuration SimpleMetaConfigurationForPull
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
SimpleMetaConfigurationForPull -Output "."
```

## <a name="see-also"></a>Viz také

- [Nastavení webového serveru vyžádané replikace DSC](pullServer.md)
- [Nastavení serveru vyžádané replikace SMB pro DSC](pullServerSMB.md)
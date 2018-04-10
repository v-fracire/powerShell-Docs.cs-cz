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
# <a name="setting-up-a-pull-client-using-configuration-id-in-powershell-40"></a><span data-ttu-id="878dd-103">Nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="878dd-103">Setting up a pull client using configuration ID in PowerShell 4.0</span></span>

><span data-ttu-id="878dd-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="878dd-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="878dd-105">Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadána adresa URL, kde může kontaktovat načítací server za účelem získání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="878dd-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="878dd-106">K tomuto účelu, budete muset nakonfigurovat místní Configuration Manager (LCM) nezbytné informace.</span><span class="sxs-lookup"><span data-stu-id="878dd-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="878dd-107">Pokud chcete nakonfigurovat LCM, vytvoříte speciální typ konfigurace označuje jako "metakonfiguraci".</span><span class="sxs-lookup"><span data-stu-id="878dd-107">To configure the LCM, you create a special type of configuration known as a "metaconfiguration".</span></span> <span data-ttu-id="878dd-108">Další informace o konfiguraci LCM najdete v tématu [Windows PowerShell 4.0 požadovaného stavu konfigurace místní Configuration Manager](metaConfig4.md)</span><span class="sxs-lookup"><span data-stu-id="878dd-108">For more information about configuring the LCM, see [Windows PowerShell 4.0 Desired State Configuration Local Configuration Manager](metaConfig4.md)</span></span>

<span data-ttu-id="878dd-109">Následující skript nakonfiguruje LCM pro vyžádání obsahu konfigurace ze serveru s názvem "PullServer":</span><span class="sxs-lookup"><span data-stu-id="878dd-109">The following script configures the LCM to pull configurations from a server named "PullServer":</span></span>

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

<span data-ttu-id="878dd-110">Ve skriptu **DownloadManagerCustomData** předává adresu URL serveru pro vyžádání obsahu a (pro tento příklad) umožňuje nezabezpečené připojení.</span><span class="sxs-lookup"><span data-stu-id="878dd-110">In the script, **DownloadManagerCustomData** passes the URL of the pull server and (for this example) allows an unsecured connection.</span></span>

<span data-ttu-id="878dd-111">Po spuštění tohoto skriptu, vytvoří novou výstupní složku s názvem **SimpleMetaConfigurationForPull** a vloží soubor MOF metakonfiguraci existuje.</span><span class="sxs-lookup"><span data-stu-id="878dd-111">After this script runs, it creates a new output folder called **SimpleMetaConfigurationForPull** and puts a metaconfiguration MOF file there.</span></span>

<span data-ttu-id="878dd-112">Chcete-li použít konfiguraci, použijte **Set-DscLocalConfigurationManager** s parametry, **ComputerName** (použijte "localhost") a **cesta** (cestu k umístění cíl souboru localhost.meta.mof uzlu).</span><span class="sxs-lookup"><span data-stu-id="878dd-112">To apply the configuration, use **Set-DscLocalConfigurationManager** with parameters for **ComputerName** (use “localhost”) and **Path** (the path to the location of the target node’s localhost.meta.mof file).</span></span> <span data-ttu-id="878dd-113">Příklad:</span><span class="sxs-lookup"><span data-stu-id="878dd-113">For example:</span></span>
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="878dd-114">ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="878dd-114">Configuration ID</span></span>
<span data-ttu-id="878dd-115">Nastaví skript **ConfigurationID** vlastnost LCM na identifikátor GUID, který byl dříve vytvořili pro tento účel (identifikátor GUID můžete vytvořit pomocí **nový Guid** rutiny).</span><span class="sxs-lookup"><span data-stu-id="878dd-115">The script sets the **ConfigurationID** property of the LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="878dd-116">**ConfigurationID** je co LCM používá k nalezení odpovídající konfiguraci na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="878dd-116">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="878dd-117">Konfigurační soubor MOF na tomto serveru musí mít název `ConfigurationID.mof`, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="878dd-117">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="pulling-from-an-smb-server"></a><span data-ttu-id="878dd-118">Vyžádání ze serveru SMB</span><span class="sxs-lookup"><span data-stu-id="878dd-118">Pulling from an SMB server</span></span>

<span data-ttu-id="878dd-119">Pokud server vyžádané replikace je nastavený jako sdílené složky SMB, nikoli webové služby, zadejte **DscFileDownloadManager** místo **WebDownLoadManager**.</span><span class="sxs-lookup"><span data-stu-id="878dd-119">If the pull server is set up as an SMB file share, rather than a web service, you specify the **DscFileDownloadManager** rather than the **WebDownLoadManager**.</span></span>
<span data-ttu-id="878dd-120">**DscFileDownloadManager** trvá **SourcePath** vlastnost místo **ServerUrl**.</span><span class="sxs-lookup"><span data-stu-id="878dd-120">The **DscFileDownloadManager** takes a **SourcePath** property instead of **ServerUrl**.</span></span> <span data-ttu-id="878dd-121">Následující skript nakonfiguruje LCM načítat konfigurace ze složky SMB s názvem "SmbDscShare" na serveru s názvem "Serveru CONTOSO":</span><span class="sxs-lookup"><span data-stu-id="878dd-121">The following script configures the LCM to pull configurations from an SMB share named "SmbDscShare" on a server named "CONTOSO-SERVER":</span></span>

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

## <a name="see-also"></a><span data-ttu-id="878dd-122">Viz také</span><span class="sxs-lookup"><span data-stu-id="878dd-122">See Also</span></span>

- [<span data-ttu-id="878dd-123">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="878dd-123">Setting up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="878dd-124">Nastavení serveru vyžádané replikace SMB pro DSC</span><span class="sxs-lookup"><span data-stu-id="878dd-124">Setting up a DSC SMB pull server</span></span>](pullServerSMB.md)
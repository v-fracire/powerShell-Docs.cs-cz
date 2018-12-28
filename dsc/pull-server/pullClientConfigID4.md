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
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-40"></a><span data-ttu-id="2935c-103">Při nastavování klienta o přijetí změn pomocí ID konfigurace v Powershellu 4.0</span><span class="sxs-lookup"><span data-stu-id="2935c-103">Set up a Pull Client using Configuration IDs in PowerShell 4.0</span></span>

><span data-ttu-id="2935c-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="2935c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2935c-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="2935c-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="2935c-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="2935c-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="2935c-107">Před nastavení načítacího klienta, byste měli nastavit serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="2935c-107">Before setting up a pull client, you should set up a pull server.</span></span> <span data-ttu-id="2935c-108">I když toto pořadí není vyžadována, pomáhá při řešení potíží a vám pomůže zajistit, že registrace byla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="2935c-108">Though this order is not required, it helps with troubleshooting, and helps you ensure that the registration was successful.</span></span> <span data-ttu-id="2935c-109">Nastavení serveru vyžádané replikace, můžete použít následující příručky:</span><span class="sxs-lookup"><span data-stu-id="2935c-109">To set up a pull server, you can use the following guides:</span></span>

- [<span data-ttu-id="2935c-110">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="2935c-110">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="2935c-111">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="2935c-111">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="2935c-112">Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav.</span><span class="sxs-lookup"><span data-stu-id="2935c-112">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="2935c-113">Následující části ukazují, jak nakonfigurovat klienta o přijetí změn s sdílenou složku protokolu SMB nebo protokolu HTTP serveru vyžádané replikace DSC.</span><span class="sxs-lookup"><span data-stu-id="2935c-113">The sections below show you how to configure a pull client with an SMB share or HTTP DSC Pull Server.</span></span> <span data-ttu-id="2935c-114">Při aktualizaci uzlu LCM se vás bude kontaktovat do nakonfigurovaného umístění ke stažení všechny přiřazené konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2935c-114">When the Node's LCM refreshes, it will reach out to the configured location to download any assigned configurations.</span></span> <span data-ttu-id="2935c-115">Pokud všechny požadované prostředky neexistuje na uzlu, se bude automaticky si je stáhnout z nakonfigurovaných umístění.</span><span class="sxs-lookup"><span data-stu-id="2935c-115">If any required resources do not exist on the Node, it will automatically download them from the configured location.</span></span> <span data-ttu-id="2935c-116">Pokud uzel je nakonfigurované [serveru sestav](reportServer.md), potom oznámí stav operace.</span><span class="sxs-lookup"><span data-stu-id="2935c-116">If the Node is configured with a [Report Server](reportServer.md), it will then report the status of the operation.</span></span>

## <a name="configure-the-pull-client-lcm"></a><span data-ttu-id="2935c-117">Konfigurace LCM klienta o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="2935c-117">Configure the pull client LCM</span></span>

<span data-ttu-id="2935c-118">Provádění některý z níže uvedených příkladech vytvoří nový výstupní složka s názvem **PullClientConfigID** a umístí soubor MOF metaconfiguration existuje.</span><span class="sxs-lookup"><span data-stu-id="2935c-118">Executing any of the examples below creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="2935c-119">V takovém případě bude mít název souboru MOF metaconfiguration `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="2935c-119">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="2935c-120">Chcete-li použít konfiguraci, zavolejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavit umístění souboru MOF metaconfiguration.</span><span class="sxs-lookup"><span data-stu-id="2935c-120">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="2935c-121">Příklad:</span><span class="sxs-lookup"><span data-stu-id="2935c-121">For example:</span></span>

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="2935c-122">ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="2935c-122">Configuration ID</span></span>

<span data-ttu-id="2935c-123">V příkladech níže sada **ConfigurationID** vlastnost funkce LCM se **Guid** , který byl dříve vytvořili pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="2935c-123">The examples below set the **ConfigurationID** property of the LCM to a **Guid** that had been previously created for this purpose.</span></span> <span data-ttu-id="2935c-124">**ConfigurationID** je co LCM používá k nalezení odpovídající konfigurace na serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="2935c-124">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="2935c-125">Musí mít název konfiguračního souboru MOF na serveru vyžádané replikace `ConfigurationID.mof`, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="2935c-125">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="2935c-126">Další informace najdete v tématu [publikovat konfigurace serveru vyžádaných replikací s (v4/v5)](publishConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="2935c-126">For more information, see [Publish Configurations to a Pull Server (v4/v5)](publishConfigs.md).</span></span>

<span data-ttu-id="2935c-127">Můžete vytvořit náhodnou **Guid** pomocí příkladu níže.</span><span class="sxs-lookup"><span data-stu-id="2935c-127">You can create a random **Guid** using the example below.</span></span>

```powershell
[System.Guid]::NewGuid()
```

## <a name="set-up-a-pull-client-to-download-configurations"></a><span data-ttu-id="2935c-128">Při nastavování klienta o přijetí změn ke stažení konfigurace</span><span class="sxs-lookup"><span data-stu-id="2935c-128">Set up a Pull Client to download Configurations</span></span>

<span data-ttu-id="2935c-129">Každý klient musí být nakonfigurovaný v **o přijetí změn** režimu a adresu url serveru o přijetí změn jeho konfigurace se mají ukládat.</span><span class="sxs-lookup"><span data-stu-id="2935c-129">Each client must be configured in **Pull** mode and given the pull server url where its configuration is stored.</span></span> <span data-ttu-id="2935c-130">K tomuto účelu, budete muset nakonfigurovat místní Configuration Manageru (LCM) potřebné informace.</span><span class="sxs-lookup"><span data-stu-id="2935c-130">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="2935c-131">Konfigurace LCM, vytvoříte speciální typ konfigurace, s **LocalConfigurationManager** bloku.</span><span class="sxs-lookup"><span data-stu-id="2935c-131">To configure the LCM, you create a special type of configuration, with a **LocalConfigurationManager** block.</span></span> <span data-ttu-id="2935c-132">Další informace týkající se konfigurace LCM v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig4.md).</span><span class="sxs-lookup"><span data-stu-id="2935c-132">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig4.md).</span></span>

## <a name="http-dsc-pull-server"></a><span data-ttu-id="2935c-133">HTTP Server s DSC o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="2935c-133">HTTP DSC Pull Server</span></span>

<span data-ttu-id="2935c-134">Pokud serveru vyžádané replikace je nastaven jako webovou službu, můžete nastavit **DownloadManagerName** k **WebDownloadManager**.</span><span class="sxs-lookup"><span data-stu-id="2935c-134">If the pull server is set up as a web service, you set the **DownloadManagerName** to **WebDownloadManager**.</span></span> <span data-ttu-id="2935c-135">**WebDownloadManager** potřeba zadat **ServerUrl** k **DownloadManagerCustomData** klíč.</span><span class="sxs-lookup"><span data-stu-id="2935c-135">The **WebDownloadManager** requires that you specify a **ServerUrl** to the **DownloadManagerCustomData** key.</span></span> <span data-ttu-id="2935c-136">Můžete také zadat hodnotu pro **AllowUnsecureConnection**, jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="2935c-136">You can also specify a value for **AllowUnsecureConnection**, as in the example below.</span></span> <span data-ttu-id="2935c-137">Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze serveru s názvem "PullServer".</span><span class="sxs-lookup"><span data-stu-id="2935c-137">The following script configures the LCM to pull configurations from a server named "PullServer".</span></span>

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

## <a name="smb-share"></a><span data-ttu-id="2935c-138">Sdílené složky SMB</span><span class="sxs-lookup"><span data-stu-id="2935c-138">SMB Share</span></span>

<span data-ttu-id="2935c-139">Pokud serveru vyžádané replikace je nastaven jako sdílené složky SMB, nikoli webovou službu, můžete nastavit **DownloadManagerName** k **DscFileDownloadManager** místo **WebDownLoadManager**.</span><span class="sxs-lookup"><span data-stu-id="2935c-139">If the pull server is set up as an SMB file share, rather than a web service, you set the **DownloadManagerName** to **DscFileDownloadManager** rather than the **WebDownLoadManager**.</span></span> <span data-ttu-id="2935c-140">**DscFileDownloadManager** potřeba zadat **SourcePath** vlastnost **DownloadManagerCustomData**.</span><span class="sxs-lookup"><span data-stu-id="2935c-140">The **DscFileDownloadManager** requires that you specify a **SourcePath** property in the **DownloadManagerCustomData**.</span></span> <span data-ttu-id="2935c-141">Následující skript nakonfiguruje funkce LCM se o přijetí změn konfigurace ze sdílené složce SMB na serveru s názvem "CONTOSO-SERVER" s názvem "SmbDscShare".</span><span class="sxs-lookup"><span data-stu-id="2935c-141">The following script configures the LCM to pull configurations from an SMB share named "SmbDscShare" on a server named "CONTOSO-SERVER".</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2935c-142">Další kroky</span><span class="sxs-lookup"><span data-stu-id="2935c-142">Next Steps</span></span>

<span data-ttu-id="2935c-143">Po načítacího klienta nakonfigurovaný, můžete provést další kroky následující příručky:</span><span class="sxs-lookup"><span data-stu-id="2935c-143">Once the pull client has been configured, you can use the following guides to perform the next steps:</span></span>

- [<span data-ttu-id="2935c-144">Publikování na serveru vyžádané replikace (v4 nebo verze 5) konfigurace</span><span class="sxs-lookup"><span data-stu-id="2935c-144">Publish Configurations to a Pull Server (v4/v5)</span></span>](publishConfigs.md)
- [<span data-ttu-id="2935c-145">Balíček a prostředky nahrávání na serveru vyžádané replikace (v4)</span><span class="sxs-lookup"><span data-stu-id="2935c-145">Package and Upload Resources to a Pull Server (v4)</span></span>](package-upload-resources.md)

## <a name="see-also"></a><span data-ttu-id="2935c-146">Viz také</span><span class="sxs-lookup"><span data-stu-id="2935c-146">See Also</span></span>

- [<span data-ttu-id="2935c-147">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="2935c-147">Set up a DSC web pull server</span></span>](pullServer.md)
- [<span data-ttu-id="2935c-148">Nastavení serveru vyžádané replikace SMB pro DSC</span><span class="sxs-lookup"><span data-stu-id="2935c-148">Set up a DSC SMB pull server</span></span>](pullServerSMB.md)

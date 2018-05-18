---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Použití konfiguračních identifikátorů k nastavení načítacího klienta
ms.openlocfilehash: b4a45c4d014b3c4fc0140ad492f81474b260065a
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a><span data-ttu-id="0d857-103">Použití konfiguračních identifikátorů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="0d857-103">Setting up a pull client using configuration ID</span></span>

> <span data-ttu-id="0d857-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0d857-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d857-105">Server pro vyžádání obsahu (funkce systému Windows *DSC služby*) je podporované součásti systému Windows Server jsou však nejsou žádné plány, které nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="0d857-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="0d857-106">Doporučujeme začít Přechod spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace s v systému Windows Server) nebo jedno z řešení komunity uvedené [zde](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="0d857-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="0d857-107">Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadána adresa URL, kde může kontaktovat načítací server za účelem získání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="0d857-107">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span> <span data-ttu-id="0d857-108">K tomuto účelu, budete muset nakonfigurovat místní Configuration Manager (LCM) nezbytné informace.</span><span class="sxs-lookup"><span data-stu-id="0d857-108">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="0d857-109">Pokud chcete nakonfigurovat LCM, vytvoříte speciální typ konfigurace, označených pomocí **DSCLocalConfigurationManager** atribut.</span><span class="sxs-lookup"><span data-stu-id="0d857-109">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="0d857-110">Další informace o konfiguraci LCM najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="0d857-110">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="0d857-111">**Poznámka:**: Toto téma se týká PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="0d857-111">**Note**: This topic applies to PowerShell 5.0.</span></span> <span data-ttu-id="0d857-112">Informace o nastavení klienta přijetí změn v prostředí PowerShell 4.0 najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="0d857-112">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="0d857-113">Následující skript nakonfiguruje LCM přijetí změn konfigurace ze serveru s názvem "CONTOSO-PullSrv".</span><span class="sxs-lookup"><span data-stu-id="0d857-113">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

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

<span data-ttu-id="0d857-114">Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="0d857-114">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="0d857-115">**ServerURL**</span><span class="sxs-lookup"><span data-stu-id="0d857-115">The **ServerURL**</span></span>

<span data-ttu-id="0d857-116">Po spuštění tohoto skriptu vytvoří nový výstupní složky s názvem **PullClientConfigID** a vloží soubor MOF metakonfiguraci existuje.</span><span class="sxs-lookup"><span data-stu-id="0d857-116">After this script runs, it creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="0d857-117">V takovém případě bude mít název souboru MOF metakonfiguraci `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="0d857-117">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="0d857-118">Chcete-li použít konfiguraci, volejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavte na umístění souboru MOF metakonfiguraci.</span><span class="sxs-lookup"><span data-stu-id="0d857-118">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="0d857-119">Příklad: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span><span class="sxs-lookup"><span data-stu-id="0d857-119">For example: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`</span></span>

## <a name="configuration-id"></a><span data-ttu-id="0d857-120">ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="0d857-120">Configuration ID</span></span>

<span data-ttu-id="0d857-121">Nastaví skript **ConfigurationID** vlastnost LCM na identifikátor GUID, který byl dříve vytvořili pro tento účel (identifikátor GUID můžete vytvořit pomocí **nový Guid** rutiny).</span><span class="sxs-lookup"><span data-stu-id="0d857-121">The script sets the **ConfigurationID** property of LCM to a GUID that had been previously created for this purpose (you can create a GUID by using the **New-Guid** cmdlet).</span></span> <span data-ttu-id="0d857-122">**ConfigurationID** je co LCM používá k nalezení odpovídající konfiguraci na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="0d857-122">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="0d857-123">Konfigurační soubor MOF na tomto serveru musí mít název _ConfigurationID_MOF, kde _ConfigurationID_ je hodnota **ConfigurationID** vlastnost cíle LCM uzlu.</span><span class="sxs-lookup"><span data-stu-id="0d857-123">The configuration MOF file on the pull server must be named _ConfigurationID_.mof, where _ConfigurationID_ is the value of the **ConfigurationID** property of the target node's LCM.</span></span>

## <a name="smb-pull-server"></a><span data-ttu-id="0d857-124">Vyžádání serveru SMB</span><span class="sxs-lookup"><span data-stu-id="0d857-124">SMB pull server</span></span>

<span data-ttu-id="0d857-125">Nastavení klienta pro vyžádání obsahu konfigurace ze serveru SMB, použijte **ConfigurationRepositoryShare** bloku.</span><span class="sxs-lookup"><span data-stu-id="0d857-125">To set up a client to pull configurations from an SMB server, use a **ConfigurationRepositoryShare** block.</span></span> <span data-ttu-id="0d857-126">V **ConfigurationRepositoryShare** bloku, musíte zadat cestu k serveru nastavením **SourcePath** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="0d857-126">In a **ConfigurationRepositoryShare** block, you specify the path to the server by setting the **SourcePath** property.</span></span> <span data-ttu-id="0d857-127">Následující metakonfiguraci nakonfiguruje cílový uzel načítat z serveru SMB vyžádání obsahu s názvem **SMBPullServer**.</span><span class="sxs-lookup"><span data-stu-id="0d857-127">The following metaconfiguration configures the target node to pull from an SMB pull server named **SMBPullServer**.</span></span>

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

## <a name="resource-and-report-servers"></a><span data-ttu-id="0d857-128">Servery prostředků a sestavy</span><span class="sxs-lookup"><span data-stu-id="0d857-128">Resource and report servers</span></span>

<span data-ttu-id="0d857-129">Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat ve vaší konfiguraci LCM (jako v předchozím příkladu), klient pro vyžádání obsahu načte prostředky z Zadaný server, ale nebude odesílat zprávy do něj.</span><span class="sxs-lookup"><span data-stu-id="0d857-129">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span> <span data-ttu-id="0d857-130">Jeden načítacího serveru můžete použít pro konfigurace, prostředky a vytváření sestav, ale je nutné vytvořit **ReportRepositoryWeb** blok k nastavení vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="0d857-130">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>

<span data-ttu-id="0d857-131">Následující příklad ukazuje metakonfiguraci, který nastaví kolekci klienta k přijetí změn konfigurace a prostředky a odesílat data, pro vytváření sestav k jedné z vlastního serveru.</span><span class="sxs-lookup"><span data-stu-id="0d857-131">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="0d857-132">Můžete také zadat servery různých vyžádání obsahu pro prostředky a vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="0d857-132">You can also specify different pull servers for resources and reporting.</span></span> <span data-ttu-id="0d857-133">K určení serveru prostředků, můžete buď použít **ResourceRepositoryWeb** (pro webový server pro vyžádání obsahu) nebo **ResourceRepositoryShare** blok (pro vyžádání obsahu serveru SMB).</span><span class="sxs-lookup"><span data-stu-id="0d857-133">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="0d857-134">Chcete-li zadat server sestav, je použít **ReportRepositoryWeb** bloku.</span><span class="sxs-lookup"><span data-stu-id="0d857-134">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="0d857-135">Server sestav nemůže být serveru SMB.</span><span class="sxs-lookup"><span data-stu-id="0d857-135">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="0d857-136">Následující metakonfiguraci nakonfiguruje klienta vyžádání obsahu k získání jeho konfigurace z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**a k odeslání zprávy o stavu do  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="0d857-136">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="0d857-137">Viz také</span><span class="sxs-lookup"><span data-stu-id="0d857-137">See Also</span></span>

* [<span data-ttu-id="0d857-138">Nastavení klienta vyžádání obsahu s názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="0d857-138">Setting up a pull client with configuration names</span></span>](pullClientConfigNames.md)
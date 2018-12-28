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
# <a name="set-up-a-pull-client-using-configuration-names-in-powershell-50-and-later"></a><span data-ttu-id="1c533-103">Nastavení klienta o přijetí změn se názvy konfigurací v Powershellu 5.0 a novější</span><span class="sxs-lookup"><span data-stu-id="1c533-103">Set up a Pull Client using Configuration Names in PowerShell 5.0 and later</span></span>

> <span data-ttu-id="1c533-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1c533-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c533-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="1c533-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="1c533-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="1c533-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="1c533-107">Před nastavení načítacího klienta, byste měli nastavit serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="1c533-107">Before setting up a pull client, you should set up a pull server.</span></span> <span data-ttu-id="1c533-108">I když toto pořadí není vyžadována, pomáhá při řešení potíží a vám pomůže zajistit, že registrace byla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="1c533-108">Though this order is not required, it helps with troubleshooting, and helps you ensure that the registration was successful.</span></span> <span data-ttu-id="1c533-109">Nastavení serveru vyžádané replikace, můžete použít následující příručky:</span><span class="sxs-lookup"><span data-stu-id="1c533-109">To set up a pull server, you can use the following guides:</span></span>

- [<span data-ttu-id="1c533-110">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="1c533-110">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="1c533-111">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="1c533-111">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="1c533-112">Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav.</span><span class="sxs-lookup"><span data-stu-id="1c533-112">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="1c533-113">Následující části ukazují, jak nakonfigurovat klienta o přijetí změn s sdílenou složku protokolu SMB nebo protokolu HTTP serveru vyžádané replikace DSC.</span><span class="sxs-lookup"><span data-stu-id="1c533-113">The sections below show you how to configure a pull client with an SMB share or HTTP DSC Pull Server.</span></span> <span data-ttu-id="1c533-114">Při aktualizaci uzlu LCM se vás bude kontaktovat do nakonfigurovaného umístění ke stažení všechny přiřazené konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1c533-114">When the Node's LCM refreshes, it will reach out to the configured location to download any assigned configurations.</span></span> <span data-ttu-id="1c533-115">Pokud všechny požadované prostředky neexistuje na uzlu, se bude automaticky si je stáhnout z nakonfigurovaných umístění.</span><span class="sxs-lookup"><span data-stu-id="1c533-115">If any required resources do not exist on the Node, it will automatically download them from the configured location.</span></span> <span data-ttu-id="1c533-116">Pokud uzel je nakonfigurované [serveru sestav](reportServer.md), potom oznámí stav operace.</span><span class="sxs-lookup"><span data-stu-id="1c533-116">If the Node is configured with a [Report Server](reportServer.md), it will then report the status of the operation.</span></span>

> <span data-ttu-id="1c533-117">**Poznámka:**: Toto téma platí pro PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="1c533-117">**Note**: This topic applies to PowerShell 5.0.</span></span>
<span data-ttu-id="1c533-118">Informace o nastavení načítacího klienta v Powershellu 4.0 najdete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů v Powershellu 4.0](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="1c533-118">For information on setting up a pull client in PowerShell 4.0, see [Set up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

## <a name="configure-the-pull-client-lcm"></a><span data-ttu-id="1c533-119">Konfigurace LCM klienta o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="1c533-119">Configure the pull client LCM</span></span>

<span data-ttu-id="1c533-120">Provádění některý z níže uvedených příkladech vytvoří nový výstupní složka s názvem **PullClientConfigName** a umístí soubor MOF metaconfiguration existuje.</span><span class="sxs-lookup"><span data-stu-id="1c533-120">Executing any of the examples below creates a new output folder named **PullClientConfigName** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="1c533-121">V takovém případě bude mít název souboru MOF metaconfiguration `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="1c533-121">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="1c533-122">Chcete-li použít konfiguraci, zavolejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavit umístění souboru MOF metaconfiguration.</span><span class="sxs-lookup"><span data-stu-id="1c533-122">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="1c533-123">Příklad:</span><span class="sxs-lookup"><span data-stu-id="1c533-123">For example:</span></span>

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigName –Verbose.
```

## <a name="configuration-name"></a><span data-ttu-id="1c533-124">Název konfigurace</span><span class="sxs-lookup"><span data-stu-id="1c533-124">Configuration Name</span></span>

<span data-ttu-id="1c533-125">V příkladech níže sad **ConfigurationName** vlastnost LCM název předtím zkompilovanou konfiguraci, vytvořený k tomuto účelu.</span><span class="sxs-lookup"><span data-stu-id="1c533-125">The examples below sets the **ConfigurationName** property of the LCM to the name of a previously compiled Configuration, created for this purpose.</span></span> <span data-ttu-id="1c533-126">**ConfigurationName** je co LCM používá k nalezení odpovídající konfigurace na serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="1c533-126">The **ConfigurationName** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="1c533-127">Musí mít název konfiguračního souboru MOF na serveru vyžádané replikace `<ConfigurationName>.mof`, v tomto případě "ClientConfig.mof".</span><span class="sxs-lookup"><span data-stu-id="1c533-127">The configuration MOF file on the pull server must be named `<ConfigurationName>.mof`, in this case, "ClientConfig.mof".</span></span> <span data-ttu-id="1c533-128">Další informace najdete v tématu [publikovat konfigurace serveru vyžádaných replikací s (v4/v5)](publishConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="1c533-128">For more information, see [Publish Configurations to a Pull Server (v4/v5)](publishConfigs.md).</span></span>

## <a name="set-up-a-pull-client-to-download-configurations"></a><span data-ttu-id="1c533-129">Při nastavování klienta o přijetí změn ke stažení konfigurace</span><span class="sxs-lookup"><span data-stu-id="1c533-129">Set up a Pull Client to download Configurations</span></span>

<span data-ttu-id="1c533-130">Každý klient musí být nakonfigurovaný v **o přijetí změn** režimu a adresu url serveru o přijetí změn jeho konfigurace se mají ukládat.</span><span class="sxs-lookup"><span data-stu-id="1c533-130">Each client must be configured in **Pull** mode and given the pull server url where its configuration is stored.</span></span> <span data-ttu-id="1c533-131">K tomuto účelu, budete muset nakonfigurovat místní Configuration Manageru (LCM) potřebné informace.</span><span class="sxs-lookup"><span data-stu-id="1c533-131">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="1c533-132">Konfigurace LCM, vytvoříte speciální typ konfigurace dekorován **DSCLocalConfigurationManager** atribut.</span><span class="sxs-lookup"><span data-stu-id="1c533-132">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="1c533-133">Další informace týkající se konfigurace LCM v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="1c533-133">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md).</span></span>

<span data-ttu-id="1c533-134">Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze serveru s názvem "CONTOSO-PullSrv".</span><span class="sxs-lookup"><span data-stu-id="1c533-134">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

- <span data-ttu-id="1c533-135">Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="1c533-135">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="1c533-136">**ServerURL** vlastnost určuje koncový bod pro vyžádání obsahu server.</span><span class="sxs-lookup"><span data-stu-id="1c533-136">The **ServerURL** property specifies the endpoint for the pull server.</span></span>

- <span data-ttu-id="1c533-137">**RegistrationKey** vlastnost se sdílený klíč mezi všechny uzly klienta pro server na vyžádání a tohoto serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="1c533-137">The **RegistrationKey** property is a shared key between all client nodes for a pull server and that pull server.</span></span> <span data-ttu-id="1c533-138">Stejná hodnota uložená v souboru na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="1c533-138">The same value is stored in a file on the pull server.</span></span>
  > <span data-ttu-id="1c533-139">**Poznámka:**: Registrační kódy fungovat jenom s **webové** o přijetí změn servery.</span><span class="sxs-lookup"><span data-stu-id="1c533-139">**Note**: Registration keys work only with **web** pull servers.</span></span> <span data-ttu-id="1c533-140">Je nutné použít **ConfigurationID** s **SMB** serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="1c533-140">You must still use **ConfigurationID** with an **SMB** pull server.</span></span>
  > <span data-ttu-id="1c533-141">Informace o konfiguraci serveru vyžádané replikace s použitím **ConfigurationID**, naleznete v tématu [nastavení načítacího klienta pomocí ID konfigurace](pullClientConfigId.md)</span><span class="sxs-lookup"><span data-stu-id="1c533-141">For information about configuring a pull server by using **ConfigurationID**, see [Setting up a pull client using configuration ID](pullClientConfigId.md)</span></span>

- <span data-ttu-id="1c533-142">**ConfigurationNames** vlastnost je pole, které určuje názvy konfigurace určené pro uzel klienta.</span><span class="sxs-lookup"><span data-stu-id="1c533-142">The **ConfigurationNames** property is an array that specifies the names of the configurations intended for the client node.</span></span>
  ><span data-ttu-id="1c533-143">**Poznámka:** Pokud zadáte více než jednu hodnotu v **ConfigurationNames**, musíte zadat také **PartialConfiguration** blokuje v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1c533-143">**Note:** If you specify more than one value in the **ConfigurationNames**, you must also specify **PartialConfiguration** blocks in your configuration.</span></span>
  ><span data-ttu-id="1c533-144">Informace o částečné konfigurace najdete v tématu [částečné konfigurace prostředí PowerShell Desired State Configuration](partialConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="1c533-144">For information about partial configurations, see [PowerShell Desired State Configuration partial configurations](partialConfigs.md).</span></span>

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

## <a name="set-up-a-pull-client-to-download-resources"></a><span data-ttu-id="1c533-145">Chcete-li stáhnout prostředky při nastavování klienta o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="1c533-145">Set up a Pull Client to download Resources</span></span>

<span data-ttu-id="1c533-146">Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat v konfiguraci LCM (jako v předchozím příkladu), načítacího klienta přetáhne prostředky ze stejné umístění, kde jsou uložené soubory ".mof".</span><span class="sxs-lookup"><span data-stu-id="1c533-146">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from same location where your ".mof" files are stored.</span></span> <span data-ttu-id="1c533-147">Můžete také zadat různá umístění, ve kterém klienti mohli stahovat prostředky.</span><span class="sxs-lookup"><span data-stu-id="1c533-147">You can also specify different locations where clients can download resources.</span></span> <span data-ttu-id="1c533-148">K určení prostředků serveru, můžete použít buď **ResourceRepositoryWeb** (pro webový server se o přijetí změn) nebo **ResourceRepositoryShare** blok (pro serveru vyžádané replikace SMB).</span><span class="sxs-lookup"><span data-stu-id="1c533-148">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>

<span data-ttu-id="1c533-149">Následující příklad ukazuje metaconfiguration, který nastaví kolekci klienta ke stažení konfigurace ze serveru vyžádaných replikací s a zdroje ze sdílené složce SMB.</span><span class="sxs-lookup"><span data-stu-id="1c533-149">The following example shows a metaconfiguration that sets up a client to download configurations from a Pull Server, and resources from an SMB share.</span></span>

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

## <a name="set-up-a-pull-client-to-report-status"></a><span data-ttu-id="1c533-150">Při nastavování klienta o přijetí změn do sestav stavu</span><span class="sxs-lookup"><span data-stu-id="1c533-150">Set up a Pull Client to report status</span></span>

<span data-ttu-id="1c533-151">Jeden načítacího serveru můžete použít pro konfigurace, prostředků a vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="1c533-151">You can use a single pull server for configurations, resources, and reporting.</span></span> <span data-ttu-id="1c533-152">Vytváření sestav není nakonfigurován pro klienty ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="1c533-152">Reporting is not configured for clients by default.</span></span> <span data-ttu-id="1c533-153">Abyste mohli nakonfigurovat klienta k hlášení stavu, je nutné vytvořit **ReportRepositoryWeb** bloku.</span><span class="sxs-lookup"><span data-stu-id="1c533-153">To configure a client to report status, you have to create a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="1c533-154">Následující příklad ukazuje metaconfiguration, který nastaví klienta o přijetí změn konfigurace, prostředků a odeslat data, pro generování sestav o přijetí změn jeden server.</span><span class="sxs-lookup"><span data-stu-id="1c533-154">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

> [!NOTE]
> <span data-ttu-id="1c533-155">Server sestav nemůže být sdílené složce SMB.</span><span class="sxs-lookup"><span data-stu-id="1c533-155">A report server cannot be an SMB share.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="1c533-156">Viz také</span><span class="sxs-lookup"><span data-stu-id="1c533-156">See Also</span></span>

* [<span data-ttu-id="1c533-157">Nastavení načítacího klienta s ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="1c533-157">Setting up a pull client with configuration ID</span></span>](PullClientConfigNames.md)
* [<span data-ttu-id="1c533-158">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="1c533-158">Setting up a DSC web pull server</span></span>](pullServer.md)

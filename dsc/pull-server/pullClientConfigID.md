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
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-50-and-later"></a><span data-ttu-id="4cefd-103">Při nastavování klienta o přijetí změn pomocí ID konfigurace v Powershellu 5.0 a novější</span><span class="sxs-lookup"><span data-stu-id="4cefd-103">Set up a Pull Client using Configuration IDs in PowerShell 5.0 and later</span></span>

> <span data-ttu-id="4cefd-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4cefd-104">Applies To: Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4cefd-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="4cefd-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="4cefd-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="4cefd-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="4cefd-107">Před nastavení načítacího klienta, byste měli nastavit serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-107">Before setting up a pull client, you should set up a pull server.</span></span> <span data-ttu-id="4cefd-108">I když toto pořadí není vyžadována, pomáhá při řešení potíží a vám pomůže zajistit, že registrace byla úspěšná.</span><span class="sxs-lookup"><span data-stu-id="4cefd-108">Though this order is not required, it helps with troubleshooting, and helps you ensure that the registration was successful.</span></span> <span data-ttu-id="4cefd-109">Nastavení serveru vyžádané replikace, můžete použít následující příručky:</span><span class="sxs-lookup"><span data-stu-id="4cefd-109">To set up a pull server, you can use the following guides:</span></span>

- [<span data-ttu-id="4cefd-110">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="4cefd-110">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="4cefd-111">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="4cefd-111">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="4cefd-112">Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav.</span><span class="sxs-lookup"><span data-stu-id="4cefd-112">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="4cefd-113">Následující části ukazují, jak nakonfigurovat klienta o přijetí změn s sdílenou složku protokolu SMB nebo protokolu HTTP serveru vyžádané replikace DSC.</span><span class="sxs-lookup"><span data-stu-id="4cefd-113">The sections below show you how to configure a pull client with an SMB share or HTTP DSC Pull Server.</span></span> <span data-ttu-id="4cefd-114">Při aktualizaci uzlu LCM se vás bude kontaktovat do nakonfigurovaného umístění ke stažení všechny přiřazené konfigurace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-114">When the Node's LCM refreshes, it will reach out to the configured location to download any assigned configurations.</span></span> <span data-ttu-id="4cefd-115">Pokud všechny požadované prostředky neexistuje na uzlu, se bude automaticky si je stáhnout z nakonfigurovaných umístění.</span><span class="sxs-lookup"><span data-stu-id="4cefd-115">If any required resources do not exist on the Node, it will automatically download them from the configured location.</span></span> <span data-ttu-id="4cefd-116">Pokud uzel je nakonfigurované [serveru sestav](reportServer.md), potom oznámí stav operace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-116">If the Node is configured with a [Report Server](reportServer.md), it will then report the status of the operation.</span></span>

> <span data-ttu-id="4cefd-117">**Poznámka:**: Toto téma platí pro PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="4cefd-117">**Note**: This topic applies to PowerShell 5.0.</span></span> <span data-ttu-id="4cefd-118">Informace o nastavení načítacího klienta v Powershellu 4.0 najdete v tématu [nastavení načítacího klienta použití konfiguračních identifikátorů v Powershellu 4.0](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="4cefd-118">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

## <a name="configure-the-pull-client-lcm"></a><span data-ttu-id="4cefd-119">Konfigurace LCM klienta o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="4cefd-119">Configure the pull client LCM</span></span>

<span data-ttu-id="4cefd-120">Provádění některý z níže uvedených příkladech vytvoří nový výstupní složka s názvem **PullClientConfigID** a umístí soubor MOF metaconfiguration existuje.</span><span class="sxs-lookup"><span data-stu-id="4cefd-120">Executing any of the examples below creates a new output folder named **PullClientConfigID** and puts a metaconfiguration MOF file there.</span></span> <span data-ttu-id="4cefd-121">V takovém případě bude mít název souboru MOF metaconfiguration `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="4cefd-121">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="4cefd-122">Chcete-li použít konfiguraci, zavolejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavit umístění souboru MOF metaconfiguration.</span><span class="sxs-lookup"><span data-stu-id="4cefd-122">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span> <span data-ttu-id="4cefd-123">Příklad:</span><span class="sxs-lookup"><span data-stu-id="4cefd-123">For example:</span></span>

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a><span data-ttu-id="4cefd-124">ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="4cefd-124">Configuration ID</span></span>

<span data-ttu-id="4cefd-125">V příkladech níže sad **ConfigurationID** vlastnost funkce LCM se **Guid** , který byl dříve vytvořili pro tento účel.</span><span class="sxs-lookup"><span data-stu-id="4cefd-125">The examples below sets the **ConfigurationID** property of the LCM to a **Guid** that had been previously created for this purpose.</span></span> <span data-ttu-id="4cefd-126">**ConfigurationID** je co LCM používá k nalezení odpovídající konfigurace na serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-126">The **ConfigurationID** is what the LCM uses to find the appropriate configuration on the pull server.</span></span> <span data-ttu-id="4cefd-127">Musí mít název konfiguračního souboru MOF na serveru vyžádané replikace `ConfigurationID.mof`, kde *ConfigurationID* je hodnota **ConfigurationID** vlastnost LCM cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="4cefd-127">The configuration MOF file on the pull server must be named `ConfigurationID.mof`, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="4cefd-128">Další informace najdete v části [publikovat konfigurace serveru vyžádaných replikací s (v4/v5)](publishConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="4cefd-128">For more information see [Publish Configurations to a Pull Server (v4/v5)](publishConfigs.md).</span></span>

<span data-ttu-id="4cefd-129">Můžete vytvořit náhodnou **Guid** pomocí příkladu níže nebo pomocí [nový identifikátor Guid](/powershell/module/microsoft.powershell.utility/new-guid) rutiny.</span><span class="sxs-lookup"><span data-stu-id="4cefd-129">You can create a random **Guid** using the example below, or by using the [New-Guid](/powershell/module/microsoft.powershell.utility/new-guid) cmdlet.</span></span>

```powershell
[System.Guid]::NewGuid()
```

<span data-ttu-id="4cefd-130">Další informace o používání **GUID** ve vašem prostředí, najdete v článku [plánování GUID](/powershell/dsc/secureserver#guids).</span><span class="sxs-lookup"><span data-stu-id="4cefd-130">For more information about using **Guids** in your environment, see [Plan for Guids](/powershell/dsc/secureserver#guids).</span></span>

## <a name="set-up-a-pull-client-to-download-configurations"></a><span data-ttu-id="4cefd-131">Při nastavování klienta o přijetí změn ke stažení konfigurace</span><span class="sxs-lookup"><span data-stu-id="4cefd-131">Set up a Pull Client to download Configurations</span></span>

<span data-ttu-id="4cefd-132">Každý klient musí být nakonfigurovaný v **o přijetí změn** režimu a adresu url serveru o přijetí změn jeho konfigurace se mají ukládat.</span><span class="sxs-lookup"><span data-stu-id="4cefd-132">Each client must be configured in **Pull** mode and given the pull server url where its configuration is stored.</span></span> <span data-ttu-id="4cefd-133">K tomuto účelu, budete muset nakonfigurovat místní Configuration Manageru (LCM) potřebné informace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-133">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span> <span data-ttu-id="4cefd-134">Konfigurace LCM, vytvoříte speciální typ konfigurace dekorován **DSCLocalConfigurationManager** atribut.</span><span class="sxs-lookup"><span data-stu-id="4cefd-134">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span> <span data-ttu-id="4cefd-135">Další informace týkající se konfigurace LCM v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="4cefd-135">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md).</span></span>

### <a name="http-dsc-pull-server"></a><span data-ttu-id="4cefd-136">HTTP Server s DSC o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="4cefd-136">HTTP DSC Pull Server</span></span>

<span data-ttu-id="4cefd-137">Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze serveru s názvem "CONTOSO-PullSrv".</span><span class="sxs-lookup"><span data-stu-id="4cefd-137">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv".</span></span>

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

<span data-ttu-id="4cefd-138">Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-138">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span> <span data-ttu-id="4cefd-139">**ServerUrl** Určuje adresu url DSC o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="4cefd-139">The **ServerUrl** specifies the url of the DSC Pull</span></span>

### <a name="smb-share"></a><span data-ttu-id="4cefd-140">Sdílené složky SMB</span><span class="sxs-lookup"><span data-stu-id="4cefd-140">SMB Share</span></span>

<span data-ttu-id="4cefd-141">Následující skript nakonfiguruje LCM o přijetí změn konfigurace ze sdílené složky SMB `\\SMBPullServer\Pull`.</span><span class="sxs-lookup"><span data-stu-id="4cefd-141">The following script configures the LCM to pull configurations from the SMB Share `\\SMBPullServer\Pull`.</span></span>

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

<span data-ttu-id="4cefd-142">Ve skriptu **ConfigurationRepositoryShare** bloku definuje serveru vyžádané replikace, který v tomto případě je právě do sdílené složky SMB.</span><span class="sxs-lookup"><span data-stu-id="4cefd-142">In the script, the **ConfigurationRepositoryShare** block defines the pull server, which in this case, is just an SMB share.</span></span>

## <a name="set-up-a-pull-client-to-download-resources"></a><span data-ttu-id="4cefd-143">Chcete-li stáhnout prostředky při nastavování klienta o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="4cefd-143">Set up a Pull Client to download Resources</span></span>

<span data-ttu-id="4cefd-144">Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat v konfiguraci LCM (podobně jako v předchozích příkladech), načítacího klienta přetáhne prostředky ze stejného umístění, načte její konfigurace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-144">If you specify only the **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous examples), the pull client will pull resources from the same location it retrieves its configurations.</span></span> <span data-ttu-id="4cefd-145">Můžete také zadat samostatné umístění pro prostředky.</span><span class="sxs-lookup"><span data-stu-id="4cefd-145">You can also specify separate locations for resources.</span></span> <span data-ttu-id="4cefd-146">Pokud chcete zadat umístění prostředků jako samostatný server, použijte **ResourceRepositoryWeb** bloku.</span><span class="sxs-lookup"><span data-stu-id="4cefd-146">To specify a resource location as a separate server, use the **ResourceRepositoryWeb** block.</span></span> <span data-ttu-id="4cefd-147">Pokud chcete zadat umístění prostředku jako sdílenou složku protokolu SMB, použijte **ResourceRepositoryShare** bloku.</span><span class="sxs-lookup"><span data-stu-id="4cefd-147">To specify a resource location as an SMB share, use the **ResourceRepositoryShare** block.</span></span>

> [!NOTE]
> <span data-ttu-id="4cefd-148">Můžete kombinovat **ConfigurationRepositoryWeb** s **ResourceRepositoryShare** nebo **ConfigurationRepositoryShare** s **ResourceRepositoryWeb** .</span><span class="sxs-lookup"><span data-stu-id="4cefd-148">You can combine **ConfigurationRepositoryWeb** with **ResourceRepositoryShare** or **ConfigurationRepositoryShare** with **ResourceRepositoryWeb**.</span></span> <span data-ttu-id="4cefd-149">Příklady nejsou zobrazeny níže.</span><span class="sxs-lookup"><span data-stu-id="4cefd-149">Examples of this are not shown below.</span></span>

### <a name="http-dsc-pull-server"></a><span data-ttu-id="4cefd-150">HTTP Server s DSC o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="4cefd-150">HTTP DSC Pull Server</span></span>

<span data-ttu-id="4cefd-151">Následující metaconfiguration nakonfiguruje klienta o přijetí změn zobrazíte jeho konfiguraci z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**.</span><span class="sxs-lookup"><span data-stu-id="4cefd-151">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**.</span></span>

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

### <a name="smb-share"></a><span data-ttu-id="4cefd-152">Sdílené složky SMB</span><span class="sxs-lookup"><span data-stu-id="4cefd-152">SMB Share</span></span>

<span data-ttu-id="4cefd-153">Následující příklad ukazuje metaconfiguration, který nastaví klienta o přijetí změn konfigurace ze sdílené složky SMB `\\SMBPullServer\Configurations`a prostředky ze sdílené složky SMB `\\SMBPullServer\Resources`.</span><span class="sxs-lookup"><span data-stu-id="4cefd-153">The following example shows a metaconfiguration that sets up a client to pull configurations from the SMB share `\\SMBPullServer\Configurations`, and resources from the SMB share `\\SMBPullServer\Resources`.</span></span>

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

#### <a name="automatically-download-resources-in-push-mode"></a><span data-ttu-id="4cefd-154">Automaticky stahovat prostředků v režimu Push</span><span class="sxs-lookup"><span data-stu-id="4cefd-154">Automatically download Resources in Push Mode</span></span>

<span data-ttu-id="4cefd-155">Od v Powershellu 5.0, klienty o přijetí změn můžete stáhnout moduly ze sdílené složky SMB, i když jsou nakonfigurované pro **Push** režimu.</span><span class="sxs-lookup"><span data-stu-id="4cefd-155">Beginning in PowerShell 5.0, your pull clients can download modules from an SMB share, even when they are configured for **Push** mode.</span></span> <span data-ttu-id="4cefd-156">To je zvláště užitečná v situacích, kdy nechcete k nastavení serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-156">This is especially useful in scenarios where you do not want to set up a Pull Server.</span></span> <span data-ttu-id="4cefd-157">**ResourceRepositoryShare** bloku lze použít bez zadání **ConfigurationRepositoryShare**.</span><span class="sxs-lookup"><span data-stu-id="4cefd-157">The **ResourceRepositoryShare** block can be used without specifying a **ConfigurationRepositoryShare**.</span></span> <span data-ttu-id="4cefd-158">Následující příklad ukazuje metaconfiguration, který nastaví kolekci klienta o přijetí změn prostředků ze sdílené složce SMB `\\SMBPullServer\Resources`.</span><span class="sxs-lookup"><span data-stu-id="4cefd-158">The following example shows a metaconfiguration that sets up a client to pull resources from an SMB Share `\\SMBPullServer\Resources`.</span></span> <span data-ttu-id="4cefd-159">Pokud je uzel **PUSHED** konfigurace, se automaticky stáhne všechny požadované prostředky ze sdílené složky zadané.</span><span class="sxs-lookup"><span data-stu-id="4cefd-159">When the Node is **PUSHED** a configuration, it will automatically download any required resources, from the share specified.</span></span>

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

## <a name="set-up-a-pull-client-to-report-status"></a><span data-ttu-id="4cefd-160">Při nastavování klienta o přijetí změn do sestav stavu</span><span class="sxs-lookup"><span data-stu-id="4cefd-160">Set up a Pull Client to report status</span></span>

<span data-ttu-id="4cefd-161">Ve výchozím nastavení nebude uzly odesílat sestavy do nakonfigurovaného serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="4cefd-161">By default, Nodes will not send reports to a configured Pull Server.</span></span> <span data-ttu-id="4cefd-162">Jeden načítacího serveru můžete použít pro konfigurace, prostředků a vytváření sestav, ale je nutné vytvořit **ReportRepositoryWeb** bloku k nastavení vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="4cefd-162">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>

### <a name="http-dsc-pull-server"></a><span data-ttu-id="4cefd-163">HTTP Server s DSC o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="4cefd-163">HTTP DSC Pull Server</span></span>

<span data-ttu-id="4cefd-164">Následující příklad ukazuje metaconfiguration, který nastaví klienta o přijetí změn konfigurace, prostředků a odeslat data, pro generování sestav o přijetí změn jeden server.</span><span class="sxs-lookup"><span data-stu-id="4cefd-164">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="4cefd-165">K určení serveru sestav, můžete použít **ReportRepositoryWeb** bloku.</span><span class="sxs-lookup"><span data-stu-id="4cefd-165">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span> <span data-ttu-id="4cefd-166">Server sestav nemůže být serveru SMB.</span><span class="sxs-lookup"><span data-stu-id="4cefd-166">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="4cefd-167">Následující metaconfiguration nakonfiguruje klienta o přijetí změn zobrazíte jeho konfiguraci z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**a k odeslání zprávy o stavu  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="4cefd-167">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

### <a name="smb-share"></a><span data-ttu-id="4cefd-168">Sdílené složky SMB</span><span class="sxs-lookup"><span data-stu-id="4cefd-168">SMB Share</span></span>

<span data-ttu-id="4cefd-169">Server sestav nemůže být sdílené složce SMB.</span><span class="sxs-lookup"><span data-stu-id="4cefd-169">A report server cannot be an SMB share.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cefd-170">Další kroky</span><span class="sxs-lookup"><span data-stu-id="4cefd-170">Next Steps</span></span>

<span data-ttu-id="4cefd-171">Po načítacího klienta nakonfigurovaný, můžete provést další kroky následující příručky:</span><span class="sxs-lookup"><span data-stu-id="4cefd-171">Once the pull client has been configured, you can use the following guides to perform the next steps:</span></span>

- [<span data-ttu-id="4cefd-172">Publikování na serveru vyžádané replikace (v4 nebo verze 5) konfigurace</span><span class="sxs-lookup"><span data-stu-id="4cefd-172">Publish Configurations to a Pull Server (v4/v5)</span></span>](publishConfigs.md)
- [<span data-ttu-id="4cefd-173">Balíček a prostředky nahrávání na serveru vyžádané replikace (v4)</span><span class="sxs-lookup"><span data-stu-id="4cefd-173">Package and Upload Resources to a Pull Server (v4)</span></span>](package-upload-resources.md)

## <a name="see-also"></a><span data-ttu-id="4cefd-174">Viz také</span><span class="sxs-lookup"><span data-stu-id="4cefd-174">See Also</span></span>

* [<span data-ttu-id="4cefd-175">Nastavení načítacího klienta s názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="4cefd-175">Setting up a pull client with configuration names</span></span>](pullClientConfigNames.md)

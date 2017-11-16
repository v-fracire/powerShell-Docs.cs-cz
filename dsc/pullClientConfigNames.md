---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Nastavení vyžadování klienta pomocí názvy konfigurace"
ms.openlocfilehash: 9bfcac87300d30a59b66e60ed24add32e2420e21
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a><span data-ttu-id="70979-103">Nastavení vyžadování klienta pomocí názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="70979-103">Setting up a pull client using configuration names</span></span>

> <span data-ttu-id="70979-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="70979-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="70979-105">Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadána adresa URL, kde může kontaktovat načítací server za účelem získání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="70979-105">Each target node has to be told to use pull mode and given the URL where it can contact the pull server to get configurations.</span></span>
<span data-ttu-id="70979-106">K tomuto účelu, budete muset nakonfigurovat místní Configuration Manager (LCM) nezbytné informace.</span><span class="sxs-lookup"><span data-stu-id="70979-106">To do this, you have to configure the Local Configuration Manager (LCM) with the necessary information.</span></span>
<span data-ttu-id="70979-107">Pokud chcete nakonfigurovat LCM, vytvoříte speciální typ konfigurace, označených pomocí **DSCLocalConfigurationManager** atribut.</span><span class="sxs-lookup"><span data-stu-id="70979-107">To configure the LCM, you create a special type of configuration, decorated with the **DSCLocalConfigurationManager** attribute.</span></span>
<span data-ttu-id="70979-108">Další informace o konfiguraci LCM najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="70979-108">For more information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

> <span data-ttu-id="70979-109">**Poznámka:**: Toto téma se týká PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="70979-109">**Note**: This topic applies to PowerShell 5.0.</span></span>
<span data-ttu-id="70979-110">Informace o nastavení klienta přijetí změn v prostředí PowerShell 4.0 najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0](pullClientConfigID4.md)</span><span class="sxs-lookup"><span data-stu-id="70979-110">For information on setting up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md)</span></span>

<span data-ttu-id="70979-111">Následující skript nakonfiguruje LCM pro vyžádání obsahu konfigurace ze serveru s názvem "CONTOSO-PullSrv":</span><span class="sxs-lookup"><span data-stu-id="70979-111">The following script configures the LCM to pull configurations from a server named "CONTOSO-PullSrv":</span></span>

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

<span data-ttu-id="70979-112">Ve skriptu **ConfigurationRepositoryWeb** bloku definuje serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="70979-112">In the script, the **ConfigurationRepositoryWeb** block defines the pull server.</span></span>
<span data-ttu-id="70979-113">**ServerURL** vlastnost určuje koncový bod pro vyžádání obsahu serveru.</span><span class="sxs-lookup"><span data-stu-id="70979-113">The **ServerURL** property specifies the endpoint for the pull server.</span></span>

<span data-ttu-id="70979-114">**RegistrationKey** vlastnost je sdílený klíč mezi všechny uzly klienta pro vyžádání obsahu server a tento server pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="70979-114">The **RegistrationKey** property is a shared key between all client nodes for a pull server and that pull server.</span></span>
<span data-ttu-id="70979-115">Stejné hodnota je uložena v souboru na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="70979-115">The same value is stored in a file on the pull server.</span></span>

<span data-ttu-id="70979-116">**ConfigurationNames** vlastnost je pole, které určuje názvy konfigurace určené pro klientský uzel.</span><span class="sxs-lookup"><span data-stu-id="70979-116">The **ConfigurationNames** property is an array that specifies the names of the configurations intended for the client node.</span></span>
<span data-ttu-id="70979-117">Na tomto serveru, MOF konfigurační soubor pro tento uzel klienta musí mít název *ConfigurationNames*MOF, kde *ConfigurationNames* odpovídá hodnotě **ConfigurationNames**  sadu v této metakonfiguraci vlastností.</span><span class="sxs-lookup"><span data-stu-id="70979-117">On the pull server, the configuration MOF file for this client node must be named *ConfigurationNames*.mof, where *ConfigurationNames* matches the value of the **ConfigurationNames** property you set in this metaconfiguration.</span></span>

><span data-ttu-id="70979-118">**Poznámka:** Pokud zadáte více než jednu hodnotu v **ConfigurationNames**, musíte zadat také **PartialConfiguration** bloků v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="70979-118">**Note:** If you specify more than one value in the **ConfigurationNames**, you must also specify **PartialConfiguration** blocks in your configuration.</span></span>
<span data-ttu-id="70979-119">Informace o částečné konfiguracích najdete v tématu [konfigurace požadovaného stavu prostředí PowerShell částečné konfigurace](partialConfigs.md).</span><span class="sxs-lookup"><span data-stu-id="70979-119">For information about partial configurations, see [PowerShell Desired State Configuration partial configurations](partialConfigs.md).</span></span>

<span data-ttu-id="70979-120">Po spuštění tohoto skriptu vytvoří nový výstupní složky s názvem **PullClientConfigNames** a vloží soubor MOF metakonfiguraci existuje.</span><span class="sxs-lookup"><span data-stu-id="70979-120">After this script runs, it creates a new output folder named **PullClientConfigNames** and puts a metaconfiguration MOF file there.</span></span>
<span data-ttu-id="70979-121">V takovém případě bude mít název souboru MOF metakonfiguraci `localhost.meta.mof`.</span><span class="sxs-lookup"><span data-stu-id="70979-121">In this case, the metaconfiguration MOF file will be named `localhost.meta.mof`.</span></span>

<span data-ttu-id="70979-122">Chcete-li použít konfiguraci, volejte **Set-DscLocalConfigurationManager** rutiny s **cesta** nastavte na umístění souboru MOF metakonfiguraci.</span><span class="sxs-lookup"><span data-stu-id="70979-122">To apply the configuration, call the **Set-DscLocalConfigurationManager** cmdlet, with the **Path** set to the location of the metaconfiguration MOF file.</span></span>

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> <span data-ttu-id="70979-123">**Poznámka:**: registrační kódy pracovat pouze s webovými servery vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="70979-123">**Note**: Registration keys work only with web pull servers.</span></span>
<span data-ttu-id="70979-124">Je nutné použít **ConfigurationID** se serverem SMB vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="70979-124">You must still use **ConfigurationID** with an SMB pull server.</span></span>
<span data-ttu-id="70979-125">Informace o konfiguraci serveru vyžádané replikace pomocí **ConfigurationID**, najdete v části [nastavení vyžadování klienta pomocí ID konfigurace](PullClientConfigNames.md)</span><span class="sxs-lookup"><span data-stu-id="70979-125">For information about configuring a pull server by using **ConfigurationID**, see [Setting up a pull client using configuration ID](PullClientConfigNames.md)</span></span>

## <a name="resource-and-report-servers"></a><span data-ttu-id="70979-126">Servery prostředků a sestavy</span><span class="sxs-lookup"><span data-stu-id="70979-126">Resource and report servers</span></span>

<span data-ttu-id="70979-127">Pokud zadáte pouze **ConfigurationRepositoryWeb** nebo **ConfigurationRepositoryShare** blokovat ve vaší konfiguraci LCM (jako v předchozím příkladu), klient pro vyžádání obsahu načte prostředky z Zadaný server, ale nebude odesílat zprávy do něj.</span><span class="sxs-lookup"><span data-stu-id="70979-127">If you specify only a **ConfigurationRepositoryWeb** or **ConfigurationRepositoryShare** block in your LCM configuration (as in the previous example), the pull client will pull resources from the specified server, but it will not send reports to it.</span></span>
<span data-ttu-id="70979-128">Jeden načítacího serveru můžete použít pro konfigurace, prostředky a vytváření sestav, ale je nutné vytvořit **ReportRepositoryWeb** blok k nastavení vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="70979-128">You can use a single pull server for configurations, resources, and reporting, but you have to create a **ReportRepositoryWeb** block to set up reporting.</span></span>
<span data-ttu-id="70979-129">Následující příklad ukazuje metakonfiguraci, který nastaví kolekci klienta k přijetí změn konfigurace a prostředky a odesílat data, pro vytváření sestav k jedné z vlastního serveru.</span><span class="sxs-lookup"><span data-stu-id="70979-129">The following example shows a metaconfiguration that sets up a client to pull configurations and resources, and send reporting data, to a single pull server.</span></span>

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

<span data-ttu-id="70979-130">Můžete také zadat servery různých vyžádání obsahu pro prostředky a vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="70979-130">You can also specify different pull servers for resources and reporting.</span></span>
<span data-ttu-id="70979-131">K určení serveru prostředků, můžete buď použít **ResourceRepositoryWeb** (pro webový server pro vyžádání obsahu) nebo **ResourceRepositoryShare** blok (pro vyžádání obsahu serveru SMB).</span><span class="sxs-lookup"><span data-stu-id="70979-131">To specify a resource server, you use either a **ResourceRepositoryWeb** (for a web pull server) or a **ResourceRepositoryShare** block (for an SMB pull server).</span></span>
<span data-ttu-id="70979-132">Chcete-li zadat server sestav, je použít **ReportRepositoryWeb** bloku.</span><span class="sxs-lookup"><span data-stu-id="70979-132">To specify a report server, you use a **ReportRepositoryWeb** block.</span></span>
<span data-ttu-id="70979-133">Server sestav nemůže být serveru SMB.</span><span class="sxs-lookup"><span data-stu-id="70979-133">A report server cannot be an SMB server.</span></span>
<span data-ttu-id="70979-134">Následující metakonfiguraci nakonfiguruje klienta vyžádání obsahu k získání jeho konfigurace z **CONTOSO-PullSrv** a jejích prostředcích z **CONTOSO-ResourceSrv**a k odeslání zprávy o stavu do  **CONTOSO-ReportSrv**:</span><span class="sxs-lookup"><span data-stu-id="70979-134">The following metaconfiguration configures a pull client to get its configurations from **CONTOSO-PullSrv** and its resources from **CONTOSO-ResourceSrv**, and to send status reports to **CONTOSO-ReportSrv**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="70979-135">Viz také</span><span class="sxs-lookup"><span data-stu-id="70979-135">See Also</span></span>

* [<span data-ttu-id="70979-136">Nastavení vyžadování klienta s ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="70979-136">Setting up a pull client with configuration ID</span></span>](PullClientConfigNames.md)
* [<span data-ttu-id="70979-137">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="70979-137">Setting up a DSC web pull server</span></span>](pullServer.md)


---
ms.date: 2017-10-16
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Přijetí konfigurace"
ms.openlocfilehash: 01294b85d33e147593299de8ecf46c027a69f7a3
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="enacting-configurations"></a><span data-ttu-id="f557c-103">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="f557c-103">Enacting configurations</span></span>

><span data-ttu-id="f557c-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f557c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="f557c-105">Existují dva způsoby, jak uplatní požadovaného stavu konfigurace (konfiguracích DSC Powershellu): push režim a režim vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="f557c-105">There are two ways to enact PowerShell Desired State Configuration (DSC) configurations: push mode and pull mode.</span></span>

## <a name="push-mode"></a><span data-ttu-id="f557c-106">Push režimu</span><span class="sxs-lookup"><span data-stu-id="f557c-106">Push mode</span></span>

<span data-ttu-id="f557c-107">![Režim push](images/pushModel.png "jak funguje režim push")</span><span class="sxs-lookup"><span data-stu-id="f557c-107">![Push mode](images/pushModel.png "How push mode works")</span></span>

<span data-ttu-id="f557c-108">Režim push odkazuje na uživatele aktivně použití konfigurace na cílový uzel voláním [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f557c-108">Push mode refers to a user actively applying a configuration to a target node by calling the [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) cmdlet.</span></span>

<span data-ttu-id="f557c-109">Po vytváření a kompilování konfigurace, můžete můžete uplatní je v režimu nabízení voláním [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) rutiny nastavení parametr - Path rutiny na cestu, kde se nachází v konfiguraci MOF.</span><span class="sxs-lookup"><span data-stu-id="f557c-109">After creating and compiling a configuration, you can enact it in push mode by calling the [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) cmdlet, setting the -Path parameter of the cmdlet to the path where the configuration MOF is located.</span></span>
<span data-ttu-id="f557c-110">Například, pokud se nachází v konfiguraci MOF `C:\DSC\Configurations\localhost.mof`, by ho použít k místnímu počítači pomocí následujícího příkazu: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span><span class="sxs-lookup"><span data-stu-id="f557c-110">For example, if the configuration MOF is located at `C:\DSC\Configurations\localhost.mof`, you would apply it to the local machine with the following command: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span></span>

> <span data-ttu-id="f557c-111">__Poznámka:__: ve výchozím nastavení spouští DSC konfigurace jako úlohu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="f557c-111">__Note__: By default, DSC runs a configuration as a background job.</span></span> <span data-ttu-id="f557c-112">Konfigurace běžet interaktivně, volání [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) s __-počkejte__ parametr.</span><span class="sxs-lookup"><span data-stu-id="f557c-112">To run the configuration interactively, call the [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) with the __-Wait__ parameter.</span></span>

## <a name="pull-mode"></a><span data-ttu-id="f557c-113">Režim pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="f557c-113">Pull mode</span></span>

<span data-ttu-id="f557c-114">![Režim pro vyžádání obsahu](images/pullModel.png "vyžádané funguje režim")</span><span class="sxs-lookup"><span data-stu-id="f557c-114">![Pull Mode](images/pullModel.png "How pull mode works")</span></span>

<span data-ttu-id="f557c-115">V režimu pro vyžádání obsahu klienti vyžádání obsahu umožňují získat jejich požadovaný stav konfigurace ze služby vzdálené vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="f557c-115">In pull mode, pull clients are configured to get their desired state configurations from a remote pull service.</span></span>
<span data-ttu-id="f557c-116">Podobně služba vyžádání obsahu je nastaven pro hostitele DSC služby a zřízená s prostředky, které jsou vyžadovány klienty pro vyžádání obsahu a konfigurace.</span><span class="sxs-lookup"><span data-stu-id="f557c-116">Likewise, the pull service has been set up to host the DSC service, and has been provisioned with the configurations and resources that are required by the pull clients.</span></span>
<span data-ttu-id="f557c-117">Každý z klientů vyžádání obsahu má plánovaná událost, která provádí kontrolu pravidelné dodržování předpisů v konfiguraci uzlu.</span><span class="sxs-lookup"><span data-stu-id="f557c-117">Each of the pull clients has a scheduled event that performs a periodic compliance check on the configuration of the node.</span></span>
<span data-ttu-id="f557c-118">Při prvním je aktivována událost, místní Configuration Manager (LCM) na vyžádání klient odešle požadavek službu vyžádání obsahu a získat konfiguraci zadanou v LCM.</span><span class="sxs-lookup"><span data-stu-id="f557c-118">When the event is triggered the first time, the Local Configuration Manager (LCM) on the pull client makes a request to the pull service to get the configuration specified in the LCM.</span></span>
<span data-ttu-id="f557c-119">Pokud tato konfigurace existuje ve službě vyžádání obsahu a předává počáteční ověřovacích kontrol, konfigurace se stáhne do klienta vyžádání obsahu, kde je pak provést pomocí LCM.</span><span class="sxs-lookup"><span data-stu-id="f557c-119">If that configuration exists on the pull service, and it passes initial validation checks, the configuration is downloaded to the pull client, where it is then executed by the LCM.</span></span>

<span data-ttu-id="f557c-120">LCM ověří, že klient je v souladu s konfigurací v pravidelných intervalech určeného **ConfigurationModeFrequencyMins** vlastnost LCM.</span><span class="sxs-lookup"><span data-stu-id="f557c-120">The LCM checks that the client is in compliance with the configuration at regular intervals specified by the **ConfigurationModeFrequencyMins** property of the LCM.</span></span>
<span data-ttu-id="f557c-121">LCM vyhledává aktualizované konfigurace ve službě vyžádání obsahu v pravidelných intervalech určeného **RefreshModeFrequency** vlastnost LCM.</span><span class="sxs-lookup"><span data-stu-id="f557c-121">The LCM checks for updated configurations on the pull service at regular intervals specified by the **RefreshModeFrequency** property of the LCM.</span></span>
<span data-ttu-id="f557c-122">Informace o konfiguraci LCM najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="f557c-122">For information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

<span data-ttu-id="f557c-123">Doporučené řešení pro hostování služby pro vyžádání obsahu, je Cloudová služba DSC, [Azure Automation](https://azure.microsoft.com/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="f557c-123">The recommended solution for hosting a Pull Service, is the DSC cloud service, [Azure Automation](https://azure.microsoft.com/services/automation/).</span></span>
<span data-ttu-id="f557c-124">To je hostovaná řešení poskytuje správu grafického rozhraní, vytváření sestav a centralizovanou správu.</span><span class="sxs-lookup"><span data-stu-id="f557c-124">This is hosted solution provides graphical management, reporting, and centralized administration.</span></span>

<span data-ttu-id="f557c-125">Další informace o nastavení vyžadování služby v systému Windows Server najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="f557c-125">For more information on setting up a Pull Service on Windows Server, see [Setting up a DSC web pull server](pullServer.md).</span></span>
<span data-ttu-id="f557c-126">Porozumět však, že tato implementace má omezené funkce a nevyžaduje některé integrace "provést sami".</span><span class="sxs-lookup"><span data-stu-id="f557c-126">Understand however, that this implementation has limited features and does require some "do it yourself" integration.</span></span>

<span data-ttu-id="f557c-127">Následující témata popisují vyžádání služby a klienti:</span><span class="sxs-lookup"><span data-stu-id="f557c-127">The following topics explain pull service and clients:</span></span>

- [<span data-ttu-id="f557c-128">Přehled služby Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="f557c-128">Azure Automation DSC Overview</span></span>](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="f557c-129">Nastavení vyžadování serveru SMB</span><span class="sxs-lookup"><span data-stu-id="f557c-129">Setting up an SMB pull server</span></span>](pullServerSMB.md)
- [<span data-ttu-id="f557c-130">Konfigurace klienta vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="f557c-130">Configuring a pull client</span></span>](pullClientConfigID.md)

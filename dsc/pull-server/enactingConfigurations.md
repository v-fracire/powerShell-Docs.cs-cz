---
ms.date: 10/16/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Přijetí konfigurace
ms.openlocfilehash: 4a6e7e511446ab27307683ad3d5676391e7c791c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404041"
---
# <a name="enacting-configurations"></a><span data-ttu-id="df735-103">Přijetí konfigurace</span><span class="sxs-lookup"><span data-stu-id="df735-103">Enacting configurations</span></span>

><span data-ttu-id="df735-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="df735-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="df735-105">Existují dva způsoby, jak přijmout konfigurace prostředí PowerShell Desired State Configuration (DSC): push a pull režimu.</span><span class="sxs-lookup"><span data-stu-id="df735-105">There are two ways to enact PowerShell Desired State Configuration (DSC) configurations: push mode and pull mode.</span></span>

## <a name="push-mode"></a><span data-ttu-id="df735-106">Režim nabízených oznámení</span><span class="sxs-lookup"><span data-stu-id="df735-106">Push mode</span></span>

<span data-ttu-id="df735-107">![Režimu nabízení](../images/pushModel.png "nabízená replikace funguje režim")</span><span class="sxs-lookup"><span data-stu-id="df735-107">![Push mode](../images/pushModel.png "How push mode works")</span></span>

<span data-ttu-id="df735-108">Režimu nabízení odkazuje na uživatele aktivně použití konfigurace k cílovému uzlu voláním [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="df735-108">Push mode refers to a user actively applying a configuration to a target node by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

<span data-ttu-id="df735-109">Po vytvoření a kompilace konfigurace, je můžete přijmout ho v režimu nabízení voláním [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny nastavení parametr - Path rutiny na cestu, kde se nachází konfigurační soubor MOF.</span><span class="sxs-lookup"><span data-stu-id="df735-109">After creating and compiling a configuration, you can enact it in push mode by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet, setting the -Path parameter of the cmdlet to the path where the configuration MOF is located.</span></span>
<span data-ttu-id="df735-110">Například, pokud se nachází v konfiguraci MOF `C:\DSC\Configurations\localhost.mof`, by ho použít v místním počítači pomocí následujícího příkazu: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span><span class="sxs-lookup"><span data-stu-id="df735-110">For example, if the configuration MOF is located at `C:\DSC\Configurations\localhost.mof`, you would apply it to the local machine with the following command: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span></span>

> <span data-ttu-id="df735-111">__Poznámka:__: Ve výchozím nastavení spouští DSC konfigurace jako úlohu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="df735-111">__Note__: By default, DSC runs a configuration as a background job.</span></span> <span data-ttu-id="df735-112">Chcete-li spustit konfiguraci interaktivně, zavolejte [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) s __– počkejte__ parametru.</span><span class="sxs-lookup"><span data-stu-id="df735-112">To run the configuration interactively, call the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) with the __-Wait__ parameter.</span></span>

## <a name="pull-mode"></a><span data-ttu-id="df735-113">Režim načítání</span><span class="sxs-lookup"><span data-stu-id="df735-113">Pull mode</span></span>

<span data-ttu-id="df735-114">![Režim načítání](../images/pullModel.png "vyžádané funguje režim")</span><span class="sxs-lookup"><span data-stu-id="df735-114">![Pull Mode](../images/pullModel.png "How pull mode works")</span></span>

<span data-ttu-id="df735-115">V režimu o přijetí změn jsou o přijetí změn klienti nakonfigurováni na získání jejich konfigurace požadovaného stavu ze služby vzdálené o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="df735-115">In pull mode, pull clients are configured to get their desired state configurations from a remote pull service.</span></span>
<span data-ttu-id="df735-116">Podobně službu přijetí změn je nastavený na hostitele DSC služby a zřízení s konfigurací a prostředků, které jsou vyžadovány klienty o přijetí změn.</span><span class="sxs-lookup"><span data-stu-id="df735-116">Likewise, the pull service has been set up to host the DSC service, and has been provisioned with the configurations and resources that are required by the pull clients.</span></span>
<span data-ttu-id="df735-117">Každá z klientů o přijetí změn obsahuje naplánované události, která provádí kontrolu dodržování předpisů pravidelné konfigurace uzlu.</span><span class="sxs-lookup"><span data-stu-id="df735-117">Each of the pull clients has a scheduled event that performs a periodic compliance check on the configuration of the node.</span></span>
<span data-ttu-id="df735-118">Když událost se aktivuje poprvé, místní Configuration Manageru (LCM) na straně klienta o přijetí změn učiní žádost vůči službě o přijetí změn a získat konfiguraci zadanou v LCM.</span><span class="sxs-lookup"><span data-stu-id="df735-118">When the event is triggered the first time, the Local Configuration Manager (LCM) on the pull client makes a request to the pull service to get the configuration specified in the LCM.</span></span>
<span data-ttu-id="df735-119">Pokud tuto konfiguraci existuje ve službě o přijetí změn, a předá počáteční ověřovacích kontrol, konfigurace se stáhne do klienta o přijetí změn, kde ji potom provádí LCM.</span><span class="sxs-lookup"><span data-stu-id="df735-119">If that configuration exists on the pull service, and it passes initial validation checks, the configuration is downloaded to the pull client, where it is then executed by the LCM.</span></span>

<span data-ttu-id="df735-120">LCM kontroluje, zda klient je v souladu s konfigurací v pravidelných intervalech, které jsou určené **ConfigurationModeFrequencyMins** vlastnost LCM.</span><span class="sxs-lookup"><span data-stu-id="df735-120">The LCM checks that the client is in compliance with the configuration at regular intervals specified by the **ConfigurationModeFrequencyMins** property of the LCM.</span></span>
<span data-ttu-id="df735-121">LCM kontroluje aktualizace konfigurace na službu přijetí změn v pravidelných intervalech, které jsou určené **RefreshModeFrequency** vlastnost LCM.</span><span class="sxs-lookup"><span data-stu-id="df735-121">The LCM checks for updated configurations on the pull service at regular intervals specified by the **RefreshModeFrequency** property of the LCM.</span></span>
<span data-ttu-id="df735-122">Informace o konfiguraci LCM najdete v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="df735-122">For information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md).</span></span>

<span data-ttu-id="df735-123">Doporučené řešení pro hostování služby o přijetí změn, je Cloudová služba DSC, [Azure Automation](https://azure.microsoft.com/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="df735-123">The recommended solution for hosting a Pull Service, is the DSC cloud service, [Azure Automation](https://azure.microsoft.com/services/automation/).</span></span>
<span data-ttu-id="df735-124">To je hostované řešení poskytuje správu grafického rozhraní, vytváření sestav a centralizovanou správu.</span><span class="sxs-lookup"><span data-stu-id="df735-124">This is hosted solution provides graphical management, reporting, and centralized administration.</span></span>

<span data-ttu-id="df735-125">Další informace o nastavení služby o přijetí změn ve Windows serveru najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="df735-125">For more information on setting up a Pull Service on Windows Server, see [Setting up a DSC web pull server](pullServer.md).</span></span>
<span data-ttu-id="df735-126">Seznamte se však, že tato implementace má omezené funkce a potřebuje k fungování integraci některé "to sami".</span><span class="sxs-lookup"><span data-stu-id="df735-126">Understand however, that this implementation has limited features and does require some "do it yourself" integration.</span></span>

<span data-ttu-id="df735-127">Následující témata popisují službu přijetí změn a klienti:</span><span class="sxs-lookup"><span data-stu-id="df735-127">The following topics explain pull service and clients:</span></span>

- [<span data-ttu-id="df735-128">Přehled Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="df735-128">Azure Automation DSC Overview</span></span>](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="df735-129">Nastavení serveru vyžádané replikace SMB</span><span class="sxs-lookup"><span data-stu-id="df735-129">Setting up an SMB pull server</span></span>](pullServerSMB.md)
- [<span data-ttu-id="df735-130">Konfigurace načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="df735-130">Configuring a pull client</span></span>](pullClientConfigID.md)
---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Přehled stavu konfigurace požadovaného prostředí Windows PowerShell"
ms.openlocfilehash: 1d6ba0b2fdb514e703ddad11adf4cdace5c001a9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="windows-powershell-desired-state-configuration-overview"></a><span data-ttu-id="336af-103">Přehled stavu konfigurace požadovaného prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="336af-103">Windows PowerShell Desired State Configuration Overview</span></span> 

> <span data-ttu-id="336af-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="336af-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="336af-105">DSC je platforma pro správu v prostředí PowerShell, které umožňuje spravovat vaše IT a vývoj infrastruktury s konfigurací jako kód.</span><span class="sxs-lookup"><span data-stu-id="336af-105">DSC is a management platform in PowerShell that enables you to manage your IT and development infrastructure with configuration as code.</span></span>

- <span data-ttu-id="336af-106">Přehled obchodní výhody používání DSC, najdete v tématu [potřeby přehled stavu konfigurace pro rozhodují](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="336af-106">For an overview of the business benefits of using DSC, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>
- <span data-ttu-id="336af-107">Přehled engineering výhody používání DSC, najdete v tématu [potřeby přehled stavu konfigurace pro techniky](DscForEngineers.md).</span><span class="sxs-lookup"><span data-stu-id="336af-107">For an overview of the engineering benefits of using DSC, see [Desired State Configuration Overview for Engineers](DscForEngineers.md).</span></span>
- <span data-ttu-id="336af-108">Chcete-li začít rychle používat DSC, přečtěte si téma [DSC úvodní](quickStart.md).</span><span class="sxs-lookup"><span data-stu-id="336af-108">To start using DSC quickly, see [DSC quick start](quickStart.md).</span></span>

## <a name="key-concepts"></a><span data-ttu-id="336af-109">Klíčové koncepty</span><span class="sxs-lookup"><span data-stu-id="336af-109">Key Concepts</span></span>

<span data-ttu-id="336af-110">DSC je deklarativní platforma používá pro konfiguraci, nasazení a Správa systémů.</span><span class="sxs-lookup"><span data-stu-id="336af-110">DSC is a declarative platform used for configuration, deployment, and management of systems.</span></span> <span data-ttu-id="336af-111">Obsahuje tři hlavní komponenty:</span><span class="sxs-lookup"><span data-stu-id="336af-111">It consists of three primary components:</span></span>

- <span data-ttu-id="336af-112">[Konfigurace](configurations.md) jsou deklarativní skriptů prostředí PowerShell, které definují a konfigurace instance prostředků.</span><span class="sxs-lookup"><span data-stu-id="336af-112">[Configurations](configurations.md) are declarative PowerShell scripts which define and configure instances of resources.</span></span>
    <span data-ttu-id="336af-113">Při spuštění konfigurace DSC (a prostředky volané konfigurace) bude jednoduše "bylo tak", zajistíte, že v systému existuje ve stavu nastíněny konfigurace.</span><span class="sxs-lookup"><span data-stu-id="336af-113">Upon running the configuration, DSC (and the resources being called by the configuration) will simply “make it so”, ensuring that the system exists in the state laid out by the configuration.</span></span> 
    <span data-ttu-id="336af-114">Konfigurace DSC se také idempotent: místní Configuration Manager (LCM) budou nadále počítače musí být nastaveny v ať stav konfigurace deklaruje.</span><span class="sxs-lookup"><span data-stu-id="336af-114">DSC configurations are also idempotent: the Local Configuration Manager (LCM) will continue to ensure that machines are configured in whatever state the configuration declares.</span></span>
- <span data-ttu-id="336af-115">[Prostředky](resources.md) jsou součástí DSC "bylo tak".</span><span class="sxs-lookup"><span data-stu-id="336af-115">[Resources](resources.md) are the "make it so" part of DSC.</span></span> <span data-ttu-id="336af-116">Obsahuje kód, který put a zachovat cíl konfigurace v zadaném stavu.</span><span class="sxs-lookup"><span data-stu-id="336af-116">They contain the code that put and keep the target of a configuration in the specified state.</span></span> 
    <span data-ttu-id="336af-117">Prostředky jsou umístěny v moduly Powershellu a je možné zapsat do modelu něco jako obecný jako soubor nebo procesu systému Windows nebo jako konkrétní jako server služby IIS nebo na virtuální počítač běží v Azure.</span><span class="sxs-lookup"><span data-stu-id="336af-117">Resources reside in PowerShell modules and can be written to model something as generic as a file or a Windows process, or as specific as an IIS server or a VM running in Azure.</span></span>
- <span data-ttu-id="336af-118">[Místní Configuration Manager (LCM)](metaConfig.md) je modulem, podle kterého DSC usnadňuje interakce mezi prostředky a konfigurace.</span><span class="sxs-lookup"><span data-stu-id="336af-118">The [Local Configuration Manager (LCM)](metaConfig.md) is the engine by which DSC facilitates the interaction between resources and configurations.</span></span> 
    <span data-ttu-id="336af-119">LCM pravidelně dotazuje systému pomocí tok řízení implementované prostředky k zajištění, že se zachová stav definovaný konfigurace.</span><span class="sxs-lookup"><span data-stu-id="336af-119">The LCM regularly polls the system using the control flow implemented by resources to ensure that the state defined by a configuration is maintained.</span></span> 
    <span data-ttu-id="336af-120">Pokud systém nemá dostatek stavu, LCM volá kód v prostředky usnadnit "," závislosti na konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="336af-120">If the system is out of state, the LCM makes calls to the code in resources to “make it so” according to the configuration.</span></span> 

## <a name="see-also"></a><span data-ttu-id="336af-121">Viz také</span><span class="sxs-lookup"><span data-stu-id="336af-121">See Also</span></span>

- [<span data-ttu-id="336af-122">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="336af-122">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="336af-123">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="336af-123">DSC Resources</span></span>](resources.md)
- [<span data-ttu-id="336af-124">Konfigurace správce místní konfigurace</span><span class="sxs-lookup"><span data-stu-id="336af-124">Configuring The Local Configuration Manager</span></span>](metaConfig.md)


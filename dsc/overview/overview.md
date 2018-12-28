---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředí Windows PowerShell Desired State Configuration – přehled
ms.openlocfilehash: 3e4f0afa17ab60bfa98f1b86b9830462a7c8e1cf
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403831"
---
# <a name="windows-powershell-desired-state-configuration-overview"></a><span data-ttu-id="8da3f-103">Prostředí Windows PowerShell Desired State Configuration – přehled</span><span class="sxs-lookup"><span data-stu-id="8da3f-103">Windows PowerShell Desired State Configuration Overview</span></span>

> <span data-ttu-id="8da3f-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="8da3f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="8da3f-105">DSC je platforma pro správu v prostředí PowerShell, které umožňuje spravovat vaši IT a rozvoj infrastruktury s konfigurací jako kód.</span><span class="sxs-lookup"><span data-stu-id="8da3f-105">DSC is a management platform in PowerShell that enables you to manage your IT and development infrastructure with configuration as code.</span></span>

- <span data-ttu-id="8da3f-106">Přehled o výhodách pro firmy pomocí DSC, naleznete v tématu [Desired State Configuration přehled pro pracovníky s rozhodovací pravomocí](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="8da3f-106">For an overview of the business benefits of using DSC, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>
- <span data-ttu-id="8da3f-107">Přehled technických výhody používání DSC, naleznete v tématu [Desired State Configuration přehled pro techniky](DscForEngineers.md).</span><span class="sxs-lookup"><span data-stu-id="8da3f-107">For an overview of the engineering benefits of using DSC, see [Desired State Configuration Overview for Engineers](DscForEngineers.md).</span></span>
- <span data-ttu-id="8da3f-108">Chcete-li začít rychle používat DSC, přečtěte si téma [rychlý start DSC](../quickstarts/website-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="8da3f-108">To start using DSC quickly, see [DSC quick start](../quickstarts/website-quickstart.md).</span></span>

## <a name="key-concepts"></a><span data-ttu-id="8da3f-109">Klíčové koncepty</span><span class="sxs-lookup"><span data-stu-id="8da3f-109">Key Concepts</span></span>

<span data-ttu-id="8da3f-110">DSC je deklarativní platforma sloužící ke konfiguraci, nasazení a správě systémů.</span><span class="sxs-lookup"><span data-stu-id="8da3f-110">DSC is a declarative platform used for configuration, deployment, and management of systems.</span></span> <span data-ttu-id="8da3f-111">Skládá se z tři hlavní komponenty:</span><span class="sxs-lookup"><span data-stu-id="8da3f-111">It consists of three primary components:</span></span>

- <span data-ttu-id="8da3f-112">[Konfigurace](../configurations/configurations.md) jsou deklarativní Powershellové skripty, které definují a konfigurace instancí prostředků.</span><span class="sxs-lookup"><span data-stu-id="8da3f-112">[Configurations](../configurations/configurations.md) are declarative PowerShell scripts which define and configure instances of resources.</span></span>
    <span data-ttu-id="8da3f-113">Při spouštění konfigurace (DSC a prostředky volané konfiguraci) bude jednoduše "aby tak", zajištění, že v systému existuje ve stavu rozloženy modulem konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8da3f-113">Upon running the configuration, DSC (and the resources being called by the configuration) will simply “make it so”, ensuring that the system exists in the state laid out by the configuration.</span></span>
    <span data-ttu-id="8da3f-114">Konfigurace DSC se také idempotentní: místní Configuration Manageru (LCM) budou i nadále zajistit, že počítače jsou konfigurované v cokoli, co stavu konfigurace deklaruje.</span><span class="sxs-lookup"><span data-stu-id="8da3f-114">DSC configurations are also idempotent: the Local Configuration Manager (LCM) will continue to ensure that machines are configured in whatever state the configuration declares.</span></span>
- <span data-ttu-id="8da3f-115">[Prostředky](../resources/resources.md) jsou součástí DSC "usnadňují tak".</span><span class="sxs-lookup"><span data-stu-id="8da3f-115">[Resources](../resources/resources.md) are the "make it so" part of DSC.</span></span> <span data-ttu-id="8da3f-116">Obsahující kód, který put a zachovat cílovou konfigurace v zadaném stavu.</span><span class="sxs-lookup"><span data-stu-id="8da3f-116">They contain the code that put and keep the target of a configuration in the specified state.</span></span>
    <span data-ttu-id="8da3f-117">Prostředky jsou umístěny v moduly Powershellu a je možné zapisovat na model něco jako obecný jako soubor nebo proces Windows nebo jako specifické jako server služby IIS nebo na virtuální počítač běží v Azure.</span><span class="sxs-lookup"><span data-stu-id="8da3f-117">Resources reside in PowerShell modules and can be written to model something as generic as a file or a Windows process, or as specific as an IIS server or a VM running in Azure.</span></span>
- <span data-ttu-id="8da3f-118">[Místní Configuration Manageru (LCM)](../managing-nodes/metaConfig.md) je modul, podle kterého DSC usnadňuje interakce mezi prostředky a konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8da3f-118">The [Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md) is the engine by which DSC facilitates the interaction between resources and configurations.</span></span>
    <span data-ttu-id="8da3f-119">LCM se pravidelně dotazuje systému použití toku řízení implementované prostředky, abyste zajistili zachování stavu určené konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8da3f-119">The LCM regularly polls the system using the control flow implemented by resources to ensure that the state defined by a configuration is maintained.</span></span>
    <span data-ttu-id="8da3f-120">Pokud systém nemá dostatek stavu, LCM provede volání do kódu na prostředcích, které "usnadňují tak" závislosti na konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="8da3f-120">If the system is out of state, the LCM makes calls to the code in resources to “make it so” according to the configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="8da3f-121">Viz také</span><span class="sxs-lookup"><span data-stu-id="8da3f-121">See Also</span></span>

- [<span data-ttu-id="8da3f-122">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="8da3f-122">DSC Configurations</span></span>](../configurations/configurations.md)
- [<span data-ttu-id="8da3f-123">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="8da3f-123">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="8da3f-124">Konfigurace Local Configuration Manageru</span><span class="sxs-lookup"><span data-stu-id="8da3f-124">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)

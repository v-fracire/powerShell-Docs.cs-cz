---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Přehled stavu konfigurace požadovaného prostředí Windows PowerShell
ms.openlocfilehash: 3f357ea11a388a05b73539a63e52e639ee906f68
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="windows-powershell-desired-state-configuration-overview"></a><span data-ttu-id="965e0-103">Přehled stavu konfigurace požadovaného prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="965e0-103">Windows PowerShell Desired State Configuration Overview</span></span>

> <span data-ttu-id="965e0-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="965e0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="965e0-105">DSC je platforma pro správu v prostředí PowerShell, které umožňuje spravovat vaše IT a vývoj infrastruktury s konfigurací jako kód.</span><span class="sxs-lookup"><span data-stu-id="965e0-105">DSC is a management platform in PowerShell that enables you to manage your IT and development infrastructure with configuration as code.</span></span>

- <span data-ttu-id="965e0-106">Přehled obchodní výhody používání DSC, najdete v tématu [potřeby přehled stavu konfigurace pro rozhodují](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="965e0-106">For an overview of the business benefits of using DSC, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>
- <span data-ttu-id="965e0-107">Přehled engineering výhody používání DSC, najdete v tématu [potřeby přehled stavu konfigurace pro techniky](DscForEngineers.md).</span><span class="sxs-lookup"><span data-stu-id="965e0-107">For an overview of the engineering benefits of using DSC, see [Desired State Configuration Overview for Engineers](DscForEngineers.md).</span></span>
- <span data-ttu-id="965e0-108">Chcete-li začít rychle používat DSC, přečtěte si téma [DSC úvodní](quickStart.md).</span><span class="sxs-lookup"><span data-stu-id="965e0-108">To start using DSC quickly, see [DSC quick start](quickStart.md).</span></span>

## <a name="key-concepts"></a><span data-ttu-id="965e0-109">Klíčové koncepty</span><span class="sxs-lookup"><span data-stu-id="965e0-109">Key Concepts</span></span>

<span data-ttu-id="965e0-110">DSC je deklarativní platforma používá pro konfiguraci, nasazení a Správa systémů.</span><span class="sxs-lookup"><span data-stu-id="965e0-110">DSC is a declarative platform used for configuration, deployment, and management of systems.</span></span> <span data-ttu-id="965e0-111">Obsahuje tři hlavní komponenty:</span><span class="sxs-lookup"><span data-stu-id="965e0-111">It consists of three primary components:</span></span>

- <span data-ttu-id="965e0-112">[Konfigurace](configurations.md) jsou deklarativní skriptů prostředí PowerShell, které definují a konfigurace instance prostředků.</span><span class="sxs-lookup"><span data-stu-id="965e0-112">[Configurations](configurations.md) are declarative PowerShell scripts which define and configure instances of resources.</span></span>
    <span data-ttu-id="965e0-113">Při spuštění konfigurace DSC (a prostředky volané konfigurace) bude jednoduše "bylo tak", zajistíte, že v systému existuje ve stavu nastíněny konfigurace.</span><span class="sxs-lookup"><span data-stu-id="965e0-113">Upon running the configuration, DSC (and the resources being called by the configuration) will simply “make it so”, ensuring that the system exists in the state laid out by the configuration.</span></span>
    <span data-ttu-id="965e0-114">Konfigurace DSC se také idempotent: místní Configuration Manager (LCM) budou nadále počítače musí být nastaveny v ať stav konfigurace deklaruje.</span><span class="sxs-lookup"><span data-stu-id="965e0-114">DSC configurations are also idempotent: the Local Configuration Manager (LCM) will continue to ensure that machines are configured in whatever state the configuration declares.</span></span>
- <span data-ttu-id="965e0-115">[Prostředky](resources.md) jsou součástí DSC "bylo tak".</span><span class="sxs-lookup"><span data-stu-id="965e0-115">[Resources](resources.md) are the "make it so" part of DSC.</span></span> <span data-ttu-id="965e0-116">Obsahuje kód, který put a zachovat cíl konfigurace v zadaném stavu.</span><span class="sxs-lookup"><span data-stu-id="965e0-116">They contain the code that put and keep the target of a configuration in the specified state.</span></span>
    <span data-ttu-id="965e0-117">Prostředky jsou umístěny v moduly Powershellu a je možné zapsat do modelu něco jako obecný jako soubor nebo procesu systému Windows nebo jako konkrétní jako server služby IIS nebo na virtuální počítač běží v Azure.</span><span class="sxs-lookup"><span data-stu-id="965e0-117">Resources reside in PowerShell modules and can be written to model something as generic as a file or a Windows process, or as specific as an IIS server or a VM running in Azure.</span></span>
- <span data-ttu-id="965e0-118">[Místní Configuration Manager (LCM)](metaConfig.md) je modulem, podle kterého DSC usnadňuje interakce mezi prostředky a konfigurace.</span><span class="sxs-lookup"><span data-stu-id="965e0-118">The [Local Configuration Manager (LCM)](metaConfig.md) is the engine by which DSC facilitates the interaction between resources and configurations.</span></span>
    <span data-ttu-id="965e0-119">LCM pravidelně dotazuje systému pomocí tok řízení implementované prostředky k zajištění, že se zachová stav definovaný konfigurace.</span><span class="sxs-lookup"><span data-stu-id="965e0-119">The LCM regularly polls the system using the control flow implemented by resources to ensure that the state defined by a configuration is maintained.</span></span>
    <span data-ttu-id="965e0-120">Pokud systém nemá dostatek stavu, LCM volá kód v prostředky usnadnit "," závislosti na konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="965e0-120">If the system is out of state, the LCM makes calls to the code in resources to “make it so” according to the configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="965e0-121">Viz také</span><span class="sxs-lookup"><span data-stu-id="965e0-121">See Also</span></span>

- [<span data-ttu-id="965e0-122">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="965e0-122">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="965e0-123">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="965e0-123">DSC Resources</span></span>](resources.md)
- [<span data-ttu-id="965e0-124">Konfigurace správce místní konfigurace</span><span class="sxs-lookup"><span data-stu-id="965e0-124">Configuring The Local Configuration Manager</span></span>](metaConfig.md)
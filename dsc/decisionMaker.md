---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Přehled platformy Desired State Configuration pro pracovníky s rozhodovací pravomocí
ms.openlocfilehash: 7c36aa5fadeab8bcb381f316288d102b5ce402e2
ms.sourcegitcommit: ac20e0faaa37142e9c6e4507a21df2f4a3fdbece
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/10/2018
ms.locfileid: "44339833"
---
# <a name="desired-state-configuration-overview-for-decision-makers"></a><span data-ttu-id="3e7bc-103">Přehled platformy Desired State Configuration pro pracovníky s rozhodovací pravomocí</span><span class="sxs-lookup"><span data-stu-id="3e7bc-103">Desired State Configuration Overview for Decision Makers</span></span>

<span data-ttu-id="3e7bc-104">Tento dokument popisuje výhodách pro firmy pomocí Windows Powershellu Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="3e7bc-104">This document describes the business benefits of using Windows PowerShell Desired State Configuration (DSC).</span></span> <span data-ttu-id="3e7bc-105">Nejedná se o technický průvodce.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-105">It is not a technical guide.</span></span>

## <a name="what-is-desired-state-configuration"></a><span data-ttu-id="3e7bc-106">Co je Desired State Configuration?</span><span class="sxs-lookup"><span data-stu-id="3e7bc-106">What Is Desired State Configuration?</span></span>

<span data-ttu-id="3e7bc-107">Prostředí PowerShell Desired State Configuration je platforma pro správu konfigurace integrovaný do Windows, která je založená na otevřených standardech.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-107">PowerShell Desired State Configuration is a configuration management platform built into Windows that is based on open standards.</span></span> <span data-ttu-id="3e7bc-108">DSC je dostatečně flexibilní, aby funkce konzistentně a spolehlivě v jednotlivých fázích životního cyklu nasazení (vývojové, testovací, předprodukčním prostředí, produkční), stejně jako při škálování na víc systémů.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-108">DSC is flexible enough to function reliably and consistently in each stage of the deployment lifecycle (development, test, pre-production, production), as well as during scale-out.</span></span>

<span data-ttu-id="3e7bc-109">DSC se soustředí kolem [konfigurace](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="3e7bc-109">DSC centers around [configurations](configurations.md).</span></span>
<span data-ttu-id="3e7bc-110">Konfigurace je snadné čtení dokumentu, který popisuje prostředí skládá z počítače ("uzly") s konkrétními vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-110">A configuration is an easy-to-read document that describes an environment made up of computers ("nodes") with specific characteristics.</span></span>
<span data-ttu-id="3e7bc-111">Tyto vlastnosti lze jednoduše zajištění, že se že konkrétní funkce Windows je povolený nebo komplexního, jako při nasazování služby SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-111">These characteristics can be as simple as ensuring a specific Windows feature is enabled or as complex as deploying SharePoint.</span></span>

<span data-ttu-id="3e7bc-112">DSC má také monitorování a vytváření sestav, integrované.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-112">DSC also has monitoring and reporting built in.</span></span>
<span data-ttu-id="3e7bc-113">Pokud již není kompatibilní s systému, DSC můžete vygenerovat výstrahu a Jednejte a opravte systém.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-113">If a system is no longer compliant, DSC can raise an alert and act to correct the system.</span></span>

## <a name="benefits-of-using-desired-state-configuration"></a><span data-ttu-id="3e7bc-114">Výhody použití Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="3e7bc-114">Benefits of Using Desired State Configuration</span></span>

<span data-ttu-id="3e7bc-115">Konfigurace jsou určeny k snadno přečíst, ukládat a aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-115">Configurations are designed to be easily read, stored, and updated.</span></span>
<span data-ttu-id="3e7bc-116">Konfigurace deklarace zařízení cílový stav by měl být v, místo psaní pokyny, jak uvést v tomto stavu.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-116">Configurations declare the state target devices should be in, instead of writing instructions for how to put them in that state.</span></span>
<span data-ttu-id="3e7bc-117">Díky tomu je mnohem méně nákladné na další, přijmout, implementaci a údržbu konfigurací pomocí DSC.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-117">This makes it much less costly to learn, adopt, implement, and maintain configuration through DSC.</span></span>

<span data-ttu-id="3e7bc-118">Vytvoření konfigurace znamená, že složité nasazení kroky se zaznamenají jako "jediný zdroj pravdivých informací" na jednom místě.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-118">Creating configurations means that complex deployment steps are captured as a "single source of truth" in a single location.</span></span>
<span data-ttu-id="3e7bc-119">Tím je mnohem méně náchylný opakované nasazení konkrétní sady počítačů.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-119">This makes repeated deployments of a specific set of machines much less error-prone.</span></span>
<span data-ttu-id="3e7bc-120">Zase provádět nasazení, rychlejší a spolehlivější umožňující rychlé vyřízení na komplexních nasazení.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-120">In turn, making deployments faster and more reliable which enables a quick turnaround on complex deployments.</span></span>

<span data-ttu-id="3e7bc-121">Konfigurace jsou také sdílet prostřednictvím [Galerie prostředí PowerShell](https://powershellgallery.com) znamená běžné scénáře a osvědčené postupy možná již existuje pro práci, kterou je potřeba udělat.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-121">Configurations are also shareable via the [PowerShell Gallery](https://powershellgallery.com) meaning common scenarios and best practices might already exist for the work that needs to be done.</span></span>


## <a name="desired-state-configuration-and-devops"></a><span data-ttu-id="3e7bc-122">Desired State Configuration a DevOps</span><span class="sxs-lookup"><span data-stu-id="3e7bc-122">Desired State Configuration and DevOps</span></span>

<span data-ttu-id="3e7bc-123">DSC byla navržena s [DevOps](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx) na paměti, kombinaci lidi, procesy a nástroje, které umožňují rychlé nasazení a iterace, zaměřuje na poskytování hodnoty koncovým uživatelům, ať už interní nebo externí.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-123">DSC was designed with [DevOps](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx) in mind, a combination of people, processes, and tools that allow for rapid deployment and iteration focused on delivering value to end users whether internal or external.</span></span>
<span data-ttu-id="3e7bc-124">S konfigurací jedné definice prostředí znamená, že vývojáři můžou kódování jejich požadavky na konfiguraci, zkontrolujte, že konfigurace do správy zdrojového kódu a týmy, které operace můžete snadno nasadit kód bez nutnosti přejít náchylné k chybě ruční procesy.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-124">Having a single configuration define an environment means that developers can encode their requirements into a configuration, check that configuration into source control, and operation teams can easily deploy code without having to go through error-prone manual processes.</span></span>

<span data-ttu-id="3e7bc-125">Konfigurace jsou také [řízené daty](configData.md), což usnadňuje ops tak může identifikovat a změnit prostředí bez zásahu pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-125">Configurations are also [data-driven](configData.md), which makes it easier for ops to identify and change environments without developer intervention.</span></span>

## <a name="desired-state-configuration-on--and-off-premises"></a><span data-ttu-id="3e7bc-126">Desired State Configuration a vypnout – místní</span><span class="sxs-lookup"><span data-stu-id="3e7bc-126">Desired State Configuration On- and Off-Premises</span></span>

<span data-ttu-id="3e7bc-127">DSC umožňuje spravovat místní a provozovaných nasazení.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-127">DSC can be used to manage both on-premise and off-premise deployments.</span></span>
<span data-ttu-id="3e7bc-128">Pro místní řešení má DSC [serveru vyžádané replikace](pullServer.md) , který umožňuje centralizovat správu počítačů a tvorba sestav o stavu.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-128">For on-premise solutions, DSC has a [pull server](pullServer.md) that can be used to centralize management of machines and report on their status.</span></span>
<span data-ttu-id="3e7bc-129">Cloudová řešení je DSC použít všude, kde je možné použít Windows.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-129">For cloud solutions, DSC is usable wherever Windows is usable.</span></span>
<span data-ttu-id="3e7bc-130">Existují také určité nabídky z Azure postavená na Desired State Configuration, jako například [Azure Automation](https://azure.microsoft.com/en-us/documentation/services/automation/), který centralizuje, vytvářet sestavy DSC.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-130">There are also specific offerings from Azure built on Desired State Configuration, such as [Azure Automation](https://azure.microsoft.com/en-us/documentation/services/automation/), which centralizes reporting of DSC.</span></span>

## <a name="dsc-and-compatibility"></a><span data-ttu-id="3e7bc-131">DSC a kompatibility</span><span class="sxs-lookup"><span data-stu-id="3e7bc-131">DSC and Compatibility</span></span>

<span data-ttu-id="3e7bc-132">Přestože DSC byla zavedena v systému Windows Server 2012 R2, je dostupná pro operační systémy nižší úrovně prostřednictvím balíček Windows Management Frameworku (WMF).</span><span class="sxs-lookup"><span data-stu-id="3e7bc-132">Although DSC was introduced in Windows Server 2012 R2, it is available for down-level operating systems via the Windows Management Framework (WMF) package.</span></span>
<span data-ttu-id="3e7bc-133">Další informace o WMF najdete na [domovské stránce Powershellu](/powershell/).</span><span class="sxs-lookup"><span data-stu-id="3e7bc-133">More information about the WMF can be found on the [PowerShell homepage](/powershell/).</span></span>

<span data-ttu-id="3e7bc-134">DSC můžete také použít ke správě systému Linux.</span><span class="sxs-lookup"><span data-stu-id="3e7bc-134">DSC can also be used to manage Linux.</span></span> <span data-ttu-id="3e7bc-135">Další informace najdete v tématu [Začínáme s DSC pro Linux](lnxGettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="3e7bc-135">For more information, see [Getting Started with DSC for Linux](lnxGettingStarted.md).</span></span>

---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutiny, psgallery, psget
title: Galerie prostředí PowerShell
ms.openlocfilehash: dc7e8dd7e4d96d8424a62cb3256c3164b63a3684
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/25/2018
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="87743-103">Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="87743-103">The PowerShell Gallery</span></span>

<span data-ttu-id="87743-104">Galerie prostředí PowerShell je centrálním úložištěm pro obsah prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87743-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="87743-105">V něm můžete najít užitečné moduly Powershellu obsahující příkazy prostředí PowerShell a prostředky konfigurace požadovaného stavu (DSC).</span><span class="sxs-lookup"><span data-stu-id="87743-105">In it, you can find useful PowerShell modules containing PowerShell commands and Desired State Configuration (DSC) resources.</span></span>
<span data-ttu-id="87743-106">Můžete také získat skripty prostředí PowerShell, některé z nich může obsahovat pracovních postupů prostředí PowerShell a které popisují sadu úloh a zadejte sekvencování pro tyto úlohy.</span><span class="sxs-lookup"><span data-stu-id="87743-106">You can also find PowerShell scripts, some of which may contain PowerShell workflows, and which outline a set of tasks and provide sequencing for those tasks.</span></span> <span data-ttu-id="87743-107">Některé z těchto položek vytvořené společností Microsoft a ostatní vytvořené komunitou prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87743-107">Some of these items are authored by Microsoft, and others are authored by the PowerShell community.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="87743-108">Přehled PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="87743-108">PowerShellGet Overview</span></span>

<span data-ttu-id="87743-109">Tento modul PowerShellGet obsahuje rutiny pro zjišťování, instalaci, aktualizaci a publikování prostředí PowerShell artefaktů, jako jsou moduly, prostředků DSC, funkce Role a skripty od [Galerie prostředí PowerShell](https://www.PowerShellGallery.com) a jiné privátní úložiště.</span><span class="sxs-lookup"><span data-stu-id="87743-109">The PowerShellGet module contains cmdlets for discovering, installing, updating and publishing PowerShell artifacts such as Modules, DSC Resources, Role Capabilities and Scripts from the [PowerShell Gallery](https://www.PowerShellGallery.com) and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="87743-110">Začínáme s Galerie</span><span class="sxs-lookup"><span data-stu-id="87743-110">Getting Started with the Gallery</span></span>

<span data-ttu-id="87743-111">Instalace položky z Galerie vyžaduje nejnovější verzi modulu PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="87743-111">Installing items from the Gallery requires the latest version of the PowerShellGet module.</span></span>
<span data-ttu-id="87743-112">V tématu [instalace PowerShellGet](installing-psget.md) úplné pokyny.</span><span class="sxs-lookup"><span data-stu-id="87743-112">See [Installing PowerShellGet](installing-psget.md) for complete instructions.</span></span>

<span data-ttu-id="87743-113">Podívejte se [Začínáme](getting-started.md) stránka Další informace o tom, jak pomocí příkazů PowerShellGet galerie.</span><span class="sxs-lookup"><span data-stu-id="87743-113">Check out the [Getting Started](getting-started.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="87743-114">Můžete také spouštět *Update-Help-modulu PowerShellGet* k instalaci místní Nápověda pro tyto příkazy.</span><span class="sxs-lookup"><span data-stu-id="87743-114">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="87743-115">Podporované operační systémy</span><span class="sxs-lookup"><span data-stu-id="87743-115">Supported Operating Systems</span></span>

<span data-ttu-id="87743-116">**PowerShellGet** module vyžaduje **prostředí Windows PowerShell 3.0 nebo novější**, nebo **základní prostředí PowerShell 6.0 nebo novější**.</span><span class="sxs-lookup"><span data-stu-id="87743-116">The **PowerShellGet** module requires **Windows PowerShell 3.0 or newer**, or **PowerShell Core 6.0 or newer**.</span></span>

<span data-ttu-id="87743-117">Vhodná verze **prostředí Windows PowerShell** je k dispozici pro tyto operační systémy:</span><span class="sxs-lookup"><span data-stu-id="87743-117">A suitable version of **Windows PowerShell** is available for these operating systems:</span></span>

- <span data-ttu-id="87743-118">Windows 10</span><span class="sxs-lookup"><span data-stu-id="87743-118">Windows 10</span></span>
- <span data-ttu-id="87743-119">Windows 8.1 Pro</span><span class="sxs-lookup"><span data-stu-id="87743-119">Windows 8.1 Pro</span></span>
- <span data-ttu-id="87743-120">Windows 8.1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="87743-120">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="87743-121">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="87743-121">Windows 7 SP1</span></span>
- <span data-ttu-id="87743-122">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="87743-122">Windows Server 2016</span></span>
- <span data-ttu-id="87743-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="87743-123">Windows Server 2012 R2</span></span>
- <span data-ttu-id="87743-124">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="87743-124">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="87743-125">**PowerShellGet** taky vyžaduje rozhraní .NET Framework 4.5 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="87743-125">**PowerShellGet** also requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="87743-126">Můžete nainstalovat rozhraní .NET Framework 4.5 nebo novější z [zde](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="87743-126">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>

<span data-ttu-id="87743-127">**Základní prostředí PowerShell** podporuje řada operačních systémů.</span><span class="sxs-lookup"><span data-stu-id="87743-127">**PowerShell Core** supports many operating systems.</span></span> <span data-ttu-id="87743-128">V tématu [v tomto článku](https://blogs.msdn.microsoft.com/powershell/2018/01/10/powershell-core-6-0-generally-available-ga-and-supported/) úplný seznam.</span><span class="sxs-lookup"><span data-stu-id="87743-128">See [this article](https://blogs.msdn.microsoft.com/powershell/2018/01/10/powershell-core-6-0-generally-available-ga-and-supported/) for a full list.</span></span>

<span data-ttu-id="87743-129">Mnoho modulů, které jsou hostované v galerii bude podporovat různé operační systémy nebo mají další požadavky.</span><span class="sxs-lookup"><span data-stu-id="87743-129">Many modules hosted in the gallery will support different OSes and have additional requirements.</span></span> <span data-ttu-id="87743-130">Naleznete v dokumentaci pro moduly pro další informace.</span><span class="sxs-lookup"><span data-stu-id="87743-130">Please refer to the documentation for the modules for more information.</span></span>

## <a name="got-a-question-have-feedback"></a><span data-ttu-id="87743-131">Máte dotaz?</span><span class="sxs-lookup"><span data-stu-id="87743-131">Got a question?</span></span> <span data-ttu-id="87743-132">Zpětné vazby máte?</span><span class="sxs-lookup"><span data-stu-id="87743-132">Have feedback?</span></span>

<span data-ttu-id="87743-133">Další informace o galerii prostředí PowerShell a PowerShellGet najdete v [Začínáme](getting-started.md) stránky.</span><span class="sxs-lookup"><span data-stu-id="87743-133">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](getting-started.md) page.</span></span> <span data-ttu-id="87743-134">Zadejte prosím zpětnou vazbu a sestava problémy s [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="87743-134">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>

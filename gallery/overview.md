---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutiny, psgallery, psget
title: Galerie prostředí PowerShell
ms.openlocfilehash: 65e0c427310ac20621109a6620e926a7894cf8f8
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="2dc99-103">Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dc99-103">The PowerShell Gallery</span></span>

<span data-ttu-id="2dc99-104">Galerie prostředí PowerShell je centrálním úložištěm pro obsah prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dc99-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="2dc99-105">V něm můžete najít užitečné moduly Powershellu obsahující příkazy prostředí PowerShell a prostředky konfigurace požadovaného stavu (DSC).</span><span class="sxs-lookup"><span data-stu-id="2dc99-105">In it, you can find useful PowerShell modules containing PowerShell commands and Desired State Configuration (DSC) resources.</span></span>
<span data-ttu-id="2dc99-106">Můžete také získat skripty prostředí PowerShell, některé z nich může obsahovat pracovních postupů prostředí PowerShell a které popisují sadu úloh a zadejte sekvencování pro tyto úlohy.</span><span class="sxs-lookup"><span data-stu-id="2dc99-106">You can also find PowerShell scripts, some of which may contain PowerShell workflows, and which outline a set of tasks and provide sequencing for those tasks.</span></span> <span data-ttu-id="2dc99-107">Některé z těchto položek vytvořené společností Microsoft a ostatní vytvořené komunitou prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dc99-107">Some of these items are authored by Microsoft, and others are authored by the PowerShell community.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="2dc99-108">Přehled PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="2dc99-108">PowerShellGet Overview</span></span>

<span data-ttu-id="2dc99-109">Tento modul PowerShellGet obsahuje rutiny pro zjišťování, instalaci, aktualizaci a publikování prostředí PowerShell artefaktů, jako jsou moduly, prostředků DSC, funkce Role a skripty od [Galerie prostředí PowerShell](https://www.PowerShellGallery.com) a jiné privátní úložiště.</span><span class="sxs-lookup"><span data-stu-id="2dc99-109">The PowerShellGet module contains cmdlets for discovering, installing, updating and publishing PowerShell artifacts such as Modules, DSC Resources, Role Capabilities and Scripts from the [PowerShell Gallery](https://www.PowerShellGallery.com) and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="2dc99-110">Začínáme s Galerie</span><span class="sxs-lookup"><span data-stu-id="2dc99-110">Getting Started with the Gallery</span></span>

<span data-ttu-id="2dc99-111">Instalace položky z Galerie vyžaduje nejnovější verzi modulu PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="2dc99-111">Installing items from the Gallery requires the latest version of the PowerShellGet module.</span></span>
<span data-ttu-id="2dc99-112">V tématu [instalace PowerShellGet](installing-psget.md) úplné pokyny.</span><span class="sxs-lookup"><span data-stu-id="2dc99-112">See [Installing PowerShellGet](installing-psget.md) for complete instructions.</span></span>

<span data-ttu-id="2dc99-113">Podívejte se [Začínáme](getting-started.md) stránka Další informace o tom, jak pomocí příkazů PowerShellGet galerie.</span><span class="sxs-lookup"><span data-stu-id="2dc99-113">Check out the [Getting Started](getting-started.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="2dc99-114">Můžete také spouštět *Update-Help-modulu PowerShellGet* k instalaci místní Nápověda pro tyto příkazy.</span><span class="sxs-lookup"><span data-stu-id="2dc99-114">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="2dc99-115">Podporované operační systémy</span><span class="sxs-lookup"><span data-stu-id="2dc99-115">Supported Operating Systems</span></span>

<span data-ttu-id="2dc99-116">**PowerShellGet** module vyžaduje **prostředí PowerShell 3.0 nebo novější**.</span><span class="sxs-lookup"><span data-stu-id="2dc99-116">The **PowerShellGet** module requires **PowerShell 3.0 or newer**.</span></span>

<span data-ttu-id="2dc99-117">Proto **PowerShellGet** vyžaduje jednu z následujících operačních systémů:</span><span class="sxs-lookup"><span data-stu-id="2dc99-117">Therefore, **PowerShellGet** requires one of the following operating systems:</span></span>

- <span data-ttu-id="2dc99-118">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2dc99-118">Windows 10</span></span>
- <span data-ttu-id="2dc99-119">Windows 8.1 Pro</span><span class="sxs-lookup"><span data-stu-id="2dc99-119">Windows 8.1 Pro</span></span>
- <span data-ttu-id="2dc99-120">Windows 8.1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="2dc99-120">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="2dc99-121">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="2dc99-121">Windows 7 SP1</span></span>
- <span data-ttu-id="2dc99-122">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2dc99-122">Windows Server 2016</span></span>
- <span data-ttu-id="2dc99-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2dc99-123">Windows Server 2012 R2</span></span>
- <span data-ttu-id="2dc99-124">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="2dc99-124">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="2dc99-125">**PowerShellGet** taky vyžaduje rozhraní .NET Framework 4.5 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="2dc99-125">**PowerShellGet** also requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="2dc99-126">Můžete nainstalovat rozhraní .NET Framework 4.5 nebo novější z [zde](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="2dc99-126">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>

## <a name="got-a-question-have-feedback"></a><span data-ttu-id="2dc99-127">Máte dotaz?</span><span class="sxs-lookup"><span data-stu-id="2dc99-127">Got a question?</span></span> <span data-ttu-id="2dc99-128">Zpětné vazby máte?</span><span class="sxs-lookup"><span data-stu-id="2dc99-128">Have feedback?</span></span>

<span data-ttu-id="2dc99-129">Další informace o galerii prostředí PowerShell a PowerShellGet najdete v [Začínáme](getting-started.md) stránky.</span><span class="sxs-lookup"><span data-stu-id="2dc99-129">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](getting-started.md) page.</span></span> <span data-ttu-id="2dc99-130">Zadejte prosím zpětnou vazbu a sestava problémy s [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="2dc99-130">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>
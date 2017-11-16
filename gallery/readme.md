---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery, psget"
title: "Galerie prostředí PowerShell"
ms.openlocfilehash: 9fe341e4b297764321f3b3f07caca8ef4b8b40e0
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/13/2017
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="08e84-103">Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="08e84-103">The PowerShell Gallery</span></span>

<span data-ttu-id="08e84-104">Galerie prostředí PowerShell je centrálním úložištěm pro obsah prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08e84-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="08e84-105">Nové příkazy prostředí PowerShell nebo prostředky konfigurace požadovaného stavu (DSC) najdete v galerii.</span><span class="sxs-lookup"><span data-stu-id="08e84-105">You can find new PowerShell commands or Desired State Configuration (DSC) resources in the Gallery.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="08e84-106">Přehled PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="08e84-106">PowerShellGet Overview</span></span>

<span data-ttu-id="08e84-107">Tento modul PowerShellGet obsahuje rutiny pro zjišťování, instalaci, aktualizaci a publikování prostředí PowerShell artefaktů, jako jsou moduly, prostředků DSC, funkce Role a skripty od [Galerie prostředí PowerShell](https://www.PowerShellGallery.com) a jiné privátní úložiště.</span><span class="sxs-lookup"><span data-stu-id="08e84-107">The PowerShellGet module contains cmdlets for discovering, installing, updating and publishing PowerShell artifacts such as Modules, DSC Resources, Role Capabilities and Scripts from the [PowerShell Gallery](https://www.PowerShellGallery.com) and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="08e84-108">Začínáme s Galerie</span><span class="sxs-lookup"><span data-stu-id="08e84-108">Getting Started with the Gallery</span></span>

<span data-ttu-id="08e84-109">Instalace položky z Galerie vyžaduje nejnovější verzi PowerShellGet modul, který je k dispozici v systému Windows 10, v systému Windows Management Framework (WMF) 5.0 nebo v instalačním programu na základě MSI (pro prostředí PowerShell 3 a 4).</span><span class="sxs-lookup"><span data-stu-id="08e84-109">Installing items from the Gallery requires the latest version of the PowerShellGet module, which is available in Windows 10, in Windows Management Framework (WMF) 5.0, or in the MSI-based installer (for PowerShell 3 and 4).</span></span>

- <span data-ttu-id="08e84-110">[**Získat Windows 10**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),</span><span class="sxs-lookup"><span data-stu-id="08e84-110">[**Get Windows 10**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),</span></span>
- <span data-ttu-id="08e84-111">[**Získat WMF 5.0**](http://go.microsoft.com/fwlink/?LinkId=398175), nebo</span><span class="sxs-lookup"><span data-stu-id="08e84-111">[**Get WMF 5.0**](http://go.microsoft.com/fwlink/?LinkId=398175), or</span></span>
- [<span data-ttu-id="08e84-112">**Získání Instalační služby MSI**</span><span class="sxs-lookup"><span data-stu-id="08e84-112">**Get MSI Installer**</span></span>](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

<span data-ttu-id="08e84-113">Na nejnovější [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) modul, můžete:</span><span class="sxs-lookup"><span data-stu-id="08e84-113">With the latest [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) module, you can:</span></span>

-   <span data-ttu-id="08e84-114">Vyhledávání pomocí položky v galerii s [najít modulu](https://go.microsoft.com/fwlink/?LinkId=821658) a [najít skriptu](https://go.microsoft.com/fwlink/?LinkId=822322)</span><span class="sxs-lookup"><span data-stu-id="08e84-114">Search through items in the Gallery with [Find-Module](https://go.microsoft.com/fwlink/?LinkId=821658) and [Find-Script](https://go.microsoft.com/fwlink/?LinkId=822322)</span></span>
-   <span data-ttu-id="08e84-115">Uložit položky do systému z galerie s [uložit modulu](https://go.microsoft.com/fwlink/?LinkId=821669) a [uložit skriptu](https://go.microsoft.com/fwlink/?LinkId=822334)</span><span class="sxs-lookup"><span data-stu-id="08e84-115">Save items to your system from the Gallery with [Save-Module](https://go.microsoft.com/fwlink/?LinkId=821669) and [Save-Script](https://go.microsoft.com/fwlink/?LinkId=822334)</span></span>
-   <span data-ttu-id="08e84-116">Nainstalujte položky z galerie s [instalace modulu](https://go.microsoft.com/fwlink/?LinkId=821663) a [instalační skript](https://go.microsoft.com/fwlink/?LinkId=822327)</span><span class="sxs-lookup"><span data-stu-id="08e84-116">Install items from the Gallery with [Install-Module](https://go.microsoft.com/fwlink/?LinkId=821663) and [Install-Script](https://go.microsoft.com/fwlink/?LinkId=822327)</span></span>
-   <span data-ttu-id="08e84-117">Nahrát položky do galerie s [publikovat modulu](https://go.microsoft.com/fwlink/?LinkId=821666) a [publikovat skriptu](https://go.microsoft.com/fwlink/?LinkId=822331)</span><span class="sxs-lookup"><span data-stu-id="08e84-117">Upload items to the Gallery with [Publish-Module](https://go.microsoft.com/fwlink/?LinkId=821666) and [Publish-Script](https://go.microsoft.com/fwlink/?LinkId=822331)</span></span>
-   <span data-ttu-id="08e84-118">Přidat vlastní úložiště s [PSRepository registrace](https://go.microsoft.com/fwlink/?LinkId=821668)</span><span class="sxs-lookup"><span data-stu-id="08e84-118">Add your own custom repository with [Register-PSRepository](https://go.microsoft.com/fwlink/?LinkId=821668)</span></span>

<span data-ttu-id="08e84-119">Podívejte se [Začínáme](psgallery/psgallery_gettingstarted.md) stránka Další informace o tom, jak pomocí příkazů PowerShellGet galerie.</span><span class="sxs-lookup"><span data-stu-id="08e84-119">Check out the [Getting Started](psgallery/psgallery_gettingstarted.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="08e84-120">Můžete také spouštět *Update-Help-modulu PowerShellGet* k instalaci místní Nápověda pro tyto příkazy.</span><span class="sxs-lookup"><span data-stu-id="08e84-120">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="08e84-121">Podporované operační systémy</span><span class="sxs-lookup"><span data-stu-id="08e84-121">Supported Operating Systems</span></span>

<span data-ttu-id="08e84-122">**PowerShellGet** module vyžaduje **prostředí PowerShell 3.0 nebo novější**.</span><span class="sxs-lookup"><span data-stu-id="08e84-122">The **PowerShellGet** module requires **PowerShell 3.0 or newer**.</span></span>

<span data-ttu-id="08e84-123">Proto **PowerShellGet** vyžaduje jednu z následujících operačních systémů:</span><span class="sxs-lookup"><span data-stu-id="08e84-123">Therefore, **PowerShellGet** requires one of the following operating systems:</span></span>

- <span data-ttu-id="08e84-124">Windows 10</span><span class="sxs-lookup"><span data-stu-id="08e84-124">Windows 10</span></span>
- <span data-ttu-id="08e84-125">Windows 8.1 Pro</span><span class="sxs-lookup"><span data-stu-id="08e84-125">Windows 8.1 Pro</span></span>
- <span data-ttu-id="08e84-126">Windows 8.1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="08e84-126">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="08e84-127">Windows 7 s aktualizací SP1</span><span class="sxs-lookup"><span data-stu-id="08e84-127">Windows 7 SP1</span></span>
- <span data-ttu-id="08e84-128">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="08e84-128">Windows Server 2016</span></span>
- <span data-ttu-id="08e84-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="08e84-129">Windows Server 2012 R2</span></span>
- <span data-ttu-id="08e84-130">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="08e84-130">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="08e84-131">**PowerShellGet** taky vyžaduje rozhraní .NET Framework 4.5 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="08e84-131">**PowerShellGet** also  requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="08e84-132">Můžete nainstalovat rozhraní .NET Framework 4.5 nebo novější z [zde](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="08e84-132">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx).</span></span>


## <a name="got-a-question-have-feedback"></a><span data-ttu-id="08e84-133">Máte dotaz?</span><span class="sxs-lookup"><span data-stu-id="08e84-133">Got a question?</span></span> <span data-ttu-id="08e84-134">Zpětné vazby máte?</span><span class="sxs-lookup"><span data-stu-id="08e84-134">Have feedback?</span></span>

<span data-ttu-id="08e84-135">Další informace o galerii prostředí PowerShell a PowerShellGet najdete v [Začínáme](psgallery/psgallery_gettingstarted.md) stránky.</span><span class="sxs-lookup"><span data-stu-id="08e84-135">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](psgallery/psgallery_gettingstarted.md) page.</span></span> <span data-ttu-id="08e84-136">Zadejte prosím zpětnou vazbu a sestava problémy s [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="08e84-136">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>


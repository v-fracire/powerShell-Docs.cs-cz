---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery, psget
title: Galerie prostředí PowerShell
ms.openlocfilehash: d3e3b9d8bb3d6cefd3a3bfe79b012bb1dc1d8a2d
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225614"
---
# <a name="the-powershell-gallery"></a><span data-ttu-id="9f527-103">Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f527-103">The PowerShell Gallery</span></span>

<span data-ttu-id="9f527-104">Galerie prostředí PowerShell je centrálním úložištěm pro obsah PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f527-104">The PowerShell Gallery is the central repository for PowerShell content.</span></span> <span data-ttu-id="9f527-105">V něm můžete najít užitečné moduly Powershellu, který obsahuje příkazy prostředí PowerShell a prostředky Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="9f527-105">In it, you can find useful PowerShell modules containing PowerShell commands and Desired State Configuration (DSC) resources.</span></span>
<span data-ttu-id="9f527-106">Můžete také vyhledat skriptů prostředí PowerShell, některé z nich může obsahovat pracovní postupy Powershellu a který popisují sadu úloh a zadejte klasifikace pro tyto úlohy.</span><span class="sxs-lookup"><span data-stu-id="9f527-106">You can also find PowerShell scripts, some of which may contain PowerShell workflows, and which outline a set of tasks and provide sequencing for those tasks.</span></span> <span data-ttu-id="9f527-107">Některé tyto balíčky jsou vytvořené microsoftem a jiné jsou vytvořené komunitou prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f527-107">Some of these packages are authored by Microsoft, and others are authored by the PowerShell community.</span></span>

## <a name="powershellget-overview"></a><span data-ttu-id="9f527-108">Přehled modulu PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="9f527-108">PowerShellGet Overview</span></span>

<span data-ttu-id="9f527-109">Modul PowerShellGet obsahuje rutiny pro zjišťování, instalaci, aktualizaci a publikovat balíčky prostředí PowerShell, které obsahují součásti, jako jsou moduly, prostředky DSC, funkce rolí a skriptů [Galerie prostředí PowerShell](https://www.PowerShellGallery.com)a jiných privátních úložišť.</span><span class="sxs-lookup"><span data-stu-id="9f527-109">The PowerShellGet module contains cmdlets for discovering, installing, updating and publishing PowerShell packages which contain artifacts such as Modules, DSC Resources, Role Capabilities and Scripts from the [PowerShell Gallery](https://www.PowerShellGallery.com) and other private repositories.</span></span>

## <a name="getting-started-with-the-gallery"></a><span data-ttu-id="9f527-110">Začínáme s Galerie</span><span class="sxs-lookup"><span data-stu-id="9f527-110">Getting Started with the Gallery</span></span>

<span data-ttu-id="9f527-111">Instalace balíčků z Galerie vyžaduje nejnovější verzi modulu PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="9f527-111">Installing packages from the Gallery requires the latest version of the PowerShellGet module.</span></span>
<span data-ttu-id="9f527-112">Zobrazit [instalace Správce balíčků PowerShellGet](installing-psget.md) úplné pokyny.</span><span class="sxs-lookup"><span data-stu-id="9f527-112">See [Installing PowerShellGet](installing-psget.md) for complete instructions.</span></span>

<span data-ttu-id="9f527-113">Podívejte se [Začínáme](getting-started.md) stránky pro další informace o tom, jak použití příkazů PowerShellGet pro galerii.</span><span class="sxs-lookup"><span data-stu-id="9f527-113">Check out the [Getting Started](getting-started.md) page for more information on how to use PowerShellGet commands with the Gallery.</span></span> <span data-ttu-id="9f527-114">Můžete také spustit *Update-Help-Module PowerShellGet* nainstalovat místní nápovědu pro tyto příkazy.</span><span class="sxs-lookup"><span data-stu-id="9f527-114">You can also run *Update-Help -Module PowerShellGet* to install local help for these commands.</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="9f527-115">Podporované operační systémy</span><span class="sxs-lookup"><span data-stu-id="9f527-115">Supported Operating Systems</span></span>

<span data-ttu-id="9f527-116">**PowerShellGet** modul vyžaduje **prostředí Windows PowerShell 3.0 nebo novější**, nebo **PowerShell Core 6.0 nebo novější**.</span><span class="sxs-lookup"><span data-stu-id="9f527-116">The **PowerShellGet** module requires **Windows PowerShell 3.0 or newer**, or **PowerShell Core 6.0 or newer**.</span></span>

<span data-ttu-id="9f527-117">Vhodnou verzi **prostředí Windows PowerShell** je k dispozici pro tyto operační systémy:</span><span class="sxs-lookup"><span data-stu-id="9f527-117">A suitable version of **Windows PowerShell** is available for these operating systems:</span></span>

- <span data-ttu-id="9f527-118">Windows 10</span><span class="sxs-lookup"><span data-stu-id="9f527-118">Windows 10</span></span>
- <span data-ttu-id="9f527-119">Windows 8.1 Pro</span><span class="sxs-lookup"><span data-stu-id="9f527-119">Windows 8.1 Pro</span></span>
- <span data-ttu-id="9f527-120">Windows 8.1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="9f527-120">Windows 8.1 Enterprise</span></span>
- <span data-ttu-id="9f527-121">Windows 7 SP1</span><span class="sxs-lookup"><span data-stu-id="9f527-121">Windows 7 SP1</span></span>
- <span data-ttu-id="9f527-122">Windows Server. 2019</span><span class="sxs-lookup"><span data-stu-id="9f527-122">Windows Server 2019</span></span>
- <span data-ttu-id="9f527-123">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9f527-123">Windows Server 2016</span></span>
- <span data-ttu-id="9f527-124">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="9f527-124">Windows Server 2012 R2</span></span>
- <span data-ttu-id="9f527-125">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="9f527-125">Windows Server 2008 R2 SP1</span></span>

<span data-ttu-id="9f527-126">**Správce balíčků PowerShellGet** vyžaduje rozhraní .NET Framework 4.5 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="9f527-126">**PowerShellGet** requires .NET Framework 4.5 or above.</span></span> <span data-ttu-id="9f527-127">Můžete nainstalovat rozhraní .NET Framework 4.5 nebo novější z [tady](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f527-127">You can install .NET Framework 4.5 or above from [here](https://msdn.microsoft.com/library/5a4x27ek.aspx).</span></span>

<span data-ttu-id="9f527-128">Protože **PowerShell Core** je multiplatformní a, znamená, že funguje ve Windows, Linuxu a MacOS, které také zajišťují **PowerShellGet** dostupná v těchto systémech.</span><span class="sxs-lookup"><span data-stu-id="9f527-128">Since **PowerShell Core** is cross-platform and that means it works on Windows, Linux and MacOS, that also makes **PowerShellGet** available on those systems.</span></span> <span data-ttu-id="9f527-129">Úplný seznam systémů, které podporuje **PowerShell Core** naleznete v tématu [instalace prostředí PowerShell](/powershell/scripting/setup/installing-powershell).</span><span class="sxs-lookup"><span data-stu-id="9f527-129">For a full list of systems supported by **PowerShell Core** see [Installing PowerShell](/powershell/scripting/setup/installing-powershell).</span></span>

<span data-ttu-id="9f527-130">Mnoho modulů, které jsou hostované v galerii se podporují různé operační systémy a mají další požadavky.</span><span class="sxs-lookup"><span data-stu-id="9f527-130">Many modules hosted in the gallery will support different OSes and have additional requirements.</span></span> <span data-ttu-id="9f527-131">Najdete v dokumentaci pro moduly pro další informace.</span><span class="sxs-lookup"><span data-stu-id="9f527-131">Please refer to the documentation for the modules for more information.</span></span>

## <a name="got-a-question-have-feedback"></a><span data-ttu-id="9f527-132">Máte dotaz?</span><span class="sxs-lookup"><span data-stu-id="9f527-132">Got a question?</span></span> <span data-ttu-id="9f527-133">Podněty?</span><span class="sxs-lookup"><span data-stu-id="9f527-133">Have feedback?</span></span>

<span data-ttu-id="9f527-134">Další informace o galerii prostředí PowerShell a Správce balíčků PowerShellGet najdete v [Začínáme](getting-started.md) stránky.</span><span class="sxs-lookup"><span data-stu-id="9f527-134">More information about the PowerShell Gallery and PowerShellGet can be found in the [Getting Started](getting-started.md) page.</span></span> <span data-ttu-id="9f527-135">Poskytněte prosím zpětnou vazbu a sestavy problémů pomocí [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span><span class="sxs-lookup"><span data-stu-id="9f527-135">Please provide feedback and report issues using [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).</span></span>

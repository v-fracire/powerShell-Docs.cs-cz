---
ms.date: 12/11/2018
contributor: JKeithB, SydneyhSmith
keywords: Galerie prostředí powershell, rutina, psgallery
title: Balíčky s kompatibilní operační systém nebo edice Powershellu
ms.openlocfilehash: 8230866561d3021379a48cc2c83fb4104a4058c1
ms.sourcegitcommit: d396d0e4cfe3d279f399c17e7337380a31d373ac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2018
ms.locfileid: "53747700"
---
# <a name="packages-with-compatible-powershell-editions-or-operating-systems"></a><span data-ttu-id="f7f5a-103">Balíčky s kompatibilní edice Powershellu nebo operační systémy</span><span class="sxs-lookup"><span data-stu-id="f7f5a-103">Packages with compatible PowerShell Editions or Operating Systems</span></span>

<span data-ttu-id="f7f5a-104">Od verze 5.1, prostředí PowerShell je k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibility platformy.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibilities.</span></span>

## <a name="searching-by-powershell-edition"></a><span data-ttu-id="f7f5a-105">Vyhledávání podle edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="f7f5a-105">Searching by PowerShell Edition</span></span> 
<span data-ttu-id="f7f5a-106">Edice powershellu jsou:</span><span class="sxs-lookup"><span data-stu-id="f7f5a-106">The two editions of Powershell are:</span></span>
- <span data-ttu-id="f7f5a-107">**Desktop Edition:** Založený na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na plných edicích Windows, jako je jádro serveru a Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-107">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="f7f5a-108">**Core Edition:** Založená na prostředí .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na edicích Windows, jako je Nano Server a Windows IoT nízké nároky.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-108">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

### <a name="powershell-gallery-allows-you-to-filter-packages-compatible-for-specific-powershell-editions"></a><span data-ttu-id="f7f5a-109">Galerie prostředí PowerShell vám umožní filtrovat kompatibilní balíčků pro konkrétní edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="f7f5a-109">PowerShell Gallery allows you to filter packages compatible for specific PowerShell Editions</span></span>

<span data-ttu-id="f7f5a-110">Pokud balíček nemá kompatibilní PSEditions zadán, jsou uvedeny jako součást 'Edice Powershellu' ve stránce balíček pro zobrazení a také ve výsledcích balíčky.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-110">If a package has compatible PSEditions specified, they are listed as part of 'PowerShell Editions' in the package display page and also in packages results.</span></span>
<span data-ttu-id="f7f5a-111">Můžete také vyhledat kompatibilní balíčků pomocí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-111">You can also search for compatible packages using PowerShell.</span></span>

![Položka zobrazení stránky s PSEditions](../../Images/packagedisplaypagewithpseditions.PNG)

### <a name="search-for-packages-in-the-gallery-ui-that-work-on-powershell-core"></a><span data-ttu-id="f7f5a-113">Vyhledat balíčky v galerii uživatelského rozhraní, které fungují v prostředí PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="f7f5a-113">Search for packages in the gallery UI that work on PowerShell Core</span></span>

<span data-ttu-id="f7f5a-114">Použití značek: "PSEdition_Desktop" a značky: "PSEdition_Core" filtrům balíčky v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-114">Use Tags:"PSEdition_Desktop" and Tags:"PSEdition_Core" to filters the packages on PowerShell Gallery.</span></span>

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a><span data-ttu-id="f7f5a-115">Použití značek: "PSEdition_Core" k vyhledání položek, které jsou kompatibilní s PowerShell Core Edition.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-115">Use Tags:"PSEdition_Core" to search items compatible with PowerShell Core Edition.</span></span>

![Výsledky hledání pro položky, které jsou kompatibilní s Core PSEdition](../../Images/searchresultswithpseditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a><span data-ttu-id="f7f5a-117">Použití značek: "PSEdition_Desktop" k vyhledání položek, které jsou kompatibilní s Powershellu Desktop Edition.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-117">Use Tags:"PSEdition_Desktop" to search items compatible with PowerShell Desktop Edition.</span></span>

![Výsledky hledání pro položky, které jsou kompatibilní s Desktop PSEdition](../../Images/searchresultswithpseditionsdesktop.PNG)

### <a name="search-for-packages-to-find-compatible-editions-using-powershell"></a><span data-ttu-id="f7f5a-119">Hledat balíčky a najděte kompatibilní edice powershellu</span><span class="sxs-lookup"><span data-stu-id="f7f5a-119">Search for packages to find compatible editions using PowerShell</span></span>
<span data-ttu-id="f7f5a-120">Můžete zadat značky, chcete-li filtrovat edice Powershellu a operačního systému.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-120">You can specify tags to filter for the PowerShell edition and OS.</span></span> <span data-ttu-id="f7f5a-121">Můžete použít `Find-Package` zadáním rutiny `-Tag` parametr k určení edition (a operačního systému) cílíte.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-121">You use the `Find-Package` cmdlet specifying the `-Tag` parameter to specify the edition (and OS) you are targeting.</span></span>
<span data-ttu-id="f7f5a-122">Nějak tak:</span><span class="sxs-lookup"><span data-stu-id="f7f5a-122">Like this:</span></span>

```powershell
# Find modules compatible with PowerShell Core:
Find-Module -Tag PSEdition_Core

# Find modules compatible with PowerShell Core on Linux:
Find-Module -Tag PSEdition_Core, Linux
```

## <a name="searching-by-operating-system"></a><span data-ttu-id="f7f5a-123">Hledání podle operačního systému</span><span class="sxs-lookup"><span data-stu-id="f7f5a-123">Searching by Operating System</span></span> 

<span data-ttu-id="f7f5a-124">PowerShell Core je k dispozici pro Windows, Linux a MacOS, mohou být balíčky v galerii navrženy pro libovolnou kombinaci těchto operačních systémů.</span><span class="sxs-lookup"><span data-stu-id="f7f5a-124">Since PowerShell Core is available for Windows, Linux, and MacOS, packages in the Gallery may be designed for any combination of these operating systems.</span></span> <span data-ttu-id="f7f5a-125">V galerii uživatelského rozhraní pomocí následujících značek searchs najít balíčků označené podle operačního systému:</span><span class="sxs-lookup"><span data-stu-id="f7f5a-125">In the gallery UI use the following searchs tags to find packages tagged by operating system:</span></span>

- <span data-ttu-id="f7f5a-126">Značky: "Windows"</span><span class="sxs-lookup"><span data-stu-id="f7f5a-126">Tags: "Windows"</span></span>
- <span data-ttu-id="f7f5a-127">Značky: "Linux"</span><span class="sxs-lookup"><span data-stu-id="f7f5a-127">Tags: "Linux"</span></span>
- <span data-ttu-id="f7f5a-128">Značky: "MacOS"</span><span class="sxs-lookup"><span data-stu-id="f7f5a-128">Tags: "MacOS"</span></span> 

<span data-ttu-id="f7f5a-129">Určíte tyto značky na `Find-Module` (a další rutiny v modulu PowerShellGet) tímto způsobem:</span><span class="sxs-lookup"><span data-stu-id="f7f5a-129">You can specify these tags on `Find-Module` (and other cmdlets in the PowerShellGet module), like this:</span></span>

```powershell
# Find Modules compatible with Windows
Find-Module -Tag Linux
```

## <a name="searching-for-multiple-compatibilities"></a><span data-ttu-id="f7f5a-130">Vyhledávání pro více kompatibility</span><span class="sxs-lookup"><span data-stu-id="f7f5a-130">Searching for Multiple Compatibilities</span></span>

<span data-ttu-id="f7f5a-131">Můžete vyhledat balíček, který má více kompatibility pomocí syntaxe:</span><span class="sxs-lookup"><span data-stu-id="f7f5a-131">You can look for a package that has multiple compatibilities by using the syntax:</span></span> 

<span data-ttu-id="f7f5a-132">Značky: "Compatibility1" "Compatibility2"</span><span class="sxs-lookup"><span data-stu-id="f7f5a-132">Tags: "Compatibility1" "Compatibility2"</span></span> 

<span data-ttu-id="f7f5a-133">Například pokud chcete pro balíček díky PowerShell Core, která běží na počítačích Moje Windows i Linuxem, použijte vyhledávací značky:</span><span class="sxs-lookup"><span data-stu-id="f7f5a-133">For example, if you are looking for a package with PowerShell Core Compatibility that runs on both my Windows and Linux machines, use the search tags:</span></span>

<span data-ttu-id="f7f5a-134">Značky: "PSEdition_Core" "Windows" "Linux"</span><span class="sxs-lookup"><span data-stu-id="f7f5a-134">Tags: "PSEdition_Core" "Windows" "Linux"</span></span> 

<span data-ttu-id="f7f5a-135">Hledání s použitím prostředí PowerShell, můžete použít `Find-Module` (a další rutiny v modulu PowerShellGet) tímto způsobem:</span><span class="sxs-lookup"><span data-stu-id="f7f5a-135">To search using PowerShell, you can use the `Find-Module` (and the other cmdlets in the PowerShellGet module), like this:</span></span>

```powewrshell
# Find scripts compatible with PowerShell Core, Windows, and Linux
Find-Script -Tag PSEdition_Core,Linux,Windows

# Find modules compatible with PowerSHellCore and MacOS
Find-Module -Tag PSEdition_Core,MacOS
```

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a><span data-ttu-id="f7f5a-136">Další informace o vytváření a hledání balíčky s kompatibilní edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="f7f5a-136">More details on authoring and finding the packages with compatible PowerShell Editions</span></span>

- [<span data-ttu-id="f7f5a-137">Moduly s PSEditions</span><span class="sxs-lookup"><span data-stu-id="f7f5a-137">Modules with PSEditions</span></span>](../../concepts/module-psedition-support.md)
- [<span data-ttu-id="f7f5a-138">Skripty s PSEditions</span><span class="sxs-lookup"><span data-stu-id="f7f5a-138">Scripts with PSEditions</span></span>](../../concepts/script-psedition-support.md)

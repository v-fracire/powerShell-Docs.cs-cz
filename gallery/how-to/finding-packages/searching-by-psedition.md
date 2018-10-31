---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Balíčky s kompatibilní edice Powershellu
ms.openlocfilehash: e16cfb0ee30e344c9399bec2985baafc5a252fd7
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004012"
---
# <a name="packages-with-compatible-powershell-editions"></a><span data-ttu-id="69332-103">Balíčky s kompatibilní edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="69332-103">Packages with compatible PowerShell Editions</span></span>

<span data-ttu-id="69332-104">Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.</span><span class="sxs-lookup"><span data-stu-id="69332-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="69332-105">**Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="69332-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="69332-106">**Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="69332-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-packages-compatible-for-specific-powershell-editions"></a><span data-ttu-id="69332-107">Extrahuje metadata podporované PSEditions Galerie prostředí PowerShell a umožňuje filtry balíčky kompatibilní pro konkrétní edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="69332-107">PowerShell Gallery extracts supported PSEditions metadata and allows you to filters the packages compatible for specific PowerShell Editions</span></span>

<span data-ttu-id="69332-108">Pokud balíček nemá kompatibilní PSEditions zadán, budou uvedené jako součást 'Edice Powershellu' ve stránce balíček pro zobrazení a také ve výsledcích balíčky.</span><span class="sxs-lookup"><span data-stu-id="69332-108">If a package has compatible PSEditions specified, they will be listed as part of 'PowerShell Editions' in the package display page and also in packages results.</span></span>

![Položka zobrazení stránky s PSEditions](../../Images/manual_package_download.png)

## <a name="search-for-packages-in-the-gallery-ui-which-works-on-powershellcore"></a><span data-ttu-id="69332-110">Vyhledat balíčky v galerii uživatelského rozhraní, který pracuje na PowerShellCore</span><span class="sxs-lookup"><span data-stu-id="69332-110">Search for packages in the gallery UI which works on PowerShellCore</span></span>

<span data-ttu-id="69332-111">Použití značek: "PSEdition_Desktop" a značky: "PSEdition_Core" filtrům balíčky v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69332-111">Use Tags:"PSEdition_Desktop" and Tags:"PSEdition_Core" to filters the packages on PowerShell Gallery.</span></span>

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a><span data-ttu-id="69332-112">Použití značek: "PSEdition_Core" k vyhledání položek, které jsou kompatibilní s PowerShell Core Edition.</span><span class="sxs-lookup"><span data-stu-id="69332-112">Use Tags:"PSEdition_Core" to search items compatible with PowerShell Core Edition.</span></span>

![Výsledky hledání pro položky, které jsou kompatibilní s Core PSEdition](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a><span data-ttu-id="69332-114">Použití značek: "PSEdition_Desktop" k vyhledání položek, které jsou kompatibilní s Powershellu Desktop Edition.</span><span class="sxs-lookup"><span data-stu-id="69332-114">Use Tags:"PSEdition_Desktop" to search items compatible with PowerShell Desktop Edition.</span></span>

![Výsledky hledání pro položky, které jsou kompatibilní s Desktop PSEdition](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a><span data-ttu-id="69332-116">Další informace o vytváření a hledání balíčky s kompatibilní edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="69332-116">More details on authoring and finding the packages with compatible PowerShell Editions</span></span>

- [<span data-ttu-id="69332-117">Moduly s PSEditions</span><span class="sxs-lookup"><span data-stu-id="69332-117">Modules with PSEditions</span></span>](../../concepts/module-psedition-support.md)
- [<span data-ttu-id="69332-118">Skripty s PSEditions</span><span class="sxs-lookup"><span data-stu-id="69332-118">Scripts with PSEditions</span></span>](../../concepts/script-psedition-support.md)

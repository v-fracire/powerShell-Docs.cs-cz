---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_pseditions
ms.openlocfilehash: 6634da5c2dadee9c0c6470b3d3e8883e6d02160f
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="items-with-compatible-powershell-editions"></a><span data-ttu-id="bdf88-103">Položky s kompatibilní verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdf88-103">Items with compatible PowerShell Editions</span></span>
<span data-ttu-id="bdf88-104">Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.</span><span class="sxs-lookup"><span data-stu-id="bdf88-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="bdf88-105">**Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="bdf88-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="bdf88-106">**Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="bdf88-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-items-compatible-for-specific-powershell-editions"></a><span data-ttu-id="bdf88-107">Galerie prostředí PowerShell extrahuje podporované PSEditions metadata a umožňuje filtry položky kompatibilní pro konkrétní edice prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdf88-107">PowerShell Gallery extracts supported PSEditions metadata and allows you to filters the items compatible for specific PowerShell Editions</span></span>

<span data-ttu-id="bdf88-108">Pokud má položka kompatibilní PSEditions zadané, budou uvedené jako součást 'prostředí PowerShell edice, na stránce položky zobrazení a také ve výsledcích položky.</span><span class="sxs-lookup"><span data-stu-id="bdf88-108">If an item has compatible PSEditions specified, they will be listed as part of 'PowerShell Editions' in the item display page and also in items results.</span></span>
<span data-ttu-id="bdf88-109">![Stránka zobrazení položky s PSEditions](Images/ItemDisplayPageWithPSEditions.PNG)</span><span class="sxs-lookup"><span data-stu-id="bdf88-109">![Item display page with PSEditions](Images/ItemDisplayPageWithPSEditions.PNG)</span></span>

## <a name="search-for-items-in-the-gallery-ui-which-works-on-powershellcore"></a><span data-ttu-id="bdf88-110">Hledání položek v galerii uživatelského rozhraní, který pracuje na PowerShellCore</span><span class="sxs-lookup"><span data-stu-id="bdf88-110">Search for items in the gallery UI which works on PowerShellCore</span></span>
<span data-ttu-id="bdf88-111">Použití značek: značky a "PSEdition_Desktop": "PSEdition_Core" filtrů prostřednictvím položky z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdf88-111">Use Tags:"PSEdition_Desktop" and Tags:"PSEdition_Core" to filters the items on PowerShell Gallery.</span></span>

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a><span data-ttu-id="bdf88-112">Použití značek: "PSEdition_Core" k vyhledání položek, které jsou kompatibilní s edicí základní prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdf88-112">Use Tags:"PSEdition_Core" to search items compatible with PowerShell Core Edition.</span></span>
![Výsledky hledání pro položky, které jsou kompatibilní s PSEdition jádra](Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a><span data-ttu-id="bdf88-114">Použití značek: "PSEdition_Desktop" k vyhledání položek, které jsou kompatibilní s edicí plochy prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bdf88-114">Use Tags:"PSEdition_Desktop" to search items compatible with PowerShell Desktop Edition.</span></span>
![Výsledky hledání pro položky, které jsou kompatibilní s PSEdition plochy](Images/SearchResultsWithPSEdition_Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-items-with-compatible-powershell-editions"></a><span data-ttu-id="bdf88-116">Další informace o vytváření a hledání položek s kompatibilní verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdf88-116">More details on authoring and finding the items with compatible PowerShell Editions</span></span>
### <a name="modules-with-pseditionspsgetmodulemodulewithpseditionsupportmd"></a>[<span data-ttu-id="bdf88-117">Moduly s PSEditions</span><span class="sxs-lookup"><span data-stu-id="bdf88-117">Modules with PSEditions</span></span>](../psget/module/modulewithpseditionsupport.md)
### <a name="scripts-with-pseditionspsgetscriptscriptwithpseditionsupportmd"></a>[<span data-ttu-id="bdf88-118">Skripty s PSEditions</span><span class="sxs-lookup"><span data-stu-id="bdf88-118">Scripts with PSEditions</span></span>](../psget/script/scriptwithpseditionsupport.md)

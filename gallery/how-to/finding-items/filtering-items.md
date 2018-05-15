---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Filtrování výsledků hledání
ms.openlocfilehash: 5a7ea8207619318efd8195ee3d1c8f8ab51209da
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="filtering-search-results"></a><span data-ttu-id="20c6e-103">Filtrování výsledků hledání</span><span class="sxs-lookup"><span data-stu-id="20c6e-103">Filtering search results</span></span>

<span data-ttu-id="20c6e-104">[Karta položky](https://www.powershellgallery.com/items) zobrazí všechny položky k dispozici v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20c6e-104">The [Items tab](https://www.powershellgallery.com/items) displays all available items in the PowerShell Gallery.</span></span>

<span data-ttu-id="20c6e-105">Existuje několik způsobů k filtrování, řazení a vyhledávání položek.</span><span class="sxs-lookup"><span data-stu-id="20c6e-105">There are several ways to filter, sort, and search the items.</span></span>
<span data-ttu-id="20c6e-106">Pokud chcete zobrazit další podrobnosti o konkrétní položky, klikněte na položku.</span><span class="sxs-lookup"><span data-stu-id="20c6e-106">To see more details about a particular item, click the item.</span></span>

## <a name="filter-by"></a><span data-ttu-id="20c6e-107">Filtrovat podle</span><span class="sxs-lookup"><span data-stu-id="20c6e-107">Filter By</span></span>

<span data-ttu-id="20c6e-108">Rozevírací seznam v části "Filtrovat podle" umožňuje uživatelům filtrovat výsledky podle:</span><span class="sxs-lookup"><span data-stu-id="20c6e-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
- <span data-ttu-id="20c6e-109">Zahrnout předběžné verze</span><span class="sxs-lookup"><span data-stu-id="20c6e-109">Include Prerelease</span></span>
- <span data-ttu-id="20c6e-110">Pouze ustájení</span><span class="sxs-lookup"><span data-stu-id="20c6e-110">Stable Only</span></span>

<span data-ttu-id="20c6e-111">Informace o "předběžné verze" a "Stabilní" najdete v tématu [předběžné verze Správa verzí přidat do PowerShellGet a Galerie prostředí PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) v blogu týmu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20c6e-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="20c6e-112">Zaškrtávací políčka v rozevíracím seznamu umožňují uživatelům filtrovat výsledky podle:</span><span class="sxs-lookup"><span data-stu-id="20c6e-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
- <span data-ttu-id="20c6e-113">Typy položek</span><span class="sxs-lookup"><span data-stu-id="20c6e-113">Item Types</span></span>
  - <span data-ttu-id="20c6e-114">Modul</span><span class="sxs-lookup"><span data-stu-id="20c6e-114">Module</span></span>
  - <span data-ttu-id="20c6e-115">Skript</span><span class="sxs-lookup"><span data-stu-id="20c6e-115">Script</span></span>
- <span data-ttu-id="20c6e-116">Kategorie</span><span class="sxs-lookup"><span data-stu-id="20c6e-116">Categories</span></span>
  - <span data-ttu-id="20c6e-117">Rutina</span><span class="sxs-lookup"><span data-stu-id="20c6e-117">Cmdlet</span></span>
  - <span data-ttu-id="20c6e-118">Prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="20c6e-118">DSC Resource</span></span>
  - <span data-ttu-id="20c6e-119">Funkce</span><span class="sxs-lookup"><span data-stu-id="20c6e-119">Function</span></span>
  - <span data-ttu-id="20c6e-120">Funkce role</span><span class="sxs-lookup"><span data-stu-id="20c6e-120">Role Capability</span></span>
  - <span data-ttu-id="20c6e-121">pracovní postup</span><span class="sxs-lookup"><span data-stu-id="20c6e-121">Workflow</span></span>

<span data-ttu-id="20c6e-122">Pokud chcete zobrazit jenom moduly v galerii prostředí PowerShell, zkontrolujte modulu v typů položek.</span><span class="sxs-lookup"><span data-stu-id="20c6e-122">To see only modules in the PowerShell Gallery, check Module in the Item Types.</span></span>
<span data-ttu-id="20c6e-123">Podobně zobrazí jenom skripty v galerii prostředí PowerShell, zkontrolujte skript v typů položek.</span><span class="sxs-lookup"><span data-stu-id="20c6e-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Item Types.</span></span>

> [!NOTE]
> <span data-ttu-id="20c6e-124">Filtry jsou inkluzivní.</span><span class="sxs-lookup"><span data-stu-id="20c6e-124">Filters are inclusive.</span></span>
> <span data-ttu-id="20c6e-125">Příklad: Položky obsahující rutiny a funkce se zobrazí, pokud jsou zaškrtnutá políčka buď rutiny nebo funkci (nebo obě).</span><span class="sxs-lookup"><span data-stu-id="20c6e-125">Example: An item containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="20c6e-126">Pokud ani jeden z nich jsou vybrané, nebude se zobrazovat položky.</span><span class="sxs-lookup"><span data-stu-id="20c6e-126">If neither are selected, the item will not appear.</span></span>
> <span data-ttu-id="20c6e-127">Podobně pokud jsou vybrané všechny kategorie, se zobrazí pouze položky obsahující jednu z těchto kategorií.</span><span class="sxs-lookup"><span data-stu-id="20c6e-127">Similarly, if all categories are selected, only items containing one of those categories will appear.</span></span>
> <span data-ttu-id="20c6e-128">**Položky, které nepatří do žádné z těchto kategorií se nezobrazí.**</span><span class="sxs-lookup"><span data-stu-id="20c6e-128">**Items that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="20c6e-129">Řadit podle</span><span class="sxs-lookup"><span data-stu-id="20c6e-129">Sort By</span></span>

<span data-ttu-id="20c6e-130">Seřadit podle rozevíracího seznamu umožňuje uživatelům výsledky seřaďte podle:</span><span class="sxs-lookup"><span data-stu-id="20c6e-130">The Sort By drop-down allows users to sort the results by:</span></span>
- <span data-ttu-id="20c6e-131">Oblíbenosti - oblíbenosti je určen podle počtu stažení</span><span class="sxs-lookup"><span data-stu-id="20c6e-131">Popularity - Popularity is determined by Download Count</span></span>
- <span data-ttu-id="20c6e-132">A-Z – abecedně podle názvu položky</span><span class="sxs-lookup"><span data-stu-id="20c6e-132">A-Z - Alphabetically by item name</span></span>
- <span data-ttu-id="20c6e-133">Poslední - položky se zobrazí v pořadí podle data publikování</span><span class="sxs-lookup"><span data-stu-id="20c6e-133">Recent - Items appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="20c6e-134">Pole pro vyhledávání</span><span class="sxs-lookup"><span data-stu-id="20c6e-134">Search Box</span></span>

<span data-ttu-id="20c6e-135">Do vyhledávacího pole umožňuje uživatelům vyhledávat položky klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="20c6e-135">The Search Box allows users to search the items on keywords.</span></span>
<span data-ttu-id="20c6e-136">Další informace najdete v tématu [syntaxe vyhledávání Galerie](search-syntax.md).</span><span class="sxs-lookup"><span data-stu-id="20c6e-136">For more information, see [Gallery Search Syntax](search-syntax.md).</span></span>
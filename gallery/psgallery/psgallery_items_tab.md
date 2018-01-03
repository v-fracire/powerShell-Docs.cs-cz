---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_items_tab
ms.openlocfilehash: 8704091542de5c19817ab0b4f77fd98987084b5d
ms.sourcegitcommit: 1a0a0928c1e3cae4e8df8d79b0737bd7ed6b4e47
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2017
---
# <a name="items-tab"></a><span data-ttu-id="7acb1-103">Karta položky</span><span class="sxs-lookup"><span data-stu-id="7acb1-103">Items Tab</span></span>

<span data-ttu-id="7acb1-104">[Karta položky](https://www.powershellgallery.com/items) zobrazí všechny položky k dispozici v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7acb1-104">The [Items tab](https://www.powershellgallery.com/items) displays all available items in the PowerShell Gallery.</span></span>

<span data-ttu-id="7acb1-105">Existuje několik způsobů k filtrování, řazení a vyhledávání položek.</span><span class="sxs-lookup"><span data-stu-id="7acb1-105">There are several ways to filter, sort, and search the items.</span></span>
<span data-ttu-id="7acb1-106">Pokud chcete zobrazit další podrobnosti o konkrétní položky, klikněte na položku.</span><span class="sxs-lookup"><span data-stu-id="7acb1-106">To see more details about a particular item, click the item.</span></span>

## <a name="filter-by"></a><span data-ttu-id="7acb1-107">Filtrovat podle</span><span class="sxs-lookup"><span data-stu-id="7acb1-107">Filter By</span></span>

<span data-ttu-id="7acb1-108">Rozevírací seznam v části "Filtrovat podle" umožňuje uživatelům filtrovat výsledky podle:</span><span class="sxs-lookup"><span data-stu-id="7acb1-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
* <span data-ttu-id="7acb1-109">Zahrnout předběžné verze</span><span class="sxs-lookup"><span data-stu-id="7acb1-109">Include Prerelease</span></span>
* <span data-ttu-id="7acb1-110">Pouze ustájení</span><span class="sxs-lookup"><span data-stu-id="7acb1-110">Stable Only</span></span>

<span data-ttu-id="7acb1-111">Informace o "předběžné verze" a "Stabilní" najdete v tématu [předběžné verze Správa verzí přidat do PowerShellGet a Galerie prostředí PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) v blogu týmu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7acb1-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="7acb1-112">Zaškrtávací políčka v rozevíracím seznamu umožňují uživatelům filtrovat výsledky podle:</span><span class="sxs-lookup"><span data-stu-id="7acb1-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
* <span data-ttu-id="7acb1-113">Typy položek</span><span class="sxs-lookup"><span data-stu-id="7acb1-113">Item Types</span></span>
  - <span data-ttu-id="7acb1-114">Modul</span><span class="sxs-lookup"><span data-stu-id="7acb1-114">Module</span></span>
  - <span data-ttu-id="7acb1-115">Skript</span><span class="sxs-lookup"><span data-stu-id="7acb1-115">Script</span></span>
* <span data-ttu-id="7acb1-116">Kategorie</span><span class="sxs-lookup"><span data-stu-id="7acb1-116">Categories</span></span>
  - <span data-ttu-id="7acb1-117">Rutina</span><span class="sxs-lookup"><span data-stu-id="7acb1-117">Cmdlet</span></span>
  - <span data-ttu-id="7acb1-118">Prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="7acb1-118">DSC Resource</span></span>
  - <span data-ttu-id="7acb1-119">Funkce</span><span class="sxs-lookup"><span data-stu-id="7acb1-119">Function</span></span>
  - <span data-ttu-id="7acb1-120">Funkce role</span><span class="sxs-lookup"><span data-stu-id="7acb1-120">Role Capability</span></span>
  - <span data-ttu-id="7acb1-121">pracovní postup</span><span class="sxs-lookup"><span data-stu-id="7acb1-121">Workflow</span></span>

<span data-ttu-id="7acb1-122">Pokud chcete zobrazit jenom moduly v galerii prostředí PowerShell, zkontrolujte modulu v typů položek.</span><span class="sxs-lookup"><span data-stu-id="7acb1-122">To see only modules in the PowerShell Gallery, check Module in the Item Types.</span></span>
<span data-ttu-id="7acb1-123">Podobně zobrazí jenom skripty v galerii prostředí PowerShell, zkontrolujte skript v typů položek.</span><span class="sxs-lookup"><span data-stu-id="7acb1-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Item Types.</span></span>

> [!NOTE]
> <span data-ttu-id="7acb1-124">Filtry jsou inkluzivní.</span><span class="sxs-lookup"><span data-stu-id="7acb1-124">Filters are inclusive.</span></span>
> <span data-ttu-id="7acb1-125">Příklad: Položky obsahující rutiny a funkce se zobrazí, pokud jsou zaškrtnutá políčka buď rutiny nebo funkci (nebo obě).</span><span class="sxs-lookup"><span data-stu-id="7acb1-125">Example: An item containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="7acb1-126">Pokud ani jeden z nich jsou vybrané, nebude se zobrazovat položky.</span><span class="sxs-lookup"><span data-stu-id="7acb1-126">If neither are selected, the item will not appear.</span></span>
> <span data-ttu-id="7acb1-127">Podobně pokud jsou vybrané všechny kategorie, se zobrazí pouze položky obsahující jednu z těchto kategorií.</span><span class="sxs-lookup"><span data-stu-id="7acb1-127">Similarly, if all categories are selected, only items containing one of those categories will appear.</span></span>
> <span data-ttu-id="7acb1-128">**Položky, které nepatří do žádné z těchto kategorií se nezobrazí.**</span><span class="sxs-lookup"><span data-stu-id="7acb1-128">**Items that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="7acb1-129">Řadit podle</span><span class="sxs-lookup"><span data-stu-id="7acb1-129">Sort By</span></span>

<span data-ttu-id="7acb1-130">Seřadit podle rozevíracího seznamu umožňuje uživatelům výsledky seřaďte podle:</span><span class="sxs-lookup"><span data-stu-id="7acb1-130">The Sort By drop-down allows users to sort the results by:</span></span>
* <span data-ttu-id="7acb1-131">Oblíbenosti - oblíbenosti je určen podle počtu stažení</span><span class="sxs-lookup"><span data-stu-id="7acb1-131">Popularity - Popularity is determined by Download Count</span></span>
* <span data-ttu-id="7acb1-132">A-Z – abecedně podle názvu položky</span><span class="sxs-lookup"><span data-stu-id="7acb1-132">A-Z - Alphabetically by item name</span></span>
* <span data-ttu-id="7acb1-133">Poslední - položky se zobrazí v pořadí podle data publikování</span><span class="sxs-lookup"><span data-stu-id="7acb1-133">Recent - Items appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="7acb1-134">Pole pro vyhledávání</span><span class="sxs-lookup"><span data-stu-id="7acb1-134">Search Box</span></span>

<span data-ttu-id="7acb1-135">Do vyhledávacího pole umožňuje uživatelům vyhledávat položky klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="7acb1-135">The Search Box allows users to search the items on keywords.</span></span>
<span data-ttu-id="7acb1-136">Další informace najdete v tématu [syntaxe vyhledávání Galerie](psgallery_search_syntax.md).</span><span class="sxs-lookup"><span data-stu-id="7acb1-136">For more information, see [Gallery Search Syntax](psgallery_search_syntax.md).</span></span>

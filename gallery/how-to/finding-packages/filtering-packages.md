---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Filtrování výsledků hledání
ms.openlocfilehash: 13270a310613a974e1588a9f56d443a936cfebb8
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004032"
---
# <a name="filtering-search-results"></a><span data-ttu-id="99c76-103">Filtrování výsledků hledání</span><span class="sxs-lookup"><span data-stu-id="99c76-103">Filtering search results</span></span>

<span data-ttu-id="99c76-104">[Balíčky kartu](https://www.powershellgallery.com/packages) zobrazuje všechny dostupné balíčky v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99c76-104">The [Packages tab](https://www.powershellgallery.com/packages) displays all available packages in the PowerShell Gallery.</span></span>

<span data-ttu-id="99c76-105">Existuje několik způsobů filtrování, řazení a vyhledávání balíčků.</span><span class="sxs-lookup"><span data-stu-id="99c76-105">There are several ways to filter, sort, and search the packages.</span></span>
<span data-ttu-id="99c76-106">Pokud chcete zobrazit další podrobnosti o konkrétního balíčku, klikněte na balíček.</span><span class="sxs-lookup"><span data-stu-id="99c76-106">To see more details about a particular package, click the package.</span></span>

## <a name="filter-by"></a><span data-ttu-id="99c76-107">Filtrovat podle</span><span class="sxs-lookup"><span data-stu-id="99c76-107">Filter By</span></span>

<span data-ttu-id="99c76-108">Rozevírací seznam v části "Filtrovat podle" umožňuje filtrovat výsledky podle:</span><span class="sxs-lookup"><span data-stu-id="99c76-108">The drop-down under "Filter By" allows users to filter the results by:</span></span>
- <span data-ttu-id="99c76-109">Zahrnout předběžné verze</span><span class="sxs-lookup"><span data-stu-id="99c76-109">Include Prerelease</span></span>
- <span data-ttu-id="99c76-110">Pouze stabilní verze</span><span class="sxs-lookup"><span data-stu-id="99c76-110">Stable Only</span></span>

<span data-ttu-id="99c76-111">Informace o "předběžné verze" a "Stálé" v tématu [předběžné verze správy verzí přidat do Správce balíčků PowerShellGet a Galerie prostředí PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) na blogu týmu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99c76-111">For information about "Prerelease" and "Stable", see [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) in the PowerShell Team Blog.</span></span>

<span data-ttu-id="99c76-112">Zaškrtávací políčka v rozevíracího seznamu umožňují uživatelům výsledky filtrovat podle:</span><span class="sxs-lookup"><span data-stu-id="99c76-112">The checkboxes under the drop-down allow users to filter the results by:</span></span>
- <span data-ttu-id="99c76-113">Typy balíčků</span><span class="sxs-lookup"><span data-stu-id="99c76-113">Package Types</span></span>
  - <span data-ttu-id="99c76-114">Modul</span><span class="sxs-lookup"><span data-stu-id="99c76-114">Module</span></span>
  - <span data-ttu-id="99c76-115">Skript</span><span class="sxs-lookup"><span data-stu-id="99c76-115">Script</span></span>
- <span data-ttu-id="99c76-116">Kategorie</span><span class="sxs-lookup"><span data-stu-id="99c76-116">Categories</span></span>
  - <span data-ttu-id="99c76-117">Rutina</span><span class="sxs-lookup"><span data-stu-id="99c76-117">Cmdlet</span></span>
  - <span data-ttu-id="99c76-118">Prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="99c76-118">DSC Resource</span></span>
  - <span data-ttu-id="99c76-119">Funkce</span><span class="sxs-lookup"><span data-stu-id="99c76-119">Function</span></span>
  - <span data-ttu-id="99c76-120">Funkce rolí</span><span class="sxs-lookup"><span data-stu-id="99c76-120">Role Capability</span></span>
  - <span data-ttu-id="99c76-121">Pracovní postup</span><span class="sxs-lookup"><span data-stu-id="99c76-121">Workflow</span></span>

<span data-ttu-id="99c76-122">Pokud chcete zobrazit pouze moduly v galerii prostředí PowerShell, zkontrolujte modulu v typy balíčků.</span><span class="sxs-lookup"><span data-stu-id="99c76-122">To see only modules in the PowerShell Gallery, check Module in the Package Types.</span></span>
<span data-ttu-id="99c76-123">Podobně najdete v článku pouze skripty v galerii prostředí PowerShell, zkontrolujte skript v typy balíčků.</span><span class="sxs-lookup"><span data-stu-id="99c76-123">Similarly, to see only scripts in the PowerShell Gallery, check Script in the Package Types.</span></span>

> [!NOTE]
> <span data-ttu-id="99c76-124">Filtry jsou inkluzivní.</span><span class="sxs-lookup"><span data-stu-id="99c76-124">Filters are inclusive.</span></span>
> <span data-ttu-id="99c76-125">Příklad: Balíček, který obsahuje rutiny a funkce se zobrazí, pokud jsou kontrolovány buď rutina – funkce (nebo obojí).</span><span class="sxs-lookup"><span data-stu-id="99c76-125">Example: A package containing both cmdlets and functions will appear if either Cmdlet or Function (or both) are checked.</span></span>
> <span data-ttu-id="99c76-126">Pokud ani jedno, nezobrazí se balíček.</span><span class="sxs-lookup"><span data-stu-id="99c76-126">If neither are selected, the package will not appear.</span></span>
> <span data-ttu-id="99c76-127">Podobně pokud jsou vybrány všechny kategorie, se zobrazí pouze balíčky obsahující jednu z těchto kategorií.</span><span class="sxs-lookup"><span data-stu-id="99c76-127">Similarly, if all categories are selected, only packages containing one of those categories will appear.</span></span>
> <span data-ttu-id="99c76-128">**Balíčky, které nepatří do žádné z těchto kategorií se nezobrazí.**</span><span class="sxs-lookup"><span data-stu-id="99c76-128">**Packages that do not belong to any of those categories will not appear.**</span></span>

## <a name="sort-by"></a><span data-ttu-id="99c76-129">Seřadit podle:</span><span class="sxs-lookup"><span data-stu-id="99c76-129">Sort By</span></span>

<span data-ttu-id="99c76-130">Řadit podle rozevíracího seznamu umožňuje seřadit výsledky podle:</span><span class="sxs-lookup"><span data-stu-id="99c76-130">The Sort By drop-down allows users to sort the results by:</span></span>
- <span data-ttu-id="99c76-131">Popularita - popularita se určuje podle počtu stažení</span><span class="sxs-lookup"><span data-stu-id="99c76-131">Popularity - Popularity is determined by Download Count</span></span>
- <span data-ttu-id="99c76-132">A-Z - abecedně podle názvu balíčku</span><span class="sxs-lookup"><span data-stu-id="99c76-132">A-Z - Alphabetically by package name</span></span>
- <span data-ttu-id="99c76-133">Poslední - balíčky zobrazí v pořadí datum publikování</span><span class="sxs-lookup"><span data-stu-id="99c76-133">Recent - Packages appear in order of publish date</span></span>

## <a name="search-box"></a><span data-ttu-id="99c76-134">Vyhledávací pole</span><span class="sxs-lookup"><span data-stu-id="99c76-134">Search Box</span></span>

<span data-ttu-id="99c76-135">Do vyhledávacího pole umožňuje uživatelům vyhledávání balíčků na klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="99c76-135">The Search Box allows users to search the packages on keywords.</span></span>
<span data-ttu-id="99c76-136">Další informace najdete v tématu [syntaxe hledání v galerii](search-syntax.md).</span><span class="sxs-lookup"><span data-stu-id="99c76-136">For more information, see [Gallery Search Syntax](search-syntax.md).</span></span>

---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Syntaxe hledání v galerii
ms.openlocfilehash: 9aadb6771c85845cc3fa05cb56f0194b060d1c1b
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004010"
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="28b79-103">Syntaxe hledání v galerii</span><span class="sxs-lookup"><span data-stu-id="28b79-103">Gallery Search Syntax</span></span>

<span data-ttu-id="28b79-104">Galerie prostředí PowerShell nabízí searchbox text, ve kterém můžete použít slova, fráze a výrazy – klíčové slovo můžete zúžit výsledky hledání.</span><span class="sxs-lookup"><span data-stu-id="28b79-104">PowerShell Gallery offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="28b79-105">Hledat podle klíčových slov</span><span class="sxs-lookup"><span data-stu-id="28b79-105">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="28b79-106">Vyhledávání bude dělat jeho pokusí najít relevantní dokumenty, které obsahují všechna klíčová slova 3 a vrátí odpovídající dokumenty.</span><span class="sxs-lookup"><span data-stu-id="28b79-106">Search will do its best effort to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="28b79-107">Vyhledávání pomocí klíčových slov a vět</span><span class="sxs-lookup"><span data-stu-id="28b79-107">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="28b79-108">Zadání slovní spojení mezi uvozovky ("") změňte parametry hledání, mají hledat konkrétní fráze místo samostatných klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="28b79-108">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="28b79-109">Odpovídajících dokumentů by měl obvykle obsahují přesnou frázi "azure sql", včetně například varianty malá a velká písmena "Azure SQL" a také obvykle obsahovat slovo "nasazení".</span><span class="sxs-lookup"><span data-stu-id="28b79-109">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="28b79-110">Filtrování podle polí</span><span class="sxs-lookup"><span data-stu-id="28b79-110">Filtering on fields</span></span>

<span data-ttu-id="28b79-111">Můžete hledat pro určitý balíček ID (nebo "Id" nebo "id") nebo některých polí přidáním prefixu hledané termíny název pole.</span><span class="sxs-lookup"><span data-stu-id="28b79-111">You can search for a specific package ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="28b79-112">Aktuálně jsou prohledávatelná pole 'Id', 'Version', 'Značky', "Autor", "Vlastník", "Funkce", 'Rutiny', "DscResources" a "Verze".</span><span class="sxs-lookup"><span data-stu-id="28b79-112">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="28b79-113">[Jaký je rozdíl mezi ID a název?</span><span class="sxs-lookup"><span data-stu-id="28b79-113">[What's the difference between ID and Title?</span></span> <span data-ttu-id="28b79-114">ID je název, který používáte v konzole.</span><span class="sxs-lookup"><span data-stu-id="28b79-114">ID is the name you use in the console.</span></span> <span data-ttu-id="28b79-115">Název je, jak je zobrazeno v horní části na stránce balíček ve výsledcích hledání.]</span><span class="sxs-lookup"><span data-stu-id="28b79-115">Title is what is shown at the top of the package page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="28b79-116">Příklady</span><span class="sxs-lookup"><span data-stu-id="28b79-116">Examples</span></span>

    ID:"PSReadline"
    id:"AzureRM.Profile"

<span data-ttu-id="28b79-117">Vyhledá balíčky s "PSReadline" nebo "AzureRM.Profile" v jejich pole ID v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="28b79-117">finds packages with "PSReadline" or "AzureRM.Profile" in their ID field respectively.</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="28b79-118">je další způsob, jak vyhledat balíčky s "AzureRM.Profile" v jejich pole ID.</span><span class="sxs-lookup"><span data-stu-id="28b79-118">is another way to find packages with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="28b79-119">Filtr "Id" je dílčí řetězec shodovat, tak při hledání následující:</span><span class="sxs-lookup"><span data-stu-id="28b79-119">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"

<span data-ttu-id="28b79-120">Zobrazí se výsledky, jako jsou "AzureRM.Profile" a "Azure.Storage".</span><span class="sxs-lookup"><span data-stu-id="28b79-120">You'll get results like 'AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="28b79-121">Můžete také vyhledat více klíčových slov do jednoho pole.</span><span class="sxs-lookup"><span data-stu-id="28b79-121">You can also search for multiple keywords in a single field.</span></span> <span data-ttu-id="28b79-122">Nebo kombinovat a Párovat pole.</span><span class="sxs-lookup"><span data-stu-id="28b79-122">Or mix and match fields.</span></span>

    id:azure tags:intellisense
    id:azure id:storage

<span data-ttu-id="28b79-123">A můžete provádět vyhledávání frází:</span><span class="sxs-lookup"><span data-stu-id="28b79-123">And you can perform phrase searches:</span></span>

    id:"azure.storage"


<span data-ttu-id="28b79-124">K vyhledání všech balíčků značkou DSC.</span><span class="sxs-lookup"><span data-stu-id="28b79-124">To search all packages with DSC tag.</span></span>

    Tags:"DSC"

<span data-ttu-id="28b79-125">K vyhledání všech balíčků pomocí zadané funkce.</span><span class="sxs-lookup"><span data-stu-id="28b79-125">To search all packages with the specified function.</span></span>

    Functions:"Update-AzureRM"

<span data-ttu-id="28b79-126">K vyhledání všech balíčků pomocí zadaného rutiny.</span><span class="sxs-lookup"><span data-stu-id="28b79-126">To search all packages with the specified cmdlet.</span></span>

    Cmdlets:"Get-AzureRmEnvironment"

<span data-ttu-id="28b79-127">K vyhledání všech balíčků se zadaným názvem prostředku DSC.</span><span class="sxs-lookup"><span data-stu-id="28b79-127">To search all packages with the specified DSC Resource name.</span></span>

    DscResources:"xArchive"

<span data-ttu-id="28b79-128">K vyhledání všech balíčků pomocí zadané verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="28b79-128">To search all packages with the specified PowerShellVersion</span></span>

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


<span data-ttu-id="28b79-129">Nakonec pokud používáte pole, které nepodporujeme, jako je například "příkazy", vytvoříme právě ho ignorovat a hledat všechna pole.</span><span class="sxs-lookup"><span data-stu-id="28b79-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="28b79-130">Proto následující dotaz</span><span class="sxs-lookup"><span data-stu-id="28b79-130">So the following query</span></span>

    commands:blobs storage

<span data-ttu-id="28b79-131">Je interpretován stejně jako tento dotaz:</span><span class="sxs-lookup"><span data-stu-id="28b79-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage

---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Syntaxe hledání v galerii
ms.openlocfilehash: aabcaa1f1b5b641ab5033c9ba2e358477c84a23b
ms.sourcegitcommit: e24525046dd37166b9d83eeecdc534726316f429
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/01/2018
ms.locfileid: "52742852"
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="03fad-103">Syntaxe hledání v galerii</span><span class="sxs-lookup"><span data-stu-id="03fad-103">Gallery Search Syntax</span></span>

<span data-ttu-id="03fad-104">Můžete vyhledávat pomocí Galerie prostředí PowerShell [webu Galerie prostředí PowerShell](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="03fad-104">You can search the PowerShell Gallery using the [PowerShell Gallery's web site](https://www.powershellgallery.com/).</span></span>
<span data-ttu-id="03fad-105">Webu Galerie prostředí PowerShell nabízí searchbox text, ve kterém můžete použít slova, fráze a výrazy – klíčové slovo můžete zúžit výsledky hledání.</span><span class="sxs-lookup"><span data-stu-id="03fad-105">PowerShell Gallery web site offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="03fad-106">Hledat podle klíčových slov</span><span class="sxs-lookup"><span data-stu-id="03fad-106">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="03fad-107">Hledání se pokusí najít relevantní dokumenty, které obsahují všechna klíčová slova 3 a vrátí odpovídající dokumenty.</span><span class="sxs-lookup"><span data-stu-id="03fad-107">Search attempts to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="03fad-108">Vyhledávání pomocí klíčových slov a vět</span><span class="sxs-lookup"><span data-stu-id="03fad-108">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="03fad-109">Zadání slovní spojení mezi uvozovky ("") změňte parametry hledání, mají hledat konkrétní fráze místo samostatných klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="03fad-109">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="03fad-110">Odpovídajících dokumentů by měl obvykle obsahují přesnou frázi "azure sql", včetně například varianty malá a velká písmena "Azure SQL" a také obvykle obsahovat slovo "nasazení".</span><span class="sxs-lookup"><span data-stu-id="03fad-110">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="03fad-111">Filtrování podle polí</span><span class="sxs-lookup"><span data-stu-id="03fad-111">Filtering on fields</span></span>

<span data-ttu-id="03fad-112">Můžete hledat pro určitý balíček ID (nebo "Id" nebo "id") nebo některých polí přidáním prefixu hledané termíny název pole.</span><span class="sxs-lookup"><span data-stu-id="03fad-112">You can search for a specific package ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="03fad-113">Aktuálně jsou prohledávatelná pole 'Id', 'Version', 'Značky', "Autor", "Vlastník", "Funkce", 'Rutiny', "DscResources" a "Verze".</span><span class="sxs-lookup"><span data-stu-id="03fad-113">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="03fad-114">[Jaký je rozdíl mezi ID a název?</span><span class="sxs-lookup"><span data-stu-id="03fad-114">[What's the difference between ID and Title?</span></span> <span data-ttu-id="03fad-115">ID je název, který používáte v konzole.</span><span class="sxs-lookup"><span data-stu-id="03fad-115">ID is the name you use in the console.</span></span> <span data-ttu-id="03fad-116">Název je, jak je zobrazeno v horní části na stránce balíček ve výsledcích hledání.]</span><span class="sxs-lookup"><span data-stu-id="03fad-116">Title is what is shown at the top of the package page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="03fad-117">Příklady</span><span class="sxs-lookup"><span data-stu-id="03fad-117">Examples</span></span>

    ID:PSReadline
    
<span data-ttu-id="03fad-118">Vyhledá balíčky s ID obsahující "PSReadline".</span><span class="sxs-lookup"><span data-stu-id="03fad-118">finds packages with an ID containing "PSReadline".</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="03fad-119">je další způsob, jak vyhledat balíčky s "AzureRM.Profile" v jejich pole ID.</span><span class="sxs-lookup"><span data-stu-id="03fad-119">is another way to find packages with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="03fad-120">Filtr "Id" je dílčí řetězec shodovat, tak při hledání následující:</span><span class="sxs-lookup"><span data-stu-id="03fad-120">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"

<span data-ttu-id="03fad-121">To poskytuje výsledky, které zahrnují AzureRM.Profile "a"Azure.Storage".</span><span class="sxs-lookup"><span data-stu-id="03fad-121">This provides results that include AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="03fad-122">Můžete také vyhledat více klíčových slov do jednoho pole.</span><span class="sxs-lookup"><span data-stu-id="03fad-122">You can also search for multiple keywords in a single field.</span></span> 

    id:azure tags:intellisense

<span data-ttu-id="03fad-123">A můžete provádět vyhledávání frází pomocí dvojitých uvozovek:</span><span class="sxs-lookup"><span data-stu-id="03fad-123">And you can perform phrase searches using double quotes:</span></span>

    id:"azure.storage"

<span data-ttu-id="03fad-124">K vyhledání všech balíčků značkou DSC.</span><span class="sxs-lookup"><span data-stu-id="03fad-124">To search all packages with DSC tag.</span></span>

    Tags:DSC

<span data-ttu-id="03fad-125">K vyhledání všech balíčků pomocí zadané funkce.</span><span class="sxs-lookup"><span data-stu-id="03fad-125">To search all packages with the specified function.</span></span>

    Functions:Get-TreeSize

<span data-ttu-id="03fad-126">K vyhledání všech balíčků pomocí zadaného rutiny.</span><span class="sxs-lookup"><span data-stu-id="03fad-126">To search all packages with the specified cmdlet.</span></span>

    Cmdlets:Get-AzureRmEnvironment

<span data-ttu-id="03fad-127">K vyhledání všech balíčků se zadaným názvem prostředku DSC.</span><span class="sxs-lookup"><span data-stu-id="03fad-127">To search all packages with the specified DSC Resource name.</span></span>

    DscResources:xArchive

<span data-ttu-id="03fad-128">K vyhledání všech balíčků pomocí zadané verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="03fad-128">To search all packages with the specified PowerShellVersion</span></span>

    PowerShellVersion:2.0

<span data-ttu-id="03fad-129">Nakonec pokud používáte pole, které nepodporujeme, jako je například "příkazy", vytvoříme právě ho ignorovat a hledat všechna pole.</span><span class="sxs-lookup"><span data-stu-id="03fad-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="03fad-130">Proto následující dotaz</span><span class="sxs-lookup"><span data-stu-id="03fad-130">So the following query</span></span>

    commands:blobs storage

<span data-ttu-id="03fad-131">Je interpretován stejně jako tento dotaz:</span><span class="sxs-lookup"><span data-stu-id="03fad-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage

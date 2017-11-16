---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_search_syntax
ms.openlocfilehash: 409ae607557af760f9cec4e3c54f39e51b5fac18
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="gallery-search-syntax"></a><span data-ttu-id="1c3da-103">Syntaxe vyhledávání Galerie</span><span class="sxs-lookup"><span data-stu-id="1c3da-103">Gallery Search Syntax</span></span>

<span data-ttu-id="1c3da-104">Galerie prostředí PowerShell nabízí text searchbox, kde můžete použít slova, frází a výrazy – klíčové slovo Chcete-li zúžit výsledky vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="1c3da-104">PowerShell Gallery offers a text searchbox where you can use words, phrases and keyword expressions to narrow down search results.</span></span>

## <a name="search-by-keywords"></a><span data-ttu-id="1c3da-105">Vyhledávání podle klíčových slov</span><span class="sxs-lookup"><span data-stu-id="1c3da-105">Search by Keywords</span></span>

    dsc azure sql

<span data-ttu-id="1c3da-106">Hledání se provést jeho usilovně najít relevantní dokumenty obsahující všechny 3 klíčová slova a vrátí odpovídající dokumenty.</span><span class="sxs-lookup"><span data-stu-id="1c3da-106">Search will do its best effort to find relevant documents containing all 3 keywords, and return matching documents.</span></span>

## <a name="search-using-phrases-and-keywords"></a><span data-ttu-id="1c3da-107">Vyhledávání pomocí klíčových slov a frází</span><span class="sxs-lookup"><span data-stu-id="1c3da-107">Search using Phrases and keywords</span></span>

    "azure sql" deployment

<span data-ttu-id="1c3da-108">Zadání slovní spojení mezi znaky uvozovek ("") změňte parametry hledání a hledat konkrétní frázi místo samostatné klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="1c3da-108">Entering a phrase between quotation marks ("") change the search to look for the particular phrase instead of separate keywords.</span></span>
<span data-ttu-id="1c3da-109">Odpovídající dokumenty by měl obvykle obsahují přesný řetězec "azure sql", například včetně varianty malá a velká písmena "Azure SQL" a také obvykle obsahovat slovo 'nasazení'.</span><span class="sxs-lookup"><span data-stu-id="1c3da-109">Matching documents should usually contain the exact phrase "azure sql", including variations on capitalization e.g. "Azure SQL", and also usually contain the word 'deployment'.</span></span>

## <a name="filtering-on-fields"></a><span data-ttu-id="1c3da-110">Filtrování na pole</span><span class="sxs-lookup"><span data-stu-id="1c3da-110">Filtering on fields</span></span>

<span data-ttu-id="1c3da-111">Můžete vyhledat konkrétní položku ID (nebo 'Id' nebo 'id'), nebo určitá pole pomocí prefixu vyhledávání podmínky název pole.</span><span class="sxs-lookup"><span data-stu-id="1c3da-111">You can search for a specific item ID (or 'Id' or 'id'), or certain other fields by prefixing search terms with the field name.</span></span>

<span data-ttu-id="1c3da-112">Aktuálně jsou prohledávatelné pole 'Id', 'Version', 'Značky', 'Vytvořit', "Vlastník", "Funkce", 'Rutiny', 'DscResources' a 'verze prostředí PowerShell..</span><span class="sxs-lookup"><span data-stu-id="1c3da-112">Currently the searchable fields are 'Id', 'Version', 'Tags', 'Author', 'Owner', 'Functions', 'Cmdlets', 'DscResources' and 'PowerShellVersion'.</span></span>

<span data-ttu-id="1c3da-113">[Jaký je rozdíl mezi ID a název?</span><span class="sxs-lookup"><span data-stu-id="1c3da-113">[What's the difference between ID and Title?</span></span> <span data-ttu-id="1c3da-114">ID je název, který používáte v konzole.</span><span class="sxs-lookup"><span data-stu-id="1c3da-114">ID is the name you use in the console.</span></span> <span data-ttu-id="1c3da-115">Název je co se zobrazí v horní části stránky položky ve výsledcích hledání.]</span><span class="sxs-lookup"><span data-stu-id="1c3da-115">Title is what is shown at the top of the item page in search results.]</span></span>

## <a name="examples"></a><span data-ttu-id="1c3da-116">Příklady</span><span class="sxs-lookup"><span data-stu-id="1c3da-116">Examples</span></span>

    ID:"PSReadline"
    id:"AzureRM.Profile"

<span data-ttu-id="1c3da-117">Vyhledá položky "PSReadline" nebo "AzureRM.Profile" v jejich ID pole v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="1c3da-117">finds items with "PSReadline" or "AzureRM.Profile" in their ID field respectively.</span></span>

    Id:"AzureRM.Profile"

<span data-ttu-id="1c3da-118">je další způsob hledání položek s "AzureRM.Profile" v jejich ID pole.</span><span class="sxs-lookup"><span data-stu-id="1c3da-118">is another way to find items with "AzureRM.Profile" in their ID field.</span></span>

<span data-ttu-id="1c3da-119">Filtr 'Id' je dílčí řetězec shodují, tak pokud hledáte následující:</span><span class="sxs-lookup"><span data-stu-id="1c3da-119">The 'Id' filter is a substring match, so if you search for the following:</span></span>

    Id:"azure"
    
<span data-ttu-id="1c3da-120">Získáte výsledky jako 'AzureRM.Profile' a 'Azure.Storage'.</span><span class="sxs-lookup"><span data-stu-id="1c3da-120">You'll get results like 'AzureRM.Profile' and 'Azure.Storage'.</span></span>

<span data-ttu-id="1c3da-121">Můžete také prohledat několik klíčových slov do jednoho pole.</span><span class="sxs-lookup"><span data-stu-id="1c3da-121">You can also search for multiple keywords in a single field.</span></span> <span data-ttu-id="1c3da-122">Nebo kombinovat a Párovat pole.</span><span class="sxs-lookup"><span data-stu-id="1c3da-122">Or mix and match fields.</span></span>

    id:azure tags:intellisense
    id:azure id:storage

<span data-ttu-id="1c3da-123">A můžete provádět vyhledávání frázi:</span><span class="sxs-lookup"><span data-stu-id="1c3da-123">And you can perform phrase searches:</span></span>

    id:"azure.storage"


<span data-ttu-id="1c3da-124">K vyhledání všech položek s DSC značkou.</span><span class="sxs-lookup"><span data-stu-id="1c3da-124">To search all items with DSC tag.</span></span>

    Tags:"DSC"

<span data-ttu-id="1c3da-125">Chcete-li vyhledat všechny položky se zadanou funkcí.</span><span class="sxs-lookup"><span data-stu-id="1c3da-125">To search all items with the specified function.</span></span>

    Functions:"Update-AzureRM"

<span data-ttu-id="1c3da-126">K vyhledání všech položek s zadanou rutinu.</span><span class="sxs-lookup"><span data-stu-id="1c3da-126">To search all items with the specified cmdlet.</span></span>
    
    Cmdlets:"Get-AzureRmEnvironment"

<span data-ttu-id="1c3da-127">Chcete-li vyhledat všechny položky se zadaným názvem prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="1c3da-127">To search all items with the specified DSC Resource name.</span></span>

    DscResources:"xArchive"

<span data-ttu-id="1c3da-128">K vyhledání všech položek, zadaná verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c3da-128">To search all items with the specified PowerShellVersion</span></span>

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


<span data-ttu-id="1c3da-129">Nakonec pokud používáte pole, které nepodporujeme, například "příkazů, jsme budete právě ho ignorovat a hledání všechna pole.</span><span class="sxs-lookup"><span data-stu-id="1c3da-129">Finally, if you use a field we don't support, such as 'commands', we'll just ignore it and search all the fields.</span></span> <span data-ttu-id="1c3da-130">Proto tyto dotazu</span><span class="sxs-lookup"><span data-stu-id="1c3da-130">So the following query</span></span>

    commands:blobs storage
    
<span data-ttu-id="1c3da-131">Je interpretovat stejně jako tento dotaz:</span><span class="sxs-lookup"><span data-stu-id="1c3da-131">Is interpreted exactly the same as this query:</span></span>

    blobs storage


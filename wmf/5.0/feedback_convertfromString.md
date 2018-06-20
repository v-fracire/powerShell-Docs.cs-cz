---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: e4588e8c69efb965cd33c273ad09a8bef8e9bf16
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189563"
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a><span data-ttu-id="65220-102">Extrakce a analýza strukturovaných objektů mimo řetězec</span><span class="sxs-lookup"><span data-stu-id="65220-102">Extract and Parse Structured Objects out of String</span></span>
<span data-ttu-id="65220-103">Vzniká některé další funkce pro rutinu ConvertFrom řetězec:</span><span class="sxs-lookup"><span data-stu-id="65220-103">This also introduces some additional functionality for the ConvertFrom-String cmdlet:</span></span>

-   <span data-ttu-id="65220-104">Odebere rozsah vlastnost text ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="65220-104">Removes the extent text property by default.</span></span> <span data-ttu-id="65220-105">Můžete vytvořit s parametrem - IncludeExtent.</span><span class="sxs-lookup"><span data-stu-id="65220-105">You can include it with the -IncludeExtent parameter.</span></span>

-   <span data-ttu-id="65220-106">Mnoho učení algoritmu opravy chyb z MVP a komunity zpětnou vazbu.</span><span class="sxs-lookup"><span data-stu-id="65220-106">Many learning algorithm bug fixes from MVP and community feedback.</span></span>

-   <span data-ttu-id="65220-107">Nový parametr - UpdateTemplate uložte výsledky algoritmus učení na komentář v souboru šablony.</span><span class="sxs-lookup"><span data-stu-id="65220-107">A new -UpdateTemplate parameter to save the results of the learning algorithm into a comment in the template file.</span></span> <span data-ttu-id="65220-108">Díky tomu learning zpracovat jednorázové náklady (nejpomalejší fáze).</span><span class="sxs-lookup"><span data-stu-id="65220-108">This makes the learning process (the slowest stage) a one-time cost.</span></span> <span data-ttu-id="65220-109">Spuštění převést řetězec pomocí šablony, která obsahuje algoritmus učení kódovaného je nyní téměř okamžité.</span><span class="sxs-lookup"><span data-stu-id="65220-109">Running Convert-String with a template that contains the encoded learning algorithm is now nearly instantaneous.</span></span>


<a name="extract-and-parse-structured-objects-out-of-string-content"></a><span data-ttu-id="65220-110">Extrahování a analyzovat strukturovaných objekty mimo obsah řetězce</span><span class="sxs-lookup"><span data-stu-id="65220-110">Extract and parse structured objects out of string content</span></span>
----------------------------------------------------------

<span data-ttu-id="65220-111">Ve spolupráci s [Microsoft Research](http://research.microsoft.com/), nový **ConvertFrom řetězec** rutiny byla přidána.</span><span class="sxs-lookup"><span data-stu-id="65220-111">In collaboration with [Microsoft Research](http://research.microsoft.com/), a new **ConvertFrom-String** cmdlet has been added.</span></span>

<span data-ttu-id="65220-112">Tato rutina podporuje dva režimy: basic oddělený analýzy a řízené příklad analýza automaticky generovány.</span><span class="sxs-lookup"><span data-stu-id="65220-112">This cmdlet supports two modes: basic delimited parsing, and auto generated example-driven parsing.</span></span>

<span data-ttu-id="65220-113">Analýza s oddělovači, ve výchozím nastavení, rozdělí vstupu v mezer a přiřadí názvy vlastností výsledné skupinám.</span><span class="sxs-lookup"><span data-stu-id="65220-113">Delimited parsing, by default, splits the input at white space, and assigns property names to the resulting groups.</span></span> <span data-ttu-id="65220-114">Oddělovač, který můžete upravit:</span><span class="sxs-lookup"><span data-stu-id="65220-114">You can customize the delimiter:</span></span>

> <span data-ttu-id="65220-115">1 \[C:\\temp\] &gt; &gt; "Hello World" | Řetězec ConvertFrom | Format-Table-automaticky</span><span class="sxs-lookup"><span data-stu-id="65220-115">1 \[C:\\temp\] &gt;&gt; "Hello World" | ConvertFrom-String | Format-Table -Auto</span></span>

<span data-ttu-id="65220-116">P1    P2</span><span class="sxs-lookup"><span data-stu-id="65220-116">P1    P2</span></span>
--    --

<span data-ttu-id="65220-117">Rutina podporuje také automaticky generovaný řízené příklad analýza na základě [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html) zkoumání práce v [Microsoft Research](http://research.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="65220-117">The cmdlet also supports auto-generated example-driven parsing based on the [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html) research work in [Microsoft Research](http://research.microsoft.com).</span></span>

<span data-ttu-id="65220-118">Chcete-li začít, zvažte založený na textu adresáře:</span><span class="sxs-lookup"><span data-stu-id="65220-118">To get started, consider a text-based address book:</span></span>

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

    Thomas Hardy

    Seattle, WA

    Christina Berglund

    Redmond, WA

    Hanna Moos

    Puyallup, WA

<span data-ttu-id="65220-119">Do souboru, který budete používat jako šablony zkopírujte několik příkladů:</span><span class="sxs-lookup"><span data-stu-id="65220-119">Copy a few examples into a file, which you will use as your template:</span></span>

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA



<span data-ttu-id="65220-120">Uveďte složené závorky kolem data, která mají být extrahovány, ho pojmenujete jako uděláte.</span><span class="sxs-lookup"><span data-stu-id="65220-120">Put curly braces around data that you want to extract, giving it a name as you do so.</span></span> <span data-ttu-id="65220-121">Protože **název** vlastnost (a jeho přidružené další vlastnosti) můžete zobrazit několikrát, použijte znak hvězdičky (\*) k označení, že to vede k více záznamů (ne extrahování bunch vlastností do jednoho záznam):</span><span class="sxs-lookup"><span data-stu-id="65220-121">Because the **Name** property (and its associated other properties) can appear multiple times, use an asterisk (\*) to indicate that this results in multiple records (rather than extracting a bunch of properties into one record):</span></span>

    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}

<span data-ttu-id="65220-122">Z této sady příklady **ConvertFrom řetězec** může nyní automaticky extrahovat na základě objektů výstup z vstupní soubory s podobnou strukturou.</span><span class="sxs-lookup"><span data-stu-id="65220-122">From this set of examples, **ConvertFrom-String** can now automatically extract object-based output from input files with similar structure.</span></span>

> <span data-ttu-id="65220-123">2 \[C:\\temp\]</span><span class="sxs-lookup"><span data-stu-id="65220-123">2 \[C:\\temp\]</span></span>
>
> <span data-ttu-id="65220-124">&gt;&gt; Get obsah. \\addresses.output.txt | Řetězec ConvertFrom - TemplateFile. \\addresses.template.txt | &gt; &gt; &gt; Format-Table-automaticky</span><span class="sxs-lookup"><span data-stu-id="65220-124">&gt;&gt; Get-Content .\\addresses.output.txt | ConvertFrom-String -TemplateFile .\\addresses.template.txt | &gt;&gt;&gt; Format-Table -Auto</span></span>
>
> <span data-ttu-id="65220-125">ExtentText název města stavu</span><span class="sxs-lookup"><span data-stu-id="65220-125">ExtentText                     Name               City     State</span></span>
> ----------                     ----               ----     -----
> <span data-ttu-id="65220-126">ANA Trujillo...                ANA Trujillo Redmond WA Antonio Moreno...              Antonio Moreno Renton WA Thomas Hardy...                Thomas Hardy Seattle WA Jana Berglund...          Jana Berglund Redmond WA Hanna Moos...                  Hanna Moos Puyallup WA</span><span class="sxs-lookup"><span data-stu-id="65220-126">Ana Trujillo...                Ana Trujillo       Redmond  WA Antonio Moreno...              Antonio Moreno     Renton   WA Thomas Hardy...                Thomas Hardy       Seattle  WA Christina Berglund...          Christina Berglund Redmond  WA Hanna Moos...                  Hanna Moos         Puyallup WA</span></span>

<span data-ttu-id="65220-127">Udělat manipulaci s daty další na extrahované textu **ExtentText** vlastnost zaznamená nezpracovaný text, ze kterého jste extrahovali záznamu.</span><span class="sxs-lookup"><span data-stu-id="65220-127">To do additional data manipulation on extracted text, the **ExtentText** property captures the raw text from which the record was extracted.</span></span> <span data-ttu-id="65220-128">K poskytnutí zpětné vazby o této funkci nebo pro sdílení obsahu, pro které máte potíže s zápis příklady, pošlete e-mail <psdmfb@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="65220-128">To provide feedback on this feature, or to share content for which you are having difficulty writing examples, please email <psdmfb@microsoft.com>.</span></span>

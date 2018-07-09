---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: fcf2adf67f36edb534df3e2a849459fb20e1c2de
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892349"
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a><span data-ttu-id="cc4cb-102">Extrakce a analýza strukturovaných objektů mimo řetězec</span><span class="sxs-lookup"><span data-stu-id="cc4cb-102">Extract and Parse Structured Objects out of String</span></span>

<span data-ttu-id="cc4cb-103">Také zavádí některé další funkce pro `ConvertFrom-String` rutiny:</span><span class="sxs-lookup"><span data-stu-id="cc4cb-103">This also introduces some additional functionality for the `ConvertFrom-String` cmdlet:</span></span>

- <span data-ttu-id="cc4cb-104">Ve výchozím nastavení odebere vlastnost text rozsahu.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-104">Removes the extent text property by default.</span></span> <span data-ttu-id="cc4cb-105">Můžete ho zahrnout s parametrem - IncludeExtent.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-105">You can include it with the -IncludeExtent parameter.</span></span>

- <span data-ttu-id="cc4cb-106">Mnoho učení algoritmu opravy chyb od MVP a komunity zpětnou vazbu.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-106">Many learning algorithm bug fixes from MVP and community feedback.</span></span>

- <span data-ttu-id="cc4cb-107">Nový parametr - UpdateTemplate uložit výsledky algoritmus učení do komentáře v souboru šablony.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-107">A new -UpdateTemplate parameter to save the results of the learning algorithm into a comment in the template file.</span></span> <span data-ttu-id="cc4cb-108">Díky tomu učení, zpracování (nejpomalejší fáze) jednorázové náklady.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-108">This makes the learning process (the slowest stage) a one-time cost.</span></span> <span data-ttu-id="cc4cb-109">Převést řetězec šablonou, která obsahuje algoritmu učení kódovaného se nyní téměř okamžité.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-109">Running Convert-String with a template that contains the encoded learning algorithm is now nearly instantaneous.</span></span>

## <a name="extract-and-parse-structured-objects-out-of-string-content"></a><span data-ttu-id="cc4cb-110">Extrakce a analýza strukturovaných objektů mimo řetězec obsahu</span><span class="sxs-lookup"><span data-stu-id="cc4cb-110">Extract and parse structured objects out of string content</span></span>

<span data-ttu-id="cc4cb-111">Ve spolupráci s [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F), nový `ConvertFrom-String` rutiny se přidala.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-111">In collaboration with [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F), a new `ConvertFrom-String` cmdlet has been added.</span></span>

<span data-ttu-id="cc4cb-112">Tato rutina podporuje dva režimy: basic s oddělovači, analýze a příklad řízené analýze automaticky generovány.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-112">This cmdlet supports two modes: basic delimited parsing, and auto generated example-driven parsing.</span></span>

<span data-ttu-id="cc4cb-113">Analýza s oddělovači, ve výchozím nastavení, rozdělí vstupu v prázdné znaky a přiřadí názvy vlastností výsledné skupiny.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-113">Delimited parsing, by default, splits the input at white space, and assigns property names to the resulting groups.</span></span> <span data-ttu-id="cc4cb-114">Můžete přizpůsobit oddělovač:</span><span class="sxs-lookup"><span data-stu-id="cc4cb-114">You can customize the delimiter:</span></span>

```powershell
"Hello World" | ConvertFrom-String | Format-Table -Auto
```

```output
P1     P2
--     --
Hello  World
```

<span data-ttu-id="cc4cb-115">Rutina podporuje také automaticky generované řízené příklad analýza kódu na základě [FlashExtract](https://www.microsoft.com/en-us/research/publication/flashextract-framework-data-extraction-examples/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fsumitg%2Fflashextract.html) výzkum práce v [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F).</span><span class="sxs-lookup"><span data-stu-id="cc4cb-115">The cmdlet also supports auto-generated example-driven parsing based on the [FlashExtract](https://www.microsoft.com/en-us/research/publication/flashextract-framework-data-extraction-examples/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fsumitg%2Fflashextract.html) research work in [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F).</span></span>

<span data-ttu-id="cc4cb-116">Abyste mohli začít, vezměte v úvahu založený na textu adresář:</span><span class="sxs-lookup"><span data-stu-id="cc4cb-116">To get started, consider a text-based address book:</span></span>

```
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
```

<span data-ttu-id="cc4cb-117">Kopírovat do souboru, který budete používat jako šablona pár příkladů:</span><span class="sxs-lookup"><span data-stu-id="cc4cb-117">Copy a few examples into a file, which you will use as your template:</span></span>

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA
```

<span data-ttu-id="cc4cb-118">Umístěte složené závorky kolem data, která mají být extrahovány, zadání názvu jako uděláte.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-118">Put curly braces around data that you want to extract, giving it a name as you do so.</span></span> <span data-ttu-id="cc4cb-119">Protože **název** vlastnosti (a jeho spojené další vlastnosti) může objevit víckrát, použijte hvězdičku (\*) k označení, výsledkem je, že několik záznamů (spíše než extrahování spoustu vlastností do jednoho záznam):</span><span class="sxs-lookup"><span data-stu-id="cc4cb-119">Because the **Name** property (and its associated other properties) can appear multiple times, use an asterisk (\*) to indicate that this results in multiple records (rather than extracting a bunch of properties into one record):</span></span>

```
    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}
```

<span data-ttu-id="cc4cb-120">Z této sady příklady `ConvertFrom-String` můžete teď automaticky extrahovat založenou na objektech výstupu ze vstupních souborů s podobnou strukturou.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-120">From this set of examples, `ConvertFrom-String` can now automatically extract object-based output from input files with similar structure.</span></span>

```powershell
Get-Content .\addresses.output.txt | ConvertFrom-String -TemplateFile .\addresses.template.txt | Format-Table -Auto
```

```output
ExtentText                     Name               City     State
----------                     ----               ----     -----
Ana Trujillo...                Ana Trujillo       Redmond  WA
Antonio Moreno...              Antonio Moreno     Renton   WA
Thomas Hardy...                Thomas Hardy       Seattle  WA
Christina Berglund...          Christina Berglund Redmond  WA
Hanna Moos...                  Hanna Moos         Puyallup WA
```

<span data-ttu-id="cc4cb-121">Provádět manipulace s daty další na byl extrahován text **ExtentText** vlastnost zachycuje nezpracovaný text, ze které byl extrahován záznamu.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-121">To do additional data manipulation on extracted text, the **ExtentText** property captures the raw text from which the record was extracted.</span></span> <span data-ttu-id="cc4cb-122">Chcete poskytnout zpětnou vazbu o této funkci nebo sdílet obsah, pro kterou máte potíže zápis příklady prosím e-mail <psdmfb@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="cc4cb-122">To provide feedback on this feature, or to share content for which you are having difficulty writing examples, please email <psdmfb@microsoft.com>.</span></span>
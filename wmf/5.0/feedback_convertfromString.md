---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 3413672e73705252225300a853c10a514500baa2
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a>Extrakce a analyzovat strukturovaných objekty z řetězce
Vzniká některé další funkce pro rutinu ConvertFrom řetězec:

-   Odebere rozsah vlastnost text ve výchozím nastavení. Můžete vytvořit s parametrem - IncludeExtent.

-   Mnoho učení algoritmu opravy chyb z MVP a komunity zpětnou vazbu.

-   Nový parametr - UpdateTemplate uložte výsledky algoritmus učení na komentář v souboru šablony. Díky tomu learning zpracovat jednorázové náklady (nejpomalejší fáze). Spuštění převést řetězec pomocí šablony, která obsahuje algoritmus učení kódovaného je nyní téměř okamžité.


<a name="extract-and-parse-structured-objects-out-of-string-content"></a>Extrahování a analyzovat strukturovaných objekty mimo obsah řetězce
----------------------------------------------------------

Ve spolupráci s [Microsoft Research](http://research.microsoft.com/), nový **ConvertFrom řetězec** rutiny byla přidána.

Tato rutina podporuje dva režimy: basic oddělený analýzy a řízené příklad analýza automaticky generovány.

Analýza s oddělovači, ve výchozím nastavení, rozdělí vstupu v mezer a přiřadí názvy vlastností výsledné skupinám. Oddělovač, který můžete upravit:

> 1 \[C:\\temp\] &gt; &gt; "Hello World" | Řetězec ConvertFrom | Format-Table-automaticky

P1    P2
--    --

Rutina podporuje také automaticky generovaný řízené příklad analýza na základě [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html) zkoumání práce v [Microsoft Research](http://research.microsoft.com).

Chcete-li začít, zvažte založený na textu adresáře:

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

Do souboru, který budete používat jako šablony zkopírujte několik příkladů:

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

   

Uveďte složené závorky kolem data, která mají být extrahovány, ho pojmenujete jako uděláte. Protože **název** vlastnost (a jeho přidružené další vlastnosti) můžete zobrazit několikrát, použijte znak hvězdičky (\*) k označení, že to vede k více záznamů (ne extrahování bunch vlastností do jednoho záznam):

    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}

Z této sady příklady **ConvertFrom řetězec** může nyní automaticky extrahovat na základě objektů výstup z vstupní soubory s podobnou strukturou.

> 2 \[C:\\temp\]
>
> &gt;&gt; Get obsah. \\addresses.output.txt | Řetězec ConvertFrom - TemplateFile. \\addresses.template.txt | &gt; &gt; &gt; Format-Table-automaticky
>
> ExtentText název města stavu
> ----------                     ----               ----     -----
> Ana Trujillo...                ANA Trujillo Redmond WA Antonio Moreno...              Antonio Moreno Renton WA Thomas Hardy...                Thomas Hardy Seattle WA Jana Berglund...          Jana Berglund Redmond WA Hanna Moos...                  Hanna Moos Puyallup WA

Udělat manipulaci s daty další na extrahované textu **ExtentText** vlastnost zaznamená nezpracovaný text, ze kterého jste extrahovali záznamu. K poskytnutí zpětné vazby o této funkci nebo pro sdílení obsahu, pro které máte potíže s zápis příklady, pošlete e-mail <psdmfb@microsoft.com>.


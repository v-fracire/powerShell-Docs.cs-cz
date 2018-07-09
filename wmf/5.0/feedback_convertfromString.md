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
# <a name="extract-and-parse-structured-objects-out-of-string"></a>Extrakce a analýza strukturovaných objektů mimo řetězec

Také zavádí některé další funkce pro `ConvertFrom-String` rutiny:

- Ve výchozím nastavení odebere vlastnost text rozsahu. Můžete ho zahrnout s parametrem - IncludeExtent.

- Mnoho učení algoritmu opravy chyb od MVP a komunity zpětnou vazbu.

- Nový parametr - UpdateTemplate uložit výsledky algoritmus učení do komentáře v souboru šablony. Díky tomu učení, zpracování (nejpomalejší fáze) jednorázové náklady. Převést řetězec šablonou, která obsahuje algoritmu učení kódovaného se nyní téměř okamžité.

## <a name="extract-and-parse-structured-objects-out-of-string-content"></a>Extrakce a analýza strukturovaných objektů mimo řetězec obsahu

Ve spolupráci s [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F), nový `ConvertFrom-String` rutiny se přidala.

Tato rutina podporuje dva režimy: basic s oddělovači, analýze a příklad řízené analýze automaticky generovány.

Analýza s oddělovači, ve výchozím nastavení, rozdělí vstupu v prázdné znaky a přiřadí názvy vlastností výsledné skupiny. Můžete přizpůsobit oddělovač:

```powershell
"Hello World" | ConvertFrom-String | Format-Table -Auto
```

```output
P1     P2
--     --
Hello  World
```

Rutina podporuje také automaticky generované řízené příklad analýza kódu na základě [FlashExtract](https://www.microsoft.com/en-us/research/publication/flashextract-framework-data-extraction-examples/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fsumitg%2Fflashextract.html) výzkum práce v [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F).

Abyste mohli začít, vezměte v úvahu založený na textu adresář:

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

Kopírovat do souboru, který budete používat jako šablona pár příkladů:

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA
```

Umístěte složené závorky kolem data, která mají být extrahovány, zadání názvu jako uděláte. Protože **název** vlastnosti (a jeho spojené další vlastnosti) může objevit víckrát, použijte hvězdičku (\*) k označení, výsledkem je, že několik záznamů (spíše než extrahování spoustu vlastností do jednoho záznam):

```
    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}
```

Z této sady příklady `ConvertFrom-String` můžete teď automaticky extrahovat založenou na objektech výstupu ze vstupních souborů s podobnou strukturou.

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

Provádět manipulace s daty další na byl extrahován text **ExtentText** vlastnost zachycuje nezpracovaný text, ze které byl extrahován záznamu. Chcete poskytnout zpětnou vazbu o této funkci nebo sdílet obsah, pro kterou máte potíže zápis příklady prosím e-mail <psdmfb@microsoft.com>.
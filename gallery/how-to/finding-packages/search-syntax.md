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
# <a name="gallery-search-syntax"></a>Syntaxe hledání v galerii

Galerie prostředí PowerShell nabízí searchbox text, ve kterém můžete použít slova, fráze a výrazy – klíčové slovo můžete zúžit výsledky hledání.

## <a name="search-by-keywords"></a>Hledat podle klíčových slov

    dsc azure sql

Vyhledávání bude dělat jeho pokusí najít relevantní dokumenty, které obsahují všechna klíčová slova 3 a vrátí odpovídající dokumenty.

## <a name="search-using-phrases-and-keywords"></a>Vyhledávání pomocí klíčových slov a vět

    "azure sql" deployment

Zadání slovní spojení mezi uvozovky ("") změňte parametry hledání, mají hledat konkrétní fráze místo samostatných klíčová slova.
Odpovídajících dokumentů by měl obvykle obsahují přesnou frázi "azure sql", včetně například varianty malá a velká písmena "Azure SQL" a také obvykle obsahovat slovo "nasazení".

## <a name="filtering-on-fields"></a>Filtrování podle polí

Můžete hledat pro určitý balíček ID (nebo "Id" nebo "id") nebo některých polí přidáním prefixu hledané termíny název pole.

Aktuálně jsou prohledávatelná pole 'Id', 'Version', 'Značky', "Autor", "Vlastník", "Funkce", 'Rutiny', "DscResources" a "Verze".

[Jaký je rozdíl mezi ID a název? ID je název, který používáte v konzole. Název je, jak je zobrazeno v horní části na stránce balíček ve výsledcích hledání.]

## <a name="examples"></a>Příklady

    ID:"PSReadline"
    id:"AzureRM.Profile"

Vyhledá balíčky s "PSReadline" nebo "AzureRM.Profile" v jejich pole ID v uvedeném pořadí.

    Id:"AzureRM.Profile"

je další způsob, jak vyhledat balíčky s "AzureRM.Profile" v jejich pole ID.

Filtr "Id" je dílčí řetězec shodovat, tak při hledání následující:

    Id:"azure"

Zobrazí se výsledky, jako jsou "AzureRM.Profile" a "Azure.Storage".

Můžete také vyhledat více klíčových slov do jednoho pole. Nebo kombinovat a Párovat pole.

    id:azure tags:intellisense
    id:azure id:storage

A můžete provádět vyhledávání frází:

    id:"azure.storage"


K vyhledání všech balíčků značkou DSC.

    Tags:"DSC"

K vyhledání všech balíčků pomocí zadané funkce.

    Functions:"Update-AzureRM"

K vyhledání všech balíčků pomocí zadaného rutiny.

    Cmdlets:"Get-AzureRmEnvironment"

K vyhledání všech balíčků se zadaným názvem prostředku DSC.

    DscResources:"xArchive"

K vyhledání všech balíčků pomocí zadané verze prostředí PowerShell

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


Nakonec pokud používáte pole, které nepodporujeme, jako je například "příkazy", vytvoříme právě ho ignorovat a hledat všechna pole. Proto následující dotaz

    commands:blobs storage

Je interpretován stejně jako tento dotaz:

    blobs storage

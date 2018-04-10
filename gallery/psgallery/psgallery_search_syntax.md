---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: psgallery_search_syntax
ms.openlocfilehash: 337b4b1e702994fcbc456eb31a2d8632f5220d09
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="gallery-search-syntax"></a>Syntaxe vyhledávání Galerie

Galerie prostředí PowerShell nabízí text searchbox, kde můžete použít slova, frází a výrazy – klíčové slovo Chcete-li zúžit výsledky vyhledávání.

## <a name="search-by-keywords"></a>Vyhledávání podle klíčových slov

    dsc azure sql

Hledání se provést jeho usilovně najít relevantní dokumenty obsahující všechny 3 klíčová slova a vrátí odpovídající dokumenty.

## <a name="search-using-phrases-and-keywords"></a>Vyhledávání pomocí klíčových slov a frází

    "azure sql" deployment

Zadání slovní spojení mezi znaky uvozovek ("") změňte parametry hledání a hledat konkrétní frázi místo samostatné klíčová slova.
Odpovídající dokumenty by měl obvykle obsahují přesný řetězec "azure sql", například včetně varianty malá a velká písmena "Azure SQL" a také obvykle obsahovat slovo 'nasazení'.

## <a name="filtering-on-fields"></a>Filtrování na pole

Můžete vyhledat konkrétní položku ID (nebo 'Id' nebo 'id'), nebo určitá pole pomocí prefixu vyhledávání podmínky název pole.

Aktuálně jsou prohledávatelné pole 'Id', 'Version', 'Značky', 'Vytvořit', "Vlastník", "Funkce", 'Rutiny', 'DscResources' a 'verze prostředí PowerShell.

[Jaký je rozdíl mezi ID a název? ID je název, který používáte v konzole. Název je co se zobrazí v horní části stránky položky ve výsledcích hledání.]

## <a name="examples"></a>Příklady

    ID:"PSReadline"
    id:"AzureRM.Profile"

Vyhledá položky "PSReadline" nebo "AzureRM.Profile" v jejich ID pole v uvedeném pořadí.

    Id:"AzureRM.Profile"

je další způsob hledání položek s "AzureRM.Profile" v jejich ID pole.

Filtr 'Id' je dílčí řetězec shodují, tak pokud hledáte následující:

    Id:"azure"

Získáte výsledky jako 'AzureRM.Profile' a 'Azure.Storage'.

Můžete také prohledat několik klíčových slov do jednoho pole. Nebo kombinovat a Párovat pole.

    id:azure tags:intellisense
    id:azure id:storage

A můžete provádět vyhledávání frázi:

    id:"azure.storage"


K vyhledání všech položek s DSC značkou.

    Tags:"DSC"

Chcete-li vyhledat všechny položky se zadanou funkcí.

    Functions:"Update-AzureRM"

K vyhledání všech položek s zadanou rutinu.

    Cmdlets:"Get-AzureRmEnvironment"

Chcete-li vyhledat všechny položky se zadaným názvem prostředek DSC.

    DscResources:"xArchive"

K vyhledání všech položek, zadaná verze prostředí PowerShell

    PowerShellVersion:"5.0"
    PowerShellVersion:"3.0"
    PowerShellVersion:"2.0"


Nakonec pokud používáte pole, které nepodporujeme, například "příkazů, jsme budete právě ho ignorovat a hledání všechna pole. Proto tyto dotazu

    commands:blobs storage

Je interpretovat stejně jako tento dotaz:

    blobs storage
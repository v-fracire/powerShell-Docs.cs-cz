---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_items_tab
ms.openlocfilehash: 8704091542de5c19817ab0b4f77fd98987084b5d
ms.sourcegitcommit: 1a0a0928c1e3cae4e8df8d79b0737bd7ed6b4e47
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2017
---
# <a name="items-tab"></a>Karta položky

[Karta položky](https://www.powershellgallery.com/items) zobrazí všechny položky k dispozici v galerii prostředí PowerShell.

Existuje několik způsobů k filtrování, řazení a vyhledávání položek.
Pokud chcete zobrazit další podrobnosti o konkrétní položky, klikněte na položku.

## <a name="filter-by"></a>Filtrovat podle

Rozevírací seznam v části "Filtrovat podle" umožňuje uživatelům filtrovat výsledky podle:
* Zahrnout předběžné verze
* Pouze ustájení

Informace o "předběžné verze" a "Stabilní" najdete v tématu [předběžné verze Správa verzí přidat do PowerShellGet a Galerie prostředí PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) v blogu týmu prostředí PowerShell.

Zaškrtávací políčka v rozevíracím seznamu umožňují uživatelům filtrovat výsledky podle:
* Typy položek
  - Modul
  - Skript
* Kategorie
  - Rutina
  - Prostředek DSC
  - Funkce
  - Funkce role
  - pracovní postup

Pokud chcete zobrazit jenom moduly v galerii prostředí PowerShell, zkontrolujte modulu v typů položek.
Podobně zobrazí jenom skripty v galerii prostředí PowerShell, zkontrolujte skript v typů položek.

> [!NOTE]
> Filtry jsou inkluzivní.
> Příklad: Položky obsahující rutiny a funkce se zobrazí, pokud jsou zaškrtnutá políčka buď rutiny nebo funkci (nebo obě).
> Pokud ani jeden z nich jsou vybrané, nebude se zobrazovat položky.
> Podobně pokud jsou vybrané všechny kategorie, se zobrazí pouze položky obsahující jednu z těchto kategorií.
> **Položky, které nepatří do žádné z těchto kategorií se nezobrazí.**

## <a name="sort-by"></a>Řadit podle

Seřadit podle rozevíracího seznamu umožňuje uživatelům výsledky seřaďte podle:
* Oblíbenosti - oblíbenosti je určen podle počtu stažení
* A-Z – abecedně podle názvu položky
* Poslední - položky se zobrazí v pořadí podle data publikování

## <a name="search-box"></a>Pole pro vyhledávání

Do vyhledávacího pole umožňuje uživatelům vyhledávat položky klíčová slova.
Další informace najdete v tématu [syntaxe vyhledávání Galerie](psgallery_search_syntax.md).

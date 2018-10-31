---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Filtrování výsledků hledání
ms.openlocfilehash: 13270a310613a974e1588a9f56d443a936cfebb8
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004032"
---
# <a name="filtering-search-results"></a>Filtrování výsledků hledání

[Balíčky kartu](https://www.powershellgallery.com/packages) zobrazuje všechny dostupné balíčky v galerii prostředí PowerShell.

Existuje několik způsobů filtrování, řazení a vyhledávání balíčků.
Pokud chcete zobrazit další podrobnosti o konkrétního balíčku, klikněte na balíček.

## <a name="filter-by"></a>Filtrovat podle

Rozevírací seznam v části "Filtrovat podle" umožňuje filtrovat výsledky podle:
- Zahrnout předběžné verze
- Pouze stabilní verze

Informace o "předběžné verze" a "Stálé" v tématu [předběžné verze správy verzí přidat do Správce balíčků PowerShellGet a Galerie prostředí PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/) na blogu týmu prostředí PowerShell.

Zaškrtávací políčka v rozevíracího seznamu umožňují uživatelům výsledky filtrovat podle:
- Typy balíčků
  - Modul
  - Skript
- Kategorie
  - Rutina
  - Prostředek DSC
  - Funkce
  - Funkce rolí
  - Pracovní postup

Pokud chcete zobrazit pouze moduly v galerii prostředí PowerShell, zkontrolujte modulu v typy balíčků.
Podobně najdete v článku pouze skripty v galerii prostředí PowerShell, zkontrolujte skript v typy balíčků.

> [!NOTE]
> Filtry jsou inkluzivní.
> Příklad: Balíček, který obsahuje rutiny a funkce se zobrazí, pokud jsou kontrolovány buď rutina – funkce (nebo obojí).
> Pokud ani jedno, nezobrazí se balíček.
> Podobně pokud jsou vybrány všechny kategorie, se zobrazí pouze balíčky obsahující jednu z těchto kategorií.
> **Balíčky, které nepatří do žádné z těchto kategorií se nezobrazí.**

## <a name="sort-by"></a>Seřadit podle:

Řadit podle rozevíracího seznamu umožňuje seřadit výsledky podle:
- Popularita - popularita se určuje podle počtu stažení
- A-Z - abecedně podle názvu balíčku
- Poslední - balíčky zobrazí v pořadí datum publikování

## <a name="search-box"></a>Vyhledávací pole

Do vyhledávacího pole umožňuje uživatelům vyhledávání balíčků na klíčová slova.
Další informace najdete v tématu [syntaxe hledání v galerii](search-syntax.md).

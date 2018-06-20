---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Položky s kompatibilní verze prostředí PowerShell
ms.openlocfilehash: f661c2cd076acb9c11394ba0b752ebd154965ff4
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189495"
---
# <a name="items-with-compatible-powershell-editions"></a>Položky s kompatibilní verze prostředí PowerShell

Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.

- **Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.
- **Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-items-compatible-for-specific-powershell-editions"></a>Galerie prostředí PowerShell extrahuje podporované PSEditions metadata a umožňuje filtry položky kompatibilní pro konkrétní edice prostředí PowerShell

Pokud má položka kompatibilní PSEditions zadané, budou uvedené jako součást 'prostředí PowerShell edice, na stránce položky zobrazení a také ve výsledcích položky.

![Stránka zobrazení položky s PSEditions](../../Images/ItemDisplayPageWithPSEditions.PNG)

## <a name="search-for-items-in-the-gallery-ui-which-works-on-powershellcore"></a>Hledání položek v galerii uživatelského rozhraní, který pracuje na PowerShellCore

Použití značek: značky a "PSEdition_Desktop": "PSEdition_Core" filtrů prostřednictvím položky z Galerie prostředí PowerShell.

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>Použití značek: "PSEdition_Core" k vyhledání položek, které jsou kompatibilní s edicí základní prostředí PowerShell.

![Výsledky hledání pro položky, které jsou kompatibilní s PSEdition jádra](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>Použití značek: "PSEdition_Desktop" k vyhledání položek, které jsou kompatibilní s edicí plochy prostředí PowerShell.

![Výsledky hledání pro položky, které jsou kompatibilní s PSEdition plochy](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-items-with-compatible-powershell-editions"></a>Další informace o vytváření a hledání položek s kompatibilní verze prostředí PowerShell

- [Moduly s PSEditions](../../concepts/module-psedition-support.md)
- [Skripty s PSEditions](../../concepts/script-psedition-support.md)
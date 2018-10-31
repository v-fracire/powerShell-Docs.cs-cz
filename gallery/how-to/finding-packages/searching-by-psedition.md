---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Balíčky s kompatibilní edice Powershellu
ms.openlocfilehash: e16cfb0ee30e344c9399bec2985baafc5a252fd7
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004012"
---
# <a name="packages-with-compatible-powershell-editions"></a>Balíčky s kompatibilní edice Powershellu

Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.

- **Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.
- **Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-packages-compatible-for-specific-powershell-editions"></a>Extrahuje metadata podporované PSEditions Galerie prostředí PowerShell a umožňuje filtry balíčky kompatibilní pro konkrétní edice Powershellu

Pokud balíček nemá kompatibilní PSEditions zadán, budou uvedené jako součást 'Edice Powershellu' ve stránce balíček pro zobrazení a také ve výsledcích balíčky.

![Položka zobrazení stránky s PSEditions](../../Images/manual_package_download.png)

## <a name="search-for-packages-in-the-gallery-ui-which-works-on-powershellcore"></a>Vyhledat balíčky v galerii uživatelského rozhraní, který pracuje na PowerShellCore

Použití značek: "PSEdition_Desktop" a značky: "PSEdition_Core" filtrům balíčky v galerii prostředí PowerShell.

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>Použití značek: "PSEdition_Core" k vyhledání položek, které jsou kompatibilní s PowerShell Core Edition.

![Výsledky hledání pro položky, které jsou kompatibilní s Core PSEdition](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>Použití značek: "PSEdition_Desktop" k vyhledání položek, které jsou kompatibilní s Powershellu Desktop Edition.

![Výsledky hledání pro položky, které jsou kompatibilní s Desktop PSEdition](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a>Další informace o vytváření a hledání balíčky s kompatibilní edice Powershellu

- [Moduly s PSEditions](../../concepts/module-psedition-support.md)
- [Skripty s PSEditions](../../concepts/script-psedition-support.md)

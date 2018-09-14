---
ms.date: 09/11/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, psgallery
title: Ruční balíček ke stažení
ms.openlocfilehash: 7d228ccea9b840e4850d03a7a2e3e1c71e11d95e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523310"
---
# <a name="manual-package-download"></a>Ruční balíček ke stažení

Galerie prostředí Powershell podporuje stahování balíčku z webu přímo, bez použití rutiny Správce balíčků PowerShellGet. Balíček se stáhne jako soubor balíčku (.nupkg) NuGet, který je pak snadno zkopírovat do interní úložiště.

> [!NOTE]
> Stažení balíčku ruční **není** určené jako náhrada za rutinu Install-Module.
> Stahuje se balíček nenainstaluje modulu nebo skriptu. Závislosti nejsou zahrnuté do balíčku NuGet stáhli. Následující pokyny jsou k dispozici pouze pro referenční účely.

## <a name="using-manual-download-to-acquire-a-package"></a>Získat balíček pomocí ruční stažení

Každá stránka obsahuje odkaz pro ruční stažení, jak je znázorněno zde:

![Ruční stažení](../../Images/Manual_Item_Download.PNG)

Pokud chcete stáhnout ručně, klikněte na **stáhnout soubor nupkg nezpracovaná**. Kopii balíčku zkopírován do složky pro stahování pro váš prohlížeč s názvem `<name>.<version>.nupkg`.

Balíček NuGet je archiv ZIP s další soubory, které obsahují informace o obsahu balíčku. Některé prohlížeče, jako třeba Internet Explorer, automaticky nahradit `.nupkg` s příponou souboru `.zip`. Rozbalte balíček, přejmenujte je tak `.nupkg` soubor `.zip`, v případě potřeby extrahujte obsah do místní složky.

Soubor balíčku NuGet obsahuje následující prvky specifické pro NuGet, které nejsou součástí původní zabaleného kódu:

- Složka s názvem `_rels` – obsahuje `.rels` soubor, který obsahuje seznam závislostí
- Složka s názvem `package` -obsahuje data specifická pro NuGet
- Soubor s názvem `[Content_Types].xml` – popisuje, jak rozšíření, jako je Správce balíčků PowerShellGet fungují s NuGet
- Soubor s názvem `<name>.nuspec` – obsahuje hromadně metadat

## <a name="installing-powershell-modules-from-a-nuget-package"></a>Instalace modulů Powershellu z balíčku NuGet

> [!NOTE]
> Tyto pokyny **neměňte** poskytují stejný výsledek jako spuštění `Install-Module`. Tyto pokyny splňovat minimální požadavky. Nejsou určeny k jako náhrada za `Install-Module`. Některé kroky prováděné `Install-Module` nejsou zahrnuty.

Nejjednodušší způsob je NuGet specifické prvky odeberete ze složky. Kvůli tomu Powershellu kód vytvořený pomocí autora balíčku. Tyto kroky jsou:

1. Extrahujte obsah balíčku NuGet do místní složky.
2. Odstraňte NuGet specifické prvky ze složky.
3. Přejmenujte složku. Výchozí název složky je obvykle `<name>.<version>`. Verze může obsahovat "-předprodejní" Pokud modul je označený jako zkušební verzi. Přejmenujte složku pouze na název modulu. Například "azurerm.storage.5.0.4 ve verzi preview" se změní na "azurerm.storage".
4. Zkopírujte složku pro váš PSModulePath.

> [!IMPORTANT]
> Ruční stažení neobsahuje žádné závislosti, které vyžaduje modulem. Pokud balíček obsahuje závislosti, musí být nainstalovány v systému pro tento modul fungovat správně. Galerie prostředí PowerShell ukazuje všechny závislosti, které vyžaduje balíček.

## <a name="installing-powershell-scripts-from-a-nuget-package"></a>Instalace Powershellové skripty z balíčku NuGet

> [!NOTE]
> Tyto pokyny **neměňte** poskytují stejný výsledek jako spuštění `Install-Script`. Tyto pokyny splňovat minimální požadavky. Nejsou určeny k jako náhrada za `Install-Script`.

Nejjednodušší způsob je přímo extrahovat balíček NuGet a pak pomocí skriptu. Tyto kroky jsou:

1. Extrahujte obsah balíčku NuGet.
2. `.PS1` Soubor ve složce můžete použít přímo z tohoto umístění.
3. Můžete odstranit prvky specifické pro NuGet ve složce.

> [!IMPORTANT]
> Ruční stažení neobsahuje žádné závislosti, které vyžaduje modulem. Pokud balíček obsahuje závislosti, musí být nainstalovány v systému pro tento modul fungovat správně. Galerie prostředí PowerShell ukazuje všechny závislosti, které vyžaduje balíček.

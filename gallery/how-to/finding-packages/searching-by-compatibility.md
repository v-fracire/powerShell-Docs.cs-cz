---
ms.date: 12/11/2018
contributor: JKeithB, SydneyhSmith
keywords: Galerie prostředí powershell, rutina, psgallery
title: Balíčky s kompatibilní operační systém nebo edice Powershellu
ms.openlocfilehash: 8230866561d3021379a48cc2c83fb4104a4058c1
ms.sourcegitcommit: d396d0e4cfe3d279f399c17e7337380a31d373ac
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2018
ms.locfileid: "53747700"
---
# <a name="packages-with-compatible-powershell-editions-or-operating-systems"></a>Balíčky s kompatibilní edice Powershellu nebo operační systémy

Od verze 5.1, prostředí PowerShell je k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibility platformy.

## <a name="searching-by-powershell-edition"></a>Vyhledávání podle edice Powershellu 
Edice powershellu jsou:
- **Desktop Edition:** Založený na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na plných edicích Windows, jako je jádro serveru a Windows Desktop.
- **Core Edition:** Založená na prostředí .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na edicích Windows, jako je Nano Server a Windows IoT nízké nároky.

### <a name="powershell-gallery-allows-you-to-filter-packages-compatible-for-specific-powershell-editions"></a>Galerie prostředí PowerShell vám umožní filtrovat kompatibilní balíčků pro konkrétní edice Powershellu

Pokud balíček nemá kompatibilní PSEditions zadán, jsou uvedeny jako součást 'Edice Powershellu' ve stránce balíček pro zobrazení a také ve výsledcích balíčky.
Můžete také vyhledat kompatibilní balíčků pomocí prostředí PowerShell.

![Položka zobrazení stránky s PSEditions](../../Images/packagedisplaypagewithpseditions.PNG)

### <a name="search-for-packages-in-the-gallery-ui-that-work-on-powershell-core"></a>Vyhledat balíčky v galerii uživatelského rozhraní, které fungují v prostředí PowerShell Core

Použití značek: "PSEdition_Desktop" a značky: "PSEdition_Core" filtrům balíčky v galerii prostředí PowerShell.

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>Použití značek: "PSEdition_Core" k vyhledání položek, které jsou kompatibilní s PowerShell Core Edition.

![Výsledky hledání pro položky, které jsou kompatibilní s Core PSEdition](../../Images/searchresultswithpseditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>Použití značek: "PSEdition_Desktop" k vyhledání položek, které jsou kompatibilní s Powershellu Desktop Edition.

![Výsledky hledání pro položky, které jsou kompatibilní s Desktop PSEdition](../../Images/searchresultswithpseditionsdesktop.PNG)

### <a name="search-for-packages-to-find-compatible-editions-using-powershell"></a>Hledat balíčky a najděte kompatibilní edice powershellu
Můžete zadat značky, chcete-li filtrovat edice Powershellu a operačního systému. Můžete použít `Find-Package` zadáním rutiny `-Tag` parametr k určení edition (a operačního systému) cílíte.
Nějak tak:

```powershell
# Find modules compatible with PowerShell Core:
Find-Module -Tag PSEdition_Core

# Find modules compatible with PowerShell Core on Linux:
Find-Module -Tag PSEdition_Core, Linux
```

## <a name="searching-by-operating-system"></a>Hledání podle operačního systému 

PowerShell Core je k dispozici pro Windows, Linux a MacOS, mohou být balíčky v galerii navrženy pro libovolnou kombinaci těchto operačních systémů. V galerii uživatelského rozhraní pomocí následujících značek searchs najít balíčků označené podle operačního systému:

- Značky: "Windows"
- Značky: "Linux"
- Značky: "MacOS" 

Určíte tyto značky na `Find-Module` (a další rutiny v modulu PowerShellGet) tímto způsobem:

```powershell
# Find Modules compatible with Windows
Find-Module -Tag Linux
```

## <a name="searching-for-multiple-compatibilities"></a>Vyhledávání pro více kompatibility

Můžete vyhledat balíček, který má více kompatibility pomocí syntaxe: 

Značky: "Compatibility1" "Compatibility2" 

Například pokud chcete pro balíček díky PowerShell Core, která běží na počítačích Moje Windows i Linuxem, použijte vyhledávací značky:

Značky: "PSEdition_Core" "Windows" "Linux" 

Hledání s použitím prostředí PowerShell, můžete použít `Find-Module` (a další rutiny v modulu PowerShellGet) tímto způsobem:

```powewrshell
# Find scripts compatible with PowerShell Core, Windows, and Linux
Find-Script -Tag PSEdition_Core,Linux,Windows

# Find modules compatible with PowerSHellCore and MacOS
Find-Module -Tag PSEdition_Core,MacOS
```

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a>Další informace o vytváření a hledání balíčky s kompatibilní edice Powershellu

- [Moduly s PSEditions](../../concepts/module-psedition-support.md)
- [Skripty s PSEditions](../../concepts/script-psedition-support.md)

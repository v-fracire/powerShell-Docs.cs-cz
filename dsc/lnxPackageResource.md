---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: DSC pro Linux nxPackage prostředků
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218701"
---
# <a name="dsc-for-linux-nxpackage-resource"></a>DSC pro Linux nxPackage prostředků

**NxPackage** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě balíčků na uzlu Linux.

## <a name="syntax"></a>Syntaxe

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| Název| Název balíčku, pro které chcete zajistit určitý stav.|
| Ujistěte se| Určuje, jestli se má zkontrolovat, zda balíček existuje. Nastavením této vlastnosti "Přítomen" zajistěte, aby byl že balíček existuje. Nastavte ji na "Chybí" zajistěte, aby byl že balíček neexistuje. Výchozí hodnota je "Dispozici".|
| PackageManager| Podporované hodnoty jsou "yum", "výstižný" a "zypper". Určuje Správce balíčků, které chcete použít při instalaci balíčků. Pokud **FilePath** je zadán, že zadaná cesta se použije k instalaci balíčku. Správce balíčků, jinak hodnota použije k instalaci balíčku z předem nakonfigurovaná úložiště. Pokud ani **PackageManager** ani **FilePath** součástí jsou výchozí Správce balíčků pro systém, který se použije.|
| Cesta k souboru| Cesta k souboru, ve kterém se nachází balíček|
| PackageGroup| Pokud **$true**, **název** musí být název skupiny balíček pro použití s **PackageManager**. **PacakgeGroup** není platný při poskytování **FilePath**.|
| Argumenty| Řetězec argumenty, které se předá do balíčku přesně tak, jak zadat.|
| ReturnCode| Očekávaný návratový kód. Pokud skutečnou návratový kód neodpovídá očekávané hodnotě zadané tady že konfigurace vrátí chybu.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Následující příklad zajistí, že balíček s názvem "httpd" je nainstalovat na počítač se systémem Linux, pomocí Správce balíčků "Yum".

```
Import-DSCResource -Module nx

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```
---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxPackage
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048130"
---
# <a name="dsc-for-linux-nxpackage-resource"></a>DSC pro Linux prostředek nxPackage

**NxPackage** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě balíčků na uzlu systému Linux.

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
| Name| Název balíčku, pro které chcete zajistit určitý stav.|
| Zkontrolujte| Určuje, jestli se má zkontrolovat, zda balíček existuje. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že balíček existuje. Nastavte ho na "Chybí" Ujistěte se, že balíček neexistuje. Výchozí hodnota je "K dispozici".|
| PackageManager| Podporované hodnoty jsou "yumu", "apt" a "zypperu". Určuje Správce balíčků pro použití při instalaci balíčků. Pokud **FilePath** není zadán, použije se zadaná cesta k instalaci balíčku. V opačném případě se použije k instalaci balíčku z předem nakonfigurované úložiště Správce balíčků. Pokud ani **PackageManager** ani **FilePath** jsou k dispozici, výchozí Správce balíčků pro systém, který se použije.|
| Cesta k souboru| Cesta k souboru, ve které se nachází balíček|
| PackageGroup| Pokud **$true**, **název** očekává se název skupiny balíčku pro použití se službou **PackageManager**. **PacakgeGroup** není platný při zadávání **FilePath**.|
| Argumenty| Řetězec s argumenty, které budou předány do balíčku přesně tak, jak je uvedeno.|
| ReturnCode| Očekávaný návratový kód. Pokud skutečný návratový kód neodpovídá očekávané hodnotě. k dispozici tady, že konfiguraci, vrátí se chyba.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Následující příklad zajistí, že je nainstalován balíček s názvem "httpd" na počítači s Linuxem pomocí Správce balíčků "Yumu".

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
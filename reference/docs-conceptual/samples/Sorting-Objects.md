---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Řazení objektů
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 06aa15d89888f1ecbe60b8e1dfb4efebb1d73673
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403644"
---
# <a name="sorting-objects"></a>Řazení objektů

Jsme můžete uspořádat zobrazených dat, aby bylo snazší vyhledávání s použitím `Sort-Object` rutiny. `Sort-Object` přebírá název jednu nebo více vlastností, které se budou řadit a vrací data seřazené podle hodnoty těchto vlastností.

## <a name="basic-sorting"></a>Základní řazení

Vezměte v úvahu problém uvedení podadresáře a soubory v aktuálním adresáři.
Pokud chceme řadit **LastWriteTime** a potom podle **název**, můžeme to udělat tak, že zadáte:

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
11/6/2017 10:10:11 AM  .localization-config
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:15 AM  tests
6/6/2018 7:58:59 PM    CONTRIBUTING.md
6/6/2018 7:58:59 PM    README.md
...
```

Můžete také řadit objektů v obráceném pořadí tak, že zadáte **sestupně** přepnout parametru.

```powershell
Get-ChildItem |
  Sort-Object -Property LastWriteTime, Name -Descending |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  reference
12/1/2018 10:13:50 PM  dsc
...
6/6/2018 7:58:59 PM    README.md
6/6/2018 7:58:59 PM    CONTRIBUTING.md
11/6/2017 10:10:15 AM  tests
11/6/2017 10:10:11 AM  ThirdPartyNotices
11/6/2017 10:10:11 AM  LICENSE-CODE
11/6/2017 10:10:11 AM  LICENSE
11/6/2017 10:10:11 AM  appveyor.yml
11/6/2017 10:10:11 AM  .openpublishing.build.ps1
11/6/2017 10:10:11 AM  .localization-config
```

## <a name="using-hash-tables"></a>Pomocí zatřiďovacích tabulek

S použitím v poli zatřiďovacích tabulek můžete seřadit různé vlastnosti v různém pořadí.
Každá tabulka hash používá **výraz** klíč k určení názvu vlastnosti jako řetězec a **vzestupně** nebo **sestupně** klíč k určení pořadí řazení podle `$true` nebo `$false`.
**Výraz** klíč je povinný.
**Vzestupně** nebo **sestupně** klíč je volitelný.

Následující příklad řadí objekty v sestupném **LastWriteTime** pořadí a vzestupně **název** pořadí.

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = 'LastWriteTime'; Descending = $true }, @{ Expression = 'Name'; Ascending = $true } |
  Format-Table -Property LastWriteTime, Name
```

```output
LastWriteTime          Name
-------------          ----
12/1/2018 10:13:50 PM  dsc
12/1/2018 10:13:50 PM  reference
11/29/2018 6:56:01 PM  .openpublishing.redirection.json
11/29/2018 6:56:01 PM  gallery
11/24/2018 10:33:22 AM developer
11/20/2018 7:22:19 PM  .markdownlint.json
...
```

Můžete také nastavit vlastnost scriptblock **výraz** klíč.
Při spuštění `Sort-Object` rutiny, spouští se vlastnost scriptblock a výsledek je použít k řazení.

Následující příklad seřadí v sestupném pořadí podle časový interval mezi objekty **CreationTime** a **LastWriteTime**.

```powershell
Get-ChildItem |
  Sort-Object -Property @{ Expression = { $_.LastWriteTime - $_.CreationTime }; Descending = $true } |
  Format-Table -Property LastWriteTime, CreationTime
```

```output
LastWriteTime          CreationTime
-------------          ------------
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
12/1/2018 10:13:50 PM  11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:11 AM
11/7/2018 6:52:24 PM   11/6/2017 10:10:15 AM
11/3/2018 9:58:17 AM   11/6/2017 10:10:11 AM
10/26/2018 4:50:21 PM  11/6/2017 10:10:11 AM
11/17/2018 1:10:57 PM  11/29/2017 5:48:30 PM
11/12/2018 6:29:53 PM  12/7/2017 7:57:07 PM
...
```

## <a name="tips"></a>Tipy

Můžete vynechat **vlastnost** název parametru následujícím způsobem:

```powershell
Sort-Object LastWriteTime, Name
```

Kromě toho se můžete vrátit k `Sort-Object` podle jeho alias integrované `sort`:

```powershell
sort LastWriteTime, Name
```

Klíče v zatřiďovací tabulky pro řazení lze zkrátit následujícím způsobem:

```powershell
Sort-Object @{ e = 'LastWriteTime'; d = $true }, @{ e = 'Name'; a = $true }
```

V tomto příkladu **e** zastupuje **výraz**, **d** zastupuje **sestupně**a **a** zastupuje **vzestupně**.

Aby se zlepšila čitelnost, můžete umístit zatřiďovací tabulky do samostatných proměnné:

```powershell
$order = @(
  @{ Expression = 'LastWriteTime'; Descending = $true }
  @{ Expression = 'Name'; Ascending = $true }
)

Get-ChildItem |
  Sort-Object $order |
  Format-Table LastWriteTime, Name
```
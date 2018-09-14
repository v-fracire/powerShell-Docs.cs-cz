---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Katalogové rutiny
ms.openlocfilehash: ec5fc866fe27a894b23b93d3ea46ad9c0cba288e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522884"
---
# <a name="catalog-cmdlets"></a>Katalogové rutiny

Přidali jsme dvě nové rutiny v [Microsoft.Powershell.Secuity](https://technet.microsoft.com/library/hh847877.aspx) modul pro generování a ověřování souborů katalogu systému windows.

## <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

`New-FileCatalog` Vytvoří soubor katalogu systému windows pro sadu složek a souborů. Soubor katalogu obsahuje hodnoty hash pro všechny soubory v zadané cesty. Sadu složek společně s odpovídající soubor katalogu, který představuje tyto složky můžete distribuovat uživatelům. Soubor katalogu lze příjemci obsahu k ověření, zda byly provedeny žádné změny do složek po vytvoření katalogu.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
Podporuje vytváření katalogu verze 1 a 2. K vytvoření hodnoty hash souboru a verze 2 používá SHA256 verze 1 používá algoritmus hash SHA1. Katalog verze 2 nepodporuje *systému Windows Server 2008 R2* a *Windows 7*. Doporučuje se použití katalogu verze 2, pokud používáte platformy *Windows 8*, *systému Windows Server 2012* a vyšší.

Pokud chcete použít tento příkaz na existující modul, určete CatalogFilePath a cestu proměnné tak, aby odpovídaly umístění manifestu modulu. V následujícím příkladu je manifestu modulu v C:\Program Files\Windows PowerShell\Modules\Pester.

![](../images/NewFileCatalog.jpg)

Tím se vytvoří soubor katalogu.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Chcete-li ověřit integritu souboru katalogu (Pester.cat v nad příkladu) by měl být podepsáno, pomocí [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) rutiny.


## <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

`Test-FileCatalog` ověří katalogu představující sadu složek.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Tato rutina porovnává hodnoty hash všechny soubory a jejich relativní cesty nacházejí v souboru katalogu s těmi, které je uloženo na disk. Když najde jakákoli Neshoda mezi hodnoty hash souboru a cesty vrátí stav `ValidationFailed`.
Uživatelé mohou načítat všechny informace pomocí `Detailed` přepnout. Podepisování stav katalogu se zobrazí jako `Signature` pole, která je stejná jako volání funkce [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) rutinu na soubor katalogu.
Uživatelé také přeskočit všechny soubory během ověřování s použitím `FilesToSkip` parametru.

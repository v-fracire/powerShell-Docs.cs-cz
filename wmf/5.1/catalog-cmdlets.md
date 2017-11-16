---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
title: Rutiny katalogu
ms.openlocfilehash: f0869e8c174ab127996866775ad20d056f877345
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="catalog-cmdlets"></a>Rutiny katalogu  

Jsme přidali dvě nové rutiny v [Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx) modulu pro vygenerování a ověření souborů katalogu systému windows.  

## <a name="new-filecatalog"></a>Nové FileCatalog 
--------------------------------

`New-FileCatalog`Vytvoří soubor katalogu systému windows pro sadu složek a souborů. Soubor katalogu obsahuje hodnoty hash pro všechny soubory v zadané cesty. Uživatele můžete distribuovat sadu složek spolu s odpovídající soubor katalogu, který představuje těchto složek. Soubor katalogu lze příjemce obsahu k ověření, zda všechny změny byly provedeny do složek, po vytvoření katalogu.    

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
Podporujeme vytváření katalogu verze 1 a 2. Verze 1 používá algoritmus hash SHA1 k vytvoření hodnoty hash souboru a verze 2 používá algoritmus SHA256. Katalog verze 2 není podporována na *Windows Server 2008 R2* a *Windows 7*. Doporučuje se používat katalog verze 2, pokud pomocí platformy *Windows 8*, *systému Windows Server 2012* a vyšší.  

Chcete-li použít tento příkaz na existující modul, zadejte CatalogFilePath a cestu proměnné tak, aby odpovídala umístění manifestu modulu. V následujícím příkladu je manifestu modulu v C:\Program Files\Windows PowerShell\Modules\Pester. 

![](../images/NewFileCatalog.jpg)

Tím se vytvoří soubor katalogu. 

![](../images/CatalogFile1.jpg)  

![](../images/CatalogFile2.jpg) 

Chcete-li ověřit integritu soubor katalogu (Pester.cat v výše exmaple) by měla být podepsána, pomocí [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) rutiny.   


## <a name="test-filecatalog"></a>Test FileCatalog 
--------------------------------

`Test-FileCatalog`ověří katalogu představující sadu složek. 

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Tato rutina porovnává hodnoty hash všech souborů a jejich relativní cesty nacházejí v souboru katalogu s těch, které jsou uloženy na disk. Pokud zjistí jakékoli neshody mezi hodnoty hash souboru a cesty vrátí stav `ValidationFailed`. Uživatele můžete načíst všechny tato informace pomocí `Detailed` přepínače. Podpisový stav katalogu se zobrazí jako `Signature` pole, která je stejná jako volání [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) na soubor katalogu rutinu. Uživatelé také přeskočit všechny soubory během ověřování pomocí `FilesToSkip` parametr. 


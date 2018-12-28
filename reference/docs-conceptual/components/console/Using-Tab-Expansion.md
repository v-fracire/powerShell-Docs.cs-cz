---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití rozšíření Tab
ms.assetid: c8730471-bf6a-43b8-ab1d-f9ef5a74f04e
ms.openlocfilehash: 3d047bf0691c8a304d7637aa50fba6ae99709a82
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404114"
---
# <a name="using-tab-expansion"></a>Použití rozšíření Tab

Příkazový řádek prostředí často poskytují způsob, jak, automatické dokončování názvů dlouhých souborů nebo příkazů urychlení položky příkazu a poskytuje. Prostředí Windows PowerShell umožňuje zadat názvy souborů a názvy rutin stisknutím kombinace kláves **kartu** klíč.

> [!NOTE]
> Vnitřní funkce TabExpansion nebo TabExpansion2 řídí rozšíření TAB. Protože tato funkce může přepsat nebo upraví, této diskuse je návod k chování výchozí konfigurace prostředí PowerShell.

Chcete-li automaticky vyplnit název souboru nebo cesta z dostupných voleb, zadejte část názvu a stiskněte klávesu **kartu** klíč. Prostředí PowerShell bude automaticky rozbalte název tak, aby první shodu, kterou najde. Stisknutím klávesy **kartu** klíč bude opakovaně cyklicky procházet všechny dostupné možnosti.

Karta rozšíření názvy rutin se mírně liší. Použití rozšíření tab na název rutiny, zadejte celý první část názvu (akce) a pomlčku, která ji následuje. Můžete vyplnit informace pro částečné shody názvu. Pokud zadáte například **get-co** a potom stiskněte klávesu **kartu** klíče, prostředí PowerShell se automaticky rozšíří na **Get-Command** rutiny (Všimněte si, že také změní velikost písmen posloupnost písmen na jejich běžného formuláře). Pokud stisknete **kartu** klíče znovu, prostředí PowerShell nahradí to jenom další odpovídající název rutiny, **Get-Content**.

Rozšíření tab můžete opakovaně použít na stejném řádku. Například můžete použít rozšíření tab na název **Get-Content** rutiny tak, že zadáte:

```
PS> Get-Con<Tab>
```

Po stisknutí klávesy **kartu** klíče, příkaz rozšíří na:

```
PS> Get-Content
```

Potom můžete částečně zadejte cestu k souboru protokolu Active instalace a použití rozšíření tab znovu:

```
PS> Get-Content c:\windows\acts<Tab>
```

Po stisknutí klávesy **kartu** klíče, příkaz rozšíří na:

```
PS> Get-Content C:\windows\actsetup.log
```

> [!NOTE]
> Jedním z procesu rozšiřující karty omezení je, že jsou karty vždy interpretován jako pokusy o dokončení slova. Pokud zkopírujete a vložíte příklady příkazů do konzoly Powershellu, ujistěte se, že ukázky neobsahuje karet; Pokud ano, mít nepředvídatelné výsledky a nebudou téměř jistě jste zamýšleli.
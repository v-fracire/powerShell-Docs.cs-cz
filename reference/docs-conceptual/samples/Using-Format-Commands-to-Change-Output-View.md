---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití formátovacích příkazů ke změně zobrazení výstupů
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 97d3a9e04abb61bb80a0b8c67d9fb9e885a0b91b
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403867"
---
# <a name="using-format-commands-to-change-output-view"></a>Použití formátovacích příkazů ke změně zobrazení výstupů

Prostředí Windows PowerShell obsahuje sadu rutin, které umožňují řídit vlastnosti, které se zobrazují pro konkrétní objekty. Názvy všechny rutiny začínají znakem příkaz **formátu**. Umožňují vybrat jednu nebo více vlastností zobrazíte.

**Formátu** jsou rutiny **formátu celou**, **Format-List**, **Format-Table**, a **formátu – vlastní**. Jenom popíšeme **formátu celou**, **Format-List**, a **Format-Table** rutiny v této uživatelské příručce.

Každá rutina formátu má výchozí vlastnosti, které se použijí, pokud nezadáte konkrétní vlastnosti k zobrazení. Každá rutina také používá stejný název parametru **vlastnost**, chcete-li určit vlastnosti, které chcete zobrazit. Protože **formátu celou** zobrazuje pouze jednu vlastnost jeho **vlastnost** parametr přijímá pouze jednu hodnotu, ale vlastnost parametry **Format-List** a **Format-Table** přijme seznam názvů vlastností.

Pokud použijete příkaz **Get-Process - název powershellu** se dvěma instancemi spuštění prostředí Windows PowerShell, získáte výstup, který vypadá takto:

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

Ve zbytku této části se podíváme na tom, jak používat **formátu** rutiny, které mění způsob, zobrazí se výstup tohoto příkazu.

### <a name="using-format-wide-for-single-item-output"></a>Pomocí formátu celý výstup z jedné položky

**Formátu celou** rutinu, ve výchozím nastavení, zobrazí pouze výchozí vlastností objektu. Zobrazí se informace týkající se jednotlivých objektů v jednom sloupci:

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

Můžete také zadat jiné než výchozí vlastnost:

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a>Řízení formátu celé zobrazení se sloupcem

S **formátu celou** rutiny, jednu vlastnost může zobrazit pouze v čase. Díky tomu užitečné pro zobrazení jednoduché seznamy, které zobrazují pouze jeden element na každý řádek. Chcete-li získat jednoduchý seznam, nastavte hodnotu **sloupec** parametr na hodnotu 1 zadáním:

```powershell
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a>Použití Format-List pro zobrazení seznamu

**Format-List** rutina zobrazí objektu ve formě výpis, s každou vlastnost s názvem a zobrazují na samostatný řádek:

```
PS> Get-Process -Name powershell | Format-List

Id      : 2760
Handles : 1242
CPU     : 3.03125
Name    : powershell

Id      : 3448
Handles : 328
CPU     : 1.0625
Name    : powershell
```

Můžete zadat libovolný počet vlastností chcete:

```
PS> Get-Process -Name powershell | Format-List -Property ProcessName,FileVersion
,StartTime,Id

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:42:00
Id          : 2760

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:54:28
Id          : 3448
```

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a>Získat podrobné informace s použitím seznamu formát se zástupnými znaky

**Format-List** rutina umožňuje použít zástupný znak jako hodnota jeho **vlastnost** parametru. To umožňuje zobrazit podrobné informace. Objekty často zahrnují více informací, než budete potřebovat, což je důvod, proč Windows Powershellu se nezobrazují všechny hodnoty vlastností ve výchozím nastavení. Chcete-li zobrazit všechny vlastnosti objektu, použijte **Format-List-vlastnost \&#42;** příkazu. Následující příkaz vytvoří více než 60 řádky výstupu pro jeden proces:

```powershell
Get-Process -Name powershell | Format-List -Property *
```

I když **Format-List** příkaz je užitečné pro zobrazení podrobností, pokud chcete základní informace o výstupu, který obsahuje mnoho položek, jednodušší tabulkové zobrazení je často užitečné.

### <a name="using-format-table-for-tabular-output"></a>Použití Format-Table pro tabulkový výstup

Pokud používáte **Format-Table** rutinu s žádné názvy vlastností zadané pro formátování výstupu **Get-Process** příkazu se zobrazí stejně jako bez provedení jakékoli formátování výstupu. Důvodem je, že procesy se obvykle zobrazují ve formátu tabulky, jako jsou většinu objektů prostředí Windows PowerShell.

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a>Vylepšení výstupu Format-Table (AutoSize)

I když v tabulkovém zobrazení je užitečné pro zobrazení velké množství informací srovnatelné, může být obtížné pro interpretaci, pokud je příliš úzký, data zobrazení. Například pokud se pokusíte zobrazit cesta procesu, ID, název a společnosti, získáte zkrácený výstup pro cestu proces a ve sloupci společnosti:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

Pokud zadáte **AutoSize** parametr při spuštění **Format-Table** příkazu prostředí Windows PowerShell se vypočítat šířku sloupců, které jsou založené na skutečná data chcete zobrazit. Díky tomu **cesta** sloupec čitelné, ale sloupec společnosti zůstává zkrácený:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

**Format-Table** rutina může být stále zkrátit data, ale pouze provede to na konci na obrazovce. Vlastnosti, než poslední zobrazený disponují tolik velikost podle potřeby pro jejich nejdelší element dat zobrazit správně. Vidíte, zobrazí se název společnosti, ale cesta je zkrácen, pokud odkládacího umístění **cesta** a **společnosti** v **vlastnost** seznam hodnot:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

**Format-Table** příkaz předpokládá, nearer vlastnost je na začátek seznamu vlastností je čím více důležité. Tak se pokusí zobrazit vlastnosti nejbližší začátku úplně. Pokud **Format-Table** příkaz nelze zobrazit všechny vlastnosti, bude ze zobrazení odebrat některé sloupce a zobrazit upozornění. Toto chování můžete zobrazit, pokud provedete **název** vlastnost poslední v seznamu:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

Ve výstupu výše sloupec ID se zkrátí na aby se vešel do seznamu a záhlaví sloupců jsou navršeny. Automatická změna velikosti sloupců není vždy nutné co chcete.

#### <a name="wrapping-format-table-output-in-columns-wrap"></a>Zabalení Format-Table výstup ve sloupcích (zalamování řádků)

Můžete vynutit zdlouhavé **Format-Table** dat v rámci jeho zobrazovaný sloupec zabalit pomocí **zabalení** parametru. Použití **zabalení** parametr samostatně není nutně co můžete očekávat, protože používá výchozí nastavení, pokud také nezadáte **AutoSize**:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

Výhodou použití **zabalení** parametr sám o sobě je, že ho nedošlo ke zpomalení zpracování velmi velká. Pokud provádíte rekurzivní souboru výpis velkého adresáře systému, může trvat velmi dlouho a použít spoustu paměti před zobrazením první výstupní položky, pokud používáte **AutoSize**.

Pokud si nejste obavy týkající se zatížení systému, potom **AutoSize** dobře funguje s **zabalení** parametru. Počáteční sloupce jsou vždy přidělený tolik šířka podle potřeby k zobrazení položek na jeden řádek, stejně jako při zadání **AutoSize** bez **zabalení** parametru. Jediným rozdílem je, že v případě potřeby se zalomí posledního sloupce:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

Některé sloupce nemusí zobrazit, pokud nejprve zadejte nejširší sloupce tak, aby byl nejbezpečnější nejprve určit nejmenší datové prvky. V následujícím příkladu určíme element path velmi široké nejprve a i obtékané jsme stále ztratit finální **název** sloupce:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a>Uspořádání tabulkového výstupu (-GroupBy)

Další užitečné parametr pro ovládací prvek Tabulkový výstup je **GroupBy**. Už tabulkovém výpisu zejména může být obtížné pro porovnání. **GroupBy** parametr skupiny výstup podle hodnoty vlastnosti. Například můžete seskupíme procesy společností pro snazší kontroly vynechání hodnoty společnosti v seznamu vlastností:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```
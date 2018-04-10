---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití formátovacích příkazů ke změně zobrazení výstupů
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 97d3a9e04abb61bb80a0b8c67d9fb9e885a0b91b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="using-format-commands-to-change-output-view"></a>Použití formátovacích příkazů ke změně zobrazení výstupů

Prostředí Windows PowerShell obsahuje sadu rutin, které umožňují řídit vlastnosti, které se zobrazují pro konkrétní objekty. Názvy všechny rutiny začít s příkazem **formátu**. Můžete vybrat jednu nebo více vlastností zobrazíte umožňují.

**Formátu** jsou rutiny **formátu celou**, **Format-List**, **Format-Table**, a **formát vlastních**. Jsme popíše pouze **formátu celou**, **Format-List**, a **Format-Table** rutiny v této uživatelské příručce.

Každá rutina formátu má výchozí vlastnosti, které se použijí, pokud nezadáte vlastnosti specifické pro zobrazení. Každá rutina také používá stejný název parametru, **vlastnost**, chcete-li určit vlastnosti, které chcete zobrazit. Protože **formátu celou** se zobrazí pouze jednu vlastnost jeho **vlastnost** přebírá parametr pouze jednu hodnotu, ale vlastnost parametry **Format-List** a **Format-Table** přijme seznam názvů vlastností.

Pokud použijete příkaz **Get-Process - powershell název** se dvěma instancemi spuštění prostředí Windows PowerShell získat výstup, který vypadá takto:

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

Ve zbývající části této části, se podíváme na tom, jak používat **formát** rutiny změnit způsob výstup tohoto příkazu se zobrazí.

### <a name="using-format-wide-for-single-item-output"></a>Pomocí formátu celou pro výstup jedné položky

**Formátu celou** rutinu, ve výchozím nastavení, zobrazí jenom výchozí vlastnost objektu. V jednom sloupci se zobrazují informace související s každého objektu:

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

Můžete také určit jiné než výchozí vlastnost:

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a>Řízení zobrazení formátu celou se sloupcem

S **formátu celou** rutiny současně může zobrazit pouze jednu vlastnost. Díky tomu je užitečné pro zobrazení jednoduchých seznamů, které se zobrazí pouze jeden element na každý řádek. Pokud chcete získat jednoduchý seznam, nastavte hodnotu **sloupec** parametr 1 zadáním:

```powershell
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a>Použití Format-List pro zobrazení seznamu

**Format-List** rutina zobrazí objekt ve formátu v seznamu, s každou vlastnost s názvem bez přípony a zobrazují na samostatném řádku:

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

Můžete zadat libovolný počet vlastnosti tak, jak chcete:

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

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a>Získávání podrobné informace pomocí seznamu formát se zástupnými znaky

**Format-List** rutina umožňuje použít zástupný znak jako hodnota jeho **vlastnost** parametr. Díky tomu můžete zobrazit podrobné informace. Často objekty zahrnují více informací, než budete potřebovat, proto prostředí Windows PowerShell nezobrazuje ve výchozím nastavení všechny hodnoty vlastností. Chcete-li zobrazit všechny vlastnosti objektu, použijte **Format-List-vlastnost \&#42;** příkaz. Následující příkaz se vytvoří víc než 60 řádky výstupu pro jeden procesu:

```powershell
Get-Process -Name powershell | Format-List -Property *
```

I když **Format-List** příkaz je užitečný pro zobrazení podrobností, pokud chcete přehled výstupu, který obsahuje mnoho položek, jednodušší tabulkové zobrazení je často užitečné.

### <a name="using-format-table-for-tabular-output"></a>Použití formátu tabulky pro tabulkový výstup

Pokud použijete **Format-Table** rutiny s žádné názvy vlastností zadaný k formátování výstupu z **Get-Process** příkazu, získáte stejně výstup jako bez žádné formátování. Důvodem je, že procesy se obvykle zobrazují v tabulkovém formátu, jsou většinu objektů prostředí Windows PowerShell.

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a>Vylepšení výstup Format-Table (AutoSize)

I když tabulkové zobrazení je užitečná pro zobrazení spousty porovnatelný z hlediska informací, může být obtížné vysvětlit, pokud je příliš úzké pro data zobrazení. Například pokud se pokusíte zobrazit cesta procesu, ID, názvu a společnosti, zobrazí se zkrácený výstup pro cestu proces a ve sloupci společnosti:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

Pokud zadáte **AutoSize** parametr při spuštění **Format-Table** příkazu prostředí Windows PowerShell se vypočítat šířku sloupců, které jsou založené na skutečná data chcete zobrazit. Díky tomu **cesta** sloupec čitelný, ale sloupec společnosti zůstává zkrácený:

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

**Format-Table** rutiny může stále zkrátit data, ale ho bude tak učinit pouze na konci části obrazovky. Vlastnosti, než byl naposledy zobrazí, mají stejnou velikost jako potřebují pro jejich nejdelší datový prvek ke správnému zobrazení. Uvidíte, že název společnosti je viditelná, ale cesta je oříznuta, pokud Prohodit umístění **cesta** a **společnosti** v **vlastnost** seznam hodnot:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

**Format-Table** příkaz předpokládá, že nearer vlastnost je na začátek seznamu vlastností je více důležité. Pokusí se zobrazí vlastnosti nejbližší začátku úplně. Pokud **Format-Table** příkaz nelze zobrazit všechny vlastnosti, bude ze zobrazení odeberte některé sloupce a zobrazit upozornění. Toto chování můžete zobrazit, jestliže provedete **název** vlastnost poslední v seznamu:

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

Ve výstupu výše sloupec ID zkrácen lze přizpůsobit do seznam a záhlaví sloupců jsou skládaný. Automatická změna velikosti sloupců vždy neprovádí co chcete použít.

#### <a name="wrapping-format-table-output-in-columns-wrap"></a>Výstupní formát tabulky zabalení ve sloupcích (zkrácení)

Můžete vynutit zdlouhavé **Format-Table** data v rámci jeho sloupec zobrazení zabalit pomocí **zabalení** parametr. Pomocí **zabalení** parametr samostatně nebude provádět nutně očekávat, protože používá výchozí nastavení, pokud taky nezadáte **AutoSize**:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

Výhodou **zabalení** parametr sám o sobě je, že ho nedošlo ke zpomalení zpracování velmi velká. Pokud provádíte rekurzivní souboru výpis velkého adresáře systému, může být časově velmi náročná a použít velké množství paměti, než se zobrazí první položky výstupu, pokud používáte **AutoSize**.

Pokud si nejste zajímá zatížení systému, potom **AutoSize** dobře funguje s **zabalení** parametr. Počáteční sloupce jsou vždy vyhrazených tolik šířka podle potřeby k zobrazení položek na jeden řádek, stejně jako při zadání **AutoSize** bez **zabalení** parametr. Jediným rozdílem je, že bude zalomit posledního sloupce v případě potřeby:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

Některé sloupce nemusí zobrazit, pokud nejprve zadejte nejširší sloupce, proto je nejbezpečnější nejprve vybrat nejmenší datové prvky. V následujícím příkladu určíme element velmi široké cesty nejprve a i obtékané jsme konečné stále ztratit **název** sloupce:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a>Uspořádání výstupní tabulky (-GroupBy)

Další užitečné parametr pro ovládací prvek Tabulkový výstup **GroupBy**. Již tabulkové výpisech zejména může být obtížné porovnat. **GroupBy** parametr skupin výstup v závislosti na hodnotu vlastnosti. Například můžeme můžete seskupit procesy ve společnosti pro snazší kontroly vynechání společnosti hodnotu ze seznamu vlastností:

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```
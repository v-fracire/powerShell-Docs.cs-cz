---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Člen Get struktury objekt zobrazení
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: cc93e45e4306b3d623c1d3d1096dd20c1afc59c8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404043"
---
# <a name="viewing-object-structure-get-member"></a>Zobrazení struktury objektu (Get-Member)

Protože objekty hrají hlavní roli ve Windows Powershellu, existuje několik nativních příkazů, které jsou navrženy pro práci s typy libovolného objektu. Nejdůležitějším je **Get-Member** příkazu.

Nejjednodušší techniku pro analýzu objekty, které příkaz vrátí je do kanálu výstup tohoto příkazu **Get-Member** rutiny. **Get-Member** rutina ukazuje formální název typu objektu a úplný seznam všech jejích členů. Počet prvků, které jsou vráceny, které může být někdy náročné. Například objekt procesu může obsahovat více než 100 členy.

Pokud chcete zobrazit všechny členy objektu Process a stránky výstupu, abyste mohli zobrazit všechno, zadejte:

```powershell
Get-Process | Get-Member | Out-Host -Paging
```

Výstup tohoto příkazu bude vypadat přibližně takto:

```output
TypeName: System.Diagnostics.Process

Name                           MemberType     Definition
----                           ----------     ----------
Handles                        AliasProperty  Handles = Handlecount
Name                           AliasProperty  Name = ProcessName
NPM                            AliasProperty  NPM = NonpagedSystemMemorySize
PM                             AliasProperty  PM = PagedMemorySize
VM                             AliasProperty  VM = VirtualMemorySize
WS                             AliasProperty  WS = WorkingSet
add_Disposed                   Method         System.Void add_Disposed(Event...
...
```

Můžeme provádět tento dlouhý seznam informace použitelnější pomocí filtrování pro prvky, které chceme vidět. **Get-Member** příkaz umožňuje zobrazit seznam pouze členů, které jsou vlastnostmi. Existuje několik tvarů vlastnosti. Rutiny zobrazuje vlastnosti libovolného typu, pokud jsme si nastavili **Get-Member MemberType** parametr na hodnotu **vlastnosti**. V rozevíracím seznamu je stále velmi dlouhý, ale o něco lépe zvládnutelné:

```
PS> Get-Process | Get-Member -MemberType Properties

   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
...
ExitCode                   Property       System.Int32 ExitCode {get;}
...
Handle                     Property       System.IntPtr Handle {get;}
...
CPU                        ScriptProperty System.Object CPU {get=$this.Total...
...
Path                       ScriptProperty System.Object Path {get=$this.Main...
...
```

> [!NOTE]
> Povolené hodnoty MemberType jsou AliasProperty, CodeProperty, vlastnost, NoteProperty, ScriptProperty, vlastnosti, PropertySet, metoda, CodeMethod, ScriptMethod, metody, ParameterizedProperty, členů a všechny.

Existuje více než 60 vlastnosti pro proces. Prostředí Windows PowerShell ukazuje, často že pouze několik vlastností pro libovolný objekt dobře známé, zobrazuje všechny z nich je důvod, proč byste mohli vytvořit nezvladatelné množství informací.

> [!NOTE]
> Určuje způsob zobrazení typ objektu, který s použitím informací uložených v soubory XML, které mají jména končící na prostředí Windows PowerShell. format.ps1xml. Formátování dat pro proces objekty, které jsou objekty .NET System.Diagnostics.Process, je uložen v DotNetTypes.format.ps1xml.

Pokud potřebujete, podívejte se na vlastnosti než ty, které prostředí Windows PowerShell zobrazí ve výchozím nastavení, je potřeba formátovat sami výstupní data. To můžete udělat pomocí rutin formátu.
---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Zobrazení objektu struktura Get člena
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: cc93e45e4306b3d623c1d3d1096dd20c1afc59c8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="viewing-object-structure-get-member"></a>Zobrazení struktury objektu (Get člen)

Protože objekty centrální roli hrají v prostředí Windows PowerShell, existuje několik nativní příkazy, které jsou navrženy pro práci s typy libovolného objektu. Je nejdůležitějším **Get-člen** příkaz.

Nejjednodušším způsobem pro analýzu objekty, které vrátí příkaz je výstup tohoto příkazu **Get-člen** rutiny. **Get-člen** rutiny uvádí formální název tohoto typu objektu a úplný seznam všech jejích členů. Počet elementů, které jsou vráceny, v některých případech může být čtenáře. Například objekt procesu můžete mít více než 100 členy.

Aby se zobrazily všechny členy objekt procesu a stránky výstup, můžete zobrazit všechny, zadejte:

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

Abychom mohli provádět tento dlouhý seznam informace více použitelné pomocí filtrování pro prvky, které chcete v tématu. **Get-člen** příkaz umožňuje zobrazit seznam pouze členové, které jsou vlastnosti. Existuje několik typů vlastností. Rutiny zobrazuje vlastnosti všech typů jsme nastaveného **Get-člen MemberType** parametr na hodnotu **vlastnosti**. V rozevíracím seznamu je stále velmi dlouhé, ale trochu udržitelnější:

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

Nejsou k dispozici více než 60 vlastnosti procesu. Z důvodu, prostředí Windows PowerShell často zobrazuje, že je jen několik vlastností pro všechny známé objekt, který zobrazuje všechny z nich vytvoří nezvladatelné množství informací.

> [!NOTE]
> Postupy: zobrazení pomocí informace uložené v souborech XML, které mají názvy končící na typ objektu, který určuje, prostředí Windows PowerShell. format.ps1xml. Formátování dat pro proces objekty, které jsou objekty .NET System.Diagnostics.Process, je uložen v DotNetTypes.format.ps1xml.

Pokud potřebujete podívejte se na vlastnosti kromě těch, které ve výchozím nastavení zobrazí prostředí Windows PowerShell, musíte se k formátování výstupní data sami. Tento krok můžete provést pomocí rutiny formátu.
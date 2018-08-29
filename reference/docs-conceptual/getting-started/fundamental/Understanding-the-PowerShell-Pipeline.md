---
ms.date: 08/23/2018
keywords: rutiny prostředí PowerShell
title: Principy kanály v Powershellu
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: 3ee03f001668fb24ff9be1ea6ecb3817e319d0ee
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134212"
---
# <a name="understanding-pipelines"></a>Principy kanály

Kanály fungují jako řada připojených segmenty kanálu. Položky přesun podél kanálu prochází každý segment. K vytvoření kanálu v prostředí PowerShell, připojíte příkazy spolu s operátorem kanálu "|". Tento výstup každý příkaz se používá jako vstup pro další příkaz.

Zápis použitý pro kanály se podobá notaci používané v jiných prostředí. Na první pohled nemusí být zřejmé, jak se liší v prostředí PowerShell kanály. I když se text zobrazí na obrazovce, prostředí PowerShell prostřednictvím kanálu předá objekty, není text mezi příkazy.

## <a name="the-powershell-pipeline"></a>Kanál prostředí PowerShell

Kanály jsou pravděpodobně nejcennější pojem v rozhraní příkazového řádku. Při použití správně, kanály úsilí použití komplexní příkazy a usnadňují naleznete v tématu Postup pro příkazy. Každý příkaz v kanálu (označované jako element kanálu) se předá výstup další příkaz v rámci kanálu jednotlivých položkách. Příkazy nemusí zpracovávat více položek najednou. Výsledkem je snížení spotřebovaných a možnost začít okamžitě získávání výstupu.

Například, pokud použijete `Out-Host` k vynucení stránku po stránce zobrazení výstupu z jiného příkazu, výstup vypadá stejně jako normální text zobrazený na obrazovce, rozdělit do stránky:

```powershell
Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging
```

```Output
    Directory: C:\WINDOWS\system32

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        4/12/2018   2:15 AM                0409
d-----        5/13/2018  11:31 PM                1033
d-----        4/11/2018   4:38 PM                AdvancedInstallers
d-----        5/13/2018  11:13 PM                af-ZA
d-----        5/13/2018  11:13 PM                am-et
d-----        4/11/2018   4:38 PM                AppLocker
d-----        5/13/2018  11:31 PM                appmgmt
d-----        7/11/2018   2:05 AM                appraiser
d---s-        4/12/2018   2:20 AM                AppV
d-----        5/13/2018  11:10 PM                ar-SA
d-----        5/13/2018  11:13 PM                as-IN
d-----        8/14/2018   9:03 PM                az-Latn-AZ
d-----        5/13/2018  11:13 PM                be-BY
d-----        5/13/2018  11:10 PM                BestPractices
d-----        5/13/2018  11:10 PM                bg-BG
d-----        5/13/2018  11:13 PM                bn-BD
d-----        5/13/2018  11:13 PM                bn-IN
d-----        8/14/2018   9:03 PM                Boot
d-----        8/14/2018   9:03 PM                bs-Latn-BA
d-----        4/11/2018   4:38 PM                Bthprops
d-----        4/12/2018   2:19 AM                ca-ES
d-----        8/14/2018   9:03 PM                ca-ES-valencia
d-----        5/13/2018  10:46 PM                CatRoot
d-----        8/23/2018   5:07 PM                catroot2
<SPACE> next page; <CR> next line; Q quit
...
```

Stránkování také snižuje nároky na CPU, protože zpracování přenese `Out-Host` rutiny po dokončení stránky připravený k zobrazení. Rutiny, které jej předcházejí v kanálu pozastavit provádění, dokud nebude k dispozici na další stránku výstup.

Uvidíte rozdíl Správce úloh Windows ke sledování procesoru a paměti používá PowerShell. Spusťte následující příkaz: `Get-ChildItem C:\\Windows -Recurse`. Porovnání využití procesoru a paměti pro tento příkaz: `Get-ChildItem C:\\Windows -Recurse | Out-Host -Paging`.

## <a name="objects-in-the-pipeline"></a>Objekty v kanálu

Při spuštění rutiny v prostředí PowerShell se zobrazí textový výstup, protože je nezbytná k reprezentaci objektů jako text v okně konzoly. Textový výstup nemusí být zobrazeny všechny vlastnosti objekt, který je výstup.

Představme si třeba, `Get-Location` rutiny. Pokud spustíte `Get-Location` své aktuální polohy je kořenové jednotce C, zobrazí se následující výstup:

```
PS> Get-Location

Path
----
C:\
```

Textový výstup je uveden seznam informací, ne úplnou reprezentaci objekt vrácený rutinou `Get-Location`. Záhlaví ve výstupu se přidal proces, který zformátuje data pro zobrazení na obrazovce.

Když přesměrujte výstup do `Get-Member` rutinu můžete získat informace o objekt vrácený rutinou `Get-Location`.

```powershell
PS> Get-Location | Get-Member
```

```Output
   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Equals       Method     bool Equals(System.Object obj)
GetHashCode  Method     int GetHashCode()
GetType      Method     type GetType()
ToString     Method     string ToString()
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   string Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {get;}
ProviderPath Property   string ProviderPath {get;}
```

`Get-Location` Vrátí **PathInfo** objekt, který obsahuje aktuální cestě a dalších informací.

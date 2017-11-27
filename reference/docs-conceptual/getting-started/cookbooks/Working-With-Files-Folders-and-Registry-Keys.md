---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Práce se složkami soubory a klíče registru"
ms.assetid: e6cf87aa-b5f8-48d5-a75a-7cb7ecb482dc
ms.openlocfilehash: 22a2390686659033bfd8b02a151b3397cfd46a22
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="working-with-files-folders-and-registry-keys"></a>Práce se soubory, složky a klíče registru
Prostředí Windows PowerShell používá podstatným jménem **položky** odkazovat na položky najít na jednotku prostředí Windows PowerShell. Při plánování práce s poskytovateli Windows PowerShell FileSystem **položky** může být soubor, složku nebo jednotku prostředí Windows PowerShell. Výpis a práci s těmito položkami je důležité základní úloha v většinu nastavení pro správu, tak chceme tyto úlohy podrobně popisují.

### <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a>Vytváření výčtu souborů, složek a klíčů registru (Get-ChildItem)
Vzhledem k tomu, že získání kolekce položek z konkrétního umístění, je takový běžné úlohy, **Get-ChildItem** rutiny je navrženo konkrétně k vrátí všechny položky v rámci kontejneru, například do složky nalezen.

Pokud chcete vrátit všechny soubory a složky, které jsou obsažena přímo ve složce C:\\Windows, zadejte:

```
PS> Get-ChildItem -Path C:\Windows
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-16   8:10 AM          0 0.log
-a---        2005-11-29   3:16 PM         97 acc1.txt
-a---        2005-10-23  11:21 PM       3848 actsetup.log
...
```

Seznam bude vypadat podobně jako co uvidí, když zadáte **dir** v **Cmd.exe**, nebo **ls** příkazu v příkazovém prostředí UNIX.

Velmi složité výpisech můžete provádět pomocí parametrů **Get-ChildItem** rutiny. Podíváme se na několik scénářů Další. Zobrazí se syntaxe **Get-ChildItem** rutiny zadáním:

```
PS> Get-Command -Name Get-ChildItem -Syntax
```

Tyto parametry můžete ve smíšeném a namapovat na získat vysoce přizpůsobenou výstup.

#### <a name="listing-all-contained-items--recurse"></a>Výpis všech obsažených položek (-Recurse)
Pokud chcete zobrazit položky ve složce Windows a všechny položky, které jsou obsaženy v rámci podsložky, použijte **Recurse** parametr **Get-ChildItem**. Seznam všechno, co zobrazí ve složce Windows a položek v jejích podsložkách. Příklad:

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

#### <a name="filtering-items-by-name--name"></a>Filtrování položek podle názvu (-název)
Chcete-li zobrazit pouze názvy položek, použijte **název** parametr **Get-Childitem**:

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

#### <a name="forcibly-listing-hidden-items--force"></a>Vynuceně seznam skrytých položky (-Force)
Položky, které jsou obvykle neviditelná v Průzkumníkovi souborů nebo Cmd.exe nejsou zobrazeny ve výstupu **Get-ChildItem** příkaz. Chcete-li zobrazit skryté položky, použijte **Force** parametr **Get-ChildItem**. Příklad:

```
Get-ChildItem -Path C:\Windows -Force
```

Tento parametr je s názvem Force, protože normální chování můžete přepsat vynuceně **Get-ChildItem** příkaz. Platnost je často používaný parametr, který vynutí akci, která rutina nebude fungovat normálně, i když ho nebude provádět žádnou akci, která ohrožuje zabezpečení systému.

#### <a name="matching-item-names-with-wildcards"></a>Odpovídající názvy položek se zástupnými znaky
**Get-ChildItem** příkaz přijímá zástupné znaky v cestě položky k zobrazení seznamu.

Vzhledem k porovnávání se zástupnými znaky se zpracovává souborem modul prostředí Windows PowerShell, všechny rutiny, které přijímá zástupné znaky použít stejný zápis a mít stejné odpovídající chování. Zápis zástupný znak prostředí Windows PowerShell obsahuje:

- Znak hvězdičky (\*) odpovídá počtu nula či více výskytů libovolného znaku.

- Otazník (?) odpovídá přesně jeden znak.

- Levé závorky (\[) znak a znak pravé závorky (]), uzavřete sadu znaků lze porovnat.

Zde jsou některé příklady, jak funguje specifikace zástupný znak.

Chcete-li vyhledat všechny soubory v adresáři systému Windows s příponou **.log** a přesně 5 znaků v základním názvem, zadejte následující příkaz:

```
PS> Get-ChildItem -Path C:\Windows\?????.log
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
...
-a---        2006-05-11   6:31 PM     204276 ocgen.log
-a---        2006-05-11   6:31 PM      22365 ocmsn.log
...
-a---        2005-11-11   4:55 AM         64 setup.log
-a---        2005-12-15   2:24 PM      17719 VxSDM.log
...
```

Najít všechny soubory, které začínají písmenem **x** v adresáři systému Windows, zadejte:

```
Get-ChildItem -Path C:\Windows\x*
```

Chcete-li vyhledat všechny soubory, jejichž názvy začínají řetězcem **x** nebo **z**, zadejte:

```
Get-ChildItem -Path C:\Windows\[xz]*
```

#### <a name="excluding-items--exclude"></a>Vyloučení položek (-vyloučení)
Můžete vyloučit konkrétní položky pomocí **vyloučit** parametr Get-ChildItem. To umožňuje provádět komplexní filtrování v jediném příkazu.

Předpokládejme například chcete najít knihovnu DLL čas služby systému Windows ve složce System32, a všechny, které si pamatujete týkající se názvu DLL je, že začíná "W" a "32" je v ní.

Výraz jako **w\&#42; 32\&#42;. knihovny DLL** najdete všechny knihovny DLL, které splňují podmínky, ale také může vrátit systém Windows 95 a Windows kompatibility 16bitové knihovny DLL, které zahrnují "95" nebo "16" v jejich názvy. Je možné vynechat soubory, které mají některou z těchto čísla v jejich názvy pomocí **vyloučit** parametr se vzorkem  **\&#42;\[ 9516]\&#42;**:

<pre>PS> Get-ChildItem -Path C:\WINDOWS\System32\w*32*.dll -Exclude *[9516]*
Directory: Microsoft.PowerShell.Core\FileSystem::C:\WINDOWS\System32
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     174592 w32time.dll
-a---        2004-08-04   8:00 AM      22016 w32topl.dll
-a---        2004-08-04   8:00 AM     101888 win32spl.dll
-a---        2004-08-04   8:00 AM     172032 wldap32.dll
-a---        2004-08-04   8:00 AM     264192 wow32.dll
-a---        2004-08-04   8:00 AM      82944 ws2_32.dll
-a---        2004-08-04   8:00 AM      42496 wsnmp32.dll
-a---        2004-08-04   8:00 AM      22528 wsock32.dll
-a---        2004-08-04   8:00 AM      18432 wtsapi32.dll</pre>

#### <a name="mixing-get-childitem-parameters"></a>Kombinování parametry Get-ChildItem
Můžete použít několik parametrů **Get-ChildItem** rutiny v jednom příkazu. Předtím, než můžete kombinovat parametry, ujistěte se, že rozumíte porovnávání se zástupnými znaky. Například následující příkaz vrátí žádné výsledky:

```
PS> Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

Nebyly nalezeny žádné výsledky, i když se dvě knihovny DLL, která začínají znakem "z" ve složce Windows.

Nebyly vráceny žádné výsledky, protože jsme zadali zástupného jako část této cesty. I když příkaz byl rekurzivní, **Get-ChildItem** rutiny omezený položky na ty, které se nacházejí ve složce Windows s názvy konče ".dll".

Pokud chcete zadat rekurzivní hledání pro soubory, jejichž názvy odpovídají speciální vzorku, použijte **-zahrnují** parametr.

```
PS> Get-ChildItem -Path C:\Windows -Include *.dll -Recurse -Exclude [a-y]*.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32\Setup

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM       8261 zoneoc.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     337920 zipfldr.dll
```


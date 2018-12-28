---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce se složkami souborů a klíči registru
ms.assetid: e6cf87aa-b5f8-48d5-a75a-7cb7ecb482dc
ms.openlocfilehash: a09b127d4ba37d33cb4c0f0ce0819e645fd4b137
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404065"
---
# <a name="working-with-files-folders-and-registry-keys"></a>Práce se soubory, složky a klíče registru

Prostředí Windows PowerShell používá podstatným jménem **položky** odkazovat na položky na jednotku prostředí Windows PowerShell. Při zpracování komplexnějších zprostředkovatele systému souborů Windows Powershellu **položky** může být soubor, složku nebo jednotku prostředí Windows PowerShell. Výpis prostředků a práci s následujícími položkami je důležité základní úlohy ve většině nastavení pro správu, proto jsme tyto úlohy podrobně popisují.

### <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a>Vytváření výčtu souborů, složek a klíčů registru (Get-ChildItem)

Protože získání kolekce položek z konkrétního umístění je takový běžné úlohy, **Get-ChildItem** rutiny je určený konkrétně pro vrátí všechny položky v rámci kontejneru, jako je například složka nebyl nalezen.

Pokud chcete vrátit všechny soubory a složky, které jsou obsaženy přímo v rámci složky C:\\Windows, zadejte:

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

Výpis vypadá podobně jako na co se zobrazí při zadávání **dir** v příkaz **Cmd.exe**, nebo **ls** příkazu v příkazovém řádku systému UNIX.

Pomocí parametrů můžete provádět velmi složité výpisy **Get-ChildItem** rutiny. Podíváme se na několik scénářů dále. Zobrazí se syntaxe **Get-ChildItem** rutiny zadáním:

```powershell
Get-Command -Name Get-ChildItem -Syntax
```

Tyto parametry můžete kombinovat a namapovat na vysoce přizpůsobených výstup.

#### <a name="listing-all-contained-items--recurse"></a>Výpis všech položek obsažené (-Recurse)

K zobrazení položek ve složce Windows a všechny položky, které jsou obsaženy v rámci podsložky, použijte **Recurse** parametr **Get-ChildItem**. Výpis všechno, co se zobrazí ve složce Windows a položky v jejích podsložkách. Příklad:

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

#### <a name="filtering-items-by-name--name"></a>Filtrování podle názvu položky (-Name)

Chcete-li zobrazit pouze názvy položek, použijte **název** parametr **Get-Childitem**:

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

#### <a name="forcibly-listing-hidden-items--force"></a>Nuceně výpis skryté položky (-Force)

Položky, které nejsou obvykle viditelná v Průzkumníku souborů nebo Cmd.exe nejsou zobrazeny ve výstupu příkazu **Get-ChildItem** příkazu. Chcete-li zobrazit skryté položky, použijte **platnost** parametr **Get-ChildItem**. Příklad:

```powershell
Get-ChildItem -Path C:\Windows -Force
```

Tento parametr je s názvem vynutit, protože normálního chování můžete přepsat nuceně **Get-ChildItem** příkazu. Platnost je často používaný parametr, který vynutí akci, která rutina nebude fungovat normálně, ale neprovede žádnou akci, která ohrožuje zabezpečení systému.

#### <a name="matching-item-names-with-wildcards"></a>Odpovídající názvy položek se zástupnými znaky

**Rutina Get-ChildItem** příkaz přijímá zástupné znaky v cestě položky do seznamu.

Protože vyhledávání pomocí zástupných znaků se postará modul prostředí Windows PowerShell, používá stejná notace všechny rutiny, které přijímá zástupné znaky a mají stejné chování odpovídající. Obsahuje zástupný znak zápisu Windows Powershellu:

- Hvězdička (\*) odpovídá žádnému nebo více výskytům libovolného znaku.

- Otazník (?) shoda právě jednoho znaku.

- Levá závorka (\[) znaků a pravá hranatá závorka (]) znaků před a za sadu znaků, které mají být porovnány.

Tady je několik příkladů toho, jak funguje specifikace zástupných znaků.

Chcete-li vyhledat všechny soubory v adresáři Windows s příponou **.log** a přesně pět znaků v názvu základní, zadejte následující příkaz:

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

Chcete-li vyhledat všechny soubory, které začínají písmenem **x** v adresáři Windows, zadejte:

```powershell
Get-ChildItem -Path C:\Windows\x*
```

Chcete-li vyhledat všechny soubory, jejichž názvy začínají řetězcem **x** nebo **z**, typ:

```powershell
Get-ChildItem -Path C:\Windows\[xz]*
```

#### <a name="excluding-items--exclude"></a>S výjimkou položky (-vyloučení)

Můžete vyloučit konkrétní položky pomocí **vyloučit** parametr Get-ChildItem. To umožňuje provádět složité filtrování v jediném příkazu.

Předpokládejme například, se pokoušíte najít knihovnu DLL služeb Windows čas do složky System32, a vše, co můžete nezapomeňte o název knihovny DLL je, že začíná řetězcem "W" a "32" v sobě obsahuje.

Výraz, jako jsou **w\&#42; 32\&#42;. Knihovna DLL** najdete všechny knihovny DLL, které splňují podmínky, ale také může vrátit Windows 95 a Windows compatibility 16bitové knihovny DLL, které zahrnují "95" nebo "16" v názvu. Při vynechání souborů, které mají některý z těchto čísel v názvu pomocí **vyloučit** parametr se vzorem  **\&#42;\[ 9516]\&#42;**:

```
PS> Get-ChildItem -Path C:\WINDOWS\System32\w*32*.dll -Exclude *[9516]*

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
-a---        2004-08-04   8:00 AM      18432 wtsapi32.dll
```

#### <a name="mixing-get-childitem-parameters"></a>Kombinování parametry Get-ChildItem

Můžete použít několik parametrů **Get-ChildItem** rutiny v jednom příkazu. Předtím, než je kombinovat parametry, ujistěte se, že rozumíte vyhledávání pomocí zástupných znaků. Například následující příkaz vrátí žádné výsledky:

```powershell
Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

Nebyly nalezeny žádné výsledky, i když existují dvě knihovny DLL, které začínají písmenem "z" ve složce Windows.

Nebyly vráceny žádné výsledky, protože jsme zadali zástupný znak jako součást cesty. I v případě, že příkaz je rekurzivní, **Get-ChildItem** rutiny s omezením pomocí specifikátoru položky na ty, které jsou ve složce Windows s názvy končící ".dll".

Chcete-li určit rekurzivní vyhledávání pro soubory, jejichž názvy odpovídají zvláštní vzor, použijte **– zahrnout** parametru.

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
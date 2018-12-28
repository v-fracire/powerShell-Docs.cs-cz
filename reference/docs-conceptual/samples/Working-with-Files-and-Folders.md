---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce se soubory a složkami
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: a8d57a1c269d95e692db6c3f1ae10df49e305e4e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403674"
---
# <a name="working-with-files-and-folders"></a>Práce se soubory a složkami

Procházení jednotek Windows Powershellu a manipulace s položkami na nich je podobný práce se soubory a složky na fyzických disků Windows. Tato část popisuje, jak zacházet s konkrétní souborům a složkám manipulací s použitím prostředí PowerShell.

### <a name="listing-all-the-files-and-folders-within-a-folder"></a>Výpis všech souborů a složek ve složce

Všechny položky můžete získat přímo ve složce pomocí **Get-ChildItem**. Přidat nepovinný **platnost** parametr zobrazení skrytých nebo položky system. Tento příkaz například zobrazí přímý obsah Windows Powershellu jednotce C (který je stejný jako fyzický disk Windows C):

```powershell
Get-ChildItem -Path C:\ -Force
```

Příkaz vypíše pouze přímo obsažené položky, podobně jako pomocí jeho Cmd.exe **DIR** příkazu nebo **ls** v prostředí systému UNIX. Chcete-li zobrazit položky obsažené, je třeba zadat **-Recurse** také parametr. (To může trvat extrémně dlouhou dobu pro dokončení.) Chcete-li vypsat vše na jednotce C:

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

**Rutina Get-ChildItem** můžete filtrovat položky, které její **cesta**, **filtr**, **zahrnout**, a **vyloučit** parametry, ale ty jsou obvykle pouze na základě názvu. Pokud chcete provádět složité filtrování založené na jiné vlastnosti položek pomocí **Where-Object**.

Následující příkaz vyhledá všechny spustitelné soubory ve složce Program Files, které bylo naposledy změněno po 1 říjnu 2005 a které jsou menší než 1 megabajt ani větší než 10 MB:

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

### <a name="copying-files-and-folders"></a>Kopírování souborů a složek

Kopírování se provádí pomocí **Copy-Item**. Následující příkaz vytvoří zálohu C:\\boot.ini do C:\\boot.bak:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

Pokud cílový soubor už existuje, se nezdaří pokus o kopírování. Chcete-li přepsat existující cíl, použijte **platnost** parametr:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

Tento příkaz funguje i v případě, že cíl je jen pro čtení.

Kopírování složek funguje stejným způsobem. Tento příkaz kopíruje složky C:\\temp\\test1 do nové složky C:\\temp\\nástroji DeleteMe rekurzivně:

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

Můžete také zkopírovat výběr položek. Následující příkaz zkopíruje všechny soubory s příponou .txt kdekoli součástí c:\\data do c:\\temp\\text:

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

Další nástroje můžete stále použít ke zkopírování souborů systému. Příkazu XCOPY, ROBOCOPY a modelu COM objekty, jako **Scripting.FileSystemObject,** všechny fungují v prostředí Windows PowerShell. Například můžete použít modul Windows Script Host **Scripting.FileSystem COM** třídy zálohování C:\\boot.ini do C:\\boot.bak:

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

### <a name="creating-files-and-folders"></a>Vytváření souborů a složek

Vytvoření nové položky funguje na všichni poskytovatelé Windows Powershellu. Pokud zprostředkovatele Windows PowerShell obsahuje víc než jeden typ položky – například zprostředkovatele systému souborů Windows Powershellu rozlišuje mezi adresářů a souborů, je třeba zadat typ položky.

Tento příkaz vytvoří novou složku C:\\temp\\nová složka:

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

Tento příkaz vytvoří nový prázdný soubor C:\\temp\\novou složku\\soubor.txt

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

### <a name="removing-all-files-and-folders-within-a-folder"></a>Odebrání všech souborů a složek ve složce

Můžete odebrat obsažené položky pomocí **Remove-Item**, ale zobrazí se výzva k potvrzení odebrání, pokud položka obsahuje cokoli. Například, pokud při pokusu o odstranění složky C:\\temp\\nástroji DeleteMe, který obsahuje jiné položky, prostředí Windows PowerShell vás vyzve k potvrzení před odstranit tuto složku:

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Pokud nechcete vyzváni k zadání jednotlivých obsažené položky, určete **Recurse** parametr:

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

### <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a>Mapování do místní složky jako dostupná jednotka Windows

Můžete také namapovat do místní složky pomocí **subst** příkazu. Následující příkaz vytvoří místní jednotku, kterou P: root v místním adresáři Program Files:

```powershell
subst p: $env:programfiles
```

Stejně jako u síťových jednotkách namapované jednotky v rámci prostředí Windows PowerShell pomocí **subst** jsou okamžitě viditelné pro prostředí Windows PowerShell.

### <a name="reading-a-text-file-into-an-array"></a>Čtení textového souboru do pole

Jeden z běžných formátů úložiště pro textová data se v souboru samostatné řádky, které jsou považovány za odlišné datové prvky. **Get-Content** rutinu je možné číst celý soubor v jednom kroku, jak je znázorněno zde:

```
PS> Get-Content -Path C:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional"
 /noexecute=AlwaysOff /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS=" Microsoft Windows XP Professional
with Data Execution Prevention" /noexecute=optin /fastdetect
```

**Get-Content** již zpracovává data načtená ze souboru jako pole s jedním prvkem na řádek obsah souboru. Můžete to ověřit tak, že zkontrolujete **délka** vráceného obsahu:

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

Tento příkaz je zvláště užitečná pro zobrazení seznamů informace do prostředí Windows PowerShell přímo. Například může ukládat seznam názvů počítačů nebo IP adres v souboru C:\\temp\\domainMembers.txt názvem jednu na každý řádek v souboru. Můžete použít **Get-Content** načíst obsah souboru a umístit je do proměnné **$Computers**:

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

**$Computers** je nyní pole obsahující název počítače v jednotlivých prvcích.

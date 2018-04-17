---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce se soubory a složkami
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: 6b1fcd438570c8708aa87e4b213f33474921d5f8
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-files-and-folders"></a>Práce se soubory a složkami

Procházení jednotky prostředí Windows PowerShell a manipulace s nimi prostřednictvím položky z nich je podobná práce se soubory a složky na fyzické disky systému Windows. Tato část popisuje postupy řešení konkrétních souborů a složek manipulací s adresami pomocí prostředí PowerShell.

### <a name="listing-all-the-files-and-folders-within-a-folder"></a>Výpis všech souborů a složek ve složce

Všechny položky přímo ve složce můžete získat pomocí **Get-ChildItem**. Přidejte volitelné **Force** parametr zobrazení skrytý nebo položky system. Tento příkaz například zobrazí přímé obsah Windows PowerShell jednotka C (což je stejný jako fyzický disk systému Windows C):

```powershell
Get-ChildItem -Path C:\ -Force
```

Příkaz uvádí jenom přímo obsažených položek, podobně jako pomocí jeho Cmd.exe **DIR** příkaz nebo **ls** v prostředí systému UNIX. Chcete-li zobrazit položky, budete muset zadat **-Recurse** také parametr. (To může trvat dokončení velmi dlouho.) Seznam vše na jednotce C:

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

**Get-ChildItem** můžete filtrovat položky s jeho **cesta**, **filtru**, **zahrnout**, a **vyloučit** parametry, ale ty jsou obvykle pouze na základě názvu. Můžete provádět komplexní filtrování založené na jiné vlastnosti položek pomocí **Where-Object**.

Následující příkaz vyhledá všechny spustitelné soubory ve složce Program Files, které jsou menší než 1 megabajt ani větší než 10 MB a která byly poslední změny po 1. října 2005:

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

### <a name="copying-files-and-folders"></a>Kopírování souborů a složek

Kopírování provádí pomocí **Copy-Item**. Následující příkaz zálohuje C:\\boot.ini do C:\\boot.bak:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

Pokud cílový soubor již existuje, kopie pokus selže. Pokud chcete přepsat existující cíl, použijte **Force** parametr:

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

Tento příkaz lze použít i v případě, že cíl je jen pro čtení.

Kopírování složek funguje stejným způsobem. Tento příkaz zkopíruje složce C:\\temp\\test1 do nové složky C:\\temp\\nástroji DeleteMe rekurzivně:

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

Můžete také zkopírovat výběr položek. Následující příkaz zkopíruje všechny soubory s příponou .txt kdekoli součástí c:\\data do c:\\temp\\text:

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

Můžete stále dalších nástrojů ke zkopírování systému souborů. XCOPY ROBOCOPY a COM objekty, jako **Scripting.FileSystemObject,** všechny fungují v prostředí Windows PowerShell. Například můžete použít modul Windows Script Host **Scripting.FileSystem COM** třída zálohování C:\\boot.ini do C:\\boot.bak:

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

### <a name="creating-files-and-folders"></a>Vytváření souborů a složek

Vytvoření nové položky stejné funguje na všech poskytovatelů prostředí Windows PowerShell. Pokud poskytovatele prostředí Windows PowerShell obsahuje víc než jeden typ položky – například zprostředkovateli prostředí Windows PowerShell pro systém souborů rozlišuje adresářů a souborů, je třeba zadat typ položky.

Tento příkaz vytvoří novou složku C:\\temp\\novou složku:

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

Tento příkaz vytvoří nový prázdný soubor C:\\temp\\novou složku\\soubor.txt

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

### <a name="removing-all-files-and-folders-within-a-folder"></a>Odebrání všech souborů a složek ve složce

Můžete odebrat pomocí položky **odebrat položky**, ale zobrazí se výzva k potvrzení odebrání, pokud položka obsahuje cokoliv jiného. Například, pokud se pokusíte odstranit složku C:\\temp\\nástroji DeleteMe, který obsahuje další položky, prostředí Windows PowerShell vás vyzve k potvrzení před odstranit tuto složku:

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Pokud nechcete pro každou položku obsažené vyzváni, zadejte **Recurse** parametr:

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

### <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a>Mapování do místní složky jako přístupné jednotka Windows

Můžete také mapovat do místní složky pomocí **subst** příkaz. Následující příkaz vytvoří na místní jednotku, kterou P: root v místním adresáři soubory programu:

```powershell
subst p: $env:programfiles
```

Stejně jako v síťové jednotky, jednotky namapovaný v rámci prostředí Windows PowerShell pomocí **subst** jsou okamžitě viditelné pro prostředí Windows PowerShell.

### <a name="reading-a-text-file-into-an-array"></a>Čtení textových souborů na pole

Jeden z běžných formátů úložiště pro data textu je v souboru s samostatné řádky, které jsou považovány za různé datové prvky. **Get-Content** rutiny můžete použít ke čtení celý soubor v jednom kroku, jak je vidět tady:

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

**Get-Content** již zpracovává data načtená ze souboru jako pole, s jedním prvkem na každý řádek obsahu souboru. Můžete to ověřit kontrolou **délka** vrácený obsahu:

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

Tento příkaz je nejvhodnější pro získávání přímo seznam informací do prostředí Windows PowerShell. Například může uložit seznam názvů počítačů nebo IP adresy v souboru C:\\temp\\domainMembers.txt s určitým názvem na každém řádku souboru. Můžete použít **Get-Content** načíst obsah souboru a jejich umístění v proměnné **$Computers**:

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

**$Computers** je nyní pole obsahující název počítače v jednotlivých prvků.

---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s položkami registru
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: bffdf80931fc4dc570b584623487077dc5d449dc
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403866"
---
# <a name="working-with-registry-entries"></a>Práce s položkami registru

Protože položky registru jsou vlastnosti klíče a v důsledku toho nelze procházet přímo, musíme provést trochu jiný přístup při práci s nimi.

### <a name="listing-registry-entries"></a>Výpis položky registru

Zkontrolujte položky registru mnoha různými způsoby. Nejjednodušší způsob je získat názvy vlastností, které jsou spojené s klíčem. Například, pokud chcete zobrazit názvy položek v klíči registru **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**, použijte **Get-Item** . Klíče registru mají vlastnost s obecným názvem "Vlastnosti", který je uveden seznam položky registru v klíči. Následující příkaz vybere vlastnost Property a rozbalí položky tak, aby se zobrazí v seznamu:

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

Chcete-li zobrazit položky registru ve formě lépe čitelný, použijte **Get-ItemProperty**:

```
PS> Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

Vlastnosti související s prostředí Windows PowerShell pro klíč jsou předponu "PS", jako například **PSPath**, **PSParentPath**, **PSChildName**, a **PSProvider** .

Můžete použít "**.**" notace pro odkazování na aktuální umístění. Můžete použít **nastavení umístění** změnit **CurrentVersion** registru kontejneru první:

```powershell
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Alternativně můžete použít předdefinované PSDrive HKLM s **nastavení umístění**:

```powershell
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Pak můžete použít "**.**" podle aktuálního umístění do seznamu vlastností bez zadání úplné cesty:

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

Rozšíření cesty funguje stejně jako v systému souborů, takže z tohoto místa můžete získat **ItemProperty** výpis pro **HKLM:\\softwaru\\Microsoft\\Windows \\Pomáhají** pomocí **Get-ItemProperty-cesta... \\Pomáhají**.

### <a name="getting-a-single-registry-entry"></a>Získání položky jednoho registru

Pokud chcete načíst konkrétní položky klíče registru, můžete použít jeden z několika možných přístupů. Tento příklad vyhledá hodnotu **DevicePath** v **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**.

Pomocí **Get-ItemProperty**, použijte **cesta** parametru určete název klíče a **název** parametr zadejte název **DevicePath** položka.

```
PS> Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

Tento příkaz vrátí standardní vlastnosti prostředí Windows PowerShell společně s **DevicePath** vlastnost.

> [!NOTE]
> I když **Get-ItemProperty** má **filtr**, **zahrnout**, a **vyloučit** parametry, nelze je použít k filtrování podle názvu vlastnosti. Přečtěte si tyto parametry ke klíčům registru – což jsou cesty položky – a položky registru není – které jsou vlastnosti položky.

Další možností je použít nástroj příkazového řádku Reg.exe. Nápovědu k reg.exe, zadejte **reg.exe /?** na příkazovém řádku. Pokud chcete zjistit položce, použijte reg.exe, jak je znázorněno v následujícím příkazu:

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

Můžete také použít **WshShell COM** objekt také najít některé položky registru, i když tato metoda nebude fungovat s velkými binárními datovými nebo s názvy položky registru, které obsahují znaky, například "\\"). Připojit k cesta položky s názvem vlastnosti \\ oddělovač:

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### <a name="creating-new-registry-entries"></a>Vytvoření nové položky registru

Chcete-li přidat novou položku s názvem "PowerShellPath" k **CurrentVersion** použití klíčů, **New-ItemProperty** s cestou ke klíči, název položky a hodnotu položky. V tomto příkladu my podnikneme hodnotu proměnné prostředí Windows PowerShell **$PSHome**, která ukládá ji do instalačního adresáře pro prostředí Windows PowerShell.

Pomocí následujícího příkazu můžete přidat novou položku klíče a příkaz také vrátí informace o nové položky:

```
PS> New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome

PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

**Typ PropertyType** musí být název **Microsoft.Win32.RegistryValueKind** člena výčtu v následující tabulce:

|Typ hodnoty|Význam|
|----------------------|-----------|
|Binární|Binární data|
|DWord|Číslo, které je platný typ UInt32|
|ExpandString|Řetězec, který může obsahovat proměnné prostředí, které jsou dynamicky rozbaleny|
|Řetězci FixedLength multiString|Víceřádkový řetězec|
|Řetězec|Libovolnou hodnotou řetězce|
|QWord|8 bajtů binárních dat|

> [!NOTE]
> Můžete přidat položku registru do víc umístění tak, že zadáte pole hodnot **cesta** parametr:

```powershell
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

Můžete také přepsat existující hodnotu položky registru tak, že přidáte **platnost** parametr k libovolnému **New-ItemProperty** příkazu.

### <a name="renaming-registry-entries"></a>Přejmenování položky registru

Přejmenovat **PowerShellPath** položku "PSHome," použití **Rename-ItemProperty**:

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

Chcete-li zobrazit hodnotu byl přejmenován, přidejte **PassThru** parametr k příkazu.

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### <a name="deleting-registry-entries"></a>Odstranění položky registru

Chcete-li odstranit PSHome i PowerShellPath položky registru, použijte **Remove-ItemProperty**:

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```
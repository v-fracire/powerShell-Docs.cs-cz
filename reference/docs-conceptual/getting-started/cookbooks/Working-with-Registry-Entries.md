---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Práce s položky registru"
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: 039203a1a6549d4ba33424a278e4803a5e143d4d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-registry-entries"></a>Práce s položky registru
Protože položky registru jsou vlastnosti klíčů a jako takový nelze procházet přímo, je potřeba provést mírně odlišný postup při práci s nimi.

### <a name="listing-registry-entries"></a>Výpis položky registru
Zkontrolujte položky registru mnoha různými způsoby. Nejjednodušší způsob, jak se má získat názvy vlastností, které jsou přidružené k klíči. Chcete-li například zobrazit názvy položek v klíči registru **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**, použijte **Get-položky** . Klíče registru mít vlastnost s obecný název "Vlastnosti", který je přehled položek registru v klíči. Následující příkaz vybere vlastnost a rozbalí položky tak, aby se zobrazí v seznamu:

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

Chcete-li zobrazit položky registru v přehlednějším tvaru, použijte **Get-ItemProperty**:

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

Vlastnosti týkající se prostředí Windows PowerShell pro klíč jsou všechny s předponou "PS", jako například **PSPath**, **PSParentPath**, **PSChildName**, a **PSProvider** .

Můžete použít "**.**" zápis pro odkaz na aktuální umístění. Můžete použít **nastavení umístění** změnit na **CurrentVersion** registru kontejneru první:

```
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Alternativně můžete použít předdefinované PSDrive HKLM s **nastavení umístění**:

```
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

Potom můžete pomocí "**.**" zápis pro aktuální umístění zobrazte seznam vlastností bez zadání úplnou cestu:

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

Cesta rozšíření funguje stejně jako v systému souborů, takže z tohoto umístění můžete získat **ItemProperty** výpis pro **HKLM:\\softwaru\\Microsoft\\Windows \\Pomoci** pomocí **Get-ItemProperty-cesta... \\Pomoci**.

### <a name="getting-a-single-registry-entry"></a>Získání položky jeden registru
Pokud chcete načíst konkrétní položky klíče registru, můžete použít jeden z několika možných přístupů. Tento příklad vyhledá hodnotu **DevicePath** v **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**.

Pomocí **Get-ItemProperty**, použijte **cesta** parametr k zadání názvu klíče a **název** parametr k určení názvu **DevicePath** položku.

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
> I když **Get-ItemProperty** má **filtru**, **zahrnout**, a **vyloučit** parametry, budou nelze použít pro filtrování podle názvu vlastnosti. Tyto parametry odkazovat na klíče registru – které jsou položky cesty – a není položky registru – které jsou vlastnosti položky.

Další možností je použít nástroj příkazového řádku Reg.exe. Chcete-li zobrazit nápovědu k reg.exe, zadejte **reg.exe /?** na příkazovém řádku. Chcete-li najít položce, použijte reg.exe jak je znázorněno v následujícím příkazu:

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

Můžete také **WshShell COM** objekt také se najít některé položky registru, i když tato metoda nefunguje velké binární data nebo s názvy položek registru, které obsahují znaky, například "\\"). Název vlastnosti připojení k cesta položky s \\ oddělovače:

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### <a name="creating-new-registry-entries"></a>Vytvoření nové položky registru
Chcete-li přidat novou položku s názvem "PowerShellPath" do **CurrentVersion** použití klíče, **New-ItemProperty** s cestou k klíč, název vstupního a hodnotu položky. V tomto příkladu jsme bude trvat hodnotu proměnné prostředí Windows PowerShell **$PSHome**, která ukládá cestu k adresáři instalace pro prostředí Windows PowerShell.

Pomocí následujícího příkazu můžete přidat novou položku na klíč, a příkaz také vrátí informace o nový záznam:

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

**PropertyType** musí být název **Microsoft.Win32.RegistryValueKind** – člen výčtu z v následující tabulce:

|Hodnota PropertyType|Význam|
|----------------------|-----------|
|Binární|Binární data|
|DWord|Číslo, které je platný UInt32|
|ExpandString|Řetězec, který může obsahovat proměnné prostředí, které jsou dynamicky rozšířit|
|MultiString|Víceřádkový řetězec|
|Řetězec|Libovolnou hodnotu řetězce|
|QWORD –|8 bajtů binárních dat|

> [!NOTE]
> Položky registru můžete přidat do víc umístění zadáním hodnot pro pole **cesta** parametr:

```
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

Můžete také přepsat existující hodnotu položky registru přidáním **Force** parametr žádnému **New-ItemProperty** příkaz.

### <a name="renaming-registry-entries"></a>Přejmenování položky registru
Přejmenování **PowerShellPath** položku na "PSHome," použití **přejmenování ItemProperty**:

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

Chcete-li zobrazit přejmenovat hodnotu, přidejte **PassThru** do příkazu parametr.

```
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### <a name="deleting-registry-entries"></a>Odstranění položky registru
Pokud chcete odstranit položky registru PSHome i PowerShellPath, použijte **Remove-ItemProperty**:

```
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```


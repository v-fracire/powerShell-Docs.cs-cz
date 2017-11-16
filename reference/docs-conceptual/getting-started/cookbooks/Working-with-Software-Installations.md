---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Práce s instalací softwaru"
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: 2078376a8be19c9ff8ecc44183eb89f14bc388ed
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-software-installations"></a>Práce s instalací softwaru
Aplikace, které jsou určeny k použití Instalační služby systému Windows je možné přistupovat prostřednictvím rozhraní WMI na **objektu Win32_Product** třídy, ale ne všechny aplikace používá v dnešní době používá Instalační služba systému Windows. Protože instalační služba systému Windows obsahuje širokou škálu standardní techniky pro práci s instalovat aplikace, jsme se soustředí hlavně na tyto aplikace. Aplikace, které používají rutiny alternativní nastavení nebude spravovaný obecně Instalační služby systému Windows. Konkrétní postupy pro práci s těmito aplikacemi bude záviset na instalační program softwaru a rozhodnutí o vývojář aplikace.

> [!NOTE]
> Aplikace, které jsou nainstalované pomocí kopírování souborů aplikace do počítače obvykle nelze spravovat pomocí technik popsaných v tomto poli. Tyto aplikace jako soubory a složky, můžete spravovat pomocí technik popsaných v oddílu "Práce se soubory a složky".

### <a name="listing-windows-installer-applications"></a>Výpis aplikace Instalační služby systému Windows
K zobrazení seznamu aplikace instalované pomocí Instalační služby systému Windows v místním nebo vzdáleném systému, použijte následující jednoduchý dotaz rozhraní WMI:

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

Chcete-li zobrazit všechny vlastnosti objektu Win32_Product objekt zobrazení, použijte parametr vlastnosti formátování rutin, jako je například rutinu Format-List s hodnotou \* (vše).

```
PS> Get-WmiObject -Class Win32_Product -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Microsoft .NET Framework 2.0"} | Format-List -Property *
Name              : Microsoft .NET Framework 2.0
Version           : 2.0.50727
InstallState      : 5
Caption           : Microsoft .NET Framework 2.0
Description       : Microsoft .NET Framework 2.0
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
InstallDate       : 20060506
InstallDate2      : 20060506000000.000000-000
InstallLocation   :
PackageCache      : C:\WINDOWS\Installer\619ab2.msi
SKUNumber         :
Vendor            : Microsoft Corporation
```

Nebo můžete použít **Get-WmiObject filtru** parametr vybrat jenom rozhraní Microsoft .NET Framework 2.0. Protože filtr použité v tomto příkazu je filtr rozhraní WMI, používá syntaxi dotazu jazyka WQL (WMI), není syntaxe prostředí Windows PowerShell. Místo toho:

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

Všimněte si, že dotazy WQL často znaky, jako jsou mezery nebo znaky rovná, které mají zvláštní význam v prostředí Windows PowerShell. Z tohoto důvodu je vhodné vždy hodnota parametru filtru uzavřít do uvozovek. Můžete také použít prostředí Windows PowerShell řídicí znak, backtick (\`), i když proto nemusí zlepšení čitelnosti. Příkaz je ekvivalentní předchozí příkaz a vrátí stejné výsledky, ale používá backtick, abyste se vyhnuli speciální znaky, místo citací řetězec celý filtru.

```
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

Pro zobrazení seznamu pouze vlastnosti, které vás zajímají, použijte parametr vlastností formátování rutin seznam požadované vlastnosti.

```
Get-WmiObject -Class Win32_Product -ComputerName . | Format-List -Property Name,InstallDate,InstallLocation,PackageCache,Vendor,Version,IdentifyingNumber
...
Name              : HighMAT Extension to Microsoft Windows XP CD Writing Wizard
InstallDate       : 20051022
InstallLocation   : C:\Program Files\HighMAT CD Writing Wizard\
PackageCache      : C:\WINDOWS\Installer\113b54.msi
Vendor            : Microsoft Corporation
Version           : 1.1.1905.1
IdentifyingNumber : {FCE65C4E-B0E8-4FBD-AD16-EDCBE6CD591F}
...
```

Nakonec najít pouze názvy nainstalované aplikace, jednoduchou **formátu celou** příkaz zjednodušuje výstup:

```
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

I když nyní je k dispozici několik způsobů, jak podívejte se na aplikace, které používá Instalační služba systému Windows pro instalaci, jsme nepřemýšlí jiné aplikace. Protože většina standardních aplikací zaregistrovat jejich odinstalační program, který se systémem Windows, jsme můžete pracovat s těmi, která místně tak, že najdete je v registru systému Windows.

### <a name="listing-all-uninstallable-applications"></a>Výpis všech bez možnosti odinstalace aplikace
I když neexistuje žádné zaručenou způsob, jak najít každá aplikace v systému, je možné najít všechny programy s výpisech zobrazí v dialogovém okně Přidat nebo odebrat programy. Přidat nebo odebrat programy najde tyto aplikace v následující klíč registru:

**HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion\\odinstalovat**.

Můžeme také zkontrolovat, jestli tento klíč k vyhledání aplikace. Aby bylo snazší, chcete-li zobrazit klíč odinstalace, jsme můžete namapovat jednotku prostředí Windows PowerShell do tohoto umístění registru:

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall    

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> **HKLM:** jednotka mapovaná do kořenového adresáře **HKEY_LOCAL_MACHINE**, takže jsme použili tuto jednotku v cestě ke klíči odinstalovat. Místo **HKLM:** jsme může zadali cestu registru pomocí **HKLM** nebo **HKEY_LOCAL_MACHINE**. Výhodou použití existující jednotce registru je, že budeme moci použít kartu dokončení vyplnit názvy klíčů, takže jsme není potřeba je zadat.

Nyní je k dispozici na jednotku s názvem "Odinstalovat", který umožňuje rychle a snadno najít aplikace instalace. Počet nainstalovaných aplikací jsme můžete najít určovat počet klíčů registru v odinstalace: jednotku prostředí Windows PowerShell:

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

Jsme můžete hledat v seznamu aplikací další pomocí řady různých způsobů, počínaje **Get-ChildItem**. Chcete získat seznam aplikací a uložit je do **$UninstallableApplications** proměnnou, použijte následující příkaz:

```
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> Používáme zdlouhavé název proměnné pro přehlednost. Při skutečném použití neexistuje žádný důvod používat dlouhé názvy. I když používáte – dokončování pomocí tabulátorů pro názvy proměnných můžete taky názvy znaků 1 – 2 pro rychlost. Déle, popisné názvy jsou velmi užitečné při vývoji kód pro opakované použití.

K zobrazení hodnot položky v registru v klíči registru v odinstalovat, použijte metodu GetValue klíče registru. Hodnota metody je název položky registru.

Například pro vyhledání názvů zobrazení aplikací v klíči odinstalovat, použijte následující příkaz:

```
PS> Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("DisplayName") }
```

Není zaručeno, že tyto hodnoty jsou jedinečné. Dva nainstalované položky se zobrazí jako "Windows Media Encoder 9 Series" v následujícím příkladu:

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

### <a name="installing-applications"></a>Instalace aplikace
Můžete použít **objektu Win32_Product** třída k instalaci balíčků Instalační služby systému Windows, vzdáleně nebo místně.

> [!NOTE]
> Na Windows Vista, Windows Server 2008 a novějších verzích Windows Pokud chcete nainstalovat aplikaci, musí spustit prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".

Při instalaci vzdáleně, použijte síťovou cestu Universal Naming Convention (UNC) pro zadání cesty k balíčku MSI, protože subsystém WMI nerozumí cesty prostředí Windows PowerShell. Například k instalaci balíčku NewPackage.msi umístěný ve sdílené síťové složce \\ \\AppServ\\dsp na vzdáleném počítači PC01, zadejte následující příkaz v příkazovém řádku prostředí Windows PowerShell:

```
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq "Win32_Product"}).Install(\\AppSrv\dsp\NewPackage.msi)
```

Aplikace, které nepoužívají technologii Instalační služby systému Windows může mít specifické pro aplikaci metody dostupné pro automatické nasazení. Pokud chcete zjistit, zda je metoda pro automatizaci nasazení, naleznete v dokumentaci k aplikaci nebo se obraťte na systém pro podporu dodavatele aplikace. V některých případech i v případě, že dodavatele aplikace není návrh konkrétně aplikace pro automatizaci instalace instalační program softwaru výrobce pravděpodobně některé postupy pro automatizaci.

### <a name="removing-applications"></a>Odebírání aplikací
Odebrání balíčku Instalační služby systému Windows pomocí prostředí Windows PowerShell funguje v přibližně stejným způsobem jako instalaci balíčku. Tady je příklad, který vybere balíček, který chcete odinstalovat, na základě jeho názvu; v některých případech může být snazší filtrovat, u kterých **hodnotu IdentifyingNumber**:

```
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

Odebrání dalších aplikací není proto je poměrně jednoduché i v případě, že se neprovádí místně. Nemůžeme najít řetězce odinstalace příkazového řádku pro tyto aplikace extrahováním **UninstallString** vlastnost. Tato metoda funguje pro aplikace Instalační služby systému Windows a zobrazování pod klíčem odinstalovat starší programů:

```
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

Výstup můžete filtrovat podle zobrazovaného jména, pokud chcete:

```
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -like "Win*"} | ForEach-Object -Process { $_.GetValue("UninstallString") }
```

Tyto řetězce však nemusí být použitelná přímo z příkazového řádku prostředí Windows PowerShell bez některé úprav.

### <a name="upgrading-windows-installer-applications"></a>Upgrade aplikace Instalační služby systému Windows
Pokud chcete upgradovat aplikaci, musíte znát název aplikace a cestu pro balíček s upgradem aplikace. S touto informací se můžete upgradovat aplikace pomocí jednoho příkazu prostředí Windows PowerShell:

```
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```


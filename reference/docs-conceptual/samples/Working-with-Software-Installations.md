---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s nainstalovaným softwarem
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: bb97ad37c4295351c0fc2e3c6e1209c8dd673f06
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404102"
---
# <a name="working-with-software-installations"></a>Práce s nainstalovaným softwarem

Aplikace, které jsou navrženy pro použití Instalační služby systému Windows je přístupná prostřednictvím služby WMI **objektu Win32_Product** třídy, ale u některých aplikací není používán Dnes pomocí Instalační služby systému Windows. Vzhledem k tomu, že instalační služby systému Windows poskytuje širokou škálu standardní techniky pro práci s instalovat aplikace, jsme se soustředí hlavně na těchto aplikací. Aplikace, které používají rutiny alternativní nastavení nebude obecně spravovaný Instalační služby systému Windows. Konkrétní postupy pro práci s těmito aplikacemi bude záviset na instalační program softwaru a rozhodnutí vývojáře aplikace.

> [!NOTE]
> Aplikace, které jsou nainstalovány pomocí kopírování souborů aplikace do počítače obvykle nelze spravovat pomocí technik popsaných tady. Tyto aplikace jako soubory a složky, můžete spravovat pomocí technik popsaných v části "Práce se soubory a složky".

### <a name="listing-windows-installer-applications"></a>Výpis aplikací Instalační služby systému Windows

K zobrazení seznamu aplikací nainstalovaných Instalační služby systému Windows na místním nebo vzdáleném systému, použijte následující jednoduchý dotaz rozhraní WMI:

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .

IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

Chcete-li zobrazit všechny vlastnosti objektu Win32_Product objektu na obrazovce, použijte parametr vlastnosti formátování rutin, jako je například rutinu Format-List s hodnotou \* (vše).

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

Nebo můžete použít **Get-WmiObject filtr** parametr vybrat jenom rozhraní Microsoft .NET Framework 2.0. Vzhledem k tomu, že filtr použité v tomto příkazu je filtr rozhraní WMI, používá syntaxi dotazu jazyka WQL (WMI), není syntaxe prostředí Windows PowerShell. Místo toho:

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

Všimněte si, že dotazy WQL často znaky, jako jsou mezery ani rovnítko, které mají speciální význam v prostředí Windows PowerShell. Z tohoto důvodu je vhodné vždy hodnotu parametru filtru uzavřete do uvozovek. Můžete také použít řídicí znak prostředí Windows PowerShell prvními (\`), i když je možná lepší čitelnost. Následující příkaz je ekvivalentní předchozí příkaz vrátí stejné výsledky, ale prvními používá k uvození zvláštní znaky, namísto uvozovky u filtru celý řetězec.

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

K zobrazení seznamu pouze vlastnosti, které vás zajímají, použijte vlastnost parametru formátování rutin seznam požadovaných vlastností.

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

A konečně k vyhledání pouze názvy nainstalovaných aplikací, jednoduché **formátu celou** zjednodušuje výstup příkazu:

```powershell
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

I když teď máme několik způsobů, jak podívejte se na aplikace, které se používá pro instalace Instalační služby systému Windows, jsme nebyly považovány za jiné aplikace. Vzhledem k tomu, že většinu standardních aplikací zaregistrovat jejich odinstalační program s Windows, budeme pracovat s těmi, která místně, hledání v registru Windows.

### <a name="listing-all-uninstallable-applications"></a>Výpis všech aplikací bez možnosti odinstalace

Ačkoli neexistuje žádné zaručené způsob, jak najít všechny aplikace v systému, je možné najít všechny programy s výpisy zobrazí v dialogovém okně Přidat nebo odebrat programy. Přidat nebo odebrat programy najde tyto aplikace v následujícím klíči registru:

**HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion\\odinstalovat**.

Můžeme také můžete prozkoumat tento klíč chcete hledat aplikace. Aby bylo snazší zobrazit klíč odinstalovat, jsme namapujete jednotku prostředí Windows PowerShell do tohoto umístění registru:

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> **HKLM:** jednotka mapovaná do kořenového adresáře **HKEY_LOCAL_MACHINE**, takže jsme použili v cestě ke klíči odinstalovat tuto jednotku. Místo **HKLM:** jsme mohli zadali cestu registru pomocí **HKLM** nebo **HKEY_LOCAL_MACHINE**. Výhodou použití existujícího disku registru je, že jsme dokončování pomocí tabulátoru – použít tak, aby vyplnil v názvech klíčů, takže jsme není potřeba je zadat.

Teď máme jednotky s názvem "Odinstalovat", který je možné rychle a jednoduše vyhledejte instalace aplikací. Počet nainstalovaných aplikací nám můžete najít určeno spočítáním počet klíčů registru v odinstalaci: Jednotku prostředí Windows PowerShell:

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

Jsme můžete hledat v seznamu aplikací dál pomocí celé řady metod, počínaje **Get-ChildItem**. Chcete získat seznam aplikací a uložit je do **$UninstallableApplications** proměnné, použijte následující příkaz:

```powershell
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> Dlouhý název proměnné pro přehlednost používáme. V praxi neexistuje žádný důvod používat dlouhé názvy. I když používáte – dokončování pomocí tabulátoru pro názvy proměnných, můžete také použít 1 – 2 znaky názvu pro rychlost. Delší a popisné názvy jsou nejužitečnější, když vyvíjíte kód pro další použití.

K zobrazení hodnot z položky registru v klíčích registru pod odinstalovat, použijte metodu GetValue klíče registru. Hodnota metody je název položky registru.

Například pokud chcete vyhledat názvy zobrazení aplikací v klíči odinstalovat, použijte následující příkaz:

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('DisplayName') }
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

### <a name="installing-applications"></a>Instalace aplikací

Můžete použít **objektu Win32_Product** třídy nainstalovat balíčky Instalační služby systému Windows, vzdáleně nebo místně.

> [!NOTE]
> Ve Windows Vista, Windows Server 2008 a novějších verzích Windows jak nainstalovat aplikaci, je nutné spustit prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".

Při instalaci vzdáleně, použijte cestu sítě (Universal Naming Convention) pro zadání cesty k balíčku MSI, protože subsystém rozhraní WMI nerozumí cest prostředí Windows PowerShell. Například k instalaci balíčku NewPackage.msi umístěný ve sdílené síťové složce \\ \\AppServ\\dsp na vzdáleném počítači PC01, zadejte následující příkaz na příkazovém řádku Windows Powershellu:

```powershell
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq 'Win32_Product'}).Install(\\AppSrv\dsp\NewPackage.msi)
```

Aplikace, které nepoužívají technologie instalačního programu Windows mohou mít metody specifické pro aplikaci pro automatické nasazení. Pokud chcete zjistit, zda je metoda pro automatizaci nasazení, naleznete v dokumentaci k aplikaci nebo se obraťte na systém pro podporu dodavatele aplikace. V některých případech i v případě, že na dodavatele aplikace není návrhu konkrétně aplikace pro automatizaci instalace, pravděpodobně výrobce instalačního programu softwaru některé postupy pro automatizaci.

### <a name="removing-applications"></a>Odebírání aplikací

Odebírá se balíček Instalační služby systému Windows pomocí prostředí Windows PowerShell funguje v přibližně stejným způsobem jako instalaci balíčku. Tady je příklad, který vybere balíček odinstalovat na základě jeho názvu; v některých případech může být jednodušší filtr s **IdentifyingNumber**:

```powershell
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

Odebrání dalších aplikací není tak jednoduché to zase, i když dělat místně. Jsme najít odinstalace řetězce příkazového řádku pro tyto aplikace tak, že extrahují **UninstallString** vlastnost. Tato metoda funguje pro aplikace Instalační služby systému Windows a pro starší programy uvedené pod klíčem odinstalace:

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

Výstup můžete filtrovat podle zobrazovaného názvu, pokud chcete, můžete:

```powershell
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue('DisplayName') -like 'Win*'} | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

Tyto řetězce však nemusí být možné přímo použít z příkazového řádku Windows Powershellu bez určitými úpravami.

### <a name="upgrading-windows-installer-applications"></a>Upgrade aplikace Instalační služby systému Windows

Pokud chcete upgradovat aplikaci, budete muset znát název aplikace a cestu pro balíček s upgradem aplikace. Pomocí těchto informací můžete upgradovat aplikaci pomocí jediného příkazu Windows Powershellu:

```powershell
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```
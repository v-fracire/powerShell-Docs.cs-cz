---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa jednotek Windows PowerShellu
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: cfc5418e9d2efb1a786817e1b941d75e22291742
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="managing-windows-powershell-drives"></a>Správa jednotek Windows PowerShellu

A *jednotku prostředí Windows PowerShell* je umístění úložiště dat, která se zobrazí jako jednotce systému souborů v prostředí Windows PowerShell. Zprostředkovatelé prostředí Windows PowerShell některé jednotky pro vytvoření, jako jsou jednotky systému souborů (včetně C: a D:), registru jednotky (HKCU: a HKLM:) a jednotky certifikátu (Cert:), a můžete vytvořit vlastní jednotky prostředí Windows PowerShell. Tyto disky jsou velmi užitečné, ale jsou k dispozici pouze v rámci prostředí Windows PowerShell. Nelze k nim přistupovat pomocí jiné nástroje systému Windows, jako je například Průzkumník souborů nebo Cmd.exe.

Prostředí Windows PowerShell používá podstatné jméno, **PSDrive**, příkazy, které fungují v prostředí Windows PowerShell jednotky. Pro seznam prostředí Windows PowerShell jednotek v relaci prostředí Windows PowerShell, pomocí **Get-PSDrive** rutiny.

```
PS> Get-PSDrive

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
Alias      Alias
C          FileSystem    C:\                                 ...And Settings\me
cert       Certificate   \
D          FileSystem    D:\
Env        Environment
Function   Function
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
Variable   Variable
```

I když se jednotky v systému lišit podle jednotky v zobrazení, seznam bude vypadat podobně jako výstup **Get-PSDrive** příkaz uvedené výše.

Jednotky systému souborů, jsou podmnožinou jednotky prostředí Windows PowerShell. Můžete určit jednotky systému souborů v systému souborů položce ve sloupci zprostředkovatele. (Jednotky systému souborů v prostředí Windows PowerShell podporované poskytovatelem FileSystem prostředí PowerShell systému Windows.)

Zobrazíte syntaxe **Get-PSDrive** rutiny, zadejte **Get-Command** s **syntaxe** parametr:

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

**PSProvider** parametr umožňuje zobrazit jenom jednotky prostředí Windows PowerShell, který podporuje konkrétního poskytovatele. Například pokud chcete zobrazit jenom jednotky prostředí Windows PowerShell, které jsou podporované poskytovatelem Windows PowerShell FileSystem, zadejte **Get-PSDrive** s **PSProvider** parametr a  **FileSystem** hodnotu:

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

Chcete-li zobrazit jednotky prostředí Windows PowerShell, které představují podregistrů registru, použijte **PSProvider** parametr pro zobrazení pouze jednotky prostředí Windows PowerShell, která jsou podporována zprostředkovatelem registru Windows PowerShell:

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

Také můžete použít standardní rutiny umístění s jednotkami prostředí Windows PowerShell:

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

### <a name="adding-new-windows-powershell-drives-new-psdrive"></a>Přidání nové prostředí Windows PowerShell jednotek (nové PSDrive)

Jednotky prostředí Windows PowerShell můžete přidat pomocí **New-PSDrive** příkaz. Získání syntaxe pro **New-PSDrive** příkazu, zadejte **Get-Command** s **syntaxe** parametr:

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

Chcete-li vytvořit nové jednotku prostředí Windows PowerShell, je nutné zadat tři parametry:

- Název disku (můžete použít libovolný platný název prostředí Windows PowerShell)

- PSProvider (použití systému souborů"" pro umístění systému souborů a "Registru" pro umístění registru)

- Kořenový adresář, to znamená, cesta ke kořenovému adresáři nové složky

Například můžete vytvořit jednotku s názvem "Office", který je namapovaný na složku, která obsahuje aplikace Microsoft Office ve vašem počítači, jako například **C:\\Program Files\\Microsoft Office\\OFFICE11**. Pokud chcete vytvořit jednotku, zadejte následující příkaz:

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> Obecně platí cesty nejsou malá a velká písmena.

Odkazujete na nové jednotku prostředí Windows PowerShell, stejně jako všechny jednotky prostředí Windows PowerShell - jeho název následovaným dvojtečkou (**:**).

Jednotku prostředí Windows PowerShell můžete provádět mnoho úloh mnohem jednodušší. Například některé nejdůležitější klíče v registru systému Windows mají extrémně dlouhé cesty, přitom náročná přístup a obtížně se mějte na paměti. Informace o důležitých konfiguraci se nachází pod **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**. K zobrazení a změna položky v klíči registru CurrentVersion, můžete vytvořit jednotku prostředí Windows PowerShell, který se zobrazuje v tomto klíči zadáním:

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

Můžete změnit umístění **cvkey:** jednotky stejně jako jakoukoli jinou jednotkou: "

`PS> cd cvkey:`

nebo:

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

Rutinu New-PsDrive přidá nový disk pouze pro aktuální relaci prostředí Windows PowerShell. Zavřete okno prostředí Windows PowerShell, dojde ke ztrátě nový disk. Chcete-li uložit jednotku prostředí Windows PowerShell, použijte rutinu Export-konzoly exportovat aktuální relace prostředí Windows PowerShell a pak použijte PowerShell.exe **PSConsoleFile** parametr ho importovat. Nebo přidat nový disk do vašeho profilu Windows Powershellu.

### <a name="deleting-windows-powershell-drives-remove-psdrive"></a>Odstranění prostředí Windows PowerShell jednotek (Remove-PSDrive)

Jednotky z prostředí Windows PowerShell můžete odstranit pomocí **odebrat PSDrive** rutiny. **Odebrat PSDrive** rutiny se snadno používá, chcete-li odstranit určitou jednotku prostředí Windows PowerShell, právě zadat název jednotky prostředí Windows PowerShell.

Například, pokud jste přidali **Office:** jednotku prostředí Windows PowerShell, jak je znázorněno **New-PSDrive** tématu, chcete-li odstranit zadáním:

```powershell
Remove-PSDrive -Name Office
```

Odstranit **cvkey:** prostředí Windows PowerShell jednotka také zobrazit v **New-PSDrive** tématu, použijte následující příkaz:

```powershell
Remove-PSDrive -Name cvkey
```

Je snadno odstranit jednotku prostředí Windows PowerShell, ale nelze odstranit, když jste na jednotce. Příklad:

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### <a name="adding-and-removing-drives-outside-windows-powershell"></a>Přidávání a odebírání jednotek mimo prostředí Windows PowerShell

Zjistí jednotky systému souborů, které jsou přidány nebo odebrány v systému Windows, včetně síťové jednotky, které jsou mapované jednotky USB, které jsou připojené a jednotky, které se odstraní pomocí prostředí Windows PowerShell **net použití** příkaz nebo  **WScript.NetworkMapNetworkDrive** a **RemoveNetworkDrive** metody ze skriptu Windows Script Host (WSH).
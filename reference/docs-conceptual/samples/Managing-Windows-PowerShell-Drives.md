---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa jednotek Windows PowerShellu
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: cfc5418e9d2efb1a786817e1b941d75e22291742
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404045"
---
# <a name="managing-windows-powershell-drives"></a>Správa jednotek Windows PowerShellu

A *jednotku prostředí Windows PowerShell* je umístění úložiště dat, který se zobrazí jako jednotku systému souborů ve Windows Powershellu. Poskytovatelé Windows Powershellu některé jednotky pro vytvoření, jako například jednotky systému souborů (včetně C: a D:), registru jednotky (HKCU: a HKLM:) a jednotky certifikát (Cert:), a můžete vytvořit vlastní jednotek Windows Powershellu. Tyto disky jsou velmi užitečné, ale jsou k dispozici pouze v rámci prostředí Windows PowerShell. Nelze k nim přistupovat pomocí jiných nástrojů Windows, jako je například Průzkumník souborů nebo Cmd.exe.

Prostředí Windows PowerShell používá podstatné jméno, **PSDrive**, příkazy, které pracují s prostředím Windows PowerShell jednotky. Pro seznam prostředí Windows PowerShell jednotek v relaci prostředí Windows PowerShell, použijte **Get-PSDrive** rutiny.

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

I když s jednotkami ve vašem systému se liší jednotek v zobrazení seznamu bude vypadat podobně jako na výstupu **Get-PSDrive** výše uvedenému příkazu.

Jednotky systému souborů, jsou podmnožinou jednotek Windows Powershellu. Můžete určit soubor systémové jednotky v položce systému souborů ve sloupci zprostředkovatele. (Jednotky systému souborů v prostředí Windows PowerShell je podporováno ve zprostředkovateli Windows Powershellu systému souborů.)

Chcete-li zobrazit syntaxi **Get-PSDrive** rutiny, zadejte **Get-Command** příkazů **syntaxe** parametr:

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

**PSProvider** parametr umožňuje zobrazit pouze pro prostředí Windows PowerShell, které disky jsou podporovány konkrétního poskytovatele. Například pokud chcete zobrazit pouze jednotek Windows Powershellu, které jsou podporovány ve zprostředkovateli Windows Powershellu systému souborů, zadejte **Get-PSDrive** příkazů **PSProvider** parametr a  **Systém souborů** hodnotu:

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

Chcete-li zobrazit jednotek Windows Powershellu, které představují podregistrům registru, použijte **PSProvider** parametr k zobrazení jen pro prostředí Windows PowerShell disky, které podporuje zprostředkovatel registru Windows Powershellu:

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

Standardní rutiny umístění můžete použít také s jednotek Windows Powershellu:

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

### <a name="adding-new-windows-powershell-drives-new-psdrive"></a>Přidání nové prostředí Windows PowerShell (nový PSDrive) jednotky

Můžete přidat jednotky prostředí Windows PowerShell pomocí **New-PSDrive** příkazu. Získání syntaxe pro **New-PSDrive** příkazu, zadejte **Get-Command** příkazů **syntaxe** parametr:

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

Chcete-li vytvořit novou jednotku prostředí Windows PowerShell, je nutné zadat tři parametry:

- Název disku (můžete použít libovolný platný název prostředí Windows PowerShell)

- PSProvider (použití systému souborů"" pro umístění systému souborů a umístění registru "registru")

- Kořenový adresář, to znamená, že cesta do kořenového adresáře nové jednotky

Můžete například vytvořit jednotku s názvem "Office", který je namapovaný na složku, která obsahuje aplikace Microsoft Office v počítači, jako například **C:\\Program Files\\Microsoft Office\\OFFICE11**. Chcete-li vytvořit jednotku, zadejte následující příkaz:

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> Obecně platí cesty nejsou malá a velká písmena.

Můžete odkazovat na novou jednotku prostředí Windows PowerShell, stejně jako u všech jednotek Windows Powershellu – podle názvu, za nímž následuje dvojtečka (**:**).

Jednotku prostředí Windows PowerShell můžete provádět mnoho úloh mnohem jednodušší. Některé z vašich nejdůležitějších klíče v registru Windows mít například extrémně dlouhé cesty, díky kterým jsou náročné na přístup a obtížně mějte na paměti. Informace o důležitých konfiguraci se nachází v části **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**. K zobrazení a změně položek v klíči registru CurrentVersion, můžete vytvořit jednotku prostředí Windows PowerShell, který je integrován v tento klíč tak, že zadáte:

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

Můžete změnit umístění **cvkey:** jednotka stejně jako jakoukoli jinou jednotkou:''

`PS> cd cvkey:`

nebo:

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

Rutina New-PsDrive přidá novou jednotku pouze do aktuální relace prostředí Windows PowerShell. Pokud zavřete okno prostředí Windows PowerShell, dojde ke ztrátě novou jednotku. Pokud chcete uložit jednotku prostředí Windows PowerShell, použijte rutinu Export-konzoly exportovat aktuální relace prostředí Windows PowerShell a pak použijte PowerShell.exe **PSConsoleFile** importujte ho. Nebo přidejte nové jednotky k vašemu profilu Windows Powershellu.

### <a name="deleting-windows-powershell-drives-remove-psdrive"></a>Odstraňuje se prostředí Windows PowerShell jednotek (Remove-PSDrive)

Jednotky z prostředí Windows PowerShell můžete odstranit pomocí **odebrat PSDrive** rutiny. **Odebrat PSDrive** rutina je snadno použitelný; Chcete-li odstranit určitou jednotku prostředí Windows PowerShell, stačí zadat název jednotku prostředí Windows PowerShell.

Například, pokud jste přidali **Office:** Jednotku prostředí Windows PowerShell, jak je znázorněno **New-PSDrive** tématu, můžete ho odstranit tak, že zadáte:

```powershell
Remove-PSDrive -Name Office
```

Chcete-li odstranit **cvkey:** Prostředí Windows PowerShell jednotka, také ukazuje **New-PSDrive** tématu, použijte následující příkaz:

```powershell
Remove-PSDrive -Name cvkey
```

Je snadné odstranit jednotku prostředí Windows PowerShell, ale nemůžete odstranit, když jste na jednotce. Příklad:

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### <a name="adding-and-removing-drives-outside-windows-powershell"></a>Přidávání a odebírání jednotek mimo prostředí Windows PowerShell

Zjistí jednotky se systémem souborů, které jsou přidány nebo odebrány ve Windows, včetně síťové jednotky, které jsou mapovány, jednotky USB, které jsou připojeny a jednotek, které jsou odstraněny pomocí prostředí Windows PowerShell **použití** příkaz nebo  **WScript.NetworkMapNetworkDrive** a **RemoveNetworkDrive** metody ze skriptu Windows Script Host (WSH).
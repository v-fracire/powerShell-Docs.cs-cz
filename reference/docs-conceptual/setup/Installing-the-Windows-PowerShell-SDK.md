---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Instalace sady SDK Windows PowerShellu
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: fa876bac0c1afac24f93d11dd2e7ecfb1165cf5f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893534"
---
# <a name="installing-the-windows-powershell-sdk"></a>Instalace sady SDK Windows PowerShellu

Následující téma popisuje, jak nainstalovat sadu SDK prostředí PowerShell v různých verzích Windows.

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a>Instalace prostředí Windows PowerShell 3.0 SDK pro Windows 8 a Windows Server 2012

Windows PowerShell 3.0 je automaticky nainstalován se systémem Windows 8 a Windows Server 2012.
Kromě toho můžete stáhnout a nainstalovat referenční sestavení pro Windows PowerShell 3.0 jako součást sady SDK pro Windows 8.
Tato sestavení umožňuje psát rutiny, poskytovatelů a hostitele aplikací pro Windows PowerShell 3.0.
Když instalujete Windows SDK pro Windows 8, sestavení prostředí Windows PowerShell jsou automaticky nainstalovány ve složce odkaz na sestavení v `\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0`.
Další informace najdete v tématu [serveru pro Windows 8 SDK stahování](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive).
Ukázky kódu v prostředí Windows PowerShell jsou k dispozici také na Centrum pro vývoj.
Další informace najdete v tématu ukázkové desktopové znakovou stránku na [webu Dev center](https://code.msdn.microsoft.com:443/windowsdesktop/).

Kromě toho Windows PowerShell 3.0 je zpětně kompatibilní se sadou SDK Windows Powershellu 2.0, která zahrnuje celou řadu ukázek kódu.
Další informace o tom, jak stáhnout sadu SDK Windows Powershellu 2.0 najdete níže.
(Všimněte si, že ukázky kódu 2.0 jsou kompatibilní se systémem Windows 8 a Windows PowerShell 3.0, nelze nainstalovat Windows PowerShell 2.0 na platformě Windows 8.)

## <a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a>Instalace prostředí Windows PowerShell 3.0 SDK pro Windows 7 a Windows Server 2008 R2

Windows 7 a Windows Server 2008 R2 mít automaticky nainstalovanou prostředí PowerShell 2.0.
Kromě toho můžete nainstalovat prostředí PowerShell 3.0 v těchto systémech.
(Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).).
Jak je popsáno výše, můžete také nainstalovat sady SDK Windows 8 na Windows 7 a Windows Server 2008 R2.

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a>Instalace prostředí Windows PowerShell 2.0 SDK pro Windows 7, Vista, XP, Server 2003 a Server 2008

Sady SDK Windows Powershellu 2.0 poskytuje referenční sestavení potřebná k zápisu rutiny, poskytovatelů a hostování aplikací, a poskytuje C# ukázkového kódu, který může sloužit jako výchozí bod, když začnete psát kód.

Instalaci této sady SDK najdete v tématu [sady SDK Windows Powershellu 2.0](http://www.microsoft.com/en-us/download/details.aspx?id=2560).

## <a name="reference-assemblies"></a>Referenční sestavení

Referenční sestavení jsou ve výchozím nastavení nainstalován v následujícím umístění: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.

> [!NOTE] 
> Kód, který je zkompilován proti sestavení Windows PowerShell 2.0 nelze načíst do zařízení Windows PowerShell 1.0.
> Nicméně kód, který je zkompilován proti sestavení Windows PowerShell 1.0 je možné načíst do instalace Windows PowerShell 2.0.

## <a name="samples"></a>Ukázky

Ukázky kódu jsou nainstalovány v následujícím umístění ve výchozím nastavení: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.

Následující části obsahují stručný popis toho, co dělá každý vzorek.

## <a name="cmdlet-samples"></a>Rutiny ukázky

### <a name="getprocesssample01"></a>GetProcessSample01

Ukazuje, jak napsat jednoduchý rutinu, která získá všechny procesy na místním počítači.

### <a name="getprocesssample02"></a>GetProcessSample02

Ukazuje, jak přidat parametry do rutiny.
Rutina převezme jeden nebo více názvů proces a vrátí odpovídajících procesů.

### <a name="getprocesssample03"></a>GetProcessSample03

Ukazuje, jak přidat parametry, které přijímají vstup z kanálu.

### <a name="getprocesssample04"></a>GetProcessSample04

Ukazuje, jak zpracovávat neukončující chyby.

### <a name="getprocesssample05"></a>GetProcessSample05

Ukazuje, jak zobrazit seznam konkrétních procesů.

### <a name="selectobject"></a>SelectObject –

Ukazuje, jak napsat filtru vybrat pouze určité objekty.

### <a name="selectstring"></a>SelectString

Ukazuje, jak pro hledání souborů pro zadanou vzory.

### <a name="stopprocesssample01"></a>StopProcessSample01

Ukazuje, jak implementovat *PassThru* parametr a jak si vyžádat zpětnou vazbu uživatelů pomocí volání [ShouldProcess](/dotnet/api/system.management.automation.cmdlet.shouldprocess) a [ShouldContinue](/dotnet/api/system.management.automation.cmdlet.shouldcontinue) metody.
Uživatelé *PassThru* parametr, když chtějí vynutit rutinu k vrácení objektu,

### <a name="stopprocesssample02"></a>StopProcessSample02

Ukazuje, jak zastavit konkrétní proces.

### <a name="stopprocesssample03"></a>StopProcessSample03

Ukazuje, jak deklarovat aliasy pro parametry a jak podporovat zástupné znaky.

### <a name="stopprocesssample04"></a>StopProcessSample04

Ukazuje, jak deklarovat sad parametrů, objekt, který rutina přijímá jako vstup a jak určit výchozí parametr nastaveno pro použití.

## <a name="remoting-samples"></a>Ukázky vzdálené komunikace

### <a name="remoterunspace01"></a>RemoteRunspace01

Ukazuje, jak vytvořit vzdálené prostředí runspace, který se používá k navázání vzdáleného připojení.

### <a name="remoterunspacepool01"></a>RemoteRunspacePool01

Ukazuje, jak vytvořit fond vzdálené prostředí runspace a o tom, jak souběžně spustit více příkazů pomocí tohoto fondu.

### <a name="serialization01"></a>Serialization01

Ukazuje, jak podívejte se na existující třídy .NET a ujistěte se, že se uchovají informace z vybraných veřejných vlastností této třídy v serializaci nebo deserializaci.

### <a name="serialization02"></a>Serialization02

Ukazuje, jak existující třídy .NET a ujistěte se, že se uchovají informace z instance této třídy v serializaci/deserializaci když informace nejsou k dispozici ve veřejné vlastnosti třídy.

### <a name="serialization03"></a>Serialization03

Ukazuje, jak podívejte se na existující třídy .NET a ujistěte se, že jsou instance této třídy a odvozených tříd deserializovat (rehydrated) do živých objektů .NET.

## <a name="event-samples"></a>Ukázky událostí

### <a name="event01"></a>Event01

Ukazuje, jak vytvořit odvozené z ObjectEventRegistrationBase rutinu pro registraci na událost.

### <a name="event02"></a>Event02

Ukazuje, jak do ukazuje, jak k přijímání oznámení o události prostředí Windows PowerShell, které jsou generovány ve vzdálených počítačích.
Využívá událost PSEventReceived prostřednictvím [prostředí Runspace](/dotnet/api/system.management.automation.runspaces.runspace) třídy.

## <a name="hosting-application-samples"></a>Hostování aplikace ukázky

### <a name="runspace01"></a>Runspace01

Ukazuje způsob použití [PowerShell](/dotnet/api/system.management.automation.powershell) má třída spustit [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutiny synchronně.
[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutina vrací [procesu](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý proces běžící na místním počítači.

### <a name="runspace02"></a>Runspace02

Ukazuje způsob použití [PowerShell](/dotnet/api/system.management.automation.powershell) má třída spustit [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) a [Sort-Object](/powershell/module/Microsoft.PowerShell.Utility/Sort-Object) rutiny synchronně.
[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutina vrací [procesu](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý proces běžící na místním počítači a `Sort-Object` řadí objekty, na základě jejich [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) Vlastnost.
Zobrazí se výsledky z těchto příkazů pomocí [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) ovládacího prvku.

### <a name="runspace03"></a>Runspace03

Ukazuje způsob použití [Powershellu](/dotnet/api/system.management.automation.powershell) má třída spustit skript synchronně a jak zacházet s neukončujícími chybami.
Skript získá seznam názvů procesu a potom načte těchto procesů.
Výsledky ze skriptu, včetně neukončující chyby, které byly generovány při spuštění skriptu, se zobrazí v okně konzoly.

### <a name="runspace04"></a>Runspace04

Ukazuje způsob použití [Powershellu](/dotnet/api/system.management.automation.powershell) má třída spustit příkazy a jak catch ukončující chyby, které jsou vyvolány při spuštění příkazů.
Dva příkazy jsou spouštěny a poslední příkaz je předán jako parametr argument, který není platný.
V důsledku toho jsou vráceny žádné objekty a dojde k ukončující chybě je vyvolána výjimka.

### <a name="runspace05"></a>Runspace05

Ukazuje, jak přidat modulu snap-in [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektu tak, aby rutiny modulu snap-in k dispozici při otevření prostředí runspace.
Modul snap-in poskytuje rutiny Get-Proc (určené [GetProcessSample01 ukázkové](https://technet.microsoft.com/library/ff602028.aspx)), který běží synchronně pomocí [Powershellu](/dotnet/api/system.management.automation.powershell) objektu.

### <a name="runspace06"></a>Runspace06

Ukazuje, jak přidat modul do [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektu tak, aby modul je načten při otevření prostředí runspace.
Tento modul obsahuje rutiny Get-Proc (určené [GetProcessSample02 ukázkové](https://technet.microsoft.com/library/ff602027.aspx)), který běží synchronně pomocí [prostředí PowerShell](/dotnet/api/system.management.automation.powershell) objektu.

### <a name="runspace07"></a>Runspace07

Ukazuje, jak vytvořit prostředí runspace a pak pomocí tohoto prostředí runspace spustíte dvě rutiny synchronně s použitím [Powershellu](/dotnet/api/system.management.automation.powershell) objektu.

### <a name="runspace08"></a>Runspace08

Ukazuje, jak přidat do kanálu z příkazů a argumentů [Powershellu](/dotnet/api/system.management.automation.powershell) objekt a jak spouštět příkazy synchronně.

### <a name="runspace09"></a>Runspace09

Ukazuje, jak přidat skript do kanálu nástroje [Powershellu](/dotnet/api/system.management.automation.powershell) objekt a jak spustit skript asynchronně.
Události se používají ke zpracování výstup skriptu.

### <a name="runspace10"></a>Runspace10

Ukazuje, jak vytvořit počáteční relace do výchozího stavu přidání rutiny [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate), jak vytvořit prostředí runspace, který používá stav relace počáteční a jak spustit pomocí příkazu [Powershellu](/dotnet/api/system.management.automation.powershell)objektu.

### <a name="runspace11"></a>Runspace11

Ukazuje způsob použití [ProxyCommand](/dotnet/api/system.management.automation.proxycommand) třídy za účelem vytvoření příkaz proxy server, který volá existující rutiny, ale omezuje sadu parametrů k dispozici.
Příkaz proxy se pak přidá do stavu počáteční relace, který se používá k vytvoření omezené prostředí runspace.
To znamená, že má uživatel přístup funkci rutiny pouze prostřednictvím příkazu proxy serveru.

### <a name="powershell01"></a>PowerShell01

Ukazuje, jak vytvořit prostředí runspace omezené použití [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektu.

### <a name="powershell02"></a>PowerShell02

Ukazuje, jak používat prostředí runspace fond jak souběžně spustit více příkazů.

## <a name="host-samples"></a>Ukázky hostitele

### <a name="host01"></a>Host01

Ukazuje, jak implementovat hostitelskou aplikaci, která používá vlastního hostitele.
V této ukázce se vytvoří prostředí runspace, který používá vlastního hostitele a pak [Powershellu](/dotnet/api/system.management.automation.powershell) rozhraní API se používá ke spuštění skriptu, který volá "ukončit".
Hostitelská aplikace potom vypadá výstup skriptu a vypíše výsledky.

### <a name="host02"></a>Host02

Ukazuje, jak psát aplikace hostitele, který používá modul runtime Windows PowerShell společně s implementace vlastního hostitele.
Hostitelská aplikace nastaví jazykovou verzi hostitele na němčinu, spustí [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutiny a zobrazí výsledky jako zobrazoval se vám je pomocí pwrsh.exe a pak vytiskne aktuální datum a čas v němčině.

### <a name="host03"></a>Host03

Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.

### <a name="host04"></a>Host04

Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.
Tato hostitelská aplikace podporuje také zobrazování výzev, které umožňují uživateli zadat více možností.

### <a name="host05"></a>Hostitel05

Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.
Tato hostitelská aplikace podporuje také volání vzdálených počítačích pomocí [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) a [ukončení relace PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) rutiny.

### <a name="host06"></a>Host06

Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.
Kromě toho tato ukázka používá rozhraní API pro Tokenizátor pro určení barvy textu, který je zadané uživatelem.

## <a name="provider-samples"></a>Ukázky poskytovatele

### <a name="accessdbprovidersample01"></a>AccessDBProviderSample01

Ukazuje, jak deklarovat třídu poskytovatele, který je odvozen přímo z [CmdletProvider](/dotnet/api/system.management.automation.provider.cmdletprovider) třídy.
Je zde zahrnuta pouze pro úplnost.

### <a name="accessdbprovidersample02"></a>AccessDBProviderSample02

Ukazuje, jak přepsat [NewDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.newdrive) a [RemoveDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.removedrive) metody pro podporu volání `New-PSDrive` a `Remove-PSDrive` rutiny.
Třída zprostředkovatele v této ukázce je odvozena z [DriveCmdletProvider](/dotnet/api/system.management.automation.provider.drivecmdletprovider) třídy.

### <a name="accessdbprovidersample03"></a>AccessDBProviderSample03

Ukazuje, jak přepsat [GetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.getitem) a [SetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.setitem) metody pro podporu volání `Get-Item` a `Set-Item` rutiny.
Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) třídy.

### <a name="accessdbprovidersample04"></a>AccessDBProviderSample04

Ukazuje, jak přepsat metody kontejneru pro podporu volání `Copy-Item`, `Get-ChildItem`, `New-Item`, a `Remove-Item` rutiny.
Tyto metody by měla být implementována, pokud úložiště dat obsahuje položky, které jsou kontejnery.
Kontejner je skupina podřízených položek v části společné nadřazené položky.
Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) třídy.

### <a name="accessdbprovidersample05"></a>AccessDBProviderSample05

Ukazuje, jak přepsat metody kontejneru pro podporu volání `Move-Item` a `Join-Path` rutiny.
Tyto metody by měla být implementována, když uživatel potřebuje pro přesun položek v rámci kontejneru, a pokud úložiště dat obsahuje vnořené kontejnery.
Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) třídy.

### <a name="accessdbprovidersample06"></a>AccessDBProviderSample06

Ukazuje, jak přepsat obsah metody pro podporu volání `Clear-Content`, `Get-Content`, a `Set-Content` rutiny.
Tyto metody by měla být implementována, když uživatel potřebuje pro správu obsahu položky dat v úložišti.
Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) a implementuje [IContentCmdletProvider](/dotnet/api/system.management.automation.provider.icontentcmdletprovider) rozhraní.
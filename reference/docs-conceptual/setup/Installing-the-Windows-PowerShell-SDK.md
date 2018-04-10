---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Instalace sady SDK Windows PowerShellu
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: 830b054c2cf2b49d935d3d96b79effa7131f6db2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="installing-the-windows-powershell-sdk"></a>Instalace sady SDK Windows PowerShellu

Následující téma popisuje postup instalace sady SDK prostředí PowerShell v různých verzích systému Windows.

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a>Instalace prostředí Windows PowerShell 3.0 SDK pro Windows 8 a Windows Server 2012

Prostředí Windows PowerShell 3.0 je automaticky nainstalován ve Windows 8 a Windows Server 2012.
Kromě toho můžete stáhnout a nainstalovat referenční sestavení pro prostředí Windows PowerShell 3.0 jako součást sady Windows 8 SDK.
Tyto sestavení umožňují zápisu rutiny, zprostředkovatele a hostitelských aplikací pro Windows PowerShell 3.0.
Když instalujete Windows SDK pro Windows 8, sestavení prostředí Windows PowerShell jsou automaticky nainstalovány do složky referenční sestavení, ve \Program soubory (x86) \Reference Assemblies\Microsoft\WindowsPowerShell\3.0.
Další informace najdete v tématu [stažení serveru Windows 8 SDK](http://msdn.microsoft.com/windows/hardware/hh852363.aspx).
Prostředí Windows PowerShell, ukázky kódu jsou k dispozici v centru vývoj.
Další informace naleznete na stránce ukázka plochy kódu na [webu Dev center](http://code.msdn.microsoft.com/windowsdesktop/).

Kromě toho prostředí Windows PowerShell 3.0 je zpětně kompatibilní s Windows PowerShell 2.0 SDK, který zahrnuje několik ukázky kódu.
Další informace o tom, jak stáhnout sadu SDK Windows PowerShell 2.0 najdete níže.
(Všimněte si, že ukázky 2.0 kódu jsou kompatibilní s Windows 8 a Windows PowerShell 3.0, nelze nainstalovat prostředí Windows PowerShell 2.0 na platformě Windows 8.)

##<a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a>Instalace prostředí Windows PowerShell 3.0 SDK pro systém Windows 7 a Windows Server 2008 R2

Windows 7 a Windows Server 2008 R2 nainstalována automaticky prostředí PowerShell 2.0.
Kromě toho můžete nainstalovat prostředí PowerShell 3.0 v těchto systémech.
(Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).).
Jak je popsáno výše, můžete taky nainstalovat sadu SDK Windows 8 na Windows 7 a Windows Server 2008 R2.

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a>Instalace prostředí Windows PowerShell 2.0 SDK pro systém Windows 7, Vista, XP, Server 2003 a Server 2008

Windows PowerShell 2.0 SDK poskytuje referenční sestavení potřebná k zápisu rutiny, zprostředkovatele a hostování aplikace a poskytuje C# ukázkový kód, který lze použít jako výchozí bod, abyste před zahájením psaní kódu.

Chcete-li instalovat tuto sadu SDK, přečtěte si téma [Windows PowerShell 2.0 SDK](http://go.microsoft.com/fwlink/?LinkId=184611).

## <a name="reference-assemblies"></a>Odkaz na sestavení

Referenční sestavení jsou ve výchozím nastavení nainstalován v následujícím umístění: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.

> **Poznámka:**: kód, který se zkompiluje proti sestavení prostředí Windows PowerShell 2.0 nelze načíst do instalace prostředí Windows PowerShell 1.0.
>Kód, který se zkompiluje proti sestavení prostředí Windows PowerShell 1.0 však může být načtena do instalace prostředí Windows PowerShell 2.0.

## <a name="samples"></a>Ukázky

Ukázky kódu jsou standardně nainstalované v následujícím umístění: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.

Následující části obsahují stručný popis, jaké jsou jednotlivé vzorky.

## <a name="cmdlet-samples"></a>Ukázky rutiny
**GetProcessSample01**

Ukazuje, jak napsat jednoduchý rutinu, která načte všechny procesy v místním počítači.

**GetProcessSample02**

Ukazuje, jak přidat parametry do rutiny.
Rutina trvá jeden nebo více názvů proces a vrátí odpovídající procesy.

**GetProcessSample03**

Ukazuje, jak přidat parametry, které přijímají vstup z kanálu.

**GetProcessSample04**

Ukazuje, jak se budou zpracovávat chyby nonterminating.

**GetProcessSample05**

Ukazuje, jak zobrazit seznam procesů, zadaný.

**SelectObject**

Ukazuje, jak napsat filtru vybrat pouze určité objekty.

**SelectString**

Ukazuje, jak pro hledání souborů pro zadaný vzory.

**StopProcessSample01**

Ukazuje, jak implementovat *PassThru* parametr a jak požádat o zpětnou vazbu od uživatelů voláním [ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx) a [ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx) metody.
Zadejte uživatele *PassThru* parametr, když chtějí vynutit se rutina mohla vrátit objekt,

**StopProcessSample02**

Ukazuje, jak zastavit konkrétní proces.

**StopProcessSample03**

Ukazuje, jak deklarovat aliasy pro parametry a jak podporovat zástupné znaky.

**StopProcessSample04**

Ukazuje, jak deklarovat sad parametrů, objekt, který rutina používá jako vstup a postup, zadejte parametr výchozí nastavení používá.

## <a name="remoting-samples"></a>Ukázky vzdálené komunikace

**RemoteRunspace01**

Ukazuje, jak vytvořit vzdálené prostředí runspace, který se používá k navázání připojení ke vzdálené.

**RemoteRunspacePool01**

Ukazuje, jak vytvořit fond vzdálené prostředí runspace a jak souběžně spustit více příkazů pomocí tohoto fondu.

**Serialization01**

Ukazuje, jak existující třídy rozhraní .NET a ujistěte se, že se zachovají informace z vybraných veřejných vlastností této třídy v serializaci nebo deserializaci.

**Serialization02**

Ukazuje, jak existující třídy rozhraní .NET a ujistěte se, že se zachovají informace z instance této třídy v serializaci nebo deserializaci když informace nejsou k dispozici v veřejné vlastnosti třídy.

**Serialization03**

Ukazuje, jak existující třídy rozhraní .NET a ujistěte se, že jsou instance této třídy a odvozených tříd deserializovat (rehydrated) do provozu objekty .NET.

## <a name="event-samples"></a>Ukázky událostí

**Event01**

Ukazuje, jak vytvořit rutinu pro registraci události odvozené z ObjectEventRegistrationBase.

**Event02**

Ukazuje, jak k ukazuje, jak k přijímání oznámení o události prostředí Windows PowerShell, které se generují ve vzdálených počítačích.
Používá událost PSEventReceived vystavenou přes [prostředí Runspace](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx) třídy.

## <a name="hosting-application-samples"></a>Hostování aplikace ukázky

**Runspace01**

Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třídy ke spuštění [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutiny synchronně.
[Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutina vrátí [proces](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý proces, který běží v místním počítači.

**Runspace02**

Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třídy ke spuštění [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) a [řazení objektu](http://go.microsoft.com/fwlink/?LinkID=113403) rutiny synchronně.
[Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutina vrátí [proces](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý zpracování spuštěna v místním počítači a objekt řazení seřadí objekty na základě jejich [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) vlastnost.
Výsledky z těchto příkazů se zobrazí pomocí [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) ovládacího prvku.

**Runspace03**

Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třída synchronně spustit skript a jak se budou zpracovávat chyby neukončující.
Skript přijímá seznam názvů proces a potom načte těchto procesů.
Výsledky skriptu, včetně všech jiných ukončován chyb, které byly generovány při spuštění skriptu, jsou zobrazeny v okně konzoly.

**Runspace04**

Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třídy ke spuštění příkazů a jak catch ukončující chyby, které se vyvolá, když spustíte příkaz.
Dva příkazy se spouštějí a poslední příkaz se předá parametr argument, který není platný.
V důsledku toho jsou vráceny žádné objekty a je vyvolána ukončující chyba.

**Runspace05**

Ukazuje, jak přidat modul snap-in k [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektu, aby rutiny modulu snap-in k dispozici, když je otevřen prostředí runspace.
Modul snap-in poskytuje rutiny Get-Proc (definované [GetProcessSample01 ukázka](https://technet.microsoft.com/library/ff602028.aspx)) je synchronně spustit pomocí [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektu.

**Runspace06**

Popisuje postup pro přidání modulu do [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektu tak, aby modul je načtena, když je otevřen prostředí runspace.
Modul poskytuje rutiny Get-Proc (definované [GetProcessSample02 ukázka](https://technet.microsoft.com/library/ff602027.aspx)) je synchronně spustit pomocí [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektu.

**Runspace07**

Ukazuje, jak vytvořit prostředí runspace a pak použít rutin dvě synchronně pomocí tohoto prostředí runspace [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektu.

**Runspace08**

Ukazuje, jak přidat příkazy a argumenty do kanálu nástroje [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objekt a jak spouštět příkazy synchronně.

**Runspace09**

Ukazuje, jak přidat skript do kanálu nástroje [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objekt a postupy pro spuštění skriptu asynchronně.
Události se používají pro zpracování výstup skriptu.

**Runspace10**

Ukazuje, jak vytvořit počáteční relace do výchozího stavu postup přidání rutiny [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), jak vytvořit prostředí runspace, který používá stav relace počáteční a jak spustit pomocí příkazu [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)objektu.

**Runspace11**

Ukazuje, jak používat [ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx) třídy za účelem vytvoření příkaz proxy serveru, který volá existující rutiny, ale omezuje sadu parametrů, k dispozici.
Příkaz proxy serveru se pak přidá do stavu počáteční relace, který se používá k vytvoření omezené prostředí runspace.
To znamená, že uživatel může přistupovat k funkcím rutiny pouze pomocí příkazu proxy.

**PowerShell01**

Ukazuje, jak vytvořit omezené prostředí runspace pomocí [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektu.

**PowerShell02**

Ukazuje, jak používat prostředí runspace fondu současně spustit více příkazů.

## <a name="host-samples"></a>Ukázky hostitele

**Host01**

Ukazuje, jak implementovat hostitelskou aplikaci, která používá vlastní hostitel.
V této ukázce je vytvořena prostředí runspace, která používá vlastní hostitel a potom [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) rozhraní API slouží k spustit skript, který volá "Ukončete".
Hostitelskou aplikaci pak porovná výstup skriptu a zobrazí výsledky.

**Host02**

Ukazuje, jak psát aplikace hostitele používající modul runtime prostředí Windows PowerShell společně s implementace vlastního hostitele.
Hostitelskou aplikaci nastaví hostitele jazykovou verzi, němčina, spustí [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutiny a zobrazí výsledky podle by zobrazovat pomocí pwrsh.exe a potom vytiskne aktuální datum a čas v němčině.

**Host03**

Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.

**Host04**

Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.
Tato aplikace hostitele také podporuje zobrazování výzev, které umožní uživateli zadat více možností.

**Host05**

Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.
Tato aplikace hostitele taky podporuje volání vzdálených počítačů pomocí [Enter-PsSession](http://go.microsoft.com/fwlink/?LinkId=135210) a [ukončení-PsSession](http://go.microsoft.com/fwlink/?LinkId=135212) rutiny.

**Host06**

Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.
Kromě toho tato ukázka pomocí rozhraní API Tokenizátor Určuje barvu textu, který je zadaný uživatel.

## <a name="provider-samples"></a>Ukázky zprostředkovatele

**AccessDBProviderSample01**

Ukazuje, jak deklarovat zprostředkovatele třídu, která pochází přímo z [CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx) třídy.
Je zde uveden pouze pro úplnost.

**AccessDBProviderSample02**

Ukazuje, jak přepsat [NewDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx) a [RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx) metody pro podporu volání rutiny New-PSDrive a PSDrive odebrat.
Třída zprostředkovatele v této ukázce je odvozena z [DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx) třídy.

**AccessDBProviderSample03**

Ukazuje, jak přepsat [GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx) a [SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx) metody pro podporu volání rutiny Get-Item a sadu položek.
Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) třídy.

**AccessDBProviderSample04**

Ukazuje, jak k přepsání metody kontejner pro podporu volání Copy-Item, Get-ChildItem, nové položky a rutiny Remove-položky.
Tyto metody by měla být implementována, pokud úložiště dat obsahuje položky, které jsou kontejnery.
Kontejner je skupina podřízené položky v rámci běžných nadřazené položky.
Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) třídy.

**AccessDBProviderSample05**

Ukazuje, jak k přepsání metody kontejner pro podporu volání rutiny přesunout položku a připojení k cestě.
Tyto metody by měla být implementována, pokud uživatel musí přesunout položky do kontejneru, a v případě úložiště dat obsahuje vnořené kontejnery.
Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) třídy.

**AccessDBProviderSample06**

Ukazuje, jak k přepsání obsahu metody pro podporu volání Clear-obsahu, Get-obsahu a obsahu sady rutin.
Tyto metody by měla být implementována, když uživatel potřebuje ke správě obsahu položek v úložišti.
Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) třídy ale implementuje [IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx) rozhraní.
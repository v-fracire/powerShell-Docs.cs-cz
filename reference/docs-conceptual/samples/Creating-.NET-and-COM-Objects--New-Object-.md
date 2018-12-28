---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytváření objektů .NET a COM nový objekt
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 1ffd8d4afa419ec0c24321e44aa4a2f41a9bee44
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404109"
---
# <a name="creating-net-and-com-objects-new-object"></a>Vytváření objektů .NET a COM (New-Object)

Existují softwarové komponenty pomocí rozhraní .NET Framework a modelu COM, které vám umožní provádět mnoho úkolů správy systému. Prostředí Windows PowerShell vám umožní používat tyto komponenty, takže nejste omezeni na úlohy, které lze provádět pomocí rutin. Mnoho rutin v počáteční verzi Windows Powershellu nebudou fungovat na vzdálených počítačích. Můžeme vám ukáže, jak získat vyhnout uvedeným potížím při správě protokolů událostí s použitím rozhraní .NET Framework **System.Diagnostics.EventLog** třídy přímo z prostředí Windows PowerShell.

### <a name="using-new-object-for-event-log-access"></a>Pomocí nového objektu pro přístup k protokolu událostí

Knihovny tříd rozhraní .NET Framework obsahuje třídu s názvem **System.Diagnostics.EventLog** , který lze použít ke správě protokolů událostí. Můžete vytvořit novou instanci třídy rozhraní .NET Framework pomocí **New-Object** rutinu s **TypeName** parametru. Například následující příkaz vytvoří odkaz na protokol událostí:

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

I když příkaz vytvořil instanci třídy protokolu událostí, instance neobsahuje žádná data. Důvodem je, jsme nezadali určitý protokol událostí. Jak můžete získat skutečný protokolu událostí?

#### <a name="using-constructors-with-new-object"></a>Použití konstruktorů s New-Object

K odkazování na určitém protokolu událostí, musíte zadat název protokolu. **Nový objekt** má **Seznam_argumentů** parametru. Argumenty, které můžete předat jako hodnoty pro tento parametr používá speciální po spuštění metody objektu. Metoda je volána *konstruktor* vzhledem k tomu, že se používá ke konstrukci objektu. Třeba získat odkaz na aplikaci protokolu, zadejte řetězec "Aplikace" jako argument:

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> Protože většina základních tříd rozhraní .NET Framework jsou obsaženy v oboru názvů System, prostředí Windows PowerShell se automaticky pokusí vyhledat třídy, které zadáte v oboru názvů System, pokud nemůže najít shoda pro název typu, který zadáte. To znamená, že je možné zadat Diagnostics.EventLog místo System.Diagnostics.EventLog.

#### <a name="storing-objects-in-variables"></a>Ukládání objektů v proměnných

Může být vhodné k uložení odkazu na objekt, takže ho můžete použít v aktuálním prostředí. I když se prostředí Windows PowerShell umožňuje provádět spoustu práce s kanály, lessening potřebu proměnné, někdy ukládání odkazů na objekty v proměnné umožňuje efektivněji pracovat s těmito objekty.

Prostředí Windows PowerShell umožňuje vytvářet proměnné, které jsou v podstatě pojmenované objekty. Výstup z jakékoli platný příkaz prostředí Windows PowerShell lze uložit do proměnné. Proměnné názvy vždy začínají znakem $. Pokud chcete uložit do proměnné s názvem $AppLog referenční informace k protokolům aplikace, zadejte název proměnné, za nímž následuje znaménko rovná se a zadejte příkaz použít k vytvoření objektu protokolu aplikace:

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

Zadejte $AppLog uvidíte, že obsahuje protokolu aplikace:

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### <a name="accessing-a-remote-event-log-with-new-object"></a>Přístup k vzdálené protokolu událostí s New-Object

Příkazy v předchozí části cílit na místní počítač; **Get-EventLog** rutiny, které můžete provést. Pro přístup k protokolu aplikací ve vzdáleném počítači, musíte zadat jak název protokolu a název počítače (nebo IP adresu) jako argumenty.

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

Když teď máme odkaz na protokol událostí, který je uložen v proměnné $RemoteAppLog, jaké úkoly jsme provádět v něm?

#### <a name="clearing-an-event-log-with-object-methods"></a>Vymazání protokolu událostí s objektových metod

Objekty často mají metody, které lze volat pro provádění úloh. Můžete použít **Get-Member** zobrazíte metody přidružené k objektu. Následující příkaz a vybrané výstupní představují některé metody třídy událostí:

```
PS> $RemoteAppLog | Get-Member -MemberType Method

   TypeName: System.Diagnostics.EventLog

Name                      MemberType Definition
----                      ---------- ----------
...
Clear                     Method     System.Void Clear()
Close                     Method     System.Void Close()
...
GetType                   Method     System.Type GetType()
...
ModifyOverflowPolicy      Method     System.Void ModifyOverflowPolicy(Overfl...
RegisterDisplayName       Method     System.Void RegisterDisplayName(String ...
...
ToString                  Method     System.String ToString()
WriteEntry                Method     System.Void WriteEntry(String message),...
WriteEvent                Method     System.Void WriteEvent(EventInstance in...
```

**Clear()** metodu je možné vymazat protokol událostí. Při volání metody, je nutné provést název metody v závorkách, i v případě, že metoda nevyžaduje argumenty. Díky tomu prostředí Windows PowerShell rozlišovat mezi metodu a potenciální vlastnost se stejným názvem. Zadejte následující příkaz pro volání **vymazat** metody:

```
PS> $RemoteAppLog.Clear()
```

Zadejte následující příkaz pro zobrazení protokolu. Uvidíte, že byl vymazán. v protokolu událostí a teď má 0 položek místo 262:

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### <a name="creating-com-objects-with-new-object"></a>Vytváření objektů COM pomocí New-Object
Můžete použít **New-Object** pro práci s komponenty modelu COM (Component Object). Součásti v rozsahu od různé knihovny zahrnuté do ActiveX aplikací, jako je například Internet Explorer, které jsou nainstalovány ve většině systémů Windows Script Host (WSH).

**Nový objekt** používá rozhraní .NET Framework Runtime – obálky s možností k vytváření objektů modelu COM, tak má stejné omezení, které rozhraní .NET Framework při volání metody COM objekty. Chcete-li vytvořit objekt modelu COM, je třeba zadat **ComObject** parametr s programový identifikátor nebo *ProgId* třídy modelu COM, kterou chcete použít. Úplné informace o omezení použití modelu COM a určení, jaké jsou k dispozici v systému ProgID je nad rámec tohoto průvodce, ale dobře známým objektům z prostředí, jako je prostředí WSH lze použít v prostředí Windows PowerShell.

Můžete vytvořit prostředí WSH objekty tak, že zadáte tyto ProgID: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, a **Scripting.FileSystemObject**. Následující příkazy vytvoří tyto objekty:

```powershell
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

Přestože většinu funkcí těchto tříd je k dispozici jiným způsobem v prostředí Windows PowerShell, jsou stále snazší používání tříd prostředí WSH několik úloh, jako je například vytváření zástupce.

### <a name="creating-a-desktop-shortcut-with-wscriptshell"></a>Vytvoření zástupce na ploše pomocí WScript.Shell

Jeden úkol, který můžete rychle provést pomocí objektu COM je vytvoření zástupce. Předpokládejme, že chcete vytvořit zástupce na ploše, který odkazuje na domovskou složku pro prostředí Windows PowerShell. Nejprve musíte vytvořit odkaz na **WScript.Shell**, kterém jsme se uloží do proměnné s názvem **$WshShell**:

```powershell
$WshShell = New-Object -ComObject WScript.Shell
```

Get-Member funguje s objekty COM, abyste mohli zkoumat členy objektu tak, že zadáte:

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

**Get-Member** má volitelnou **InputObject** parametr, můžete místo zřetězení příkazů k zadání **Get-Member**. Byste získali stejný výstup, jak je znázorněno výše, pokud jste místo toho použili příkaz **Get-Member - InputObject $WshShell**. Pokud používáte **InputObject**, zpracovává svůj argument jako jednu položku. To znamená, že pokud máte několik objektů v proměnné, **Get-Member** je zpracovává jako pole objektů. Příklad:

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

**WScript.Shell CreateShortcut** metoda přijímá jeden argument, cesta k souboru zástupce k vytvoření. Jsme mohli zadejte úplnou cestu k pracovní ploše, ale je snadnější. Ploše obvykle představuje složku s názvem Desktopu uvnitř domovskou složku aktuálního uživatele. Prostředí Windows PowerShell obsahuje proměnnou s **$Home** , který obsahuje cestu k této složce. Můžeme zadat cestu k domovské složky pomocí této proměnné a pak přidejte název složky Desktop a název zástupce vytvořit zadáním:

```powershell
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

Pokud používáte něco, co vypadá jako název proměnné v uvozovkách, prostředí Windows PowerShell se pokusí nahradit odpovídající hodnotu. Pokud používáte nabídek jedním, nepokusí se k nahrazení hodnoty proměnné prostředí Windows PowerShell. Zkuste například zadat následující příkazy:

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

Teď máme proměnnou s názvem **$lnk** , který obsahuje nový odkaz na místní. Pokud chcete zobrazit jejích členů, můžete zřetězit ho do **Get-Member**. Následující výstup zobrazí členy, že musíme použít k dokončení vytvoření náš zástupce:

```
PS> $lnk | Get-Member
TypeName: System.__ComObject#{f935dc23-1cf0-11d0-adb9-00c04fd58a0b}
Name             MemberType   Definition
----             ----------   ----------
...
Save             Method       void Save ()
...
TargetPath       Property     string TargetPath () {get} {set}
```

Budeme muset zadat **TargetPath**, což je složka aplikace pro Windows PowerShell a uložit místní **$lnk** voláním **Uložit** metody. Cesta ke složce aplikace prostředí Windows PowerShell je uložen v proměnné **$PSHome**, takže můžeme to udělat tak, že zadáte:

```powershell
$lnk.TargetPath = $PSHome
$lnk.Save()
```

### <a name="using-internet-explorer-from-windows-powershell"></a>Pomocí aplikace Internet Explorer z prostředí Windows PowerShell

Mnoho aplikací (včetně Microsoft Office řady aplikací a prohlížeče Internet Explorer) je možné automatizovat pomocí modelu COM. Aplikace Internet Explorer ukazuje některé typické technik a problémy při práci s aplikací založených na modelu COM.

Vytvořit instanci aplikace Internet Explorer tak, že zadáte Internet Explorer ProgId, **InternetExplorer.Application**:

```powershell
$ie = New-Object -ComObject InternetExplorer.Application
```

Tento příkaz spustí aplikaci Internet Explorer, ale není viditelný. Pokud zadáte Get-Process, uvidíte, že proces s názvem iexplore běží. Ve skutečnosti Pokud ukončení prostředí Windows PowerShell procesu nadále spuštěn. Musíte restartovat počítač nebo použijte nástroj Správce úloh, jako je ukončit proces iexplore.

> [!NOTE]
> Objekty COM, které začínají jako samostatné procesy říká *spustitelné soubory ActiveX*, může nebo nemusí být zobrazeny okno uživatelského rozhraní při jejich spuštění. Je-li vytvořit časové období, ale není viditelný, jako třeba Internet Explorer, budou obecně fokus na plochu Windows a je nutné provést v okně viditelné s ní pracovat.

Zadáním **$ie | Get-Member**, můžete zobrazit vlastnosti a metody pro aplikaci Internet Explorer. Pokud chcete zobrazit v okně aplikace Internet Explorer, nastavení vlastnosti Visible na $true zadáním:

```powershell
$ie.Visible = $true
```

Pak můžete přejít na konkrétní webovou adresu pomocí metody navigace:

```powershell
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

Pomocí dalších členů objektový model aplikace Internet Explorer, je možné načíst textový obsah z webové stránky. Následující příkaz zobrazí text ve formátu HTML v těle aktuální webové stránky:

```powershell
$ie.Document.Body.InnerText
```

Zavřete aplikaci Internet Explorer z v rámci prostředí PowerShell, volání metody Quit():

```powershell
$ie.Quit()
```

Tato akce vynutí ho zavřete. Přestože stále zdá být objekt modelu COM, ie proměnné $ už neobsahuje platný odkaz. Při pokusu o jeho použití, obdržíte chybu služby automation:

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

Můžete buď odstranit zbývající odkazovat pomocí příkazu jako $, ie = $null nebo úplně odebrat proměnnou tak, že zadáte:

```powershell
Remove-Variable ie
```

> [!NOTE]
> Neexistuje žádné je běžný standard pro Určuje, zda spustitelné soubory ActiveX ukončit nebo pokračovat v běhu při odebrání odkazu na jeden. V závislosti na okolnosti – třeba Určuje, zda je viditelný aplikaci, určuje, zda je spuštěna upravený dokument v něm a ještě Určuje, zda prostředí Windows PowerShell je stále spuštěna aplikace může nebo nemusí ukončete. Z tohoto důvodu byste měli otestovat chování pro každou ActiveX spustitelného souboru, že kterou chcete použít v prostředí Windows PowerShell.

### <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a>Získávání upozornění na objekty .NET Framework zabalené COM

V některých případech může mít objekt modelu COM přidružené rozhraní .NET Framework *Runtime Callable Wrapper* nebo obálky RCW a tím se použije **New-Object**. Protože chování Objekt RCW může lišit od chování normální objektu COM **New-Object** má **Strict** parametr upozornit RCW přístup. Pokud zadáte **Strict** parametr a poté vytvoříte objekt modelu COM, který používá obálky RCW, dostanete zprávu s upozorněním:

```
PS> $xl = New-Object -ComObject Excel.Application -Strict
New-Object : The object written to the pipeline is an instance of the type "Mic
rosoft.Office.Interop.Excel.ApplicationClass" from the component's primary inte
rop assembly. If this type exposes different members than the IDispatch members
, scripts written to work with this object might not work if the primary intero
p assembly is not installed.
At line:1 char:17
+ $xl = New-Object  <<<< -ComObject Excel.Application -Strict
```

I když je objekt stále vytvořen, se zobrazí upozornění, že není standardní objekt modelu COM.
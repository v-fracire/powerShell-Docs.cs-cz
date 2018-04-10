---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření nového objektu .NET a COM – objekty
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 1ffd8d4afa419ec0c24321e44aa4a2f41a9bee44
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="creating-net-and-com-objects-new-object"></a>Vytváření rozhraní .NET a objekty modelu COM (nový objekt)

Existují softwarové komponenty pomocí rozhraní .NET Framework a COM, které vám umožní provádět mnoho úloh správy systému. Prostředí Windows PowerShell umožňuje použít tyto součásti, takže můžete nejsou omezeny na úlohy, které lze provést pomocí rutin. Mnoho rutin v původní verze prostředí Windows PowerShell nefungují na vzdálených počítačích. Popisuje, jak získat obejít toto omezení při správě protokolů událostí pomocí rozhraní .NET Framework **System.Diagnostics.EventLog** třídy přímo z prostředí Windows PowerShell.

### <a name="using-new-object-for-event-log-access"></a>Použití nový objekt pro přístup k protokolu událostí

Knihovna tříd rozhraní .NET Framework zahrnuje třídy s názvem **System.Diagnostics.EventLog** který lze použít ke správě protokolů událostí. Můžete vytvořit novou instanci třídy rozhraní .NET Framework pomocí **New-Object** rutiny s **TypeName** parametr. Například následující příkaz vytvoří odkaz na protokol událostí:

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

I když příkaz vytvořil instanci třídy protokolu událostí, instance neobsahuje žádná data. Je to způsobeno jsme nezadali určitý protokol událostí. Jak získáte skutečné protokolu událostí

#### <a name="using-constructors-with-new-object"></a>Použití konstruktorů s nový objekt

Odkázat na určitém protokolu událostí, budete muset zadat název protokolu. **Nový objekt** má **ArgumentList** parametr. Argumenty, které můžete předat jako hodnoty tohoto parametru jsou používány speciální spuštění metodu objektu. Volání metody *konstruktor* protože se používá k vytvoření objektu. Například k získání odkazu do aplikačního protokolu, můžete zadat řetězec "Žádost" jako argument:

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> Vzhledem k tomu, že většina základní třídy rozhraní .NET Framework jsou obsaženy v oboru názvů systému, prostředí Windows PowerShell se automaticky pokusí vyhledat třídy, které zadáte v oboru názvů systému, pokud nemůže najít shodu pro typename, které zadáte. To znamená, že je možné zadat Diagnostics.EventLog místo System.Diagnostics.EventLog.

#### <a name="storing-objects-in-variables"></a>Ukládání objektů v proměnné

Můžete chtít uložit odkaz na objekt, abyste je mohli používat v aktuálním prostředí. I když prostředí Windows PowerShell můžete dělat spoustu práce s kanály, lessening potřebu proměnné, někdy ukládání odkazů na objekty v proměnné je pohodlnější k manipulaci s těchto objektů.

Prostředí Windows PowerShell umožňuje vytvářet proměnné, které jsou v podstatě s názvem objekty. Výstup z jakékoli platný příkaz prostředí Windows PowerShell můžete uložené v proměnné. Názvy proměnných vždy začínat $. Pokud chcete uložit do proměnné s názvem $AppLog protokolu odkaz na aplikaci, zadejte název proměnné následuje symbol rovná a pak zadejte příkaz sloužící k vytvoření objektu Application protokolu:

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

Pokud zadejte $AppLog můžete zjistit, že obsahuje protokolu aplikace:

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### <a name="accessing-a-remote-event-log-with-new-object"></a>Přístup k vzdáleného protokolu událostí s nový objekt

Funkce použité v předchozí části cílit na místní počítač; **Get-EventLog** rutiny můžete udělat. Chcete-li získat přístup k protokolu aplikace ve vzdáleném počítači, je nutné zadat název protokolu a název počítače (i IP adresu) jako argumenty.

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

Teď, když máme odkaz na protokol událostí uložené v proměnné $RemoteAppLog, můžete nám jaké úlohy provádět na něm?

#### <a name="clearing-an-event-log-with-object-methods"></a>Vymazání protokolu událostí pomocí metod objektu

Objekty mají často metody, které lze volat pro provádění úloh. Můžete použít **Get-člen** zobrazíte metody přidružená k objektu. Následující příkaz a vybrané výstupní zobrazit některé metody třídy protokolu událostí:

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

**Funkce Clear()** metoda slouží k vymazání protokolu událostí. Při volání metody, je nutné provést název metody v závorkách, i v případě, že metoda nevyžaduje argumenty. Díky tomu prostředí Windows PowerShell rozlišit mezi metoda a potenciální vlastnost se stejným názvem. Zadejte následující příkaz pro volání **zrušte** metoda:

```
PS> $RemoteAppLog.Clear()
```

Zadejte následující příkaz k zobrazení v protokolu. Zobrazí se, že protokol událostí byl vymazán a má teď 0 položek místo 262:

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### <a name="creating-com-objects-with-new-object"></a>Vytváření objektů modelu COM pomocí nového objektu
Můžete použít **New-Object** pro práci s komponenty modelu COM (Component Object). Součásti v rozsahu od různých knihoven zahrnuté do ActiveX aplikace, jako je například Internet Explorer, které jsou nainstalované na většina systémů s skriptu hostitele prostředí WSH (Windows).

**Nový objekt** používá rozhraní .NET Framework Runtime-– obálky s možností vytvořit objekty modelu COM, takže má stejná omezení, které nepodporuje rozhraní .NET Framework při volání COM – objekty. Vytvoření objektu COM, budete muset zadat **ComObject** parametr s programový identifikátor nebo *ProgId* třídy COM, kterou chcete použít. Úplné informace o omezení použití COM a určit, jaké ProgID jsou k dispozici v systému je nad rámec této uživatelské příručce, ale dobře známé objekty z prostředích, jako je prostředí WSH dá v prostředí Windows PowerShell.

Můžete vytvořit objekty WSH zadáním těchto ProgID: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, a  **Scripting.FileSystemObject**. Následující příkazy vytvořit tyto objekty:

```powershell
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

Přestože většinu funkcí těchto tříd je k dispozici jiným způsobem v prostředí Windows PowerShell, jsou stále lépe pomocí WSH třídy několik úloh, jako je například vytváření zástupce.

### <a name="creating-a-desktop-shortcut-with-wscriptshell"></a>Vytvoření zástupce na ploše s WScript.Shell

Jednu úlohu, která lze rychle provést pomocí objektu COM je vytvoření zástupce. Předpokládejme, že chcete vytvořit zástupce na ploše odkazující na domovskou složku pro prostředí Windows PowerShell. Je nutné nejprve vytvořit odkaz na **WScript.Shell**, který jsme budou ukládat do proměnné s názvem **$WshShell**:

```powershell
$WshShell = New-Object -ComObject WScript.Shell
```

Get-člen funguje s objekty modelu COM, abyste jej mohli prozkoumat členy objektu zadáním:

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

**Get-člen** má volitelný **InputObject** parametr, můžete místo zřetězení k zadání **Get-člen**. Které byste získali stejný výstup jako v příkladu nahoře, pokud místo toho použít příkaz **člen Get - InputObject $WshShell**. Pokud používáte **InputObject**, ho pracuje s její argument jako jednu položku. To znamená, že pokud máte několik objektů do proměnné, **Get-člen** pracuje s nimi jako pole objektů. Příklad:

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

**WScript.Shell CreateShortcut** metoda přijímá jeden argument, cesta k souboru zástupce vytvořit. Jsme může zadejte úplnou cestu k pracovní ploše, ale je jednodušší způsob. Na ploše je obvykle reprezentována složku s názvem plochy uvnitř domovskou složku aktuálního uživatele. Prostředí Windows PowerShell obsahuje proměnnou **$Home** obsahující cestu k této složce. Jsme můžete zadat cestu ke složce domácí pomocí této proměnné a poté přidejte název plochy složky a názvu zástupce vytvořit zadáním:

```powershell
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

Použijete-li objekt, který vypadá jako název proměnné uvnitř dvojitých uvozovek, pokusí se prostředí Windows PowerShell nahraďte odpovídající hodnotu. Pokud použijete jeden uvozovky, není pokusí nahraďte hodnotu proměnné prostředí Windows PowerShell. Zkuste například zadáním následujících příkazů:

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

Nyní je k dispozici proměnné s názvem **$lnk** obsahující odkaz na nový zástupce. Pokud chcete zobrazit členy, můžete zřetězit ho do **Get-člen**. Následující výstup zobrazuje členy, že je potřeba pro dokončení vytváření naše zástupce:

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

Je potřeba zadat **TargetPath –**, což je složka aplikace pro prostředí Windows PowerShell a potom uložte zástupce **$lnk** voláním **Uložit** metoda. Cesta ke složce aplikace prostředí Windows PowerShell je uložené v proměnné **$PSHome**, takže jsme lze provést zadáním:

```powershell
$lnk.TargetPath = $PSHome
$lnk.Save()
```

### <a name="using-internet-explorer-from-windows-powershell"></a>Použijte Internet Explorer z prostředí Windows PowerShell

Mnoho aplikací (včetně aplikace Microsoft Office řadu aplikací a prohlížeče Internet Explorer) je možné automatizovat pomocí modelu COM. Internet Explorer ukazuje některé typické techniky a problémy při práci s aplikace založené na modelu COM.

Vytvoření instance aplikace Internet Explorer tak, že zadáte v Internet Exploreru ProgId, **InternetExplorer.Application**:

```powershell
$ie = New-Object -ComObject InternetExplorer.Application
```

Tento příkaz spustí aplikaci Internet Explorer, ale není zviditelnit. Pokud zadáte Get-Process, uvidíte, že proces s názvem iexplore běží. Ve skutečnosti Pokud ukončení prostředí Windows PowerShell, proces bude nadále spouštět. Musíte restartovat počítač nebo použít nástroj podobně jako u Správce úloh ukončit proces iexplore.

> [!NOTE]
> Objekty COM, které začínají jako samostatné procesy, označovaného jako *spustitelné soubory ActiveX*, může nebo nemusí být zobrazeny okno uživatelského rozhraní při jejich spuštění. Pokud vytvoření okna, ale není zviditelnit, jako třeba Internet Explorer, budou obecně fokus na ploše systému Windows a je nutné provést okna viditelné pracovat s ním.

Zadáním **$ie | Get-člen**, můžete zobrazit vlastnosti a metody pro Internet Explorer. Pokud chcete zobrazit okno aplikace Internet Explorer, nastavte vlastnost Visible na $true zadáním:

```powershell
$ie.Visible = $true
```

Potom můžete přejít na konkrétní webovou adresu pomocí metody přejděte:

```powershell
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

Pomocí ostatním členům objektový model aplikace Internet Explorer, je možné načíst textový obsah z webové stránky. Následující příkaz zobrazí text ve formátu HTML v těle aktuální webové stránky:

```powershell
$ie.Document.Body.InnerText
```

Zavřete Internet Explorer z prostředí PowerShell, volejte příslušnou metodu Quit():

```powershell
$ie.Quit()
```

Tato akce vynutí ho zavřete. Ie proměnné $ už neobsahuje platný odkaz, i když stále se zdá, že se objekt COM. Pokud se pokusíte použít, obdržíte chybu automatizace:

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

Můžete buď odstranit zbývající odkazovat pomocí příkazu jako $ie = $null nebo úplně odebrat proměnnou zadáním:

```powershell
Remove-Variable ie
```

> [!NOTE]
> Neexistuje žádné běžný standard pro jestli spustitelné soubory ActiveX ukončit nebo pokračovat v běhu při odebrání odkaz na jednu. V závislosti na případech, například zda je aplikace viditelné, jestli je v něm spuštěný upravený dokument a i jestli prostředí Windows PowerShell je stále spuštěná aplikace může nebo nemusí ukončit. Z tohoto důvodu byste měli otestovat chování při ukončení pro každý ActiveX spustitelného souboru, že kterou chcete použít v prostředí Windows PowerShell.

### <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a>Získávání upozornění o rozhraní .NET Framework zabalené COM – objekty

V některých případech může mít objekt COM přidružené rozhraní .NET Framework *obálka volatelná za běhu* nebo RCW a tím se použije **New-Object**. Vzhledem k tomu, že chování RCW se může lišit od chování normální objektu COM **New-Object** má **Strict** parametru informují o RCW přístup. Pokud zadáte **Strict** parametr a potom vytvoříte objekt modelu COM, který se používá RCW, zobrazí zprávu s upozorněním:

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

I když je objekt stále vytvořen, budete upozorněni, že se nejedná o standardní objektu COM.
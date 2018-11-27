---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Co je nového ve Windows Powershellu 5.0
ms.openlocfilehash: 78304b0eac6e58e43bffc3abb7059a1e4b02de23
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320716"
---
# <a name="whats-new-in-windows-powershell-50"></a>Co je nového ve Windows Powershellu 5.0
Windows PowerShell 5.0 obsahuje důležité nové funkce, které rozšiřují jeho použití, lepší použitelnost a umožňují řídit a spravovat prostředí Windows snadněji a komplexněji.

Windows PowerShell 5.0 je zpětně kompatibilní. Rutiny, poskytovatelů, moduly, moduly snap in, skripty, funkce a profily, které byly navrženy pro Windows PowerShell 4.0, Windows PowerShell 3.0 a Windows PowerShell 2.0 obecně fungovat bez nutnosti změn ve Windows Powershellu 5.0.

## <a name="installing-windows-powershell"></a>Instalace Windows PowerShellu
Ve výchozím nastavení v systému Windows Server 2016 Technical Preview a Windows 10 je nainstalovaný Windows PowerShell 5.0.

Pokud chcete nainstalovat Windows PowerShell 5.0 na Windows Server 2012 R2, Windows 8.1 Enterprise nebo Windows 8.1 Pro, stáhněte a nainstalujte [Windows Management Framework 5.0](https://aka.ms/wmf5download). Nezapomeňte si přečíst podrobnosti o stahování a splňovat všechny požadavky na systém, před instalací Windows Management Framework 5.0.

## <a name="in-this-topic"></a>V tomto tématu

- [Windows PowerShell 4.0 DSC aktualizace KB 3000850](#windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850)
- [Nové funkce ve Windows Powershellu 5.0](#new-features-in-windows-powershell-50)
- [Nové funkce ve Windows Powershellu 4.0](#new-features-in-windows-powershell-40)
- [Nové funkce ve Windows Powershellu 3.0](#new-features-in-windows-powershell-30)

## <a name="windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850"></a>Windows PowerShell 4.0 aktualizace z listopadu 2014 kumulativní (KB 3000850)
Jsou k dispozici v mnoha aktualizace a vylepšení pro Windows PowerShell Desired State Configuration (DSC) ve Windows PowerShell 4.0 [kumulativní aktualizace z listopadu 2014 pro Windows RT 8.1, Windows 8.1 a Windows Server 2012 R2](https://support.microsoft.com/kb/3000850/) (KB 3000850 ). Můžete určit, pokud je KB 3000850 nainstalovaný ve vašem systému spuštěním `Get-Hotfix -Id KB3000850` v prostředí Windows PowerShell.

- Aktualizace stávající rutiny v [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modulu
  - [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) je rychlejší (zejména v prostředí ISE).
  - [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) má nový parametr - UseExisting, která znovu použije poslední použité konfigurace.
  - [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) – platnost byla opravena.
  - [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx) zobrazí další užitečné informace o stavu modulu.
  - [Test-DscConfiguration](https://technet.microsoft.com/library/dn407382.aspx) nyní vrátí název počítače společně s hodnotu True nebo False.
  - [Nové DscChecksum](https://technet.microsoft.com/library/dn521622.aspx) teď podporuje cesty UNC.

- Nové rutiny v [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modulu
  - [Update-DscConfiguration](https://technet.microsoft.com/library/mt143541(v=wps.630).aspx): kontroluje server na vyžádání.
  - [Stop-DscConfiguration](https://technet.microsoft.com/library/mt143542(v=wps.630).aspx): ukončí konfiguraci, která je již spuštěna.
  - [Odebrat DscConfigurationDocument](https://technet.microsoft.com/library/mt143544(v=wps.630).aspx): umožňuje odebrání konfigurace dokumentů v různých fázích (čekající na vyřízení, předchozí nebo aktuální).

- Vylepšení jazyka
  - DependsOn teď podporuje složené prostředky.
  - DependsOn teď podporuje čísla v instanci názvy prostředků.
  - Uzel výrazy, které už vyhodnocena jako prázdná vyvolat chyby.
  - Opravili jsme chybu, která nastane, pokud uzel výraz vyhodnocen jako prázdný.
  - Konfigurace volání konfigurace nyní pracují v konzole Windows Powershellu.

- Vylepšení režimu o přijetí změn
  - Režim o přijetí změn teď podporuje všechny soubory ZIP.
  - **AllowModuleOverwrite** teď funguje správně.

- Vylepšení odolnosti proti chybám
  - Nové **režim DebugMode** umožňuje znovu načíst prostředek moduly.
  - Pokud dojde k selhání konfigurace, soubor pending.mof není odstraněn.
  - Místní Configuration Manageru (LCM) je nyní odolnější, při nastavení metaconfiguration byly poškozeny.

- Vylepšení diagnostiky
  - Zobrazí se upozornění, když časovač LCM nastaví na různá nastavení, než jste zadali.
  - Soubory protokolů chyb teď obsahují zásobník volání pro prostředky v prostředí Windows PowerShell.

- Vylepšení flexibilitu
  - Prostředek LocalConfigurationManager má nové vlastnosti **ActionAfterReboot**.
    - ContinueConfiguration (výchozí hodnota): automaticky obnoví konfiguraci po restartování cílového uzlu.
    - StopConfiguration: Není automaticky pokračovat na konfiguraci po restartování uzlu.
  - Spustit konzistence můžete nyní častěji než operace přijetí změn, nebo naopak.
  - Podpora správy verzí: DSC na novější klient teď poznáte dokument, který byl vygenerován (je součástí [WMF 5.0](https://aka.ms/wmf5download)).

- Chyba vylepšení ochrany před únikem informací
  - Verze modulu je nyní vynucena služba před použitím konfigurace.
  - **DebugPreference** jsou správně nastavena teď pro Get-, Set- nebo TargetResource testovací volání.

- Zlepšení zpracování přihlašovacích údajů
  - Certifikát se teď používá, pokud mají oba **certifikát** a **PSDscAllowPlainTextPassword** jsou uvedeny.
  - Přihlašovací údaje se dešifrují i pro Get-TargetResource.
  - Metaconfiguration přihlašovací údaje jsou zašifrované a dešifrovat.
  - PSCredentials jsou nyní dešifrovat, pokud se nachází ve vložený objekt.

- Vylepšení integrované prostředků
  - Prostředek Package
    - Už nainstaluje balíček nesprávné (buď z místní nebo webového zdroje).
    - Teď podporuje protokol HTTPS.
  - Byla přidána podpora pro protokol HTTPS v [balíček prostředků](https://technet.microsoft.com/library/dn282132.aspx).
  - [Archivovat prostředků](https://technet.microsoft.com/library/dn249917.aspx) nyní podporuje přihlašovací údaje.

## <a name="new-features-in-windows-powershell-50"></a>Nové funkce ve Windows Powershellu 5.0

- [Nové funkce v prostředí Windows PowerShell](#new-features-in-windows-powershell)
- [Nové funkce ve Windows Powershellu Desired State Configuration](#new-features-in-windows-powershell-desired-state-configuration)
- [Nové funkce v prostředí Windows PowerShell ISE](#new-features-in-windows-powershell-ise)
- [Nové funkce ve Windows Powershellu webové služby](#new-features-in-windows-powershell-web-services-management-odata-iis-extension)
- [Důležité opravy chyb ve Windows Powershellu 5.0](#notable-bug-fixes-in-windows-powershell-50)

### <a name="new-features-in-windows-powershell"></a>Nové funkce v prostředí Windows PowerShell

- Od verze Windows Powershellu 5.0, můžete vyvíjet s použitím tříd, s použitím formální syntaxi a sémantiku, která se podobně jako jiné objektově orientované programovací jazyky. **Třída**, **výčtu**, a dalších klíčových slovech byly přidány do prostředí Windows PowerShell jazyk o podporu nové funkce. Další informace o práci s třídami naleznete v tématu about_Classes.

- Windows PowerShell 5.0 zavádí nové, strukturované informace datového proudu, který vám umožní přenést strukturovaná data mezi skriptu a jeho volající (nebo hostitelské prostředí). Write-Host teď můžete generovat výstup do datového proudu informace. Informace o datových proudů fungovat i pro PowerShell.Streams, úlohy, naplánované úlohy a pracovních postupů. Tyto funkce podporují informační stream.
  - Nová rutina Write-informace, které umožňuje určit způsob, jakým zpracovává data datového proudu informace pro příkaz prostředí Windows PowerShell. Write-Host tvoří obálku pro zápis informace. Zápis informace jsou také aktivita podporované pracovního postupu.
  - Dvě nové společné parametry, InformationVariable a InformationAction, umožňují určit, jak se zobrazují informace o datových proudů z příkazu. Platné hodnoty pro InformationAction jsou SilentlyContinue, zastavení, pokračovat, Inquire, ignorovat nebo pozastavit s SilentlyContinue je výchozí hodnota. InformationVariable Určuje řetězec jako název proměnné, do kterého chcete data Write-Host z příkazu Uložit.
  - Nové proměnné předvoleb InformationPreference, určuje vaše výchozí prioritu pro informace o streamování dat v relaci Windows Powershellu. Výchozí hodnota je SilentlyContinue.
  - Přidali jsme dvě nové společné parametry pracovního postupu, PSInformation a InformationAction.
  - Při použití příkazu Format-Table sloupců tabulky jsou nyní automaticky naformátovat vyhodnocením první 300ms data, která se předá prostřednictvím datového proudu.

- Ve spolupráci s [Microsoft Research](https://research.microsoft.com/), byla přidána nová rutina ConvertFrom-řetězec. ConvertFrom-String umožňuje extrakce a analýza strukturovaných objektů z obsahu textového řetězce. Další informace najdete v tématu ConvertFrom-řetězec.
- Nová rutina převést řetězec automaticky formátuje text založené na příklad, který zadáte parametr – příklad.
- Nový modul Microsoft.PowerShell.Archive, zahrnuje rutiny, které umožňují komprimovat soubory a složky v souborech archivu (označované také jako soubor ZIP), extrahujte soubory z existujících souborů ZIP a aktualizovat soubory ZIP s novějšími verzemi soubory zkomprimované v nich.
- Nový modul PackageManagement, umožňuje zjišťovat a instalovat softwarové balíčky v síti Internet. Modulu PackageManagement (dříve označované jako OneGet) je správce nebo multiplexor z existujícího Správce balíčků (také nazývané poskytovatelé balíčku) umožní sjednotit správu balíčků Windows pomocí jednoho rozhraní prostředí Windows PowerShell.
- Nový modul PowerShellGet, umožňuje hledat, instalovat, publikovat a aktualizovat moduly a prostředky DSC na [Galerie prostředí PowerShell](https://www.powershellgallery.com/), nebo na interní modul úložiště, která můžete nastavit tak, spustíte rutinu Register-PSRepository.
- Nové klíčové slovo jazyka, **skryté**, byla přidána k určení, že člena (vlastnost nebo metodu) nezobrazuje ve výchozím nastavení ve výsledcích Get-Member (Pokud nepřidáte parametr - Force). Vlastnosti nebo metody, které byly označeny jako skryté také nezobrazí ve výsledcích technologie IntelliSense, pokud jsou v kontextu, kde by mělo být člen viditelný. například na automatické proměnné $, které by se zobrazit skryté členy v metodu třídy.
- Nová položka, odeberte položku a Get-ChildItem vylepšené a podporují vytváření a správu [symbolické odkazy](https://en.wikipedia.org/wiki/Symbolic_link). **- ItemType** přijímá nová hodnota parametru pro New-Item **SymbolicLink**. Nyní můžete vytvořit symbolické odkazy na jednom řádku, spuštěním rutiny New-Item.
- Rutina Get-ChildItem má také nové - Depth parametr, který používáte s parametrem - Recurse omezit rekurze. Například Get-ChildItem-Recurse - 2 hloubky vrátí výsledky z aktuální složky, všechny podřízené složky do aktuální složky a všechny složky v rámci podřízené složky.
- Teď umožňuje zkopírujete soubory nebo složky z jedné relace prostředí Windows PowerShell do druhého, což znamená, že můžete zkopírovat soubory do relací, které jsou připojené ke vzdáleným počítačům copy-Item (včetně počítačů, na kterých běží [Nano Server](https://blogs.technet.com/b/windowsserver/archive/2015/04/08/microsoft-announces-nano-server-for-modern-apps-and-cloud.aspx), a tedy mít žádné rozhraní). Kopírování souborů, zadejte jako hodnotu nové parametry - FromSession a - ToSession ID relace PSSession a přidejte - cestu a - cíl a zadejte cestu ke zdroji a určení, v uvedeném pořadí. Například Copy-Item-c: cesta\\myFile.txt - ToSession $s – určení d:\\můžete.
- Vylepšili jsme prostředí Windows PowerShell určené k transkripci má použít pro všechny hostitelské aplikace (jako je Windows PowerShell ISE) kromě hostitel konzoly (**powershell.exe**). Možnosti přepisu (včetně povolení systémová přepisu) můžete nakonfigurovat tím, že **zapnout prostředí PowerShell určené k transkripci** nastavení zásad skupiny, nalezen v správu součásti šablony/Windows/Windows Prostředí PowerShell.
- Nová funkce skriptu podrobné trasování umožňuje povolit podrobné sledování a analýza použití skriptu prostředí Windows PowerShell v systému. Po povolení trasování podrobné skript prostředí Windows PowerShell zaznamená do protokolu událost Event Tracing for Windows (ETW), všechny bloky skriptu **Microsoft-Windows-PowerShell/Operational**.
- Od verze Windows Powershellu 5.0, nové rutiny Cryptographic Message Syntax podporují šifrování a dešifrování obsahu s využitím standardního formátu IETF kryptograficky ochrany zprávy podle ní správný [RFC5652](https://tools.ietf.org/html/rfc5652). Rutiny Get-CmsMessage CmsMessage chránit a Unprotect-CmsMessage byly přidány do [Microsoft.PowerShell.Security](https://technet.microsoft.com/library/hh849807.aspx) modulu.
- Nové rutiny v [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modulu, Get-prostředí Runspace, ladicí prostředí Runspace, Get-RunspaceDebug, RunspaceDebug povolit a zakázat RunspaceDebug, můžete tak nastavit možnosti ladění na prostředí runspace a spouštění a zastavování ladění na prostředí runspace. Pro ladění libovolného prostředí runspace "tedy prostředí runspace, které nejsou v konzole Windows Powershellu nebo Windows PowerShell ISE relace prostředí runspace výchozí" "prostředí Windows PowerShell vám umožní nastavit zarážky ve skriptu a přidali zarážky zastavit z spuštění, dokud se můžete připojit ladicí program k ladění skriptu prostředí runspace. Vnořené podporu ladění pro libovolné prostředí runspace byla přidána k ladicímu prostředku skriptů prostředí Windows PowerShell pro prostředí runspace.
- Přibyla nová rutina formátu Hex [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modulu. Formát Hex umožňuje zobrazit text nebo binární data v šestnáctkovém formátu.
- Byly přidány do rutiny Get-schránky a schránky sadu [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modul; usnadňují jejich přenos obsahu do a z relace prostředí Windows PowerShell. Rutiny schránky podporují obrázky, zvukové soubory, seznamy souborů a text.
- Nová rutina Clear-odpadkový koš, byl přidán do [Microsoft.PowerShell.Management](https://technet.microsoft.com/library/hh849827(v=wps.640).aspx) modulu; tato rutina prázdné recyklace Bin pro pevnou jednotku, která zahrnuje externích jednotek. Ve výchozím nastavení se výzva k potvrzení příkazu vymazat odpadkový koš, protože vlastnost ConfirmImpact rutiny je nastavena na ConfirmImpact.High.
- Nová rutina New-TemporaryFile umožňuje vytvořit dočasný soubor jako součást skriptování. Ve výchozím nastavení, je vytvořen nový dočasný soubor v ```C:\Users\<user name>\AppData\Local\Temp```.
- Out-File, přidat obsah a rutiny Set-obsahu teď mají nový parametr - NoNewline vynechá nový řádek za výstupem.
- Rutina New-Guid využívá rozhraní .NET Framework Guid třídu pro generování identifikátoru GUID, užitečné při psaní skriptů nebo prostředky DSC.
- Vzhledem k tomu, že informace o verzi souboru může být matoucí, zejména po opravit soubor, jsou k dispozici pro objekty FileInfo nové vlastnosti skriptu FileVersionRaw a ProductVersionRaw. Můžete například spustit následující příkaz, který zobrazí hodnoty těchto vlastností pro powershell.exe, kde $pid obsahuje ID procesu pro spuštěné relaci Windows powershellu:  ```Get-Process -Id $pid -FileVersionInfo | Format-List *version* -Force```
- Nové rutiny Enter PSHostProcess a ukončení PSHostProcess umožňují ladění skriptů prostředí Windows PowerShell v procesy nezávisle na aktuální proces, na kterém běží v konzole Windows Powershellu. Spusťte Enter PSHostProcess nebo připojit k ID procesů a pak spusťte Get-prostředí Runspace se vraťte aktivní prostředí runspace v rámci procesu. Spusťte ukončovací PSHostProcess se odpojit od procesu po dokončení ladění skriptu v rámci procesu.
- Přibyla nová rutina čekání ladicího programu [Microsoft.PowerShell.Utility](https://technet.microsoft.com/library/hh849958.aspx) modulu. Můžete spustit čekání – ladicí program zastaví skript v ladicím programu před spuštěním dalšího příkazu do skriptu.
- Ladicí program pracovní postup prostředí Windows PowerShell teď podporuje dokončení příkazu nebo kartu a vnořený pracovní postup funkce můžete ladit. Nyní můžete stisknout **Ctrl + Break** zadat ladicí program spouští skript, místních i vzdálených relací a pracovního postupu skriptu.
- Rutiny ladění úlohy byl přidán do [Microsoft.PowerShell.Core](https://technet.microsoft.com/library/hh849695.aspx) modul ladění skriptů spuštěných úloh pro pracovní postup prostředí Windows PowerShell, pozadí a úlohy spuštěné v vzdálené relace.
- Byl přidán nový stav AtBreakpoint, pro úlohy Windows Powershellu. Stav AtBreakpoint platí, pokud úlohy běží skript, který obsahuje nastavení zarážek a skript dosáhne zarážky. Úlohy zastavení na zarážce ladění, musí ladění úlohy po spuštění rutiny ladění úlohy.
- Windows PowerShell 5.0 implementuje podporu více verzí jeden modul prostředí Windows PowerShell ve stejné složce v $PSModulePath. Vlastnost RequiredVersion přidaná do třídy ModuleSpecification umožňující že získat požadovaná verze modulu; Tato vlastnost je vzájemně se vylučuje s vlastnost verze modulu. RequiredVersion je teď podporovaná jako část hodnoty parametru FullyQualifiedName příkazu Get-Module, Import-Module a rutiny Remove-Module.
- Po spuštění rutiny Test-ModuleManifest můžete nyní provést ověření verze modulu.
- Výsledky rutiny Get-Command teď zobrazí sloupec verze. do třídy CommandInfo byla přidána nová vlastnost verze. Get-Command ukazuje příkazy z více verzí stejného modulu. Vlastnost verze je také součástí odvozené třídy CmdletInfo: CmdletInfo a ApplicationInfo.
- Get-Command má nový parametr - ShowCommandInfo, který vrací informace ShowCommand jako PSObjects. Toto je obzvláště užitečná funkce pro při spuštění zobrazit příkaz v prostředí Windows PowerShell ISE pomocí vzdálené komunikace Windows Powershellu. Parametr - ShowCommandInfo nahrazuje stávající funkci Get-SerializedCommand v modulu Microsoft.PowerShell.Utility Get-SerializedCommand skriptu je však stále k dispozici a podporují skriptování nižší úrovně.
- Nová Rutina Get-ItemPropertyValue umožňuje získat hodnotu vlastnosti bez použití zápisu s tečkou. Například ve starších verzích Windows Powershellu spustíte následující příkaz k získání hodnoty vlastnosti základ cesty aplikace PowerShellEngine klíče registru: **(Get-ItemProperty-cesta HKLM:\\softwaru\\ Microsoft\\PowerShell\\3\\PowerShellEngine – název ApplicationBase). ApplicationBase**. Od verze Windows Powershellu 5.0, můžete spustit **Get ItemPropertyValue-cesta HKLM:\\softwaru\\Microsoft\\PowerShell\\3\\PowerShellEngine – název ApplicationBase** .
- Konzoly Windows Powershellu teď používá syntaxi barevné zvýrazňování, stejně jako u Windows PowerShell ISE.
- Nový modul NetworkSwitch obsahuje rutiny, které vám umožní použít přepínač virtuální sítě LAN (VLAN) a základní konfigurací portu síťového přepínače vrstvy 2 pro systém Windows Server 2012 R2 měly certifikované logo síťové přepínače.
- Parametr FullyQualifiedName se přidala do rutiny Import-Module a Remove-Module pro podporu ukládání více verzí modulu single.
- Nový parametr FullyQualifiedModule typu ModuleSpecification mít Save-Help, Update-Help, Import-PSSession, Export-PSSession a Get-Command. Přidejte tento parametr k určení modul pomocí jeho plně kvalifikovaného názvu.
- Hodnota **$PSVersionTable.PSVersion** byl aktualizován na 5.0.

### <a name="new-features-in-windows-powershell-desired-state-configuration"></a>Nové funkce ve Windows Powershellu Desired State Configuration

- Vylepšení jazyka prostředí Windows PowerShell vám umožní definovat prostředky Windows PowerShell Desired State Configuration (DSC) pomocí tříd. Import-DscResource je nyní true dynamické klíčové slovo; Analyzuje zadaný modul prostředí Windows PowerShell "™ s kořenový modul, hledání třídy, které obsahují atribut DscResource. Nyní můžete tříd k definování prostředků DSC, které ani souboru MOF ani DSCResource podsložky ve složce modulu není povinné. Soubor modulu Windows PowerShell může obsahovat více tříd prostředků DSC.
- Nový parametr ThrottleLimit, byla přidána do následujících rutin v modulu PSDesiredStateConfiguration. Přidáte parametr ThrottleLimit můžete určit počet cílových počítačů nebo zařízení, na kterých se má příkaz pracovat ve stejnou dobu.
  - Get-DscConfiguration
  - Get-DscConfigurationStatus
  - Get-DscLocalConfigurationManager
  - Restore-DscConfiguration
  - Test-DscConfiguration
  - Porovnání DscConfiguration
  - Publikování DscConfiguration
  - Set-DscLocalConfigurationManager
  - Start-DscConfiguration
  - Update-DscConfiguration
- S centralizovanou DSC hlášení chyb, se bohaté chybové informace neprotokolují pouze v případě, že protokolu, ale je odeslat do centrálního umístění pro pozdější analýzu. Můžete použít tento centrální umístění pro uložení chyby konfigurace DSC, ke kterým došlo u libovolného serveru v jejich prostředí. Po server sestav je definované v meta konfiguraci, všechny chyby odeslání na server sestav a pak uloženy v databázi. Tato funkce bez ohledu na to, jestli je nakonfigurovaná cílový uzel můžete nastavit na o přijetí změn konfigurace ze serveru vyžádané replikace.
- Vylepšení pro Windows PowerShell ISE usnadňují vytváření prostředků DSC. Nyní můžete provést následující.
  - Všechny prostředky DSC v seznamu **konfigurace** nebo **uzel** bloku tak, že zadáte **kombinace kláves Ctrl + mezerník** na prázdný řádek v rámci bloku.
  - Automatické dokončování ve vlastnosti prostředku **výčet** typu.
  - Automatické dokončení **DependsOn** vlastnost prostředků DSC, podle instance jiných prostředků v konfiguraci.
  - Vylepšené tab k dokončování příkazů hodnot vlastností prostředku.
- Uživatel teď můžete prostředek pod zadanou sadu přihlašovacích údajů spustit tak, že přidáte **PSDscRunAsCredential** atribut uzlu bloku. Například PSDscRunAsCredential = Get-Credential Contoso\\DscUser. Tato funkce je užitečná pro vytvoření konfigurace, které spuštění Instalační služby systému Windows a spustitelný instalační programy, přístup k podregistru na uživatele nebo provádět jiné úlohy mimo aktuální uživatelský kontext.
- byla přidána podpora (založený na x86) 32-bit pro **konfigurace** – klíčové slovo.
- Prostředí Windows PowerShell teď zahrnuje podporu pro vlastní nápovědy ke konfiguracím DSC, definována tak, že přidáte \[CmdletBinding()] funkce vygenerovanou konfiguraci.
- Nový **DscLocalConfigurationManager** atribut označí blok konfigurace jako meta konfigurace, který se používá ke konfiguraci DSC Local Configuration Manageru. Tento atribut omezuje konfiguraci, kterou chcete obsahující jenom položky, které konfigurace DSC Local Configuration Manageru. Během zpracování, tato konfigurace generuje \*. meta.mof soubor, který se pak posílají do příslušné cílové uzly spuštěním rutiny Set-DscLocalConfigurationManager.
- Částečné konfigurace jsou teď povolené ve Windows Powershellu 5.0. Konfigurace dokumentů můžete doručovat do uzlu ve fragmentech. U uzlu přijímat více fragmentů dokumentu konfigurace uzlu '™ s Local Configuration Manageru musíte nejprve nastavit k určení očekávaných fragmenty
- Synchronizace mezi počítači je novinkou ve Windows Powershellu 5.0 DSC. Pomocí předdefinovaných WaitFor\* prostředky (**WaitForAll**, **WaitForAny**, a **WaitForSome**), můžete nyní určení závislostí mezi počítači Během konfigurace spuštění bez externí Orchestrace. Tyto zdroje poskytují s použitím modelu CIM připojení přes protokol WS-Man synchronizace mezi uzly. Konfigurace může čekat na jiný počítač "™ chcete změnit stav s konkrétní prostředek.
- Právě Enough Administration (JEA), nová funkce zabezpečení delegování, využívá DSC a prostředí Windows PowerShell omezené prostředí runspace pomáhá zabezpečené podnikům proti ztrátě dat nebo ohrožení zaměstnanci, zda úmyslnému i neúmyslnému. Další informace o JEA, včetně, kde si můžete stáhnout prostředek xJEA DSC, naleznete v tématu [Just Enough Administration, krok za krokem](https://blogs.technet.com/b/privatecloud/archive/2014/05/14/just-enough-administration-step-by-step.aspx).
- Byly přidány následující nové rutiny modulu PSDesiredStateConfiguration.
  - Nová Rutina Get-DscConfigurationStatus získá základní informace o konfiguraci stavu z cílového uzlu. Můžete získat stav posledního, nebo všechny konfigurace.
  - Nová rutina Compare-DscConfiguration porovnává zadanou konfiguraci se skutečným stavem jeden nebo více cílových uzlů.
  - Nové rutiny Publish-DscConfiguration zkopíruje na cílový uzel konfiguračního souboru MOF, ale v konfiguraci se nevztahuje. Tato konfigurace používá další průchodu konzistence, nebo při spuštění rutiny Update-DscConfiguration.
  - Nová rutina Test-DscConfiguration slouží k ověření, že výsledný konfigurace odpovídá požadované konfigurace, vrátí hodnotu True, pokud konfigurace odpovídá požadované konfigurace, nebo hodnotu NEPRAVDA, pokud skutečnou konfiguraci neodpovídá požadované konfigurace.
  - Nová rutina Update-DscConfiguration vynutí konfiguraci, kterou chcete zpracovat. Pokud Local Configuration Manageru je v režimu o přijetí změn, rutina před každým jejím použitím získá konfiguraci ze serveru vyžádané replikace.

### <a name="new-features-in-windows-powershell-ise"></a>Nové funkce v prostředí Windows PowerShell ISE

- Teď můžete upravit vzdáleného prostředí Windows PowerShell skriptů a souborů v místní kopii Windows PowerShell ISE spuštěním Enter-PSSession spouští vzdálenou relaci v počítači, který "™ s ukládání souborů, které chcete upravit a následné spuštění **PSEdit <path and file name on the remote computer>**. Tato funkce usnadňuje úpravy souborů Windows Powershellu, které jsou uložené na instalaci jádra serveru systému Windows Server, ve kterém nelze spustit Windows PowerShell ISE.
- Rutina Start-přepisu se teď podporuje v prostředí Windows PowerShell ISE.
- Teď můžete ladit vzdálenou skriptů v prostředí Windows PowerShell ISE.
- Nový příkaz nabídky **příkaz Pozastavit vše** (Ctrl + B) rozdělí do ladicího programu pro místní a vzdálené spuštění skriptů.

### <a name="new-features-in-windows-powershell-web-services-management-odata-iis-extension"></a>Nové funkce ve Windows Powershellu webové služby (IIS rozšíření správy OData)

- Od verze Windows Powershellu 5.0, můžete vygenerovat sadu rutin Windows Powershellu závislosti na funkcích vystavené daný koncový bod OData, spuštěním rutiny Export-ODataEndpointProxy, nalezen v novém [ Microsoft.PowerShell.OdataUtils](https://technet.microsoft.com/library/dn818507(v=wps.640).aspx) modulu.

### <a name="notable-bug-fixes-in-windows-powershell-50"></a>Důležité opravy chyb ve Windows Powershellu 5.0

- Windows PowerShell 5.0 obsahuje novou implementaci modelu COM, která nabízí výrazné zlepšení výkonu při práci s objekty COM. Video ukázku účinek, najdete v části [Com_Perf_Improvements](https://1drv.ms/1qu3UPZ).
- Výrazné zlepšení výkonu byly provedeny na první kartě dokončení v relaci Windows Powershellu zkrácení času dokončení kartu podle téměř 500 ms.

## <a name="new-features-in-windows-powershell-40"></a>Nové funkce ve Windows Powershellu 4.0

Windows PowerShell 4.0 je zpětně kompatibilní. Rutiny, poskytovatelů, moduly, moduly snap in, skripty, funkce a profily, které byly navrženy pro Windows PowerShell 3.0 a Windows PowerShell 2.0 fungovat bez nutnosti změn ve Windows Powershellu 4.0.

Windows PowerShell 4.0 se instaluje standardně na Windows 8.1 a Windows Server 2012 R2. Pokud chcete nainstalovat Windows PowerShell 4.0 na Windows 7 s aktualizací SP1 nebo Windows Server 2008 R2, stáhněte a nainstalujte [Windows Management Framework 4.0](https://www.microsoft.com/download/details.aspx?id=40855). Nezapomeňte si přečíst podrobnosti o stahování a splňovat všechny požadavky na systém, před instalací Windows Management Framework 4.0.

- [Nové funkce v prostředí Windows PowerShell](#new-features-in-windows-powershell-1)
- [Nové funkce ve Windows Powershellu integrovaném skriptovacím prostředí (ISE)](#new-features-in-windows-powershell-integrated-scripting-environment-ise)
- [Nové funkce v pracovním postupu Windows Powershellu](#new-features-in-windows-powershell-workflow)
- [Nové funkce ve Windows Powershellu webové služby](#new-features-in-windows-powershell-web-services)
- [Nové funkce ve Windows PowerShell Web Accessu](#new-features-in-windows-powershell-web-access)
- [Důležité opravy chyb ve Windows Powershellu 4.0](#notable-bug-fixes-in-windows-powershell-40)

Windows PowerShell 4.0 obsahuje následující nové funkce.

### <a name="new-features-in-windows-powershell"></a>Nové funkce v prostředí Windows PowerShell

- **Windows PowerShell Desired State Configuration** (DSC) je nový systém pro správu ve Windows PowerShell 4.0, která umožňuje nasazení a správu konfigurační data pro softwarových služeb a prostředí, ve kterém je spuštěný těchto služeb. Další informace o DSC najdete v tématu [začít pracovat s Windows PowerShell Desired State Configuration](https://technet.microsoft.com/library/c134aa32-b085-4656-9a89-955d8ff768d0).
- **Save-Help** teď umožňuje uložit nápovědy pro moduly, které jsou nainstalovány na vzdálených počítačích. Save-Help můžete použít ke stažení modulu nápovědy z klienta připojeného k Internetu (na kterém všechny moduly, pro které chcete zobrazit nápovědu je nutně nainstalováno) a potom zkopírujte uložené nápovědy k vzdálené sdílené složky nebo vzdáleném počítači, který nemá Internet přístup.
- Vylepšili jsme prostředí Windows PowerShell ladicí program pro povolení ladění pracovních postupů prostředí Windows PowerShell, jakož i skripty, které jsou spuštěny na vzdálených počítačích. Pracovní postupy prostředí Windows PowerShell se teď dají ladit na úrovni skriptu z příkazového řádku prostředí Windows PowerShell nebo Windows PowerShell ISE. Skripty prostředí Windows PowerShell, včetně skriptových pracovních postupech, se teď dají ladit přes vzdálené relace. Vzdálené ladění relace jsou zachovány prostřednictvím vzdálené relace prostředí Windows PowerShell, odpojí a znovu připojena později.
- A **RunNow** parametr pro **Register-ScheduledJob** a **Set-ScheduledJob** eliminuje nutnost nastavit okamžitou počáteční datum a čas pro úlohy s použitím **Aktivační událost** parametru.
- **Invoke-RestMethod** a **Invoke-WebRequest** teď můžete tak nastavit všechny hlavičky pomocí parametru záhlaví. I když tento parametr má vždy existoval, byl jeden z několika parametrů pro rutiny webových, jejímž výsledkem výjimek nebo chyby.
- **Get-Module** má nový parametr **FullyQualifiedName**, typu **ModuleSpecification\[]**. **FullyQualifiedName** parametr Get-Module teď umožňuje určit modulu s použitím modulů název, verzi a volitelně její identifikátor GUID.
- Výchozí nastavení zásady spouštění v systému Windows Server 2012 R2 je **RemoteSigned**. Na Windows 8.1 není žádná změna ve výchozím nastavení.
- Od verze Windows PowerShell 4.0, volání metody pomocí názvů dynamickou metodu, je podporována. Můžete použít proměnnou pro uložení názvu metody a dynamické vyvolání metody při volání proměnné.
- Úlohy asynchronního pracovního postupu se už smaže časový limit, která je určená **PSElapsedTimeoutSec** společný parametr pracovního postupu vypršel.
- Nový parametr **RepeatIndefinitely**, byl přidán do **New-JobTrigger** a **Set-JobTrigger** rutiny. Tím se eliminuje nutnost zadávání **hodnotu TimeSpan.MaxValue** hodnota **RepetitionDuration** parametr opakovaně spouštět plánované úlohy na dobu neurčitou.
- A **Passthru** parametr byl přidán do **Enable-JobTrigger** a **Disable-JobTrigger** rutiny. Parametr Passthru zobrazí všechny objekty, které jsou vytvořené nebo změněné ve svých rukou.
- Názvy parametrů pro zadání v pracovní skupině **Add-Computer** a **Remove-Computer** rutiny jsou konzistentní vzhledem k aplikacím. Obě rutiny teď použít parametr **Název_pracovní_skupiny**.
- Nové společný parametr **PipelineVariable**, byl přidán. PipelineVariable umožňuje uložit výsledky potrubím příkazu (nebo část potrubím příkaz) jako proměnnou, která mohou být předány až do kanálu.
- Filtrování pomocí syntaxe metody kolekce se teď podporuje. To znamená, že teď můžete filtrovat kolekce objektů s použitím zjednodušenou syntaxi, podobný tomu Where() nebo Where-Object, formátovaný jako volání metody. Tady je příklad: (Get-Process) .where ({$_. Název - odpovídají "powershell"})
- **Get-Process** rutina má nového přepínacího parametru **IncludeUserName**.
- Nová rutina **Get-FileHash**, který vrátí hodnotu hash souboru v jednom z několika formátů pro zadaný soubor, byl přidán.
- Ve Windows Powershellu 4.0, pokud modul používá **DefaultCommandPrefix** klíče v jeho manifestu, nebo pokud uživatel importuje modul s **předpony** parametr, **ExportedCommands**vlastnost modulu ukazuje příkazy v modulu s předponou. Při spuštění příkazu pomocí syntaxe kvalifikací modulu ModuleName\\CommandName, názvy příkazů musí obsahovat předponu.
- Hodnota **$PSVersionTable.PSVersion** byl aktualizován na 4.0.
- **Metody WHERE()** operátor chování změnilo. `Collection.Where('property -match name')` přijímá řetězcového výrazu ve formátu `"Property -CompareOperator Value"` už není podporovaná. Ale **Where()** operátor přijímá výrazy řetězec ve formátu scriptblock; to je podporováno.

### <a name="new-features-in-windows-powershell-integrated-scripting-environment-ise"></a>Nové funkce ve Windows Powershellu integrovaném skriptovacím prostředí (ISE)

- Windows PowerShell ISE podporuje ladění pracovního postupu prostředí Windows PowerShell i skript vzdáleného ladění.
- Byla přidána podpora technologie IntelliSense pro poskytovatele Windows PowerShell Desired State Configuration a konfigurace.

### <a name="new-features-in-windows-powershell-workflow"></a>Nové funkce v pracovním postupu Windows Powershellu

- Byla přidána podpora pro nový **PipelineVariable** společný parametr v kontextu iterativní kanály, jako jsou ty používané nástroje System Center Orchestrator; to znamená, kanály, která spustí příkazy, jednoduše zleva doprava, nikoli spolu s pomocí vysílání datového proudu.
- Vazby parametru je výrazně Vylepšená pracovat mimo kartu dokončení scénáře, jako například příkazy, které neexistují v aktuálním prostředí runspace.
- Byla přidána podpora pro vlastní kontejner aktivity do pracovního postupu prostředí Windows PowerShell. Pokud je parametr aktivity typů **aktivity**, **aktivity\[]**""nebo je obecná kolekce aktivity "a uživatel dodal blok skriptu jako argument, pak Windows Prostředí PowerShell Workflow převádí bloku skriptu pro XAML, stejně jako normální kompilace skriptu do pracovního postupu prostředí Windows PowerShell.
- Po selhání pracovní postup prostředí Windows PowerShell automaticky znovu připojí ke spravovaným uzlům.
- Teď můžete omezit **Foreach-Parallel** aktivity příkazy pomocí **ThrottleLimit** vlastnost.
- **ErrorAction** má novou platnou hodnotu společného parametru **pozastavit**, která je určená výhradně pro pracovní postupy.
- Koncový bod pracovního postupu teď automaticky zavře, pokud neexistují žádná aktivní relace, žádné probíhající úlohy a žádné čekající úlohy. Tato funkce šetří prostředky na počítači, který funguje jako server pracovního postupu při splnění podmínek pro automatické ukončení.

### <a name="new-features-in-windows-powershell-web-services"></a>Nové funkce ve Windows Powershellu webové služby

- Při výskytu chyby ve Windows Powershellu webové služby (PSWS, také nazývané OData IIS rozšíření pro správu), při spuštění je rutina, podrobné chybové zprávy jsou vráceny volajícímu. Kromě toho postupujte podle kódů chyb [pokyny pro REST API služby Windows Azure chyba kódu](https://msdn.microsoft.com/library/windowsazure/dd179357.aspx).
- Koncový bod lze nyní definovat verze rozhraní API, jakož i vynutit použití konkrétní verzi rozhraní API. Pokaždé, když se neshoduje verze, ke kterým dochází mezi klientem a serverem, se zobrazí chyby klienta i serveru.
- Správa schématu odeslání zjednodušenou topologickou pomocí automatického generování hodnoty pro všechny chybějící pole ve schématu. Generování dojde k jako počáteční bod užitečné i v případě, že schéma odeslání neexistuje.
- Vylepšili jsme zpracování v PSWS typ pro podporu typů, které používají jiný konstruktor než výchozí konstruktor, tímto chová podobně jako **PSTypeConverter** v prostředí Windows PowerShell. To vám umožní používat komplexní typy s PSWS.
- PSWS teď umožňuje rozbalením přidruženou instanci při spuštění dotazu. Pro větší binární obsah (jako jsou obrázky, zvuk nebo video) náklady na přenos je důležité a je vhodnější převést binární data bez kódování. PSWS používá datové proudy pojmenovaný prostředek pro přenos bez kódování. Datový proud s názvem prostředku je vlastností entity **Edm.Stream** typu. Každý datový proud prostředku s názvem má samostatné identifikátor URI pro operace GET nebo UPDATE.
- Akce OData teď poskytují mechanismus pro volání metod bez CRUD (vytváření, čtení, aktualizace a odstraňování) na prostředek. Vyvolat akci odesláním požadavku HTTP POST na identifikátor URI, který je definován pro akci. Parametry pro akce jsou definovány v textu požadavku POST.
- Pro zajištění konzistence s pokyny pro Windows Azure, je třeba zjednodušit všechny adresy URL. Změna součástí **klíč jako segmentu** umožňuje jednoho klíče je reprezentovaná jako segmenty. Všimněte si, že odkazy, které používají více hodnot klíče vyžadovat hodnot oddělených čárkami v kulatých závorek zápisu, stejně jako předtím.
- Než tato verze PSWS jen pro až po provedení vytvoření, aktualizace nebo odstranění operace byla k vyvolání Post, Put nebo odstranění prostředku nejvyšší úrovně. Nový v této verzi PSWS operace obsažených prostředků uživatelům umožňují dosáhnete stejných výsledků při dosažení stejného prostředku méně přímo blíží jakoby byly obsažené tyto prostředky.

### <a name="new-features-in-windows-powershell-web-access"></a>Nové funkce ve Windows PowerShell Web Accessu

- Můžete odpojit a znovu připojit k existující relace ve webové konzole Windows PowerShell Web Accessu. A **Uložit** tlačítka ve webové konzole umožňuje odpojení z relace, ale neodstraní ho a znovu připojit k relaci jiný čas.
- Výchozí parametry lze zobrazit na přihlašovací stránku. Pokud chcete zobrazit výchozí parametry, nakonfigurujte hodnoty pro všechna nastavení, zobrazí v **volitelná nastavení připojení** oblasti přihlašovací stránky v souboru s názvem **web.config**. Můžete použít **web.config** souboru nakonfigurujte všechny volitelná nastavení připojení s výjimkou druhý nebo alternativní sadu pověření.
- Ve Windows serveru 2012 R2 můžete vzdáleně spravovat autorizačních pravidel pro Windows PowerShell Web Accessu. **Add-PswaAuthorizationRule** a **Test-PswaAuthorizationRule** rutiny teď obsahují parametr Credential, který umožňuje správcům spravovat autorizační pravidla ze vzdáleného počítače nebo do Windows PowerShell Web Accessu relace.
- Nyní je možné mít více relací Windows PowerShell Web Access v jedné relace prohlížeče pomocí na nové kartě prohlížeče pro každou relaci. Už nemusíte otevřete novou relaci prohlížeče připojení k nové relaci ve webové konzole Windows Powershellu.

### <a name="notable-bug-fixes-in-windows-powershell-40"></a>Důležité opravy chyb ve Windows Powershellu 4.0

- **Get-Counter** můžete nyní vracet čítače, které obsahují znak apostrofu ve francouzské verzi Windows.
- Teď si můžete zobrazit **GetType** metodu na objekty deserializovat.
- **#Requires** příkazy teď uživatelům umožňují požadovat přístupová práva správce v případě potřeby.
- **Import Csv** rutina nyní ignoruje prázdné řádky.
- Problém, kdy používá Windows PowerShell ISE příliš mnoho paměti při spouštění **Invoke-WebRequest** příkazu byl opraven.
- **Get-Module** verze modulu v se teď zobrazují **verze** sloupce.
- Remove-Item - Recurse nyní odebere položky z podsložky podle očekávání.
- A **uživatelské jméno** byla přidána vlastnost **Get-Process** výstup objektů.
- **Invoke-RestMethod** rutina nyní vrátí všechny dostupné výsledky.
- **Přidat člena** nyní se projeví na zatřiďovací tabulky, i v případě, zatřiďovacích tabulkách dosud nebyly použity.
- **Select-Object - rozbalte** už selže nebo vygeneruje výjimku, pokud hodnota vlastnosti je null nebo prázdný.
- **Get-Process** je teď možné v rámci kanálu s jinými příkazy, které **ComputerName** vlastnost z objektů.
- **ConvertTo-Json** a **ConvertFrom-Json** teď může přijmout podmínky v rámci dvojité uvozovky a jeho chybové zprávy jsou nyní lokalizovatelné.
- **Get-Job** nyní vrátí všechny dokončit plánované úlohy, dokonce i v nové relace.
- Problémy s připojením a odpojení virtuální pevné disky s použitím **systému souborů** zprostředkovatele ve Windows PowerShell 4.0 byly vyřešeny. Je teď možné rozpoznat nové jednotky, kdy jsou připojené ve stejné relaci prostředí Windows PowerShell.
- Už nemusíte explicitně načítat **ScheduledJob** nebo **pracovního postupu** moduly pro práci s jejich typy úloh.
- Vylepšení výkonu se provedly importu pracovních postupů, které definují vnořené pracovní postupy; Tento proces je nyní rychlejší.

## <a name="new-features-in-windows-powershell-30"></a>Nové funkce ve Windows Powershellu 3.0

Windows PowerShell 3.0 obsahuje následující nové funkce.

- [Pracovní postup prostředí Windows PowerShell](#windows-powershell-workflow)
- [Windows PowerShell Web Accessu](#windows-powershell-web-access)
- [Nové funkce Windows PowerShell ISE](#new-windows-powershell-ise-features)
- [Podpora rozhraní Microsoft .NET Framework 4.0](#support-for-microsoft-net-framework-4)
- [Podpora pro prostředí Windows Preinstallation Environment](#support-for-windows-preinstallation-environment)
- [Odpojené relace](#disconnected-sessions)
- [Robustní relace připojení](#robust-session-connectivity)
- [Aktualizovatelné nápovědy systému](#updatable-help-system)
- [Vylepšené Online nápovědy](#enhanced-online-help)
- [Integrace CIM](#cim-integration)
- [Relace konfiguračních souborů](#session-configuration-files)
- [Naplánované úlohy a integrace Plánovač úloh](#scheduled-jobs-and-task-scheduler-integration)
- [Vylepšení Powershellu jazyka Windows](#windows-powershell-language-enhancements)
- [Nové rutiny Core](#new-core-cmdlets)
- [Vylepšení pro existující základních rutin a poskytovatele](#improvements-to-existing-core-cmdlets-and-providers)
- [Import modulu vzdálené a zjišťování](#remote-module-import-and-discovery)
- [Vylepšené Tab k dokončování příkazů](#enhanced-tab-completion)
- [Automatické načítání modulů](#module-auto-loading)
- [Vylepšení uživatelského prostředí modulu](#module-experience-improvements)
- [Zjednodušené příkaz zjišťování](#simplified-command-discovery)
- [Zdokonalené funkce protokolování diagnostiky a podpora zásad skupiny](#improved-logging-diagnostics-and-group-policy-support)
- [Formátování a vylepšení výstupu](#formatting-and-output-improvements)
- [Rozšířené konzole hostitele zkušenost](#enhanced-console-host-experience)
- [Nová rutina a rozhraní API pro hostování](#new-cmdlet-and-hosting-apis)
- [Vylepšení výkonu](#performance-improvements)
- [Spustit jako a podporu sdílené hostitele](#runas-and-shared-host-support)
- [Zlepšení zpracování speciální znak](#special-character-handling-improvements)

### <a name="windows-powershell-workflow"></a>Pracovní postup prostředí Windows PowerShell

Pracovní postup prostředí Windows PowerShell přináší výkon Windows Workflow Foundation do prostředí Windows PowerShell. Můžete napsat pracovních postupů v XAML nebo v jazyce prostředí Windows PowerShell a spusťte je stejně, jako by spuštění rutiny. [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) rutina načte workflw příkazy a [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) rutiny vyvolání nápovědy pro pracovní postupy.

Pracovní postupy jsou sekvence multicomputer správy aktivit, které jsou dlouhotrvající, opakovatelných, časté, paralelizovat, přerušitelné, suspendable a dá se restartovat. Pracovní postupy lze obnovit z úmyslnému i náhodnému přerušení, jako je výpadek sítě, restartování Windows nebo přerušení napájení.

Pracovní postupy jsou také přenositelné; může být exportovat jako nebo importovat ze souborů XAML. Můžete napsat vlastních konfigurací relací, které umožňují pracovní postupy nebo aktivity v pracovním postupu spustit delegovanou nebo podřízené uživatelé.

Následují výhody pracovního postupu prostředí Windows PowerShell

- Automatizace sekvencované, dlouhotrvajících úloh.
- **Vzdálené sledování dlouho běžících úloh**. Stav a průběh činností jsou viditelné v každém okamžiku.
- **Multicomputer správy.** Souběžně spouštět úlohy jako pracovní postupy na stovky spravovaných uzlů. Pracovní postup prostředí Windows PowerShell obsahuje integrované knihovnu společné parametry správy, například **PSComputerName**, která umožňuje takové scénáře správy více počítačů.
- **Provedení jednoho úkolu komplexní procesy.** Můžete kombinovat související skripty, které implementují celý scénář začátku do konce do jednoho pracovního postupu.
- **Trvalost.** : pracovní postup je uložit (nebo kontrola ukazuje) v určitých bodech, které jsou definované autorem tak můžete obnovit od posledního trvalého úlohu (nebo kontrolního bodu), místo restartování pracovní postup od začátku.
- **Odolnosti.** Automatizované zotavení po chybě. Pracovní postupy fungují po plánované a neplánované restartování. Můžete pozastavit provádění pracovního postupu a potom obnovit od posledního trvalého bodu. Autoři pracovního postupu můžete určit konkrétní aktivity k opětovné použití v případě selhání na jeden nebo víc spravovaných uzlech.
- **Možnost odpojit, znovu připojit a spusťte v odpojeném relace.** Uživatelé se můžete připojit a odpojit od serveru pracovního postupu, ale pracovní postup běží nepřetržitě. Můžete odhlaste se z klientského počítače nebo restartujte klientský počítač a sledujte provádění pracovního postupu z jiného počítače bez přerušení pracovního postupu.
- **Plánování.** Úkoly pracovního postupu můžete naplánovat stejně jako všechny rutiny prostředí Windows PowerShell nebo skriptu.
- **Pracovní postup a omezení připojení.** Spuštění pracovního postupu a připojení k uzlům, můžu omezit, což umožní scénáře škálovatelnost a vysokou dostupnost.

### <a name="windows-powershell-web-access"></a>Windows PowerShell Web Access

Windows PowerShell Web Accessu je funkce systému Windows Server 2012, která umožňuje uživatelům spouštět příkazy prostředí Windows PowerShell a skriptů ve webové konzole. Zařízení, která používají webové konzoly, aby prostředí Windows PowerShell, software pro vzdálenou správu nebo instalace modulu plug-in prohlížeče. Vyžaduje se Windows PowerShell Web Accessu brána správně nakonfigurovaná a prohlížeč v klientském zařízení, která podporuje JavaScript a přijímá soubory cookie.

Další informace najdete v tématu [nasadit Windows PowerShell Web Accessu](https://go.microsoft.com/fwlink/p/?LinkID=221050).

### <a name="new-windows-powershell-ise-features"></a>Nové funkce Windows PowerShell ISE

Pro Windows PowerShell 3.0, Windows PowerShell integrovaném skriptovacím prostředí (ISE) má mnoho nových funkcí, včetně IntelliSense, zobrazit příkazové okno, jednotné podokně konzoly, fragmenty kódu, závorky, Rozbalit / sbalit oddíly, automatické ukládání, nedávné položky seznam, bohaté možnosti kopírovat, blokovat kopírování a plná podpora pro psaní pracovní postupy skriptů prostředí Windows PowerShell. Další informace najdete v tématu [about_Windows_PowerShell_ISE [verze 3]](https://technet.microsoft.com/library/dfa54d47-60c6-4fff-8197-c747e8d411bb).

### <a name="support-for-microsoft-net-framework-4"></a>Podpora rozhraní Microsoft .NET Framework 4

Prostředí Windows PowerShell je sestaveno s Common 4.0 modulu Runtime jazyka. Rutiny, skripty a autoři pracovního postupu můžete použít nové třídy rozhraní Microsoft .NET Framework 4 v prostředí Windows PowerShell s funkcemi, které patří kompatibilitě aplikací a nasazení, Managed Extensibility Framework, paralelní výpočty, sítě, Windows Communication Foundation a Windows Workflow Foundation.

### <a name="support-for-windows-preinstallation-environment"></a>Podpora pro prostředí Windows Preinstallation Environment

Windows PowerShell 3.0 je volitelná součást Windows Preinstallation Environment (Windows PE) 4.0, Windows 8. Prostředí Windows PE je minimální operační systém, který se spustí počítač, který nemá žádný operační systém a připraví ho k instalaci Windows. Prostředí Windows PE můžete použít k oddílu a formátování pevných disků, zkopírujte imagí disků do počítače a zahájení instalace Windows ze síťové sdílené složky. Windows PowerShell 3.0 je možné v prostředí Windows PE pro správu nasazení, Diagnostika a scénáře obnovení.

### <a name="disconnected-sessions"></a>Odpojené relace

Počínaje Windows PowerShell 3.0, trvalé spravovaného uživatele relací ("PSSessions"), které vytvoříte pomocí rutiny New-PSSession se uloží ve vzdáleném počítači. Už nejsou závislé na relace, ve kterém byly vytvořeny.

Teď v relaci můžete odpojit bez narušení běžného příkazy, které jsou spuštěny v relaci. Můžete zavřít relaci a vypnout počítač. Později se můžete připojit k relaci z jiné relaci na stejném nebo na jiném počítači.

**ComputerName** parametr [Get-PSSession](https://technet.microsoft.com/library/b2b10531-d0df-4746-b877-e75c09955cb6) rutina nyní získá všech relací uživatele, které připojení k počítači, i v případě, že byly spuštěny v jiné relaci v jiném počítači. Můžete připojit na relace, získat výsledky příkazů, spusťte nové příkazy a pak odpojení z relace.

Byly přidány nové rutiny pro podporu funkcí odpojí relace včetně [Disconnect-PSSession](https://technet.microsoft.com/library/f8f95111-612f-4cba-9098-77904b0473d8), [Connect-PSSession](https://technet.microsoft.com/library/b803dd29-f208-4079-80d4-db04d778f060), a Receive-PSSession a nové parametry byly přidány do rutiny, které Správa PSSessions, například **InDisconnectedSession** parametr [Invoke-Command](https://technet.microsoft.com/library/906b4b41-7da8-4330-9363-e7164e5e6970) rutiny.

Funkce odpojí relace je podporována pouze v případě, že počítače v obou pocházející ("client") a ukončení ("server") koncích připojení se systémem Windows PowerShell 3.0.

### <a name="robust-session-connectivity"></a>Robustní relace připojení

Windows PowerShell 3.0 zjistí neočekávané ztráty připojení mezi klientem a serverem a pokusí se znovu vytvořit připojení a spuštění automaticky pokračovat. Pokud v přiděleném čase nelze znovu navázat připojení klient server, bude informován uživatel a relace se odpojí. Při pokusu o opakované připojení k prostředí Windows PowerShell poskytuje nepřetržitou zpětnou vazbu pro uživatele.

Pokud odpojené relaci byl spuštěn s použitím invokecommand –, prostředí Windows PowerShell vytvoří úlohu pro odpojené relaci, aby bylo snazší znovu připojit a pokračovat v provádění.

Tyto funkce poskytují spolehlivé a obnovitelnost dokonalejší prostředí a umožňují uživatelům provádět dlouho běžících úloh, které vyžadují robustní relace, jako jsou pracovní postupy.

### <a name="updatable-help-system"></a>Aktualizovatelné nápovědy systému

Teď si můžete stáhnout soubory aktualizace nápovědy pro rutiny v modulech. [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) rutiny identifikuje nejnovější soubory nápovědy, stáhne z Internetu, rozbalí je, ověřuje je a nainstaluje je do správného adresáře konkrétní jazyk pro modul.

Pokud chcete použít soubory aktualizované nápovědy, stačí zadat `Get-Help`. Není nutné restartovat Windows nebo prostředí Windows PowerShell. Abyste mohli aktualizovat nápovědu pro moduly v adresáři $pshome, spusťte prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".

Pro podporu uživatelů, kteří nemají přístup k Internetu a uživatelů za firewally, nové [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) rutiny stáhne soubory nápovědy na adresář systému souborů, jako jsou sdílené složky. Uživatelé pak můžou použít [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) rutiny pro získání nápovědy aktualizované soubory ze sdílené složky.

Můžete použít [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) rutiny, abyste mohli aktualizovat nápovědu soubory pro všechny nebo uživatelské rozhraní nepodporuje konkrétní moduly ve všech jazykových verzí. Dokonce můžete umístit [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) příkaz ve vašem profilu Windows Powershellu. Ve výchozím nastavení prostředí Windows PowerShell stáhne soubory nápovědy pro modul více než jednou denně.

Moduly Windows 8 a Windows Server 2012 neobsahují soubory nápovědy. Chcete-li stáhnout nejnovější soubory nápovědy, zadejte `Update-Help`. Další informace získáte zadáním `Get-Help` (bez parametrů) nebo se podívejte [about_Updatable_Help](https://technet.microsoft.com/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe).

Pokud soubory nápovědy pro rutinu nejsou nainstalovaní v počítači, [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) rutina nyní zobrazí automaticky generované nápovědy. Automaticky generované Nápověda obsahuje syntaxi příkazů a pokyny k používání [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) rutina ke stahování souborů nápovědy.

Žádné Autor modulu může podporovat aktualizovatelné nápovědy pro jejich modulu. Můžete zahrnout soubory nápovědy v modulu a pomocí aktualizovatelné nápovědy je aktualizovat nebo přitom vynechat ty soubory nápovědy a používat aktualizovatelné nápovědy k instalaci. Další informace o podpoře aktualizovatelné nápovědy najdete v tématu [podpora aktualizovatelné nápovědy](https://go.microsoft.com/FWLink/?LinkID=242129) na webu MSDN.

### <a name="enhanced-online-help"></a>Vylepšené Online nápovědy

Online nápověda prostředí Windows PowerShell je cenný materiál pro všechny uživatele, ale je obzvláště důležité pro uživatele, kteří nepodporují nebo nelze nainstalovat soubory aktualizace nápovědy.

Pokud chcete získat online nápovědu pro všechny rutiny prostředí Windows PowerShell, zadejte:

```
Get-Help <cmdlet-name> -Online
```

Prostředí Windows PowerShell se online verzi tématu nápovědy otevře ve výchozím internetovém prohlížeči.

**Get-Help-Online** funkce ve Windows Powershellu 3.0 je teď ještě výkonnější vzhledem k tomu, že to funguje, i když soubory nápovědy pro rutinu nejsou v počítači nainstalována. **Get-Help-Online** funkce získá identifikátor URI pro online téma nápovědy z vlastnosti HelpUri rutiny a pokročilých funkcí.

```
PS C:\>(Get-Command Get-ScheduledJob).HelpUri
http://go.microsoft.com/fwlink/?LinkID=223923
```

Počínaje Windows Powershellu 3.0 se autoři C# rutiny můžete naplnit **HelpUri** vlastnost tak, že vytvoříte **HelpUri** atribut ve třídě rutiny. Můžete definovat autoři pokročilé funkce **HelpUri** vlastnost **CmdletBinding** atribut. Hodnota **HelpUri** vlastnosti musí začínat řetězcem "http" nebo "https".

Můžete použít také **HelpUri** hodnoty v první související odkaz k souboru nápovědy rutiny založené na XML nebo. Direktiva odkazu založená na komentářích nápovědy ve funkci.

Další informace o podpoře online nápovědy najdete v tématu [podpora Online nápovědy](https://go.microsoft.com/fwlink/?LinkId=242132) na webu MSDN.

### <a name="cim-integration"></a>Integrace CIM

Windows PowerShell 3.0 obsahuje podporu pro CIM Common Information Model (), který poskytuje společné definice spravovaných informací pro systémy, sítě, aplikace a služby, povolením výměny informací správy mezi heterogenní systémy. Podpora pro CIM ve Windows Powershellu 3.0, včetně schopnosti vytváření rutiny Windows Powershellu založené na nové nebo existující třídy modelu CIM, příkazy na základě rutiny definice soubory XML, podporu pro rozhraní .NET Framework CIM. Rozhraní API, rutin modelu CIM správy a poskytovatele služby WMI 2.0.

### <a name="session-configuration-files"></a>Relace konfiguračních souborů

Počínaje Windows PowerShell 3.0, můžete navrhnout vlastní konfiguraci relace s použitím souboru. Konfigurační soubor nová relace vám umožní určit prostředí relace, které používají konfiguraci relace, které moduly skriptů, včetně a soubory ve formátu se načtou do relací, kteří uživatelé rutiny a jazykové prvky můžete použít, které moduly a skripty můžete spustit a které proměnné můžete zobrazit.

Můžete navrhnout relace, ve které uživatelé můžou jenom spouštět rutiny z jednoho konkrétního modulu nebo relace, ve kterém uživatelé mají úplný jazyk, přístup k všechny moduly a přístup k skripty, které provádět pokročilé úlohy.

V předchozích verzích Windows Powershellu, byl k dispozici pouze pro ty, kteří mohou zapsat ovládací prvek na této úrovni C# komplexní objem požadovaný při spuštění skriptu nebo programu. Každý člen skupiny Administrators na počítači, můžete přizpůsobit konfiguraci relace pomocí konfiguračního souboru.

Chcete-li vytvořit soubor konfigurace relace, použijte [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866) rutiny. Chcete-li použít konfigurační soubor pro relaci ke konfiguraci relace, použijte [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) nebo [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) rutiny.

Další informace najdete v tématu [about_Session_Configuration_Files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configuration_files?view=powershell-5.0) a [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866).

### <a name="scheduled-jobs-and-task-scheduler-integration"></a>Naplánované úlohy a integrace Plánovač úloh

Teď můžete naplánovat úlohy na pozadí prostředí Windows PowerShell a spravovat je v prostředí Windows PowerShell a v Plánovači úloh.

Prostředí Windows PowerShell naplánované úlohy jsou užitečné hybridní úlohy na pozadí prostředí Windows PowerShell a úkolů plánovače úloh.

Stejně jako úlohy na pozadí prostředí Windows PowerShell naplánované úlohy asynchronně spustí na pozadí. Instance plánované úlohy, které byly dokončeny lze spravovat pomocí rutin úlohy, jako například [Start-Job](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442) a [Get-Job](https://technet.microsoft.com/library/1352c534-7193-46ca-9ab1-0c5219a661ad).

Stejně jako úkoly plánovače úloh můžete spustit plánované úlohy podle plánu jednorázové nebo opakované nebo v reakci na akce nebo události. Můžete zobrazit a spravovat plánovaných úloh v Plánovači úloh, povolit a zakázat podle potřeby, spouštět nebo použít jako šablony a nastavit podmínky, za kterých se zahájením úloh.

Naplánované úlohy navíc obsahuje vlastní sadu rutin pro jejich správu. Rutiny umožňují vytvářet, upravovat, spravovat, zakázat a znovu povolit naplánované úlohy, vytvoření naplánované úlohy aktivačních událostí a nastavit možnosti naplánované úlohy.

Další informace o plánovaných úlohách najdete v tématu [about_Scheduled_Jobs](https://technet.microsoft.com/library/3b546629-703c-4939-b44f-52dd567bce92).

### <a name="windows-powershell-language-enhancements"></a>Vylepšení Powershellu jazyka Windows

Windows PowerShell 3.0 obsahuje řadu funkcí, které jsou navržené tak, aby jeho jazyk jednodušší, snazší používat a vyhnout se běžných chyb. Mezi vylepšení patří vlastnosti, výčtu, počet a délku vlastnosti na skalární objekty, nové operátory přesměrování, modifikátor oboru $Using, formátování PSItem automatické proměnné a flexibilní skriptu, atributy proměnných, zjednodušené atribut argumenty, názvů číselné příkazů, Stop analýza operátor, vylepšené pole seskupování, nové bitové operátory, seřazený slovníky, PSCustomObject přetypování a vylepšené Nápověda založená na komentářích.

### <a name="new-core-cmdlets"></a>Nové rutiny Core

Nové rutiny byly přidány do instalace jádra Windows Powershellu, včetně rutiny pro správu naplánované úlohy, odpojené relaci, integrace CIM a aktualizovatelné nápovědy.

|||
|-|-|
|Přidat JobTrigger|Nový JobTrigger|
|Connect-PSSession|Nové PSSessionConfigurationFile|
|ConvertFrom-Json|New-PSTransportOption|
|ConvertTo-Json|Nové PSWorkflowExecutionOption|
|Disable-JobTrigger|Nové PSWorkflowSession|
|Disable-ScheduledJob|Nové ScheduledJobOption|
|Odpojit relace PSSession|Nový WinEvent|
|Enable-JobTrigger|Zobrazí PSSession|
|Enable-ScheduledJob|Register-CimIndicationEvent|
|Get-CimAssociatedInstance|Register-ScheduledJob|
|Get-CimClass|Remove-CimInstance|
|Get-CimInstance|Remove-CimSession|
|Get-CimSession|Odebrat TypeData|
|Get-ControlPanelItem|Rename-Computer|
|Get-IseSnippet|Resume-Job|
|Get-JobTrigger|Save-Help|
|Get-ScheduledJob|Set-CimInstance|
|Get-ScheduledJobOption|Set-JobTrigger|
|Get-TypeData|Set-ScheduledJob|
|Import IseSnippet|Set-ScheduledJobOption|
|Vyvolání AsWorkflow|Show-– příkaz|
|Invoke CimMethod|Show ControlPanelItem|
|Vyvolání RestMethod|Pozastavit úlohu|
|Invoke-WebRequest|Test-PSSessionConfigurationFile|
|Nový CimInstance|Blokování souborů|
|Nový CimSession|Unregister-ScheduledJob|
|Nové CimSessionOption|Update-Help|
|Nové IseSnippet||

### <a name="improvements-to-existing-core-cmdlets-and-providerswindows-powershell-30-includes-new-features-for-existing-cmdlets-including-the-simplified-syntax-and-new-parameters-for-the-following-cmdlets-computer-cmdlets-csv-cmdlets-get-childitem-get-command-get-content-get-history-measure-object-security-cmdlets-select-object-select-string-split-path-start-process-tee-object-test-connection-add-member-and-wmi-cmdlets"></a>Vylepšení existujících základních rutin a ProvidersWindows prostředí PowerShell 3.0 obsahuje nové funkce pro existující rutiny včetně zjednodušenou syntaxi a nové parametry pro následující rutiny: rutiny počítače, CSV rutin Get-ChildItem, Get-Command, Get-Content, Get-historie, míru-Object, rutiny zabezpečení Select-Object, String vyberte, Split-Path, spustit proces Tee-Object, Test-Connection, přidat člena a rutiny WMI.

Poskytovatelé Windows Powershellu se také k významnému vylepšení včetně podpory poskytovatel certifikátu pro správu certifikátů vrstvy SSL (Secure Socket) pro hostování webů, credential nebo trvalé síťové jednotky a alternativní datové proudy v jednotky systému souborů.

### <a name="remote-module-import-and-discovery"></a>Import modulu vzdálené a zjišťování

Windows PowerShell 3.0 rozšiřuje modulu zjišťování, importování a možnosti implicitní vzdálené komunikace na vzdálených počítačích. Rutiny modulu získání modulů na vzdálených počítačích a naimportujte moduly do vzdáleného nebo místního počítače pomocí vzdálené komunikace Windows Powershellu. Nová podpora relaci CIM můžete použít model CIM a WMI ke správě počítačů bez Windows importováním příkazy do místního počítače, která implicitně spustí ve vzdáleném počítači.

Další informace najdete v tématech nápovědy pro [Get-Module](https://technet.microsoft.com/library/2cccd4c4-9a21-4c77-b691-984ee57242e1) a [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) rutiny.

### <a name="enhanced-tab-completion"></a>Vylepšené Tab k dokončování příkazů

Dokončování pomocí tabulátoru v konzole Windows Powershellu teď dokončí názvy rutin, parametry, hodnoty parametrů, výčtů, rozhraní .NET Framework typy, COM objekty, skrytých složek a informace. Funkci doplňování karta je kompletně přepsaná založené na strom abstraktní syntaxe pro podporu více scénářů, včetně stromů analýzy v paměti a středovou tab k dokončování příkazů a nový analyzátor.

### <a name="module-auto-loading"></a>Automatické načítání modulů

[Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) rutina nyní získá všechny rutiny a funkce ze všech modulů, které jsou nainstalovány v počítači, i když v modulu není importován do aktuální relace.

Když se zobrazí rutiny, které potřebujete, můžete ho okamžitě bez importu všech modulů. Moduly Windows Powershellu jsou nyní automaticky importován při použít všechny rutiny v modulu. Už nepotřebujete a vyhledejte modul a importovat, a použít jeho rutinu.

Automatické import modulů se aktivuje pomocí rutiny v příkazu, spuštěná **Get-Command** pro rutinu bez zástupných znaků nebo spuštění [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) pro rutinu bez zástupných znaků.

Můžete povolit, zakázat a nakonfigurovat automatické import modulů pomocí **$PSModuleAutoLoadingPreference** preferenční proměnné.

Další informace najdete v tématu [týkajícím se modulů](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_modules?view=powershell-5.0), [about_Preference_Variables [v4]](https://technet.microsoft.com/library/31344314-be29-4286-b039-afa5460cbe8b)a témata nápovědy [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) a [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) rutiny.

### <a name="module-experience-improvements"></a>Vylepšení uživatelského prostředí modulu

Windows PowerShell 3.0 přináší podporu pokročilých funkcí pro moduly, včetně následující nové funkce.

1. Modul protokolování pro jednotlivé moduly (LogPipelineExecutionDetails) a nové nastavení zásad skupiny "Zapnout na modul protokolování"
2. Rozšířených objektů modulu, které vystavují hodnoty z manifestu modulu
3. Nové **ExportedCommands** vnořené vlastnosti modulů, včetně modulů, které kombinuje příkazy všech typů
4. Vylepšené zjišťování modulů k dispozici (zrušení importovaných), včetně, což **cesta** a **ListAvailable** parametry v jednom příkazu
5. Nové **DefaultCommandPrefix** klíče v modulu manifestů, které zabrání konfliktům název beze změny kódu modulu.
6. Vylepšené modulu požadavky, včetně plně kvalifikovaný požadované moduly s verzí a identifikátor GUID a automatického importu požadované moduly.
7. Náročném, efektivní fungování [New-ModuleManifest](https://technet.microsoft.com/library/512adced-f42f-4e88-ba7c-834fc9e5d047) rutiny.
8. Nové **modulu** parametr pro #Requires
9. Vylepšené [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) rutiny s oběma **MinimumVersion** a **RequiredVersion** parametry.

### <a name="simplified-command-discovery"></a>Zjednodušené příkaz zjišťování

Už nepotřebujete naimportujte všechny moduly ke zjištění příkazy, které jsou k dispozici do relace. Ve Windows Powershellu 3.0 [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) rutina načte všechny příkazy ze všech nainstalovaných modulů. A pokud použijete příkaz, je automaticky naimportován do relace modul, který exportuje příkazu.

Nové [zobrazit příkaz](https://technet.microsoft.com/library/65bba50b-91a8-49d5-80a2-a30fc684ba41) rutiny určené speciálně pro začátečníky. Můžete hledat příkazy v okně. Můžete zobrazit všechny příkazy nebo filtrovat podle modulu, importovat modul klepnutím na tlačítko, textová pole a rozevírací seznamy můžete vytvořit platný příkaz a potom zkopírujte nebo spusťte příkaz bez opuštění okna.

### <a name="improved-logging-diagnostics-and-group-policy-support"></a>Zdokonalené funkce protokolování diagnostiky a podpora zásad skupiny

Windows PowerShell 3.0 zlepšuje protokolování a trasování podpory pro příkazy a modulů s podporou pro trasování událostí v protokolech trasování událostí pro Windows (Windows), upravitelné **LogPipelineExecutionDetails** vlastnost modulů a "zapnout v modulu Skupina položky protokolování"nastavení zásad. Nyní můžete z protokolu podrobnosti zobrazením vlastností protokolu získat hodnoty parametrů.

### <a name="formatting-and-output-improvements"></a>Formátování a vylepšení výstupu

Nové formátování a výstup vylepšení zvýšit efektivitu všech uživatelů, prostředí Windows PowerShell. Mezi vylepšení patří výstupní přesměrování pro všechny datové proudy, rozšířené rutiny Update-Type, která přidá typy dynamicky bez Format.ps1xml souborů, zalamování řádků ve výstupu, výchozí vlastnosti formátování vlastních objektů, **PSCustomObject** text, vylepšené formátování objektů WMI heterogenní objekty a podporu pro zjišťování přetížení metody.

### <a name="enhanced-console-host-experience"></a>Rozšířené konzole hostitele zkušenost

Hostitelského programu konzoly prostředí Windows PowerShell obsahuje nové funkce ve Windows Powershellu 3.0 včetně jednovláknový objekt apartment ve výchozím nastavení. Nová možnost "Spustit s PowerShell" v Průzkumníku souborů umožňuje spouštět skripty v relaci neomezený právě kliknutím pravým tlačítkem myši. Nové konzoly hostitele spuštění logiky spouští rychleji prostředí Windows PowerShell a nová písma umožňují přizpůsobit okno prostředí známých konzoly.

Další informace najdete v tématu [about_Run_With_PowerShell](https://technet.microsoft.com/library/c9d9ca5f-eff9-4409-be9d-e43b5b4087eb).

### <a name="new-cmdlet-and-hosting-apis"></a>Nová rutina a rozhraní API pro hostování

Nové rutiny API a rozhraní API hostování zahrnují strom veřejné pokročilé syntaxe (AST) rozhraní API a rozhraní API pro kanál stránkování, vnořené kanály, prostředí runspace fondy tab k dokončování příkazů, Windows RT, atribut zastaralé rutiny a sloveso a podstatné jméno vlastnosti objektu FunctionInfo.

### <a name="performance-improvements"></a>Vylepšení výkonu

Výrazné zlepšení výkonu ve Windows Powershellu pocházejí z nový analyzátor jazyka, které je postavené na dynamický modul Runtime jazyka (DLR) v rozhraní .NET Framework 4. společně s runtime kompilace skriptu, vylepšení spolehlivosti modulu a změny algoritmus [Get-ChildItem](https://technet.microsoft.com/library/75cf79bb-4db6-4a67-8c36-3d20754e2190) , který vylepšit výkon, zejména v případě, že hledání síťové sdílené složky.

### <a name="runas-and-shared-host-support"></a>Spustit jako a podporu sdílené hostitele

Windows PowerShell 3.0 obsahuje podporu pro funkce RunAs a sdílené hostitele.

*RunAs* funkce, navržená pro pracovního postupu Windows Powershellu, umožňuje uživatelům konfiguraci relace, vytváření relací, které běží s oprávněním sdíleného uživatelského účtu. Díky tomu méně privilegovaným uživatelům spouštět určité příkazy a skripty s oprávněními správce a snižuje nutnost přidávání méně vedoucí uživatelů do skupiny Administrators.

**SharedHost** funkce umožňuje více uživatelům ve více počítačích pro připojení k relaci workflowu souběžně a sledovat průběh pracovního postupu. Uživatelé můžou spouštět pracovní postup na jednom počítači a připojte se k relaci workflowu na jiném počítači bez odpojení relace z původního počítače. Uživatelé musí mít stejná oprávnění a používat stejné konfiguraci relace. Další informace najdete v tématu "Spuštěná Windows pracovního postupu Powershellu" v části Začínáme s pracovním postupem prostředí Windows PowerShell.

### <a name="special-character-handling-improvements"></a>Zlepšení zpracování speciální znak

Zlepšit schopnost Windows PowerShell 3.0, jak interpretovat a zpracovat správně speciální znaky, **LiteralPath** parametr, který zpracovává speciální znaky v cestách, je platný pro téměř všechny rutiny, které mají  **Cesta** parametr, včetně nového [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) a [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) rutiny. Analyzátor také zahrnuje zvláštní logiku ke zlepšení zpracování prvními znaku (\`) a hranaté závorky v názvech souborů a cesty.

## <a name="see-also"></a>Viz také

- [about_Windows_PowerShell_5.0](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_windows_powershell_5.0?view=powershell-5.0)
- [Prostředí Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
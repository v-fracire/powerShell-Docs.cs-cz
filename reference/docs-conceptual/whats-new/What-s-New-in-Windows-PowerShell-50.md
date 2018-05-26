---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Co je nového v prostředí Windows PowerShell 5.0
ms.openlocfilehash: f5a27c0541e21b379f88b318cbe09a0344c1b372
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/25/2018
---
# <a name="whats-new-in-windows-powershell-50"></a>Co je nového v prostředí Windows PowerShell 5.0
Prostředí Windows PowerShell 5.0 obsahuje důležité nové funkce, které rozšiřují jeho použití, zlepšují použitelnost a umožňují řídit a spravovat prostředí ve Windows snadněji a komplexněji.

Prostředí Windows PowerShell 5.0 je zpětně kompatibilní. Rutiny, zprostředkovatelé, moduly, moduly snap in, skripty, funkce a profily, které byly navrženy pro prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 2.0 obecně fungovat bez změny v prostředí Windows PowerShell 5.0.

# <a name="installing-windows-powershell"></a>Instalace Windows PowerShellu
Prostředí Windows PowerShell 5.0 je nainstalována ve výchozím nastavení v systému Windows Server 2016 Technical Preview a Windows 10.

Chcete-li nainstalovat prostředí Windows PowerShell 5.0 na Windows Server 2012 R2, Windows 8.1 Enterprise nebo Windows 8.1 Pro, stáhněte a nainstalujte [Windows Management Framework 5.0](http://aka.ms/wmf5download). Nezapomeňte přečíst podrobnosti o stažení a před instalací Windows Management Framework 5.0 splňují všechny požadavky na systém.

## <a name="in-this-topic"></a>V tomto tématu

- [Aktualizace Windows PowerShell 4.0 DSC v KB 3000850](#windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850)
- [Nové funkce v prostředí Windows PowerShell 5.0](#new-features-in-windows-powershell-50)
- [Nové funkce v prostředí Windows PowerShell 4.0](#new-features-in-windows-powershell-40)
- [Nové funkce v prostředí Windows PowerShell 3.0](#new-features-in-windows-powershell-30)

## <a name="windows-powershell-40-updates-in-november-2014-update-rollup-kb-3000850"></a>Prostředí Windows PowerShell 4.0 aktualizace v listopadu 2014 kumulativní (KB 3000850)
Mnoho aktualizací a vylepšení pro Windows PowerShell požadovaného stavu konfigurace (DSC) v prostředí Windows PowerShell 4.0 je k dispozici v [kumulativní aktualizace pro Windows RT 8.1, Windows 8.1 a Windows Server 2012 R2 z listopadu 2014](https://support.microsoft.com/kb/3000850/) (KB 3000850 ). Můžete určit, zda KB 3000850 je nainstalován v systému spuštěním `Get-Hotfix -Id KB3000850` v prostředí Windows PowerShell.

- Aktualizace stávající rutiny ve [PSDesiredStateConfiguration](https://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modulu

    -   [Get-DscResource](http://technet.microsoft.com/library/dn521625.aspx) je rychlejší (zejména v ISE).

    -   [Spuštění DscConfiguration](http://technet.microsoft.com/library/dn521623.aspx) má nový parametr - UseExisting, který znovu použije poslední použité konfigurace.

    -   [Spuštění DscConfiguration](http://technet.microsoft.com/library/dn521623.aspx) -Force byl opraven.

    -   [Get-DscLocalConfigurationManager](http://technet.microsoft.com/library/dn407378.aspx) zobrazí další užitečné informace o stav modulu.

    -   [Test DscConfiguration](http://technet.microsoft.com/library/dn407382.aspx) nyní vrátí název počítače společně s hodnotu True nebo False.

    -   [Nové DscChecksum](http://technet.microsoft.com/library/dn521622.aspx) teď podporuje cesty UNC.

- Nové rutiny v [PSDesiredStateConfiguration](http://technet.microsoft.com/library/dn391651(v=wps.640).aspx) modulu

    -   [Aktualizace DscConfiguration](http://technet.microsoft.com/library/mt143541(v=wps.630).aspx): server zkontroluje vyžádání obsahu na vyžádání.

    -   [Stop-DscConfiguration](http://technet.microsoft.com/library/mt143542(v=wps.630).aspx): zastaví konfigurace, která je již spuštěna.

    -   [Odebrat DscConfigurationDocument](http://technet.microsoft.com/library/mt143544(v=wps.630).aspx): vám umožní odebrat konfiguraci dokumenty v různých fázích (čekající na vyřízení, předchozí nebo aktuální).

- Vylepšení jazyk

    -   DependsOn teď podporuje složené prostředky.

    -   DependsOn teď podporuje čísla v názvech zdrojů instance.

    -   Uzel výrazy, které už vyhodnoceny na prázdnou throw chyby.

    -   Byl opraven chybu, ke kterému dochází, pokud uzel výraz vyhodnocen jako prázdný.

    -   Konfigurace volání konfigurace nyní fungovat v konzole Windows PowerShell.

- Vylepšení režimu pro vyžádání obsahu

    -   Režim přijetí změn teď podporuje všechny soubory ZIP.

    -   **AllowModuleOverwrite** nyní pracuje správně.

- Vylepšení odolnost proti chybám

    -   Nové **režim DebugMode** umožňuje znovu načíst moduly prostředků.

    -   Pokud dojde k selhání konfigurace, není soubor pending.mof odstraněn.

    -   Místní Configuration Manager (LCM) je nyní pružnější při nastavení metakonfiguraci mohlo dojít k poškození.

- Vylepšení diagnostiky

    -   Když LCM nastaví časovač na různá nastavení, než jste zadali, zobrazí se upozornění.

    -   Soubory protokolu chyb nyní obsahují zásobníku volání pro prostředí Windows PowerShell prostředky.

- Vylepšení flexibilitu

    -   Prostředek LocalConfigurationManager má novou vlastnost **ActionAfterReboot**.

        -   ContinueConfiguration (výchozí hodnota): automaticky obnoví konfiguraci po restartování cílový uzel.

        -   StopConfiguration: Pokračovat automaticky konfigurace po restartování uzlu.

    -   Konzistence spustit nyní dochází častěji, než na operaci PULL nebo naopak.

    -   Podpora správy verzí: DSC teď rozpoznat dokumentu, který byl vytvořen v novější klient (součástí [WMF 5.0](http://aka.ms/wmf5download)).

- Vylepšení prevence chyb

    -   Verze modulu teď se vynucuje před použitím konfigurace.

    -   **DebugPreference** je teď nastavená správně pro Get - Set- a testovací TargetResource volání.

- Zpracování vylepšení přihlašovacích údajů

    -   Certifikát se teď používá, pokud obě **certifikát** a **PSDscAllowPlainTextPassword** nejsou zadány.

    -   Přihlašovací údaje jsou dešifrovat i pro Get-TargetResource.

    -   Metakonfiguraci přihlašovací údaje jsou šifrované a dešifrovat.

    -   PSCredentials jsou nyní dešifrovat, pokud se nachází ve vložený objekt.

- Vylepšení předdefinované prostředků

    -   Balíček prostředků

        -   Už nainstaluje balíček nesprávný (buď z místní nebo webové zdroje).

        -   Teď podporuje protokol HTTPS.

    -   Je teď podporují řešení pro protokol HTTPS v [balíček prostředků](http://technet.microsoft.com/library/dn282132.aspx).

    -   [Archivovat prostředků](http://technet.microsoft.com/library/dn249917.aspx) nyní podporuje přihlašovací údaje.

## <a name="new-features-in-windows-powershell-50"></a>Nové funkce v prostředí Windows PowerShell 5.0

- [Nové funkce v prostředí Windows PowerShell](#new-features-in-windows-powershell)
- [Nové funkce v Konfigurace požadovaného stavu aplikace Windows PowerShell](#new-features-in-windows-powershell-desired-state-configuration)
- [Nové funkce v systému Windows PowerShell ISE](#new-features-in-windows-powershell-ise)
- [Nové funkce v systému Windows PowerShell webové služby](#new-features-in-windows-powershell-web-services-management-odata-iis-extension)
- [Významné opravy chyb v prostředí Windows PowerShell 5.0](#notable-bug-fixes-in-windows-powershell-50)

### <a name="new-features-in-windows-powershell"></a>Nové funkce v prostředí Windows PowerShell

- Spouštění v prostředí Windows PowerShell 5.0, můžete vyvíjet pomocí třídy, pomocí formální syntaxe a sémantikou, které jsou podobné jinými objektově orientované programovací jazyky. **Třída**, **výčtu**, a žádná jiná klíčová slova jsou přidané do jazyka prostředí Windows PowerShell, který má podpory nové funkce. Další informace o práci s třídami, najdete v tématu about_Classes.

- Prostředí Windows PowerShell 5.0 zavádí nové, strukturovaných informace datový proud, který můžete použít k přenosu strukturovaných dat mezi skript a jeho volající (nebo hostitelské prostředí). Nyní můžete Write-Host pro vydávání výstup do datového proudu informace. Datové proudy informace také fungovat pro PowerShell.Streams, úlohy, naplánované úlohy a pracovních postupů. Tyto funkce podporují informace datového proudu.

    -   Nový zápis informace rutinu, která umožňuje určit, jak Windows PowerShell zpracovává data datového proudu informace pro příkaz. Zápis hostitel je obálka pro zápis informace. Zápis informace jsou také aktivit podporované pracovního postupu.

    -   Dva nové společné parametry, InformationVariable a InformationAction, umožňují určit, jak se zobrazují informace o datových proudů v příkazu. Platné hodnoty pro InformationAction jsou SilentlyContinue, zastavení, pokračovat, Inquire, ignorovat nebo pozastavit s SilentlyContinue se výchozí hodnota. InformationVariable Určuje řetězec jako název proměnné, do kterého chcete data Write-Host z příkazu Uložit.

    -   Nové proměnné předvoleb, InformationPreference, určuje zúčastníte výchozí datový proud informace v relaci prostředí Windows PowerShell. Výchozí hodnota je SilentlyContinue.

    -   Dva nové společné parametry pracovního postupu, PSInformation a InformationAction, byly přidány.

    -   Při použití příkazu Format-Table sloupců tabulky jsou nyní automaticky formátovaná vyhodnocením první 300ms dat, která předá prostřednictvím datového proudu.

- Ve spolupráci s [Microsoft Research](http://research.microsoft.com/), byla přidána nové rutiny, ConvertFrom-řetězec. Řetězec ConvertFrom umožňuje extrahovat a analyzovat strukturovaných objekty z obsahu textového řetězce. Další informace najdete v tématu ConvertFrom řetězec.

- Novou rutinu převést řetězec automaticky formátovat text podle příklad, který je zadat parametr - příklad.

- Nový modul, Microsoft.PowerShell.Archive, zahrnuje rutiny, které umožňují komprimujte soubory a složky v souborech archivu (také označované jako ZIP), extrahujte soubory z existujících souborů ZIP a aktualizovat soubory ZIP s novější verzí souborů komprimované v nich.

- Nový modul, PackageManagement, umožňuje zjišťovat a instalovat balíčky softwaru na Internetu. Modul PackageManagement (dříve označované jako OneGet) je k sjednocení správy balíčků systému Windows pomocí jediného rozhraní prostředí Windows PowerShell a správce nebo multiplexor existující balíček správce (také nazývané poskytovatelé balíčku).

- Nový modul, PowerShellGet, umožňuje najít, nainstalovat, publikovat a aktualizovat moduly a prostředků DSC na [Galerie prostředí PowerShell](http://www.powershellgallery.com/), nebo na úložiště interní modul, který můžete nastavit tak, že spustíte rutinu Register-PSRepository.

- Nové klíčové slovo jazyka, **Hidden**, byla přidána k určení, zda ve výchozím nastavení ve výsledcích Get-člen není zobrazen člena (vlastnost nebo metodu) (Pokud přidáte parametr - Force). Vlastnosti nebo metody, které byly označeny jako skrytá také se nezobrazí ve výsledcích IntelliSense, pokud si nejste v kontextu, kde má být zobrazena; člena například automatické proměnné $to by měl zobrazit skryté členy v metodu třídy.

- Nová položka, odeberte položku a Get-ChildItem vylepšily podporují vytváření a správu [symbolické odkazy](http://en.wikipedia.org/wiki/Symbolic_link). **- ItemType** parametr nové položky přijímá nová hodnota **SymbolicLink**. Nyní můžete vytvořit symbolické odkazy na jediném řádku spuštěním rutiny New-položky.

- Get-ChildItem má také novou - hloubka parametr, který používáte s parametrem - Recurse omezit rekurze. Například Get-ChildItem-Recurse - 2 hloubka vrátí výsledky v aktuální složce všechny podřízené složky v aktuální složce a všechny složky v rámci podřízené složky.

- Teď umožňuje můžete kopírovat soubory nebo složky z jednu relaci prostředí Windows PowerShell do jiného, což znamená, že můžete zkopírovat soubory do relací, které jsou připojené ke vzdáleným počítačům copy-Item (včetně počítačů, na kterých běží [Nano Server](http://blogs.technet.com/b/windowsserver/archive/2015/04/08/microsoft-announces-nano-server-for-modern-apps-and-cloud.aspx), a proto mít žádné další rozhraní). Kopírování souborů, zadejte jako hodnotu nové parametry - FromSession a - ToSession PSSession ID a přidat - cestu a - cílové k určení cesty ke zdroji a cíl, v uvedeném pořadí. Například Copy-Item-cesta c:\\myFile.txt - ToSession $s – d: cílové\\můžete.

- Vylepšili jsme prostředí Windows PowerShell přepis použít na všechny hostování aplikace (například systému Windows PowerShell ISE) kromě hostitele konzoly (**powershell.exe**). Přepis možnosti (včetně povolení systémové přepis) se dá nakonfigurovat povolení **zapnout prostředí PowerShell přepis** nastavení zásad skupiny, najít v správce součástí šablony/Windows/Windows Prostředí PowerShell.

- Nová funkce trasování podrobné skriptu umožňuje povolit podrobné sledování a analýza skriptování použití prostředí Windows PowerShell v systému. Po povolení trasování podrobné skriptu prostředí Windows PowerShell zaznamená do protokolu událostí události trasování událostí pro Windows (ETW), všechny bloky skriptu **Microsoft-Windows-PowerShell/Operational**.

- Spouštění v prostředí Windows PowerShell 5.0, nové rutiny Cryptographic Message Syntax podporu pro šifrování a dešifrování obsahu pomocí formátu standard sdružení IETF pro kryptograficky ochranu zprávy, jak je uvedeno ve [RFC5652](http://tools.ietf.org/html/rfc5652). Rutiny Get-CmsMessage CmsMessage chránit a Unprotect-CmsMessage byly přidány do [Microsoft.PowerShell.Security](http://technet.microsoft.com/library/hh849807.aspx) modulu.

- Nové rutiny v [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modulu, Get-prostředí Runspace, ladění Runspace, Get-RunspaceDebug, RunspaceDebug povolit a zakázat-RunspaceDebug, umožňují nastavit možnosti ladění na prostředí runspace a zahájení a ukončení ladění na prostředí runspace. Pro ladění libovolný prostředí runspace "tedy prostředí runspace, které nejsou pro prostředí Windows PowerShell konzoly nebo Windows PowerShell ISE relace prostředí runspace výchozí '"prostředí Windows PowerShell umožňuje nastavit zarážky ve skriptu a přidali zarážky zastavit z spuštění, dokud se můžete připojit ladicí program k ladění skriptu prostředí runspace. Ladicí program skriptu prostředí Windows PowerShell pro prostředí runspace přidala podporu vnořené ladění pro libovolný prostředí runspace.

- Nové rutiny formátu šestnáctkový byl přidán do [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modulu. Formát šestnáctkový umožňuje zobrazit textu nebo binárních dat v šestnáctkovém formátu.

- Rutiny Get-schránky a schránky sadu byly přidány do [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modulu; jejich usnadňují přenos obsahu do a z relace prostředí Windows PowerShell. Rutiny schránky podporovat bitové kopie, zvukové soubory, seznamy souborů a text.

- Nové rutiny, Clear-odpadkový koš, byl přidán do [Microsoft.PowerShell.Management](http://technet.microsoft.com/library/hh849827(v=wps.640).aspx) modulu; tato rutina prázdné Bin recyklování pro pevnou jednotku, která zahrnuje externích jednotek. Ve výchozím nastavení se výzva k potvrzení příkazu Clear-odpadkový koš, protože vlastnost ConfirmImpact rutiny je nastavena na ConfirmImpact.High.

- Novou rutinu New-TemporaryFile, můžete vytvořit dočasný soubor v rámci skriptování. Ve výchozím nastavení, je vytvořen nový dočasný soubor v ```C:\Users\<user name>\AppData\Local\Temp```.

- Out-File, přidat obsahu a rutiny Set-obsahu teď mají nový parametr - NoNewline vynechá nový řádek po výstup.

- Rutinu New-Guid využívá třídy pro rozhraní .NET Framework Guid generovat identifikátor GUID je užitečné, pokud píšete skripty nebo prostředky DSC.

- Protože informací o verzi souboru může být zavádějící, zejména po souboru je opravit, jsou k dispozici pro objekty FileInfo vlastnosti nového FileVersionRaw a ProductVersionRaw skriptu. Například můžete spustit následující příkaz k zobrazení hodnot z těchto vlastností pro powershell.exe, kde $pid obsahuje ID procesu pro spuštěné relaci prostředí Windows PowerShell:  ```Get-Process -Id $pid -FileVersionInfo | Format-List *version* -Force```

- Nové rutiny Enter PSHostProcess a ukončení PSHostProcess umožňuje ladění skriptů prostředí Windows PowerShell v procesy, které jsou oddělené od aktuální proces, který běží v konzole Windows PowerShell. Spusťte Enter PSHostProcess zadejte, nebo připojení k konkrétní proces s ID a pak spusťte Get-prostředí Runspace vrátit active prostředí runspace v rámci procesu. Spusťte ukončení PSHostProcess odpojit z procesu po dokončení ladění skriptu v rámci procesu.

- Nové rutiny čekání-ladicí program byl přidán do [Microsoft.PowerShell.Utility](http://technet.microsoft.com/library/hh849958.aspx) modulu. Můžete spustit čekání-ladicí program k zastavení skript v ladicím programu před spuštěním další příkaz ve skriptu.

- Ladicí program pracovního postupu prostředí Windows PowerShell teď podporuje příkaz nebo kartě dokončení, a můžete ladit funkce vnořený pracovní postup. Nyní můžete stisknout **Ctrl + Break** k zadání ladicího programu spouštění skriptu, místní a vzdálené relace a skript pracovního postupu.

- Rutiny ladění-Job byl přidán do [Microsoft.PowerShell.Core](http://technet.microsoft.com/library/hh849695.aspx) modulu k ladění skriptů spuštěné úlohy pracovního postupu prostředí Windows PowerShell, pozadí a úlohy spuštěné v vzdálené relace.

- Nový stav, AtBreakpoint, přidala pro prostředí Windows PowerShell úlohy. Stav AtBreakpoint platí, pokud úloha spuštěna skript, který obsahuje nastavit zarážky a skript narazil na zarážky. Po zastavení úlohy u ladicí zarážky musíte ladit úlohy po spuštění rutiny ladění úlohy.

- Prostředí Windows PowerShell 5.0 implementuje podporu pro více verzí jeden modul prostředí Windows PowerShell ve stejné složce v $PSModulePath. Vlastnost RequiredVersion přidaná do třídy ModuleSpecification pomohou že získat požadovanou verzi modulu; Tato vlastnost je vzájemně se vylučuje s vlastnost verze modulu. RequiredVersion se teď podporuje v rámci hodnoty parametru položka FullyQualifiedName Get-Module, Import-Module a rutiny Remove-modulu.

- Teď můžete dělat ověření verze modulu spuštěním rutiny Test-ModuleManifest.

- Výsledky rutiny Get-Command teď měla zobrazovat sloupec verze; nové verze vlastnost byla přidána k třídě CommandInfo. Get-Command zobrazuje příkazy z více verzí stejného modulu. Vlastnost verze je také součástí odvozené třídy CmdletInfo: CmdletInfo a ApplicationInfo.

- Get-Command má nový parametr - ShowCommandInfo, který vrací ShowCommand informace jako PSObjects. To je obzvláště užitečná funkce pro při spuštění zobrazit příkaz v systému Windows PowerShell ISE pomocí vzdálenou komunikaci prostředí Windows PowerShell. Parametr - ShowCommandInfo nahrazuje stávající funkci Get-SerializedCommand v modulu Microsoft.PowerShell.Utility, ale skript Get-SerializedCommand je stále k dispozici pro podporu skriptování nižší úrovně.

- Novou rutinu Get-ItemPropertyValue umožňuje získat hodnotu vlastnosti, bez použití zápisu s tečkou. Například můžete starší verze prostředí Windows PowerShell, spusťte následující příkaz k získání hodnoty vlastnosti základ cesty aplikace PowerShellEngine klíče registru: **(Get-ItemProperty-HKLM cesta:\\softwaru\\ Microsoft\\prostředí PowerShell\\3\\PowerShellEngine-název ApplicationBase). ApplicationBase**. Spouštění v prostředí Windows PowerShell 5.0, můžete spustit **Get ItemPropertyValue-HKLM cesta:\\softwaru\\Microsoft\\prostředí PowerShell\\3\\PowerShellEngine-ApplicationBase název** .

- Konzolu prostředí Windows PowerShell teď používá jako v případě systému Windows PowerShell ISE zvýrazňování syntaxe.

- Nový modul NetworkSwitch obsahuje rutiny, které vám umožní použít přepínač virtuální sítě LAN (VLAN) a základní konfigurací portu síťového přepínače vrstvy 2 na Windows Server 2012 R2 logo certified síťové přepínače.

- Položka FullyQualifiedName parametr přidala do rutiny Import-Module a Remove-Module, k podpoře ukládání více verzí jeden modul.

- Nový parametr, FullyQualifiedModule typu ModuleSpecification mají Save-Help, Update-Help, Import PSSession, Export-PSSession a Get-Command. Přidejte tento parametr k určení plně kvalifikovaným názvem modulu.

- Hodnota **$PSVersionTable.PSVersion** byl aktualizovaný, aby 5.0.

### <a name="new-features-in-windows-powershell-desired-state-configuration"></a>Nové funkce v Konfigurace požadovaného stavu aplikace Windows PowerShell

- Vylepšení jazyk prostředí Windows PowerShell umožňují definovat požadovaného stavu aplikace Windows PowerShell (DSC) prostředky pomocí třídy. DscResource importu je nyní true dynamické klíčové slovo; Analyzuje zadaný modul prostředí Windows PowerShell se™ s kořenové modulu, hledání tříd, které obsahují DscResource atribut. Nyní můžete třídy k definování prostředků DSC, při jejichž je požadovaný soubor MOF ani DSCResource podsložky ve složce modulu. Soubor modulu prostředí Windows PowerShell může obsahovat několik tříd prostředků DSC.

- Byl přidán nový parametr, ThrottleLimit, na následující rutiny v modulu PSDesiredStateConfiguration. Přidejte parametr ThrottleLimit určuje počet cílových počítačů nebo zařízení, na kterých se má příkaz pro práci ve stejnou dobu.

    -   Get-DscConfiguration

    -   Get-DscConfigurationStatus

    -   Get-DscLocalConfigurationManager

    -   Obnovení DscConfiguration

    -   Test DscConfiguration

    -   Porovnání DscConfiguration

    -   Publikování DscConfiguration

    -   Set-DscLocalConfigurationManager

    -   Počáteční DscConfiguration

    -   Aktualizace DscConfiguration

- S centralizovanou DSC zpráv o chybách, bohaté zaznamenána informace o chybě není pouze v případě, že protokolu, ale lze odeslat buď do centrálního umístění pro pozdější analýzu. Tento centrální umístění můžete použít k ukládání chyby konfigurace DSC, které se vyskytly pro všechny servery ve svém prostředí. Po server sestav je definována v konfiguraci meta, všechny chyby odeslána na server sestav a pak uloženy v databázi. Tato funkce bez ohledu na to, jestli je nakonfigurovaná cílový uzel můžete nastavit načítat konfigurace z načítacího serveru.

- Vylepšení systému Windows PowerShell ISE usnadňují vytváření prostředků DSC. Nyní můžete provést následující.

    -   Všechny prostředky DSC v seznamu **konfigurace** nebo **uzlu** blok zadáním **Ctrl + mezerník** na prázdný řádek uvnitř bloku.

    -   Automatické dokončování na vlastnosti prostředku **výčtu** typu.

    -   Automatické dokončování na **DependsOn** vlastnost prostředky DSC, v závislosti na dalších prostředků instancí v konfiguraci.

    -   Dokončování pomocí tabulátorů vylepšené hodnot vlastností prostředku.

- Uživatele můžete nyní spustit prostředek pod zadanou sadu přihlašovacích údajů přidáním **PSDscRunAsCredential** atribut blok uzlu. Například PSDscRunAsCredential = Get-Credential Contoso\\DscUser. Tato funkce je užitečná pro vytvoření konfigurace, které spuštění Instalační služby systému Windows a spustitelný instalační programy, přístup k podregistru jednotlivé uživatele nebo provádět další úlohy mimo aktuální uživatelský kontext.

- byla přidána podpora (x86 na základě) 32-bit **konfigurace** – klíčové slovo.

- Prostředí Windows PowerShell teď zahrnuje podporu pro vlastní Nápověda pro konfigurace DSC, definované přidáním \[CmdletBinding()] funkce generované konfigurace.

- Nový **DscLocalConfigurationManager** atribut určuje blok konfigurace jako meta konfigurace, které slouží ke konfiguraci správce místní konfigurace DSC. Tento atribut omezuje konfiguraci, kterou chcete obsahující pouze položky, které nakonfigurovat správce místní konfigurace DSC. Během zpracování, tato konfigurace generuje \*. meta.mof souboru, který je poté odeslán do příslušné cílové uzly spuštěním rutiny Set-DscLocalConfigurationManager.

- V prostředí Windows PowerShell 5.0 jsou nyní povolené částečné konfigurace. Dokumenty konfigurace dokáže zajistit do uzlu v fragmenty. Pro uzel pro příjem více fragmentů dokumentem konfigurace uzlu se™ s správce místní konfigurace musíte nejprve nastavit k určení očekávaných fragmenty

- Synchronizace mezi počítači je nového v DSC v prostředí Windows PowerShell 5.0. Pomocí předdefinovaných WaitFor\* prostředky (**WaitForAll**, **WaitForAny**, a **WaitForSome**), teď můžete zadat závislosti mezi počítači Během konfigurace běží bez externí orchestrations. Tyto zdroje poskytují pomocí CIM připojení přes protokol WS-Man synchronizace mezi uzly. Konfiguraci můžete čekat na jiném počítači,™ chcete změnit stav s konkrétní prostředek.

- Stačí dostatečně správy (JEA), nové funkce zabezpečení delegování, využívá DSC a prostředí Windows PowerShell omezené prostředí runspace pomohou zabezpečené podniky před ztrátou dat nebo ohrožení zabezpečení zaměstnanci, ať už úmyslně nebo neúmyslně se překrývající. Další informace o sadě nástrojů JEA včetně, kde si můžete stáhnout prostředků xJEA DSC, najdete v části [právě dostatečně správy, krok za krokem](http://blogs.technet.com/b/privatecloud/archive/2014/05/14/just-enough-administration-step-by-step.aspx).

- Byly přidány následující nové rutiny v modulu PSDesiredStateConfiguration.

    -   Novou rutinu Get-DscConfigurationStatus získá souhrnné informace o konfiguraci stavu z cílového uzlu. Můžete získat stav posledního, nebo všechny konfigurace.

    -   Novou rutinu porovnání DscConfiguration porovnává zadanou konfigurací se skutečným stavem nejméně jeden cílový uzel.

    -   Novou rutinu Publish-DscConfiguration zkopíruje na cílový uzel konfigurační soubor MOF, ale nevztahuje konfigurace. Konfigurace se použije během průchodu další konzistence, nebo když spustíte rutinu Update-DscConfiguration.

    -   Nové rutiny Test-DscConfiguration umožňuje ověřit, jestli odpovídá Výsledná konfigurace požadované konfigurace, vrátí hodnotu PRAVDA, pokud konfigurace odpovídá požadované konfigurace, nebo hodnotu NEPRAVDA, pokud skutečné konfigurace neodpovídá požadované konfigurace.

    -   Novou rutinu Update-DscConfiguration vynutí konfiguraci, kterou chcete zpracovat. Pokud správce místní konfigurace je v režimu vyžádání obsahu, rutina získá konfigurace z načítacího serveru před každým jejím použitím.

### <a name="new-features-in-windows-powershell-ise"></a>Nové funkce v systému Windows PowerShell ISE

- Nyní můžete upravovat vzdálené skriptů prostředí Windows PowerShell a souborů v místní kopii systému Windows PowerShell ISE spuštěním Enter-PSSession spouští vzdálenou relaci v počítači, se™ s ukládání souborů, které chcete upravit a pak spuštěna **PSEdit <path and file name on the remote computer>**. Tato funkce usnadňuje úpravy soubory prostředí Windows PowerShell, které jsou uložené na možnost instalace jádra serveru systému Windows Server, kde nelze spustit Windows PowerShell ISE.

- Rutina Start-přepis se teď podporuje v systému Windows PowerShell ISE.

- Nyní můžete ladit vzdálené skriptů v systému Windows PowerShell ISE.

- Nový příkaz nabídky, **přerušení všech** (Ctrl + B), ladicímu pro místní i vzdálené spouštění skriptů.

### <a name="new-features-in-windows-powershell-web-services-management-odata-iis-extension"></a>Nové funkce v systému Windows PowerShell webové služby (IIS rozšíření Správa OData)

- Spouštění v prostředí Windows PowerShell 5.0, můžete vygenerovat sadu rutin prostředí Windows PowerShell podle funkce vystavené dané koncový bod OData, spuštěním rutiny Export-ODataEndpointProxy, najít v novém [ Microsoft.PowerShell.OdataUtils](http://technet.microsoft.com/library/dn818507(v=wps.640).aspx) modulu.

### <a name="notable-bug-fixes-in-windows-powershell-50"></a>Významné opravy chyb v prostředí Windows PowerShell 5.0

- Prostředí Windows PowerShell 5.0 obsahuje nové implementace modelu COM, který nabízí výrazné vylepšení výkonu při práci s objekty COM. Videoukázka účinek, najdete v části [Com_Perf_Improvements](http://1drv.ms/1qu3UPZ).

- Významné zlepšení výkonu byly provedeny na první kartě dokončení v relaci prostředí Windows PowerShell, zkrátit čas dokončení karta podle téměř 500 ms.

## <a name="new-features-in-windows-powershell-40"></a>Nové funkce v prostředí Windows PowerShell 4.0
Prostředí Windows PowerShell 4.0 je zpětně kompatibilní. Rutiny, zprostředkovatelé, moduly, moduly snap in, skripty, funkce a profily, které byly navrženy pro prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 2.0 fungují v prostředí Windows PowerShell 4.0 beze změn.

Prostředí Windows PowerShell 4.0 je nainstalována ve výchozím nastavení systému Windows 8.1 a Windows Server 2012 R2. Chcete-li nainstalovat prostředí Windows PowerShell 4.0 na systému Windows 7 s aktualizací SP1 nebo Windows Server 2008 R2, stáhněte a nainstalujte [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855). Nezapomeňte přečíst podrobnosti o stažení a splňovat všechny požadavky na systém, před instalací Windows Management Framework 4.0.

- [Nové funkce v prostředí Windows PowerShell](#new-features-in-windows-powershell-1)
- [Nové funkce v systému Windows PowerShell Integrované skriptovací prostředí (ISE)](#new-features-in-windows-powershell-integrated-scripting-environment-ise)
- [Nové funkce v pracovním postupu Windows PowerShell](#new-features-in-windows-powershell-workflow)
- [Nové funkce v systému Windows PowerShell webové služby](#new-features-in-windows-powershell-web-services)
- [Nové funkce v systému Windows PowerShell Web Access](#new-features-in-windows-powershell-web-access)
- [Významné opravy chyb v prostředí Windows PowerShell 4.0](#notable-bug-fixes-in-windows-powershell-40)

Prostředí Windows PowerShell 4.0 obsahuje následující nové funkce.

### <a name="new-features-in-windows-powershell"></a>Nové funkce v prostředí Windows PowerShell

- **Konfigurace požadovaného stavu aplikace Windows PowerShell** (DSC) je nový systém správy v prostředí Windows PowerShell 4.0 umožňující nasazení a správa konfiguračních dat pro služby softwaru a prostředí, ve kterém se tyto služby spuštěny. Další informace o DSC najdete v tématu [začít pracovat s konfigurace požadovaného stavu aplikace Windows PowerShell](https://technet.microsoft.com/library/c134aa32-b085-4656-9a89-955d8ff768d0).

- **Save-Help** teď umožňuje uložit nápovědy pro moduly, které jsou nainstalovány na vzdálených počítačích. Save-Help vám pomůže stáhnout modul nápovědy z klienta připojeného k Internetu (na kterém není všechny moduly, pro které chcete zobrazit nápovědu nutně nainstalovaných) a poté zkopírujte uložené nápovědy na vzdálené sdílené složce nebo ve vzdáleném počítači, který nemá Internet přístup.

- Ladicí program prostředí Windows PowerShell je vylepšená povolit ladění pracovních postupů prostředí Windows PowerShell, jakož i skripty, které běží na vzdálených počítačích. Pracovní postupy prostředí Windows PowerShell můžete ladit nyní na úrovni skriptu z příkazového řádku prostředí Windows PowerShell nebo Windows PowerShell ISE. Skripty prostředí Windows PowerShell, včetně pracovními postupy skriptů, můžete nyní ladit prostřednictvím vzdálené relace. Vzdálené ladění relace se zachovají přes vzdálené relací prostředí Windows PowerShell, které jsou odpojen a pak znovu později.

- A **RunNow** parametr pro **Register-ScheduledJob** a **Set-ScheduledJob** se eliminuje potřeba nastavit okamžité počáteční datum a čas pro úlohy pomocí **Aktivační událost** parametr.

- **Invoke-RestMethod** a **Invoke-WebRequest** teď umožňují nastavit všechny hlavičky pomocí parametru hlavičky. I když tento parametr má vždy existovalo, bylo několik parametrů pro webové rutiny, jejichž výsledkem výjimky nebo chyby.

- **Get-Module** má parametr nového **položka FullyQualifiedName**, typu **ModuleSpecification\[]**. **Položka FullyQualifiedName** parametr Get-Module teď umožňuje zadat modul pomocí modulu název, verzi a volitelně její identifikátor GUID.

- Výchozí nastavení zásady spouštění v systému Windows Server 2012 R2 je **RemoteSigned**. Na Windows 8.1 nedojde ke změně ve výchozím nastavení.

- Spouštění v prostředí Windows PowerShell 4.0, je volání metody pomocí názvů dynamické metoda podporována. Můžete použít proměnnou pro uložení název metody a dynamicky vyvolání metody při volání proměnné.

- Asynchronní pracovní postup úlohy jsou již odstraněny při časovém limitu, který je uveden ve **PSElapsedTimeoutSec** uplynul společný parametr pracovního postupu.

- Nový parametr **RepeatIndefinitely**, byl přidán do **New-JobTrigger** a **Set-JobTrigger** rutiny. Tím se eliminuje nutnost zadávání **TimeSpan.MaxValue, což** hodnota **RepetitionDuration** parametru opakovaně spouštět naplánované úlohy na dobu neurčitou.

- A **Passthru** parametr byl přidán do **Enable-JobTrigger** a **Disable-JobTrigger** rutiny. Parametr Passthru zobrazí objekty, které jsou vytvořit nebo změnit pomocí příkazu.

- Názvy parametrů pro zadání v pracovní skupině **Add-Computer** a **Remove-Computer** rutiny jsou konzistentní. Obě rutiny teď použít parametr **Název_pracovní_skupiny**.

- Nové společný parametr **PipelineVariable**, byla přidána. PipelineVariable umožňuje výsledky vytvoření kanálu příkazu (nebo součást vytvoření kanálu příkazu) uložit jako proměnnou a tu lze předat ve zbývající části kanálu.

- Kolekce filtrování pomocí syntaxe využívající metody se teď podporuje. To znamená, že teď můžete filtrovat na kolekci objektů pomocí zjednodušenou syntaxi, které je podobné pro Where() nebo Where-Object formátu volání metody. Následuje příklad: (Get-Process) .where ({$_. Název - shodovat s "powershell"})

- **Get-Process** rutina má parametr nového přepínače **IncludeUserName**.

- Nové rutiny **Get-FileHash**, která vrátí hodnotu hash souboru v některém z formátů pro určitý název souboru, byla přidána.

- V prostředí Windows PowerShell 4.0, pokud modul používá **DefaultCommandPrefix** klíče v manifestu, nebo pokud uživatel importuje modul s **předpony** parametr **ExportedCommands**vlastnost modulu zobrazuje příkazy v modulu s předponou. Při spouštění příkazů pomocí syntaxe modulu kvalifikovaný název modulu\\CommandName, názvy příkazů musí obsahovat předponu.

- Hodnota **$PSVersionTable.PSVersion** byl aktualizovaný, aby 4.0.

- **WHERE()** operátor chování změnilo. `Collection.Where('property -match name')` přijetí řetězcového výrazu ve formátu `"Property -CompareOperator Value"` již není podporována. Ale **Where()** operátor přijímá výrazy řetězec ve formátu scriptblock; to je podporováno.

### <a name="new-features-in-windows-powershell-integrated-scripting-environment-ise"></a>Nové funkce v systému Windows PowerShell Integrované skriptovací prostředí (ISE)

- Windows PowerShell ISE podporuje pracovního postupu prostředí Windows PowerShell ladění i ladění vzdáleného skriptu.

- Byla přidána podpora technologie IntelliSense pro zprostředkovatele konfigurace požadovaného stavu aplikace Windows PowerShell a konfigurace.

### <a name="new-features-in-windows-powershell-workflow"></a>Nové funkce v pracovním postupu Windows PowerShell

- Byla přidána podpora pro novou **PipelineVariable** společný parametr v kontextu iterativní kanálů, jako jsou ty používané System Center Orchestrator; to znamená, který spustí příkazy jednoduše zleva doprava, naproti tomu kanálů spolu s pomocí vysílání datového proudu.

- Vazby parametru je výrazně Vylepšená pro práci mimo karta dokončení scénáře, jako třeba s příkazy, které nejsou k dispozici v aktuální prostředí runspace.

- Byla přidána podpora pro vlastní kontejner aktivity do pracovního postupu prostředí Windows PowerShell. Pokud je parametrem aktivity typy **aktivity**, **aktivity\[]**' ", nebo je obecný kolekce aktivit" a uživatel má zadaný blok skriptu jako argument, pak Windows Prostředí PowerShell Workflow převádí blok skriptu do jazyka XAML, stejně jako u normálních kompilace skript do pracovního postupu prostředí Windows PowerShell.

- Po chybě pracovní postup prostředí Windows PowerShell automaticky znovu připojí ke spravovaným uzlům.

- Teď můžete omezit **Foreach-Parallel** příkazy aktivity pomocí **ThrottleLimit** vlastnost.

- **ErrorAction** společný parametr má novou platnou hodnotu **pozastavit**, která je výhradně pro pracovní postupy.

- Koncový bod pracovního postupu nyní automaticky zavře, pokud nejsou žádné aktivní relace, žádné probíhající úlohy a žádné úlohy čekající na vyřízení. Tato funkce šetří prostředky na počítači, který funguje jako server pracovního postupu při splnění podmínek automatické uzavření.

### <a name="new-features-in-windows-powershell-web-services"></a>Nové funkce v systému Windows PowerShell webové služby

- Když dojde k chybě v systému Windows PowerShell webové služby (PSWS, také zavolat OData IIS rozšíření Management), při použití rutiny běží, více podrobné chybové zprávy jsou vrácena volajícímu. Kromě toho postupujte podle kódů chyb [pokyny kódu chyby REST API služby Windows Azure](http://msdn.microsoft.com/library/windowsazure/dd179357.aspx).

- Koncový bod můžete nyní definovat verze rozhraní API, a také vynutit použití na konkrétní verzi rozhraní API. Vždy, když dojde k verze neshody mezi klientem a serverem, se zobrazí chyby na klientovi i na serveru.

- Správa schématu odesílání je jednodušší pomocí automatického generování hodnoty pro všechna pole chybí ve schématu. Generování dojde k užitečné počáteční bod, i když odesílání schéma neexistuje.

- Vylepšili jsme zpracování v PSWS typu pro podporu typů, které používají jiný konstruktor než výchozí konstruktor podle chovají podobně jako **PSTypeConverter** v prostředí Windows PowerShell. To umožňuje využívat komplexní typy s PSWS.

- PSWS teď umožňuje rozšíření přidruženou instanci při spuštění dotazu. Pro větší binární obsah (například obrázky, zvuk nebo video) náklady na přenos je důležité, a je lepší pro přenos binární data bez kódování. PSWS používá k přenosu bez kódování datových proudů s názvem prostředku. Datový proud s názvem prostředku je vlastností entitu **Edm.Stream** typu. Každý datový proud prostředku s názvem má samostatnou identifikátor URI pro operace GET nebo aktualizace.

- Akce OData nyní poskytují mechanismus pro volání metod (vytvoření, čtení, aktualizaci a odstraňování) bez CRUD na prostředku. Akce můžete vyvolat odesláním požadavku HTTP POST na identifikátor URI, která je definována pro akci. Parametry pro akce jsou definovány v textu požadavku POST.

- Chcete-li být v souladu s pokyny pro Windows Azure, je třeba zjednodušit všechny adresy URL. Změna součástí **klíč jako Segment** umožňuje jednoho klíče na být reprezentován jako segmenty. Všimněte si, odkazy, které používají více hodnot klíčů vyžadují, aby se s hodnotami oddělenými čárkami shod notaci jako předtím.

- Než tato verze PSWS pouze způsob, jak provést vytvoření, aktualizace nebo odstranění operace byla k vyvolání Post, Put, nebo odstranění na nejvyšší úrovni prostředku. Nové v této verzi PSWS operations obsažených prostředků uživatelům umožňují dosáhnout stejné výsledky při dosažení stejného zdroje méně přímo blíží, jako kdyby byly obsaženy tyto prostředky.

### <a name="new-features-in-windows-powershell-web-access"></a>Nové funkce v systému Windows PowerShell Web Access

- Můžete odpojit od a znovu připojit k existující relací ve webové konzole Windows PowerShell Web Access. A **Uložit** tlačítka ve webové konzole umožňuje odpojení z relace bez odstranění ji a znovu připojit k relaci jiného čas.

- Výchozí parametry lze zobrazit na stránce přihlášení. Pokud chcete zobrazit výchozí parametry, konfigurovat hodnoty pro všechna nastavení, zobrazí v **volitelná nastavení připojení** oblast přihlašovací stránky v souboru s názvem **web.config**. Můžete použít **web.config** souboru ke konfiguraci všech volitelná nastavení připojení s výjimkou sekundu nebo alternativní sadu pověření.

- Ve Windows serveru 2012 R2 můžete vzdáleně spravovat autorizační pravidla pro Windows PowerShell Web Access. **Add-PswaAuthorizationRule** a **Test-PswaAuthorizationRule** rutiny nyní obsahují parametr Credential, který umožňuje správcům spravovat autorizační pravidla ze vzdáleného počítače nebo v Windows PowerShell Web Access relace.

- Nyní můžete mít více relací Windows PowerShell Web Access v jedné relace prohlížeče pomocí novou kartu prohlížeče pro každou relaci. Již nepotřebujete otevřete novou relaci prohlížeče připojení k nové relaci ve webové konzole Windows PowerShell.

### <a name="notable-bug-fixes-in-windows-powershell-40"></a>Významné opravy chyb v prostředí Windows PowerShell 4.0

- **Get-Counter** teď vrátit čítače, které obsahují znak apostrofu ve francouzštině edicích systému Windows.

- Teď si můžete zobrazit **GetType** metodu deserializovat objekty.

- **#Requires** příkazy teď uživatelům umožňují vyžadovat oprávnění správce, v případě potřeby.

- **Import Csv** rutiny teď ignoruje prázdné řádky.

- Problém, kde Windows PowerShell ISE využívá příliš mnoho paměti při spuštění **Invoke-WebRequest** příkaz byl opraven.

- **Get-Module** teď zobrazuje verze modulu v **verze** sloupce.

- Remove-Item - Recurse teď odebere položky z podsložky podle očekávání.

- A **uživatelské jméno** vlastnost byla přidána do **Get-Process** výstup objektů.

- **Invoke-RestMethod** rutiny teď vrací všechny výsledky k dispozici.

- **Přidat člena** teď se projeví na zatřiďovací tabulky, i když zatřiďovacích tabulkách nebyly dosud přístup.

- **Select-Object - rozbalte** už selže nebo vygeneruje výjimku, pokud je hodnota vlastnosti null nebo prázdný.

- **Get-Process** může být použit v kanálu s jinými příkazy, které získají **ComputerName** vlastnost z objektů.

- **ConvertTo-Json** a **ConvertFrom Json** teď může přijmout podmínky v rámci dvojité uvozovky, a jeho chybové zprávy jsou teď možnosti lokalizace.

- **Get-Job** nyní vrátí všechny dokončit naplánované úlohy, i v jiných relacích.

- Problémy s připojení a odpojení bitové virtuálních pevných disků pomocí **FileSystem** zprostředkovatele v prostředí Windows PowerShell 4.0 byly opraveny. Prostředí Windows PowerShell je teď dokáže detekovat nové jednotky, pokud jsou připojené ve stejné relaci.

- Už nemusíte explicitně načíst **ScheduledJob** nebo **pracovního postupu** moduly pro práci s jejich typy úloh.

- Vylepšení výkonu byly provedeny importu pracovní postupy, které definují vnořené pracovní postupy; Tento proces je rychlejší.

## <a name="new-features-in-windows-powershell-30"></a>Nové funkce v prostředí Windows PowerShell 3.0
Prostředí Windows PowerShell 3.0 obsahuje následující nové funkce.

- [Pracovní postup prostředí Windows PowerShell](#windows-powershell-workflow)
- [Windows PowerShell Web Accessu](#windows-powershell-web-access)
- [Nové funkce systému Windows PowerShell ISE](#new-windows-powershell-ise-features)
- [Podpora pro rozhraní Microsoft .NET Framework 4.0](#support-for-microsoft-net-framework-4)
- [Podpora pro prostředí předinstalace systému Windows](#support-for-windows-preinstallation-environment)
- [Odpojené relace](#disconnected-sessions)
- [Robustní relace připojení](#robust-session-connectivity)
- [Systém aktualizovatelné nápovědy](#updatable-help-system)
- [Rozšířené Online nápovědy](#enhanced-online-help)
- [Integrace CIM](#cim-integration)
- [Relace konfigurační soubory](#session-configuration-files)
- [Naplánované úlohy a integrace Plánovač úloh](#scheduled-jobs-and-task-scheduler-integration)
- [Vylepšení jazyk prostředí PowerShell systému Windows](#windows-powershell-language-enhancements)
- [Nové rutiny jádra](#new-core-cmdlets)
- [Vylepšení existující základní rutiny a zprostředkovatelé](#improvements-to-existing-core-cmdlets-and-providers)
- [Modul vzdáleného importu a zjišťování](#remote-module-import-and-discovery)
- [Dokončování pomocí tabulátorů rozšířené](#enhanced-tab-completion)
- [Automatické načítání modulu](#module-auto-loading)
- [Vylepšení prostředí modulu](#module-experience-improvements)
- [Zjednodušená příkaz zjišťování](#simplified-command-discovery)
- [Vylepšené protokolování diagnostiky a podpora zásad skupiny](#improved-logging-diagnostics-and-group-policy-support)
- [Formátování a vylepšení výstup](#formatting-and-output-improvements)
- [Prostředí hostitele rozšířené konzoly](#enhanced-console-host-experience)
- [Nové rutiny a hostování rozhraní API](#new-cmdlet-and-hosting-apis)
- [Vylepšení výkonu](#performance-improvements)
- [RunAs a podpory sdílené hostitelů](#runas-and-shared-host-support)
- [Vylepšení zpracování speciální znak](#special-character-handling-improvements)

### <a name="windows-powershell-workflow"></a>Pracovní postup prostředí Windows PowerShell
Pracovní postup prostředí Windows PowerShell přináší výkon modelu Windows Workflow Foundation pro prostředí Windows PowerShell. Můžete napsat pracovních postupů v jazyce XAML, nebo v jazyce prostředí Windows PowerShell a spustit je stejně, jako by spustit rutinu. [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) rutiny získá workflw příkazy a [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) rutiny získá nápovědy pro pracovní postupy.

Pracovní postupy jsou pořadí multicomputer správy aktivit, které jsou dlouho běžící, opakovatelných, časté, paralelní, přerušitelné, suspendable a nabízet možnost restartování. Pracovní postupy lze obnovit z úmyslnému nebo náhodnému přerušení, jako je výpadek sítě, restartování systému Windows nebo výpadku napájení.

Pracovní postupy jsou také přenosné; může být exportovány jako nebo naimportovaná ze souborů XAML. Můžete napsat vlastní relaci konfigurace, které umožňují pracovní postupy nebo aktivity v pracovním postupu ke spuštění delegovaný nebo podřízené uživatelů.

Následující seznam uvádí výhody pracovního postupu prostředí Windows PowerShell

- Automatizace sekvencované, dlouhotrvajících úloh.

- **Vzdálené monitorování dlouhotrvající úlohy**. Stav a průběh činností jsou viditelné kdykoli.

- **Multicomputer správy.** Současně spouštět úlohy jako pracovních postupů na stovky spravovaných uzlů. Pracovního postupu prostředí Windows PowerShell obsahuje integrovanou knihovnu společné parametry správy, například **PSComputerName**, který povolení scénářů správy více počítači.

- **Jediná úloha provádění komplexní procesy.** Související skripty, které implementují celém scénáři začátku do konce do jednoho pracovního postupu můžete kombinovat.

- **Trvalost.** : pracovní postup je uložit (nebo zkontrolujte odkazoval) v určitých bodech definovaný autorem, můžete obnovit od posledního trvalého úlohu (nebo kontrolního bodu), nemuseli ho od začátku.

- **Robustnost.** Automatizované zotavení po chybě. Pracovní postupy fungují po plánovaných a neplánovaných restartování. Můžete pozastavit provádění pracovního postupu a poté obnovit od vytvoření posledního bodu trvalost. Autoři pracovního postupu můžete určit konkrétní aktivity potřeba znovu spustit v případě selhání na jeden nebo více spravovaných uzlů.

- **Možnost odpojit, znovu připojit a spusťte v odpojených relací.** Uživatelé můžou připojit a odpojit od server pracovního postupu, ale pracovní postup běží nepřetržitě. Můžete odhlásit, klientský počítač nebo restartujte klientský počítač a monitorovat spuštění pracovního postupu z jiného počítače bez přerušení pracovního postupu.

- **Plánování.** Úkoly pracovního postupu může být naplánována jako všechny rutiny prostředí Windows PowerShell nebo skriptu.

- **Pracovní postup a omezení připojení.** Spuštění pracovního postupu a připojení k uzlům, můžete omezena, a tak umožňuje scénáře škálovatelnost a vysokou dostupností.

### <a name="windows-powershell-web-access"></a>Windows PowerShell Web Access
Windows PowerShell Web Access je funkce systému Windows Server 2012, která umožňuje uživatelům spustit příkazy prostředí Windows PowerShell a skriptů ve webové konzole. Zařízení, která používají webové konzoly nevyžadují prostředí Windows PowerShell, software pro vzdálenou správu nebo instalace modulu plug-in prohlížeče. Je vyžadováno je správně nakonfigurovaná brána Windows PowerShell Web Access a prohlížeč v klientském zařízení, která podporuje JavaScript a přijímá soubory cookie.

Další informace najdete v tématu [nasazení Windows PowerShell Web Access](http://go.microsoft.com/fwlink/p/?LinkID=221050).

### <a name="new-windows-powershell-ise-features"></a>Nové funkce systému Windows PowerShell ISE
Pro prostředí Windows PowerShell 3.0, Windows PowerShell Integrované skriptovací prostředí (ISE) má mnoho nových funkcí, technologii IntelliSense, zobrazit příkazové okno, včetně jednotná podokna konzoly, fragmenty, odpovídající složené závorce, rozbalení a sbalení části, automatické ukládání, poslední položky seznam, bohaté kopírování, kopie bloku a plnou podporu pro zápis pracovní postupy skriptů prostředí Windows PowerShell. Další informace najdete v tématu [about_Windows_PowerShell_ISE [verze 3]](https://technet.microsoft.com/library/dfa54d47-60c6-4fff-8197-c747e8d411bb).

### <a name="support-for-microsoft-net-framework-4"></a>Podpora pro rozhraní Microsoft .NET Framework 4
Prostředí Windows PowerShell je založený na běžné 4.0 Runtime jazyka. Rutiny, skript a autoři pracovního postupu můžete použít nové třídy rozhraní Microsoft .NET Framework 4 v prostředí Windows PowerShell s funkcemi, které zahrnují kompatibilita aplikací a nasazení, spravované rozhraní rozšiřitelnosti, paralelní výpočty, sítě, Windows Communication Foundation a modelu Windows Workflow Foundation.

### <a name="support-for-windows-preinstallation-environment"></a>Podpora pro prostředí předinstalace systému Windows
Prostředí Windows PowerShell 3.0 je volitelná součást Windows Preinstallation Environment (Windows PE) 4.0, pro systém Windows 8. Prostředí Windows PE je minimální operační systém, který spustí počítač, který nemá žádný operační systém a připraví je k instalaci systému Windows. Prostředí Windows PE můžete použít k oddílu a formátování pevných disků, zkopírujte bitových kopií disku do počítače a zahájení instalace systému Windows ze síťové sdílené složky. Prostředí Windows PowerShell 3.0 lze použít v prostředí Windows PE ke správě nasazení, diagnostiky a obnovení scénáře.

### <a name="disconnected-sessions"></a>Odpojené relace
Počínaje Windows PowerShell 3.0 je trvalé spravovaná uživatelem relací ("PSSessions"), které vytvoříte pomocí rutiny New-PSSession ukládají na vzdáleném počítači. Již nejsou závislé na relace, ve kterém byly vytvořeny.

Teď můžete odpojit z relace, a to bez přerušení příkazy, které jsou spuštěné v relaci. Můžete zavřít relace a vypnout počítač. Později se můžete připojit k relaci z jiné relace na stejné nebo na jiném počítači.

**ComputerName** parametr [Get-PSSession](https://technet.microsoft.com/library/b2b10531-d0df-4746-b877-e75c09955cb6) rutiny nyní získá všechny uživatele relací, které se připojují k počítači, i v případě, že byly spuštěny v jiné relaci v jiném počítači. Můžete připojit k relací, získat výsledky příkazy, spusťte nové příkazy a pak odpojení z relace.

Byly přidané nové rutiny pro podporu funkce odpojí relace, včetně [Disconnect-PSSession](https://technet.microsoft.com/library/f8f95111-612f-4cba-9098-77904b0473d8), [Connect-PSSession](https://technet.microsoft.com/library/b803dd29-f208-4079-80d4-db04d778f060), a Receive-PSSession a nové parametry byly přidány do rutiny, které spravovat PSSessions, například **InDisconnectedSession** parametr [Invoke-Command](https://technet.microsoft.com/library/906b4b41-7da8-4330-9363-e7164e5e6970) rutiny.

Odpojení relace funkce je podporována pouze v případě, že počítače v obou pocházející ("client") a ukončení ("server") konců připojení je spuštěné prostředí Windows PowerShell 3.0.

### <a name="robust-session-connectivity"></a>Robustní relace připojení
Prostředí Windows PowerShell 3.0 zjistí neočekávané ztráty připojení mezi klientem a serverem a pokusí se znovu vytvořit připojení a pokračovat v provádění automaticky. Pokud v přiděleném čase nelze znovu navázat připojení klient server, je uživateli upozornění, že a se odpojí relace. Při pokusu o připojení prostředí Windows PowerShell poskytuje neustálé zpětné vazby pro uživatele.

Pokud odpojené relaci byl spuštěn s použitím invokecommand –, prostředí Windows PowerShell vytvoří úlohu pro odpojené relaci, aby bylo snazší nové připojení a pokračovat v provádění.

Tyto funkce poskytuje vzdálenou komunikaci prostředí spolehlivější a obnovitelných a umožňují uživatelům provádět dlouhotrvající úlohy, které vyžadují robustní relace, jako jsou pracovní postupy.

### <a name="updatable-help-system"></a>Systém aktualizovatelné nápovědy
Teď si můžete stáhnout soubory aktualizované nápovědy k rutinám v modulech. [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) rutiny identifikuje nejnovější soubory nápovědy, je stáhne z Internetu, je rozbalí, ověřuje je a nainstaluje je ve správném adresáři konkrétní jazyk pro modul.

Pokud chcete použít soubory aktualizované nápovědy, stačí zadat `Get-Help`. Není nutné restartování systému Windows nebo prostředí Windows PowerShell. Abyste mohli aktualizovat nápovědu pro moduly v adresáři $pshome, spusťte prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".

Pro podporu uživatelů, kteří nemají přístup k Internetu a uživatelů za branami firewall, nové [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) rutiny stáhne soubory nápovědy k adresáři systému souborů, například do sdílené složky. Uživatelé pak můžou použít [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) rutiny soubory aktualizované nápovědy ze sdílené složky.

Můžete použít [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) soubory rutiny, abyste mohli aktualizovat nápovědu pro všechny nebo konkrétní modulů ve všech podporována uživatelského rozhraní jazykové verze. Můžete vložit i [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) příkazu ve vašem profilu prostředí Windows PowerShell. Ve výchozím nastavení prostředí Windows PowerShell stáhne soubory nápovědy pro modul více než jednou denně.

Windows 8 a Windows Server 2012 moduly neobsahují soubory nápovědy. Chcete-li stáhnout nejnovější soubory nápovědy, zadejte `Update-Help`. Další informace získáte zadáním `Get-Help` (bez parametrů) nebo najdete [about_Updatable_Help](https://technet.microsoft.com/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe).

Pokud nejsou instalovány soubory nápovědy pro rutinu v počítači, [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) rutiny teď zobrazuje automaticky generovaný nápovědy. Nápověda automaticky generovaný obsahuje syntaxi příkazu a pokyny pro použití [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) rutiny stáhnout soubory nápovědy.

Všechny Autor modulu může podporovat aktualizovatelné nápovědy pro jejich modulu. Můžete zahrnout soubory nápovědy v modulu a pomocí aktualizovatelné nápovědy je aktualizovat nebo vynechejte soubory nápovědy a k jejich instalaci použít aktualizovatelné nápovědy. Další informace o podpoře aktualizovatelné nápovědy najdete v tématu [podpora aktualizovatelné nápovědy](http://go.microsoft.com/FWLink/?LinkID=242129) na webu MSDN.

### <a name="enhanced-online-help"></a>Rozšířené Online nápovědy
Online nápověda prostředí Windows PowerShell je cenné prostředků pro všechny uživatele, ale je obzvláště důležité pro uživatele, kteří nepodporují nebo nelze nainstalovat soubory aktualizované nápovědy.

Chcete-li získat online nápovědu pro všechny rutiny prostředí Windows PowerShell, zadejte:

```
Get-Help <cmdlet-name> -Online
```

Prostředí Windows PowerShell se otevře online verzi tématu nápovědy v výchozí prohlížeč Internetu.

**Get-Help-Online** funkce v prostředí Windows PowerShell 3.0 je ještě účinnější nyní, protože funguje i, pokud nejsou soubory nápovědy pro rutinu nainstalovány v počítači. **Get-Help-Online** funkce získá identifikátor URI pro online téma nápovědy z vlastnosti HelpUri rutin a pokročilé funkce.

```
PS C:\>(Get-Command Get-ScheduledJob).HelpUri
http://go.microsoft.com/fwlink/?LinkID=223923
```

Od verze prostředí Windows PowerShell 3.0, může vyplnit autoři rutin C# **HelpUri** vlastnost tak, že vytvoříte **HelpUri** atribut k třídě rutiny. Autoři pokročilé funkce můžete definovat **HelpUri** vlastnost **CmdletBinding** atribut. Hodnota **HelpUri** vlastnost musí začínat řetězcem "http" nebo "https".

Můžete použít také **HelpUri** hodnota v první odkaz související souboru nápovědy rutiny založené na XML nebo. Odkaz – direktiva založená na komentářích nápovědy ve funkci.

Další informace o podpoře online nápovědy najdete v tématu [podpora Online nápovědy](http://go.microsoft.com/fwlink/?LinkId=242132) na webu MSDN.

### <a name="cim-integration"></a>Integrace CIM
Prostředí Windows PowerShell 3.0 zahrnuje podporu pro informace modelu CIM (Common), která poskytuje společné definice informace pro správu pro systémy, sítě, aplikace a služby, což jim exchange management informací mezi heterogenní systémy. Podpora pro CIM v prostředí Windows PowerShell 3.0, včetně schopnosti vytváření rutin prostředí Windows PowerShell, které jsou založené na nový nebo existující třídy modelu CIM, příkazy založený na definici rutiny soubory XML, podporu pro rozhraní .NET Framework CIM. Rozhraní API správy rutin modelu CIM a zprostředkovatelé rozhraní WMI 2.0.

### <a name="session-configuration-files"></a>Relace konfigurační soubory
Od verze prostředí Windows PowerShell 3.0, můžete navrhnout vlastní konfiguraci relace pomocí souboru. Konfigurační soubor novou relaci vám umožní určit prostředí relace, které používají konfiguraci relace, které moduly, skripty, včetně a soubory ve formátu jsou načtena do relací, kteří uživatelé elementy rutiny a jazyk, můžete použít, které moduly a skripty můžete spustit, a které proměnné uvidí.

Můžete navrhnout relace, ve kterém uživatelé mohou pouze spouštět rutiny z jednoho konkrétního modulu nebo relace, ve kterém uživatelé mají úplným jazykovým, přístup k všechny moduly a přístup k skripty, které provádět pokročilé úlohy.

V předchozích verzích Windows PowerShell byl k dispozici jenom pro ty, kteří mohou zapsat programu v C# nebo komplexní spuštění skriptu ovládacího prvku na této úrovni. Každý člen skupiny Administrators v počítači teď můžete přizpůsobit konfiguraci relace pomocí konfiguračního souboru.

Chcete-li vytvořit konfigurační soubor relace, použijte [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866) rutiny. Pro použití konfiguračního souboru relace ke konfiguraci relace, použijte [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) nebo [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) rutiny.

Další informace najdete v tématu [about_Session_Configuration_Files](https://technet.microsoft.com/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8) a [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866).

### <a name="scheduled-jobs-and-task-scheduler-integration"></a>Naplánované úlohy a integrace Plánovač úloh
Teď můžete naplánovat úlohy na pozadí prostředí Windows PowerShell a spravovat je v prostředí Windows PowerShell a v Plánovači úloh.

Prostředí Windows PowerShell naplánované úlohy jsou užitečné hybridní úlohy na pozadí prostředí Windows PowerShell a úkolů plánovače úloh.

Jako úlohy na pozadí prostředí Windows PowerShell spusťte naplánované úlohy asynchronně na pozadí. Instance naplánované úlohy, které byly dokončeny lze spravovat pomocí rutin úlohy, jako například [Start-Job](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442) a [Get-Job](https://technet.microsoft.com/library/1352c534-7193-46ca-9ab1-0c5219a661ad).

Jako úkolů plánovače úloh můžete spustit naplánované úlohy podle plánu jednorázové nebo opakující nebo v reakci na akci nebo událostí. Můžete zobrazit a spravovat naplánované úlohy v Plánovači úloh, povolit nebo zakázat, je podle potřeby, je spustit nebo používat jako šablony a nastavit podmínky, za kterých se zahájením úloh.

Kromě toho naplánované úlohy se dodávají s vlastní sadu rutin pro jejich správu. Rutiny umožňují vytvářet, upravovat, spravovat, zakázat a znovu povolte naplánované úlohy, vytvořte naplánovanou úlohu aktivační události a nastavit možnosti naplánovanou úlohu.

Další informace o naplánované úlohy najdete v tématu [about_Scheduled_Jobs](https://technet.microsoft.com/library/3b546629-703c-4939-b44f-52dd567bce92).

### <a name="windows-powershell-language-enhancements"></a>Vylepšení jazyk prostředí PowerShell systému Windows
Prostředí Windows PowerShell 3.0 obsahuje řadu funkcí, které jsou navržené tak, aby jeho jazyk jednodušší, snazší použít a vyhnout se běžných chyb. Mezi vylepšení patří vlastnost výčtu, počet a délku vlastnosti na skalární objekty, nových operátorů přesměrování, modifikátor oboru $Using, PSItem automatické proměnnou, flexibilní skriptu formátování, atributy proměnných, zjednodušené atribut argumenty, názvy číselné příkazů, analýza Stop operátor, vylepšené pole splatting, nové operátory bitového, seřazené slovník, PSCustomObject přetypování a vylepšené Nápověda založená na komentář.

### <a name="new-core-cmdlets"></a>Nové rutiny jádra
Byly přidané nové rutiny na instalaci jádro systému Windows PowerShell, včetně rutin určených ke správě naplánované úlohy, odpojené relace, integrace CIM a v aktualizovatelné systému nápovědy.

|||
|-|-|
|Přidat JobTrigger|Nový JobTrigger|
|Connect-PSSession|Nové PSSessionConfigurationFile|
|ConvertFrom Json|New-PSTransportOption|
|ConvertTo-Json|Nové PSWorkflowExecutionOption|
|Disable-JobTrigger|Nové PSWorkflowSession|
|Disable-ScheduledJob|Nové ScheduledJobOption|
|Odpojení PSSession|Nový WinEvent.|
|Povolit JobTrigger|Zobrazí PSSession|
|Povolit ScheduledJob|Registrace CimIndicationEvent|
|Get-CimAssociatedInstance|Register-ScheduledJob|
|Get-CimClass|Odebrat CimInstance|
|Get-CimInstance|Remove-CimSession|
|Get-CimSession|Odebrat TypeData|
|Get-ControlPanelItem|Přejmenování počítače|
|Get-IseSnippet|Resume-Job|
|Get-JobTrigger|Save-Help|
|Get-ScheduledJob|Set-CimInstance|
|Get-ScheduledJobOption|Set-JobTrigger|
|Get-TypeData|Set-ScheduledJob|
|Import IseSnippet|Set-ScheduledJobOption|
|Vyvolání AsWorkflow|Zobrazit – příkaz|
|Vyvolání CimMethod|Zobrazit ControlPanelItem|
|Vyvolání RestMethod|Pozastavení úlohy|
|Vyvolání WebRequest|Test PSSessionConfigurationFile|
|Nové CimInstance|Zrušení blokování souborů|
|Nový CimSession|Unregister-ScheduledJob|
|Nové CimSessionOption|Update-Help|
|Nové IseSnippet||

### <a name="improvements-to-existing-core-cmdlets-and-providers"></a>Vylepšení existující základní rutiny a zprostředkovatelé
Prostředí Windows PowerShell 3.0 obsahuje nové funkce pro existující rutiny včetně zjednodušenou syntaxi a nové parametry pro následující rutiny: rutiny počítače, CSV rutiny Get-ChildItem Get-Command, Get-obsah, Get-historie, objekt míry zabezpečení rutiny Select-Object, vyberte řetězec, rozdělení-Path, spuštění procesu, typu t-Object, Test-Connection, přidat člena a rutin rozhraní WMI.

Zprostředkovatelé prostředí Windows PowerShell byly také výrazně zlepšila, včetně podpory zprostředkovatele certifikát ke správě certifikátů vrstvy SSL (Secure Socket) pro hostování webů, podporu pro přihlašovací údaje, trvalé síťové jednotky a alternativní datové proudy v jednotky systému souborů.

### <a name="remote-module-import-and-discovery"></a>Modul vzdáleného importu a zjišťování
Prostředí Windows PowerShell 3.0 rozšiřuje modul zjišťování, import a možnosti implicitní Vzdálená komunikace na vzdálených počítačích. Rutiny modulu získání modulů na vzdálených počítačích a naimportujte moduly do vzdáleného nebo místního počítače pomocí vzdálené komunikace Windows Powershellu. Nová podpora relace CIM umožňuje používat CIM a WMI ke správě počítačů jiný systém než Windows importováním příkazy do místního počítače, který implicitně spustit na vzdáleném počítači.

Další informace najdete v tématech nápovědy pro [Get-Module](https://technet.microsoft.com/library/2cccd4c4-9a21-4c77-b691-984ee57242e1) a [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) rutiny.

### <a name="enhanced-tab-completion"></a>Dokončování pomocí tabulátorů rozšířené
Dokončování pomocí tabulátorů v konzole Windows PowerShell teď dokončení názvy rutin, parametry, hodnoty parametrů, výčty, rozhraní .NET Framework typů, COM objekty, skrytých složek a další. Funkci doplňování karta je kompletně přepsaná, na základě nový analyzátor a abstraktního syntaktického stromu pro podporu více scénářů, včetně analýzy stromové struktury v paměti a dokončování pomocí tabulátorů středovou.

### <a name="module-auto-loading"></a>Automatické načítání modulu
[Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) rutiny nyní získá všechny rutiny a funkce z všechny moduly, které jsou nainstalovány v počítači, i když není modul naimportovat do aktuální relace.

Když získáte rutiny, které potřebujete, můžete ji okamžitě bez import všech modulů. Moduly prostředí Windows PowerShell jsou nyní automaticky importován při použití jakékoli rutině v modulu. Již nepotřebujete vyhledejte modul a importovat ho na použití jeho rutinu.

Automatické importu modulů se aktivuje při spuštění pomocí rutiny v příkazu, **Get-Command** pro rutinu bez zástupných znaků nebo spuštění [Get-Help](https://technet.microsoft.com/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) pro rutinu bez zástupných znaků.

Můžete povolit, zakázat a nakonfigurovat automatické importu modulů pomocí **$PSModuleAutoLoadingPreference** preferenční proměnné.

Další informace najdete v tématu [týkajícím se modulů [verze 4]](https://technet.microsoft.com/library/94f57429-a539-4aee-bb0d-205cd7e801f9), [about_Preference_Variables [v4]](https://technet.microsoft.com/library/31344314-be29-4286-b039-afa5460cbe8b)a témata nápovědy [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) a [Import-Module ](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) rutiny.

### <a name="module-experience-improvements"></a>Vylepšení prostředí modulu
Prostředí Windows PowerShell 3.0 přináší podporu pokročilých funkcí pro moduly, včetně následující nové funkce.

1. Modul protokolování pro jednotlivé moduly (LogPipelineExecutionDetails) a nové nastavení zásad skupiny "Zapnout na modulu protokolování"

2. Rozšířených objektů modulu, které zveřejňují hodnoty z manifestu modulu

3. Nové **ExportedCommands** vlastnost modulů, včetně vnořené moduly, které kombinuje příkazy všech typů

4. Vylepšené zjišťování k dispozici (zrušení importovaných) modulů, včetně, což **cesta** a **ListAvailable** parametry v jednom příkazu

5. Nové **DefaultCommandPrefix** klíče v manifesty modulů, které zabraňuje konfliktu názvů beze změny kódu modulu.

6. Vylepšené modulu požadavky, včetně plně kvalifikovaný požadované moduly s verzí a identifikátor GUID a automatického importu požadované moduly

7. Tišším, možnosti efektivní fungování [New-ModuleManifest](https://technet.microsoft.com/library/512adced-f42f-4e88-ba7c-834fc9e5d047) rutiny.

8. Nové **modulu** parametr pro #Requires

9. Vylepšené [Import-Module](https://technet.microsoft.com/library/af616c24-e122-4098-930e-1e3ea2080ade) rutiny s oběma **MinimumVersion** a **RequiredVersion** parametry.

### <a name="simplified-command-discovery"></a>Zjednodušená příkaz zjišťování
Už je nutné importovat všechny moduly, které chcete zjistit, příkazy, které jsou k dispozici do relace. V prostředí Windows PowerShell 3.0 [Get-Command](https://technet.microsoft.com/library/59c6d302-6e8c-48b7-a6f6-f0172df936ad) rutiny získá všechny příkazy z všechny nainstalované moduly. A pokud chcete použít příkaz, je automaticky importují do relace modul, který exportuje příkaz.

Nové [zobrazit příkaz](https://technet.microsoft.com/library/65bba50b-91a8-49d5-80a2-a30fc684ba41) rutiny je určený pro začátečníky. Můžete vyhledat příkazů v okně. Můžete zobrazit všechny příkazy nebo filtrovat podle modulu, importovat modul klepnutím na tlačítko, použijte textová pole a rozevírací seznamy vytvořit platný příkaz a poté zkopírujte nebo spuštěním příkazu, aniž byste opustili okna.

### <a name="improved-logging-diagnostics-and-group-policy-support"></a>Vylepšené protokolování diagnostiky a podpora zásad skupiny
Prostředí Windows PowerShell 3.0 zlepšuje protokolování a trasování podporu pro příkazy a moduly s podporou pro trasování událostí v protokolech systému Windows (ETW), upravitelné **LogPipelineExecutionDetails** vlastnost modulů a "zapnout v modulu Protokolování"skupina nastavení zásad. Nyní můžete z podrobnosti protokolu zobrazením vlastností protokolu získat hodnoty parametrů.

### <a name="formatting-and-output-improvements"></a>Formátování a vylepšení výstup
Nové formátování a výstup vylepšení zlepšit efektivitu všichni uživatelé v prostředí Windows PowerShell. Mezi vylepšení patří výstupní přesměrování pro všechny datové proudy, rozšířené rutiny typ aktualizace, která přidává typy dynamicky bez Format.ps1xml souborů, zalamování řádků ve výstupu, výchozí formátování vlastnosti vlastní objekty, **PSCustomObject** typu, vylepšené formátování pro objekty rozhraní WMI a heterogenní objekty a podporu pro zjišťování přetížení metody.

### <a name="enhanced-console-host-experience"></a>Prostředí hostitele rozšířené konzoly
Program hostitele konzoly prostředí Windows PowerShell obsahuje nové funkce v prostředí Windows PowerShell 3.0 ve výchozím nastavení včetně jeden model typu apartment. Nové možnosti "Spustit s PowerShell" v Průzkumníku souborů umožňuje spouštět skripty v relaci neomezený právě kliknutím pravým tlačítkem myši. Nové konzoly hostitele spuštění logiku rychleji spustí prostředí Windows PowerShell a nová písma umožňují přizpůsobit okno prostředí známé konzoly.

Další informace najdete v tématu [about_Run_With_PowerShell](https://technet.microsoft.com/library/c9d9ca5f-eff9-4409-be9d-e43b5b4087eb).

### <a name="new-cmdlet-and-hosting-apis"></a>Nové rutiny a hostování rozhraní API
Nové rutiny API a hostování rozhraní API obsahují veřejné rozšířené syntaxe stromu (AST) rozhraní API a rozhraní API pro kanálu stránkování, vnořené kanály, dokončování pomocí tabulátorů fondy prostředí runspace, Windows RT, atribut zastaralé rutiny a operaci a podstatné jméno vlastnosti objektu FunctionInfo.

### <a name="performance-improvements"></a>Vylepšení výkonu
Výrazné vylepšení výkonu v prostředí Windows PowerShell pochází z nové analyzátor jazyka, který je založený na modulu Runtime DLR (Dynamic Language) v rozhraní .NET Framework 4., společně s kompilace skriptu runtime, modul vylepšení spolehlivosti a změny algoritmus [Get-ChildItem](https://technet.microsoft.com/library/75cf79bb-4db6-4a67-8c36-3d20754e2190) , zvýšit jeho výkon, zejména v případě, že hledání síťové sdílené složky.

### <a name="runas-and-shared-host-support"></a>RunAs a podpory sdílené hostitelů
Prostředí Windows PowerShell 3.0 zahrnuje podporu pro funkce RunAs a sdílené hostitele.

*RunAs* funkce, které jsou určené pro pracovní postup prostředí Windows PowerShell, umožňuje uživatelům konfiguraci relace, vytváření relací, které spustit s oprávněním sdíleného uživatelského účtu. To umožňuje méně privilegovaní uživatelé spouštět určité příkazy a skripty s oprávněním správce a snižuje potřebu přidává menší senior uživatele do skupiny Administrators.

**SharedHost** funkce umožňuje více uživatelům na několika počítačích pro připojení k relaci workflowu souběžně a sledovat průběh pracovního postupu. Uživatelé mohou spustit pracovní postup na jednom počítači a potom se připojte k relaci workflowu na jiném počítači bez odpojení relace z původního počítače. Uživatelé musí mít stejná oprávnění a používat stejné konfiguraci relace. Další informace najdete v tématu "Spuštěna pracovním postupu Windows PowerShell" v části Začínáme s pracovním postupem prostředí Windows PowerShell.

### <a name="special-character-handling-improvements"></a>Vylepšení zpracování speciální znak
Pro zlepšení schopnost prostředí Windows PowerShell 3.0 jak interpretovat a pracuje správně speciální znaky, **LiteralPath** parametr, který zpracovává speciální znaky v cestách, je platný na téměř všechny rutiny, které mají  **Cesta** parametr, včetně nové [Update-Help](https://technet.microsoft.com/library/93e1d870-ace6-432b-8778-8920291d7545) a [Save-Help](https://technet.microsoft.com/library/aed94f90-b73f-4e25-a25d-7c18d9f161fa) rutiny. Analyzátor také obsahuje speciální logiku ke zlepšení zpracování znaku backtick (\`) a hranaté závorky v názvů a cest souborů.

## <a name="see-also"></a>Viz také
- [about_Windows_PowerShell_5.0](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_windows_powershell_5.0?view=powershell-5.0)
- [Prostředí Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116)
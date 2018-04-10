# <a name="whats-new-in-powershell-core-60"></a>Co je nového v prostředí PowerShell základní 6.0

[Prostředí PowerShell Core 6.0] [ github] je nová verze prostředí PowerShell, který je platformy (Windows, systému macOS a Linux), open source a vytvořené pro heterogenní prostředí a hybridní cloud.

## <a name="moved-from-net-framework-to-net-core"></a>Přesunout z rozhraní .NET Framework na .NET Core

Základní prostředí PowerShell používá [.NET Core 2.0][] jako jeho runtime.
.NET core 2.0 umožňuje základní prostředí PowerShell pro práci na více platforem (Windows, systému macOS a Linux).
Základní prostředí PowerShell také poskytuje sada rozhraní API, které nabízí rozhraní .NET Core 2.0 pro použití v prostředí PowerShell rutin a skriptů.

Prostředí Windows PowerShell použít modul runtime rozhraní .NET Framework pro hostování modul prostředí PowerShell.
To znamená, že prostředí Windows PowerShell zpřístupní sada rozhraní API, které nabízí rozhraní .NET Framework.

Rozhraní API sdílena mezi .NET Core a rozhraní .NET Framework, které jsou definované jako součást [.NET Standard][].

Další informace o tom, jak ovlivňuje kompatibilitu modulu nebo skript základní prostředí PowerShell a prostředí Windows PowerShell najdete v tématu [Backwards compatibility pomocí prostředí Windows PowerShell](#backwards-compatibility-with-windows-powershell).

## <a name="support-for-macos-and-linux"></a>Podpora systému macOS a Linux

PowerShell teď oficiálně podporuje systému macOS a Linux, včetně:

- Windows 7, 8.1 a 10
- Windows Server 2008 R2, 2012 R2, 2016
- [Windows Server zadáte roční kanálu][semi-annual]
- Ubuntu 14.04 a 16.04, č. 17.04
- Debian 8.7 + a 9
- CentOS 7
- Red Hat Enterprise Linux 7
- OpenSUSE 42.2
- Fedora 25, 26
- macOS 10.12+

Naše komunita také přispívá balíčky pro tyto platformy, ale nejsou oficiálně podporované:

- Arch Linux
- Kali Linux
- AppImage (funguje na více platforem Linux)

Máme také experimentální (nepodporované) verze těchto platforem:

- Windows na ARM32/ARM64
- Raspbian (Stretch)

Počet změn, byly provedeny na v prostředí PowerShell Core 6.0 ke spolupráci lépe na jiné operační systémy.
Některé z nich jsou nejnovější změny, které ovlivňují také systému Windows.
Ostatní jsou pouze přítomen nebo je použít v instalacích jiný systém než Windows PowerShell jádra.

- Přidaná podpora pro nativní příkaz expanze názvů na platformách systému Unix.
- `more` Funkce respektuje sady Linux `$PAGER` a použije se výchozí hodnota `less`.
  To znamená, že teď můžete použít zástupné znaky s nativní binární soubory nebo příkazy (například `ls *.txt`). (#3463)
- Koncové lomítko je uvozena automaticky při plánování práce s argumenty nativní příkazu. (#4965)
- Ignorovat `-ExecutionPolicy` přepínače při spuštění prostředí PowerShell na platformách systému Windows, protože podepisování skriptů se aktuálně nepodporuje. (#3481)
- Pevné ConsoleHost vyhovět `NoEcho` na platformách systému Unix. (#3801)
- Opravené `Get-Help` pro podporu rozlišování malých a velkých písmen vzor odpovídající na platformách systému Unix. (#3852)
- `powershell` Přidání balíčku Man stránky

### <a name="logging"></a>Protokolování

V systému macOS, PowerShell používá nativního `os_log` rozhraní API do protokolu společnosti Apple [unified protokolování systému][os_log].
V systému Linux, PowerShell používá [Syslog][], řešení všudypřítomný protokolování.

### <a name="filesystem"></a>Systém souborů

Počet změn, byly provedeny v systému macOS a Linux pro podporu znaků filename tradičně není podporována v systému Windows:

- Cesty zadané rutiny jsou nyní vázané lomítko (jak / a \ pracovní jako oddělovače adresáře)
- Specifikaci XDG základní adresáře je nyní dodrženy a ve výchozím nastavení používá:
  - Cesta profilu systému Linux nebo macOS se nachází v `~/.config/powershell/profile.ps1`
  - Se nachází v historii cestu uložení `~/.local/share/powershell/PSReadline/ConsoleHost_history.txt`
  - Cesta k modulu uživatele se nachází v `~/.local/share/powershell/Modules`
- Podpora pro názvy souborů a složek obsahující znak dvojtečky v systému Unix. (#4959)
- Podpora pro názvy skriptu nebo úplné cesty, které mají čárkami. (#4136) (Poděkování @TimCurwick!)
- Rozpoznat, kdy `-LiteralPath` je použít k potlačení rozšíření zástupného znaku rutinám navigace. (#5038)
- Aktualizovat `Get-ChildItem` fungovat jako další * nix `ls -R` a Windows `DIR /S` nativní příkazy.
  `Get-ChildItem` nyní vrátí symbolické odkazy došlo během rekurzivní hledání a neprohledává adresáře, tyto odkazy cíl. (#3780)

### <a name="case-sensitivity"></a>Rozlišování velkých a malých písmen

Linux a systému macOS zpravidla je malá a velká písmena, zatímco Windows nerozlišuje při zachování případu.
Obecné prostředí PowerShell je malá a velká písmena.

Proměnné prostředí jsou například malá a velká písmena v systému macOS a Linux, proto velikosti písmen systému `PSModulePath` standardizované proměnné prostředí. (#3255) `Import-Module` je malá a velká písmena, když používá cestu k souboru určit název modulu. (#5097)

## <a name="support-for-side-by-side-installations"></a>Podpora instalací vedle sebe

Základní prostředí PowerShell je nainstalovaný, konfiguraci a spustit samostatně z prostředí Windows PowerShell.
Základní prostředí PowerShell má "přenosných" balíček ZIP.
Pomocí balíčku ZIP, můžete nainstalovat libovolný počet verzí libovolné místo na disku, včetně místní pro aplikaci, která přebírá prostředí PowerShell jako závislost.
Souběžně sdílená instalace usnadňuje otestovat nové verze prostředí PowerShell a migrace existující skripty v čase.
Vedle sebe, taky umožňuje zpětné kompatibility jako skripty lze připojit do konkrétních verzí, které vyžadují.

> [!NOTE]
> Ve výchozím nastavení Instalační služby MSI založené na Windows nepodporuje instalaci aktualizace na místě.
>

## <a name="renamed-powershellexe-to-pwshexe"></a>Přejmenovat `powershell(.exe)` na `pwsh(.exe)`

Binární název pro základní prostředí PowerShell byla změněna z hodnoty `powershell(.exe)` k `pwsh(.exe)`.
Tato změna umožňuje deterministickou uživatelům spouštět základní prostředí PowerShell na počítačích pro podporu prostředí Windows PowerShell vedle sebe a instalací jádra prostředí PowerShell.
`pwsh` je také mnohem kratší a jednodušší zadat.

Další změny, aby `pwsh(.exe)` z `powershell.exe`:

- Změnit první parametr poziční z `-Command` k `-File`.
  Tato změna řeší použití `#!` (neboli jako shebang) v prostředí PowerShell skripty, které se spouštějí z prostředí shell – prostředí PowerShell na jiných platforem než Windows.
  Také znamená, že můžete spouštět příkazy, jako je `pwsh foo.ps1` nebo `pwsh fooScript` bez zadání `-File`.
  Však tato změna vyžaduje, aby explicitně zadáte `-c` nebo `-Command` při pokusu o spuštění příkazy, jako je `pwsh.exe -Command Get-Command`. (#4019)
- Přijme základní prostředí PowerShell `-i` (nebo `-Interactive`) přepínač tak, aby znamenat interaktivní prostředí. (#3558) To umožňuje prostředí PowerShell má být použit jako výchozí prostředí na platformě Unix.
- Odebere parametry `-importsystemmodules` a `-psconsoleFile` z `pwsh.exe`. (#4995)
- Změnit `pwsh -version` a integrovanou nápovědu pro `pwsh.exe` vyrovnání jiných nativních nástrojů. (#4958 & #4931) (Děkujeme @iSazonov)
- Neplatný argument chybové zprávy pro `-File` a `-Command` a konzistentní se systémem Unix standardy kódy ukončení (#4573)
- Přidat `-WindowStyle` parametr v systému Windows. (#4573) Podobně instalací založených na balíček aktualizace na jiných platforem než Windows jsou místní aktualizace.

## <a name="backwards-compatibility-with-windows-powershell"></a>Zpětné kompatibility v prostředí Windows PowerShell

Cílem jádra prostředí PowerShell je zůstanou jako kompatibilní nejblíže pomocí prostředí Windows PowerShell.
Základní prostředí PowerShell používá [.NET Standard][] zajistit binární kompatibilitu s existující sestavení rozhraní .NET 2.0.
Řada modulů Powershellu závisí na těchto sestavení (často časy DLL), takže .NET Standard umožňuje pracovat s .NET Core.
Základní prostředí PowerShell také zahrnuje Heuristika k prohledání známých složek – například kde do globální mezipaměti sestavení se obvykle nachází na disku--najít knihovnu DLL rozhraní .NET Framework závislosti.

Další informace o .NET Standard na [blogu .NET][], v tomto [YouTube][] video a to prostřednictvím [– nejčastější dotazy][] na Githubu.

Byly provedeny nejlepší ve snaze zajistit, aby na jazyk a "integrované" moduly Powershellu (jako je `Microsoft.PowerShell.Management`, `Microsoft.PowerShell.Utility`atd) fungovat stejně jako v prostředí Windows PowerShell.
V mnoha případech za pomoci komunity jsme přidali nové funkce a opravy chyb do těchto rutin.
V některých případech se z důvodu chybějící závislosti ve vrstvách základní rozhraní .NET funkce byla odebrána, nebo není k dispozici.

Většina modulů, které se dodávají jako součást systému Windows (například `DnsClient`, `Hyper-V`, `NetTCPIP`, `Storage`atd) a další produkty společnosti Microsoft, včetně Azure a Office nebyly *explicitně* která je součástí. Ještě NET jádra.
Prostředí PowerShell tým pracuje s tyto skupiny produktů a týmy ověření a portem, jejich stávající moduly Powershellu jádra.
Pomocí rozhraní .NET Standard a [CDXML][], řadu tyto tradiční moduly prostředí Windows PowerShell se zdá, že fungují v prostředí PowerShell jádra, ale nebyly byl oficiálně ověřen a nejsou oficiálně podporované.

Nainstalováním [ `WindowsPSModulePath` ] [ windowspsmodulepath] modul, můžete použít moduly prostředí Windows PowerShell připojením prostředí Windows PowerShell `PSModulePath` pro vaše prostředí PowerShell základní `PSModulePath`.

Nejdřív nainstalujte `WindowsPSModulePath` modulu z Galerie prostředí PowerShell:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

Po instalaci tohoto modulu, spusťte `Add-WindowsPSModulePath` rutiny prostředí Windows PowerShell přidat `PSModulePath` na jádro prostředí PowerShell:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="docker-support"></a>Podpora docker

Základní prostředí PowerShell přidává podporu pro Docker kontejnery pro hlavní platformy podporujeme (včetně více distribucích systému Linux, Windows Server Core a Nano Server).

Úplný seznam, projděte si značek na [ `microsoft/powershell` na úložiště Docker Hub][docker-hub].
Další informace o Docker a základní prostředí PowerShell najdete v tématu [Docker][] na Githubu.

## <a name="ssh-based-powershell-remoting"></a>Vzdálená komunikace prostředí PowerShell založeného na protokolu SSH

Protokol vzdálenou komunikaci prostředí PowerShell (PSRP) pomocí protokolu Secure Shell (SSH) kromě tradičních na základě WinRM PSRP nyní pracuje.

To znamená, že můžete použít rutiny jako `Enter-PSSession` a `New-PSSession` a provést ověření pomocí SSH.
Stačí je zaregistrovat prostředí PowerShell jako subsystém se serverem na základě OpenSSH SSH, a můžete použít stávající založeného na protokolu SSH ověření mechanismy (třeba hesla nebo privátní klíče) s tradiční `PSSession` sémantiku.

Další informace o konfiguraci a použití založeného na protokolu SSH vzdálené komunikace najdete v tématu [vzdálenou komunikaci prostředí PowerShell přes protokol SSH][ssh-remoting].

## <a name="default-encoding-is-utf-8-without-a-bom-except-for-new-modulemanifest"></a>Výchozím kódováním je UTF-8 bez BOM s výjimkou New-ModuleManifest

V minulosti, rutiny prostředí Windows PowerShell jako `Get-Content`, `Set-Content` použít různá kódování, například ASCII nebo UTF-16.
Odchylky v kódování výchozí nastavení vytvoří problémy při kombinování rutiny bez zadání kódování.

Znakové sady UTF-8 bez značky pořadí bajtů (BOM) nejsou pro Windows platformy tradičně používají jako výchozí kódování pro textové soubory.
Více aplikací systému Windows a nástroje jsou přesunutí od UTF-16 a směrem kódování BOM bez znakové sady UTF-8.
Základní prostředí PowerShell změní výchozí kódování, aby odpovídal širší ekosystémů.

To znamená, že všechny integrované rutiny, které používají `-Encoding` použití parametrů `UTF8NoBOM` hodnotu ve výchozím nastavení.
Tato změna se týká následující rutiny:

- Přidání obsahu
- Export-Clixml
- Export-Csv
- Export-PSSession
- Rutina Format-Hex
- Get obsahu
- Import-Csv
- Out-File
- Vyberte řetězec
- Poštovní odesílání – zpráva
- Obsah sady

Tyto rutiny také byly aktualizovány tak, aby `-Encoding` parametr všeobecně přijímá `System.Text.Encoding`.

Výchozí hodnota `$OutputEncoding` také byl změněn na UTF-8.

Jako osvědčený postup, byste měli explicitně nastavit kódování ve skriptech pomocí `-Encoding` parametr k vytvoření deterministické chování napříč platformami.

`New-ModuleManifest` rutina nemá **kódování** parametr. Kódování souboru manifestu (.psd1) modulu vytvořené pomocí `New-ModuleManifest` rutiny závisí na prostředí: Pokud je základní prostředí PowerShell systémem Linux pak kódováním je UTF-8 (žádné BOM); jinak kódováním je UTF-16 (s BOM). (#3940)

## <a name="support-backgrounding-of-pipelines-with-ampersand--3360"></a>Podpora backgrounding z kanálů s ampersand (`&`) (#3360)

Vložení `&` na konci kanálu způsobí, že kanál spustit jako úlohu prostředí PowerShell.
Když je backgrounded kanál, se vrátí objekt úlohy.
Jakmile kanálu pracuje jako úlohu, všechny standardní `*-Job` rutiny můžete použít ke správě úlohy.
Proměnné (ignorována specifické pro proces proměnné) používané v kanálu se automaticky zkopírují do úlohy tak `Copy-Item $foo $bar &` prostě funguje.
V aktuálním adresáři místo uživatele domovský adresář je také spuštění úlohy.
Další informace o úlohách prostředí PowerShell najdete v tématu [about_Jobs](https://msdn.microsoft.com/powershell/reference/6/about/about_jobs).

## <a name="semantic-versioning"></a>Sémantické verze

- Provedené `SemanticVersion` kompatibilní s `SemVer 2.0`. (#5037) (Děkujeme @iSazonov!)
- Změnit výchozí `ModuleVersion` v `New-ModuleManifest` k `0.0.1` vyrovnání SemVer. (#4842) (Děkujeme @LDSpits)
- Přidat `semver` jako typ akcelerátoru pro `System.Management.Automation.SemanticVersion`. (#4142) (Poděkování @oising!)
- Porovnání mezi povolené `SemanticVersion` instance a `Version` instance, který je sestavený pouze s `Major` a `Minor` hodnoty verze.

## <a name="language-updates"></a>Jazyky aktualizací

- Implementujte Unicode řídicí analýza tak, aby uživatelé můžou použít znaky Unicode jako argumenty, řetězce nebo názvy proměnných. (#3958) (Poděkování @rkeithhill!)
- Přidání nové řídicí znak pro ESC: `` `e``
- Přidaná podpora pro převod výčty do řetězce (#4318) (Děkujeme @KirkMunro)
- Pole pevné přetypování jeden element pro obecnou kolekci. (#3170)
- Přetížení rozsah přidané znak `..` operátor, takže `'a'..'z'` vrátí znaků od 'a' do 'z'. (#5026) (Děkujeme @IISResetMe!)
- Pevné přiřazení proměnné není přepsat. proměnné jen pro čtení
- Nabízená lokální automatické proměnné 'DottedScopes, když dotting skript rutiny (#4709)
- Povolit použití možnosti 'Jednořákový, víceřádkového výrazu' v rozdělení operátoru (#4721) (Děkujeme @iSazonov)

## <a name="engine-updates"></a>Aktualizací stroje

- `$PSVersionTable` má čtyři nové vlastnosti:
  - `PSEdition`: Tato hodnota je nastavena `Core` na základní prostředí PowerShell a `Desktop` na prostředí Windows PowerShell
  - `GitCommitId`: Jedná se o ID potvrzení Git Git větev nebo značky, které bylo vytvořeno prostředí PowerShell.
    U vydaných sestavení, pravděpodobně bude stejná jako `PSVersion`.
  - `OS`: Toto je řetězec verze operačního systému vrácené `[System.Runtime.InteropServices.RuntimeInformation]::OSDescription`
  - `Platform`: Toto je vrácen rutinou `[System.Environment]::OSVersion.Platform` je nastaven na hodnotu `Win32NT` v systému Windows, `Unix` v systému macOS, a `Unix` v systému Linux.
- Odebrat `BuildVersion` vlastnost z `$PSVersionTable`.
  Tato vlastnost byla důrazně vázaný na verzi Windows sestavení.
  Místo toho doporučujeme používat `GitCommitId` načíst verzi přesný sestavení jádra prostředí PowerShell. (#3877) (Poděkování @iSazonov!)
- Odebrat `ClrVersion` vlastnost z `$PSVersionTable`.
  Tato vlastnost je důležité pro .NET Core a bylo zachováno pouze v .NET Core pro konkrétní účely starší verze, které jsou nepoužitelných prostředí PowerShell.
- Přidat tři nové automatické proměnné k určení, zda je spuštěn prostředí PowerShell v dané operačního systému: `$IsWindows`, `$IsMacOs`, a `$IsLinux`.
- Přidat `GitCommitId` nápis základní prostředí PowerShell.
  Teď není nutné spustit `$PSVersionTable` při spuštění prostředí PowerShell získat verzi! (#3916) (Poděkování @iSazonov!)
- Přidejte konfigurační soubor JSON s názvem `powershell.config.json` v `$PSHome` k uložení některých nastavení potřebné před časem spuštění (například `ExecutionPolicy`).
- Nedošlo k blokování kanálu při spuštění Windows EXE
- Povoleno výčtu COM kolekcí. (#4553)

## <a name="cmdlet-updates"></a>Rutina aktualizace

### <a name="new-cmdlets"></a>Nové rutiny

- Přidat `Get-Uptime` k `Microsoft.PowerShell.Utility`.
- Přidat `Remove-Alias` příkaz. (#5143) (Děkujeme @PowershellNinja!)
- Přidat `Remove-Service` modulu správy. (#4858) (Děkujeme @joandrsn!)

### <a name="web-cmdlets"></a>Rutiny Web

- Přidáte podporu ověřování certifikátu pro rutiny web. (#4646) (Děkujeme @markekraus)
- Přidáte podporu pro hlavičky obsahu do rutiny web. (#4494 & #4640) (Děkujeme @markekraus)
- Podpora více záhlaví odkaz přidejte do rutiny Web. (#5265) (Děkujeme @markekraus!)
- Podporu stránkování záhlaví odkaz v rutiny webových (#3828)
  - Pro `Invoke-WebRequest`, pokud odpověď obsahuje hlavičku odkaz vytvoříme vlastnost RelationLink jako slovník reprezentující adresy URL a `rel` atributy a zajistěte aby bylo snazší pro vývojáře používat absolutní adresy URL.
  - Pro `Invoke-RestMethod`, pokud odpověď obsahuje hlavičku odkaz zveřejňujeme `-FollowRelLink` přepínač tak, aby automaticky podle `next` `rel` odkazy, dokud již neexistují nebo jednou jsme dosáhl nepovinný `-MaximumFollowRelLink` hodnota parametru.
- Přidat `-CustomMethod` parametru rutiny web umožňující nestandardní metoda akce. (#3142) (Poděkování @Lee303!)
- Přidat `SslProtocol` podporují rutiny Web. (#5329) (Děkujeme @markekraus!)
- Přidat Multipart podporu, aby rutiny web. (#4782) (Děkujeme @markekraus)
- Přidat `-NoProxy` do rutiny web tak, aby se ignorovat systémová nastavení proxy serveru. (#3447) (Poděkování @TheFlyingCorpse!)
- Agent uživatele rutiny webových nyní hlásí platformu operačního systému (#4937) (Děkujeme @LDSpits)
- Přidat `-SkipHeaderValidation` přepnout na rutiny web pro podporu přidávání záhlaví bez ověření hodnota hlavičky. (#4085)
- Povolte rutiny webových neověří certifikát HTTPS serveru podle potřeby.
- Přidejte do rutiny webových parametry ověřování. (#5052) (Děkujeme @markekraus)
  - Přidat `-Authentication` poskytuje tři možnosti: Basic, OAuth a nosiče.
  - Přidat `-Token` se získat token nosiče OAuth a nosiče možnosti.
  - Přidat `-AllowUnencryptedAuthentication` obejít ověřování, který je k dispozici pro žádné schéma přenosu než protokol HTTPS.
- Přidat `-ResponseHeadersVariable` k `Invoke-RestMethod` povolit zaznamenávání hlavičky odpovědi. (#4888) (Děkujeme @markekraus)
- Opravte rutiny webových do odpovědi HTTP zahrnout v výjimce stavový kód odpovědi není úspěšná. (#3201)
- Změnit rutiny webových `UserAgent` z `WindowsPowerShell` k `PowerShell`. (#4914) (Děkujeme @markekraus)
- Přidejte explicitní `ContentType` zjišťování, aby `Invoke-RestMethod` (#4692)
- Opravte rutiny webových `-SkipHeaderValidation` pro práci s nestandardní hlavičky User-Agent. (#4479 & #4512) (Děkujeme @markekraus)

### <a name="json-cmdlets"></a>Rutiny JSON

- Přidat `-AsHashtable` k `ConvertFrom-Json` vrátit `Hashtable` místo. (#5043) (Děkujeme @bergmeister!)
- Použít prettier formátovací modul s `ConvertTo-Json` výstup. (#2787) (Poděkování @kittholland!)
- Přidat `Jobject` serializace podporu, aby `ConvertTo-Json`. (#5141)
- Opravte `ConvertFrom-Json` k deserializaci pole řetězců z kanálu, které společně vytvořit úplný řetězec formátu JSON.
  To opravy některých případech, kde by vložení znaků newline rozdělit JSON analýze. (#3823)
- Odeberte `AliasProperty "Count"` definované pro `System.Array`.
  Odebere se tak nadbytečné `Count` vlastnost u některých `ConvertFrom-Json` výstup. (#3231) (Poděkování @PetSerAl!)

### <a name="csv-cmdlets"></a>Rutiny sdíleného svazku clusteru

- Přidat `PSTypeName` podporu pro `Import-Csv` a `ConvertFrom-Csv`. (#5389) (Děkujeme @markekraus!)
- Ujistěte se, `Import-Csv` podporu `CR`, `LF`, a `CRLF` jako řádek oddělovače. (#5363) (Děkujeme @iSazonov!)
- Ujistěte se, `-NoTypeInformation` výchozí na `Export-Csv` a `ConvertTo-Csv`. (#5164) (Děkujeme @markekraus)

### <a name="service-cmdlets"></a>Rutiny pro

- Přidání vlastnosti `UserName`, `Description`, `DelayedAutoStart`, `BinaryPathName`, a `StartupType` k `ServiceController` objektů vrácený `Get-Service`. (#4907) (Děkujeme @joandrsn)
- Přidání funkce nastavování přihlašovací údaje pro `Set-Service` příkaz. (#4844) (Děkujeme @joandrsn)

### <a name="other-cmdlets"></a>Ostatní rutiny

- Přidat parametr, který se `Get-ChildItem` názvem `-FollowSymlink` ten, který prochází symbolických odkazů na vyžádání, se kontroluje odkaz smyčky. (#4020)
- Aktualizace `Add-Type` pro podporu `CSharpVersion7`. (#3933) (Poděkování @iSazonov)
- Odeberte `Microsoft.PowerShell.LocalAccounts` modulu kvůli použití nepodporované rozhraní API, dokud nebude nalezen lepší řešení. (#4302)
- Odeberte `*-Counter` rutiny v `Microsoft.PowerShell.Diagnostics` kvůli použití nepodporované rozhraní API, dokud nebude nalezen lepší řešení. (#4303)
- Přidání podpory pro `Invoke-Item -Path <folder>`. (#4262)
- Přidat `-Extension` a `-LeafBase` přepne do `Split-Path` tak, aby můžete rozdělit cest mezi příponu názvu souboru a zbytek název souboru. (#2721) (Poděkování @powercode!)
- Přidání parametrů `-Top` a `-Bottom` k `Sort-Object` pro řazení horní nebo dolní N
- Vystavení proces nadřazeného procesu přidáním `CodeProperty "Parent"` k `System.Diagnostics.Process`. (#2850) (Poděkování @powercode!)
- Použití MB místo KB paměti sloupce `Get-Process`
- Přidat `-NoNewLine` přepínač pro `Out-String`. (#5056) (Děkujeme @raghav710)
- `Move-Item` rutiny ctí `-Include`, `-Exclude`, a `-Filter` parametry. (#3878)
- Povolit `*` mají být použity v cesta v registru pro `Remove-Item`. (#4866)
- Přidat `-Title` k `Get-Credential` a sjednocení výzva prostředí napříč platformami.
- Přidat `-TimeOut` parametru `Test-Connection`. (#2492)
- `Get-AuthenticodeSignature` rutiny nyní můžete získat časové razítko podpis souboru. (#4061)
- Odeberte nepodporované `-ShowWindow` přejít z `Get-Help`. (#4903)
- Opravte `Get-Content -Delimiter` možnost Nezahrnovat elementy pole oddělovač, který vrátil (#3706) (Děkujeme @mklement0)
- Přidat `Meta`, `Charset`, a `Transitional` parametry, které `ConvertTo-HTML` (#4184) (Děkujeme @ergo3114)
- Přidat `WindowsUBR` a `WindowsVersion` vlastnosti, které chcete `Get-ComputerInfo` výsledek
- Přidat `-Group` parametru `Get-Verb`
- Přidat `ShouldProcess` podporují `New-FileCatalog` a `Test-FileCatalog` (opravy `-WhatIf` a `-Confirm`). (#3074) (Poděkování @iSazonov!)
- Přidat `-WhatIf` přepnout `Start-Process` rutiny (#4735) (Děkujeme @sarithsutha)
- Přidat `ValidateNotNullOrEmpty` existující příliš mnoho parametrů.

## <a name="tab-completion"></a>Dokončování pomocí tabulátorů

- Rozšířené odvození typu v dokončování pomocí tabulátorů na základě hodnot proměnných runtime. (#2744) (Poděkování @powercode!) To umožňuje dokončování pomocí tabulátorů v situacích, jako jsou:

  ```powershell
  $p = Get-Process
  $p | Foreach-Object Prio<tab>
  ```

- Přidat dokončování pomocí tabulátorů zatřiďovací tabulky pro `-Property` z `Select-Object`. (#3625) (Poděkování @powercode)
- Povolit automatické dokončování argument pro `-ExcludeProperty` a `-ExpandProperty` z `Select-Object`. (#3443) (Poděkování @iSazonov!)
- Opravte chyby v dokončování pomocí tabulátorů aby `native.exe --<tab>` volání do nativního dokončení. (#3633) (Poděkování @powercode!)

## <a name="breaking-changes"></a>Nejnovější změny

Zavedli jsme řadu nejnovějších změn v prostředí PowerShell Core 6.0.
Další informace o nich podrobně, najdete v části [nejnovějších změn v prostředí PowerShell Core 6.0][breaking-changes].

## <a name="debugging"></a>Ladění

- Podpora pro vzdálené step-in ladění pro `Invoke-Command -ComputerName`. (#3015)
- Povolení protokolování v prostředí PowerShell základní vazač ladění

## <a name="filesystem-updates"></a>Aktualizace systému souborů

- Povolte použití zprostředkovatele systému souborů z cesty UNC. ($4998)
- `Split-Path` nyní pracuje s kořeny UNC
- `cd` bez argumentů nyní chová jako `cd ~`
- Opravené základní prostředí PowerShell k povolení použití cesty, které jsou větší než 260 znaků dlouhé. (#3960)

## <a name="bug-fixes-and-performance-improvements"></a>Opravy chyb a vylepšení výkonu

Provedli jsme *mnoho* vylepšení výkonu v prostředí PowerShell, včetně čas spuštění, různé integrované rutiny a interakci s nativní binární soubory.

Vyřešili jsme také počet chyb v rámci základní prostředí PowerShell.
Úplný seznam opravy a změny, podívejte se na naše [protokol změn][] na Githubu.

## <a name="telemetry"></a>Telemetrie

- Základní 6.0 přidat telemetrie prostředí PowerShell k hostiteli konzoly a sestav dvě hodnoty (#3620):
  - Platforma operačního systému (`$PSVersionTable.OSDescription`)
  - přesné verze prostředí PowerShell (`$PSVersionTable.GitCommitId`)

Pokud se chcete odhlásit tuto telemetrii, jednoduše odstranit `$PSHome\DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` nebo vytvořte `POWERSHELL_TELEMETRY_OPTOUT` proměnnou prostředí s jedním z následujících hodnot: `true`, `1` nebo `yes`.
Odstranění tohoto souboru nebo vytváření proměnné obchází všechny telemetrická data i před prvním spuštěním prostředí PowerShell.
Plánujeme také na vystavení tato data telemetrie a statistiky jsme glean z telemetrických dat v [řídicí panel komunity][community-dashboard].
Můžete najít další informace o tom, jak tato data používáme v tomto [příspěvku na blogu][telemetry-blog].

[github]: https://github.com/PowerShell/PowerShell
[.NET Core 2.0]: https://docs.microsoft.com/dotnet/core/
[.NET Standard]: https://docs.microsoft.com/en-us/dotnet/standard/net-standard
[os_log]: https://developer.apple.com/documentation/os/logging
[Syslog]: https://en.wikipedia.org/wiki/Syslog
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[breaking-changes]: https://github.com/PowerShell/PowerShell/tree/master/docs/BREAKINGCHANGES.md
[protokol změn]: https://github.com/PowerShell/PowerShell/tree/master/CHANGELOG.md
[community-dashboard]: https://aka.ms/PSGitHubBI
[telemetry-blog]: https://blogs.msdn.microsoft.com/powershell/2017/01/31/powershell-open-source-community-dashboard/
[Standardní rozhraní .NET]: https://docs.microsoft.com/dotnet/standard/net-standard
[blogu .NET]: https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard
[YouTube]: https://www.youtube.com/watch?v=YI4MurjfMn8&list=PLRAdsfhKI4OWx321A_pr-7HhRNk7wOLLY
[– nejčastější dotazy]: https://github.com/dotnet/standard/blob/master/docs/faq.md
[CDXML]: https://msdn.microsoft.com/library/jj542525(v=vs.85).aspx
[docker-hub]: https://hub.docker.com/r/microsoft/powershell/
[docker]: https://github.com/PowerShell/PowerShell/tree/master/docker
[windowspsmodulepath]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
---
title: Co je nového v Powershellu Core 6.0
description: Nové funkce a změny vydané ve Windows Powershellu 6.0
ms.date: 08/06/2018
ms.openlocfilehash: 83c104d838db9d86fe1d485e92245a9c8f2d2057
ms.sourcegitcommit: 59e568ac9fa8ba28e2c96932b7c84d4a855fed2f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46289238"
---
# <a name="whats-new-in-powershell-core-60"></a>Co je nového v Powershellu Core 6.0

[Windows Powershellu 6.0] [ github] je nová edice Powershellu, které jsou víc platforem (Windows, macOS a Linux), open source a vytvořené pro heterogenní prostředí a hybridní cloud.

## <a name="moved-from-net-framework-to-net-core"></a>Přesunout z rozhraní .NET Framework do .NET Core

PowerShell Core používá [.NET Core 2.0][] jako jeho modulu runtime.
.NET core 2.0 umožňuje PowerShell Core pracovat na více platforem (Windows, macOS a Linux).
PowerShell Core také poskytuje sadu rozhraní API nabízí .NET Core 2.0 pro použití v rutin a skriptů Powershellu.

K hostování Powershellového jádra prostředí Windows PowerShell používá modul runtime rozhraní .NET Framework.
To znamená, že prostředí Windows PowerShell poskytuje sada rozhraní API, které nabízí rozhraní .NET Framework.

Rozhraní API sdílené mezi .NET Core a .NET Framework jsou definované jako součást [.NET Standard][].

Další informace o tom, jak ovlivňuje kompatibilitu modulu nebo skript PowerShell Core a prostředí Windows PowerShell najdete v tématu [Backwards compatibility pomocí Windows Powershellu](#backwards-compatibility-with-windows-powershell).

## <a name="support-for-macos-and-linux"></a>Podpora pro macOS a Linux

Prostředí PowerShell teď oficiálně podporuje macOS a Linux, včetně:

- Windows 7, 8.1 a 10
- Windows Server 2008 R2, 2012 R2, 2016
- [Windows Server prostřednictvím půlročního kanálu][semi-annual]
- Ubuntu 14.04 a 16.04, č. 17.04
- Debian 8.7 + a 9
- CentOS 7
- Red Hat Enterprise Linux 7
- OpenSUSE 42.2
- Fedora 25, 26
- macOS 10.12 +

Naše komunita také přidal balíčky pro tyto platformy, ale nejsou oficiálně podporované:

- Arch Linux
- Kali Linux
- AppImage (funguje na různých platformách Linux)

Máme také experimentální vydání (nepodporované) pro tyto platformy:

- Windows na ARM32/ARM64
- Raspbian (roztáhnout)

Počet změn ve Windows Powershellu 6.0 byly provedeny aby to fungovalo lépe systémech než Windows.
Některé z nich jsou rozbíjející změny, které také mít vliv na Windows.
Jenom ostatní jsou k dispozici nebo není platná v jiných Windows instalacích PowerShell Core.

- Přidání podpory pro příkaz nativní podpory zástupných znaků na platformách systému Unix.
- `more` Funkce respektuje Linuxový `$PAGER` a výchozí hodnota je `less`.
  To znamená, že teď můžete použít zástupné znaky s nativní binární soubory a příkazy (například `ls *.txt`). (#3463)
- Zpětné lomítko na konci je automaticky převeden při práci s argumenty nativní příkazu. (#4965)
- Ignorovat `-ExecutionPolicy` přepnout při spouštění prostředí PowerShell na platformách než Windows, protože podepisování skriptů v tuto chvíli nepodporuje. (#3481)
- Oprava ConsoleHost případném dalším sdílení dodržovat `NoEcho` na platformách systému Unix. (#3801)
- Oprava `Get-Help` pro podporu malá a velká písmena porovnávání vzorů na platformách systému Unix. (#3852)
- `powershell` Přidat do balíčku Man stránky

### <a name="logging"></a>Protokolování

Prostředí PowerShell v systému macOS, využívá nativní `os_log` rozhraní API pro přihlášení do společnosti Apple [sjednoceného systému protokolování][os_log].
V Linuxu pomocí prostředí PowerShell [Syslog][], řešení všudypřítomná protokolování.

### <a name="filesystem"></a>Systém souborů

Počet změny byly provedeny v systémech macOS a Linux pro podporu znaky pro název souboru není tradičně podporované ve Windows:

- Cesty k rutiny jsou nezávislá na chvíli lomítko (i / a \ pracovní jako oddělovač adresářů)
- XDG Base adresářovou specifikaci je nyní dodrženy a ve výchozím nastavení používá:
  - Cesta profilu Linux nebo macOS se nachází v `~/.config/powershell/profile.ps1`
  - Historie cesta pro uložení se nachází v `~/.local/share/powershell/PSReadline/ConsoleHost_history.txt`
  - Cesta k modulu uživatele se nachází na `~/.local/share/powershell/Modules`
- Podpora pro názvy souborů a složek obsahující znak dvojtečkou v Unixu. (#4959)
- Podpora pro názvy ve skriptu nebo úplné cesty, které mají čárkami. (#4136) (K [ @TimCurwick ](https://github.com/TimCurwick)!)
- Detekce `-LiteralPath` slouží k potlačení rozšíření zástupného znaku pro rutiny navigace. (#5038)
- Aktualizovat `Get-ChildItem` fungovat jako další * nix `ls -R` a Windows `DIR /S` nativní příkazy.
  `Get-ChildItem` nyní vrací symbolické odkazy během rekurzivní hledání a neprohledává adresáře, který tyto cílové odkazy. (#3780)

### <a name="case-sensitivity"></a>Rozlišování velikosti písmen

Systémy Linux a macOS jsou často na malá a velká písmena při Windows se zachováním případ velká a malá písmena.
Obecně platí prostředí PowerShell velká a malá písmena.

Například proměnné prostředí jsou malá a velká písmena v systému macOS a Linux, tak na velikosti písmen systému `PSModulePath` standardizované proměnné prostředí. (#3255) `Import-Module` velká a malá písmena, když používá cestu k souboru zjistit název modulu. (#5097)

## <a name="support-for-side-by-side-installations"></a>Podpora pro instalace vedle sebe

PowerShell Core je nainstalovaný, nakonfigurovat a spustit samostatně z prostředí Windows PowerShell.
PowerShell Core má "přenosné" balíček ZIP.
Použití balíčků ZIP, můžete nainstalovat libovolný počet verzí kdekoli na disku, včetně místní aplikaci, která přebírá prostředí PowerShell jako závislost.
Instalace vedle sebe usnadňuje testování nových verzí Powershellu a migrace stávající skripty v čase.
Vedle sebe také umožňuje zpětné kompatibility protože skripty můžete připnout ke konkrétním verzím, které vyžadují.

> [!NOTE]
> Ve výchozím nastavení instalační program MSI založený na Windows nepodporuje instalaci aktualizace na místě.
>

## <a name="renamed-powershellexe-to-pwshexe"></a>Přejmenovat `powershell(.exe)` do `pwsh(.exe)`

Binární název pro PowerShell Core se změnil z `powershell(.exe)` k `pwsh(.exe)`.
Tato změna umožňuje deterministické uživatelům spouštět Powershellu Core v počítačích pro podporu Windows Powershellu vedle sebe a instalace Powershellu Core.
`pwsh` je také mnohem kratší a snadněji zadejte.

Další změny v `pwsh(.exe)` z `powershell.exe`:

- Změnit první poziční parametr z `-Command` k `-File`.
  Tato změna řeší použití `#!` (neboli jako shebang) v Powershellové skripty, které se spouštějí z prostředí – prostředí PowerShell na platformách než Windows.
  Také znamená, že můžete spouštět příkazy jako `pwsh foo.ps1` nebo `pwsh fooScript` bez zadání `-File`.
  Tato změna vyžaduje však, že explicitně zadat `-c` nebo `-Command` při pokusu o spuštění příkazů, jako jsou `pwsh.exe -Command Get-Command`. (#4019)
- PowerShell Core přijímá `-i` (nebo `-Interactive`) přepínač, který určuje interaktivní prostředí. (#3558) To umožňuje prostředí PowerShell, který se použije jako výchozí prostředí na platformy Unix.
- Odebrat parametry `-importsystemmodules` a `-psconsoleFile` z `pwsh.exe`. (#4995)
- Změnit `pwsh -version` a integrovanou nápovědu pro `pwsh.exe` souladu s další nativních nástrojů. (#4958 & #4931) (Díky [ @iSazonov ](https://github.com/iSazonov))
- Neplatný argument chybové zprávy pro `-File` a `-Command` a ukončovací kódy, které jsou konzistentní se systémem Unix standardy (#4573)
- Přidání `-WindowStyle` parametru ve Windows. (#4573) Obdobně instalací balíčku aktualizací na platformách než Windows se aktualizace na místě.

## <a name="backwards-compatibility-with-windows-powershell"></a>Zpětné kompatibility s prostředím Windows PowerShell

Cílem PowerShell Core je zůstane kompatibilní nejrychleji pomocí Windows Powershellu.
PowerShell Core používá [.NET Standard][] 2.0 k poskytování binární kompatibilitu s existující sestavení .NET.
Řada modulů Powershellu závisí na tato sestavení (často časy knihovny DLL), .NET Standard umožňuje pokračovat v práci s .NET Core.
PowerShell Core zahrnuje také heuristiku k oblast hledání známých složek – stejně jako ve kterém do globální mezipaměti sestavení se obvykle nachází na disku--najít závislosti mezi knihovnami DLL .NET Framework.

Další informace o .NET Standard na [Blog k .NET][], v tomto [YouTube][] videa a to prostřednictvím [NEJČASTĚJŠÍ DOTAZY][] na Githubu.

Byly provedeny maximální úsilí a zkontrolujte, že jazyk a "integrované" modulů prostředí PowerShell (jako je `Microsoft.PowerShell.Management`, `Microsoft.PowerShell.Utility`atd) fungovat stejně jako ve Windows Powershellu.
V mnoha případech pomoci komunity přidali jsme nové funkce a opravy chyb pro tyto rutiny.
V některých případech se z důvodu chybějící závislosti v .NET vrstvách byla odebrána nebo funkce není k dispozici.

Většina modulů, které se dodávají jako součást Windows (například `DnsClient`, `Hyper-V`, `NetTCPIP`, `Storage`atd) a ostatní produkty Microsoftu včetně Azure a Office nebyly *explicitně* přenést do. Ještě v .NET Core.
Prostředí PowerShell tým pracuje s těmito produktové skupiny a týmy k ověření a přenést své stávající moduly Powershellu Core.
Pomocí .NET Standard a [CDXML][]mnohé z těchto tradiční moduly Windows Powershellu se zdá, že fungují v prostředí PowerShell Core, ale nebyly byl ověřen formálně a nejsou oficiálně podporované.

Po instalaci [ `WindowsPSModulePath` ] [ windowspsmodulepath] modul, můžete použít moduly Windows Powershellu připojením prostředí Windows PowerShell `PSModulePath` k Powershellu Core `PSModulePath`.

Nejdřív nainstalujte `WindowsPSModulePath` modulu z Galerie prostředí PowerShell:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

Po instalaci tohoto modulu, spusťte `Add-WindowsPSModulePath` rutiny prostředí Windows PowerShell přidat `PSModulePath` do prostředí PowerShell Core:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="docker-support"></a>Podpora dockeru

PowerShell Core přidává podporu pro kontejnery Dockeru pro všechny hlavní platformy podporujeme (včetně více distribuce Linuxu, Windows Server Core a Nano Server).

Úplný seznam, prohlédněte si značky na [ `microsoft/powershell` na Docker Hubu][docker-hub].
Další informace o Dockeru a PowerShell Core najdete v tématu [Docker][] na Githubu.

## <a name="ssh-based-powershell-remoting"></a>Vzdálená komunikace Powershellu založeného na protokolu SSH

Protokol vzdálené komunikace prostředí PowerShell (PSRP) teď funguje s protokolem Secure Shell (SSH) kromě tradičního PSRP založených na WinRM.

To znamená, že můžete používat rutiny jako `Enter-PSSession` a `New-PSSession` a provést ověření pomocí protokolu SSH.
Vše, musíte udělat, je zaregistrovat jako subsystém pomocí SSH na základě OpenSSH serveru prostředí PowerShell, a můžete použít stávající založeného na protokolu SSH ověření mechanismy (třeba hesla nebo soukromého klíče) s tradiční `PSSession` sémantiku.

Další informace o konfiguraci a použití vzdálené komunikace založeného na protokolu SSH najdete v tématu [Vzdálená komunikace Powershellu přes SSH][ssh-remoting].

## <a name="default-encoding-is-utf-8-without-a-bom-except-for-new-modulemanifest"></a>Výchozí kódování je UTF-8 bez BOM s výjimkou ModuleManifest nový

V minulosti, jako jsou rutiny prostředí Windows PowerShell `Get-Content`, `Set-Content` používají jiné kódování, jako je například ASCII a UTF-16.
Odchylky v jako výchozí kódování vytvoří problémy při kombinování rutiny bez zadání možnosti kódování.

Platformy Windows bez tradičně pomocí kódování UTF-8 bez značky pořadí bajtů (BOM) jako výchozí kódování pro textové soubory.
Další aplikace Windows a nástroje jsou přesun směrem od UTF-16 a na UTF-8 bez BOM kódování.
PowerShell Core změní výchozí kódování, které v souladu s širší ekosystémy.

To znamená, že všechny integrované rutiny, které používají `-Encoding` použití parametrů `UTF8NoBOM` hodnota ve výchozím nastavení.
Touto změnou jsou ovlivněny následující rutiny:

- Přidání obsahu
- Export Clixml
- Export-Csv
- Export-PSSession
- Rutina Format-Hex
- Get obsah
- Import-Csv
- Out-File
- Vyberte řetězec
- Send-MailMessage
- Obsah sady

Tyto rutiny také byly aktualizovány tak, aby `-Encoding` univerzálně přijímá parametr `System.Text.Encoding`.

Výchozí hodnota `$OutputEncoding` také byl změněn na UTF-8.

Jako osvědčený postup byste měli explicitně nastavit kódování ve skriptech pomocí `-Encoding` parametr vytvoří deterministické chování napříč platformami.

`New-ModuleManifest` rutina nemá **kódování** parametru. Kódování souboru manifestu (.psd1) modulu vytvořené pomocí `New-ModuleManifest` rutiny závisí na prostředí: Pokud je Powershellu Core v Linuxu spuštěnou pak kódování je UTF-8 (BOM); v opačném případě kódování je UTF-16 (s BOM). (#3940)

## <a name="support-backgrounding-of-pipelines-with-ampersand--3360"></a>Podpora zpracování úloh na pozadí kanálů s oddělovačem (`&`) (#3360)

Vložení `&` na konci kanálu způsobí, že kanál tak, aby byla spuštěna jako úlohy prostředí PowerShell.
Když je backgrounded kanálu, se vrátí objekt úlohy.
Jakmile je spuštění kanálu jako úlohy, všechny standardní `*-Job` rutiny můžete použít ke správě úlohy.
Proměnné (ignorování specifické pro proces proměnné) používané v kanálu se automaticky zkopírují do úlohy tak `Copy-Item $foo $bar &` prostě to funguje.
Úloha je také spustit v aktuálním adresáři místo domovského adresáře uživatele.
Další informace o úloh Powershellu najdete v tématu [about_Jobs](https://msdn.microsoft.com/powershell/reference/6/about/about_jobs).

## <a name="semantic-versioning"></a>Sémantické správy verzí

- Provedené `SemanticVersion` kompatibilní s `SemVer 2.0`. (#5037) (Díky [ @iSazonov ](https://github.com/iSazonov)!)
- Změnit výchozí `ModuleVersion` v `New-ModuleManifest` k `0.0.1` souladu s SemVer. (#4842) (Díky [ @LDSpits ](https://github.com/LDSpits))
- Přidání `semver` jako typ akcelerátoru pro `System.Management.Automation.SemanticVersion`. (#4142) (K [ @oising ](https://github.com/oising)!)
- Porovnání mezi povolené `SemanticVersion` instance a `Version` instance, který je vytvořen pouze s `Major` a `Minor` hodnoty verze.

## <a name="language-updates"></a>Jazyky aktualizací

- Implementace řídicí Unicode analýza kódu tak, aby uživatelé můžou používat znaky Unicode jako argumenty, řetězce nebo názvy proměnných. (#3958) (K [ @rkeithhill ](https://github.com/rkeithhill)!)
- Přidání nové řídicí znak pro ESC: `` `e``
- Přidali jsme podporu pro převod výčty řetězce (#4318) (Děkujeme [ @KirkMunro ](https://github.com/KirkMunro))
- Oprava přetypování jediný prvek pole pro obecné kolekce. (#3170)
- Přidání znak rozsah přetížení `..` operátor, takže `'a'..'z'` vrátí znaků od "a" do "z". (#5026) (Díky [ @IISResetMe ](https://github.com/IISResetMe)!)
- Oprava přiřazení proměnné není přepsat proměnné určené jen pro čtení
- Nabídne "DottedScopes" lokální proměnné automatických proměnných, jakmile dotting rutin skriptu (#4709)
- Povolit použití možnosti "Singleline, Multiline" v rozdělení operátoru (#4721) (Děkujeme [ @iSazonov ](https://github.com/iSazonov))

## <a name="engine-updates"></a>Aktualizace vyhledávacího stroje

- `$PSVersionTable` má čtyři nové vlastnosti:
  - `PSEdition`: Toto je nastavena na `Core` v prostředí PowerShell Core a `Desktop` v prostředí Windows PowerShell
  - `GitCommitId`: Toto je ID potvrzení změn Git z Git, pobočku nebo značku, ve kterém byla vytvořena prostředí PowerShell.
    U vydaných sestavení, pravděpodobně bude stejná jako `PSVersion`.
  - `OS`: Toto je vrácený řetězec verze operačního systému `[System.Runtime.InteropServices.RuntimeInformation]::OSDescription`
  - `Platform`: Toto je vrácený `[System.Environment]::OSVersion.Platform` je nastavený na `Win32NT` na Windows, `Unix` v systému macOS a `Unix` v Linuxu.
- Odebrat `BuildVersion` vlastnost z `$PSVersionTable`.
  Tato vlastnost se silnou vazbu na verzi Windows sestavení.
  Namísto toho doporučujeme použít `GitCommitId` sestavení přesnou verzi prostředí PowerShell Core. (#3877) (K [ @iSazonov ](https://github.com/iSazonov)!)
- Odebrat `ClrVersion` vlastnost z `$PSVersionTable`.
  Tato vlastnost je relevantní pro .NET Core a bylo zachováno pouze v .NET Core pro konkrétní účely starší verze, které jsou nepoužitelných do prostředí PowerShell.
- Přidat tři nové automatické proměnné lze zjistit, zda prostředí PowerShell je spuštěn v daném operačním systémem: `$IsWindows`, `$IsMacOs`, a `$IsLinux`.
- Přidat `GitCommitId` nápis PowerShell Core.
  Nyní není nutné ke spuštění `$PSVersionTable` co nejdříve spustit prostředí PowerShell pro získání verze! (#3916) (K [ @iSazonov ](https://github.com/iSazonov)!)
- Přidejte konfigurační soubor JSON s názvem `powershell.config.json` v `$PSHome` k uložení některá nastavení vyžaduje před časem spuštění (například `ExecutionPolicy`).
- Nedošlo k blokování kanálu při spuštění Windows EXE
- Povolené výčet COM kolekcí. (#4553)

## <a name="cmdlet-updates"></a>Rutina aktualizace

### <a name="new-cmdlets"></a>Nové rutiny

- Přidat `Get-Uptime` k `Microsoft.PowerShell.Utility`.
- Přidat `Remove-Alias` příkazu. (#5143) (Díky [ @PowershellNinja ](https://github.com/PowershellNinja)!)
- Přidat `Remove-Service` pro modul pro správu. (#4858) (Díky [ @joandrsn ](https://github.com/joandrsn)!)

### <a name="web-cmdlets"></a>Rutiny Web

- Přidání podpory ověřování certifikátů pro rutiny webových. (#4646) (Díky [ @markekraus ](https://github.com/markekraus))
- Přidání podpory pro hlavičky obsahu webové rutiny. (#4494 & #4640) (Díky [ @markekraus ](https://github.com/markekraus))
- Přidání více propojení záhlaví podpory webové rutiny. (#5265) (Díky [ @markekraus ](https://github.com/markekraus)!)
- Podporujte stránkování záhlaví odkaz v rutinách web (#3828)
  - Pro `Invoke-WebRequest`, když odpověď obsahuje záhlaví odkaz vytvoříme RelationLink vlastnost jako slovník reprezentující adresy URL a `rel` atributy a ověřte adresy URL jsou absolutní, aby bylo snazší pro vývojáře k použití.
  - Pro `Invoke-RestMethod`, když odpověď obsahuje záhlaví odkaz zveřejňujeme `-FollowRelLink` přepínač tak, aby automaticky podle `next` `rel` odkazy, dokud již neexistuje, nebo jednou jsme přístupů nepovinný `-MaximumFollowRelLink` hodnotu parametru.
- Přidat `-CustomMethod` parametr pro rutiny webových umožňující nestandardní metody akce. (#3142) (K [ @Lee303 ](https://github.com/Lee303)!)
- Přidat `SslProtocol` podpory pro rutiny webových. (#5329) (Díky [ @markekraus ](https://github.com/markekraus)!)
- Přidat Multipart podpory pro rutiny webových. (#4782) (Díky [ @markekraus ](https://github.com/markekraus))
- Přidat `-NoProxy` rutinách web tak, aby ignorují systémová nastavení proxy serveru. (#3447) (K [ @TheFlyingCorpse ](https://github.com/TheFlyingCorpse)!)
- Agent uživatele rutiny webových nyní hlásí platforma operačního systému (#4937) (Děkujeme [ @LDSpits ](https://github.com/LDSpits))
- Přidat `-SkipHeaderValidation` přepnout na web rutin pro podporu přidávání záhlaví bez ověřování hodnota hlavičky. (#4085)
- Povolte webové rutiny, které nelze ověřit certifikát HTTPS ze serveru, pokud je to nutné.
- Přidejte do rutiny webových ověřovacími parametry. (#5052) (Díky [ @markekraus ](https://github.com/markekraus))
  - Přidat `-Authentication` , který poskytuje tři možnosti: Basic, OAuth a nosiče.
  - Přidat `-Token` k získání tokenu nosiče OAuth a nosiče možnosti.
  - Přidat `-AllowUnencryptedAuthentication` obejít ověřování, která je k dispozici pro žádné schéma přepravy než HTTPS.
- Přidat `-ResponseHeadersVariable` k `Invoke-RestMethod` k povolení funkce capture hlaviček odpovědí. (#4888) (Díky [ @markekraus ](https://github.com/markekraus))
- Oprava rutiny webových zahrnovat odpovědi HTTP do výjimky, pokud kód stavu odpovědi není úspěšné. (#3201)
- Změnit rutiny webových `UserAgent` z `WindowsPowerShell` k `PowerShell`. (#4914) (Díky [ @markekraus ](https://github.com/markekraus))
- Přidat explicitní `ContentType` detekci `Invoke-RestMethod` (#4692)
- Oprava rutiny webových `-SkipHeaderValidation` pro práci s nestandardní hlavičky uživatelského agenta. (#4479 & #4512) (Díky [ @markekraus ](https://github.com/markekraus))

### <a name="json-cmdlets"></a>Rutiny JSON

- Přidat `-AsHashtable` k `ConvertFrom-Json` se vraťte `Hashtable` místo. (#5043) (Díky [ @bergmeister ](https://github.com/bergmeister)!)
- Použít prettier formátovací modul s `ConvertTo-Json` výstup. (#2787) (K @kittholland!)
- Přidat `Jobject` podporu serializace `ConvertTo-Json`. (#5141)
- Oprava `ConvertFrom-Json` pole řetězců z kanálu, které společně sestavit úplný řetězec JSON deserializovat.
  To řeší některé případy, ve kterém by vložení znaků newline přerušit parsování JSON. (#3823)
- Odeberte `AliasProperty "Count"` definované pro `System.Array`.
  Tato operace odebere cizí `Count` vlastnost u některých `ConvertFrom-Json` výstup. (#3231) (K [ @PetSerAl ](https://github.com/PetSerAl)!)

### <a name="csv-cmdlets"></a>Rutiny sdíleného svazku clusteru

- Přidat `PSTypeName` podporu `Import-Csv` a `ConvertFrom-Csv`. (#5389) (Díky [ @markekraus ](https://github.com/markekraus)!)
- Ujistěte se, `Import-Csv` podporují `CR`, `LF`, a `CRLF` jako oddělovače řádků. (#5363) (Díky [ @iSazonov ](https://github.com/iSazonov)!)
- Ujistěte se, `-NoTypeInformation` výchozí `Export-Csv` a `ConvertTo-Csv`. (#5164) (Díky [ @markekraus ](https://github.com/markekraus))

### <a name="service-cmdlets"></a>Rutiny pro

- Přidání vlastností `UserName`, `Description`, `DelayedAutoStart`, `BinaryPathName`, a `StartupType` k `ServiceController` objektů vrácených podle `Get-Service`. (#4907) (Díky [ @joandrsn ](https://github.com/joandrsn))
- Přidání funkce nastavování přihlašovacích údajů na `Set-Service` příkazu. (#4844) (Díky [ @joandrsn ](https://github.com/joandrsn))

### <a name="other-cmdlets"></a>Další rutiny

- Přidat parametr `Get-ChildItem` volá `-FollowSymlink` , který prochází skrz symbolických odkazů na vyžádání s využitím zjišťuje cykly odkazů. (#4020)
- Aktualizace `Add-Type` pro podporu `CSharpVersion7`. (#3933) (K [ @iSazonov ](https://github.com/iSazonov))
- Odeberte `Microsoft.PowerShell.LocalAccounts` modul z důvodu použití nepodporované rozhraní API, dokud nebude nalezen lepší řešení. (#4302)
- Odeberte `*-Counter` rutiny v `Microsoft.PowerShell.Diagnostics` kvůli použití nepodporované rozhraní API, dokud nebude nalezen lepší řešení. (#4303)
- Přidání podpory pro `Invoke-Item -Path <folder>`. (#4262)
- Přidat `-Extension` a `-LeafBase` přepne do `Split-Path` tak, aby můžete rozdělit cesty mezi příponu názvu souboru a zbytek název souboru. (#2721) (K [ @powercode ](https://github.com/powercode)!)
- Přidání parametrů `-Top` a `-Bottom` k `Sort-Object` pro nejvyšší či nejnižší hodnoty N řazení
- Vystavovat nadřazený proces procesu tak, že přidáte `CodeProperty "Parent"` k `System.Diagnostics.Process`. (#2850) (K [ @powercode ](https://github.com/powercode)!)
- Místo KB použít MB paměti sloupce `Get-Process`
- Přidat `-NoNewLine` přepnout `Out-String`. (#5056) (Díky [ @raghav710 ](https://github.com/raghav710))
- `Move-Item` rutiny respektuje `-Include`, `-Exclude`, a `-Filter` parametry. (#3878)
- Povolit `*` použitého v cestě registru pro `Remove-Item`. (#4866)
- Přidat `-Title` k `Get-Credential` a Sjednoťte příkazový řádek prostředí napříč platformami.
- Přidat `-TimeOut` parametr `Test-Connection`. (#2492)
- `Get-AuthenticodeSignature` rutiny teď můžete mít časové razítko souboru podpisu. (#4061)
- Odeberte nepodporované `-ShowWindow` přejít z `Get-Help`. (#4903)
- Oprava `Get-Content -Delimiter` tak, aby nezahrnovala oddělovač v prvcích pole vrácená (#3706) (Děkujeme [ @mklement0 ](https://github.com/mklement0))
- Přidat `Meta`, `Charset`, a `Transitional` parametry `ConvertTo-HTML` (#4184) (Děkujeme [ @ergo3114 ](https://github.com/ergo3114))
- Přidat `WindowsUBR` a `WindowsVersion` vlastností `Get-ComputerInfo` výsledek
- Přidat `-Group` parametr `Get-Verb`
- Přidat `ShouldProcess` podporu `New-FileCatalog` a `Test-FileCatalog` (opravy `-WhatIf` a `-Confirm`). (#3074) (K [ @iSazonov ](https://github.com/iSazonov)!)
- Přidat `-WhatIf` přepnout na `Start-Process` rutiny (#4735) (Děkujeme [ @sarithsutha ](https://github.com/sarithsutha))
- Přidat `ValidateNotNullOrEmpty` příliš mnoho existujících parametrů.

## <a name="tab-completion"></a>Dokončování pomocí tabulátoru

- Vylepšené odvození typu proměnné v dokončování pomocí tabulátoru na základě hodnot proměnných runtime. (#2744) (K [ @powercode ](https://github.com/powercode)!) To umožňuje dokončování pomocí tabulátoru v situacích, jako jsou:

  ```powershell
  $p = Get-Process
  $p | Foreach-Object Prio<tab>
  ```

- Přidání dokončování pomocí tabulátoru zatřiďovací tabulky pro `-Property` z `Select-Object`. (#3625) (K [ @powercode ](https://github.com/powercode))
- Povolit automatické dokončování argument pro `-ExcludeProperty` a `-ExpandProperty` z `Select-Object`. (#3443) (K [ @iSazonov ](https://github.com/iSazonov)!)
- Oprava chyby v dokončování pomocí tabulátoru aby `native.exe --<tab>` volání do nativního dokončování. (#3633) (K [ @powercode ](https://github.com/powercode)!)

## <a name="breaking-changes"></a>Rozbíjející změny v

Zavedli jsme řadu nejnovější změny ve Windows Powershellu 6.0.
Další informace o nich podrobněji, naleznete v tématu [Breaking Changes in Windows Powershellu 6.0][breaking-changes].

## <a name="debugging"></a>Ladění

- Podpora pro vzdálené step-in ladění pro `Invoke-Command -ComputerName`. (#3015)
- Povolení protokolování v prostředí PowerShell Core ladění vazače

## <a name="filesystem-updates"></a>Aktualizace systému souborů

- Povolte použití zprostředkovatele systému souborů pomocí cesty UNC. (4998$)
- `Split-Path` nyní funguje s kořeny UNC
- `cd` bez argumentů. nyní se chová jako `cd ~`
- Oprava PowerShell Core k povolení použití cesty, které jsou více než 260 znaků dlouhé. (#3960)

## <a name="bug-fixes-and-performance-improvements"></a>Opravy chyb a vylepšení výkonu

Provedli jsme *mnoho* vylepšení výkonu v prostředí PowerShell, včetně doby spouštění různých předdefinovaných rutinách a interakci s nativní binární soubory.

Dál jsme také vyřešili několik chyb v rámci prostředí PowerShell Core.
Úplný seznam oprav a změn, podívejte se na naše [protokolu změn][] na Githubu.

## <a name="telemetry"></a>Telemetrie

- Prostředí PowerShell Core 6.0 přidali telemetrii k hostiteli konzoly sestav dvě hodnoty (#3620):
  - Platforma operačního systému (`$PSVersionTable.OSDescription`)
  - přesnou verzi prostředí PowerShell (`$PSVersionTable.GitCommitId`)

Pokud se chcete odhlásit tato telemetrie, jednoduše vytvořte `POWERSHELL_TELEMETRY_OPTOUT` proměnnou prostředí s jednou z následujících hodnot: `true`, `1` nebo `yes`.
Vytváření proměnné je vynecháno veškerou telemetrii ještě před prvním spuštění PowerShell.
Plánujeme také na vystavení tato telemetrická data a přehledy jsme glean z telemetrických dat v [řídicí panel komunity][community-dashboard].
Můžete najít další informace o tom, jak jsme tato data použít v tomto [blogový příspěvek][telemetry-blog].

[github]: https://github.com/PowerShell/PowerShell
[.NET core 2.0]: https://docs.microsoft.com/dotnet/core/
[.NET standard]: https://docs.microsoft.com/dotnet/standard/net-standard
[os_log]: https://developer.apple.com/documentation/os/logging
[Syslog]: https://en.wikipedia.org/wiki/Syslog
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[breaking-changes]: breaking-changes-ps6.md
[protokolu změn]: https://github.com/PowerShell/PowerShell/tree/master/CHANGELOG.md
[community-dashboard]: https://aka.ms/PSGitHubBI
[telemetry-blog]: https://blogs.msdn.microsoft.com/powershell/2017/01/31/powershell-open-source-community-dashboard/
[.NET standard]: https://docs.microsoft.com/dotnet/standard/net-standard
[Blog k .NET]: https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard
[YouTube]: https://www.youtube.com/watch?v=YI4MurjfMn8&list=PLRAdsfhKI4OWx321A_pr-7HhRNk7wOLLY
[NEJČASTĚJŠÍ DOTAZY]: https://github.com/dotnet/standard/blob/master/docs/faq.md
[CDXML]: https://msdn.microsoft.com/library/jj542525(v=vs.85).aspx
[docker-hub]: https://hub.docker.com/r/microsoft/powershell/
[Docker]: https://github.com/PowerShell/PowerShell/tree/master/docker
[windowspsmodulepath]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview

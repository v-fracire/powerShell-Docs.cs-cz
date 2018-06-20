---
ms.date: 05/17/2018
keywords: prostředí PowerShell, jádra
title: Nejnovější změny pro prostředí PowerShell 6.0
ms.openlocfilehash: 60ce7a1676403bb08b57bf852ba725acde86a30c
ms.sourcegitcommit: 2d9cf1ccb9a653db7726a408ebcb65530dcb1522
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/19/2018
ms.locfileid: "34309570"
---
# <a name="breaking-changes-for-powershell-60"></a>Nejnovější změny pro prostředí PowerShell 6.0

## <a name="features-no-longer-available-in-powershell-core"></a>Funkce již není k dispozici v prostředí PowerShell jádra

### <a name="powershell-workflow"></a>Pracovní postup prostředí PowerShell

[Pracovní postup Powershellu] [ workflow] je funkce v prostředí Windows PowerShell, který sestaví na [Windows Workflow Foundation (WF)] [ workflow-foundation] umožňující vytvoření Robustní sady runbook pro dlouhodobé nebo paralelizovaná málo úloh.

Z důvodu nedostatku podpory pro Windows Workflow Foundation v .NET Core jsme nebude dále podporovat pracovního postupu Powershellu v prostředí PowerShell jádra.

V budoucnu jsme chtěli povolit nativní paralelismus za souběžnosti v jazyce prostředí PowerShell, bez nutnosti pracovní postup prostředí PowerShell.

[workflow]: https://docs.microsoft.com/powershell/scripting/core-powershell/workflows-guide
[workflow-foundation]: https://docs.microsoft.com/dotnet/framework/windows-workflow-foundation/

### <a name="custom-snap-ins"></a>Vlastní moduly snap in

[Moduly snap in prostředí PowerShell] [ snapin] jsou předchůdce moduly Powershellu, které nemají všeobecné přijetí v komunitě prostředí PowerShell.

Z důvodu složitosti podpora moduly snap in a jejich nedostatečné využití v komunitě jsme již nepodporují vlastní moduly snap in v prostředí PowerShell jádra.

V současné době to dělí `ActiveDirectory` a `DnsClient` moduly v systému Windows a Windows Server.

[snapin]: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_pssnapins

### <a name="wmi-v1-cmdlets"></a>Rutiny WMI v1

Z důvodu složitosti podporu dvou sad založených na rozhraní WMI modulů jsme odebrali rutin rozhraní WMI verze 1 ze základní prostředí PowerShell:

- `Get-WmiObject`
- `Invoke-WmiMethod`
- `Register-WmiEvent`
- `Set-WmiInstance`

Místo toho doporučujeme, aby vám použití rutin modelu CIM (neboli WMI v2), které nabízí stejnou funkčnost s přepracovanou syntaxi a nové funkce:

- `Get-CimAssociatedInstance`
- `Get-CimClass`
- `Get-CimInstance`
- `Get-CimSession`
- `Invoke-CimMethod`
- `New-CimInstance`
- `New-CimSession`
- `New-CimSessionOption`
- `Register-CimIndicationEvent`
- `Remove-CimInstance`
- `Remove-CimSession`
- `Set-CimInstance`

### <a name="microsoftpowershelllocalaccounts"></a>Microsoft.PowerShell.LocalAccounts

Kvůli použití technologie nepodporované rozhraní API `Microsoft.PowerShell.LocalAccounts` byl odebrán z prostředí PowerShell základní dokud nebude nalezen lepší řešení.

### <a name="-counter-cmdlets"></a>Rutiny pro `*-Counter`

Kvůli použití technologie nepodporované rozhraní API `*-Counter` byl odebrán z prostředí PowerShell základní dokud nebude nalezen lepší řešení.

## <a name="enginelanguage-changes"></a>Modul/jazykové změny

### <a name="rename-powershellexe-to-pwshexe-5101httpsgithubcompowershellpowershellissues5101"></a>Přejmenování `powershell.exe` k `pwsh.exe` [#5101](https://github.com/PowerShell/PowerShell/issues/5101)

Chcete-li uživatelům poskytnout deterministickou způsob, jak volat základní prostředí PowerShell v systému Windows (na rozdíl od prostředí Windows PowerShell), binární základní prostředí PowerShell byl změněn na `pwsh.exe` v systému Windows a `pwsh` na jiných platforem než Windows.

Zkrácený název je také konzistentní s názvů shells aplikací na jiných platforem než Windows.

### <a name="dont-insert-line-breaks-to-output-except-for-tables-5193httpsgithubcompowershellpowershellissues5193"></a>Nevkládejte zalomením řádku výstup (s výjimkou tabulky) [#5193](https://github.com/PowerShell/PowerShell/issues/5193)

Dříve byla výstupu zarovnán šířku konzoly a zalomení řádků byly přidány na koncovou šířku konzoly, což znamená, že výstup nebyla získat naformátována podle očekávání, pokud došlo ke změně velikosti terminálu. Tato změna nebyla použita tabulky, je třeba zachovat sloupce zarovnán konce řádků.

### <a name="skip-null-element-check-for-collections-with-a-value-type-element-type-5432httpsgithubcompowershellpowershellissues5432"></a>Přeskočit kontrolu element s hodnotou null pro kolekce s typem elementu typ hodnoty [#5432](https://github.com/PowerShell/PowerShell/issues/5432)

Pro `Mandatory` parametr a `ValidateNotNull` a `ValidateNotNullOrEmpty` atributy, Přeskočit kontrolu element s hodnotou null, pokud je typ hodnoty typ elementu kolekce.

### <a name="change-outputencoding-to-use-utf-8-nobom-encoding-rather-than-ascii-5369httpsgithubcompowershellpowershellissues5369"></a>Změna `$OutputEncoding` používat `UTF-8 NoBOM` kódování místo ASCII [#5369](https://github.com/PowerShell/PowerShell/issues/5369)

Předchozí kódování, ASCII (7-bit), by způsobilo nesprávný změnou výstupu v některých případech. Tato změna se provést `UTF-8 NoBOM` výchozí, což zachovává výstup ve formátu Unicode s kódováním nepodporuje Většina nástrojů a operačních systémů.

### <a name="remove-allscope-from-most-default-aliases-5268httpsgithubcompowershellpowershellissues5268"></a>Odebrat `AllScope` z aliasy většině výchozí [#5268](https://github.com/PowerShell/PowerShell/issues/5268)

Pro urychlení vytvoření oboru `AllScope` byla odebrána z většina výchozí aliasy. `AllScope` bylo pro několik často používaných aliasy místo, kde bylo rychlejší vyhledávání.

### <a name="-verbose-and--debug-no-longer-overrides-erroractionpreference-5113httpsgithubcompowershellpowershellissues5113"></a>`-Verbose` a `-Debug` už přepsání `$ErrorActionPreference` [#5113](https://github.com/PowerShell/PowerShell/issues/5113)

Dříve Pokud `-Verbose` nebo `-Debug` byly zadány ho overrode chování `$ErrorActionPreference`. Díky této změně `-Verbose` a `-Debug` už nebude mít vliv na chování `$ErrorActionPreference`.

## <a name="cmdlet-changes"></a>Rutiny změny

### <a name="invoke-restmethod-doesnt-return-useful-info-when-no-data-is-returned-5320httpsgithubcompowershellpowershellissues5320"></a>Vyvolání RestMethod nevrací užitečné informace, pokud nebudou vrácena žádná data. [#5320](https://github.com/PowerShell/PowerShell/issues/5320)

Když se rozhraní API vrátí jenom `null`, Invoke-RestMethod to byla serializaci jako řetězec `"null"` místo `$null`. Tato změna řeší logiku `Invoke-RestMethod` správně serializovat platnou hodnotu typu single JSON `null` literálu jako `$null`.

### <a name="remove--computername-from--computer-cmdlets-5277httpsgithubcompowershellpowershellissues5277"></a>Odebrat `-ComputerName` z `*-Computer` rutiny [#5277](https://github.com/PowerShell/PowerShell/issues/5277)

Z důvodu problémů s vzdálené komunikace RPC v CoreFX (zejména v jiných platforem než Windows) a zajistit konzistentní dokonalejší prostředí v prostředí PowerShell `-ComputerName` parametr byl odebrán z `\*-Computer` rutiny. Použití `Invoke-Command` místo jako způsob, jak můžete vzdáleně spuštění rutiny.

### <a name="remove--computername-from--service-cmdlets-5090httpsgithubcompowershellpowershellissues5094"></a>Odebrat `-ComputerName` z `*-Service` rutiny [#5090](https://github.com/PowerShell/PowerShell/issues/5094)

Aby bylo možné podporovat konzistentní používání PSRP, `-ComputerName` parametr byl odebrán z `*-Service` rutiny.

### <a name="fix-get-item--literalpath-ab-if-ab-doesnt-actually-exist-to-return-error-5197httpsgithubcompowershellpowershellissues5197"></a>Opravte `Get-Item -LiteralPath a*b` Pokud `a*b` neexistuje ve skutečnosti chybu vrátit [#5197](https://github.com/PowerShell/PowerShell/issues/5197)

Dříve `-LiteralPath` daný zástupný znak by s nimi zacházet stejné `-Path` a pokud zástupného nalézt žádné soubory, by bezobslužně ukončení. Správné, musí být chování, které `-LiteralPath` je literál, takže pokud soubor neexistuje, by měl chyby. Změny se zachází zástupné znaky použít s `-Literal` jako literál.

### <a name="import-csv-should-apply-pstypenames-upon-import-when-type-information-is-present-in-the-csv-5134httpsgithubcompowershellpowershellissues5134"></a>`Import-Csv` by se měly používat `PSTypeNames` při importu, když se nachází ve sdíleném svazku clusteru informací o typu [#5134](https://github.com/PowerShell/PowerShell/issues/5134)

Dříve, exportovat objekty pomocí `Export-CSV` s `TypeInformation` importovat s `ConvertFrom-Csv` nebyly zachování informací o typu. Tato změna přidá typ informace, které `PSTypeNames` člen, pokud je k dispozici ze souboru CSV.

### <a name="-notypeinformation-should-be-default-on-export-csv-5131httpsgithubcompowershellpowershellissues5131"></a>`-NoTypeInformation` Výchozí by měla být na `Export-Csv` [#5131](https://github.com/PowerShell/PowerShell/issues/5131)

Tato změna byla provedená na názory zákazníků adresu na výchozí chování `Export-CSV` zahrnout informace o typu.

Dříve by výstup rutiny komentář jako první řádek obsahuje název typu objektu. Změna je pro toto potlačení ve výchozím nastavení jako není rozumí Většina nástrojů. Použití `-IncludeTypeInformation` Chcete-li zachovat předchozí chování.

### <a name="web-cmdlets-should-warn-when--credential-is-sent-over-unencrypted-connections-5112httpsgithubcompowershellpowershellissues5112"></a>Rutiny webových má upozornit při `-Credential` odesílané přes nezašifrované připojení [#5112](https://github.com/PowerShell/PowerShell/issues/5112)

Při použití protokolu HTTP, obsah, včetně hesel se odesílají jako prostý text. Tuto změnu je to nepovolují ve výchozím nastavení a vrátí chybu, pokud se přihlašovací údaje jsou předávány nezabezpečeným způsobem. Uživatelé mohou obejít to pomocí `-AllowUnencryptedAuthentication` přepínače.

## <a name="api-changes"></a>Rozhraní API změny

### <a name="remove-addtypecommandbase-class-5407httpsgithubcompowershellpowershellissues5407"></a>Odebrat `AddTypeCommandBase` třída [#5407](https://github.com/PowerShell/PowerShell/issues/5407)

`AddTypeCommandBase` Třída byla odebrána z `Add-Type` ke zlepšení výkonu. Tato třída se používá pouze pomocí rutiny Add-Type a by neměla mít vliv na uživatele.

### <a name="unify-cmdlets-with-parameter--encoding-to-be-of-type-systemtextencoding-5080httpsgithubcompowershellpowershellissues5080"></a>Sjednocení rutiny s parametrem `-Encoding` být typu `System.Text.Encoding` [#5080](https://github.com/PowerShell/PowerShell/issues/5080)

`-Encoding` Hodnota `Byte` byla odebrána z rutiny zprostředkovatele systému souborů. Nový parametr `-AsByteStream`, se teď používá k určení, že tok bajtů je vyžadována jako vstup nebo zda je výstup datového proudu bajtů.

### <a name="add-better-error-message-for-empty-and-null--uformat-parameter-5055httpsgithubcompowershellpowershellissues5055"></a>Přidat lepší chybovou zprávu pro prázdný a null `-UFormat` parametr [#5055](https://github.com/PowerShell/PowerShell/issues/5055)

Dříve, když předávání formátu prázdný řetězec k `-UFormat`, objeví neužitečné chybovou zprávu. Byla přidána popisnější chyby.

### <a name="clean-up-console-code-4995httpsgithubcompowershellpowershellissues4995"></a>Vyčištění konzoly kódu [#4995](https://github.com/PowerShell/PowerShell/issues/4995)

Následující funkce byly odebrat, protože nejsou podporovány v prostředí PowerShell jádra, a neexistují žádné plány přidání podpory, které jsou starší verze z důvodů pro prostředí Windows PowerShell: `-psconsolefile` přepínače a kód, `-importsystemmodules` přepínače a kód a písma Změna kódu.

### <a name="removed-runspaceconfiguration-support-4942httpsgithubcompowershellpowershellissues4942"></a>Odebrat `RunspaceConfiguration` podporu [#4942](https://github.com/PowerShell/PowerShell/issues/4942)

Dříve, při vytváření prostředí runspace prostředí PowerShell programově pomocí rozhraní API můžete použít starší verze [ `RunspaceConfiguration` ] [ runspaceconfig] nebo novější [ `InitialSessionState` ] [ iss]. Tato změna odebranou podporu architektury `RunspaceConfiguration` a podporuje pouze `InitialSessionState`.

[runspaceconfig]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.runspaceconfiguration
[iss]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.initialsessionstate

### <a name="commandinvocationintrinsicsinvokescript-bind-arguments-to-input-instead-of-args-4923httpsgithubcompowershellpowershellissues4923"></a>`CommandInvocationIntrinsics.InvokeScript` argumenty pro vytvoření vazby `$input` místo `$args` [#4923](https://github.com/PowerShell/PowerShell/issues/4923)

Nesprávná pozice parametr výsledkem argumenty předávané jako vstup místo jako argumentů.

### <a name="remove-unsupported--showwindow-switch-from-get-help-4903httpsgithubcompowershellpowershellissues4903"></a>Odeberte nepodporované `-showwindow` přejít z `Get-Help` [#4903](https://github.com/PowerShell/PowerShell/issues/4903)

`-showwindow` spoléhá na WPF, který není podporován na CoreCLR.

### <a name="allow--to-be-used-in-registry-path-for-remove-item-4866httpsgithubcompowershellpowershellissues4866"></a>Povolit * mají být použity v cesta v registru pro `Remove-Item` [#4866](https://github.com/PowerShell/PowerShell/issues/4866)

Dříve `-LiteralPath` daný zástupný znak by s nimi zacházet stejné `-Path` a pokud zástupného nalézt žádné soubory, by bezobslužně ukončení. Správné, musí být chování, které `-LiteralPath` je literál, takže pokud soubor neexistuje, by měl chyby. Změny se zachází zástupné znaky použít s `-Literal` jako literál.

### <a name="fix-set-service-failing-test-4802httpsgithubcompowershellpowershellissues4802"></a>Opravte `Set-Service` selhání testu [#4802](https://github.com/PowerShell/PowerShell/issues/4802)

Dříve Pokud `New-Service -StartupType foo` byl použit `foo` byla ignorována a služba byla vytvořena s některé výchozí typ spuštění. Tuto změnu je explicitně vyvolána chyba typu neplatný spuštění.

### <a name="rename-isosx-to-ismacos-4700httpsgithubcompowershellpowershellissues4700"></a>Přejmenování `$IsOSX` k `$IsMacOS` [#4700](https://github.com/PowerShell/PowerShell/issues/4700)

Pojmenování v prostředí PowerShell by měla být v souladu s naše pojmenování a v souladu s systému macOS místo OSX použití společnosti Apple. Ale pro čitelnost a konzistentní jsme jsou zachování s Pascal velká a malá písmena.

### <a name="make-error-message-consistent-when-invalid-script-is-passed-to--file-better-error-when-passed-ambiguous-argument-4573httpsgithubcompowershellpowershellissues4573"></a>Zkontrolujte chybové zprávy konzistentní, když je předán neplatný skript do - souboru, chyba, když uplyne nejednoznačný argument lepší [#4573](https://github.com/PowerShell/PowerShell/issues/4573)

Změnit ukončovacích kódů z `pwsh.exe` vyrovnání Unix konvence

### <a name="removal-of-localaccount-and-cmdlets-from--diagnostics-modules-4302httpsgithubcompowershellpowershellissues4302-4303httpsgithubcompowershellpowershellissues4303"></a>Odebrání `LocalAccount` a rutiny z `Diagnostics` moduly. [#4302](https://github.com/PowerShell/PowerShell/issues/4302) [#4303](https://github.com/PowerShell/PowerShell/issues/4303)

Kvůli nepodporované rozhraní API `LocalAccounts` modulu a `Counter` rutiny v `Diagnostics` modulu byly odebrány, dokud nebude nalezen lepší řešení.

### <a name="executing-powershell-script-with-bool-parameter-does-not-work-4036httpsgithubcompowershellpowershellissues4036"></a>Provádění skriptu prostředí powershell s parametrem bool nefunguje [#4036](https://github.com/PowerShell/PowerShell/issues/4036)

Dříve, pomocí powershell.exe (teď `pwsh.exe`) pro spuštění skriptu prostředí PowerShell pomocí `-File` zadaný žádný způsob, jak předat $true nebo $false jako parametr hodnoty. Podpora pro $true/$false jako analyzované hodnoty na parametry byla přidána. Hodnoty přepínače jsou podporovány také jako nyní zdokumentovaných syntaxe nefunguje.

### <a name="remove-clrversion-property-from-psversiontable-4027httpsgithubcompowershellpowershellissues4027"></a>Odebrat `ClrVersion` vlastnost z `$PSVersionTable` [#4027](https://github.com/PowerShell/PowerShell/issues/4027)

`ClrVersion` Vlastnost `$PSVersionTable` není užitečný v případě CoreCLR, koncoví uživatelé by neměl používat tuto hodnotu určete kompatibilitu.

### <a name="change-positional-parameter-for-powershellexe-from--command-to--file-4019httpsgithubcompowershellpowershellissues4019"></a>Změnit poziční parametr pro `powershell.exe` z `-Command` k `-File` [#4019](https://github.com/PowerShell/PowerShell/issues/4019)

Povolte použití shebang prostředí PowerShell na jiných platforem než Windows. To znamená v systémech Unix na základě, můžete použít skript spustitelný soubor, který by měl vyvolat prostředí PowerShell automaticky místo explicitně vyvolání `pwsh`. To také znamená, že teď můžete dělat třeba `powershell foo.ps1` nebo `powershell fooScript` bez zadání `-File`. Tato změna však nyní vyžaduje, aby explicitně zadáte `-c` nebo `-Command` při pokusu o provádět například následující akce `powershell.exe Get-Command`.

### <a name="implement-unicode-escape-parsing-3958httpsgithubcompowershellpowershellissues3958"></a>Implementace analýza řídicí Unicode [#3958](https://github.com/PowerShell/PowerShell/issues/3958)

`` `u#### `` nebo `` `u{####} `` jsou převedeny na odpovídající znak Unicode. K vypsání literál `` `u ``, vyhnuli backtick: ``` ``u ```.

### <a name="change-new-modulemanifest-encoding-to-utf8nobom-on-non-windows-platforms-3940httpsgithubcompowershellpowershellissues3940"></a>Změna `New-ModuleManifest` kódování `UTF8NoBOM` na jiný systém než Windows platformách [#3940](https://github.com/PowerShell/PowerShell/issues/3940)

Dříve `New-ModuleManifest` vytvoří psd1 manifesty v UTF-16 s BOM, vytváření problém pro Linux nástroje. Tato změna narušující změny kódování `New-ModuleManifest` být UTF (žádné BOM) v jiných platforem než Windows.

### <a name="prevent-get-childitem-from-recursing-into-symlinks-1875-3780httpsgithubcompowershellpowershellissues3780"></a>Zabránit `Get-ChildItem` z recursing do symbolických odkazů (#1875). [#3780](https://github.com/PowerShell/PowerShell/issues/3780)

Tato změna přináší `Get-ChildItem` další souladu Unix `ls -r` a Windows `dir /s` nativní příkazy. Podobně jako uvedených příkazů rutina zobrazí symbolické odkazy na adresáře během rekurze nalezen, ale není recurse do nich.

### <a name="fix-get-content--delimiter-to-not-include-the-delimiter-in-the-returned-lines-3706httpsgithubcompowershellpowershellissues3706"></a>Opravte `Get-Content -Delimiter` tak, aby neobsahoval oddělovač řádků vrácená [#3706](https://github.com/PowerShell/PowerShell/issues/3706)

Dříve, výstup při použití `Get-Content -Delimiter` byl nekonzistentní a nepohodlná, jako je vyžadován další zpracování dat odebrat oddělovač. Tato změna odebere oddělovač vrácených řádků.

### <a name="implement-format-hex-in-c-3320httpsgithubcompowershellpowershellissues3320"></a>Implementace šestnáctkový formátu v jazyce C# [#3320](https://github.com/PowerShell/PowerShell/issues/3320)

`-Raw` Parametr je nyní "operaci-" (v tomto neprovede žádnou akci). Chvíle veškerý výstup se zobrazí reprezentativní čísla, která obsahuje všechny bajtů pro tento typ (co `-Raw` parametr dělal oficiálně před této změny).

### <a name="powershell-as-a-default-shell-doesnt-work-with-script-command-3319httpsgithubcompowershellpowershellissues3319"></a>Prostředí PowerShell jako výchozí prostředí nefunguje s příkazu skriptu [#3319](https://github.com/PowerShell/PowerShell/issues/3319)

V systému Unix, je konvence pro prostředí shell tak, aby přijímal `-i` pro interaktivní prostředí a celou řadu nástrojů očekávat toto chování (`script` například a kdy nastavení jako výchozí prostředí PowerShell) a volání prostředí s `-i` přepínače. Tuto změnu je porušením v tom, že `-i` dřív šlo použít jako krátké ruční tak, aby odpovídaly `-inputformat`, které teď musí být `-in`.

### <a name="typo-fix-in-get-computerinfo-property-name-3167httpsgithubcompowershellpowershellissues3167"></a>Oprava máte překlep v názvu vlastnosti Get-ComputerInfo [#3167](https://github.com/PowerShell/PowerShell/issues/3167)

`BiosSerialNumber` bylo zadáno chybně jako `BiosSeralNumber` a byl změněn na správný pravopis.

### <a name="add-get-stringhash-and-get-filehash-cmdlets-3024httpsgithubcompowershellpowershellissues3024"></a>Přidat `Get-StringHash` a `Get-FileHash` rutiny [#3024](https://github.com/PowerShell/PowerShell/issues/3024)

Tuto změnu je, že některé algoritmy hash nepodporuje CoreFX, proto již nejsou k dispozici:

- `MACTripleDES`
- `RIPEMD160`

### <a name="add-validation-on-get--cmdlets-where-passing-null-returns-all-objects-instead-of-error-2672httpsgithubcompowershellpowershellissues2672"></a>Přidání ověřování na `Get-*` rutiny, kde předávání $null vrátí všechny objekty místo chyby [#2672](https://github.com/PowerShell/PowerShell/issues/2672)

Předávání `$null` k některému z následujících nyní generuje se chyba:

- `Get-Credential -UserName`
- `Get-Event -SourceIdentifier`
- `Get-EventSubscriber -SourceIdentifier`
- `Get-Help -Name`
- `Get-PSBreakpoint -Script`
- `Get-PSProvider -PSProvider`
- `Get-PSSessionConfiguration -Name`
- `Get-PSSnapin -Name`
- `Get-Runspace -Name`
- `Get-RunspaceDebug -RunspaceName`
- `Get-Service -Name`
- `Get-TraceSource -Name`
- `Get-Variable -Name`
- `Get-WmiObject -Class`
- `Get-WmiObject -Property`

### <a name="add-support-w3c-extended-log-file-format-in-import-csv-2482httpsgithubcompowershellpowershellissues2482"></a>Přidat podporu rozšířený formát souboru protokolu W3C v `Import-Csv` [#2482](https://github.com/PowerShell/PowerShell/issues/2482)

Dříve `Import-Csv` rutiny nelze použít přímo importovat soubory protokolu v rozšířeném formátu protokolu W3C a další akce by bylo zapotřebí. Díky této změně se podporuje rozšířený formát protokolu W3C.

### <a name="parameter-binding-problem-with-valuefromremainingarguments-in-ps-functions-2035httpsgithubcompowershellpowershellissues2035"></a>Parametr vazby problém s `ValueFromRemainingArguments` PS funkcí [#2035](https://github.com/PowerShell/PowerShell/issues/2035)

`ValueFromRemainingArguments` Teď vrátí hodnoty jako pole místo jedné hodnoty, které je pole.

### <a name="buildversion-is-removed-from-psversiontable-1415httpsgithubcompowershellpowershellissues1415"></a>`BuildVersion` je odebrán z `$PSVersionTable` [#1415](https://github.com/PowerShell/PowerShell/issues/1415)

Odeberte `BuildVersion` vlastnost z `$PSVersionTable`. Tato vlastnost byla vázaný na verzi Windows sestavení. Místo toho doporučujeme používat `GitCommitId` načíst verzi přesný sestavení jádra prostředí PowerShell.

### <a name="changes-to-web-cmdlets"></a>Změny webové rutiny

Základní .NET API rutin Web byl změněn na `System.Net.Http.HttpClient`. Tato změna poskytuje řadu výhod. Však tato změna společně s chybějících interoperabilitu s aplikací Internet Explorer jsou výsledkem několik nejnovějších změn v rámci `Invoke-WebRequest` a `Invoke-RestMethod`.

- `Invoke-WebRequest` Teď podporuje základní HTML analýza jenom. `Invoke-WebRequest` vždy vrátí hodnotu `BasicHtmlWebResponseObject` objektu. `ParsedHtml` a `Forms` vlastnosti byly odebrány.
- `BasicHtmlWebResponseObject.Headers` hodnoty jsou nyní `String[]` místo `String`.
- `BasicHtmlWebResponseObject.BaseResponse` je teď `System.Net.Http.HttpResponseMessage` objektu.
- `Response` Vlastnost na Web rutiny výjimky je teď `System.Net.Http.HttpResponseMessage` objektu.
- Analýza striktní RFC záhlaví je teď výchozího nastavení pro `-Headers` a `-UserAgent` parametr. To lze obejít s `-SkipHeaderValidation`.
- `file://` a `ftp://` už jsou podporována schémata identifikátoru URI.
- `System.Net.ServicePointManager` nastavení jsou již omezení dodržena.
- Není aktuálně bez ověřování na základě certifikátů k dispozici v systému macOS.
- Použití `-Credential` přes `http://` URI bude mít za následek chybu. Použijte `https://` identifikátor URI nebo zadat `-AllowUnencryptedAuthentication` parametr potlačit chyby.

---
ms.date: 05/17/2018
keywords: prostředí PowerShell, core
title: Rozbíjející změny v Powershellu 6.0
ms.openlocfilehash: d477a9b27e8d5df6653ee40f8b606879b60a80c7
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655442"
---
# <a name="breaking-changes-for-powershell-60"></a>Rozbíjející změny v Powershellu 6.0

## <a name="features-no-longer-available-in-powershell-core"></a>Funkce, které již nejsou k dispozici v Powershellu Core

### <a name="powershell-workflow"></a>Pracovní postup prostředí PowerShell

[Pracovní postup Powershellu] [ workflow] je funkce ve Windows Powershellu, který vytváří nad [Windows Workflow Foundation (WF)] [ workflow-foundation] , která umožňuje vytváření Robustní sady runbook pro dlouho běžící nebo paralelizované úloh.

Z důvodu chybějící podpora jazyků Windows Workflow Foundation v .NET Core jsme nebude nadále podporovat pracovního postupu Powershellu v prostředí PowerShell Core.

V budoucnu rádi bychom Povolit nativní paralelismu/souběžnosti v jazyce Powershellu bez pracovního postupu Powershellu.

[workflow]: https://docs.microsoft.com/powershell/scripting/core-powershell/workflows-guide
[workflow-foundation]: https://docs.microsoft.com/dotnet/framework/windows-workflow-foundation/

### <a name="custom-snap-ins"></a>Vlastní moduly snap in

[Moduly snap in prostředí PowerShell] [ snapin] jsou předchůdce do modulů Powershellu, které nemají jeho využití v komunitě prostředí PowerShell.

Z důvodu složitosti podpora moduly snap in a jejich nedostatečné využití v komunitě už nadále nepodporujeme vlastní moduly snap in v prostředí PowerShell Core.

V současné době tím je prolomen `ActiveDirectory` a `DnsClient` moduly ve Windows a Windows serveru.

[snapin]: https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_pssnapins

### <a name="wmi-v1-cmdlets"></a>Rutiny WMI v1

Z důvodu složitosti podporu dvou sad založených na rozhraní WMI modulů jsme odebrali rutiny WMI v1 z Powershellu Core:

- `Get-WmiObject`
- `Invoke-WmiMethod`
- `Register-WmiEvent`
- `Set-WmiInstance`

Místo toho doporučujeme, aby vám použití rutin modelu CIM (označuje se také jako WMI v2), které poskytují stejné funkce s přepracovaný syntaxi a nové funkce:

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

Kvůli použití nepodporované rozhraní API `Microsoft.PowerShell.LocalAccounts` je odebraná ze PowerShell Core, dokud nebude nalezen lepší řešení.

### <a name="-counter-cmdlets"></a>Rutiny pro `*-Counter`

Kvůli použití nepodporované rozhraní API `*-Counter` je odebraná ze PowerShell Core, dokud nebude nalezen lepší řešení.

## <a name="enginelanguage-changes"></a>Modul/jazykové změny

### <a name="rename-powershellexe-to-pwshexe-5101httpsgithubcompowershellpowershellissues5101"></a>Přejmenovat `powershell.exe` k `pwsh.exe` [#5101](https://github.com/PowerShell/PowerShell/issues/5101)

Pokud chcete uživatelům udělit deterministické způsob, jak volat Powershellu Core ve Windows (na rozdíl od Windows Powershellu), prostředí PowerShell Core binární soubor byl změněn na `pwsh.exe` na Windows a `pwsh` na platformách než Windows.

Zkrácený název je také konzistentní s pojmenování prostředí na platformách než Windows.

### <a name="dont-insert-line-breaks-to-output-except-for-tables-5193httpsgithubcompowershellpowershellissues5193"></a>Nevkládejte konce řádků výstupu (s výjimkou tabulky) [#5193](https://github.com/PowerShell/PowerShell/issues/5193)

Dříve výstup byl zarovnané šířce konzole a zalomení řádků byly přidány na koncová šířka konzoly, což znamená, že výstup nepovedlo získat přeformátovali podle očekávání, pokud se změnila terminálu. Tato změna se neaplikovala k tabulkám, jsou také k zachování konzistence sloupce zarovnané konce řádků.

### <a name="skip-null-element-check-for-collections-with-a-value-type-element-type-5432httpsgithubcompowershellpowershellissues5432"></a>Přeskočení kontroly element s hodnotou null pro kolekce s typem elementu typu hodnoty [#5432](https://github.com/PowerShell/PowerShell/issues/5432)

Pro `Mandatory` parametr a `ValidateNotNull` a `ValidateNotNullOrEmpty` atributy, Přeskočit kontrolu element s hodnotou null, pokud typ elementu kolekce je typ hodnoty.

### <a name="change-outputencoding-to-use-utf-8-nobom-encoding-rather-than-ascii-5369httpsgithubcompowershellpowershellissues5369"></a>Změna `$OutputEncoding` používat `UTF-8 NoBOM` kódování místo ASCII [#5369](https://github.com/PowerShell/PowerShell/issues/5369)

Výsledkem předchozího kódování, ASCII (7-bit), budou nesprávné změnu ve výstupu v některých případech. Tato změna je, aby `UTF-8 NoBOM` výchozí, což zachová výstup ve formátu Unicode s kódováním nepodporuje většiny nástrojů a operačních systémů.

### <a name="remove-allscope-from-most-default-aliases-5268httpsgithubcompowershellpowershellissues5268"></a>Odebrat `AllScope` z většiny výchozí aliasy [#5268](https://github.com/PowerShell/PowerShell/issues/5268)

Ke zrychlení vytváření oboru `AllScope` byl odebrán z většiny výchozí aliasy. `AllScope` byla ponechána pro několik často používané aliasy místo, kde bylo rychlejší vyhledávání.

### <a name="-verbose-and--debug-no-longer-overrides-erroractionpreference-5113httpsgithubcompowershellpowershellissues5113"></a>`-Verbose` a `-Debug` už přepíše `$ErrorActionPreference` [#5113](https://github.com/PowerShell/PowerShell/issues/5113)

Dříve Pokud `-Verbose` nebo `-Debug` byly zadány overrode chování `$ErrorActionPreference`. Díky této změně `-Verbose` a `-Debug` už nebude mít vliv na chování `$ErrorActionPreference`.

## <a name="cmdlet-changes"></a>Změny rutin

### <a name="invoke-restmethod-doesnt-return-useful-info-when-no-data-is-returned-5320httpsgithubcompowershellpowershellissues5320"></a>Vyvolání RestMethod nevrací užitečných informací, když nebudou vrácena žádná data. [#5320](https://github.com/PowerShell/PowerShell/issues/5320)

Pokud rozhraní API vrátí jenom `null`, Invoke-RestMethod to byla serializaci jako řetězec `"null"` místo `$null`. Tato změna řeší logika `Invoke-RestMethod` správně serializovat platnou hodnotu typu single JSON `null` literálu jako `$null`.

### <a name="remove--computername-from--computer-cmdlets-5277httpsgithubcompowershellpowershellissues5277"></a>Odebrat `-ComputerName` z `*-Computer` rutiny [#5277](https://github.com/PowerShell/PowerShell/issues/5277)

Kvůli problémům s vzdálené komunikace RPC v CoreFX (zejména na platformách než Windows) a zajištění konzistentní vzdálenou komunikaci prostředí v Powershellu `-ComputerName` parametr byl odebrán z `\*-Computer` rutiny. Použití `Invoke-Command` místo jako způsob, jak vzdálené spouštění rutin.

### <a name="remove--computername-from--service-cmdlets-5090httpsgithubcompowershellpowershellissues5094"></a>Odebrat `-ComputerName` z `*-Service` rutiny [#5090](https://github.com/PowerShell/PowerShell/issues/5094)

Aby bylo možné podporovat konzistentním použitím PSRP, `-ComputerName` parametr byl odebrán z `*-Service` rutiny.

### <a name="fix-get-item--literalpath-ab-if-ab-doesnt-actually-exist-to-return-error-5197httpsgithubcompowershellpowershellissues5197"></a>Oprava `Get-Item -LiteralPath a*b` Pokud `a*b` neexistuje ve skutečnosti k vrácení chyby [#5197](https://github.com/PowerShell/PowerShell/issues/5197)

Dříve `-LiteralPath` daný zástupný znak by ji považovat za stejné `-Path` a pokud zástupný znak nenajde žádné soubory, bude tiše ukončíte. Správné chování, která by měla být `-LiteralPath` je literál, takže pokud soubor neexistuje, by mělo chyby. Změna se zachází zástupných znaků použít s `-Literal` jako literál.

### <a name="import-csv-should-apply-pstypenames-upon-import-when-type-information-is-present-in-the-csv-5134httpsgithubcompowershellpowershellissues5134"></a>`Import-Csv` by se měly používat `PSTypeNames` po import po informace o typu se nachází ve sdíleném svazku clusteru [#5134](https://github.com/PowerShell/PowerShell/issues/5134)

Dříve, exportovat objekty pomocí `Export-CSV` s `TypeInformation` importovat s `ConvertFrom-Csv` nebyly zachování informací o typu. Přidá informace o typu pro tuto změnu `PSTypeNames` člen, pokud je k dispozici ze souboru CSV.

### <a name="-notypeinformation-should-be-default-on-export-csv-5131httpsgithubcompowershellpowershellissues5131"></a>`-NoTypeInformation` by měla být výchozí na `Export-Csv` [#5131](https://github.com/PowerShell/PowerShell/issues/5131)

Tato změna byla provedena na zpětnou vazbu zákazníků na výchozí chování `Export-CSV` zahrnout informace o typu.

Dříve by výstup rutiny komentář jako první řádek, který obsahuje název typu objektu. Změna je potlačit to ve výchozím nastavení, jak ho většina nástrojů nerozumí. Použití `-IncludeTypeInformation` zachovat předchozí chování.

### <a name="web-cmdlets-should-warn-when--credential-is-sent-over-unencrypted-connections-5112httpsgithubcompowershellpowershellissues5112"></a>Rutiny web by měl zobrazit upozornění při `-Credential` je odeslán přes nezašifrované připojení [#5112](https://github.com/PowerShell/PowerShell/issues/5112)

Při použití protokolu HTTP, obsah, včetně hesel odeslány jako nešifrovaný text. Tato změna je to nepovolují ve výchozím nastavení a vrátí chybu, pokud se přihlašovací údaje jsou předávány nezabezpečeným způsobem. Uživatelé mohou obejít tím pomocí `-AllowUnencryptedAuthentication` přepnout.

## <a name="api-changes"></a>Změny rozhraní API

### <a name="remove-addtypecommandbase-class-5407httpsgithubcompowershellpowershellissues5407"></a>Odebrat `AddTypeCommandBase` třídy [#5407](https://github.com/PowerShell/PowerShell/issues/5407)

`AddTypeCommandBase` Třídy byl odebrán z `Add-Type` ke zlepšení výkonu. Tato třída se používá jenom pomocí rutiny Add-Type a by neměla mít vliv na uživatele.

### <a name="unify-cmdlets-with-parameter--encoding-to-be-of-type-systemtextencoding-5080httpsgithubcompowershellpowershellissues5080"></a>Sjednocení rutiny s parametrem `-Encoding` typu `System.Text.Encoding` [#5080](https://github.com/PowerShell/PowerShell/issues/5080)

`-Encoding` Hodnotu `Byte` byla odebrána z rutiny zprostředkovatele systému souborů. Nový parametr `-AsByteStream`, se teď používá k určení, že datový proud bajtů se vyžaduje jako vstup nebo že je výstup datového proudu bajtů.

### <a name="add-better-error-message-for-empty-and-null--uformat-parameter-5055httpsgithubcompowershellpowershellissues5055"></a>Přidat lepší chybové zprávy pro prázdný a hodnota null `-UFormat` parametr [#5055](https://github.com/PowerShell/PowerShell/issues/5055)

Dříve, když předávání formátu prázdný řetězec, který se `-UFormat`, by zobrazovat zbytečná zpráva. Více popisná chybová byla přidána.

### <a name="clean-up-console-code-4995httpsgithubcompowershellpowershellissues4995"></a>Čištění kódu konzoly [#4995](https://github.com/PowerShell/PowerShell/issues/4995)

Následující funkce byly odstraněny, protože nejsou podporovány v prostředí PowerShell Core a neexistují žádné plány. Chcete-li přidat podporu, protože existují kvůli starším verzím pro prostředí Windows PowerShell: `-psconsolefile` přepínače a kód, `-importsystemmodules` přepínače a kód a písma změny kódu.

### <a name="removed-runspaceconfiguration-support-4942httpsgithubcompowershellpowershellissues4942"></a>Odebrat `RunspaceConfiguration` podporují [#4942](https://github.com/PowerShell/PowerShell/issues/4942)

Dříve při vytváření prostředí runspace Powershellu programově pomocí rozhraní API můžete použít starší [ `RunspaceConfiguration` ] [ runspaceconfig] nebo novější [ `InitialSessionState` ] [ iss]. Tato změna odebrala podpora pro `RunspaceConfiguration` a podporuje pouze `InitialSessionState`.

[runspaceconfig]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.runspaceconfiguration
[iss]: https://docs.microsoft.com/dotnet/api/system.management.automation.runspaces.initialsessionstate

### <a name="commandinvocationintrinsicsinvokescript-bind-arguments-to-input-instead-of-args-4923httpsgithubcompowershellpowershellissues4923"></a>`CommandInvocationIntrinsics.InvokeScript` Vytvoření vazby argumenty, které mají `$input` místo `$args` [#4923](https://github.com/PowerShell/PowerShell/issues/4923)

Nesprávná pozice parametru výsledkem args předané jako vstup místo jako argumenty.

### <a name="remove-unsupported--showwindow-switch-from-get-help-4903httpsgithubcompowershellpowershellissues4903"></a>Odeberte nepodporované `-showwindow` přejít z `Get-Help` [#4903](https://github.com/PowerShell/PowerShell/issues/4903)

`-showwindow` spoléhá na WPF, což není podporováno u CoreCLR.

### <a name="allow--to-be-used-in-registry-path-for-remove-item-4866httpsgithubcompowershellpowershellissues4866"></a>Povolit * pro použití v cestě registru pro `Remove-Item` [#4866](https://github.com/PowerShell/PowerShell/issues/4866)

Dříve `-LiteralPath` daný zástupný znak by ji považovat za stejné `-Path` a pokud zástupný znak nenajde žádné soubory, bude tiše ukončíte. Správné chování, která by měla být `-LiteralPath` je literál, takže pokud soubor neexistuje, by mělo chyby. Změna se zachází zástupných znaků použít s `-Literal` jako literál.

### <a name="fix-set-service-failing-test-4802httpsgithubcompowershellpowershellissues4802"></a>Oprava `Set-Service` selhání testu [#4802](https://github.com/PowerShell/PowerShell/issues/4802)

Dříve Pokud `New-Service -StartupType foo` byl použit `foo` byla ignorována a služba byla vytvořena s nějakým typem výchozí spuštění. Tato změna je explicitně vyvolání k chybě typu neplatná spouštěcí.

### <a name="rename-isosx-to-ismacos-4700httpsgithubcompowershellpowershellissues4700"></a>Přejmenovat `$IsOSX` k `$IsMacOS` [#4700](https://github.com/PowerShell/PowerShell/issues/4700)

Pojmenování v prostředí PowerShell by bylo v souladu s naší pojmenování a v souladu s použití společnosti Apple MacOS místo OSX. Ale pro lepší čitelnost a důsledně se můžeme zůstává s Pascal velká a malá písmena.

### <a name="make-error-message-consistent-when-invalid-script-is-passed-to--file-better-error-when-passed-ambiguous-argument-4573httpsgithubcompowershellpowershellissues4573"></a>Ujistěte se, chybová zpráva konzistentní při předání neplatný skript – soubor, lepší chyby při předání argumentu nejednoznačný [#4573](https://github.com/PowerShell/PowerShell/issues/4573)

Změnit ukončovací kód z `pwsh.exe` souladu s konvencemi systému Unix

### <a name="removal-of-localaccount-and-cmdlets-from--diagnostics-modules-4302httpsgithubcompowershellpowershellissues4302-4303httpsgithubcompowershellpowershellissues4303"></a>Odebrání `LocalAccount` a rutiny z `Diagnostics` moduly. [#4302](https://github.com/PowerShell/PowerShell/issues/4302) [#4303](https://github.com/PowerShell/PowerShell/issues/4303)

Z důvodu nepodporované rozhraní API `LocalAccounts` modulu a `Counter` rutiny v `Diagnostics` modul byly odebrány, dokud nebude nalezen lepší řešení.

### <a name="executing-powershell-script-with-bool-parameter-does-not-work-4036httpsgithubcompowershellpowershellissues4036"></a>Spuštění powershellového skriptu s parametrem bool nefunguje [#4036](https://github.com/PowerShell/PowerShell/issues/4036)

Dříve, pomocí powershell.exe (nyní `pwsh.exe`) Chcete-li spustit skript prostředí PowerShell pomocí `-File` k dispozici žádný způsob, jak předat $true nebo $false jako hodnoty parametrů. Podpora pro $true nebo $false jako analyzované hodnoty pro parametry byl přidán. Přepínač hodnoty jsou také podporovány jako aktuálně zdokumentovaných syntaxe nebude fungovat.

### <a name="remove-clrversion-property-from-psversiontable-4027httpsgithubcompowershellpowershellissues4027"></a>Odebrat `ClrVersion` vlastnost z `$PSVersionTable` [#4027](https://github.com/PowerShell/PowerShell/issues/4027)

`ClrVersion` Vlastnost `$PSVersionTable` není užitečný v případě CoreCLR, koncoví uživatelé neměli byste používat tuto hodnotu k určování kompatibility.

### <a name="change-positional-parameter-for-powershellexe-from--command-to--file-4019httpsgithubcompowershellpowershellissues4019"></a>Změnit pozičních parametrů více dopředu pro `powershell.exe` z `-Command` k `-File` [#4019](https://github.com/PowerShell/PowerShell/issues/4019)

Povolte používání shebang powershellu na platformách než Windows. To znamená, že v systémech Unix na základě provedete skript spustitelný soubor, který by měl vyvolat Powershellu automaticky místo explicitně vyvolání `pwsh`. Zároveň to znamená, že můžete teď provádět věci, jako je `powershell foo.ps1` nebo `powershell fooScript` bez zadání `-File`. Však tuto změnu teď potřeba explicitně zadat `-c` nebo `-Command` při pokusu provést třeba `powershell.exe Get-Command`.

### <a name="implement-unicode-escape-parsing-3958httpsgithubcompowershellpowershellissues3958"></a>Implementace analýzy řídicí Unicode [#3958](https://github.com/PowerShell/PowerShell/issues/3958)

`` `u#### `` nebo `` `u{####} `` je převést na odpovídající znak Unicode. Do výstupního literál `` `u ``, řídicí prvními: ``` ``u ```.

### <a name="change-new-modulemanifest-encoding-to-utf8nobom-on-non-windows-platforms-3940httpsgithubcompowershellpowershellissues3940"></a>Změna `New-ModuleManifest` kódování `UTF8NoBOM` na platformách než Windows [#3940](https://github.com/PowerShell/PowerShell/issues/3940)

Dříve `New-ModuleManifest` vytvoří psd1 manifesty v kódování UTF-16 s BOM vytváření problém pro Linux nástroje. Tato změna zásadní změny kódování `New-ModuleManifest` být UTF (BOM) na platformách než Windows.

### <a name="prevent-get-childitem-from-recursing-into-symlinks-1875-3780httpsgithubcompowershellpowershellissues3780"></a>Zabránit `Get-ChildItem` z recursing do symbolických odkazů (#1875). [#3780](https://github.com/PowerShell/PowerShell/issues/3780)

Tato změna přináší `Get-ChildItem` další podle Unix `ls -r` a Windows `dir /s` nativní příkazy. Stejně jako příkazy uvedené rutina zobrazí symbolické odkazy k adresářům během rekurze nalezen, ale není do nich recurse.

### <a name="fix-get-content--delimiter-to-not-include-the-delimiter-in-the-returned-lines-3706httpsgithubcompowershellpowershellissues3706"></a>Oprava `Get-Content -Delimiter` tak, aby nezahrnovala oddělovač ve vrácených řádcích [#3706](https://github.com/PowerShell/PowerShell/issues/3706)

Dříve, výstup při používání `Get-Content -Delimiter` byl nekonzistentní a nepohodlná, protože ta vyžaduje další zpracování dat k odebrání oddělovač. Tato změna odebere oddělovač ve vrácených řádcích.

### <a name="implement-format-hex-in-c-3320httpsgithubcompowershellpowershellissues3320"></a>Implementace formát Hex C# [#3320](https://github.com/PowerShell/PowerShell/issues/3320)

`-Raw` Parametr je nyní "no-op" (v tom to nemá žádný účinek). Výhledově bude veškerý výstup se zobrazí s true reprezentace čísla, která zahrnuje všechny bajty pro daný typ (co `-Raw` parametr dělal formálně před touto změnou).

### <a name="powershell-as-a-default-shell-doesnt-work-with-script-command-3319httpsgithubcompowershellpowershellissues3319"></a>Prostředí PowerShell jako výchozí prostředí nefunguje při využití příkaz skriptu [#3319](https://github.com/PowerShell/PowerShell/issues/3319)

V systému Unix, je konvence pro prostředí tak, aby přijímal `-i` pro toto chování očekávalo interaktivní prostředí a celou řadu nástrojů (`script` například a při nastavení prostředí PowerShell jako výchozí prostředí) a zavolá prostředí s `-i` přepnout. Tato změna je zásadní v dané `-i` dříve může sloužit jako krátký ručně tak, aby odpovídaly `-inputformat`, které je teď potřeba `-in`.

### <a name="typo-fix-in-get-computerinfo-property-name-3167httpsgithubcompowershellpowershellissues3167"></a>Oprava překlep v názvu vlastnosti Get-ComputerInfo [#3167](https://github.com/PowerShell/PowerShell/issues/3167)

`BiosSerialNumber` bylo zadáno chybně jako `BiosSeralNumber` a byl změněn na správně.

### <a name="add-get-stringhash-and-get-filehash-cmdlets-3024httpsgithubcompowershellpowershellissues3024"></a>Přidat `Get-StringHash` a `Get-FileHash` rutiny [#3024](https://github.com/PowerShell/PowerShell/issues/3024)

Tato změna je, že některé hashovacích algoritmů nepodporuje CoreFX, proto už nejsou k dispozici:

- `MACTripleDES`
- `RIPEMD160`

### <a name="add-validation-on-get--cmdlets-where-passing-null-returns-all-objects-instead-of-error-2672httpsgithubcompowershellpowershellissues2672"></a>Přidání ověřování na `Get-*` rutiny, kde předávání $null vrátí všechny objekty místo chyby [#2672](https://github.com/PowerShell/PowerShell/issues/2672)

Předání `$null` na některý z následujících nyní vyvolá chybu:

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

### <a name="add-support-w3c-extended-log-file-format-in-import-csv-2482httpsgithubcompowershellpowershellissues2482"></a>Přidání podpory W3C rozšířený formát souborů protokolu v `Import-Csv` [#2482](https://github.com/PowerShell/PowerShell/issues/2482)

Dříve `Import-Csv` rutiny nelze použít k přímému importu souborů protokolu v rozšířeném formátu protokolu W3C a provádět další akce by bylo zapotřebí. Díky této změně se podporuje rozšířený formát protokolu W3C.

### <a name="parameter-binding-problem-with-valuefromremainingarguments-in-ps-functions-2035httpsgithubcompowershellpowershellissues2035"></a>Parametr vazby problém s `ValueFromRemainingArguments` ve funkcích PS [#2035](https://github.com/PowerShell/PowerShell/issues/2035)

`ValueFromRemainingArguments` nyní vrátí hodnoty jako pole namísto jediného hodnotu, která sama je pole.

### <a name="buildversion-is-removed-from-psversiontable-1415httpsgithubcompowershellpowershellissues1415"></a>`BuildVersion` Odebereme z `$PSVersionTable` [#1415](https://github.com/PowerShell/PowerShell/issues/1415)

Odeberte `BuildVersion` vlastnost z `$PSVersionTable`. Tato vlastnost se vázalo na verzi Windows sestavení. Namísto toho doporučujeme použít `GitCommitId` sestavení přesnou verzi prostředí PowerShell Core.

### <a name="changes-to-web-cmdlets"></a>Změny v rutinách webové

Základní rozhraní .NET API rutin Web byl změněn na `System.Net.Http.HttpClient`. Tato změna má spoustu výhod. Ale tato změna spolu s chybějící interoperability s aplikací Internet Explorer vyústila v několika rozbíjející změny v rámci `Invoke-WebRequest` a `Invoke-RestMethod`.

- `Invoke-WebRequest` Teď podporuje základní HTML Parsování pouze. `Invoke-WebRequest` vždy vrátí hodnotu `BasicHtmlWebResponseObject` objektu. `ParsedHtml` a `Forms` byly odebrány vlastnosti.
- `BasicHtmlWebResponseObject.Headers` hodnoty jsou nyní `String[]` místo `String`.
- `BasicHtmlWebResponseObject.BaseResponse` je teď `System.Net.Http.HttpResponseMessage` objektu.
- `Response` Vlastnost na Web rutiny výjimky je nyní `System.Net.Http.HttpResponseMessage` objektu.
- Analýza striktní RFC záhlaví je teď výchozí nastavení pro `-Headers` a `-UserAgent` parametru. To lze obejít s `-SkipHeaderValidation`.
- `file://` a `ftp://` schémata identifikátoru URI již nejsou podporovány.
- `System.Net.ServicePointManager` nastavení omezení se už nebude dodržena.
- Není aktuálně bez ověřování na základě certifikátů k dispozici v systému macOS.
- Použití `-Credential` přes `http://` URI způsobí chybu. Použití `https://` identifikátor URI nebo zadat `-AllowUnencryptedAuthentication` parametr potlačit chyby.
- `-MaximumRedirection` nyní vytvoří dojde k ukončující chybě při pokusy o přesměrování překračuje zadaný limit místo vrácení výsledků z poslední přesměrování.

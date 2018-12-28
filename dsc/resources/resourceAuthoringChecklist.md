---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Kontrolní seznam při tvorbě prostředku
ms.openlocfilehash: 7b1a096bba1b729c096b6689178ee022e12e4634
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403769"
---
# <a name="resource-authoring-checklist"></a>Kontrolní seznam při tvorbě prostředku

Tento kontrolní seznam je seznam osvědčených postupů při vytváření nového prostředku DSC.

## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a>Modul prostředků obsahuje souboru .psd1 a schema.mof pro každý prostředek

Zkontrolujte, zda váš prostředek má správnou strukturu a obsahuje všechny požadované soubory. Každý modul prostředků by měl obsahovat souboru .psd1 a každý bez složený prostředek by měl mít schema.mof souboru. Prostředky, které neobsahují schématu nebude uvedené podle `Get-DscResource` a uživatelé nebudou moct používat technologii intellisense při psaní kódu pro tyto moduly v prostředí ISE.
Adresářové struktury xRemoteFile prostředků, která je součástí sady [xPSDesiredStateConfiguration prostředků modulu](https://github.com/PowerShell/xPSDesiredStateConfiguration), vypadá takto:

```
xPSDesiredStateConfiguration
    DSCResources
        MSFT_xRemoteFile
            MSFT_xRemoteFile.psm1
            MSFT_xRemoteFile.schema.mof
    Examples
        xRemoteFile_DownloadFile.ps1
    ResourceDesignerScripts
        GenerateXRemoteFileSchema.ps1
    Tests
        ResourceDesignerTests.ps1
    xPSDesiredStateConfiguration.psd1
```

## <a name="resource-and-schema-are-correct"></a>Správnost prostředků a schématu

Ověření schématu prostředků (*. schema.mof) soubor. Můžete použít [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) usnadňují vývoj a testování vašeho schématu.
Ujistěte se, že:

- Typy vlastností jsou správné (například nepoužívejte řetězec pro vlastnosti, které přijímají číselných hodnot, byste měli použít místo toho UInt32 nebo další číselné typy)
- Atributy vlastnosti jsou správně zadané jako: ([klíč], [povinné], [psaní], [pro čtení])
- Nejméně jeden parametr ve schématu musí být označený jako [klíč]
- [pro čtení] vlastnost není existovat vedle sebe spolu s případnými z: [povinné], [key], [psaní]
- Pokud více kvalifikátory jsou zadaný – s výjimkou [čtení], pak [klíč] má přednost před
- Pokud [psaní] a [povinné] je zadán, pak [povinné] přednost
- Je zadán chybu případně příkladu:

  ```
  [Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
  ```

- Popisný název je zadán a potvrdí DSC zásady vytváření názvů pro

  Příklad: `[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]`

- Každé pole má výstižný popis. Úložiště GitHub Powershellu má dobrými příklady, například [. schema.mof pro xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)

Kromě toho byste měli použít **testovací xDscResource** a **testovací xDscSchema** rutiny z [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/1.12.0.0) můžete si automaticky ověřit zdroj a schéma:

```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```

Příklad:

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a>Prostředek načte bez chyb

Zkontrolujte, zda modul prostředků je možné úspěšně načíst.
Toho lze dosáhnout ručně spuštěním `Import-Module <resource_module> -force` a potvrzení, že nedošlo k žádným chybám, nebo za zápis automatizace testů. V druhém případě můžete postupovat podle této struktuře ve svém testovacím případu:

```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```

## <a name="resource-is-idempotent-in-the-positive-case"></a>Prostředek je idempotentní v případě pozitivní

Mezi základní charakteristiky prostředky DSC je idempotence. Znamená to, že použití DSC konfigurace obsahující více než jednou tento prostředek se vždycky dosažení stejného výsledku. Pokud například vytvoříme konfigurace, která obsahuje následující prostředek souboru:

```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```

Po jeho použití poprvé souboru test.txt by se zobrazit v `C:\test` složky. Ale při dalším spuštění se stejnou konfigurací by neměla změnit stav počítače (třeba žádná kopie `test.txt` by měl být vytvořen soubor).
K zajištění prostředek je idempotentní můžete opakovaně volat `Set-TargetResource` při testování prostředku přímo, nebo volat `Start-DscConfiguration` více než jednou při provádění testování začátku do konce. Výsledek by měl být stejný po každé spuštění.

## <a name="test-user-modification-scenario"></a>Testovací scénář úpravy uživatele

Změna stavu počítače a pak znovu spustíte DSC, můžete ověřit, že `Set-TargetResource` a `Test-TargetResource` fungovat správně. Tady jsou kroky, které byste měli provést:

1. Začněte s prostředku není v požadovaném stavu.
2. Konfigurace spuštění s vaším prostředkem
3. Ověřte `Test-DscConfiguration` vrátí hodnotu True
4. Upravit nakonfigurované položky, která má být z požadovaného stavu
5. Ověřte `Test-DscConfiguration` vrátí hodnotu false

Zde je příklad konkrétnější pomocí registru prostředků:

1. Spustit pomocí klíče registru není v požadovaném stavu.
2. Spustit `Start-DscConfiguration` s konfiguraci, kterou chcete vložit ho do požadovaného stavu a ověří, že předává.
3. Spustit `Test-DscConfiguration` a ověřit, vrátí hodnotu true
4. Upravte hodnotu klíče, aby není v požadovaném stavu.
5. Spustit `Test-DscConfiguration` a ověřit, vrátí hodnotu false
6. `Get-TargetResource` funkce se ověřila pomocí `Get-DscConfiguration`

`Get-TargetResource` by měl vrátit podrobnosti o aktuálním stavem prostředku. Ujistěte se, že ho otestovat pomocí volání `Get-DscConfiguration` po použití konfigurace a ověření, který výstup správně odráží aktuální stav stroje. Je potřeba otestovat samostatně, protože všechny problémy v této oblasti se nezobrazí při volání metody `Start-DscConfiguration`.

## <a name="call-getsettest-targetresource-functions-directly"></a>Volání **Get/Set/Test-TargetResource** přímo funkce

Ujistěte se, že je otestovat **Get/Set/Test-TargetResource** funkce implementované ve svém prostředku přímého volání a ověření, že fungují podle očekávání.

## <a name="verify-end-to-end-using-start-dscconfiguration"></a>Ověření pomocí koncového **Start-DscConfiguration**

Testování **Get/Set/Test-TargetResource** funkcí pomocí přímého volání je důležité, ale ne všechny problémy, bude zjištěno tímto způsobem. Měli byste se zaměřit podstatnou část testování pomocí `Start-DscConfiguration` nebo serveru vyžádané replikace. Ve skutečnosti to je, jak budou uživatelé používat prostředků, takže Nepodceňujte význam tohoto typu testy.
Možné typy problémů:

- Přihlašovací údaje nebo relace může chovat jinak, protože DSC agent běží jako služba.  Nezapomeňte otestovat tady žádné funkce začátku do konce.
- Ve výstupu chyby `Start-DscConfiguration` může být jiný než ty, které zobrazí při volání `Set-TargetResource` fungovat přímo.

## <a name="test-compatability-on-all-dsc-supported-platforms"></a>Kompatibilita test na všechny DSC podporované platformy

Prostředků by měly fungovat na všech platformách nepodporuje DSC (Windows Server 2008 R2 a novější). Nainstalujte nejnovější WMF (Windows Management Framework) na vašem operačním systému, abyste získali nejnovější verzi DSC. Pokud váš prostředek nelze použít u některé z těchto platforem záměrné, má být vrácen určité chybové zprávě. Také se ujistěte, že váš prostředek kontroluje, zda jsou rutiny, ke kterému se připojujete na konkrétním počítači. Windows Server 2012 přidali velký počet nové rutiny, které nejsou k dispozici na Windows Server 2008 R2, i při instalaci WMF.

## <a name="verify-on-windows-client-if-applicable"></a>Ověřte v klientovi Windows (Pokud je k dispozici)

Jednu mezeru velmi běžné testu se ověřuje se prostředek pouze v serverových verzí systému Windows. Mnoho prostředků jsou také navrženy pro práci na SKU klienta, takže pokud je to váš případ true, nezapomeňte ji otestovat na těchto platformách.

## <a name="get-dscresource-lists-the-resource"></a>Get-DSCResource uvádí prostředku

Po nasazení modulu volání `Get-DscResource` váš prostředek mimo jiné díky tomu zveřejnit. Pokud váš prostředek nejde najít v seznamu, ujistěte se, že tento soubor schema.mof pro daný prostředek existuje.

## <a name="resource-module-contains-examples"></a>Modul prostředků obsahuje příklady

Vytváření kvalitní příklady, které pomůže ostatním pochopit, jak ho použít. Toto je zásadní, zejména, protože mnoho uživatelů považovat dokumentaci ukázkový kód.

- Nejdřív byste měli určit příklady, které budou součástí modulu – minimálně, by mělo zahrnovat nejdůležitější případy použití pro prostředek:
- Pokud modul obsahuje několik prostředků, které je potřeba ve scénáři začátku do konce společně, základní příklad začátku do konce v ideálním případě by první.
- Počáteční příklady by měla být velmi jednoduché – jak začít pracovat s vašimi prostředky v malých spravovatelných blocích (třeba vytvoření nového virtuálního pevného disku)
- Následující příklady by měl vytvářet v těchto příkladech (např. vytvoření virtuálního počítače z virtuálního pevného disku, odebrání virtuálního počítače, změna virtuálního počítače) a zobrazit pokročilé funkce (např. vytvoření virtuálního počítače s dynamickou pamětí)
- Příklad konfigurace by měly být parametrizovány (všechny hodnoty by měly být předány konfiguraci jako parametry a měl by existovat žádné hodnoty pevně zakódované):

  ```powershell
  configuration Sample_xRemoteFile_DownloadFile
  {
    param
    (
        [string[]] $nodeName = 'localhost',

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $destinationPath,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $uri,

        [String] $userAgent,

        [Hashtable] $headers
    )

    Import-DscResource -Name MSFT_xRemoteFile -ModuleName xPSDesiredStateConfiguration

    Node $nodeName
    {
        xRemoteFile DownloadFile
        {
            DestinationPath = $destinationPath
            Uri = $uri
            UserAgent = $userAgent
            Headers = $headers
        }
    }
  }
  ```

- Je dobrým zvykem zahrnout (komentovaný navýšení kapacity) příklad toho, jak volat konfigurace a skutečné hodnoty na konci ukázkový skript.
  Například ve výše uvedené konfigurace není nutně jasné, že je nejlepší způsob, jak určit UserAgent:

  `UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` Komentář v takovém případě můžete zpřehlednit zamýšlený provádění konfigurace:

  ```powershell
  <#
  Sample use (parameter values need to be changed according to your scenario):

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
  -userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
  #>
  ```

- Pro každý příklad zápisu krátký popis, který vysvětluje, co to dělá a význam parametry.
- Ujistěte se, že příklady pokrývají většinu scénářů, které jsou důležité pro váš prostředek a pokud není nic nechybí, ověřte, že všechny spustit a změnit počítače v požadovaném stavu.

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a>Chybové zprávy jsou srozumitelné a pomáhají uživatelům řešit problémy

By měl být dobrým chybové zprávy:

- Existuje: Největší problém s chybové zprávy je, že často neexistují, proto se ujistěte, že jsou zde.
- Snadná na pochopení: Kódy chyb lidské čitelný, ne skrytého
- Přesné: Popište, co je právě tento problém
- Konstruktivní: Pokyny k vyřešení problému
- Zdvořilé: Nemáte blame uživatele nebo je pocit, že chybné

Ujistěte se, že ověříte chyby v komplexní scénáře (pomocí `Start-DscConfiguration`), protože se může lišit od těch vráceného po spuštění funkce resource přímo.

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a>Zprávy protokolu jsou snadno pochopitelný a informativní (včetně – verbose, – ladění a protokoly trasování událostí pro Windows)

Zajistěte, aby byly protokoly výstupem prostředkem srozumitelné a zadejte hodnotu pro uživatele. Prostředky by měly výstup všechny informace, které mohou být pro uživatele užitečné, ale další protokoly není vždy lepší. Měli byste vyhnout redundance a výstup dat, která ho nemá zvyšujících hodnotu – neprovádějte někdo projít stovky položek protokolu. Pokud chcete zjistit, co hledají. Samozřejmě žádné protokoly není přijatelná řešení tohoto problému buď.

Při testování, by měl také podrobné analýze a ladění protokoly (spuštěním `Start-DscConfiguration` s `–Verbose` a `–Debug` přepne odpovídajícím způsobem), stejně jako protokoly trasování událostí pro Windows. Pokud chcete zobrazit protokoly trasování událostí pro Windows DSC, přejděte do prohlížeče událostí a otevřete následující složku: Aplikace a služby – Microsoft - Windows - Desired State Configuration.  Ve výchozím nastavení existuje budou provozní kanál, ale ujistěte se, že povolíte analytické a ladit kanály před spuštěním konfigurace.
Povolení analýzy/Debug kanály, můžete spustit skript níže:

```powershell
$statusEnabled = $true
# Use "Analytic" to enable Analytic channel
$eventLogFullName = "Microsoft-Windows-Dsc/Debug"
$commandToExecute = "wevtutil set-log $eventLogFullName /e:$statusEnabled /q:$statusEnabled   "
$log = New-Object System.Diagnostics.Eventing.Reader.EventLogConfiguration $eventLogFullName
if($statusEnabled -eq $log.IsEnabled)
{
    Write-Host -Verbose "The channel event log is already enabled"
    return
}
Invoke-Expression $commandToExecute
```

## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a>Implementace prostředků neobsahuje pevně zakódované cesty

Zkontrolujte v implementaci prostředku nejsou žádné pevně zakódované cesty, zejména v případě, že předpokládají jazyka (en-us), nebo když se systémové proměnné, které lze použít.
Pokud váš prostředek potřebovat přístup ke konkrétní cesty, proměnné prostředí použít namísto hardcoding cestu, protože se může lišit na jiných počítačích.

Příklad:

Namísto:

```powershell
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
```

Můžete psát:

```powershell
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```

## <a name="resource-implementation-does-not-contain-user-information"></a>Implementace prostředků neobsahuje informace o uživateli

Ujistěte se, že neexistují žádné názvy e-mailu, informace o účtu nebo jména osob v kódu.

## <a name="resource-was-tested-with-validinvalid-credentials"></a>Prostředek byl testován s přihlašovacími údaji platná nebo není platné

Pokud váš prostředek přijímá jako parametr přihlašovacích údajů:

- Při místní systém (nebo účet počítače pro vzdálené prostředky) nemá přístup zkontrolujte, jestli funguje prostředků.
- Zkontrolujte prostředek funguje s přihlašovacími údaji zadaný pro získání, nastavení a testování
- Pokud váš prostředek přistupuje ke sdílené složky, otestujte všechny varianty, které potřebujete pro podporu, jako například:
  - Sdílené složky windows na úrovni Standard.
  - Sdílené složky systému souborů DFS.
  - SAMBA složek (Pokud chcete zajistit podporu Linuxu.)

## <a name="resource-does-not-require-interactive-input"></a>Prostředek nepotřebuje interaktivní vstup

**Get/Set/Test-TargetResource** funkce by měla být spouštěny automaticky a nesmí čekat, až se uživatelovo zadání v jakékoli fázi spuštění (například byste neměli používat `Get-Credential` uvnitř těchto funkcí). Pokud je třeba zadat uživatelský vstup, je třeba předat ho do konfigurace jako parametr během fáze kompilace.

## <a name="resource-functionality-was-thoroughly-tested"></a>Funkce prostředků byla důkladně otestována.

Tento kontrolní seznam obsahuje položky, které jsou důležité k testování a/nebo jsou často provedena. Bude existovat mnoho testů, hlavně funkční ty, které budou mít specifická pro prostředek, testování a nejsou zde uvedeny. Nezapomeňte o záporné testovací případy.

## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a>Osvědčený postup: Modul prostředků obsahuje složku testy s ResourceDesignerTests.ps1 skriptu

Je vhodné vytvořit složku "testy" uvnitř modulu prostředků, vytvořte `ResourceDesignerTests.ps1` a přidejte testy pomocí **testovací xDscResource** a **testovací xDscSchema** pro všechny prostředky v zadané modulu.
Tímto způsobem můžete rychle ověřit schémata všechny prostředky z daného moduly a nechcete, zkontrolujte vhodnosti před publikováním.
Pro xRemoteFile `ResourceTests.ps1` může vypadat stejně snadné jako:

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a>Osvědčený postup: Složka prostředků obsahuje návrháře skript prostředků pro generování schématu

Každý prostředek by měl obsahovat návrháře skript prostředků, který generuje schématu mof prostředku. Tento soubor by měl být umístěn v `<ResourceName>\ResourceDesignerScripts` a bude mít název generovat `<ResourceName>Schema.ps1` xRemoteFile prostředků tento soubor bude označovat `GenerateXRemoteFileSchema.ps1` a obsahovat:

```powershell
$DestinationPath = New-xDscResourceProperty -Name DestinationPath -Type String -Attribute Key -Description 'Path under which downloaded or copied file should be accessible after operation.'
$Uri = New-xDscResourceProperty -Name Uri -Type String -Attribute Required -Description 'Uri of a file which should be copied or downloaded. This parameter supports HTTP and HTTPS values.'
$Headers = New-xDscResourceProperty -Name Headers -Type Hashtable[] -Attribute Write -Description 'Headers of the web request.'
$UserAgent = New-xDscResourceProperty -Name UserAgent -Type String -Attribute Write -Description 'User agent for the web request.'
$Ensure = New-xDscResourceProperty -Name Ensure -Type String -Attribute Read -ValidateSet "Present", "Absent" -Description 'Says whether DestinationPath exists on the machine'
$Credential = New-xDscResourceProperty -Name Credential -Type PSCredential -Attribute Write -Description 'Specifies a user account that has permission to send the request.'
$CertificateThumbprint = New-xDscResourceProperty -Name CertificateThumbprint -Type String -Attribute Write -Description 'Digital public key certificate that is used to send the request.'

New-xDscResource -Name MSFT_xRemoteFile -Property @($DestinationPath, $Uri, $Headers, $UserAgent, $Ensure, $Credential, $CertificateThumbprint) -ModuleName xPSDesiredStateConfiguration2 -FriendlyName xRemoteFile
```

## <a name="best-practice-resource-supports--whatif"></a>Osvědčený postup: Prostředek podporuje – WhatIf

Pokud váš prostředek je provádění operací "nebezpečných", je vhodné provádět `-WhatIf` funkce. Po dokončení, ujistěte se, že `-WhatIf` výstup správně popisuje operace, které by mohlo dojít, pokud příkaz se provedl zcela bez `-WhatIf` přepnout.
Ověřte také, že operace nespustí (nebudou provedeny žádné změny uzlu stavu) při `–WhatIf` přepínači je k dispozici.
Předpokládejme například, že se testují souboru prostředků. Níže je jednoduchý konfigurace, která vytvoří soubor `test.txt` s obsahem "test":

```powershell
configuration config
{
    node localhost
    {
        File file
        {
            Contents="test"
            DestinationPath="C:\test\test.txt"
        }
    }
}
config
```

Pokud jsme kompilovat a pak proveďte konfiguraci `-WhatIf` přepínače, výstup se dozvíme přesně co by mohlo dojít při konfiguraci zajišťuje každodenní provoz. V konfiguraci samotného ale neprovedl (`test.txt` soubor nebyl vytvořen).

```powershell
Start-DscConfiguration -Path .\config -ComputerName localhost -Wait -Verbose -WhatIf
```

```output
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer CHARLESX1 with user sid
S-1-5-21-397955417-626881126-188441444-5179871.
What if: [X]: LCM:  [ Start  Set      ]
What if: [X]: LCM:  [ Start  Resource ]  [[File]file]
What if: [X]: LCM:  [ Start  Test     ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]: LCM:  [ End    Test     ]  [[File]file]  in 0.0270 seconds.
What if: [X]: LCM:  [ Start  Set      ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]:                            [C:\test\test.txt] Creating and writing contents and setting attributes.
What if: [X]: LCM:  [ End    Set      ]  [[File]file]  in 0.0180 seconds.
What if: [X]: LCM:  [ End    Resource ]  [[File]file]
What if: [X]: LCM:  [ End    Set      ]
VERBOSE: [X]: LCM:  [ End    Set      ]    in  0.1050 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
```

Tento seznam není úplný, ale zahrnuje mnoho důležité problémy, které může dojít při navrhování, vývoj a testování prostředky DSC.

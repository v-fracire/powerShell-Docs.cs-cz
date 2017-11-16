---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Kontrolní seznam pro tvorbu prostředků"
ms.openlocfilehash: 9e9855f4ad4ee6db4d9e3b90d3c9a03d81429805
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="resource-authoring-checklist"></a>Kontrolní seznam pro tvorbu prostředků
Tento kontrolní seznam je seznam osvědčené postupy při vytváření nového prostředku DSC.
## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a>Modul prostředků obsahuje soubor .psd1 a schema.mof pro každý prostředek 
Zkontrolujte, zda prostředek má správnou strukturu a obsahuje všechny požadované soubory. Každý modul prostředků by měl obsahovat soubor .psd1 a každý jiný složené prostředků musí mít schema.mof souboru. Prostředky, které neobsahují schématu nebude uvedené podle **Get-DscResource** a uživatelé nebudou moci používat intellisense při psaní kódu pro tyto moduly (ISE) v. Strukturu adresáře pro prostředek xRemoteFile, která je součástí systému [xPSDesiredStateConfiguration prostředků modulu](https://github.com/PowerShell/xPSDesiredStateConfiguration), vypadá takto:


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

## <a name="resource-and-schema-are-correct"></a>Prostředek a schématu jsou správné ##
Ověření schématu zdroje (*. schema.mof) souboru. Můžete použít [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) usnadňuje vývoj a testování schéma. Ujistěte se, že:
- Typy vlastností jsou správné (například nepoužívejte řetězec pro vlastnosti, které přijímají číselných hodnot, byste měli používat místo toho UInt32 nebo jiných číselnými typy)
- Vlastnost atributy jsou správně zadané jako: ([klíč], [vyžaduje], [zapisovat], [přečíst])
- Minimálně jeden parametr ve schématu musí být označeny jako [klíč]
- [přečíst] vlastnost není existovat společně, spolu s případnými systému: [vyžaduje], [key], [zapsat.]
- Pokud více kvalifikátory jsou zadaný – s výjimkou [čtení], pak [klíč] má přednost před
- Pokud [zapsat.] a [vyžaduje] jsou zadaný, bude [vyžaduje] přednost
- Je zadán chybu, kde je to vhodné

Příklad:
```
[Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
```

- Popisný název je zadán a potvrdí, k DSC zásady vytváření názvů

Příklad: ```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```

- Každé pole má výstižný popis. Úložiště GitHub prostředí PowerShell, jako má dobrými příklady [. schema.mof pro xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)

Kromě toho byste měli používat **Test xDscResource** a **Test xDscSchema** rutiny z [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) automaticky ověření prostředků a schématu:
```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```
Příklad:
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a>Načte prostředek bez chyby ##
Zkontrolujte, zda modul prostředků mohou být úspěšně načteny.
Toho lze dosáhnout ručně spuštěním `Import-Module <resource_module> -force ` a potvrzení, že nedošlo k žádným chybám, nebo pomocí zápis test automatizace. V případě k tomu můžete následující strukturu v testovací případ:
```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```
## <a name="resource-is-idempotent-in-the-positive-case"></a>Prostředek je idempotent v případě, že kladné 
Mezi základní charakteristiky prostředků DSC je možné idempotenci. Znamená to, že použití konfigurace DSC, tento prostředek obsahující více než jednou. bude vždy dosažení stejného výsledku. Pokud například vytvoříme konfigurace, který obsahuje následující prostředek souboru:
```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
} 
```
Po jeho použití poprvé, by se zobrazit test.txt soubor ve složce C:\test. Při dalším spuštění stejnou konfiguraci nesmí však změnit stav počítače (například žádné kopie souboru test.txt by měl vytvořit).
Pro zajištění prostředek idempotent opakovaně můžete volat **Set-TargetResource** při testování prostředku přímo, nebo volejte **Start-DscConfiguration** více než jednou. při provádění testování koncové. Výsledek by měl být stejný po každé spuštění. 


## <a name="test-user-modification-scenario"></a>Scénáře úpravy uživatele testu ##
Změnou stavu počítače a pak znovu spustit DSC, můžete ověřit, která **Set-TargetResource** a **Test TargetResource** fungovat správně. Zde jsou kroky, které byste měli vzít:
1.  Začněte u prostředku není v požadovaném stavu.
2.  Spuštění konfigurace pomocí vaší prostředků
3.  Ověřte **Test DscConfiguration** vrátí hodnotu True.
4.  Upravit nakonfigurované položka, která má být mimo požadovaný stav
5.  Ověřte **Test DscConfiguration** vrací hodnotu false, tady je příklad konkrétnější pomocí registru prostředků:
1.  Spustit s klíčem registru není v požadovaném stavu
2.  Spustit **Start-DscConfiguration** s konfigurací a umístí jej v požadovaném stavu ověření předá.
3.  Spustit **Test DscConfiguration** a ověřte, vrátí hodnotu true
4.  Změňte hodnotu klíče, aby není v požadovaném stavu
5.  Spustit **Test DscConfiguration** a ověřte, vrátí hodnotu false
6.  Get-TargetResource funkce byla ověřena pomocí Get-DscConfiguration

Get-TargetResource by měl vrátit podrobnosti o aktuálním stavem prostředku. Ujistěte se, že testovací volání Get-DscConfiguration po dokončení konfigurace a ověření, že výstupní správně odráží aktuální stav počítače. Je důležité k testování samostatně, protože všechny problémy v této oblasti se nezobrazí při volání metody DscConfiguration spuštění.

## <a name="call-getsettest-targetresource-functions-directly"></a>Volání **Get/Set nebo Test-TargetResource** přímo funkce ##

Zajistěte, aby testování **Get/Set nebo Test-TargetResource** funkce implementované v prostředku přímé volání a ověření, že fungují podle očekávání.

## <a name="verify-end-to-end-using-start-dscconfiguration"></a>Ověřit pomocí koncová **Start DscConfiguration** ##

Testování **Get/Set nebo Test-TargetResource** funkcí podle přímé volání je důležité, ale ne všechny problémy budou zjištěny tímto způsobem. Měli byste se zaměřit významnou část testování na pomocí **Start-DscConfiguration** nebo serveru pro vyžádání obsahu. Ve skutečnosti to je, jak budou uživatelé používat k prostředku, a to tak není příliš nízko, násobek tohoto typu testů. Možné typy problémů:
- Přihlašovací údaje nebo relace může chovat jinak, protože DSC agent běží jako služba.  Nezapomeňte otestovat všechny funkce, zde začátku do konce.
- Chyby výstupem **Start-DscConfiguration** může být jiný než ty, které zobrazí při volání metody **Set-TargetResource** funkce přímo.

## <a name="test-compatability-on-all-dsc-supported-platforms"></a>Test kompatibility na DSC všechny podporované platformy ##
Prostředek by měly fungovat na všech platformách DSC podporované (Windows Server 2008 R2 a novější). Nainstalujte poslední verzi WMF (Windows Management Framework) v operačním systému získat nejnovější verzi DSC. Pokud prostředek nefunguje na některé z těchto platforem záměrné, má být vrácen konkrétní chybová zpráva. Taky se ujistěte, že prostředek ověří, zda jsou rutiny, ke kterému se připojujete na konkrétním počítači. Windows Server 2012 přidat velký počet nových rutin, které nejsou k dispozici v systému Windows Server 2008 R2, i s WMF nainstalována. 

## <a name="verify-on-windows-client-if-applicable"></a>Ověřte v klientovi Windows (pokud existuje) ##
Jeden velmi běžné mezera testovací ověřuje prostředků pouze v serverových verzí systému Windows. Mnoho prostředků jsou navrženy pro práci na SKU klienta, takže pokud je to pravda v váš případ, nezapomeňte otestovat ji na těchto platformách také. 
## <a name="get-dscresource-lists-the-resource"></a>Get-DSCResource uvádí prostředku ##
Po nasazení modul, volání Get-DscResource by měl seznam prostředku ostatních v důsledku. Pokud prostředek nelze najít v seznamu, ověřte, zda tento soubor schema.mof pro tento prostředek existuje. 
## <a name="resource-module-contains-examples"></a>Modul prostředků obsahuje příklady ##
Vytváření kvality příklady, které pomůže ostatním pochopit, jak ho použít. To je velmi důležitý, zejména od mnoha uživateli považovat za dokumentaci ukázkový kód. 
- Nejdřív musíte si ujasnit některé příklady, které budou zahrnuty s modulem – alespoň, by mělo zahrnovat nejdůležitější případy použití pro prostředek:
- Pokud modul obsahuje několik prostředků, které je potřeba spolupracují scénář začátku do konce, základní příklad začátku do konce v ideálním případě by první.
- Počáteční příklady by měl být velmi jednoduché – jak začít pracovat s vaše prostředky v malých spravovatelných blocích (např. k vytvoření nového virtuálního pevného disku)
- Následující příklady by měl vytvářet na tyto příklady (např. vytvoření virtuálního počítače z disku VHD, odebrání virtuálního počítače, změny virtuálního počítače) a zobrazit pokročilé funkce (např. vytvoření virtuálního počítače s dynamickou pamětí)
- Příklad konfigurace by měly být parametrizovány (všech hodnot, které mají být předány do konfigurace jako parametry a měla by existovat žádné hodnoty pevně zakódované):
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
- Je dobrým zvykem zahrnují (komentovaný out) příklad toho, jak volat konfigurace se skutečnými hodnotami na konci ukázkový skript. Například v konfiguraci výše není nutně zřejmé, že je nejlepší způsob, jak určit UserAgent:

`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer`  
V takovém případě komentář mohou objasnit zamýšlený provedení konfigurace:
```
<# 
Sample use (parameter values need to be changed according to your scenario):

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
-userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
#>  
```
- Každý například zápisu krátký popis, která vysvětluje, co znamená a význam vlastností parametrů. 
- Zajistěte, aby příklady zahrnují většině scénářů, které jsou důležité pro prostředek a pokud není nic chybí, ověřte, zda se všechny provést a uveďte počítač s požadovaným stavem.  

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a>Chybové zprávy se dají snadno pochopit a pomáhají uživatelům řešit problémy ##
By měla být funkční chybové zprávy:
- : Největších problém s chybové zprávy není, často neexistují, proto se ujistěte, že jsou dispozici. 
- Snadno pochopitelné: lidské čitelný, ne skrytého chybové kódy
- Přesné: Popisují, co je přesně tento problém
- Konstruktivní: Rady informace o vyřešení problému
- Celkem: Nemáte viny uživatele nebo zajistěte, je zaregistrované chybný Ujistěte se, ověřte chyby ve scénářích koncová (pomocí **Start-DscConfiguration**), protože se mohou lišit od těch vrácená při spuštění funkce prostředků přímo. 

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a>Zprávy protokolu jsou snadno pochopit a informativní (včetně – podrobné nastavení, – protokoly trasování a ladění) ##
Zkontrolujte, zda jsou protokoly výstupem prostředkem snadno pochopit a zadejte hodnotu pro uživatele. Prostředky by výstup všechny informace, které mohou být užitečné pro uživatele, ale další protokoly není vždy lepší. Měli byste vyhnout redundance a odesíláním dat, která ho nemá zadejte další hodnotu – nevytvářejte někdo projít stovky položky protokolu, aby bylo možné najít, co hledají. Samozřejmě žádné protokoly není přijatelného řešení tohoto problému buď. 

Při testování, by také analyzovat podrobné a ladění protokoly (spuštěním **Start-DscConfiguration** s – podrobné a – ladění přepínače správně), stejně jako protokoly trasování událostí pro Windows. Chcete-li zobrazit protokoly trasování událostí pro Windows DSC, přejděte do prohlížeče událostí a otevřete následující složku: aplikací a konfigurace požadovaného stavu služby společnosti Microsoft - Windows -.  Ve výchozím nastavení existuje budou provozní kanál, ale zajistěte, aby povolíte analýzu a ladit kanály před spuštěním konfigurace. Pokud chcete povolit kanály analýzy nebo ladění, můžete provést níže uvedený skript:
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
## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a>Implementace prostředků neobsahuje pevně zakódované cesty ##
Ujistěte se, neexistují žádné cesty pevně kódovaný v provádění prostředku, zvlášť pokud převzaly jazyka (en-us), nebo když se systémové proměnné, které lze použít.
Pokud prostředek potřebovat přístup k určité cesty, pomocí proměnné prostředí místo hardcoding cesty, protože se mohou lišit na jiné počítače.

Příklad:

Namísto:
```
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
 ```
Můžete napsat:
```
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)} 
```
## <a name="resource-implementation-does-not-contain-user-information"></a>Implementace prostředků neobsahuje informace o uživateli ##
Ujistěte se, že neexistují žádné e-mailu, informace o účtu nebo jména osob v kódu.
## <a name="resource-was-tested-with-validinvalid-credentials"></a>Prostředek byla testována s platnou nebo neplatná pověření ##
Pokud prostředek přijímá pověření jako parametr:
- Ověření funguje prostředků místní systém (nebo účet počítače pro vzdálené prostředky) nemá přístup.
- Ověřte prostředků funguje s pověření zadaná pro získáte nastavené a testování 
- Pokud získá přístup k prostředku sdílené složky, otestujte všechny varianty, které potřebujete podporovat, jako například:
  - Standardní windows sdílené složky.
  - Sdílené složky systému souborů DFS.
  - SAMBA sdílených složek (Pokud chcete podporovat Linux.)

## <a name="resource-does-not-require-interactive-input"></a>Prostředek nepotřebuje interaktivní vstup ##
**Get/Set nebo Test-TargetResource** funkce budou automaticky spuštěny a nesmí počkejte uživatelský vstup v jakékoli fázi provádění (například byste neměli používat **Get-Credential** uvnitř tyto funkce). Když musíte zadat uživatelský vstup, musí se předat do konfigurace jako parametr během fáze kompilace. 
## <a name="resource-functionality-was-thoroughly-tested"></a>Funkce prostředků byla testována ##
Tento kontrolní seznam obsahuje položky, které jsou důležité má být testována nebo jsou často vynechán. Bude bunch testů, především funkční ty, které mají být specifické pro prostředek, testování a nejsou zde uvedeným. Nezapomeňte záporné testovací případy. 
## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a>Nejvhodnější: modul prostředků obsahuje složku testy s ResourceDesignerTests.ps1 skriptu ##
Je vhodné vytvořit složku "testy" v modulu prostředků, vytvořte soubor ResourceDesignerTests.ps1 a přidejte testů pomocí **Test xDscResource** a **Test xDscSchema** pro všechny prostředky v zadané modul. Tímto způsobem můžete rychle ověřit schémata všechny prostředky z daného moduly a nechcete, správností zkontrolujte před publikováním.
Pro xRemoteFile může vypadat ResourceTests.ps1 stejně jednoduché jako:
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof 
```
##<a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a>Nejvhodnější: Složka prostředků obsahuje prostředků Návrháře skript pro generování schémat ##
Všechny prostředky by měly obsahovat prostředků Návrháře skript, který generuje schéma mof prostředku. Tento soubor musí být umístěny v <ResourceName>\ResourceDesignerScripts a bude mít název generování<ResourceName>Schema.ps1 pro prostředek xRemoteFile tento soubor by být volána GenerateXRemoteFileSchema.ps1 a obsahovat:
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
## <a name="best-practice-resource-supports--whatif"></a>Nejvhodnější: prostředek podporuje - whatif ##
Pokud prostředek provádí "nebezpečné" operace, je vhodné implementovat - whatif funkce. Po dokončení, zajistěte, aby whatif výstup správně popisuje operací, které by mohlo dojít, pokud byl proveden příkaz bez whatif přepínače.
Také ověřte, že operace nepracuje (nebudou provedeny žádné změny stavu uzlu) Pokud je zadán přepínač – whatif. Předpokládejme například, že se testují souboru prostředků. Níže je jednoduchá konfigurace, který vytvoří soubor "test.txt" obsah "test":
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
Pokud jsme zkompilovat a potom spusťte konfigurace s přepínačem – whatif, výstup nám oznamuje přesně co by se stalo při jsme spuštění konfigurace. Konfigurace samotného ale neprovedl (test.txt soubor nebyl vytvořen).
```powershell 
Start-DscConfiguration -path .\config -ComputerName localhost -wait -verbose -whatif
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

Tento seznam není vyčerpávající, týká se však mnoho důležité problémy, které můžete došlo při navrhování, vývoj a testování prostředky DSC.


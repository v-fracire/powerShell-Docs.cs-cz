---
ms.date: 04/11/2018
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Načítací služba DSC
ms.openlocfilehash: 057da50843e79ae31eef4fea1fa58e882a9d1ace
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="desired-state-configuration-pull-service"></a>Vyžádání služba Konfigurace požadovaného stavu

> Platí pro: Prostředí Windows PowerShell 5.0

> [!IMPORTANT]
> Server pro vyžádání obsahu (funkce systému Windows *DSC služby*) je podporované součásti systému Windows Server jsou však nejsou žádné plány, které nabízí nové funkce nebo funkce. Doporučujeme začít Přechod spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace s v systému Windows Server) nebo jedno z řešení komunity uvedené [zde](pullserver.md#community-solutions-for-pull-service).

Správce místní konfigurace můžou být centrálně spravované řešením pro vyžádání obsahu služby.
Pokud používáte tuto metodu, je uzlu, který je spravován zaregistrován službou a přiřazen konfiguraci v LCM nastavení.
Konfigurace a všechny prostředky DSC potřebné jako závislosti pro konfiguraci se stáhnout do počítače a používá LCM ke správě konfigurace.
Informace o stavu je počítač spravován se odešlou do služby pro vytváření sestav.
Tento koncept se označuje jako "vyžádání služba".

Aktuální možnosti pro vyžádání obsahu službu:

- Služba konfigurace stavu žádaný automatizace Azure
- Vyžádání služby spuštěné v systému Windows Server
- Komunita udržovat open-source řešení
- Sdílené složce SMB

**Doporučené řešení**, a s nejvíce funkcemi, které jsou k dispozici, není [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

Uzly na místě v datových centrech privátní nebo veřejné cloudy, například Azure a AWS můžete spravovat službu Azure.
U privátních prostředí, kde nelze servery připojit přímo k Internetu, zvažte omezení odchozí provoz jenom publikované Azure rozsah IP adres (viz [rozsahy IP Datacentra Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).

Funkce služby online, které nejsou momentálně k dispozici ve službě vyžádání v systému Windows Server:
- Všechna data se šifrují během přenosu a v klidovém stavu
- Klientské certifikáty se vytváří a spravují automaticky
- Ukládat tajné klíče pro centrální správu [hesla nebo přihlašovací údaje](/azure/automation/automation-credentials), nebo [proměnné](/azure/automation/automation-variables) například názvy serverů nebo připojovací řetězce
- Centrálně spravovat uzlu [LCM konfigurace](metaConfig.md#basic-settings)
- Centrálně přiřadit konfigurace pro klienta uzly
- Konfigurace verze se změní na "lesknice skupiny" pro testování dříve, než dorazila produkční
- Grafické vytváření sestav
  - Podrobná sestava stavu na úrovni prostředků DSC členitosti
  - Podrobné chybové zprávy z klientských počítačů pro řešení potíží
- [Integrace s Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) pro výstrahy, automatizované úlohy, aplikace pro Android nebo iOS pro vytváření sestav a výstrahy

## <a name="dsc-pull-service-in-windows-server"></a>DSC vyžádání služby v systému Windows Server

Je možné ke konfiguraci služby přijetí změn pro spouštění v systému Windows Server.
Se doporučuje, aby řešení služby vyžádání obsahu, který je součástí systému Windows Server obsahuje pouze funkce ukládání konfigurace nebo moduly pro stahování a zaznamenávání dat sestav v databázi.
Nezahrnuje řadu funkce nabízené služby v Azure a proto není funkční nástroj pro vyhodnocení, jak se použije službu.

Službu vyžádání obsahu k dispozici v systému Windows Server je webová služba ve službě IIS, který používá rozhraní OData k dispozici DSC konfigurační soubory do cílové uzly uzly, zeptejte se pro ně.

Požadavky pro používání serveru vyžádané replikace:

- Serveru se systémem:
  - WMF nebo PowerShell 5.0 nebo novější
  - Role serveru IIS
  - DSC služby
- V ideálním případě některé znamená generování certifikát, k zabezpečení přihlašovacích údajů předaných na místní Configuration Manager (LCM) na cílové uzly

Nejlepší způsob, jak konfigurovat Windows Server k hostitelské službě. vyžádanou je použití konfigurace DSC.
Ukázkový skript je uveden níže.

### <a name="supported-database-systems"></a>Podporované databázové systémy

|FORMÁT WMF 4.0   |WMF 5.0  |WMF 5.1 |Podpora produktu WMF (Windows Server zevnitř Preview 17090) 5.1|
|---------|---------|---------|---------|
|MDB     |ESENT (výchozí), MDB |ESENT (výchozí), MDB|ESENT (výchozí), SQL Server, MDB

Od verze 17090 z [systému Windows Server zevnitř Preview](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server je podporovaná možnost pro službu pro vyžádání obsahu (funkce systému Windows *DSC služby*).  To nabízí novou možnost pro škálování velkých prostředích DSC, které nebyly migrovány do [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

> **Poznámka:**: podpora systému SQL Server se nepřidají k předchozí verze 5.1 WMF (nebo starší) a bude k dispozici v systému Windows Server verze větší než nebo rovna hodnotě 17090 pouze.

Konfigurace serveru vyžádané replikace pro použití systému SQL Server, nastavte **SqlProvider** k `$true` a **SqlConnectionString** na platný připojovací řetězec SQL serveru.  Další informace najdete v tématu [SqlClient připojovací řetězce](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).
Příklad konfigurace SQL serveru s **xDscWebService**, nejdřív přečíst [pomocí prostředků xDscWebService](#using-the-xdscwebservice-resource) a poté zkontrolovat [Sample_xDscWebServiceRegistration_ UseSQLProvider.ps1 na Githubu](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).

### <a name="using-the-xdscwebservice-resource"></a>Pomocí xDscWebService prostředků

Nejjednodušší způsob, jak nastavit webový server vyžádání obsahu je použití **xDscWebService** prostředku, které jsou součástí **xPSDesiredStateConfiguration** modulu.
Následující kroky popisují, jak se daný prostředek v konfiguraci, která nastaví webovou službu.

1. Volání [instalace modulu](/powershell/module/PowershellGet/Install-Module) k instalaci **xPSDesiredStateConfiguration** modulu. **Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0. Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).
1. Získání certifikátu SSL pro vyžádání obsahu DSC server od důvěryhodné certifikační autority, buď v rámci vaší organizace nebo z veřejné autority. Certifikát obdržený od autority je obvykle ve formátu PFX. Nainstalujte certifikát na uzlu, který se stane DSC vyžádání serveru ve výchozím umístění, které by se měly CERT: \LocalMachine\My. Poznamenejte si kryptografický otisk certifikátu.
1. Vyberte identifikátor GUID, který má být použit jako registrační klíč. Generovat jednu pomocí prostředí PowerShell zadejte následující PS řádku a stiskněte klávesu enter: '``` [guid]::newGuid()```'nebo'```New-Guid```'. Tento klíč se použije klient uzly jako sdílený klíč k ověření během registrace. Další informace najdete v části registrační klíč níže.
1. V integrovaném Skriptovacím prostředí PowerShell, spusťte (F5) následující konfigurační skript (zahrnutý ve složce Příklady **xPSDesiredStateConfiguration** modulu jako Sample_xDscWebServiceRegistration.ps1). Tento skript nastaví server vyžádané replikace.

```powershell
configuration Sample_xDscWebServiceRegistration
{
    param
    (
        [string[]]$NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $certificateThumbPrint,

        [Parameter(HelpMessage='This should be a string with enough entropy (randomness) to protect the registration of clients to the pull server.  We will use new GUID by default.')]
        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey   # A guid that clients use to initiate conversation with pull server
    )

    Import-DSCResource -ModuleName xPSDesiredStateConfiguration

    Node $NodeName
    {
        WindowsFeature DSCServiceFeature
        {
            Ensure = "Present"
            Name   = "DSC-Service"
        }

        xDscWebService PSDSCPullServer
        {
            Ensure                  = "Present"
            EndpointName            = "PSDSCPullServer"
            Port                    = 8080
            PhysicalPath            = "$env:SystemDrive\inetpub\PSDSCPullServer"
            CertificateThumbPrint   = $certificateThumbPrint
            ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
            ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
            State                   = "Started"
            DependsOn               = "[WindowsFeature]DSCServiceFeature"
            RegistrationKeyPath     = "$env:PROGRAMFILES\WindowsPowerShell\DscService"
            AcceptSelfSignedCertificates = $true
            Enable32BitAppOnWin64   = $false
        }

        File RegistrationKeyFile
        {
            Ensure          = 'Present'
            Type            = 'File'
            DestinationPath = "$env:ProgramFiles\WindowsPowerShell\DscService\RegistrationKeys.txt"
            Contents        = $RegistrationKey
        }
    }
}
```

1. Spustit v konfiguraci předávání kryptografický otisk certifikátu SSL, jako **certificateThumbPrint** parametr a identifikátor GUID registrační klíč jako **RegistrationKey** parametr:

```powershell
# To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
# and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
dir Cert:\LocalMachine\my

# Then include this thumbprint when running the configuration
Sample_xDSCPullServer -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

# Run the compiled configuration to make the target node a DSC Pull Server
Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
```

#### <a name="registration-key"></a>Registrační klíč

Povolit klientské uzly registraci se serverem a používají názvy konfigurace místo ID konfigurace, registrační klíč, který byl vytvořen výše konfigurace je uložen v souboru s názvem `RegistrationKeys.txt` v `C:\Program Files\WindowsPowerShell\DscService`. Registrační klíč funguje jako sdílený tajný klíč používá při počáteční registraci klienta se serverem pro vyžádání obsahu. Klient vygeneruje certifikát podepsaný svým držitelem, který slouží k jednoznačné ověření na serveru vyžádané replikace po úspěšném dokončení registrace se. Kryptografický otisk tohoto certifikátu je uložený místně a přidružené k adrese URL serveru pro vyžádání obsahu.
> **Poznámka:**: registrace klíče nejsou podporovány v prostředí PowerShell 4.0.

Chcete-li nakonfigurovat uzel k ověření se serverem pro vyžádání obsahu, registrační klíč musí být v metakonfiguraci pro cílový uzel, který bude registrace k tomuto serveru pro vyžádání obsahu. Všimněte si, že **RegistrationKey** v metakonfiguraci níže se odebere po úspěšně zaregistrovala cílový počítač, a hodnota '140a952b-b9d6-406b-b416-e0f759c9c0e4' se musí shodovat s hodnotou uloženou v RegistrationKeys.txt soubor na tomto serveru. Vždy zacházet s hodnotou klíče registrace bezpečně, protože vědomí umožňuje, aby všechny cílové počítače k registraci se serverem pro vyžádání obsahu.

```powershell
[DSCLocalConfigurationManager()]
configuration Sample_MetaConfigurationToRegisterWithLessSecurePullServer
{
    param
    (
        [ValidateNotNullOrEmpty()]
        [string] $NodeName = 'localhost',

        [ValidateNotNullOrEmpty()]
        [string] $RegistrationKey, #same as the one used to setup pull server in previous configuration

        [ValidateNotNullOrEmpty()]
        [string] $ServerName = 'localhost' #node name of the pull server, same as $NodeName used in previous configuration
    )

    Node $NodeName
    {
        Settings
        {
            RefreshMode        = 'Pull'
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL          = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey    = $RegistrationKey
            ConfigurationNames = @('ClientConfig')
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL       = "https://$ServerName`:8080/PSDSCPullServer.svc" # notice it is https
            RegistrationKey = $RegistrationKey
        }
    }
}

Sample_MetaConfigurationToRegisterWithLessSecurePullServer -RegistrationKey $RegistrationKey -OutputPath c:\Configs\TargetNodes
```

> **Poznámka:**: **ReportServerWeb** části umožňuje data k odeslání na server vyžádané replikace pro vytváření sestav.

Nedostatek **ConfigurationID** vlastnost v souboru metakonfiguraci implicitně znamená serveru vyžádané replikace se nepodporuje verze V2 protokol server vyžádané replikace, a proto je požadována počáteční registrace.
Naopak přítomnosti **ConfigurationID** znamená, že se používá protokol server vyžádané replikace verze V1 a neexistuje žádné zpracování registrace.

>**Poznámka:**: V PUSH scénáři chyby existuje v aktuální verzi, díky které je potřeba definovat ConfigurationID vlastnost v souboru metakonfiguraci pro uzly, které nikdy zaregistrovali načítacího serveru. Tato akce vynutí protokol serveru vyžádané replikace V1 a vyhnout zprávy o selhání registrace.

## <a name="placing-configurations-and-resources"></a>Umístění konfigurace a prostředky

Po vyžádání obsahu server dokončení instalačního programu, složky, které jsou definované **ConfigurationPath** a **ModulePath** vlastnosti v konfiguraci serveru vyžádané replikace jsou, kam umístíte modulů a konfigurací které budou k dispozici pro cílové uzly načítat.
Tyto soubory musí být v konkrétním formátu v pořadí pro vyžádání obsahu server správně zpracovat.

### <a name="dsc-resource-module-package-format"></a>Formát balíčku modulu prostředků DSC

Každý modul prostředků musí být ZIP a s názvem podle vzoru následující `{Module Name}_{Module Version}.zip`.
Například modul s názvem xWebAdminstration verzí modulu 3.1.2.0 by se jmenovala 'xWebAdministration_3.2.1.0.zip'.
Každá verze nástroje modul musí být obsažena v souboru zip jeden.
Vzhledem k tomu, že existuje jenom jedna verze nástroje prostředků do každého souboru zip, formát modulu přidána v WMF 5.0 se podpora pro více verze modulu v jednom adresáři není podporovaný.
To znamená, že před zabalení moduly prostředků DSC pro použití s načítacího serveru budete muset provést změnu malá strukturu adresáře.
Výchozí formát modulů obsahující prostředek DSC v WMF 5.0 je ' {složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'.
Před balení pro vyžádání obsahu serveru, odeberte **{verze modulu}** složky, stane se cesta ' {složku modulu} \DscResources\{Složka prostředků DSC}\'.
Díky této změně zip složce, jak je popsáno výše a nastavovat tyto soubory zip v **ModulePath** složky.

Použití `New-DscChecksum {module zip file}` vytvořit soubor kontrolního součtu pro nově přidaným modulem.

### <a name="configuration-mof-format"></a>Formát MOF konfigurace

Konfigurační soubor MOF musí být spárována s soubor kontrolního součtu, takže LCM na cílový uzel můžete konfiguraci ověřit.
Chcete-li vytvořit kontrolní součet, zavolejte [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) rutiny.
Rutina trvá **cesta** parametr, který určuje složku, kde se nachází v konfiguraci MOF.
Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.
Pokud existují minimálně jedna konfigurace soubory MOF do určené složky, vytvoří se pro každou konfiguraci ve složce kontrolní součet.
Umístěte soubory MOF a jejich přidružené kontrolního součtu souborů v **ConfigurationPath** složky.

>**Poznámka:**: Pokud změníte konfigurační soubor MOF žádným způsobem, musíte také znovu vytvořit soubor kontrolního součtu.

### <a name="tooling"></a>Nástrojů

Chcete-li nastavení tvoří, ověření a Správa serveru vyžádané replikace jednodušší, tyto nástroje jsou zahrnuty jako příklady v nejnovější verzi modulu xPSDesiredStateConfiguration:

1. Modul, který vám pomůže s balení moduly prostředků DSC a konfigurační soubory pro použití na tomto serveru. [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1). Následující příklady:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. Skript, který ověří načítacího serveru správně nakonfigurován. [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).

## <a name="community-solutions-for-pull-service"></a>Řešení komunity pro vyžádání obsahu služby

Komunita DSC má vytvořené více řešení k implementaci protokol služby vyžádání obsahu.
Pro místní prostředí tyto nabízí možnosti služby vyžádání obsahu a příležitost přispívání do komunity Přírůstkové vylepšení.

- [Tug](https://github.com/powershellorg/tug)
- [DSC TRÆK](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a>Konfigurace klienta pro vyžádání obsahu

Následující témata popisují nastavení klientů pro vyžádání obsahu podrobně:

- [Nastavení klienta vyžádání DSC pomocí ID konfigurace](pullClientConfigID.md)
- [Nastavení klienta vyžádání DSC pomocí názvy konfigurace](pullClientConfigNames.md)
- [Částečné konfigurace](partialConfigs.md)

## <a name="see-also"></a>Viz taky

- [Přehled stavu konfigurace požadovaného prostředí Windows PowerShell](overview.md)
- [Přijetí konfigurace](enactingConfigurations.md)
- [Použití serveru sestav DSC](reportServer.md)
- [[MS-DSCPM]: Desired State Configuration přijetí změn modelu protokolu](https://msdn.microsoft.com/library/dn393548.aspx)
- [[MS-DSCPM]: Desired State Configuration přijetí změn modelu protokol chyby](https://msdn.microsoft.com/library/mt612824.aspx)
---
ms.date: 04/11/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Načítací služba DSC
ms.openlocfilehash: 2ef48b88cc9e14da452e0d19e5a0f43fc8a95ab2
ms.sourcegitcommit: 91786b03704fbd2d185f674df0bc67faddfb6288
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2018
ms.locfileid: "51619156"
---
# <a name="desired-state-configuration-pull-service"></a>Načítací služba Desired State Configuration

> Platí pro: Windows PowerShell 5.0

> [!IMPORTANT]
> Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce. Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).

Local Configuration Manageru můžete centrálně spravovat řešení o přijetí změn služby.
Při použití tohoto přístupu je uzel, který je spravován registrován pomocí služby a přiřazené konfigurace LCM nastavení.
Konfigurace a všechny prostředky DSC potřebné jako závislosti pro konfiguraci se stáhl do počítače a slouží ke správě konfigurace LCM.
Informace o stavu je počítač spravován se odešlou do služby pro vytváření sestav.
Tento koncept se označuje jako "službu přijetí změn."

Aktuální možnosti pro službu přijetí změn:

- Služba Azure Automation Desired State Configuration
- Načítací služba běží na Windows serveru
- Udržuje komunity open source řešení
- Do sdílené složky SMB

**Doporučené řešení**, a možnost s nejvíce funkcemi, které jsou k dispozici, je [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

Služba Azure můžete spravovat uzly s místními v privátní síti datových center nebo ve veřejných cloudech, jako jsou Azure a AWS.
Pro privátní prostředí, kde servery nemohou připojit přímo k Internetu, zvažte omezení odchozího provozu do publikované rozsah IP adres Azure (viz [Azure rozsahů IP adres Datacentra](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).

Funkce služby online, které nejsou aktuálně dostupné ve službě o přijetí změn ve Windows serveru:
- Všechna data se šifrují přenášená i neaktivní
- Vytvoření a správa automaticky klientské certifikáty
- Uložení tajných kódů pro centrální správu [hesla nebo přihlašovací údaje](/azure/automation/automation-credentials), nebo [proměnné](/azure/automation/automation-variables) například názvy serverů nebo připojovací řetězce
- Centrálně spravovat uzel [konfigurace LCM](metaConfig.md#basic-settings)
- Centrálně přiřadit konfigurace k uzlům klienta
- Konfigurace vydané verze se změní na "testovací skupiny" pro testování před dosažením produkčního prostředí
- Grafické vytváření sestav
  - Podrobnosti stavu na úrovni členitosti prostředků DSC
  - Podrobné chybové zprávy z klientských počítačů pro řešení potíží
- [Integrace s Azure Log Analytics](/azure/automation/automation-dsc-diagnostics) pro výstrahy, automatizovaných úloh, aplikace pro Android nebo iOS pro generování sestav a upozorňování

## <a name="dsc-pull-service-in-windows-server"></a>Načítací služba DSC v systému Windows Server

Je možné ke konfiguraci službu o přijetí změn, která běží na Windows serveru.
Informováni, že řešení služby o přijetí změn ve Windows serveru zahrnuje pouze možnosti ukládání konfigurace/moduly ke stažení a zaznamenávání dat sestavy do databáze.
Nezahrnuje mnoho funkcí, které nabízí služba v Azure a proto není nástroj vhodný pro vaše rozhodnutí vyzkoušet by použití služby.

Načítací služba nabízí ve Windows serveru je webová služba ve službě IIS, která používá rozhraní OData DSC konfigurační soubory k dispozici na na cílové uzly ty uzly, požádat o nich.

Požadavky na použití serveru vyžádané replikace:

- Serveru se systémem:
  - WMF/PowerShell 5.0 nebo novější
  - Role serveru služby IIS
  - Služba DSC
- V ideálním případě některé znamená, že generování certifikát k zabezpečení přihlašovacích údajů předaných do místní Configuration Manageru (LCM) na cílové uzly

Nejlepší způsob, jak konfigurovat Windows Server k hostitelské službě modulu o přijetí změn je chcete použít konfiguraci DSC.
Ukázkový skript jsou uvedeny níže.

### <a name="supported-database-systems"></a>Podporované databázové systémy

|WMF 4.0   |WMF 5.0  |WMF 5.1 |WMF 5.1 (Windows Server Insider Preview 17090)|
|---------|---------|---------|---------|
|MDB     |ESENT (výchozí), MDB |ESENT (výchozí), MDB|ESENT (výchozí), SQL Server, MDB

Od verze 17090 z [Insider Preview systému Windows Server](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver), SQL Server je podporovaná možnost pro službu o přijetí změn (funkce Windows *DSC služby*).  To poskytne nové možnosti pro škálování velkých prostředích DSC, které jste nemigrovali do [Azure Automation DSC](/azure/automation/automation-dsc-getting-started).

> **Poznámka:**: podpora systému SQL Server nebude přidán do předchozí verze WMF 5.1 (nebo starší) a budou k dispozici na Windows Server verze větší než nebo rovna hodnotě 17090 pouze.

Chcete-li nakonfigurovat serveru vyžádané replikace používat SQL Server, nastavte **SqlProvider** k `$true` a **SqlConnectionString** na platný připojovací řetězec SQL serveru.  Další informace najdete v tématu [SqlClient připojovací řetězce](/dotnet/framework/data/adonet/connection-string-syntax#sqlclient-connection-strings).
Příklad konfigurace SQL serveru s **xDscWebService**, nejdřív přečíst [pomocí prostředků xDscWebService](#using-the-xdscwebservice-resource) a pak si projděte [Sample_xDscWebServiceRegistration_ UseSQLProvider.ps1 na Githubu](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/Examples/Sample_xDscWebServiceRegistration_UseSQLProvider.ps1).

### <a name="using-the-xdscwebservice-resource"></a>Použití prostředků xDscWebService

Nejjednodušší způsob, jak nastavit webového serveru vyžádané replikace je použít **xDscWebService** zdrojů, součástí **xPSDesiredStateConfiguration** modulu.
Následující postup vysvětluje, jak použít zdroje v konfiguraci, který nastaví kolekci webové služby.

1. Volání [Install-Module](/powershell/module/PowershellGet/Install-Module) rutinu instalace **xPSDesiredStateConfiguration** modulu. **Poznámka:**: **Install-Module** je součástí **PowerShellGet** modulu, která je obsažena v Powershellu 5.0. Můžete stáhnout **PowerShellGet** modulu pro PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).
1. Získejte certifikát SSL pro server o přijetí změn DSC od důvěryhodné certifikační autority, buď v rámci vaší organizace nebo veřejné autority. Certifikát obdržený od autority se obvykle ve formátu PFX. Nainstalujte certifikát na uzlu, který se stane serveru vyžádané replikace DSC ve výchozím umístění, které by se měly CERT: \LocalMachine\My. Poznamenejte si kryptografický otisk certifikátu.
1. Vyberte identifikátor GUID, který se použije jako registrační klíč. Chcete-li vygenerovat pomocí prostředí PowerShell zadejte na příkazovém řádku PS a stiskněte klávesu enter: "``` [guid]::newGuid()```'nebo'```New-Guid```". Tento klíč se použije klient uzly jako sdílený klíč k ověření během registrace. Další informace najdete v článku níže uvedené části registrační klíč.
1. V prostředí PowerShell ISE spustit (F5) následující konfigurační skript (zahrnutý ve složce Příklady **xPSDesiredStateConfiguration** modul jako Sample_xDscWebServiceRegistration.ps1). Tento skript nastaví serveru vyžádané replikace.

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

1. Spustit konfiguraci předávání kryptografický otisk certifikátu protokolu SSL, jako **certificateThumbPrint** parametr a identifikátor GUID registrační klíč jako **RegistrationKey** parametr:

    ```powershell
    # To find the Thumbprint for an installed SSL certificate for use with the pull server list all certificates in your local store
    # and then copy the thumbprint for the appropriate certificate by reviewing the certificate subjects
    dir Cert:\LocalMachine\my

    # Then include this thumbprint when running the configuration
    Sample_xDscWebServiceRegistration -certificateThumbprint 'A7000024B753FA6FFF88E966FD6E19301FAE9CCC' -RegistrationKey '140a952b-b9d6-406b-b416-e0f759c9c0e4' -OutputPath c:\Configs\PullServer

    # Run the compiled configuration to make the target node a DSC Pull Server
    Start-DscConfiguration -Path c:\Configs\PullServer -Wait -Verbose
    ```

#### <a name="registration-key"></a>Registrační klíč

Povolit klientské uzly zaregistrovat serveru tak, aby se používají názvy konfigurace namísto ID konfigurace, registrační klíč, který byl vytvořen v konfiguraci uvedené výš se uloží do souboru s názvem `RegistrationKeys.txt` v `C:\Program Files\WindowsPowerShell\DscService`. Registrační klíč funguje jako sdílený tajný klíč použít při počáteční registraci klienta se serverem pro vyžádání obsahu. Klient vygeneruje certifikát podepsaný svým držitelem, který slouží k jednoznačné ověření na serveru vyžádané replikace po úspěšném dokončení registrace. Kryptografický otisk tohoto certifikátu se ukládají místně a přidružené k adrese URL serveru vyžádané replikace.
> **Poznámka:**: registrace klíče nejsou podporovány v Powershellu 4.0.

Aby bylo možné konfigurovat uzel k ověření na serveru vyžádané replikace, registrační klíč musí být v metaconfiguration pro libovolný cílový uzel, který se registruje k tomuto serveru o přijetí změn. Všimněte si, **RegistrationKey** ve níže metaconfiguration se odebere, až cílový počítač se úspěšně zaregistrovala, a hodnota "140a952b-b9d6-406b-b416-e0f759c9c0e4" musí odpovídat hodnotu uloženou v RegistrationKeys.txt soubor na serveru vyžádané replikace. Je vždy nutné považovat hodnotu klíče registrace bezpečné, protože mého vědomí jakékoli cílový počítač zaregistrovat u serveru vyžádané replikace.

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

> **Poznámka:**: **ReportServerWeb** část umožňuje vykazování dat k odeslání do serveru vyžádané replikace.

Chybějící **ConfigurationID** vlastnost v souboru metaconfiguration implicitně znamená, že tohoto serveru vyžádané replikace se nepodporuje V2 verze serveru protokolu o přijetí změn, a proto počáteční registrace je povinný.
Naopak přítomnost **ConfigurationID** znamená, že je použita verze V1 serveru protokolu o přijetí změn a neexistuje žádné zpracování registrace.

>**Poznámka:**: V vložit scénář chybu existuje v aktuální verzi, díky které je potřeba definovat vlastnost ConfigurationID v souboru metaconfiguration uzlů, které jste nikdy zaregistrované serveru vyžádané replikace. Se vynutí protokol serveru vyžádané replikace V1 a vyhněte se zprávy o selhání registrace.

## <a name="placing-configurations-and-resources"></a>Uvedení konfigurací a prostředků

Za operace přijetí změn server dokončení instalačního programu, určené složky **ConfigurationPath** a **ModulePath** vlastnosti v konfiguraci serveru o přijetí změn jsou, kam umístíte modulů a konfigurací který bude k dispozici pro cílové uzly na vyžádání.
Tyto soubory musí být v určitém formátu mohl serveru vyžádané replikace správně jejich zpracování.

### <a name="dsc-resource-module-package-format"></a>Formát balíčku modulu prostředků DSC

Každý modul prostředků musí být metoda ZIP a s názvem podle následujícího vzoru `{Module Name}_{Module Version}.zip`.
Například modul s názvem xWebAdminstration s verzí modulu 3.1.2.0 by se pojmenoval "xWebAdministration_3.2.1.0.zip".
Každá verze modulu musí být součástí jedné zip soubor.
Vzhledem k tomu, že existuje pouze jedna verze prostředku v každém souboru zip, formát modulu přidáno ve WMF 5.0 díky podpoře pro více verzí modulu v jednom adresáři není podporován.
To znamená, že před zabalení moduly prostředků DSC pro použití se serverem o přijetí změn budete muset proveďte malou změnu do struktury adresářů.
Výchozí formát pro moduly obsahující prostředek DSC ve WMF 5.0 je "{složku modulu}\{verze modulu} \DscResources\{Složka prostředků DSC}\'.
Před balení do serveru vyžádané replikace, odeberte **{verze modulu}** složky, stane se cesta "{složku modulu} \DscResources\{Složka prostředků DSC}\'.
Díky této změně zip složce, jak je popsáno výše a umístí tyto souboru zip v **ModulePath** složky.

Použití `New-DscChecksum {module zip file}` vytvoření kontrolního součtu souboru pro nově přidaném modulu.

### <a name="configuration-mof-format"></a>Formát MOF konfigurace

Konfiguračního souboru MOF musí být párována s typem kontrolního součtu souboru tak, aby LCM na cílový uzel můžete konfiguraci ověřit.
Chcete-li vytvořit kontrolní součet, zavolejte [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DscChecksum) rutiny.
Přijímá rutina **cesta** parametr, který určuje složku, ve kterém se nachází konfigurační soubor MOF.
Rutina vytvoří kontrolní součet souboru s názvem `ConfigurationMOFName.mof.checksum`, kde `ConfigurationMOFName` je název konfiguračního souboru mof.
Pokud existuje více než jednu konfiguraci soubory MOF v zadané složce, kontrolní součet se vytvoří pro každou konfiguraci ve složce.
Umístěte soubory MOF a jejich přidružené kontrolního součtu souborů v **ConfigurationPath** složky.

>**Poznámka:**: Pokud změníte konfiguračního souboru MOF žádným způsobem, musíte také znovu vytvořit kontrolní součet souboru.

### <a name="tooling"></a>Nástroje

Aby bylo možné tvoří nastavení, ověřování a správě serveru vyžádané replikace jednodušší, tyto nástroje jsou zahrnuty jako příklady v nejnovější verzi modulu xPSDesiredStateConfiguration:

1. Modul, který vám pomůže s balení moduly prostředků DSC a konfigurační soubory pro použití na serveru vyžádané replikace. [PublishModulesAndMofsToPullServer.psm1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PublishModulesAndMofsToPullServer.psm1). Následující příklady:

    ```powershell
        # Example 1 - Package all versions of given modules installed locally and MOF files are in c:\LocalDepot
         $moduleList = @('xWebAdministration', 'xPhp')
         Publish-DSCModuleAndMof -Source C:\LocalDepot -ModuleNameList $moduleList

         # Example 2 - Package modules and mof documents from c:\LocalDepot
         Publish-DSCModuleAndMof -Source C:\LocalDepot -Force
    ```

1. Skript, který se ověřuje serveru vyžádané replikace je správně nakonfigurován. [PullServerSetupTests.ps1](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/master/DSCPullServerSetup/PullServerDeploymentVerificationTest/PullServerSetupTests.ps1).

## <a name="community-solutions-for-pull-service"></a>Řešení komunity pro službu přijetí změn

Společenství DSC autorem více řešení, která implementují protokol služby o přijetí změn.
Pro místní prostředí nabízejí schopnosti služeb o přijetí změn a možnost zpětně přispívat ke komunitě přírůstková vylepšení.

- [Tug](https://github.com/powershellorg/tug)
- [DSC TRÆK](https://github.com/powershellorg/dsc-traek)

## <a name="pull-client-configuration"></a>Konfigurace klienta o přijetí změn

Toto téma popisuje nastavení klientů o přijetí změn podrobně:

- [Nastavení načítacího klienta DSC použití konfiguračních identifikátorů](pullClientConfigID.md)
- [Nastavení načítacího klienta DSC použití konfiguračních názvů](pullClientConfigNames.md)
- [Částečné konfigurace](partialConfigs.md)

## <a name="see-also"></a>Viz taky

- [Prostředí Windows PowerShell Desired State Configuration – přehled](overview.md)
- [Přijetí konfigurace](enactingConfigurations.md)
- [Použití serveru sestav DSC](reportServer.md)
- [[MS-DSCPM]: Desired State Configuration protokol modelu o přijetí změn](https://msdn.microsoft.com/library/dn393548.aspx)
- [[MS-DSCPM]: Desired State Configuration chyby protokolu modelu o přijetí změn](https://msdn.microsoft.com/library/mt612824.aspx)

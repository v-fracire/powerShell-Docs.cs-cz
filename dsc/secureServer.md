---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Osvědčené postupy serveru vyžádané replikace
ms.openlocfilehash: 04ad6940f443bc23d5e2347952b2d173aceac408
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893446"
---
# <a name="pull-server-best-practices"></a>Osvědčené postupy serveru vyžádané replikace

Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

> [!IMPORTANT]
> Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce. Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).

Shrnutí: Tento dokument je určený proces a rozšiřitelnost pomáhat techniků, kteří se připravuje pro řešení. Podrobnosti by měly poskytnout doporučené postupy jsme uvedli, zákazníky a poté ověřen produktovému týmu a zkontrolujte doporučení jsou budoucí přístupem a považovat za stabilní.

| |Informace o dokumentu|
|:---|:---|
Autor | Michael Greene
Recenzenti | Robert Gelens, Ravikanth Chaganti Aleksandar Nikolic
Publikování | Duben 2015

## <a name="abstract"></a>Abstraktní

Cílem tohoto dokumentu je poskytnout oficiální pokyny pro vývojáře plánující pro implementaci serveru pro vyžádání obsahu Windows PowerShell Desired State Configuration. Serveru vyžádané replikace je jednoduché služby, který zabere jenom pár minut nasadit. I když tento dokument nabídne technické příručkách s postupy, které lze použít v nasazení, hodnota tohoto dokumentu je jako reference pro osvědčené postupy a co zvážit před nasazením.
Čtenáři by měl mít základní znalost DSC a termíny používané k popisu komponenty, které jsou součástí nasazení DSC. Další informace najdete v tématu [Windows PowerShell Desired State Configuration přehled](/powershell/dsc/overview) tématu.
Rozvoj na cloudové tempo očekávaným DSC je základní technologie, včetně serveru vyžádané replikace také očekává se vyvíjí a zavádět nové funkce. Tento dokument obsahuje tabulku verzí v dodatku, která poskytuje odkazy na předchozích verzích a odkazy na budoucí vypadající řešení podporovat budoucnost návrhy.

Dvě hlavní části tohoto dokumentu:

- Plánování konfigurace
- Průvodce instalací

### <a name="versions-of-the-windows-management-framework"></a>Verze rozhraní Windows Management Framework

Informace v tomto dokumentu slouží platí pro Windows Management Framework 5.0. Zatímco WMF 5.0 není vyžadována pro nasazení a používání serveru vyžádané replikace, verze 5.0 je hlavním cílem tohoto dokumentu.

### <a name="windows-powershell-desired-state-configuration"></a>Prostředí Windows PowerShell Desired State Configuration

Desired State Configuration (DSC) je platforma pro správu, který umožňuje nasazení a správa konfiguračních dat pomocí syntaxe oboru s názvem formát MOF (Managed Object) pro popis Common Information Model (CIM). Opensourcový projekt, otevřete Management Infrastructure (OMI), existuje další rozvoj těchto standardů napříč platformami, včetně Linuxu a síťové hardwaru operační systémy. Další informace najdete v tématu [DMTF stránky propojení specifikací MOF](https://www.dmtf.org/standards/cim), a [OMI dokumenty a zdroj](https://collaboration.opengroup.org/omi/documents.php).

Prostředí Windows PowerShell poskytuje sadu jazyková rozšíření pro Desired State Configuration, můžete použít k vytvoření a správa deklarativních konfigurací.

### <a name="pull-server-role"></a>Role serveru o přijetí změn

Načítacího serveru poskytuje centralizované služby k uložení konfigurace, které budou přístupné pro cílové uzly.

Role serveru o přijetí změn můžete nasadit jako instance webového serveru nebo sdílené složky protokolu SMB. Funkce webového serveru zahrnuje rozhraní OData a může volitelně zahrnovat možnosti pro cílové uzly k hlášení zpět potvrzení úspěch nebo neúspěch jako konfigurace se použijí. Tato funkce je užitečná v prostředích, kdy existuje velký počet cílových uzlů.
Po dokončení konfigurace cílový uzel (také označované jako klient) tak, aby odkazoval na serveru vyžádané replikace nejnovější konfiguraci. jsou data a všechny požadované skripty stáhnout a použít. Může to jako jednorázová nasazení nebo znovu se vyskytující úlohy, která také umožňuje serveru vyžádané replikace prostředek důležité pro správu změn ve velkém měřítku. Další informace najdete v tématu [Windows PowerShell Desired State Configuration o přijetí změn servery](/powershell/dsc/pullServer) a

[Nabízená a vyžádaná režimů konfigurace](/powershell/dsc/pullServer).

## <a name="configuration-planning"></a>Plánování konfigurace

Pro každé nasazení softwaru enterprise je informace, které lze shromažďovat v předstihu vám pomohou při plánování pro správnou architekturu a abyste byli připraveni kroky potřebné k dokončení nasazení. Následující části obsahují informace o tom, jak připravit a organizační připojení, které pravděpodobně budete muset předem stát.

### <a name="software-requirements"></a>Požadavky na software

Nasazení serveru vyžádané replikace vyžaduje funkce DSC služby systému Windows Server. Tato funkce byla zavedena v systému Windows Server 2012 a byl aktualizován prostřednictvím probíhající vydání služby Windows Management Frameworku (WMF).

### <a name="software-downloads"></a>Stahování softwaru

Kromě instalace nejnovější obsah z webu Windows Update, jsou k dispozici dva soubory ke stažení považovat za osvědčený postup nasazení serveru vyžádané replikace DSC: nejnovější verzi Windows Management Framework a modulu DSC můžete automatizovat zřizování serveru o přijetí změn.

### <a name="wmf"></a>WMF

Windows Server 2012 R2 obsahuje funkci s názvem služby DSC. Funkce služby DSC poskytuje funkce serveru o přijetí změn, včetně binárních souborů, které podporují koncový bod OData.
WMF je součástí systému Windows Server a dojde k aktualizaci na agilní tempo mezi verzemi Windows serveru. [Nové verze WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=54616) mohou obsahovat aktualizace funkcí DSC služby. Z tohoto důvodu je osvědčeným postupem stažení nejnovější verze WMF a přečtěte si poznámky k určení, pokud tato verze obsahuje aktualizace funkcí služby DSC. Také byste měli revidovat část poznámky k verzi, která určuje, zda je stav návrhu pro aktualizaci nebo scénář uveden jako stabilní nebo experimentální.
Povolit pro agilní vývojového cyklu, jednotlivé funkce mohou být deklarovány stabilní, což znamená, funkce je připravená k použití v produkčním prostředí, dokonce i za běhu WMF vydání ve verzi preview.
Další funkce, které v minulosti byly aktualizovány podle verze WMF (viz poznámky k verzi WMF podrobnosti):

- Integrované skriptovací prostředí Windows PowerShell, Windows PowerShell
- Prostředí (ISE) Windows Powershellu webové služby (správu OData
- Rozšíření IIS pro službu) Windows Powershellu Desired State Configuration (DSC)
- Windows (WinRM) Vzdálená správa Windows Management Instrumentation (WMI)

### <a name="dsc-resource"></a>Prostředek DSC

Nasazení serveru o přijetí změn se dá zjednodušit tím, že zajistíte služby pomocí skriptu konfigurace DSC. Tento dokument obsahuje konfigurační skripty, které lze použít k nasazení uzlu produkční server připravený. Pokud chcete používat konfigurační skripty, DSC modul je potřeba, který je nejsou zahrnuty v systému Windows Server. Je název požadované modulu **xPSDesiredStateConfiguration**, což zahrnuje prostředků DSC **xDscWebService**. Je možné stáhnout modul xPSDesiredStateConfiguration [tady](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).

Použití `Install-Module` rutiny z **PowerShellGet** modulu.

```powershell
Install-Module xPSDesiredStateConfiguration
```

**PowerShellGet** modulu stáhne modul:

`C:\Program Files\Windows PowerShell\Modules`

Plánování úkolů|
---|
Máte přístup k souborům instalace pro Windows Server 2012 R2?|
Prostředí nasazení bude mít přístup k Internetu stáhnout WMF a modul z online galerie?|
Jak budou instalovat nejnovější aktualizace zabezpečení po instalaci operačního systému?|
Prostředí bude mít přístup k Internetu k získání aktualizací nebo bude mít na místním serveru Windows Server Update Services (WSUS)?|
Máte přístup k Windows serveru instalační soubory, které už zahrnují aktualizace prostřednictvím injektáže offline?|

### <a name="hardware-requirements"></a>Požadavky na hardware

Nasazení serveru vyžádané replikace se podporují na fyzických i virtuálních serverů. Požadavky na velikost pro vyžádání obsahu server souladu s požadavky na systém Windows Server 2012 R2.

: 1,4 GHz 64bitový procesor paměti: 512 MB místa na disku: 32 GB sítě: adaptér Gigabit Ethernet

Plánování úkolů|
---|
Budete nasazovat na fyzickém hardwaru nebo na virtualizační platformě?|
Jaký je proces požádat o nový server pro cílové prostředí?|
Co je průměrná doba vyřízení pro server k dispozici?|
Jaké velikosti serveru bude požadovat?|

### <a name="accounts"></a>Účty

Neexistují žádné požadavky na účet služby pro nasazení instance serveru o přijetí změn.
Existují ale scénáře, ve kterém webu může běžet v kontextu účtu místního uživatele.
Například pokud není potřeba přístup sdílené složky úložiště obsahu webu a Windows Server nebo zařízení, který je hostitelem sdílené úložiště nejsou připojené k doméně.

### <a name="dns-records"></a>Záznamy DNS

Budete potřebovat název serveru, který má použít při konfiguraci klientů pro práci s prostředím serveru o přijetí změn.
V testovacích prostředích obvykle se používá název hostitele serveru nebo IP adresa serveru je možné, pokud překlad názvů DNS není k dispozici.
V produkčním prostředí nebo v testovacím prostředí, která je určená pro produkční nasazení představují osvědčeným postupem je vytvořit záznam DNS CNAME.

Záznam CNAME DNS můžete vytvořit alias pro odkazování na hostitele (A) záznam.
Záměrem další název záznamu je zvýšit flexibilitu, třeba změny požadované v budoucnu.
Může pomoct záznam CNAME izolace konfigurace klienta tak, aby změny serverovým prostředím, jako je například nahrazení serveru vyžádané replikace nebo při přidávání serverů další o přijetí změn, nebude vyžadovat odpovídající změnu konfigurace klienta.

Pokud zvolíte, že název záznamu DNS, mějte architekturu řešení.
Pokud pomocí vyrovnávání zatížení, bude nutné mají stejný název jako záznam DNS certifikát používaný k zabezpečení přenosů přes protokol HTTPS.

Scénář |Osvědčený postup
:---|:---
Testovací prostředí |Pokud je to možné reprodukujte plánované produkčního prostředí. Název hostitele serveru je vhodný pro jednoduchá konfigurace. Pokud DNS není k dispozici, IP adresu lze namísto názvu hostitele.|
Nasazení s jedním uzlem |Vytvořte záznam DNS CNAME, který odkazuje na název hostitele serveru.|

Další informace najdete v tématu [konfigurace kruhové dotazování DNS ve Windows serveru](/previous-versions/windows/it-pro/windows-server-2003/cc787484(v=ws.10)).

Plánování úkolů|
---|
Víte, koho se obrátit na záznamy DNS vytvořit a změnit?|
Co je průměrná obrátkou pro požadavek na záznam DNS?|
Každý modul musí být zabaleny v určitém formátu souboru .zip s názvem ModuleName_Version.zip obsahující datové části modulu.|
Po zkopírování souboru na server, je nutné vytvořit kontrolní součet souboru.|
Pokud se klienti připojují k serveru, kontrolní součet se používá k ověření, že obsah modulu DSC se nezměnil, protože byla publikována. Pokud plánujete prostředí test nebo testovací prostředí, které scénáře jsou klíčem k ověření?|

### <a name="public-key-infrastructure"></a>Existují veřejně dostupných modulů, které obsahují prostředky vám pomůžou se vším, co potřebujete, nebo bude muset vytvořit vlastní prostředky?

Prostředí bude mít přístup k Internetu se načíst veřejný moduly?
Kdo bude zodpovídat za revize DSC moduly? Pokud plánujete do produkčního prostředí co budete používat jako místní úložiště pro ukládání DSC moduly?

Přijme centrální tým DSC moduly z aplikační týmy? Co bude procesu?

Plánování úkolů|
---|
Můžete automatizovat vytváření balíčků, kopírování a vytváření kontrolního součtu pro produkční prostředí DSC moduly na server z vašeho úložiště zdrojového kódu?|
Bude váš tým zodpovědného za správu platformu automatizace?|
Konfigurace DSC|
Účelem serveru vyžádané replikace je centralizovaná mechanismus pro distribuci konfigurací DSC na uzly klienta.|
Tyto konfigurace jsou uloženy na serveru jako MOF dokumenty.|
Každý dokument budou mít názvy jedinečný identifikátor GUID.|

### <a name="choosing-an-architecture"></a>Když jsou klienti nakonfigurováni pro připojení k serveru vyžádané replikace, jsou také uvedeny identifikátor GUID pro konfiguraci, kterou by měl žádat o.

Tento systém odkazuje na konfigurace podle identifikátoru GUID zaručuje jedinečnost globální a je flexibilní, takže konfiguraci lze použít s členitosti podle počtu uzlů, nebo jako konfiguraci role, která zahrnuje mnoho serverů, které by měly mít stejné konfigurace. Identifikátory GUID Plánování konfigurace GUID je vhodné další pozornost dala až po nasazení serveru o přijetí změn. Neexistuje žádný konkrétní požadavek, způsob zpracování identifikátory GUID a proces je pravděpodobně být jedinečný pro každé prostředí.
Proces může být v rozsahu od jednoduché složité: centrálně uloženého souboru CSV, jednoduché tabulky SQL, databáze CMDB nebo komplexní řešení, která vyžadují integraci s jiným řešením nástroj nebo softwaru.
Existují dvě obecné metody: Přiřazení identifikátory GUID na server – poskytuje míru záruky, že všechny konfigurace serveru je řízen jednotlivě.

#### <a name="load-balancing"></a>Vyrovnávání zatížení

To poskytuje úroveň přesnosti kolem aktualizace a může fungovat i v prostředí s několika servery. Přiřazení identifikátory GUID na roli serveru – všechny servery, které provádí stejnou funkci, jako jsou třeba webové servery, použijte stejný identifikátor GUID odkazovat na požadované konfigurační data.

Plánování úkolů|
---|
Mějte na paměti, že pokud mnoho serverů sdílejí stejný identifikátor GUID, všechny z nich se aktualizují najednou při změně konfigurace.|
Identifikátor GUID je něco, co by měl být citlivá data vzhledem k tomu, že může využít uživatel s úmyslem získat informace o tom, jak jsou servery nasazené a nakonfigurovaných ve vašem prostředí.|
Další informace najdete v tématu bezpečně přidělování identifikátorů GUID v prostředí PowerShell Desired State Configuration o přijetí změn režimu.|
Kdo bude zodpovídat za konfigurací v kopírování do složky na serveru o přijetí změn, jakmile jsou připravené?|
Pokud konfigurace vytvořené týmem aplikace, co proces bude je předat?|
Bude využívat úložiště k ukládání konfigurace podle jejich probíhá čtení zleva doprava, napříč týmy?|
Můžete automatizovat proces kopírování konfigurace do serveru a vytváření kontrolní součet, jakmile jsou připravené?|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a>Jak se namapujete identifikátory GUID na servery nebo role a kdy to se uloží?

Co budete používat jako proces ke konfiguraci klientských počítačů a jak ji integrovat s vaším procesem pro vytváření a ukládání konfigurace identifikátory GUID? Skripty, které jsou uvedené v tomto dokumentu jsou stabilní příklady.

Vždy zkontrolujte pečlivě skripty před spuštěním v produkčním prostředí.  Chcete-li ověřit verzi prostředí PowerShell na vašem serveru použijte následující příkaz.

#### <a name="dsc-modules"></a>Pokud je to možné upgradujte na nejnovější verzi Windows Management Framework.

Dále si stáhněte  modul pomocí následujícího příkazu. Příkaz vyzve ke schválení před stažením modulu. Instalace a konfigurace skriptů

Nejlepší metodou k nasazení serveru vyžádané replikace DSC je použití skriptu konfigurace DSC. Tento dokument zobrazíte skripty, včetně obě základní nastavení, které by konfigurovat jenom webovou službu DSC a upřesňující nastavení, která by konfigurovat Windows Server začátku do konce včetně DSC webové služby. Poznámka: Aktuálně  DSC modul vyžaduje serveru, aby se národního prostředí EN-US.

Základní konfigurace pro Windows Server 2012 Upřesňující konfigurace pro Windows Server 2012 R2 Ověřte funkčnost serveru o přijetí změn

```powershell
New-DscChecksum -ConfigurationPath .\ -OutPath .\
```

Plánování úkolů|
---|
Konfigurace klientů|
Další odkazy na fragmenty kódu a příklady|
Tento příklad ukazuje, jak ručně zahájit připojení klienta (vyžaduje WMF5) pro účely testování.|
Přidat DnsServerResourceRecordName rutina se používá k přidání typ záznamu CNAME do zóny DNS.|
Funkce, prostředí PowerShell vytvoření kontrolního součtu a publikovat MOF DSC na serveru vyžádané replikace SMB automaticky vytvoří požadované kontrolního součtu a pak zkopíruje MOF konfigurace i soubory kontrolního součtu serveru vyžádané replikace SMB.|
Příloha – Principy ODATA typy dat služby souborů Datový soubor je uložen vytvořit informace během nasazování serveru vyžádané replikace, který obsahuje webovou službu OData.|
Typ souboru závisí na operačním systému, jak je popsáno níže.|
Windows Server 2012 typ souboru bude vždy .mdb|

#### <a name="dsc-configurations"></a>Windows Server 2012 R2 typ souboru se ve výchozím nastavení .edb v konfiguraci je uvedeno .mdb

V Advanced ukázkový skript pro instalaci serveru vyžádaných replikací s také najdete příklad toho, jak automaticky řídit nastavení souboru web.config, aby se zabránilo pravděpodobné, že chyba způsobená podle typu souboru. Tyto konfigurace jsou uloženy na serveru jako MOF dokumenty.
Každý dokument budou mít názvy jedinečný identifikátor GUID. Když jsou klienti nakonfigurováni pro připojení k serveru vyžádané replikace, jsou také uvedeny identifikátor GUID pro konfiguraci, kterou by měl žádat o. Tento systém odkazuje na konfigurace podle identifikátoru GUID zaručuje jedinečnost globální a je flexibilní, takže konfiguraci lze použít s členitosti podle počtu uzlů, nebo jako konfiguraci role, která zahrnuje mnoho serverů, které by měly mít stejné konfigurace.

#### <a name="guids"></a>Identifikátory GUID

Plánování konfigurace GUID je vhodné další pozornost dala až po nasazení serveru o přijetí změn. Neexistuje žádný konkrétní požadavek, způsob zpracování identifikátory GUID a proces je pravděpodobně být jedinečný pro každé prostředí. Proces může být v rozsahu od jednoduché složité: centrálně uloženého souboru CSV, jednoduché tabulky SQL, databáze CMDB nebo komplexní řešení, která vyžadují integraci s jiným řešením nástroj nebo softwaru. Existují dvě obecné metody:

- **Přiřazení identifikátory GUID na server** – poskytuje míru záruky, že všechny konfigurace serveru je řízen jednotlivě. To poskytuje úroveň přesnosti kolem aktualizace a může fungovat i v prostředí s několika servery.
- **Přiřazení identifikátory GUID na roli serveru** – všechny servery, které provádí stejnou funkci, jako jsou třeba webové servery, použijte stejný identifikátor GUID odkazovat na požadované konfigurační data.  Mějte na paměti, že pokud mnoho serverů sdílejí stejný identifikátor GUID, všechny z nich se aktualizují najednou při změně konfigurace.

  Identifikátor GUID je něco, co by měl být citlivá data vzhledem k tomu, že může využít uživatel s úmyslem získat informace o tom, jak jsou servery nasazené a nakonfigurovaných ve vašem prostředí. Další informace najdete v tématu [bezpečně přidělování identifikátorů GUID v prostředí PowerShell Desired State Configuration o přijetí změn režimu](https://blogs.msdn.microsoft.com/powershell/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode/).

Plánování úkolů|
---|
Kdo bude zodpovídat za konfigurací v kopírování do složky na serveru o přijetí změn, jakmile jsou připravené?|
Pokud konfigurace vytvořené týmem aplikace, co proces bude je předat?|
Bude využívat úložiště k ukládání konfigurace podle jejich probíhá čtení zleva doprava, napříč týmy?|
Můžete automatizovat proces kopírování konfigurace do serveru a vytváření kontrolní součet, jakmile jsou připravené?|
Jak se namapujete identifikátory GUID na servery nebo role a kdy to se uloží?|
Co budete používat jako proces ke konfiguraci klientských počítačů a jak ji integrovat s vaším procesem pro vytváření a ukládání konfigurace identifikátory GUID?|

## <a name="installation-guide"></a>Průvodce instalací

*Skripty, které jsou uvedené v tomto dokumentu jsou stabilní příklady. Vždy zkontrolujte pečlivě skripty před spuštěním v produkčním prostředí.*

### <a name="prerequisites"></a>Předpoklady

Chcete-li ověřit verzi prostředí PowerShell na vašem serveru použijte následující příkaz.

```powershell
$PSVersionTable.PSVersion
```

Pokud je to možné upgradujte na nejnovější verzi Windows Management Framework.
Dále si stáhněte `xPsDesiredStateConfiguration` modul pomocí následujícího příkazu.

```powershell
Install-Module xPSDesiredStateConfiguration
```

Příkaz vyzve ke schválení před stažením modulu.

### <a name="installation-and-configuration-scripts"></a>Instalace a konfigurace skriptů

Nejlepší metodou k nasazení serveru vyžádané replikace DSC je použití skriptu konfigurace DSC. Tento dokument zobrazíte skripty, včetně obě základní nastavení, které by konfigurovat jenom webovou službu DSC a upřesňující nastavení, která by konfigurovat Windows Server začátku do konce včetně DSC webové služby.

Poznámka: Aktuálně `xPSDesiredStateConfiguation` DSC modul vyžaduje serveru, aby se národního prostředí EN-US.

### <a name="basic-configuration-for-windows-server-2012"></a>Základní konfigurace pro Windows Server 2012

```powershell
# This is a very basic Configuration to deploy a pull server instance in a lab environment on Windows Server 2012.

Configuration PullServer {
Import-DscResource -ModuleName xPSDesiredStateConfiguration

        # Load the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
          Ensure = 'Present'
          Name = 'DSC-Service'
        }

        # Use the DSC Resource to simplify deployment of the web service
        xDSCWebService PSDSCPullServer
        {
          Ensure = 'Present'
          EndpointName = 'PSDSCPullServer'
          Port = 8080
          PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
          CertificateThumbPrint = 'AllowUnencryptedTraffic'
          ModulePath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
          ConfigurationPath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
          State = 'Started'
          DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
}
PullServer -OutputPath 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'
```

### <a name="advanced-configuration-for-windows-server-2012-r2"></a>Upřesňující konfigurace pro Windows Server 2012 R2

```powershell
# This is an advanced Configuration example for Pull Server production deployments on Windows Server 2012 R2.
# Many of the features demonstrated are optional and provided to demonstrate how to adapt the Configuration for multiple scenarios
# Select the needed resources based on the requirements for each environment.
# Optional scenarios include:
#      * Reduce footprint to Server Core
#      * Rename server and join domain
#      * Switch from SSL to TLS for HTTPS
#      * Automatically load certificate from Certificate Authority
#      * Locate Modules and Configuration data on remote SMB share
#      * Manage state of default websites in IIS

param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [System.String] $ServerName,
        [System.String] $DomainName,
        [System.String] $CARootName,
        [System.String] $CAServerFQDN,
        [System.String] $CertSubject,
        [System.String] $SMBShare,
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $Credential
    )

Configuration PullServer {
    Import-DscResource -ModuleName xPSDesiredStateConfiguration, xWebAdministration, xCertificate, xComputerManagement
    Node localhost
    {

        # Configure the server to automatically corret configuration drift including reboots if needed.
        LocalConfigurationManager
        {
            ConfigurationMode = 'ApplyAndAutoCorrect'
            RebootNodeifNeeded = $node.RebootNodeifNeeded
            CertificateId = $node.Thumbprint
        }

        # Remove all GUI interfaces so the server has minimum running footprint.
        WindowsFeature ServerCore
        {
            Ensure = 'Absent'
            Name = 'User-Interfaces-Infra'
        }

        # Set the server name and if needed, join a domain. If not joining a domain, remove the DomainName parameter.
        xComputer DomainJoin
        {
            Name = $Node.ServerName
            DomainName = $Node.DomainName
            Credential = $Node.Credential
        }

        # The next series of settings disable SSL and enable TLS, for environments where that is required by policy.
        Registry TLS1_2ServerEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }

        Registry TLS1_2ServerDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }

        Registry TLS1_2ClientEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }

        Registry TLS1_2ClientDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }

        Registry SSL2ServerDisabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server'
            ValueName = 'Enabled'
            ValueData = 0
            ValueType = 'Dword'
        }

        # Install the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
            Ensure = 'Present'
            Name = 'DSC-Service'
        }

        # If using a certificate from a local Active Directory Enterprise Root Certificate Authority, complete a request and install the certificate
        xCertReq SSLCert
        {
            CARootName = $Node.CARootName
            CAServerFQDN = $Node.CAServerFQDN
            Subject = $Node.CertSubject
            AutoRenew = $Node.AutoRenew
            Credential = $Node.Credential
        }

        # Use the DSC resource to simplify deployment of the web service.  You might also consider modifying the default port, possibly leveraging port 443 in environments where that is enforced as a standard.
        xDSCWebService PSDSCPullServer
        {
            Ensure = 'Present'
            EndpointName = 'PSDSCPullServer'
            Port = 8080
            PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
            CertificateThumbPrint = 'CertificateSubject'
            CertificateSubject = $Node.CertSubject
            ModulePath = "$($Node.SMBShare)\DscService\Modules"
            ConfigurationPath = "$($Node.SMBShare)\DscService\Configuration"
            State = 'Started'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }

        # Validate web config file contains current DB settings
        xWebConfigKeyValue CorrectDBProvider
        {
            ConfigSection = 'AppSettings'
            Key = 'dbprovider'
            Value = 'System.Data.OleDb'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }
        xWebConfigKeyValue CorrectDBConnectionStr
        {
            ConfigSection = 'AppSettings'
            Key = 'dbconnectionstr'
            Value = 'Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Program Files\WindowsPowerShell\DscService\Devices.mdb;'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }

        # Stop the default website
        xWebsite StopDefaultSite
        {
            Ensure = 'Present'
            Name = 'Default Web Site'
            State = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            ServerName = $ServerName
            DomainName = $DomainName
            CARootName = $CARootName
            CAServerFQDN = $CAServerFQDN
            CertSubject = $CertSubject
            AutoRenew = $true
            SMBShare = $SMBShare
            Credential = $Credential
            RebootNodeifNeeded = $true
            CertificateFile = 'c:\PullServerConfig\Cert.cer'
            Thumbprint = 'B9A39921918B466EB1ADF2509E00F5DECB2EFDA9'
            }
        )
    }

PullServer -ConfigurationData $configData -OutputPath 'C:\PullServerConfig\'
Set-DscLocalConfigurationManager -ComputerName localhost -Path 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'

# .\Script.ps1 -ServerName web1 -domainname 'test.pha' -carootname 'test-dc01-ca' -caserverfqdn 'dc01.test.pha' -certsubject 'CN=service.test.pha' -smbshare '\\sofs1.test.pha\share'
```

### <a name="verify-pull-server-functionality"></a>Ověřte funkčnost serveru o přijetí změn

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](Invoke-WebRequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}

Verify-DSCPullServer 'INSERT SERVER FQDN'
```

```output
Expected Result:
Action
Module
StatusReport
Node
```

### <a name="configure-clients"></a>Konfigurace klientů

```powershell
Configuration PullClient {
    param(
    $ID,
    $Server
    )
        LocalConfigurationManager
                {
                    ConfigurationID = $ID;
                    RefreshMode = 'PULL';
                    DownloadManagerName = 'WebDownloadManager';
                    RebootNodeIfNeeded = $true;
                    RefreshFrequencyMins = 30;
                    ConfigurationModeFrequencyMins = 15;
                    ConfigurationMode = 'ApplyAndAutoCorrect';
                    DownloadManagerCustomData = @{ServerUrl = "http://"+$Server+":8080/PSDSCPullServer.svc"; AllowUnsecureConnection = $true}
                }
}

PullClient -ID 'INSERTGUID' -Server 'INSERTSERVER' -Output 'C:\DSCConfig\'
Set-DscLocalConfigurationManager -ComputerName 'Localhost' -Path 'C:\DSCConfig\' -Verbose
```

## <a name="additional-references-snippets-and-examples"></a>Další odkazy na fragmenty kódu a příklady

Tento příklad ukazuje, jak ručně zahájit připojení klienta (vyžaduje WMF5) pro účely testování.

```powershell
Update-DscConfiguration –Wait -Verbose
```

[Přidat DnsServerResourceRecordName](http://bit.ly/1G1H31L) rutina se používá k přidání typ záznamu CNAME do zóny DNS.

Funkce, prostředí PowerShell [vytvoření kontrolního součtu a publikovat MOF DSC na serveru vyžádané replikace SMB](https://gallery.technet.microsoft.com/scriptcenter/PowerShell-Function-to-3bc4b7f0) automaticky vytvoří požadované kontrolního součtu a pak zkopíruje MOF konfigurace i soubory kontrolního součtu serveru vyžádané replikace SMB.

## <a name="appendix---understanding-odata-service-data-file-types"></a>Příloha – Principy ODATA typy dat služby souborů

Datový soubor je uložen vytvořit informace během nasazování serveru vyžádané replikace, který obsahuje webovou službu OData. Typ souboru závisí na operačním systému, jak je popsáno níže.

- **Windows Server 2012** typ souboru bude vždy .mdb
- **Windows Server 2012 R2** typ souboru se ve výchozím nastavení .edb v konfiguraci je uvedeno .mdb

V [Advanced ukázkový skript](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) pro instalaci serveru vyžádaných replikací s také najdete příklad toho, jak automaticky řídit nastavení souboru web.config, aby se zabránilo pravděpodobné, že chyba způsobená podle typu souboru.
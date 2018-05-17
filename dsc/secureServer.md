---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Osvědčené postupy serveru vyžádané replikace
ms.openlocfilehash: 1efc016df6882fa962f59dfd3e53eaa6d6b0c121
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="pull-server-best-practices"></a>Osvědčené postupy serveru vyžádané replikace

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

> [!IMPORTANT]
> Server pro vyžádání obsahu (funkce systému Windows *DSC služby*) je podporované součásti systému Windows Server jsou však nejsou žádné plány, které nabízí nové funkce nebo funkce. Doporučujeme začít Přechod spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace s v systému Windows Server) nebo jedno z řešení komunity uvedené [zde](pullserver.md#community-solutions-for-pull-service).

Souhrn: Tento dokument je určený zahrnuje proces a rozšiřitelnost pomůže technici, kteří jsou Příprava řešení. Podrobnosti by měl poskytovat osvědčené postupy, jak identifikovaný zákazníků a potom ověřit produktový tým zajistit doporučení jsou budoucí přístupem a považovat za stabilní.

| |Informace o dokumentu|
|:---|:---|
Autor | Michael Greene
Recenzenti | Ben Gelens, Ravikanth Chaganti Aleksandar Nikolic
Publikovat | Duben 2015

## <a name="abstract"></a>Abstraktní

Tento dokument určená k poskytování oficiální pokyny pro každý, kdo plánování implementaci serveru pro vyžádání obsahu konfigurace požadovaného stavu aplikace Windows PowerShell. Vyžádání obsahu server je jednoduchý služba, která by měla trvat jenom k nasazení. I když tento dokument nabídne technické postupy pokyny, které je možné v nasazení, hodnota tohoto dokumentu je referenční osvědčené postupy a co mají vezměte v úvahu před nasazením.
Čtečky by měl mít základní znalost DSC a termínů používaných k popisu komponenty, které jsou zahrnuté v nasazení DSC. Další informace najdete v tématu [Přehled konfigurace prostředí Windows PowerShell požadovaného stavu](https://technet.microsoft.com/library/dn249912.aspx) tématu.
Očekávaným DSC vyvíjí v cloudu cadence základní technologii, včetně serveru vyžádané replikace se také očekává vyvíjí a zavádět nové funkce. Tento dokument obsahuje tabulku verze v příloze, která poskytuje odkazy na předchozí verze a odkazy na budoucí vypadající řešení podporovat budoucnost návrhů.

Dvě hlavní části tohoto dokumentu:

 - Plánování konfigurace
 - Průvodce instalací

### <a name="versions-of-the-windows-management-framework"></a>Verze Windows Management Framework
Informace v tomto dokumentu je určena pro použití na Windows Management Framework 5.0. Přestože WMF 5.0 není vyžadována pro nasazení a provozování vyžádání obsahu server, verze 5.0 je téma tohoto dokumentu.

### <a name="windows-powershell-desired-state-configuration"></a>Prostředí Windows PowerShell konfigurace požadovaného stavu
Požadované konfigurace stavu (DSC) je platformu správy, která umožňuje nasazení a správa konfiguračních dat pomocí syntaxe odvětví s názvem formát MOF (Managed Object) k popisu modelu CIM (Common Information). Opensourcový projekt, otevřete Management Infrastructure (OMI), existuje další vývoj těchto standardů napříč platformami, včetně Linux a síťové hardwaru operační systémy. Další informace najdete v tématu [DMTF stránky propojení s MOF specifikace](http://dmtf.org/standards/cim), a [OMI dokumenty a zdroj](https://collaboration.opengroup.org/omi/documents.php).

Prostředí Windows PowerShell poskytuje sadu jazyková rozšíření pro konfigurace požadovaného stavu, můžete použít k vytváření a správě deklarativní konfigurace.

### <a name="pull-server-role"></a>Role serveru vyžádané replikace
Načítacího serveru poskytuje centralizované služby k uložení konfigurace, které budou přístupné pro cílové uzly.

Role serveru vyžádané replikace se dá nasadit jako instance webového serveru nebo sdílené složky SMB. Schopnost webového serveru obsahuje rozhraní OData a může volitelně obsahovat možnosti pro cílové uzly k hlášení zpět potvrzení úspěšné nebo neúspěšné, jako jsou použita konfigurace. Tato funkce je užitečná v prostředích, kde je velké množství cílové uzly.
Po dokončení konfigurace cílový uzel (také označované jako klient) tak, aby odkazoval na server vyžádané replikace s nejnovější konfigurací jsou data a všechny požadované skripty stažení a použití. Tato situace může nastat, jako jednorázové nasazení nebo jako znovu se vyskytující úlohy, který také umožňuje serveru vyžádané replikace prostředek důležité pro správu změn ve velkém měřítku. Další informace najdete v tématu [Windows PowerShell požadovaného stavu konfigurace pro vyžádání obsahu servery](https://technet.microsoft.com/library/dn249913.aspx) a [nabízení a režimů pro vyžádání obsahu konfigurace](https://technet.microsoft.com/library/dn249913.aspx).

## <a name="configuration-planning"></a>Plánování konfigurace

Pro všechna nasazení softwaru enterprise je informace, které může být shromážděny předem vám pomohou při plánování pro správnou architekturu a abyste byli připraveni kroky potřebné k dokončení nasazení. Následující části obsahují informace o tom, jak připravit a organizační připojení, která bude pravděpodobně potřeba předem dojít.

### <a name="software-requirements"></a>Požadavky na software

Nasazení serveru pro vyžádání obsahu vyžaduje funkci DSC služby systému Windows Server. Tato funkce byla zavedená v systému Windows Server 2012 a byl aktualizován prostřednictvím probíhající verzích Windows Management Framework (WMF).

### <a name="software-downloads"></a>Stahování softwaru

Kromě instalace nejnovější obsah ze služby Windows Update, jsou považovány za osvědčený postup nasadit server DSC za dvě stahování: nejnovější verzi Windows Management Framework a modul DSC pro automatizaci vyžádání obsahu server zřizování.

### <a name="wmf"></a>WMF

Windows Server 2012 R2 obsahuje funkci s názvem služby DSC. Funkce služby DSC poskytuje funkce serveru vyžádané replikace, včetně binárních souborů, které podporují koncový bod OData.
WMF je součástí systému Windows Server a je aktualizován na agilní cadence mezi verzemi Windows serveru. [Nové verze WMF 5.0](http://aka.ms/wmf5latest) můžete zahrnout aktualizace do funkce služby DSC. Z tohoto důvodu je osvědčeným postupem stažení nejnovější verze WMF a přečtěte si poznámky k verzi k určení, pokud tato verze obsahuje aktualizaci funkce služby DSC. Měli byste taky zkontrolovat v části poznámky k verzi, která určuje, zda je stav návrhu pro aktualizaci nebo scénář v stabilní nebo experimentální.
Povolit pro agilní verze cyklus, jednotlivých funkcí lze deklarovat stabilní, což naznačuje funkci je připravený k použití v produkčním prostředí i podpora produktu WMF vydání ve verzi preview.
Další funkce, které byly v minulosti aktualizovány podle verze WMF (viz poznámky k verzi WMF další podrobnosti):

 - Integrované skriptovací prostředí Windows PowerShell Windows PowerShell
 - Prostředí (ISE) v prostředí Windows PowerShell webové služby (správu OData
 - Rozšíření IIS) prostředí Windows PowerShell konfigurace požadovaného stavu (DSC)
 - Windows (WinRM) Vzdálená správa Windows Management Instrumentation (WMI)

### <a name="dsc-resource"></a>Prostředek DSC

Nasazení na server vyžádané replikace můžete zjednodušit tím zřizováním služby pomocí skriptu konfigurace DSC. Tento dokument obsahuje konfigurační skripty, které slouží k nasazení uzlem produkční připravené serveru. Použít konfigurační skripty, DSC modul je potřeba který není součástí systému Windows Server. Název požadované modulu je **xPSDesiredStateConfiguration**, což zahrnuje prostředek DSC **xDscWebService**. Modul xPSDesiredStateConfiguration si můžete stáhnout [zde](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).

Použití **instalace modulu** rutiny z **PowerShellGet** modulu.

```powershell
Install-Module xPSDesiredStateConfiguration
```

**PowerShellGet** modulu stáhne modulu:

`C:\Program Files\Windows PowerShell\Modules`

Plánování úkolů|
---|
Máte přístup k instalačním souborům pro Windows Server 2012 R2?|
Prostředí nasazení budou mít přístup k Internetu stahovat WMF a modul z online galerie?|
Jak budou instalovat nejnovější aktualizace zabezpečení po instalaci operačního systému?|
Prostředí bude mít přístup k Internetu k získání aktualizací, nebo bude mít na místním serveru Windows Server Update Services (WSUS)?|
Máte přístup k systému Windows Server instalační soubory, které již obsahují aktualizace prostřednictvím offline vkládání?|

### <a name="hardware-requirements"></a>Požadavky na hardware

Nasazení serveru vyžádané replikace jsou podporovány na fyzické i virtuální servery. Požadavky na nastavení velikosti pro vyžádání obsahu server zarovnané s požadavky na Windows Server 2012 R2.

Využití procesoru: 1, 4 GHz 64bitový procesor paměti: 512 MB místa na disku: 32 GB sítě: adaptér Gigabit Ethernet

Plánování úkolů|
---|
Budete nasazovat na fyzickém hardwaru nebo na virtualizační platformě?|
Co je proces požádat o nový server pro cílové prostředí?|
Co je průměrná doba vyřízení pro server k dispozici?|
Jaké velikost serveru bude požadovat?|

### <a name="accounts"></a>Účty

Nejsou žádné požadavky na účet služby pro nasazení do instance serveru vyžádané replikace.
Existují však scénáře, kde může web spustit v kontextu místního uživatelského účtu.
Například pokud je potřeba přístup sdílené složky úložiště pro obsah webu a Windows Server nebo zařízení hostování sdílenou složku úložiště nejsou připojené k doméně.

### <a name="dns-records"></a>Záznamy DNS

Budete potřebovat název serveru, který má použít při konfiguraci klientů pro práci s prostředím serveru vyžádané replikace.
V testovacích prostředích obvykle se používá název hostitele serveru nebo adresu IP serveru lze použít, pokud překlad názvu DNS není k dispozici.
V produkčních prostředích nebo v testovacím prostředí, který reprezentuje produkční nasazení osvědčeným postupem je vytvořit záznam DNS CNAME.

Záznam CNAME DNS umožňuje vytvořit alias, který bude odkazovat na váš hostitel (A) záznam.
Další název záznamu je cílem zvyšování flexibility, třeba změnu vyžadovat v budoucnu.
Záznam CNAME pomůžou izolovat konfigurace klienta tak, aby změny prostředí serveru, jako je výměna načítacího serveru nebo přidání dalších vyžádání serverů, nebude vyžadovat odpovídající změny do konfigurace klienta.

Když vyberete název záznamu DNS, uvědomte si architektury řešení.
Pokud pomocí vyrovnávání zatížení, bude nutné sdílet stejný název jako záznam DNS certifikát použitý k zabezpečení přenosů přes protokol HTTPS.

Scénář |Osvědčený postup
:---|:---
Testovací prostředí |Reprodukujte plánované provozní prostředí, pokud je to možné. Název hostitele serveru je vhodná pro jednoduché konfigurace. Pokud DNS není k dispozici, může místo název hostitele použít IP adresu.|
Nasazení jednoho uzlu |Vytvořte záznam DNS CNAME, který odkazuje na název hostitele serveru.|

Další informace najdete v tématu [konfigurování kruhové dotazování DNS v systému Windows Server](https://technet.microsoft.com/en-us/library/cc787484(v=ws.10).aspx).

Plánování úkolů|
---|
Víte, kdo má záznamy DNS vytvořené a změněné kontaktovat?|
Jaká je průměrná vyřízení pro žádost o záznam DNS?|
Je třeba požádat o statické záznamy hostitele (A) pro servery?|
Co se vám požadavku jako záznam CNAME?|
V případě potřeby, jaký typ Vyrovnávání zatížení řešení bude využíváte? (viz část s názvem Vyrovnávání zatížení podrobnosti)|

### <a name="public-key-infrastructure"></a>Infrastruktura veřejných klíčů

Většina organizací dnes vyžadují, aby síťový provoz, zejména provoz, který zahrnuje takové citlivá data, jak jsou servery konfigurované, musí být ověřen nebo během přenosu šifrována.
Když je možné nasadit vyžádání obsahu server pomocí protokolu HTTP, což usnadňuje požadavky klientů v prostý text, je osvědčeným postupem zabezpečení provozu pomocí protokolu HTTPS. Službu lze nakonfigurovat k využívání HTTPS pomocí sady parametrů v prostředek DSC **xPSDesiredStateConfiguration**.

Požadavky na certifikát k zabezpečení přenosů HTTPS pro vyžádání obsahu server nejsou jiné než zabezpečení jakékoli jiný webový server HTTPS. **Webový Server** šablonu služby Windows Server certifikátů splňuje požadované možnosti.

Plánování úkolů|
---|
Pokud nejsou automatizované žádosti o certifikát, který budete potřebovat obraťte se na požadavky na certifikát?|
Jaká je průměrná vyřízení žádosti?|
Jak bude na vás přenést soubor certifikátu?|
Jak se vám převede privátní klíč certifikátu?|
Jak dlouho je výchozí doba vypršení platnosti?|
Mít vyrovnané na název DNS pro prostředí serveru vyžádání obsahu, který můžete použít pro název certifikátu?|

### <a name="choosing-an-architecture"></a>Výběr architekturu

Vyžádání obsahu server se dá nasadit pomocí služby web hostované na IIS nebo sdílenou složku SMB. Ve většině případů bude možnosti webové služby poskytují větší flexibilitu. Není komunikaci přes protokol HTTPS napříč síťovými hranicemi, zatímco přenosy SMB je často filtrované blokované nebo mezi sítěmi. Webová služba také nabízí možnost zahrnout Server shoda nebo Reporting správce webu (i témata vzít v úvahu v budoucí verzi tohoto dokumentu), poskytují mechanismus pro klienty odesílat zprávy o stavu zpět na server pro centralizované viditelnosti.
SMB nabízí možnost v prostředích, kde zásady stanoví, že webový server by neměl být využité a další požadavky prostředí, které role Webový server nežádoucí.
V obou případech musíte vyhodnotit požadavky na podepisování a šifrování komunikace. Protokol HTTPS, podepisování SMB a zásady protokolu IPSEC jsou všechny možnosti vhodné zvažování.

#### <a name="load-balancing"></a>Vyrovnávání zatížení
Klienti interakci s webovou službou může požádat o informace, které je vrácený v odpověď o jedné. Žádné sekvenční požadavky jsou povinné, takže není nutné pro platformu, která Ujistěte se, že relace udržované na jednom serveru v libovolném bodě v čase Vyrovnávání zatížení.

Plánování úkolů|
---|
Jaká řešení se použije pro vyrovnávání zatížení provozu napříč servery?|
Pokud se používá Vyrovnávání zatížení hardwaru, který bude trvat žádost o přidání novou konfiguraci zařízení?|
Co je průměrná vyřízení požadavku konfigurace nového zatížení vyrovnáváním webovou službu?|
Jaké informace budou potřeba pro požadavek?|
Budete potřebovat k vyžádání dalších IP adresy nebo týmem zodpovědný za vyrovnávání zatížení zpracovává který?|
Máte k dispozici záznamy DNS, které jsou potřebné a bude to vyžadovat tým zodpovědná za konfiguraci řešení vyrovnávání zatížení?|
Řešení vyrovnávání zatížení vyžaduje, aby zařízení zpracovávat infrastruktury veřejných KLÍČŮ nebo můžete ho Vyrovnávání zatížení, které přenosy HTTPS, dokud nejsou žádné požadavky relace?|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a>Konfigurace pracovní a modulů na tomto serveru

Jako součást plánování konfigurace musíte se zamyslet, o které DSC se bude hostovat modulů a konfigurací serverem pro vyžádání obsahu. Pro účely plánování konfigurace je důležité mít základní znalosti o tom, jak připravit a nasadit obsah na server vyžádané replikace.

V budoucnu v této části se rozšířit a zahrnuty v provozní příručce pro serveru vyžádané replikace s DSC.  V Průvodci zabývat den proces pro správu modulů a konfigurací v čase s automatizace.

#### <a name="dsc-modules"></a>Moduly DSC
Klienty, kteří požadují konfiguraci bude nutné požadované moduly DSC. Funkce serveru pro vyžádání obsahu je automatizovat distribuci na vyžádání DSC moduly klientům. Pokud nasadíte načítacího serveru poprvé, třeba jako testovacího prostředí nebo testování konceptu, pravděpodobně chcete závisí na DSC moduly, které jsou dostupné z veřejných úložišť, jako je například Galerie prostředí PowerShell nebo úložišť PowerShell.org GitHub pro moduly DSC .

Je důležité si pamatovat, že i pro důvěryhodné online zdrojů, jako je například Galerie prostředí PowerShell, libovolný modul, který byl stažen z veřejného úložiště by měl být zkontrolovány uživatelem někdo pomocí prostředí PowerShell a znalosti o prostředí, kde budou moduly použít před používá v produkčním prostředí. Při dokončení této úlohy je vhodná doba zkontrolujte všechny další datové části v modulu, který lze odebrat například dokumentaci a ukázkové skripty. Tím se sníží šířku pásma sítě pro každého klienta v jejich první žádost, když moduly budou staženy přes síť ze serveru do klienta.

Každý modul musí být zabalené v konkrétním formátu ZIP soubor s názvem ModuleName_Version.zip, který obsahuje datové části modulu. Po zkopírování souboru na server musí být vytvořeny soubor kontrolního součtu. Pokud se klienti připojují k serveru, kontrolního součtu se používá k ověření, že obsah DSC modul nebylo změněno, protože byla publikována.

```powershell
New-DscCheckSum -ConfigurationPath .\ -OutPath .\
```

Plánování úkolů|
---|
Pokud plánujete testu nebo testovacím prostředí, které scénáře jsou klíčem k ověření?|
Jsou veřejně dostupné moduly, které obsahují prostředky tak, aby pokrývalo vše, co potřebujete, nebo budete potřebovat vytvořit vaše vlastní prostředky?|
Prostředí, budou mít přístup k Internetu k načtení veřejné moduly?|
Kdo je zodpovědná za kontrola DSC moduly?|
Pokud plánujete provozním prostředí co použijete jako místní úložiště pro ukládání DSC moduly?|
Přijme centrální tým moduly DSC z týmy aplikací? Co bude tento proces?|
Je balení, kopírování a vytváření kontrolních součtů pro produkční prostředí DSC moduly na server z vaší zdrojové úložiště bude automatizovat?|
Bude váš tým zodpovědní za správu platformou automatizace?|

#### <a name="dsc-configurations"></a>Konfigurace DSC

Účelem serveru pro vyžádání obsahu je zajistit centralizovanou mechanismus pro distribuci konfigurací DSC uzlů klientů. Konfigurace jsou uloženy na serveru jako MOF dokumenty.
Každý dokument budou mít názvy jedinečný identifikátor GUID. Pokud jsou klienti nakonfigurovaní pro připojení k serveru vyžádané replikace, jsou také uvedeny identifikátor GUID pro konfiguraci, kterou by měl žádat o. Tento systém odkazující na konfigurace pomocí identifikátoru GUID zaručuje globální jedinečnost a je flexibilní, tak, aby konfigurace lze použít s rozlišením na uzel, nebo jako konfiguraci role, která zahrnuje mnoho serverů, které by měl mít identické konfigurace.

#### <a name="guids"></a>Identifikátory GUID

Plánování konfigurace identifikátory GUID je vhodné další pozornost, pokud se rozhodujete nasazení na server vyžádané replikace. Neexistuje žádný konkrétní požadavek pro identifikátory GUID zpracování a proces je pravděpodobně být jedinečný pro každé prostředí. Proces může být v rozsahu od jednoduchého do komplexní: centrálně uloženého souboru CSV, jednoduché tabulku SQL, databáze CMDB nebo komplexní řešení, které vyžadují integraci s jiné nástroje nebo softwaru řešení. Existují dvě obecné přístupy:

 - **Přiřazení identifikátory GUID na server** – poskytuje míru zajištění, že každý konfigurace serveru je řízena jednotlivě. To poskytuje úroveň přesnost kolem aktualizace a může fungovat i v prostředí s několika servery.
 - **Přiřazení identifikátory GUID podle role serveru** – všechny servery, které provádí stejnou funkci, jako jsou třeba webové servery používají stejný identifikátor GUID jako odkaz požadovaná konfigurační data.  Upozorňujeme, že pokud mnoho servery sdílejí stejný identifikátor GUID, všechny z nich by aktualizován současně při změny v konfiguraci.

Identifikátor GUID je něco, co by měly zvažovat citlivá data, protože mohou být využity uživatel se zlými úmysly k získání zjištěných informací o tom, jak nasadit servery a ve svém prostředí nakonfigurováno. Další informace najdete v tématu [bezpečně přidělování identifikátorů GUID v režimu prostředí PowerShell požadovaného stavu konfigurace pro vyžádání obsahu](http://blogs.msdn.com/b/powershell/archive/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode.aspx).

Plánování úkolů|
---|
Kdo je zodpovědná za kopírování konfigurace v ke složce pro vyžádání obsahu server, jakmile jsou připravené?|
Pokud konfigurace vytvořené týmem aplikace, co proces bude přebírají je?|
Můžete využít úložiště k ukládání konfigurace, protože se právě vytvořené, mezi týmy?|
Se dá automatizovat proces kopírování konfigurace na server a vytváření kontrolní součet, jakmile jsou připravené?|
Jak budou namapujete identifikátory GUID na servery nebo role, a to uložení?|
Co můžete používat jako proces ke konfiguraci klientských počítačů, a způsobu, jakým bude ji integrovat váš proces pro vytváření a ukládání identifikátory GUID konfigurace?|

## <a name="installation-guide"></a>Průvodce instalací

*Skripty zadané v tomto dokumentu jsou stabilní příklady. Vždy zkontrolujte si důkladně skripty před provedením jejich v produkčním prostředí.*

### <a name="prerequisites"></a>Předpoklady

Ověření verze prostředí PowerShell na serveru použijte následující příkaz.

```powershell
$PSVersionTable.PSVersion
```

Pokud je to možné upgradujte na nejnovější verzi Windows Management Framework.
V dalším kroku Stáhnout `xPsDesiredStateConfiguration` modulu pomocí následujícího příkazu.


```powershell
Install-Module xPSDesiredStateConfiguration
```

Příkaz vyzve ke schválení před stažením modulu.

### <a name="installation-and-configuration-scripts"></a>Instalace a konfigurace skriptů
-

Je nejlepší metody nasadit server DSC za použití skriptu konfigurace DSC. Tento dokument nabídne skripty, včetně obě základní nastavení, které by konfigurovat jenom DSC webovou službu a upřesňující nastavení, která by konfigurovat Windows Server začátku do konce včetně DSC webové služby.

Poznámka: Aktuálně `xPSDesiredStateConfiguation` DSC modulu vyžaduje server jako národní prostředí cs-cz.

### <a name="basic-configuration-for-windows-server-2012"></a>Základní konfigurace pro Windows Server 2012
-------------------------------------------
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


### <a name="verify-pull-server-functionality"></a>Ověřte funkčnost serveru vyžádané replikace

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](invoke-webrequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}
Verify-DSCPullServer 'INSERT SERVER FQDN'

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


## <a name="additional-references-snippets-and-examples"></a>Další informace, fragmenty kódu a příklady

Tento příklad ukazuje, jak chcete ručně zahájit připojení klienta (vyžaduje WMF5) pro testování.

```powershell
Update-DSCConfiguration –Wait -Verbose
```

[Přidat DnsServerResourceRecordName](http://bit.ly/1G1H31L) rutina se používá k přidání typu záznamu CNAME do zóny DNS.

Funkce prostředí PowerShell k [vytvoření kontrolního součtu a publikovat MOF DSC pro vyžádání obsahu serveru SMB](http://bit.ly/1E46BhI) automaticky vytvoří požadované kontrolního součtu a pak zkopíruje MOF konfigurace i kontrolního součtu souborů k vyžádání serveru SMB.

## <a name="appendix---understanding-odata-service-data-file-types"></a>Příloha – Principy ODATA data služby typy souborů

Datový soubor je uložen vytvořit informace při nasazení serveru vyžádané replikace, která zahrnuje webovou službu OData. Typ souboru závisí na operačním systému, jak je popsáno níže.

 - **Windows Server 2012** typ souboru bude vždy .mdb
 - **Windows Server 2012 R2** typ souboru bude použita výchozí .edb .mdb uvedeno v konfiguraci

V [Advanced ukázkový skript](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) při instalaci serveru pro vyžádání obsahu, také najdete příklad toho, jak automaticky řídit nastavení souboru web.config, aby se zabránilo pravděpodobné, že chyba způsobila podle typu souboru.
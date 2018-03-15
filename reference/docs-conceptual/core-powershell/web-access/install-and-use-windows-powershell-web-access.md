---
ms.date: 2017-08-23
keywords: "rutiny prostředí PowerShell"
title: "nainstalovat a používat windows powershell web Accessu"
ms.openlocfilehash: 2ad7a701dbb464088d6ed47d49a8dc3fb9b911f8
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="install-and-use-windows-powershell-web-access"></a>Instalace a používání Windows PowerShell Web Accessu

Aktualizované: 5 listopad 2013 (Upravit: 23 srpen 2017)

Platí pro: Windows Server 2012 R2, Windows Server 2012

## <a name="introduction"></a>Úvod

Windows PowerShell Web Access, která je poprvé dostupné ve Windows serveru 2012 slouží jako brána prostředí Windows PowerShell poskytuje webové konzole Windows PowerShell, který je zaměřený na vzdáleném počítači. Umožňuje odborníkům ke spuštění příkazů prostředí Windows PowerShell a skriptů z konzoly prostředí Windows PowerShell ve webovém prohlížeči, bez prostředí Windows PowerShell, software pro vzdálenou správu nebo instalace modulu plug-in prohlížeče v klientském zařízení. Všechno, co je potřeba spustit webovou konzolu prostředí Windows PowerShell je správně nakonfigurovaná brána Windows PowerShell Web Access a prohlížeč v klientském zařízení, která podporuje JavaScript a přijímá soubory cookie.

Mezi příklady klientských zařízení patří přenosné počítače, nepracovní osobních počítače, vypůjčené počítače, tablety, webové terminály, počítače, na kterých se nepoužívá operační systém Windows, a prohlížeče mobilních telefonů. Odborníci na IT můžou provádět důležité úkoly správy na vzdálených serverech se systémem Windows ze zařízení, která mají přístup na internet a webový prohlížeč.

Po úspěšné brány nastavení a konfigurace mohou uživatelé konzole Windows PowerShell pomocí webového prohlížeče. Když uživatelé otevřou zabezpečeného webu Windows PowerShell Web Access, se po úspěšném ověření spustit webovou konzolu prostředí Windows PowerShell.

Windows PowerShell Web Access instalace a konfigurace je proces třech krocích:

1. [Instalace Windows PowerShell Web Accessu](#install-windows-powershell-web-access)
1. [Konfigurace brány](#configure-the-gateway)
1. [Konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule)

Než nainstalujete a nakonfigurujete Windows PowerShell Web Access, doporučujeme, přečtěte si celou tuto příručku, která obsahuje pokyny k instalaci, zabezpečení a odinstalace Windows PowerShell Web Accessu.
[Webová konzola prostředí PowerShell systému Windows](https://technet.microsoft.com/library/hh831417(v=ws.11).aspx) téma popisuje, jak se uživatelé přihlašují k webové konzole a věnuje se omezením a rozdílům mezi webovou konzolu prostředí Windows PowerShell a  **PowerShell.exe** konzoly. Přečtěte si koncoví uživatelé webové konzoly [použití webu na základě konzoly Windows Powershellu](use-the-web-based-windows-powershell-console.md), ale nemusí číst zbývající části této příručky.

Toto téma neobsahuje podrobné pokyny operations Webový Server IIS; pouze kroky nutné ke konfiguraci brány Windows PowerShell Web Access jsou popsané v tomto tématu. Další informace o konfiguraci a zabezpečení webů ve službě IIS najdete v dokumentaci ke službě IIS v části Viz také.

Následující diagram znázorňuje, jak funguje Windows PowerShell Web Access.

![Diagram webového přístupu k prostředí Windows PowerShell](images/Windows-PowerShell-Web-Access-diagram.jpg)

## <a name="requirements-for-running-windows-powershell-web-access"></a>Požadavky na spuštění Windows PowerShell Web Accessu

Windows PowerShell Web Access vyžaduje webový Server (IIS), rozhraní .NET Framework 4.5 a prostředí Windows PowerShell 3.0 nebo prostředí Windows PowerShell 4.0, aby byl spuštěn na serveru, na kterém chcete spustit bránu. Windows PowerShell Web Access na serveru se systémem Windows Server 2012 R2 nebo Windows Server 2012 můžete nainstalovat pomocí buď Průvodci přidáním rolí a funkcí ve Správci serveru nebo rutin nasazení prostředí Windows PowerShell pro správce serveru. Při instalaci Windows PowerShell Web Access pomocí Správce serveru nebo jeho rutin nasazení, požadované role a funkce se automaticky přidají jako součást procesu instalace.

Windows PowerShell Web Access umožňuje vzdáleným uživatelům přistupovat k počítačům ve vaší organizaci pomocí prostředí Windows PowerShell ve webovém prohlížeči. I když Windows PowerShell Web Access je nástroj pro správu přehledný a výkonný, webový přístup rizika z hlediska zabezpečení a by měl být nakonfigurovaný jako bezpečně. Doporučujeme správcům, kteří konfigurují bránu Windows PowerShell Web Access používat vrstvy zabezpečení dostupné pravidla autorizace na základě rutiny součástí Windows PowerShell Web Access a zabezpečení vrstvy, které jsou k dispozici v (Webový Server Služba IIS) a aplikace třetích stran. Tato dokumentace obsahuje dva příklady nezabezpečeného použití, které doporučujeme pouze pro testovací prostředí, a příklady, které se doporučují pro zabezpečená nasazení.

## <a name="browser-and-client-device-support"></a>Podpora prohlížeče a klientského zařízení

Windows PowerShell Web Access podporuje následující internetových prohlížečů.
I když mobilní prohlížeče nejsou oficiálně podporované, mnoho může být možné spustit webovou konzolu prostředí Windows PowerShell. Jiné prohlížeče, které používají soubory cookie a umožňují spouštět JavaScript a weby HTTPS, budou pravděpodobně fungovat, ale nejsou oficiálně testované.

### <a name="supported-desktop-computer-browsers"></a>Podporované prohlížeče pro počítače

- Aplikaci Windows Internet Explorer pro Microsoft Windows 8.0, 9.0, 10.0 a 11.0
- Mozilla Firefox 10.0.2
- Google Chrome 17.0.963.56m pro Windows
- Apple Safari 5.1.2 pro Windows
- Apple Safari 5.1.2 pro Mac OS

### <a name="minimally-tested-mobile-devices-or-browsers"></a>Mobilní zařízení nebo prohlížeče, které byly jenom minimálně testované

- Windows Phone 7 a 7.5
- Google Android WebKit 3.1 prohlížeče Android 2.2.1 (jádro 2.6)
- Apple Safari pro operační systém iPhonu – 5.0.1
- Apple Safari pro operační systém Ipadu 2 – 5.0.1

### <a name="browser-requirements"></a>Požadavky na prohlížeč

Pokud chcete používat webové konzole Windows PowerShell Web Access, postupujte takto prohlížeče.

- Povolit soubory cookie z webu brány Windows PowerShell Web Access.
- Je nutné, aby umožňovaly otevírání a čtení stránek HTTPS.
- Je nutné, aby otevíraly a spouštěly weby, které používají JavaScript.

## <a name="recommended-quick-deployment"></a>Doporučené rychlé nasazení

Na serveru se systémem Windows Server 2012 R2 nebo Windows Server 2012 můžete nainstalovat Windows PowerShell Web Access bránu pomocí buď rutiny prostředí Windows PowerShell nebo pomocí Přidat role a funkce průvodce, který se otevírá ze ve Správci serveru. Pro rychlou instalaci a konfiguraci použijte rutiny prostředí Windows PowerShell, jak je popsáno v této části.

1. [Instalace Windows PowerShell Web Accessu](#install-Windows-powershell-web-access)
1. [Konfigurace brány](#configure-the-gateway)
1. [Konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule)

### <a name="install-windows-powershell-web-access"></a>Instalace Windows PowerShell Web Accessu

#### <a name="to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets"></a>Postup instalace Windows PowerShell Web Accessu pomocí rutin Windows PowerShellu

1. Proveďte jednu z následujících způsobů otevřete relaci prostředí Windows PowerShell se zvýšenými uživatelskými právy.
    - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.
    - V systému Windows **spustit** obrazovky, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na **spustit jako správce**.

    >**![Poznámka:](images/note.jpeg) Poznámka** v prostředí Windows PowerShell 3.0 a 4.0, je nutné naimportovat modul rutin Správce serveru do relace prostředí Windows PowerShell před spuštěním rutin, které jsou součástí daného modulu. Modul se automaticky importuje, jakmile poprvé spustíte rutinu, která je součástí daného modulu. Rutiny prostředí Windows PowerShell nejsou malá a velká písmena.

1. Zadejte následující příkaz a stiskněte klávesu **Enter**, kde *název_počítače* představuje vzdálený počítač, na kterém chcete nainstalovat Windows PowerShell Web Access, pokud je k dispozici. Parametr `-Restart` automaticky restartuje cílové servery, pokud je to potřeba.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -IncludeManagementTools -Restart`

   >**![Poznámka:](images/note.jpeg) Poznámka**
   >
   >Instalace Windows PowerShell Web Accessu pomocí rutin prostředí Windows PowerShell nepřidá nástroje pro správu webového serveru (IIS) ve výchozím nastavení. Pokud chcete nainstalovat nástroje pro správu na stejném serveru jako brána Windows PowerShell Web Access, přidejte `-IncludeManagementTools` parametr k instalačnímu příkazu (jak uvádí tento krok). Pokud spravujete web Windows PowerShell Web Access ze vzdáleného počítače, nainstalovat modul snap-in Správce služby IIS tak, že instalace [vzdáleného serveru správy Toolsfor Windows 8.1](http://go.microsoft.com/fwlink/?LinkID=304145) nebo [pro vzdálenou správu serveru Nástroje pro systém Windows 8](http://go.microsoft.com/fwlink/p/?LinkID=238560) na počítači, ze kterého chcete spravovat bránu.
   
   Pokud chcete nainstalovat role a funkce na offline virtuálním pevném disku, musíte přidat parametr `-ComputerName` i parametr `-VHD`. Parametr `-ComputerName` obsahuje název serveru, ke kterému se má připojit virtuální pevný disk. Parametr `-VHD` pak obsahuje cestu k souboru VHD na určeném serveru.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -IncludeManagementTools -Restart`

1. Po dokončení instalace ověřte, že Windows PowerShell Web Access byl nainstalován na cílových serverech spuštěním **Get-WindowsFeature** rutiny na cílovém serveru, v konzole Windows PowerShell, který byl otevřen se zvýšenými uživatelskými právy. Můžete také ověřit, že Windows PowerShell Web Access byla nainstalována do konzoly Správce serveru, výběrem na cílový server na **všechny servery** stránku a pak zobrazením **role a funkce** dlaždice pro vybraný server. Můžete také zobrazit soubor readme pro Windows PowerShell Web Access.

1. Po instalaci Windows PowerShell Web Access, zobrazí se výzva k souboru readme, který obsahuje pokyny základní požadované instalaci brány. Tyto pokyny k instalaci jsou také v následující části [bránu nakonfigurovat](#configure-the-gateway). Cesta k souboru readme je **C:\\Windows\\webové\\PowerShellWebAccess\\wwwroot\\README.txt**.

### <a name="configure-the-gateway"></a>Konfigurace brány

**Rutiny Install-PswaWebApplication** rutina je rychlý způsob, jak získat Windows PowerShell Web Access nakonfigurované. I když můžete do rutiny `Install-PswaWebApplication` přidat parametr `UseTestCertificate` k instalaci certifikátu SSL podepsaného držitelem pro testovací účely, není to bezpečné. Pro bezpečné produkční prostředí vždy používejte platný certifikát SSL, který podepsala certifikační autorita.
Správci mají možnost testovací certifikát nahradit podobným certifikátem, který sami vyberou, pomocí konzoly Správce služby IIS.

Můžete dokončit konfiguraci webové aplikace Windows PowerShell Web Access tak, že spustíte `Install-PswaWebApplication` rutiny nebo provedením kroků konfiguraci na základě grafickým uživatelským rozhraním ve Správci služby IIS. Ve výchozím nastavení rutina nainstaluje webovou aplikaci, **pswa** (a fond aplikací, **pswa_pool**) v **Default Web Site** kontejneru, jak je vidět ve Správci služby IIS; Pokud Chcete, můžete určit, aby se rutina mohla měnit kontejneru výchozího webu webové aplikace. Správce služby IIS nabízí možnosti konfigurace, které jsou k dispozici pro webové aplikace, jako je například změna číslo portu nebo certifikátu vrstvy SSL (Secure Sockets Layer).

>**![Poznámka k zabezpečení](images/securitynote.jpeg) Poznámka k zabezpečení**
> 
>Důrazně doporučujeme, aby správci bránu nakonfigurovali na používání platného certifikátu podepsaného certifikační autoritou. 

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-test-certificate-by-using-install-pswawebapplication"></a>Nakonfigurování brány Windows PowerShell Web Accessu s testovacím certifikátem pomocí rutiny Install-PswaWebApplication

1. Proveďte jednu z následujících způsobů otevřete relaci prostředí Windows PowerShell.

    - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu.

    - V systému Windows **spustit** obrazovky, klikněte na tlačítko **prostředí Windows PowerShell**.

2. Zadejte následující příkaz a stiskněte klávesu **Enter**.

    **Rutiny Install-PswaWebApplication - UseTestCertificate**

  >**![Poznámka k zabezpečení](images/securitynote.jpeg) Poznámka k zabezpečení**
  >
  >Parametr `UseTestCertificate` by se měl používat jenom v privátním testovacím prostředí. Pro zabezpečené produkční prostředí doporučujeme použít platný certifikát podepsaný certifikační autoritou.

Spuštěním rutiny se nainstaluje webovou aplikaci Windows PowerShell Web Access v kontejneru výchozí web služby IIS. Rutina vytvoří infrastrukturu požadovanou pro spuštění Windows PowerShell Web Access na výchozím webu, `https://<server_name>/pswa`. Pokud chcete webovou aplikaci nainstalovat na jiný web, zadejte jeho název přidáním parametru `WebSiteName`. Pokud chcete změnit název webové aplikace (výchozí je `pswa`), přidejte parametr `WebApplicationName`.

Spuštěním rutiny se konfiguruje následující nastavení. Pokud chcete, můžete je ručně změnit v konzole Správce služby IIS.

- Cesta: / pswa
- ApplicationPool: pswa_pool
- EnabledProtocols: http
- PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot

**Příklad**: `Install-PswaWebApplication -webApplicationName myWebApp -useTestCertificate`

V tomto příkladu je výsledný web pro Windows PowerShell Web Access je https://\<*název_serveru*\>/myWebApp.

>**![Poznámka:](images/note.jpeg) Poznámka** 
> 
>Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel. Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule) a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-genuine-certificate-by-using-install-pswawebapplication-and-iis-manager"></a>Nakonfigurování brány Windows PowerShell Web Access s pravým certifikátem pomocí rutiny Install-PswaWebApplication a Správce služby IIS

1. Proveďte jednu z následujících způsobů otevřete relaci prostředí Windows PowerShell.

    - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu.

    - V systému Windows **spustit** obrazovky, klikněte na tlačítko **prostředí Windows PowerShell**.

2. Zadejte následující příkaz a stiskněte klávesu **Enter**.

    **Rutiny Install-PswaWebApplication**

    Spuštěním rutiny se konfiguruje následující nastavení brány.
    Pokud chcete, můžete je ručně změnit v konzole Správce služby IIS.
    Můžete také zadat hodnoty parametrů `WebsiteName` a `WebApplicationName` rutiny `Install-PswaWebApplication`.

    - Cesta: / pswa

    - ApplicationPool: pswa_pool

    - EnabledProtocols: http

    - PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot

3. Otevřete konzolu Správce služby IIS některým z následujících postupů.

    - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows. Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.

    - V systému Windows **spustit** obrazovky, klikněte na tlačítko **správce serveru**.

4. V podokně stromu Správce služby IIS rozbalte uzel serveru, na kterém je nainstalována Windows PowerShell Web Access až **lokality** složky. Rozbalte **lokality** složky.

5. Vyberte web, ve kterém jste nainstalovali webovou aplikaci Windows PowerShell Web Access. V **akce** podokně klikněte na tlačítko **vazby**.

6. V **vazbu webu** dialogové okno, klikněte na tlačítko **přidat**.

7. V **přidat vazbu webu** dialogu **typ** pole, vyberte **https**.

8. V **certifikát SSL** certifikátu podepsaného svým vyberte z rozevírací nabídky. Klikněte na **OK**. V tématu [nakonfigurovat certifikát SSL ve Správci služby IIS](#to-configure-an-ssl-certificate-in-iis-Manager) v tomto tématu pro další informace o tom, jak získat certifikát.

    Windows PowerShell Web Access webové aplikace je nyní nakonfigurován na použití podepsaného certifikátu SSL.

    Dostanete tak, že otevřete Windows PowerShell Web Access **https://\<název_serveru\>/pswa** v okně prohlížeče.

>**![Poznámka:](images/note.jpeg) Poznámka** 
> 
>Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel. 
>Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule), v tomto tématu a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configure-a-restrictive-authorization-rule"></a>Konfigurace omezujícího autorizačního pravidla

Po nainstalování Windows PowerShell Web Access a konfiguraci brány, uživatelé mohli otevřít přihlašovací stránku v prohlížeči, ale se nelze přihlásit, dokud správce Windows PowerShell Web Access explicitně neudělí přístup. Řízení přístupu Windows PowerShell Web Access spravuje pomocí sady rutin prostředí Windows PowerShell, které jsou popsané v následující tabulce. Neexistuje žádné srovnatelné grafické uživatelské rozhraní pro přidávání nebo správu autorizačních pravidel. Podrobné informace o rutinách Windows PowerShell Web Access, najdete v referenčních tématech rutiny, [rutiny prostředí Windows PowerShell Web Access](cmdlets/web-access-cmdlets.md).

Další podrobnosti o zabezpečení a Windows PowerShell Web Access autorizačních pravidel najdete [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-add-a-restrictive-authorization-rule"></a>Přidání omezujícího autorizačního pravidla

1. Proveďte jednu z následujících způsobů otevřete relaci prostředí Windows PowerShell se zvýšenými uživatelskými právy.

    - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.

    - V systému Windows **spustit** obrazovky, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na **spustit jako správce**.

2. Volitelný krok pro omezení přístupu uživatelů s použitím konfigurací relace: Ověřte, že konfigurace relace, které chcete použít v pravidlech vaší již existuje. Pokud se ještě nejsou vytvořené, použijte pokyny pro vytvoření konfigurací relace v [about_Session_Configuration_Files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configurations).

3. Zadejte následující příkaz a stiskněte klávesu **Enter**.

   `Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>`

   Toto autorizační pravidlo umožňuje konkrétní přístup uživatele k jednomu počítači v síti, ke kterému mají obvykle přístup, včetně přístupu ke konfiguraci konkrétní relace, která je omezená na uživatele typické skriptování a je třeba rutiny.
   
   V následujícím příkladu se uživateli se jménem `JSmith` v doméně `Contoso` udělí přístup ke správě počítače `Contoso_214` a použití konfigurace relace s názvem `NewAdminsOnly`.

   `Add-PswaAuthorizationRule -UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly`

4. Ověřte, že pravidlo vytvořila spuštěním `Get-PswaAuthorizationRule` rutiny, nebo `Test-PswaAuthorizationRule -UserName <domain\user> -ComputerName <computer-name>`

5. Například `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

Po nakonfigurování autorizační pravidlo, jste připraveni Autorizovaní uživatelé přihlásit k webové konzole a začít používat Windows PowerShell Web Access.

## <a name="custom-deployment"></a>Vlastní nasazení

Brána Windows PowerShell Web Access na serveru se systémem Windows Server 2012 R2 nebo Windows Server 2012 můžete nainstalovat pomocí funkce Průvodce přidáním rolí a ve Správci serveru. Po instalaci Windows PowerShell Web Access, můžete přizpůsobit konfiguraci brány ve Správci služby IIS.

### <a name="install-windows-powershell-web-access"></a>Instalace Windows PowerShell Web Accessu

#### <a name="to-install-windows-powershell-web-access-by-using-the-add-roles-and-features-wizard"></a>Postup instalace Windows PowerShell Web Accessu pomocí průvodce přidáním rolí a funkcí

1. Pokud správce serveru je už otevřená, přejděte k dalšímu kroku. Pokud správce serveru už není otevřený, otevřete ho jedním z následujících akcí.

    - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows.

    - V systému Windows **spustit** obrazovky, klikněte na tlačítko **správce serveru**.

2. Na **spravovat** nabídky, klikněte na tlačítko **přidat role a funkce**.

3. Na **vybrat typ instalace** vyberte **instalace na základě rolí nebo na základě funkcí**. Klikněte na **Další**.

4. Na **vybrat cílový server** stránky, vyberte server z fondu serverů nebo offline virtuální pevný disk. Pokud chcete jako cílový server zvolit offline virtuální pevný disk, vyberte nejdřív server, ke kterému chcete virtuální pevný disk připojit, a pak vyberte příslušný soubor VHD. Informace o tom, jak přidat servery do fondu serverů, naleznete v nápovědě Správce serveru. Po výběru cílového serveru, klikněte na tlačítko **Další**.

5. Na **vyberte funkce** stránku průvodce, rozbalte položku **prostředí Windows PowerShell**a potom vyberte **Windows PowerShell Web Access**.

6. Zobrazí se výzva k přidání požadovaných funkcí, jako je rozhraní .NET Framework 4.5 a služby role Webový Server (IIS). Přidejte požadované funkce a pokračujte.

    >**![Poznámka:](images/note.jpeg) Poznámka** 
    >
    >Instalace Windows PowerShell Web Access pomocí funkce Průvodce přidáním rolí a nainstaluje také webový Server (IIS), včetně modulu snap-in Správce služby IIS. Modul snap-in a další nástroje správy služby IIS jsou nainstalované ve výchozím nastavení, pokud použijete Průvodce přidáním rolí a funkcí. Pokud instalujete Windows PowerShell Web Accessu pomocí rutin prostředí Windows PowerShell, jak je popsáno v následujícím postupu, nejsou ve výchozím nastavení Přidat nástroje pro správu.

7. Na **potvrdit vybrané možnosti instalace** stránky, pokud soubory funkcí pro Windows PowerShell Web Access nejsou uložené na cílovém serveru, který jste vybrali v kroku 4, klikněte na tlačítko **zadejte alternativní cestu ke zdroji**a zadejte cestu k souborům funkcí. Jinak, klikněte na tlačítko **nainstalovat**.

8. Po kliknutí na tlačítko **nainstalovat**, **průběh instalace** zobrazí průběh instalace, výsledky a zprávy, jako je například upozornění, chyby nebo kroky konfigurace po instalaci, které jsou vyžaduje se pro Windows PowerShell Web Access. Po instalaci Windows PowerShell Web Access, zobrazí se výzva k souboru readme, který obsahuje pokyny základní požadované instalaci brány. Tyto pokyny jsou také uvedené v tomto tématu. Cesta k souboru readme je `C:\Windows\Web\PowerShellWebAccess\wwwroot\README.txt`.

### <a name="configure-the-gateway"></a>Konfigurace brány

Pokyny v této části jsou určené pro instalaci Windows PowerShell Web Access webové aplikace v podadresáři a ne v kořenovém adresáři vašeho webu. Tento postup je akce v grafickém uživatelském rozhraní ekvivalentní akci, kterou provádí rutina `Install-PswaWebApplication`. Tato část také obsahuje pokyny, jak pomocí Správce služby IIS a nakonfigurujte bránu Windows PowerShell Web Access jako kořenový Web.

#### <a name="to-use-iis-manager-to-configure-the-gateway-in-an-existing-website"></a>Konfigurace brány na stávajícím webu pomocí Správce služby IIS

1. Otevřete konzolu Správce služby IIS některým z následujících postupů.

    - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows. Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.

    - V systému Windows **spustit** zadejte jakékoliv části názvu **Správce Internetové informační služby (IIS)**. Klikněte na zástupce, jakmile se zobrazí v **aplikace** výsledky.

2. Vytvořte nový fond aplikací pro Windows PowerShell Web Access. Rozbalte uzel serveru brány ve Správci služby IIS podokně stromu vyberte **fondy aplikací**a klikněte na tlačítko **přidat fond aplikací** v **akce** podokně.

3. Přidat nový fond aplikací s názvem **pswa_pool**, nebo zadejte jiný název. Klikněte na **OK**.

4. V podokně stromu Správce služby IIS rozbalte uzel serveru, na kterém je nainstalována Windows PowerShell Web Access až **lokality** složky. Vyberte **lokality** složky.

5. Klikněte pravým tlačítkem na web (například **Default Web Site**) do které chcete přidat web Windows PowerShell Web Access a potom klikněte na **přidat aplikaci**.

6. V **Alias** pole, zadejte pswa nebo uveďte jiný alias. Z aliasu se stane název virtuálního adresáře. Například **pswa** v následující adresu URL označuje alias zadaný v tomto kroku: **https://\<název serveru\>/pswa**.

7. V **fond aplikací** vyberte fond aplikací, který jste vytvořili v kroku 3.

8. V **fyzická cesta** pole, vyhledejte umístění aplikace. Můžete použít výchozí umístění %windir%/Web/PowerShellWebAccess/wwwroot. Klikněte na **OK**.

9. Postupujte podle kroků v postupu konfigurace certifikátu SSL ve službě IIS manager](#to-configure-an-ssl-certificate-in-iis-Manager) v tomto tématu.

10. ![](images/SecurityNote.jpeg) Volitelný krok zabezpečení:

    S webem vybraným v podokně stromu, dvakrát klikněte na **nastavení SSL** v podokně obsahu. Vyberte **požadovat protokol SSL**a potom v **akce** podokně klikněte na tlačítko **použít**. Volitelně můžete v **nastavení SSL** podokně, můžete vyžadovat, aby uživatelé připojující se k webu Windows PowerShell Web Access měli klientské certifikáty. Klientské certifikáty pomáhají ověřit identitu uživatele klientského zařízení. Další informace o tom, jak může vyžadování klientských certifikátů zvýšit zabezpečení Windows PowerShell Web Access naleznete v tématu [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md) v této příručce.

11. Otevře relaci prohlížeče v klientském zařízení. Další informace o podporovaných prohlížečích a zařízeních najdete v tématu [prohlížeče a klientského zařízení podporují](#browser-and-client-device-support) v tomto tématu.

12. Otevřete nový web Windows PowerShell Web Access **https://\<*názvu serveru brány*\>/pswa**.

    V prohlížeči by měl zobrazit stránku přihlášení Windows PowerShell Web Access konzoly.

    >**![Poznámka:](images/note.jpeg) Poznámka** 
    > 
    >Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel. 
    >Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule), v tomto tématu a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

13. V relaci Windows Powershellu otevřené se zvýšenými uživatelskými právy (příkazem Spustit jako správce) spusťte následující skript, ve kterém *název_fondu_aplikací* představuje název fondu aplikací, který jste vytvořili v kroku 3, aby měl fond aplikací přístupová práva k souboru autorizace.

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    Pokud chcete zobrazit stávající přístupová práva k souboru autorizace, spusťte následující příkaz:

        c:\windows\system32\icacls.exe $authorizationFile

#### <a name="to-use-iis-manager-to-configure-the-gateway-as-a-root-website-with-a-test-certificate"></a>Konfigurace brány jako kořenového webu se zkušebním certifikátem pomocí Správce služby IIS

1. Otevřete konzolu Správce služby IIS některým z následujících postupů.

    - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows. Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.

    - V systému Windows **spustit** zadejte jakékoliv části názvu **Správce Internetové informační služby (IIS)**. Klikněte na zástupce, jakmile se zobrazí v **aplikace** výsledky.

2. V podokně stromu Správce služby IIS rozbalte uzel serveru, na kterém je nainstalována Windows PowerShell Web Access až **lokality** složky. Vyberte **lokality** složky.

3. V **akce** podokně klikněte na tlačítko **přidat web**.

4. Zadejte název pro web, jako například **Windows PowerShell Web Access**.

5. Pro nový web se automaticky vytvoří fond aplikací. Chcete-li použít jiný fond aplikací, klikněte na tlačítko **vyberte** vyberte fond aplikací pro přidružení k novému webu. Vyberte alternativní fond aplikací v **vybrat fond aplikací** dialogové okno a pak klikněte na tlačítko **OK**.

6. V **fyzická cesta** textové pole, přejděte na %*windir*% / Web/PowerShellWebAccess/wwwroot.

7. V **typ** pole z **vazby** oblasti, vyberte **https**.

8. Přiřaďte číslo portu webu, který ještě nepoužívá jiný web nebo aplikace. Chcete-li vyhledat otevřené porty, můžete spustit **netstat** příkazu v okně příkazového řádku. Výchozí číslo portu je 443.

    Pokud už číslo 443 používá jiný web nebo pokud máte jiné bezpečnostní důvody pro změnu čísla portu, změňte výchozí port. Pokud vybraný port používá jiný web, který běží na serveru brány, upozornění se zobrazí po kliknutí na tlačítko **OK** v **přidat web** dialogové okno. Ke spuštění Windows PowerShell Web Access, je nutné použít nepoužívaný port.

9. Volitelně můžete v případě potřeby pro vaši organizaci, zadejte název hostitele, který vám vyhovuje vaší organizaci a uživatelích, jako například **www.contoso.com**. Klikněte na **OK**.

10. Aby bylo vaše produkční prostředí ještě bezpečnější, rozhodně doporučujeme použít platný certifikát podepsaný certifikační autoritou. Protože uživatelé lze připojit pouze k Windows PowerShell Web Access přes web HTTPS, je nutné zadat certifikát SSL. V tématu [nakonfigurovat certifikát SSL ve Správci služby IIS](#to-configure-an-ssl-certificate-in-iis-Manager) v tomto tématu pro další informace o tom, jak získat certifikát.

11. Klikněte na tlačítko **OK** zavřete **přidat web** dialogové okno.

12. V relaci Windows Powershellu otevřené se zvýšenými uživatelskými právy (příkazem Spustit jako správce) spusťte následující skript, ve kterém *název_fondu_aplikací* představuje název fondu aplikací, který jste vytvořili v kroku 4, aby měl fond aplikací přístupová práva k souboru autorizace.

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    Pokud chcete zobrazit stávající přístupová práva k souboru autorizace, spusťte následující příkaz:

        c:\windows\system32\icacls.exe $authorizationFile

13. S novým webem vybraným v podokně stromu Správce služby IIS, klikněte na tlačítko **spustit** v **akce** podokně spusťte web.

14. Otevře relaci prohlížeče v klientském zařízení. Další informace o podporovaných prohlížečích a zařízeních najdete v tématu [prohlížeče a klientského zařízení podporují](#browser-and-client-device-support) v tomto dokumentu.

15. Otevřete nový web Windows PowerShell Web Access.

    Vzhledem k tomu, že kořenový web odkazuje na složku Windows PowerShell Web Access, v prohlížeči by měla zobrazit přihlašovací stránce Windows PowerShell Web Access při spuštění **https://\<*název_serveru_brány* \>**. Je třeba ji přidat **/pswa** na adresu URL.

    >**![Poznámka:](images/note.jpeg) Poznámka** 
    > 
    >Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel. 
    >Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule), v tomto tématu a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configure-a-restrictive-authorization-rule"></a>Konfigurace omezujícího autorizačního pravidla

Po nainstalování Windows PowerShell Web Access a konfiguraci brány, uživatelé mohli otevřít přihlašovací stránku v prohlížeči, ale se nelze přihlásit, dokud správce Windows PowerShell Web Access explicitně neudělí přístup. Řízení přístupu Windows PowerShell Web Access spravuje pomocí sady rutin prostředí Windows PowerShell, které jsou popsané v následující tabulce. Neexistuje žádné srovnatelné grafické uživatelské rozhraní pro přidávání nebo správu autorizačních pravidel. Podrobné informace o rutinách Windows PowerShell Web Access, najdete v referenčních tématech rutiny, [rutiny prostředí Windows PowerShell Web Access](cmdlets/web-access-cmdlets.md).

Další podrobnosti o zabezpečení a Windows PowerShell Web Access autorizačních pravidel najdete [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-add-a-restrictive-authorization-rule"></a>Přidání omezujícího autorizačního pravidla

1. Proveďte jednu z následujících způsobů otevřete relaci prostředí Windows PowerShell se zvýšenými uživatelskými právy.

    - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.

    - V systému Windows **spustit** obrazovky, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na **spustit jako správce**.

2. ![Poznámka k zabezpečení](images/SecurityNote.jpeg) Volitelný krok pro omezení přístupu uživatelů s použitím konfigurací relace:

    Ověřte, že konfigurace relace, které chcete v pravidlech použít, už existují. Pokud se ještě nejsou vytvořené, použijte pokyny pro vytvoření konfigurací relace v [about_Session_Configuration_Files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configurations).

3. Zadejte následující příkaz a stiskněte klávesu **Enter**.

        Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    Toto autorizační pravidlo umožňuje konkrétní přístup uživatele k jednomu počítači v síti, ke kterým mají obvykle přístup, včetně přístupu ke konfiguraci konkrétní relace, která je omezená na uživatele '™ s typické skriptování a rutiny potřebám. 
    
    V následujícím příkladu se uživateli se jménem `JSmith` v doméně `Contoso` udělí přístup ke správě počítače `Contoso_214` a použití konfigurace relace s názvem `NewAdminsOnly`.

        Add-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4. Ověřte, že pravidlo vytvořila spuštěním `Get-PswaAuthorizationRule` rutiny nebo `Test-PswaAuthorizationRule -UserName '<domain\user>' -ComputerName <computer-name>`. 

    Například `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

Po nakonfigurování autorizační pravidlo, jste připraveni Autorizovaní uživatelé přihlásit k webové konzole a začít používat Windows PowerShell Web Access.

## <a name="configure-a-genuine-certificate"></a>Konfigurace pravého certifikátu

Aby bylo produkční prostředí zabezpečené, používejte vždy platný certifikát SSL podepsaný certifikační autoritou (CA). Postup v této části uvádí, jak získat a použít platný certifikát SSL od certifikační autority.

### <a name="to-configure-an-ssl-certificate-in-iis-manager"></a>Konfigurace certifikátu SSL ve Správci služby IIS

1. V podokně stromu Správce služby IIS vyberte server, na kterém je nainstalovaný Windows PowerShell Web Access.

2. V podokně obsahu poklikejte na **certifikáty serveru**.

3. V **akce** podokně, proveďte jednu z následujících akcí. Další informace o konfiguraci certifikátů serveru ve službě IIS najdete v tématu [konfigurace certifikátů serveru ve službě IIS 7](https://technet.microsoft.com/library/cc732230.aspx).

    - Klikněte na tlačítko **importovat** k naimportovat stávající platný certifikát z umístění v síti.

    - Klikněte na tlačítko **vytvořit žádost o certifikát** k vyžádání certifikátu od certifikační Autority, jako [VeriSign](http://www.verisign.com/), [Thawte](https://www.thawte.com/), nebo [GeoTrust](https://www.geotrust.com/). Běžný název certifikátu musí odpovídat hlavičce hostitele v žádosti.

      Například, pokud prohlížeč klienta požadavky http://www.contoso.com/, a také musí být běžný název http://www.contoso.com/. Toto je nejbezpečnější a doporučená možnost poskytnutí brány Windows PowerShell Web Access s certifikátem.

    - Klikněte na tlačítko **vytvořit certifikát podepsaný svým držitelem** vytvořit certifikát můžete použít okamžitě a mít později podepsaný Certifikační autoritou v případě potřeby. Zadejte popisný název certifikátu podepsaného svým držitelem, například **Windows PowerShell Web Access**. Tato možnost se nepovažuje za bezpečnou a doporučuje se pouze pro privátní testovací prostředí.

4. Po vytvoření nebo získání certifikátu, vyberte web, na kterou se certifikát používá (například **Default Web Site**) ve Správci služby IIS podokně stromu a pak klikněte na **vazby** v **Akce** podokně.

5. V **přidat vazbu webu** dialogové okno pole, přidejte **https** vazby pro lokalitu, pokud již není zobrazen. Pokud nepoužíváte certifikát podepsaný držitelem, zadejte název hostitele z kroku 3 tohoto postupu. Pokud používáte certifikát podepsaný držitelem, není tento krok povinný.

6. Vyberte certifikát, který jste získali nebo vytvořili v kroku 3 tohoto postupu a pak klikněte na tlačítko **OK**.

## <a name="using-the-web-based-windows-powershell-console"></a>Používání webové konzoly Windows PowerShellu

Po nainstalování Windows PowerShell Web Access a po dokončení konfigurace brány, jak je popsáno v tomto tématu, webové konzoly prostředí Windows PowerShell je připravený k použití. Další informace o získávání ve webové konzole najdete v tématu [Webová konzola prostředí PowerShell systému Windows](use-the-web-based-windows-powershell-console.md).

## <a name="see-also"></a>Viz také

- [Internetová informační služba (IIS) 7.0 dokumentace](https://technet.microsoft.com/library/cc753433.aspx)
- [Nápověda k aplikaci IIS 7.0 Manager](https://technet.microsoft.com/library/cc732664.aspx)
- [Konfigurace zabezpečení webového serveru (IIS 7)](https://technet.microsoft.com/library/cc731278.aspx)
- [Materiály pro nasazení protokolu IPsec](https://technet.microsoft.com/network/bb531150)

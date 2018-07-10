---
ms.date: 08/23/2017
keywords: rutiny prostředí PowerShell
title: instalace a používání windows powershell web Accessu
ms.openlocfilehash: d60670954d6ab6998e905382383d60ead1129d31
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893752"
---
# <a name="install-and-use-windows-powershell-web-access"></a>Instalace a používání Windows PowerShell Web Accessu

Aktualizováno: 5 listopad 2013 (upravovat: 23. srpna 2017)

Platí pro: Windows Server 2012 R2, Windows Server 2012

## <a name="introduction"></a>Úvod

Windows PowerShell Web Accessu, poprvé byla představena ve Windows serveru 2012, funguje jako brána Windows Powershellu, poskytuje webové konzoly prostředí Windows PowerShell, která je cílená na vzdálený počítač. Umožňuje odborníkům na IT spouštět příkazy Windows Powershellu a skripty z konzoly Windows Powershellu ve webovém prohlížeči se žádná prostředí Windows PowerShell, software pro vzdálenou správu nebo instalace modulu plug-in prohlížeče v klientském zařízení. Vše, co je potřeba spustit webovou konzolu prostředí Windows PowerShell je bránu Windows PowerShell Web Access správně nakonfigurován a prohlížeč v klientském zařízení, která podporuje JavaScript a přijímá soubory cookie.

Mezi příklady klientských zařízení patří přenosné počítače, nepracovní osobních počítače, vypůjčené počítače, tablety, webové terminály, počítače, na kterých se nepoužívá operační systém Windows, a prohlížeče mobilních telefonů. Odborníci na IT můžou provádět důležité úkoly správy na vzdálených serverech se systémem Windows ze zařízení, která mají přístup na internet a webový prohlížeč.

Po úspěšném nastavení a nakonfigurování brány mohou uživatelé konzoly Windows Powershellu pomocí webového prohlížeče. Když uživatelé otevřou zabezpečený web Windows PowerShell Web Accessu, můžou běžet po úspěšném ověření webové konzoly Windows Powershellu.

Windows PowerShell Web Accessu nastavení a konfigurace je třech krocích:

1. [Instalace Windows PowerShell Web Accessu](#install-windows-powershell-web-access)
1. [Konfigurace brány](#configure-the-gateway)
1. [Konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule)

Než nainstalujete a nakonfigurujete Windows PowerShell Web Accessu, doporučujeme, abyste si celou tuto příručku, který obsahuje pokyny k instalaci, zabezpečení a odinstalace Windows PowerShell Web Accessu.
[Pomocí webové konzoly Powershellu Windows](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831417(v=ws.11)) téma popisuje, jak se uživatelé přihlašují k webové konzole a věnuje se omezením a rozdílům mezi webovou konzolu prostředí Windows PowerShell a  **PowerShell.exe** konzoly. Přečtěte si koncoví uživatelé webové konzoly [používání webové konzoly Windows Powershellu](use-the-web-based-windows-powershell-console.md), ale nemusí číst zbývající části této příručky.

Toto téma neobsahuje podrobné pokyny operace webového serveru služby IIS; v tomto tématu jsou popsány pouze kroky nutné ke konfiguraci brány Windows PowerShell Web Accessu. Další informace o konfiguraci a zabezpečení webů ve službě IIS najdete v dokumentaci ke službě IIS v části Viz také.

Následující diagram ukazuje, jak funguje Windows PowerShell Web Accessu.

![Diagram webového přístupu k prostředí Windows PowerShell](images/Windows-PowerShell-Web-Access-diagram.jpg)

## <a name="requirements-for-running-windows-powershell-web-access"></a>Požadavky na spuštění Windows PowerShell Web Accessu

Windows PowerShell Web Accessu vyžaduje webový Server (IIS), .NET Framework 4.5 a Windows PowerShell 3.0 nebo Windows PowerShell 4.0 na server, na kterém chcete spustit bránu. Windows PowerShell Web Accessu můžete nainstalovat na serveru, na kterém běží Windows Server 2012 R2 nebo Windows Server 2012 pomocí buď Průvodci přidáním rolí a funkcí ve Správci serveru nebo rutiny prostředí Windows PowerShell pro nasazení pro správce serveru. Při instalaci Windows PowerShell Web Accessu pomocí Správce serveru nebo jeho rutin nasazení, požadované role a funkce jsou automaticky přidány jako součást procesu instalace.

Windows PowerShell Web Accessu umožňuje vzdáleným uživatelům přístup k počítačům ve vaší organizaci pomocí prostředí Windows PowerShell ve webovém prohlížeči. I když Windows PowerShell Web Accessu je nástroj pro správu pohodlný a účinný, webový přístup představuje bezpečnostní riziko a by měl být nakonfigurovaný jako bezpečné. Doporučujeme správcům, kteří konfigurují bránu Windows PowerShell Web Accessu pomocí vrstvy zabezpečení dostupné, pravidla ověřování na základě rutiny součástí Windows PowerShell Web Accessu a zabezpečení vrstvy, které jsou k dispozici v webového serveru) Služba IIS) a aplikací třetích stran. Tato dokumentace obsahuje dva příklady nezabezpečeného použití, které doporučujeme pouze pro testovací prostředí, a příklady, které se doporučují pro zabezpečená nasazení.

## <a name="browser-and-client-device-support"></a>Podpora prohlížeče a klientského zařízení

Windows PowerShell Web Accessu podporuje následujících prohlížečů Internet.
Přestože mobilní prohlížeče nejsou oficiálně podporované, mnoho může být možné spouštět webové konzoly Windows Powershellu. Jiné prohlížeče, které používají soubory cookie a umožňují spouštět JavaScript a weby HTTPS, budou pravděpodobně fungovat, ale nejsou oficiálně testované.

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

Použití prostředí Windows PowerShell Web Accessu webové konzoly, postupujte takto prohlížeče.

- Povolit soubory cookie z webu brány Windows PowerShell Web Accessu.
- Je nutné, aby umožňovaly otevírání a čtení stránek HTTPS.
- Je nutné, aby otevíraly a spouštěly weby, které používají JavaScript.

## <a name="recommended-quick-deployment"></a>Doporučujeme rychlé nasazení

Brána Windows PowerShell Web Accessu můžete nainstalovat na serveru, na kterém běží Windows Server 2012 R2 nebo Windows Server 2012 pomocí buď rutin Windows Powershellu nebo pomocí Přidat role a funkce průvodce, která je otevřena z v rámci správce serveru. Pro rychlou instalaci a konfiguraci použijte rutiny prostředí Windows PowerShell, jak je popsáno v této části.

1. [Instalace Windows PowerShell Web Accessu](#install-Windows-powershell-web-access)
1. [Konfigurace brány](#configure-the-gateway)
1. [Konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule)

### <a name="install-windows-powershell-web-access-using-powershell-cmdlets"></a>Instalace Windows PowerShell Web Accessu pomocí rutin prostředí PowerShell

#### <a name="to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets"></a>Postup instalace Windows PowerShell Web Accessu pomocí rutin Windows PowerShellu

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu se zvýšenými uživatelskými právy.
   - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.
   - V Windows **Start** obrazovce, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.

   > **![Poznámka:](images/note.jpeg) Poznámka** v prostředí Windows PowerShell 3.0 a 4.0, je nutné je importovat modul rutin Správce serveru do relace prostředí Windows PowerShell před spuštěním rutin, které jsou součástí daného modulu. Modul je automaticky importován při prvním spuštění rutiny, která je součástí daného modulu. Rutiny prostředí Windows PowerShell nejsou malá a velká písmena.

1. Zadejte následující příkaz a stiskněte klávesu **Enter**, kde *název_počítače* představuje vzdálený počítač, na kterém chcete nainstalovat Windows PowerShell Web Accessu, pokud je k dispozici. Parametr `-Restart` automaticky restartuje cílové servery, pokud je to potřeba.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -IncludeManagementTools -Restart`

   > **![Poznámka:](images/note.jpeg) Poznámka**
   >
   > Instalace Windows PowerShell Web Accessu pomocí rutin prostředí Windows PowerShell nepřidá nástroje pro správu webového serveru (IIS) ve výchozím nastavení. Pokud chcete nainstalovat nástroje pro správu na stejném serveru jako brána Windows PowerShell Web Accessu, přidejte `-IncludeManagementTools` parametr k instalačnímu příkazu (jak je uvedeno v tomto kroku). Pokud spravujete web Windows PowerShell Web Accessu ze vzdáleného počítače, nainstalujte modul snap-in Správce služby IIS nainstalováním [vzdáleného serveru pro správu Toolsfor Windows 8.1](https://www.microsoft.com/en-us/download/details.aspx?id=39296) nebo [vzdálenou správu serveru Nástroje pro systém Windows 8](https://www.microsoft.com/en-us/download/details.aspx?id=28972) na počítači, ze kterého chcete ke správě brány.

   Pokud chcete nainstalovat role a funkce na offline virtuálním pevném disku, musíte přidat parametr `-ComputerName` i parametr `-VHD`. Parametr `-ComputerName` obsahuje název serveru, ke kterému se má připojit virtuální pevný disk. Parametr `-VHD` pak obsahuje cestu k souboru VHD na určeném serveru.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -IncludeManagementTools -Restart`

1. Po dokončení instalace ověřte, zda Windows PowerShell Web Accessu byl nainstalován na cílových serverech spuštěním `Get-WindowsFeature` rutiny na cílovém serveru, v konzole Windows Powershellu otevřené se zvýšenými uživatelskými právy. Můžete také ověřit, že Windows PowerShell Web Accessu byl nainstalován do konzoly Správce serveru tak, že vyberete cílový server na **všechny servery** stránky a pak zobrazí **rolí a funkcí** dlaždice pro vybraný server. Můžete také zobrazit soubor readme pro Windows PowerShell Web Accessu.

1. Po instalaci Windows PowerShell Web Accessu, zobrazí se výzva si přečetli soubor readme, který obsahuje pokyny k instalaci základní, se vyžaduje pro bránu. Tyto pokyny k instalaci jsou také v následující části [nakonfigurovat bránu, která](#configure-the-gateway). Cesta k souboru readme je `C:\Windows\Web\PowerShellWebAccess\wwwroot\README.txt`.

### <a name="configure-the-gateway"></a>Konfigurace brány

**Rutiny Install-PswaWebApplication** rutina je rychlý způsob, jak získat Windows PowerShell Web Accessu nakonfigurované. I když můžete do rutiny `Install-PswaWebApplication` přidat parametr `UseTestCertificate` k instalaci certifikátu SSL podepsaného držitelem pro testovací účely, není to bezpečné. Pro bezpečné produkční prostředí vždy používejte platný certifikát SSL, který podepsala certifikační autorita.
Správci mají možnost testovací certifikát nahradit podobným certifikátem, který sami vyberou, pomocí konzoly Správce služby IIS.

Můžete použít Windows PowerShell Web Accessu konfiguraci webové aplikace tak, že spustíte `Install-PswaWebApplication` rutiny nebo uděláte kroky konfigurace založeným na GUI ve Správci služby IIS. Ve výchozím nastavení rutina nainstaluje webovou aplikaci **pswa** (a její fond aplikací, **pswa_pool**) v **výchozí webový server** kontejneru, jak je znázorněno v Správce služby IIS; Pokud Chcete, můžete dát pokyn rutiny změně kontejneru výchozího webu webové aplikace. Správce služby IIS nabízí možnosti konfigurace, které jsou k dispozici pro webové aplikace, jako je například změna číslo portu nebo certifikátu vrstvy SSL (Secure Sockets Layer).

> **![Poznámka k zabezpečení](images/securitynote.jpeg) Poznámka k zabezpečení**
>
> Důrazně doporučujeme, aby správci bránu nakonfigurovali na používání platného certifikátu podepsaného certifikační autoritou.

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-test-certificate-by-using-install-pswawebapplication"></a>Nakonfigurování brány Windows PowerShell Web Accessu s testovacím certifikátem pomocí rutiny Install-PswaWebApplication

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu.

   - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu.

   - V Windows **Start** obrazovce, klikněte na tlačítko **prostředí Windows PowerShell**.

2. Zadejte následující příkaz a stiskněte klávesu **Enter**.

   `Install-PswaWebApplication -UseTestCertificate`

   > **![Poznámka k zabezpečení](images/securitynote.jpeg) Poznámka k zabezpečení**
   >
   > Parametr `UseTestCertificate` by se měl používat jenom v privátním testovacím prostředí. Pro zabezpečené produkční prostředí doporučujeme použít platný certifikát podepsaný certifikační autoritou.

   Spuštěním rutiny se nainstaluje Windows PowerShell Web Accessu webové aplikace v kontejneru výchozí web služby IIS. Rutina vytvoří infrastrukturu požadovanou pro spuštění Windows PowerShell Web Accessu na výchozím webu, `https://<server_name>/pswa`. Pokud chcete webovou aplikaci nainstalovat na jiný web, zadejte jeho název přidáním parametru `WebSiteName`. Pokud chcete změnit název webové aplikace (výchozí je `pswa`), přidejte parametr `WebApplicationName`.

   Spuštěním rutiny se konfiguruje následující nastavení. Pokud chcete, můžete je ručně změnit v konzole Správce služby IIS.

   - Cesta: / pswa
   - ApplicationPool: pswa_pool
   - EnabledProtocols: http
   - PhysicalPath: `%*windir*%/Web/PowerShellWebAccess/wwwroot`

     **Příklad**: `Install-PswaWebApplication -webApplicationName myWebApp -useTestCertificate`

     V tomto příkladu je výsledný web pro Windows PowerShell Web Accessu `https://<server_name>/myWebApp`.

   > **![Poznámka:](images/note.jpeg) Poznámka**
   >
   > Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel. Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule) a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-genuine-certificate-by-using-install-pswawebapplication-and-iis-manager"></a>Nakonfigurování brány Windows PowerShell Web Access s pravým certifikátem pomocí rutiny Install-PswaWebApplication a Správce služby IIS

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu.

   - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu.

   - V Windows **Start** obrazovce, klikněte na tlačítko **prostředí Windows PowerShell**.

2. Zadejte následující příkaz a stiskněte klávesu **Enter**.

   `Install-PswaWebApplication`

   Spuštěním rutiny se konfiguruje následující nastavení brány.
   Pokud chcete, můžete je ručně změnit v konzole Správce služby IIS.
   Můžete také zadat hodnoty parametrů `WebsiteName` a `WebApplicationName` rutiny `Install-PswaWebApplication`.

   - Cesta: / pswa

   - ApplicationPool: pswa_pool

   - EnabledProtocols: http

   - PhysicalPath: `%*windir*%/Web/PowerShellWebAccess/wwwroot`

3. Otevřete konzolu Správce služby IIS některým z následujících postupů.

   - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows. Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.

   - V Windows **Start** obrazovce, klikněte na tlačítko **správce serveru**.

4. V podokně stromu Správce služby IIS rozbalte uzel pro server, na kterém je nainstalovaný Windows PowerShell Web Accessu do **lokality** složka je viditelné. Rozbalte **lokality** složky.

5. Vyberte web, ve kterém jste nainstalovali webovou aplikaci Windows PowerShell Web Accessu. V **akce** podokně klikněte na tlačítko **vazby**.

6. V **vazbu webu** dialogové okno, klikněte na tlačítko **přidat**.

7. V **přidat vazbu webu** v dialogu **typ** pole, vyberte **https**.

8. V **certifikát SSL** vyberte v rozevírací nabídce podepsaný certifikát. Klikněte na **OK**. Zobrazit [nakonfigurovat certifikát SSL ve Správci služby IIS](#to-configure-an-ssl-certificate-in-iis-Manager) v tomto tématu pro další informace o tom, jak získat certifikát.

   Windows PowerShell Web Accessu webové aplikace je nyní nakonfigurováno pro použití podepsaného certifikátu SSL.

   Dostanete tak, že otevřete Windows PowerShell Web Accessu **https://\<název_serveru\>/pswa** v okně prohlížeče.

   > **![Poznámka:](images/note.jpeg) Poznámka**
   >
   > Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel.
   > Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule), v tomto tématu a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configure-a-restrictive-authorization-rule"></a>Konfigurace omezujícího autorizačního pravidla

Po nainstalování Windows PowerShell Web Accessu a je brána nakonfigurovaná, uživatelé mohou otevřít přihlašovací stránku v prohlížeči, ale nemůže přihlásit do správce Windows PowerShell Web Accessu explicitně neudělí přístup. Řízení přístupu na Windows PowerShell Web Accessu se spravuje pomocí sady rutin Windows Powershellu jsou popsané v následující tabulce. Neexistuje žádné srovnatelné grafické uživatelské rozhraní pro přidávání nebo správu autorizačních pravidel. Podrobné informace o rutinách Windows PowerShell Web Accessu, naleznete v tématu referenční témata rutiny [rutiny Windows Powershellu webového přístupu](cmdlets/web-access-cmdlets.md).

Podrobnější informace o Windows PowerShell Web Accessu autorizačních pravidel a zabezpečení, najdete v části [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-add-a-restrictive-authorization-rule"></a>Přidání omezujícího autorizačního pravidla

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu se zvýšenými uživatelskými právy.

   - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.

   - V Windows **Start** obrazovce, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.

2. Volitelný krok pro omezení přístupu uživatelů s použitím konfigurací relace: Ověřte, že konfigurace relace, které chcete použít v pravidlech již existují. V případě, že jste ještě nevytvořili, postupujte podle pokynů pro vytvoření konfigurací relace v [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configurations).

3. Zadejte následující příkaz a stiskněte klávesu **Enter**.

   `Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>`

   Toto autorizační pravidlo umožňuje konkrétní přístup uživatele k jednomu počítači v síti, ke kterému mají obvykle přístup, včetně přístupu ke konfiguraci konkrétní relace, které působí na typické skriptování uživatele a je třeba rutina.

   V následujícím příkladu se uživateli se jménem `JSmith` v doméně `Contoso` udělí přístup ke správě počítače `Contoso_214` a použití konfigurace relace s názvem `NewAdminsOnly`.

   `Add-PswaAuthorizationRule -UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly`

4. Ověřte, zda byl vytvořen pravidla buď spuštěním `Get-PswaAuthorizationRule` rutiny, nebo `Test-PswaAuthorizationRule -UserName <domain\user> -ComputerName <computer-name>`

5. Například `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

Po nakonfigurování autorizačního pravidla se můžou Autorizovaní uživatelé přihlásit k webové konzole a začít používat Windows PowerShell Web Accessu.

## <a name="custom-deployment"></a>Vlastní nasazení

Brána Windows PowerShell Web Accessu můžete nainstalovat na serveru, na kterém běží Windows Server 2012 R2 nebo Windows Server 2012 pomocí funkce Průvodce přidáním rolí a ve Správci serveru. Po dokončení instalace Windows PowerShell Web Access můžete přizpůsobit konfiguraci brány ve Správci služby IIS.

### <a name="install-windows-powershell-web-access-using-the-add-roles-and-features-wizard"></a>Instalace Windows PowerShell Web Accessu pomocí funkce Průvodce přidáním rolí a

1. Pokud správce serveru je už otevřená, přejděte k dalšímu kroku. Správce serveru ještě není otevřený, otevřete ho jedním z následujících akcí.

   - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows.

   - V Windows **Start** obrazovce, klikněte na tlačítko **správce serveru**.

2. Na **spravovat** nabídky, klikněte na tlačítko **přidat role a funkce**.

3. Na **vybrat typ instalace** stránce **instalace na základě rolí nebo na základě funkcí**. Klikněte na **Další**.

4. Na **vybrat cílový server** stránky, vyberte server z fondu serverů nebo offline virtuální pevný disk. Pokud chcete jako cílový server zvolit offline virtuální pevný disk, vyberte nejdřív server, ke kterému chcete virtuální pevný disk připojit, a pak vyberte příslušný soubor VHD. Informace o tom, jak přidat servery do fondu serverů najdete v nápovědě k nástroji Server Manager. Po výběru cílového serveru, klikněte na tlačítko **Další**.

5. Na **zvolte funkce, které** stránku průvodce, rozbalte **prostředí Windows PowerShell**a pak vyberte **Windows PowerShell Web Accessu**.

6. Zobrazí se výzva k přidání požadovaných funkcí, jako je rozhraní .NET Framework 4.5 a služby role Webový Server (IIS). Přidejte požadované funkce a pokračujte.

   > **![Poznámka:](images/note.jpeg) Poznámka**
   >
   > Instalace Windows PowerShell Web Accessu pomocí funkce Průvodce přidáním rolí a nainstaluje také webový Server (IIS), včetně modulu snap-in Správce služby IIS. Modul snap-in a jiné nástroje pro správu služby IIS instalují ve výchozím nastavení, pokud použijete Průvodce přidání rolí a funkcí. Pokud instalujete Windows PowerShell Web Accessu pomocí rutin prostředí Windows PowerShell, jak je popsáno v následujícím postupu, nástroje pro správu nepřidají ve výchozím nastavení.

7. Na **potvrdit vybrané možnosti instalace** stránky, pokud soubory funkcí pro Windows PowerShell Web Accessu není uložený na cílovém serveru, který jste vybrali v kroku 4, klikněte na tlačítko **zadejte alternativní zdrojová_cesta_operačního_systému**a zadejte cestu k souborům funkcí. V opačném případě klikněte na tlačítko **nainstalovat**.

8. Po kliknutí na **nainstalovat**, **průběh instalace** stránka zobrazuje průběh instalace, výsledky a zprávy upozornění, chyby nebo kroky konfigurace po instalaci, které jsou vyžaduje se pro Windows PowerShell Web Accessu. Po instalaci Windows PowerShell Web Accessu, zobrazí se výzva si přečetli soubor readme, který obsahuje pokyny k instalaci základní, se vyžaduje pro bránu. Tyto pokyny jsou také uvedené v tomto tématu. Cesta k souboru readme je `C:\Windows\Web\PowerShellWebAccess\wwwroot\README.txt`.

### <a name="configure-the-gateway"></a>Konfigurace brány

Pokyny v této části jsou určené pro instalaci Windows PowerShell Web Accessu webovou aplikaci v podadresáři a ne v kořenovém adresáři vašeho webu. Tento postup je akce v grafickém uživatelském rozhraní ekvivalentní akci, kterou provádí rutina `Install-PswaWebApplication`. Tato část také obsahuje pokyny pro konfiguraci brány Windows PowerShell Web Accessu jako kořenového webu pomocí Správce služby IIS.

#### <a name="to-use-iis-manager-to-configure-the-gateway-in-an-existing-website"></a>Konfigurace brány na stávajícím webu pomocí Správce služby IIS

1. Otevřete konzolu Správce služby IIS některým z následujících postupů.

   - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows. Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.

   - V Windows **Start** zadejte libovolné části názvu **Správce Internetové informační služby (IIS)**. Až se zobrazí, klikněte na zástupce **aplikace** výsledky.

2. Vytvořte nový fond aplikací pro Windows PowerShell Web Accessu. Rozbalte uzel serveru brány ve Správci služby IIS podokně stromu vyberte **fondy aplikací**a klikněte na tlačítko **přidat fond aplikací** v **akce** podokně.

3. Přidat nový fond aplikací s názvem **pswa_pool**, nebo zadejte jiný název. Klikněte na **OK**.

4. V podokně stromu Správce služby IIS rozbalte uzel pro server, na kterém je nainstalovaný Windows PowerShell Web Accessu do **lokality** složka je viditelné. Vyberte **lokality** složky.

5. Klikněte pravým tlačítkem na web (například **výchozí webový server**) do které chcete přidat web Windows PowerShell Web Accessu a potom klikněte na **přidat aplikaci**.

6. V **Alias** pole, zadejte pswa nebo uveďte jiný alias. Z aliasu se stane název virtuálního adresáře. Například **pswa** v následující adrese URL označuje alias zadaný v tomto kroku: **https://\<název serveru\>/pswa**.

7. V **fond aplikací** vyberte fond aplikací, který jste vytvořili v kroku 3.

8. V **fyzická cesta** vyhledejte umístění aplikace. Můžete použít výchozí umístění %windir%/Web/PowerShellWebAccess/wwwroot. Klikněte na **OK**.

9. Postupujte podle kroků v postupu nakonfigurujte certifikát protokolu SSL ve službě IIS manager](#to-configure-an-ssl-certificate-in-iis-Manager) v tomto tématu.

10. ![](images/SecurityNote.jpeg) Volitelný krok zabezpečení:

    Web a v podokně stromu, klikněte dvakrát na **nastavení SSL** v podokně obsahu.
    Vyberte **požadovat protokol SSL**a pak v **akce** podokně klikněte na tlačítko **použít**.
    Volitelně **nastavení SSL** podokno, můžete vyžadovat, aby uživatelé připojující se k webu Windows PowerShell Web Accessu měli klientské certifikáty. Klientské certifikáty pomáhají ověřit identitu uživatele klientského zařízení.
    Další informace o tom, jak vyžadování klientských certifikátů můžete zvýšit zabezpečení Windows PowerShell Web Accessu, naleznete v tématu [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md) v této příručce.

11. Otevře relaci prohlížeče v klientském zařízení. Další informace o podporovaných prohlížečích a zařízeních najdete v tématu [prohlížeče a klientského zařízení podporují](#browser-and-client-device-support) v tomto tématu.

12. Otevřete nový web Windows PowerShell Web Accessu **https://\<*název serveru brány*\>/pswa**.

    Prohlížeč by měl zobrazit Windows PowerShell Web Accessu konzoly přihlašovací stránku.

    > **![Poznámka:](images/note.jpeg) Poznámka**
    >
    > Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel.
    > Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule), v tomto tématu a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

13. V relaci Windows Powershellu otevřené se zvýšenými uživatelskými právy (Spustit jako správce) spusťte následující skript, ve kterém *název_fondu_aplikací* představuje název fondu aplikací, kterou jste vytvořili v kroku 3 aby měl fond aplikací přístupová práva k souboru autorizace.

    ```
    $applicationPoolName = "<application_pool_name>"
    $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
    c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null
    ```

    Pokud chcete zobrazit stávající přístupová práva k souboru autorizace, spusťte následující příkaz:

    ```
    c:\windows\system32\icacls.exe $authorizationFile
    ```

#### <a name="to-use-iis-manager-to-configure-the-gateway-as-a-root-website-with-a-test-certificate"></a>Konfigurace brány jako kořenového webu se zkušebním certifikátem pomocí Správce služby IIS

1. Otevřete konzolu Správce služby IIS některým z následujících postupů.

   - Na ploše Windows spusťte Správce serveru klikněte na **správce serveru** na hlavním panelu Windows. Na **nástroje** nabídky ve Správci serveru klikněte na tlačítko **Správce Internetové informační služby (IIS)**.

   - V Windows **Start** zadejte libovolné části názvu **Správce Internetové informační služby (IIS)**. Až se zobrazí, klikněte na zástupce **aplikace** výsledky.

2. V podokně stromu Správce služby IIS rozbalte uzel pro server, na kterém je nainstalovaný Windows PowerShell Web Accessu do **lokality** složka je viditelné. Vyberte **lokality** složky.

3. V **akce** podokně klikněte na tlačítko **přidat web**.

4. Zadejte název webu, například **Windows PowerShell Web Accessu**.

5. Pro nový web se automaticky vytvoří fond aplikací. Pokud chcete použít jiný fond aplikací, klikněte na tlačítko **vyberte** vybrat fond aplikací k přidružení nového webu. Vyberte alternativní fond aplikací v **vybrat fond aplikací** dialogové okno a potom klikněte na **OK**.

6. V **fyzická cesta** text, přejděte na %*windir*% / Web/PowerShellWebAccess/wwwroot.

7. V **typ** pole **vazby** vyberte **https**.

8. Přiřaďte číslo portu webu, který ještě nepoužívá jiný web nebo aplikace. Pokud chcete vyhledat otevřené porty, můžete spustit **netstat** příkazu v okně příkazového řádku. Výchozí číslo portu je 443.

   Pokud už číslo 443 používá jiný web nebo pokud máte jiné bezpečnostní důvody pro změnu čísla portu, změňte výchozí port. Pokud vybraný port používá jiný web, na kterém běží na serveru brány, když kliknete, zobrazí se upozornění **OK** v **přidat web** dialogové okno. Spuštění Windows PowerShell Web Accessu musí použití nepoužitého portu.

9. Volitelně můžete v případě potřeby pro vaši organizaci, zadejte název hostitele, který dává smysl pro vaši organizaci a uživatele, jako například **www.contoso.com**. Klikněte na **OK**.

10. Aby bylo vaše produkční prostředí ještě bezpečnější, rozhodně doporučujeme použít platný certifikát podepsaný certifikační autoritou. Je nutné zadat certifikát SSL, protože uživatelé můžou připojit jenom k Windows PowerShell Web Accessu přes web HTTPS. Zobrazit [nakonfigurovat certifikát SSL ve Správci služby IIS](#to-configure-an-ssl-certificate-in-iis-Manager) v tomto tématu pro další informace o tom, jak získat certifikát.

11. Klikněte na tlačítko **OK** zavřete **přidat web** dialogové okno.

12. Další informace o tom, jak ve webové konzole najdete v tématu *pomocí webové konzoly Powershellu Windows*.

    ```    
    $applicationPoolName = "<application_pool_name>"
    $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
    c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null
    ```

    Pokud chcete zobrazit stávající přístupová práva k souboru autorizace, spusťte následující příkaz:

    ```
    c:\windows\system32\icacls.exe $authorizationFile
    ```

13. Internetová informační služba (IIS) 7.0 dokumentace

14. Otevře relaci prohlížeče v klientském zařízení. Další informace o podporovaných prohlížečích a zařízeních najdete v části [Podpora prohlížeče a klientského zařízení](#browser-and-client-device-support) v tomto dokumentu.

15. Konfigurace zabezpečení webového serveru (IIS 7)

    Vzhledem k tomu, že kořenový web odkazuje na složku Windows PowerShell Web Access, v prohlížeči by se při otevření stránky **https://\<*název_serveru_brány*\>** měla zobrazit přihlašovací stránka. By neměl muset přidat **/pswa** na adresu URL.

    > **![Poznámka:](images/note.jpeg) Poznámka**
    >
    > Není možné se přihlásit, dokud uživatelům nebude udělen přístup na web přidáním autorizačních pravidel.
    > Další informace najdete v tématu [konfigurace omezujícího autorizačního pravidla](#configure-a-restrictive-authorization-rule), v tomto tématu a [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configuring-a-restrictive-authorization-rule"></a>Konfigurace omezujícího autorizačního pravidla

Po nainstalování Windows PowerShell Web Accessu a je brána nakonfigurovaná, uživatelé mohou otevřít přihlašovací stránku v prohlížeči, ale nemůže přihlásit do správce Windows PowerShell Web Accessu explicitně neudělí přístup. Řízení přístupu na Windows PowerShell Web Accessu se spravuje pomocí sady rutin Windows Powershellu jsou popsané v následující tabulce. Neexistuje žádné srovnatelné grafické uživatelské rozhraní pro přidávání nebo správu autorizačních pravidel. Podrobné informace o rutinách Windows PowerShell Web Accessu, naleznete v tématu referenční témata rutiny [rutiny Windows Powershellu webového přístupu](cmdlets/web-access-cmdlets.md).

Podrobnější informace o Windows PowerShell Web Accessu autorizačních pravidel a zabezpečení, najdete v části [autorizačních pravidel a zabezpečení funkce systému Windows PowerShell Web Accessu](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="adding-a-restrictive-authorization-rule"></a>Přidání omezujícího autorizačního pravidla

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu se zvýšenými uživatelskými právy.

   - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.

   - V Windows **Start** obrazovce, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.

2. ![Poznámka k zabezpečení](images/SecurityNote.jpeg) Volitelný krok pro omezení přístupu uživatelů s použitím konfigurací relace:

   Ověřte, že konfigurace relace, které chcete v pravidlech použít, už existují. V případě, že jste ještě nevytvořili, postupujte podle pokynů pro vytvoření konfigurací relace v [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configurations).

3. Zadejte následující příkaz a stiskněte klávesu **Enter**.

   Add-PswaAuthorizationRule - UserName < doména\uživatel | počítač\uživatel > - ComputerName < název_počítače > - ConfigurationName < session_configuration_name >

   Toto autorizační pravidlo umožňuje konkrétní přístup uživatele k jednomu počítači v síti, ke kterým mají obvykle přístup, včetně přístupu ke konfiguraci konkrétní relace, které budou platit pro uživatele "™ potřeby typický skriptování a rutiny s.

   V následujícím příkladu se uživateli se jménem `JSmith` v doméně `Contoso` udělí přístup ke správě počítače `Contoso_214` a použití konfigurace relace s názvem `NewAdminsOnly`.

   Add-PswaAuthorizationRule - UserName "Contoso\jmacek" - ComputerName Contoso_214 - při ConfigurationName NewAdminsOnly

4. Ověřte, zda byl vytvořen pravidla buď spuštěním `Get-PswaAuthorizationRule` rutiny nebo `Test-PswaAuthorizationRule -UserName '<domain\user>' -ComputerName <computer-name>`.

   Například `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

   Po nakonfigurování autorizačního pravidla se můžou Autorizovaní uživatelé přihlásit k webové konzole a začít používat Windows PowerShell Web Accessu.

## <a name="configure-a-genuine-certificate"></a>Konfigurace pravého certifikátu

Aby bylo produkční prostředí zabezpečené, používejte vždy platný certifikát SSL podepsaný certifikační autoritou (CA). Postup v této části uvádí, jak získat a použít platný certifikát SSL od certifikační autority.

### <a name="to-configure-an-ssl-certificate-in-iis-manager"></a>Konfigurace certifikátu SSL ve Správci služby IIS

1. V podokně stromu Správce služby IIS vyberte server, na kterém je nainstalovaný Windows PowerShell Web Accessu.

2. V podokně obsahu poklikejte na **certifikáty serveru**.

3. V **akce** podokno, proveďte jednu z následujících akcí. Další informace o konfiguraci certifikátů serveru ve službě IIS najdete v tématu [konfigurace certifikátů serveru ve službě IIS 7](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732230(v=ws.10)).

   - Klikněte na tlačítko **importovat** k naimportovat stávající platný certifikát z umístění v síti.

   - Klikněte na tlačítko **vytvořit žádost o certifikát** požádat o certifikát od certifikační Autority, jako [VeriSign](http://www.verisign.com/), [Thawte](https://www.thawte.com/), nebo [GeoTrust](https://www.geotrust.com/). Běžný název certifikátu musí odpovídat hlavičce hostitele v žádosti.

   Například, pokud prohlížeč klienta požaduje http://www.contoso.com/, pak musí také být běžný název http://www.contoso.com/. Toto je nejbezpečnější a doporučená možnost poskytnutí brány Windows PowerShell Web Accessu pomocí certifikátu.

   - Klikněte na tlačítko **vytvořit certifikát podepsaný svým držitelem** vytvoření certifikátu můžete použít okamžitě a mají novější podepsaný Certifikační autoritou v případě potřeby. Zadejte popisný název certifikátu podepsaného držitelem, například **Windows PowerShell Web Accessu**. Tato možnost se nepovažuje za bezpečnou a doporučuje se pouze pro privátní testovací prostředí.

4. Po vytvoření nebo získání certifikátu, vyberte web, ke kterému se certifikát používá (například **výchozí webový server**) podokně stromu ve Správci služby IIS a pak klikněte na tlačítko **vazby** v **Akce** podokně.

5. V **přidat vazbu webu** dialogového okna přidejte **https** vazby pro lokalitu, pokud již není zobrazen. Pokud nepoužíváte certifikát podepsaný držitelem, zadejte název hostitele z kroku 3 tohoto postupu. Pokud používáte certifikát podepsaný držitelem, není tento krok povinný.

6. Vyberte certifikát, který jste získali nebo vytvořili v kroku 3 tohoto postupu a potom klikněte na tlačítko **OK**.

## <a name="using-the-web-based-windows-powershell-console"></a>Používání webové konzoly Windows PowerShellu

Po dokončení konfigurace brány, jak je popsáno v tomto tématu je nainstalovaný Windows PowerShell Web Access a webové konzoly Windows Powershellu je připravený k použití. Další informace o tom, jak ve webové konzole najdete v tématu [pomocí webové konzoly Powershellu Windows](use-the-web-based-windows-powershell-console.md).

## <a name="see-also"></a>Viz také

[Internetová informační služba (IIS) 7.0 dokumentace](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753433(v=ws.10))

[Nápověda k aplikaci IIS 7.0 Manager](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732664(v=ws.11))

[Konfigurace zabezpečení webového serveru (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731278(v=ws.10))

[Materiály pro nasazení protokolu IPsec](/previous-versions/windows/it-pro/windows-server-2003/cc776369(v=ws.10))
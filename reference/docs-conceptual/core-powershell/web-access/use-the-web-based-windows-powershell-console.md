---
ms.date: 08/23/2017
keywords: rutiny prostředí PowerShell
title: pomocí webové konzole na základě windows powershellu
ms.openlocfilehash: 2bb9c6ef486ef32012a15f9890997cf2fa6a3a0b
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320648"
---
# <a name="use-the-web-based-windows-powershell-console"></a>Používání webové konzoly Windows PowerShellu

Aktualizace: 24 červen 2013

Platí pro: Windows Server 2012 R2, Windows Server 2012

Windows PowerShell Web Accessu umožňuje uživatelům přihlašovat na zabezpečený web; Chcete-li použít ke správě vzdáleného počítače relace, rutiny a skripty Windows Powershellu.

Protože konzoly Windows Powershellu se spouští ve webovém prohlížeči, můžete otevřít z nejrůznějších klientských zařízení; téměř všechna zařízení s webovým prohlížečem, fungovat.

Webové konzoly Windows Powershellu je cílená na vzdálený počítač, který je určen jako součást procesu přihlášení uživatele.

Toto téma popisuje, jak přihlásit a začít používat webovou konzolu Windows PowerShell Web Accessu.

Toto téma nepopisuje, jak pomocí prostředí Windows PowerShell nebo spouštět rutiny nebo skripty.
Informace o tom, jak pomocí prostředí Windows PowerShell a skriptování prostředků najdete v tématu [viz taky](#see-also) oddílu na konci tohoto tématu.

## <a name="supported-browsers-and-client-devices"></a>Podporované prohlížeče a klientská zařízení

Windows PowerShell Web Accessu podporuje následujících prohlížečů Internet.
Přestože mobilní prohlížeče nejsou oficiálně podporované, mnoho může být možné spouštět webové konzoly Windows Powershellu.
Jiné prohlížeče, které používají soubory cookie a umožňují spouštět JavaScript a weby HTTPS, budou pravděpodobně fungovat, ale nejsou oficiálně testované.

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

## <a name="signing-in-to-windows-powershell-web-access"></a>Přihlášení k funkci Windows PowerShell Web Access

Správce Windows PowerShell Web Accessu by měla poskytnout s adresou URL adresu webu brány Windows PowerShell Web Accessu vaší organizace.
Ve výchozím nastavení, je tato adresa webu *https://\<název_serveru\>/pswa*.

Před přihlášením k Windows PowerShell Web Accessu, ujistěte se, že máte název nebo IP adresu vzdáleného počítače, který chcete spravovat.
Musíte být autorizovaným uživatelem na vzdáleném počítači a vzdálený počítač musí být nakonfigurovaný tak, aby umožňoval vzdálenou správu.
Další informace o konfiguraci počítače povolit vzdálenou správu najdete v tématu [povolení a používání vzdálených příkazů ve Windows Powershellu](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting).

Nejjednodušší způsob konfigurace počítače povolit vzdálenou správu, je spustit **Enable-PSRemoting - force** rutiny na počítači, v relaci Windows Powershellu otevřené se zvýšenými uživatelskými právy (**Spustit jako správce**).

### <a name="to-sign-in-to-windows-powershell-web-access"></a>Přihlášení k funkci Windows PowerShell Web Access

1. Otevřete Windows PowerShell Web Accessu webu v okně internetového prohlížeče nebo karty.

1. Na Windows PowerShell Web Accessu přihlašovací stránku zadejte vaše síťové uživatelské jméno, heslo a název počítače, který chcete spravovat (a na kterém jste autorizovaným uživatelem). Pokud správce Windows PowerShell Web Accessu sdělil, abyste místo názvu počítače použili identifikátor URI pro vlastní web nebo proxy server, vyberte **identifikátor URI připojení** v **typ připojení** pole a pak Zadejte identifikátor URI.

    > ![Poznámka:](images/Note.jpeg) **Poznámka**:
    >
    > - Pokud cílový počítač je v pracovní skupině, zadejte uživatelské jméno a přihlaste se k počítači, použijte následující syntaxi: `<workgroup_name>\<user_name>`
    > - Pokud je cílový počítač server brány, můžete zadat `localhost` v pole název počítače
    > - Pokud cílový počítač je server brány a server brány je v pracovní skupině, musíte použít `<workgroup name>\<user_name>` zaznamenaná v uživatelské jméno. Můžete použít `localhost` v pole název počítače.

1. **Volitelná nastavení připojení** část se týká požadavků na autorizaci vzdáleného počítače, který chcete spravovat. Další informace o parametrech, které jsou ekvivalentem volitelných nastavení připojení najdete v tématu [Enter-PSSession](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enter-pssession) nápovědu k rutině.

    Přihlašovací údaje, které používáte k průchodu přes Windows PowerShell Web Accessu brány jsou obvykle stejné, která rozpoznává vzdálený počítač, který chcete spravovat. Ale pokud chcete používat jiné přihlašovací údaje ke správě vzdáleného počítače, který jste zadali v kroku 2, rozbalte **volitelná nastavení připojení** části a zadat alternativní přihlašovací údaje. Jinak přejděte ke kroku 6.

1. Pokud vlastní konfiguraci relace pro uživatele Windows PowerShell Web Accessu vytvořil správce Windows PowerShell Web Accessu, zadejte název konfigurace relace v **název konfigurace** pole. Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configurations).

1. Zachovat **typ ověřování** nastavena na **výchozí** Pokud jste dostali pokyn postupovat jinak správce Windows PowerShell Web Accessu.

1. Klikněte na tlačítko **přihlášení**.

## <a name="signing-out-and-timing-out"></a>Odhlášení a vypršení časového limitu

Kterýkoli z následujících vás odhlásí webové relace prostředí Windows PowerShell.

- Kliknutím na **Odhlásit** v pravém dolním rohu konzoly. (Pouze systém Windows Server 2012)

- Kliknutím na **Uložit** nebo **ukončovací** v pravém dolním rohu konzoly (jenom Windows Server 2012 R2). Kliknutím na **Uložit** uloží a zavře relaci Windows PowerShell Web Accessu; k relaci později se můžete připojit. Při přihlášení k Windows PowerShell Web Accessu znovu, Windows PowerShell Web Access zobrazí seznam uložených relací. Můžete buď vybrat a znovu připojit k relaci uložené nebo zahájit novou relaci. Maximální povolený počet otevřených relací uživatelů (uložených a aktivních) konfiguruje správce brány.

    Kliknutím na **ukončovací** vás odhlásí relaci Windows PowerShell Web Accessu bez uložení.

- Pokus o přihlášení za účelem správy jiného vzdáleného počítače ve stejné relaci prohlížeče nebo na nové záložce stejné relace prohlížeče. (To neplatí v případě, že server brány se systémem Windows Server 2012 R2 Windows PowerShell Web Accessu a systémem Windows Server 2012 R2 neumožňuje víc uživatelských relací na nových záložkách ve stejné relaci prohlížeče.) Další informace o tom, jak používat více než jednu aktivní relaci na stejném počítači, najdete v části připojení k několika cílovým počítačům současně v [omezení webové konzoly](#limitations-of-the-web-based-console) části tohoto tématu.

- 20 minut nečinnosti v relaci. Správce brány může přizpůsobit časový limit nečinnosti; Další informace najdete v tématu [Správa relací](authorization-rules-and-security-features-of-windows-powershell-web-access.md#session-management).

    - Pokud jsou odpojené od relace ve webové konzole z důvodu chyby sítě nebo jiné neplánovaného vypnutí nebo selhání a nejsou, protože relaci nemusela uzavřít sami, Windows PowerShell Web Accessu relace i nadále běžel, připojený k cíli počítač, dokud nevyprší časový limit na zavřeli na straně klienta. Tento časový limit je ve výchozím nastavení 20 minut a konfiguruje ho správce brány. Relace se odpojí buď po uplynutí výchozích 20 minut, nebo po vypršení časového limitu určeného správcem brány, podle toho, co je kratší.

        Pokud server brány se systémem Windows Server 2012 R2, Windows PowerShell Web Access můžou uživatelé znovu připojit k uloženým relacím později, ale nedají zobrazit ani se uložené relace až po vypršení časového limitu určeného brány má správce vypršelo.

- Zavření okna nebo záložky prohlížeče.

- Vypnutí klientského zařízení, na kterém je prohlížeč spuštěný, nebo jeho odpojení ze sítě.

- Spuštění **ukončovací** příkaz ve webové konzole. Tento příkaz nefunguje, pokud konfigurace relace, ke kterému jste připojeni k je nakonfigurována pro podporu [NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx) režimu, nebo je v omezeném prostředí runspace.

Pokud chcete znovu přihlásit, otevřete Windows PowerShell Web Accessu webovou stránku znovu a přihlaste se pomocí následujících kroků v [přihlášení k Windows PowerShell Web Accessu](#signing-in-to-windows-powershell-web-access) v tomto tématu.

## <a name="differences-in-the-web-based-windows-powershell-console"></a>Rozdíly ve webové konzole Windows PowerShellu

Po přihlášení k Windows PowerShell Web Accessu, webové konzoly Windows Powershellu se otevře v okně prohlížeče nebo karty. Vzhledem k tomu, že konzola je připojená ke vzdálenému počítači, který jste zadali během procesu přihlašování, pouze tyto rutiny Windows Powershellu nebo skriptů, které jsou k dispozici na vzdáleném počítači, je možné v konzole. Tato část popisuje další omezení konzol Windows PowerShell Web Accessu a rozdíly mezi konzolami Windows PowerShell Web Accessu a nainstalovanou **PowerShell.exe** konzoly.

### <a name="functional-disparity-with-powershellexe"></a>Funkční rozdíly s PowerShell.exe

Většina funkcí hostitele prostředí Windows PowerShell je k dispozici ve webové konzole Windows PowerShell Web Accessu, ale některé funkce, které nejsou k dispozici.

- Zobrazí průběh vnořené.

  Windows PowerShell Web Accessu zobrazí průběh grafického uživatelského rozhraní pro rutiny této sestavy průběh, ale se zobrazují jenom informace o průběhu nejvyšší úrovně.

- Úpravy vstupních barev:

  Vstupní barva se nedá změnit (popředí ani pozadí). Styly výstupu, upozornění, komentářů a chybových zpráv se dají změnit spuštěním skriptu.

- PSHostRawUserInterface.

  Windows PowerShell Web Accessu se implementuje přes vzdálenou správu prostředí Windows PowerShell a používá vzdálené prostředí runspace. Windows PowerShell Web Accessu neimplementuje některé metody tohoto rozhraní; třeba jakýkoli příkaz, který zapisuje do konzoly Windows. Příkazy, jako **PowerTab** nebudou fungovat ve Windows PowerShell Web Accessu.

- Funkční klávesy.

  Windows PowerShell Web Accessu nepodporuje některé funkční klávesy v mnoha případech, protože vyhrazení těchto příkazů v prohlížeči.

### <a name="unsupported-shortcut-keys"></a>Nepodporovaná klávesové zkratky

Klíč funkce | Akce
-- | --
Ctrl+C | Ve Windows PowerShell Web Accessu **Ctrl + C** slouží ke zkopírování obsahu v prohlížeči. Konzola nabízí **zrušit** tlačítko a uživatele můžete také použít **kombinace kláves Ctrl + Q** ke zrušení příkazů.
Alt+mezerník, e, l | Posunutí ve vyrovnávací paměti zobrazení
Alt+mezerník, e, f | Hledání textu ve vyrovnávací paměti zobrazení
Alt+mezerník, e, k | Výběr textu, který se má zkopírovat z vyrovnávací paměti zobrazení
Alt+mezerník, e, p | Vložte obsah schránky do konzoly Windows Powershellu
Alt+mezerník, c | Zavřete konzolu prostředí Windows PowerShell
Ctrl+Break | Vynucení zavření okna prostředí Windows PowerShell
Ctrl+Home | Odstranění znaků od začátku aktuálního příkazového řádku
Ctrl+End | Odstranění znaků do konce příkazového řádku
F1 | Přesunutí kurzoru na příkazovém řádku o jeden znak doprava
F2 | Vytvoření nového příkazu zkopírováním vašeho posledního příkazu až do znaku, který zadáte
F3 | Vyplnění příkazového řádku obsahem z posledního příkazového řádku
F4 | Odstranění znaků z pozice kurzoru
F5 | Zpětné procházení historie příkazů. Chcete-li získat přístup k příkazům v historii příkazů ve Windows PowerShell Web Accessu, klikněte na tlačítko **historie** tlačítka ve webové konzole posouvání.
F7 | Interaktivní výběr příkazu z historie příkazů
F8 | Procházení historie se zobrazením příkazů odpovídajících aktuálnímu textu
F9 | Spuštění konkrétního číslovaného příkazu z historie
Page Up | Spuštění prvního příkazu v historii
Page Down | Spuštění posledního příkazu v historii
Alt+F7 | Vymazání seznamu historie příkazů

### <a name="limitations-of-the-web-based-console"></a>Omezení webové konzoly

- Dvěma segmenty směrování

    Se můžete setkat dvěma segmenty směrování (nebo připojení k druhému počítači z prvního připojení) omezení, pokud se pokusíte vytvořit nebo pracovat v nové relaci pomocí Windows PowerShell Web Accessu. Windows PowerShell Web Accessu používá vzdálené prostředí runspace a v současné době **PowerShell.exe** nepodporuje vytvoření vzdáleného připojení k druhému počítači ze vzdáleného prostředí runspace. Pokud při pokusu o připojení k druhému vzdálenému počítači z existujícího připojení s použitím **Enter-PSSession** rutiny, například můžete získat různé chybové zprávy, jako například €œCannot načíst síťové prostředky.

    Aby nedocházelo k chybám dvěma segmenty směrování, by měl správce v síťovém prostředí vaší organizace nakonfigurovat ověřování CredSSP. Další informace o konfiguraci ověřování CredSSP najdete v tématu [ověřování CredSSP druhé směrování vzdálené komunikace](https://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) na webu společnosti Microsoft. Pokud chcete spravovat druhý vzdálený počítač, můžete taky zadat explicitní pověření. Implicitní pověření pravděpodobně neumožní připojení přes další počítač.

- Vzdálená komunikace

    Windows PowerShell Web Accessu používá a má stejná omezení jako Vzdálená relace prostředí Windows PowerShell. Příkazy přímo volající rozhraní API konzoly Windows, třeba ty pro konzolové editory nebo programy textových nabídek, nefungují, protože tyto příkazy nečtou standardní vstupní, výstupní a chybové kanály ani do nich nezapisují. Proto se příkazy, které spouští spustitelný soubor, třeba **notepad.exe**, nebo zobrazit grafické uživatelské rozhraní, jako například `OpenGridView` nebo `ogv`, nebudou fungovat. Toto chování je ovlivněna prostředí Zdá se, že je Windows PowerShell Web Accessu nereaguje na svých rukou.

- Dokončování pomocí tabulátoru

    Dokončování pomocí tabulátoru nefunguje v konfiguraci relace s omezeném prostředí runspace nebo jeden, který je v **NoLanguage** režimu. I když správci můžou relaci nakonfigurovat tak, aby podporovala dokončování pomocí tabulátorů, nedoporučuje se to z bezpečnostních důvodů, protože to může neoprávněným uživatelům odkrýt následující informace.

    - Cesty interního systému souborů

    - Sdílené složky na interních počítačích

    - Proměnné v prostředí runspace

    - Načtené typy nebo obory názvů .NET Framework

    - Proměnné prostředí

- **NoLanguage** relace nebo prostředí runspace s omezeným přístupem

    Uživatelé, kteří se přihlásili k **NoLanguage** konfiguraci relace nebo omezenému prostředí runspace ve Windows PowerShell Web Accessu nelze spustit **ukončovací** příkaz pro ukončení relace. Odhlásit, měli byste kliknout na uživatele **Odhlásit** na stránce konzoly.

- Připojení k několika cílovým počítačům současně:

    Pokud je server brány se systémem Windows Server 2012, Windows PowerShell Web Accessu umožňuje jenom jedno připojení vzdáleného počítače relace prohlížeče; neumožňuje uživatelům přihlásit se jednou a připojit se k několika vzdáleným počítačům samostatných záložkách prohlížeče. Při otevření nové záložky nebo nového okna prohlížeče, Windows PowerShell Web Accessu vás vyzve k odpojení aktuální relace a spusťte novou relaci tak, aby se můžete připojit k nové (nebo stejnému) vzdálenému počítači. Pokud jsou dvě nebo víc samostatných relací pro různé vzdálené počítače, ale funkce v aplikaci Internet Explorer vám umožní vytvořit novou relaci. Chcete-li zahájit novou relaci prohlížeče v Internet Exploreru, stiskněte **ALT**, otevřete **souboru** nabídky a pak vyberte **novou relaci**. Potom otevřete Windows PowerShell Web Accessu webu v nové relaci a přihlaste se k jiného vzdáleného počítače.

    Když brána Windows PowerShell Web Accessu běží na Windows serveru 2012 R2, uživatelé mohou otevřít více připojení ke vzdáleným počítačům na různých záložkách prohlížeče. Pokud chcete otevřít víc než jedno připojení ke vzdálenému počítači pomocí webové konzoly Windows Powershellu, obraťte se na správce brány Windows PowerShell Web Accessu a zjistěte, jestli je tato funkce podporována serverem brány.

- Trvalé relace prostředí Windows PowerShell (obnovení připojení).

    Po vás vypršení časového limitu brány Windows PowerShell Web Accessu je uzavřen vzdálené připojení mezi bránou a cílovým počítačem. Tím se všechny aktuálně probíhající rutiny nebo skripty ukončí. Doporučujeme použít rutinu prostředí Windows PowerShell **– úloha** infrastruktury, když provádíte dlouhotrvající úlohy, takže můžete spouštět úlohy, odpojit se od počítače, se znova připojit později a dál pokračovat v úlohách. Další výhodou používání **– úloha** rutiny je můžete spustit pomocí Windows PowerShell Web Accessu, odhlásit se a potom se znova připojit později tak, že spuštěné Windows PowerShell Web Access nebo jiného hostitele (například prostředí Windows PowerShell Integrované skriptovací prostředí (ISE)).

- Změna velikosti konzoly:

    **PowerShell.exe** okna konzoly můžete dá změnit těmito třemi způsoby.

    - Přetažení a úprava velikosti okna konzoly myší

    - Změna vlastností výšky a šířky pomocí grafického uživatelského rozhraní pro vlastnosti konzoly

    - Změna výšky a šířky oken konzoly pomocí rutiny

        V okně konzoly Windows PowerShell Web Accessu je nakonfigurovat pomocí rutin. V následujícím příkladu uživatel změní šířku konzoly Windows PowerShell Web Accessu **20**.

            $newSize = $Host.UI.RawUI.WindowSize
            $newSize.Width = $newSize.Width - 20

            $oldSize = $Host.UI.RawUI.WindowSize

            $Host.UI.RawUI.WindowSize = $newSize

        Podobným způsobem se dá změnit výška konzoly.

        Další příklady přizpůsobení zobrazení konzoly jsou k dispozici v [Blog týmu Windows PowerShell](https://blogs.msdn.com/b/powershell/).

## <a name="see-also"></a>Viz také

- [Reference k rutinám Windows Powershellu](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
- [Prostředí Windows PowerShell na webu Microsoft TechNet](https://technet.microsoft.com/library/bb978526.aspx)
- [Úložiště centra skriptů TechNet](https://gallery.technet.microsoft.com/scriptcenter)
- [Centrum skriptů – Hey, Scripting Guy!](https://technet.microsoft.com/scriptcenter)
- [Windows PowerShell týmový Blog](https://blogs.msdn.com/b/powershell/)
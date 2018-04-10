---
ms.date: 08/23/2017
keywords: rutiny prostředí PowerShell
title: pomocí webové konzole na bázi windows powershell
ms.openlocfilehash: 3ef2b39279745ffe78fa928247e8a1fb76519ba0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="use-the-web-based-windows-powershell-console"></a>Používání webové konzoly Windows PowerShellu

Aktualizované: Červen 24, 2013

Platí pro: Windows Server 2012 R2, Windows Server 2012

Windows PowerShell Web Access umožňuje uživatelům přihlásit k zabezpečeným webu; Chcete-li použít ke správě vzdáleného počítače relace, rutiny a skripty prostředí Windows PowerShell.

Protože konzolu prostředí Windows PowerShell se spouští ve webovém prohlížeči, můžete ho otevřít z řady různých klientských zařízení; téměř všechna zařízení s webovým prohlížečem fungovat.

Webové konzoly prostředí Windows PowerShell je cílená na vzdálený počítač, který uživatelé určí v rámci procesu přihlášení.

Toto téma popisuje, jak začít používat webové konzole Windows PowerShell Web Access a přihlaste se k.

Toto téma nepopisuje, jak pomocí prostředí Windows PowerShell nebo spouštět rutiny nebo skripty.
Informace o tom, jak pomocí prostředí Windows PowerShell a skriptování prostředků najdete v tématu [v části Viz také](#see-also) na konci tohoto tématu.

## <a name="supported-browsers-and-client-devices"></a>Podporované prohlížeče a klientská zařízení

Windows PowerShell Web Access podporuje následující internetových prohlížečů.
I když mobilní prohlížeče nejsou oficiálně podporované, mnoho může být možné spustit webovou konzolu prostředí Windows PowerShell.
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

Pokud chcete používat webové konzole Windows PowerShell Web Access, postupujte takto prohlížeče.

- Povolit soubory cookie z webu brány Windows PowerShell Web Access.
- Je nutné, aby umožňovaly otevírání a čtení stránek HTTPS.
- Je nutné, aby otevíraly a spouštěly weby, které používají JavaScript.

## <a name="signing-in-to-windows-powershell-web-access"></a>Přihlášení k funkci Windows PowerShell Web Access

Správce Windows PowerShell Web Access by měly poskytnout adresu URL, která je adresa webu brány Windows PowerShell Web Access vaší organizace.
Ve výchozím nastavení, je tato adresa webu *https://\<název_serveru\>/pswa*.

Před přihlášením k funkci Windows PowerShell Web Access, ujistěte se, že máte název nebo IP adresu vzdáleného počítače, který chcete spravovat.
Musíte být autorizovaným uživatelem na vzdáleném počítači a vzdálený počítač musí být nakonfigurovaný tak, aby umožňoval vzdálenou správu.
Další informace o konfiguraci počítače povolit vzdálenou správu najdete v tématu [povolení a používání vzdálených příkazů ve Windows Powershellu](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting).

Nejjednodušším způsobem, jak nakonfigurovat počítač, aby umožňoval vzdálenou správu je spuštění **Enable-PSRemoting - force** rutiny v počítači, v relaci prostředí Windows PowerShell, který otevřené se zvýšenými uživatelskými právy (**Spustit jako správce**).

### <a name="to-sign-in-to-windows-powershell-web-access"></a>Přihlášení k funkci Windows PowerShell Web Access

1. Otevřete web, Windows PowerShell Web Access v okně prohlížeče Internet nebo kartě.

1. Na Windows PowerShell Web Access přihlašovací stránce zadejte vaše síťové uživatelské jméno, heslo a název počítače, který chcete spravovat (a na kterém jste autorizovaným uživatelem). Pokud správce Windows PowerShell Web Access sdělil, abyste místo názvu počítače použili identifikátor URI pro vlastní web nebo proxy server, vyberte **identifikátor URI připojení** v **typ připojení** pole a potom Zadejte identifikátor URI.

    > ![Poznámka:](images/Note.jpeg) **Poznámka**:
    >
    > - Pokud je cílový počítač v pracovní skupině, použijte následující syntaxi zadejte uživatelské jméno a přihlaste se k počítači: `<workgroup_name>\<user_name>`
    > - Pokud cílový počítač je serverem brány, můžete zadat `localhost` v poli Název počítače
    > - Pokud cílový počítač je serverem brány a server brány je v pracovní skupině, musíte použít `<workgroup name>\<user_name>` v uživatelské jméno selhala. Můžete použít `localhost` v poli Název počítače.

1. **Volitelná nastavení připojení** týká požadavků na autorizaci vzdáleného počítače, který chcete spravovat. Další informace o parametrech, které jsou ekvivalentem volitelných nastavení připojení najdete v tématu [Enter-PSSession](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enter-pssession) nápovědu rutiny.

    Přihlašovacích údajů, které používáte k průchodu přes bránu Windows PowerShell Web Access jsou obvykle stejné těmi, která rozpoznává vzdálený počítač, který chcete spravovat. Ale pokud budete chtít použít různé přihlašovací údaje ke správě vzdáleného počítače, který jste zadali v kroku 2, rozbalte **volitelná nastavení připojení** části a zadat alternativní přihlašovací údaje. Jinak přejděte ke kroku 6.

1. Pokud Windows PowerShell Web Access správce vytvoří vlastní konfiguraci relace pro uživatele Windows PowerShell Web Access, zadejte název název konfigurace relace ve **název konfigurace** pole. Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_session_configurations).

1. Zachovat **typ ověřování** nastavena na **výchozí** Pokud jste dostali pokyn správce Windows PowerShell Web Access neurčí jinak.

1. Klikněte na tlačítko **přihlášení**.

## <a name="signing-out-and-timing-out"></a>Odhlášení a vypršení časového limitu

Některé z následujících odhlášení z webové relace prostředí Windows PowerShell.

- Kliknutím na tlačítko **Odhlásit se** v pravém dolním rohu konzoly. (Pouze systém Windows Server 2012)

- Kliknutím na tlačítko **Uložit** nebo **ukončení** v pravém dolním rohu konzoly (jenom Windows Server 2012 R2). Kliknutím na tlačítko **Uložit** uloží a zavře relaci Windows PowerShell Web Access; je možné znovu připojit k relaci později. Při přihlášení do Windows PowerShell Web Access znovu, Windows PowerShell Web Access zobrazí seznam uložených relací. Můžete buď vybrat a znovu se připojte k relaci uložené nebo zahájit novou relaci. Maximální povolený počet otevřených relací uživatelů (uložených a aktivních) konfiguruje správce brány.

    Kliknutím na tlačítko **ukončení** vás odhlásí relaci Windows PowerShell Web Access bez uložení.

- Pokus o přihlášení za účelem správy jiného vzdáleného počítače ve stejné relaci prohlížeče nebo na nové záložce stejné relace prohlížeče. (Toto není platné, pokud server brány se systémem Windows Server 2012 R2; Windows PowerShell Web Access v systému Windows Server 2012 R2 povolí víc uživatelských relací na nových záložkách ve stejné relaci prohlížeče.) Další informace o tom, jak používat více než jeden aktivní relace na stejném počítači, najdete v části připojení k několika cílovým počítačům současně v [omezení webové konzoly](#limitations-of-the-web-based-console) části tohoto tématu.

- 20 minut nečinnosti v relaci. Správce brány může přizpůsobit časový limit nečinnosti; Další informace najdete v tématu [Správa relací](authorization-rules-and-security-features-of-windows-powershell-web-access.md#session-management).

    - Pokud jsou odpojení z relace ve webové konzole z důvodu chyby sítě nebo jiné neplánovaného vypnutí nebo selhání, a ne kvůli tomu uzavření relace sami, Windows PowerShell Web Access relaci stále běží, připojené k cílovým počítač, dokud nevyprší časový limit na straně klienta. Tento časový limit je ve výchozím nastavení 20 minut a konfiguruje ho správce brány. Relace se odpojí buď po uplynutí výchozích 20 minut, nebo po vypršení časového limitu určeného správcem brány, podle toho, co je kratší.

        Pokud server brány se systémem Windows Server 2012 R2, Windows PowerShell Web Access umožňuje uživatelům znovu připojit k uloženým relacím později, ale nedají zobrazit ani se znovu připojit k uložených relací až po vypršení časového limitu určeného bránu má správce vypršelo.

- Zavření okna nebo záložky prohlížeče.

- Vypnutí klientského zařízení, na kterém je prohlížeč spuštěný, nebo jeho odpojení ze sítě.

- Spuštění **ukončení** příkazu ve webové konzole. Tento příkaz nefunguje, pokud konfigurace relace, ke které jste připojeni k podpoře je nakonfigurované [NoLanguage](https://msdn.microsoft.com/library/windows/desktop/system.management.automation.pslanguagemode.aspx) režimu, nebo je v omezeném prostředí runspace.

Pokud chcete se znovu přihlásit, znovu otevřete Windows PowerShell Web Access webové stránky a přihlaste se pomocí následujících kroků v [přihlášení k Windows PowerShell Web Access](#signing-in-to-windows-powershell-web-access) v tomto tématu.

## <a name="differences-in-the-web-based-windows-powershell-console"></a>Rozdíly ve webové konzole Windows PowerShellu

Po přihlášení k Windows PowerShell Web Access, webové konzoly prostředí Windows PowerShell otevře v okně prohlížeče nebo tab. Protože konzole je připojen ke vzdálenému počítači, který jste zadali během procesu přihlášení, může v konzole použit pouze rutiny prostředí Windows PowerShell nebo skripty, které jsou k dispozici na vzdáleném počítači. Tato část popisuje další omezení konzol Windows PowerShell Web Access a rozdíly mezi konzoly Windows PowerShell Web Access a nainstalovanou **PowerShell.exe** konzoly.

### <a name="functional-disparity-with-powershellexe"></a>Funkční rozdíly s PowerShell.exe

Většina funkcí hostitele prostředí Windows PowerShell je dostupná ve webové konzole Windows PowerShell Web Access, ale některé funkce, které nejsou k dispozici.

- Zobrazí se průběh vnořené.

  Windows PowerShell Web Access zobrazí průběh grafického uživatelského rozhraní pro rutiny průběh této sestavy, které se zobrazují jenom informace o průběhu nejvyšší úrovně.

- Úpravy vstupních barev:

  Vstupní barva se nedá změnit (popředí ani pozadí). Styly výstupu, upozornění, komentářů a chybových zpráv se dají změnit spuštěním skriptu.

- PSHostRawUserInterface.

  Windows PowerShell Web Access se implementuje přes vzdálenou správu prostředí Windows PowerShell a používá vzdálené prostředí runspace. Windows PowerShell Web Access neimplementuje některé metody tohoto rozhraní; například všechny příkaz, který zapisuje do konzoly Windows. Příkazy, jako **PowerTab** nejsou funkční v systému Windows PowerShell Web Access.

- Funkční klávesy.

  Windows PowerShell Web Access nepodporuje některé funkční klávesy, v řadě případů, protože vyhrazení těchto příkazů v prohlížeči.

### <a name="unsupported-shortcut-keys"></a>Nepodporované klávesové zkratky

Klíč – funkce | Akce
-- | --
Ctrl+C | V systému Windows PowerShell Web Access **Ctrl + C** slouží ke kopírování obsahu v prohlížeči. Konzola nabízí **zrušit** tlačítko a uživatele můžete také použít **kombinace kláves Ctrl + Q** ke zrušení příkazů.
Alt+mezerník, e, l | Posunutí ve vyrovnávací paměti zobrazení
Alt+mezerník, e, f | Hledání textu ve vyrovnávací paměti zobrazení
Alt+mezerník, e, k | Výběr textu, který se má zkopírovat z vyrovnávací paměti zobrazení
Alt+mezerník, e, p | Vložit obsah schránky do konzoly prostředí Windows PowerShell
Alt+mezerník, c | Zavřete konzolu prostředí Windows PowerShell
Ctrl+Break | Vynucení zavření okna prostředí Windows PowerShell
Ctrl+Home | Odstranění znaků od začátku aktuálního příkazového řádku
Ctrl+End | Odstranění znaků do konce příkazového řádku
F1 | Přesunutí kurzoru na příkazovém řádku o jeden znak doprava
F2 | Vytvoření nového příkazu zkopírováním vašeho posledního příkazu až do znaku, který zadáte
F3 | Vyplnění příkazového řádku obsahem z posledního příkazového řádku
F4 | Odstranění znaků z pozice kurzoru
F5 | Zpětné procházení historie příkazů. Chcete-li získat přístup k příkazům v historii příkazů ve Windows PowerShell Web Access, klikněte na tlačítko **historie** posuňte tlačítka ve webové konzole.
F7 | Interaktivní výběr příkazu z historie příkazů
F8 | Procházení historie se zobrazením příkazů odpovídajících aktuálnímu textu
F9 | Spuštění konkrétního číslovaného příkazu z historie
Page Up | Spuštění prvního příkazu v historii
Page Down | Spuštění posledního příkazu v historii
Alt+F7 | Vymazání seznamu historie příkazů

### <a name="limitations-of-the-web-based-console"></a>Omezení webové konzoly

- Dvěma segmenty směrování

    Se můžete setkat dvěma segmenty směrování (neboli připojení k druhému počítači z prvního připojení) omezení, pokud se pokusíte vytvořit nebo pracovat v nové relaci pomocí Windows PowerShell Web Access. Windows PowerShell Web Access používá vzdálené prostředí runspace a v současné době **PowerShell.exe** nepodporuje vytvoření vzdáleného připojení k druhému počítači ze vzdáleného prostředí runspace. Pokud se pokusíte připojit k druhému vzdálenému počítači z existujícího připojení pomocí **Enter-PSSession** rutiny, například můžete získat různé chybové zprávy, jako například €œCannot načíst síťové prostředky.

    Abyste se vyhnuli chybám dvěma segmenty směrování, by měl váš správce nakonfigurovat ověřování CredSSP v prostředí sítě vaší organizace. Další informace o konfiguraci ověřování CredSSP najdete v tématu [CredSSP pro vzdálenou komunikaci sekundu směrování](http://blogs.msdn.com/b/powershell/archive/2008/06/05/credssp-for-second-hop-remoting-part-i-domain-account.aspx) na webu společnosti Microsoft. Pokud chcete spravovat druhý vzdálený počítač, můžete taky zadat explicitní pověření. Implicitní pověření pravděpodobně neumožní připojení přes další počítač.

- Vzdálená komunikace

    Windows PowerShell Web Access používá a má stejná omezení jako Vzdálená relace prostředí Windows PowerShell. Příkazy přímo volající rozhraní API konzoly Windows, třeba ty pro konzolové editory nebo programy textových nabídek, nefungují, protože tyto příkazy nečtou standardní vstupní, výstupní a chybové kanály ani do nich nezapisují. Proto příkazy, které spouští spustitelný soubor, třeba **notepad.exe**, nebo zobrazit grafickým uživatelským rozhraním, jako například `OpenGridView` nebo `ogv`, nefungují. Prostředí je ovlivňován toto chování; pro vás zdá se, že Windows PowerShell Web Access neodpovídá do příkazu.

- Dokončování pomocí tabulátorů

    Dokončování pomocí tabulátorů nefunguje v konfiguraci relace s omezeném prostředí runspace nebo jeden, který je v **NoLanguage** režimu. I když správci můžou relaci nakonfigurovat tak, aby podporovala dokončování pomocí tabulátorů, nedoporučuje se to z bezpečnostních důvodů, protože to může neoprávněným uživatelům odkrýt následující informace.

    - Cesty interního systému souborů

    - Sdílené složky na interních počítačích

    - Proměnné v prostředí runspace

    - Načtené typy nebo obory názvů .NET Framework

    - Proměnné prostředí

- **NoLanguage** relace nebo prostředí runspace s omezeným přístupem

    Uživatelé, kteří se přihlásili k **NoLanguage** konfiguraci relace nebo omezenému prostředí runspace ve Windows PowerShell Web Access nelze spustit **ukončení** příkaz k ukončení relace. Chcete-li odhlásit, měli uživatelé kliknout na **Odhlásit** na stránce konzoly.

- Připojení k několika cílovým počítačům současně:

    Pokud je server brány se systémem Windows Server 2012, Windows PowerShell Web Access umožňuje pouze jedno připojení vzdáleného počítače relace prohlížeče; neumožňuje uživatelům přihlásit se jednou a připojit k několika vzdálených počítačů pomocí samostatných záložkách prohlížeče. Při otevření nové záložky nebo nového okna prohlížeče, Windows PowerShell Web Access vás vyzve k odpojení aktuální relace a zahájit novou relaci, aby mohla připojit k nové (nebo stejnému) vzdálenému počítači. V případě potřeby dvou nebo víc samostatných relací pro různé vzdálené počítače jsou však funkce v Internet Exploreru umožňuje vytvořit novou relaci. Chcete-li zahájit novou relaci prohlížeče v Internet Exploreru, stiskněte **ALT**, otevřete **soubor** nabídce a potom vyberte **novou relaci**. Pak otevřít web, Windows PowerShell Web Access v nové relaci a přihlaste se k jiného vzdáleného počítače.

    Pokud brána Windows PowerShell Web Access běží na Windows Server 2012 R2, mohou uživatelé otevřít víc připojení ke vzdáleným počítačům na různých záložkách prohlížeče. Pokud chcete otevřít víc než jedno připojení ke vzdálenému počítači pomocí webové konzoly prostředí Windows PowerShell, zkontrolujte se na správce brány Windows PowerShell Web Access a zjistěte, zda tato funkce je podporovaná serverem brány.

- Trvalé relace prostředí Windows PowerShell (obnovení připojení).

    Po můžete vypršení časového limitu brány Windows PowerShell Web Access je zavřený vzdálené připojení mezi bránou a cílovým počítačem. Tím se všechny aktuálně probíhající rutiny nebo skripty ukončí. Doporučujeme použít prostředí Windows PowerShell **-úlohy** infrastruktury, když provádíte dlouhotrvající úlohy, aby mohli spouštět úlohy, odpojit se od počítače, později připojit a dál pokračovat v úlohách. Další výhodou používání **-úlohy** rutiny je můžete spustit pomocí Windows PowerShell Web Access, odhlásit se a znovu připojit později, spuštěný Windows PowerShell Web Access nebo jiného hostitele (například prostředí Windows PowerShell Integrované skriptovací prostředí (ISE)).

- Změna velikosti konzoly:

    **PowerShell.exe** okna konzoly můžete změnit následující tři způsoby.

    - Přetažení a úprava velikosti okna konzoly myší

    - Změna vlastností výšky a šířky pomocí grafického uživatelského rozhraní pro vlastnosti konzoly

    - Změna výšky a šířky oken konzoly pomocí rutiny

        V okně konzoly pro Windows PowerShell Web Access lze nakonfigurovat pomocí rutin. V následujícím příkladu uživatel změní šířku konzoly Windows PowerShell Web Access **20**.

            $newSize = $Host.UI.RawUI.WindowSize
            $newSize.Width = $newSize.Width - 20

            $oldSize = $Host.UI.RawUI.WindowSize

            $Host.UI.RawUI.WindowSize = $newSize

        Podobným způsobem se dá změnit výška konzoly.

        Další příklady přizpůsobení zobrazení konzoly jsou k dispozici v [blogu týmu Windows PowerShell](http://blogs.msdn.com/b/powershell/).

## <a name="see-also"></a>Viz také

- [Referenční informace o rutinách Windows Powershellu](https://technet.microsoft.com/library/ee407531(ws.10).aspx)
- [Prostředí Windows PowerShell na webu Microsoft TechNet](https://technet.microsoft.com/library/bb978526.aspx)
- [Úložiště centra skriptů na webu TechNet](http://gallery.technet.microsoft.com/scriptcenter)
- [Centrum skriptů – Hey, Scripting Guy!](https://technet.microsoft.com/scriptcenter)
- [Windows PowerShell Team Blog](http://blogs.msdn.com/b/powershell/)
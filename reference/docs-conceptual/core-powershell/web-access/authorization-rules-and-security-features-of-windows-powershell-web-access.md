---
ms.date: 06/27/2017
keywords: rutiny prostředí PowerShell
title: Autorizační pravidla a funkce zabezpečení Windows PowerShell Web Accessu
ms.openlocfilehash: e9bed3900263a51b1b8236a3c3430154a5d11886
ms.sourcegitcommit: 31a221d982305c7f999b1afeb15e3629e9620de8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/10/2018
ms.locfileid: "43133851"
---
# <a name="authorization-rules-and-security-features-of-windows-powershell-web-access"></a>Autorizační pravidla a funkce zabezpečení Windows PowerShell Web Accessu

Aktualizace: 24 červen 2013

Platí pro: Windows Server 2012 R2, Windows Server 2012

Windows PowerShell Web Access v systému Windows Server 2012 R2 a Windows Server 2012 je omezující model zabezpečení. Uživatelé musí mít explicitně udělený přístup předtím, než mohou přihlásit k bráně Windows PowerShell Web Accessu a pomocí webové konzoly Windows Powershellu.

## <a name="configuring-authorization-rules-and-site-security"></a>Konfigurace autorizačních pravidel a zabezpečení lokality

Po nainstalování Windows PowerShell Web Accessu a je brána nakonfigurovaná, uživatelé mohou otevřít přihlašovací stránku v prohlížeči, ale nemůže přihlásit do správce Windows PowerShell Web Accessu explicitně neudělí přístup. Řízení přístupu: Windows PowerShell Web Access"se spravuje pomocí sady rutin Windows Powershellu jsou popsané v následující tabulce. Neexistuje žádné srovnatelné grafické uživatelské rozhraní pro přidávání nebo správu autorizačních pravidel.
Zobrazit [Windows PowerShell Web Access rutiny](cmdlets/web-access-cmdlets.md).

Správci můžou určit `{0-n}` pravidla ověřování pro Windows PowerShell Web Accessu. Výchozí zabezpečení je víc omezující než povolující, nulový počet ověřovacích pravidel znamená, že uživatelé nemají k ničemu přístup.

[Add-PswaAuthorizationRule](cmdlets/add-pswaauthorizationrule.md) a [Test-PswaAuthorizationRule](cmdlets/test-pswaauthorizationrule.md) ve Windows serveru 2012 R2 obsahují parametr Credential, který umožňuje přidat a otestovat autorizační pravidla Windows PowerShell Web Accessu ze vzdálené počítače, nebo z v rámci aktivní relaci Windows PowerShell Web Accessu. Jako s jinými rutinami prostředí Windows PowerShell, které mají parametr Credential, můžete zadat objekt PSCredential jako hodnotu parametru. Chcete-li vytvořit objekt PSCredential obsahující přihlašovací údaje, které chcete předat do vzdáleného počítače, spusťte [Get-Credential](/powershell/module/microsoft.powershell.security/Get-Credential) rutiny.

Pravidla ověřování Windows PowerShell Web Accessu jsou povolená pravidla. Každé pravidlo je definicí povolených připojení mezi uživateli, cílové počítače a konkrétní PowerShellÂ Windows [konfiguracím relací](/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) (také označuje jako koncové body nebo _prostředí runspace_) na zadaných cílových počítačích.
Vysvětlení na **prostředí runspace** naleznete v tématu [začátek pomocí prostředí PowerShell prostředí runspace](https://blogs.technet.microsoft.com/heyscriptingguy/2015/11/26/beginning-use-of-powershell-runspaces-part-1/)

> [!IMPORTANT]
> Aby uživatel získal přístup, stačí, aby platilo jedno pravidlo. Pokud má uživatel přístup k jednomu počítači s úplným jazykovým přístupem nebo přístup jenom k rutinám vzdálené správy Windows Powershellu z webové konzoly, uživatel může přihlásit (nebo směrování) do jiných počítačů, které jsou připojené k prvnímu cílovému počítači. Nejbezpečnější způsob konfigurace Windows PowerShell Web Accessu je povolit uživatelům přístup jenom k omezeným konfiguracím relací, které jim umožní splnit konkrétní úlohy, které obvykle musí provádět vzdáleně.

Rutiny odkazuje [rutiny Windows Powershellu webového přístupu](cmdlets/web-access-cmdlets.md) umožňují vytvořit pravidla přístupu, které se používají k autorizaci uživatele v bráně Windows PowerShell Web Accessu. Pravidla se liší od seznamů ACL v cílovém počítači a poskytují další vrstvu zabezpečení webového přístupu. Další informace o zabezpečení jsou popsané v následující části.

Pokud uživatelé nemůžou projít žádnou z předchozích vrstev, dostanou obecný "přístup byl odepřen' zpráva v okně prohlížeče. I když se podrobnosti zabezpečení protokolují na serveru brány, koncoví uživatelé nevidí informace o tom, kolika vrstvami zabezpečení prošli a ve které vrstvě došlo k chybě přihlášení nebo ověření.

Další informace o konfiguraci autorizačních pravidel najdete v tématu [konfigurace autorizačních pravidel](#configuring-authorization-rules-and-site-security) v tomto tématu.

### <a name="security"></a>Zabezpečení

Model zabezpečení Windows PowerShell Web Accessu má mezi koncovým webové konzoly a cílovým počítače čtyři vrstvy. Windows PowerShell Web Accessu správci mohou přidávat další vrstvy zabezpečení prostřednictvím další konfigurace v konzole Správce služby IIS. Další informace o zabezpečení webů v konzole Správce služby IIS najdete v tématu [konfigurace zabezpečení webového serveru (IIS7)](https://technet.microsoft.com/library/cc731278).

Další informace o službě IIS osvědčené postupy a prevence útoků s cílem odepření služeb, naleznete v tématu [osvědčené postupy pro předcházení útokům na dostupnost služby](https://technet.microsoft.com/library/cc750213).
Správce může taky koupit a nainstalovat další maloobchodní software pro ověřování.

Následující tabulka popisuje čtyři vrstvy zabezpečení mezi koncovými uživateli a cílovými počítači.

|Úroveň|Vrstva|
|-|-|
|1|[funkce zabezpečení webového serveru služby IIS](#iis-web-server-security-features)|
|2|[ověřování založené na formulářích brány přístup webové prostředí powershell systému Windows](#windows-powershell-web-access-forms-based-gateway-authentication)|
|3|[Windows powershell web access autorizační pravidla](#windows-powershell-web-access-authorization-rules)|
|4|[cílové ověřování a autorizační pravidla](#target-authentication-and-authorization-rules)|

Podrobné informace o jednotlivých vrstev najdete v části těchto položek:

#### <a name="iis-web-server-security-features"></a>Funkce zabezpečení webového serveru služby IIS

Uživatelé Windows PowerShell Web Accessu musí vždycky zadat uživatelské jméno a heslo k ověření své účty v bráně. Však správce Windows PowerShell Web Accessu můžete také vypnout volitelné ověření klientského certifikátu na nebo, viz [nainstalovat a používat windows powershell web Accessu](install-and-use-windows-powershell-web-access.md) povolit testovací certifikát a později, jak nakonfigurovat pravého certifikátu).

Volitelná funkce klientského certifikátu vyžaduje, aby koncoví uživatelé měli kromě svých uživatelských jmen a hesel i platný klientský certifikát, a je součástí konfigurace webového serveru (IIS). Pokud je vrstva klientského certifikátu povolená, Windows PowerShell Web Accessu přihlašovací stránku vyzve uživatele před jejich přihlašovací údaje jsou vyhodnocovány poskytnout platné certifikáty. Ověření klientského certifikátu automaticky vyhledává klientský certifikát. Pokud se platný certifikát nenajde, Windows PowerShell Web Accessu informuje uživatele, aby ho mohli poskytnout certifikát. Pokud se najde platný klientský certifikát, Windows PowerShell Web Accessu otevře přihlašovací stránku uživatelé mohli zadat svá uživatelská jména a hesla.

Toto je jeden příklad dalšího nastavení zabezpečení, které nabízí Webový Server služby IIS. Další informace o jiných funkcích zabezpečení služby IIS najdete v tématu [konfigurace zabezpečení webového serveru (IIS 7)](https://technet.microsoft.com/library/cc731278).

#### <a name="windows-powershell-web-access-forms-based-gateway-authentication"></a>Ověřování pomocí formulářů brány Windows PowerShell Web Accessu

Windows PowerShell Web Accessu přihlašovací stránka vyžaduje sadu pověření (uživatelské jméno a heslo) a nabízí uživatelům možnost poskytnout jiná pověření pro cílový počítač.
Pokud uživatel jiná pověření neposkytne, primární uživatelské jméno a heslo použitá pro připojení k bráně se použijí i pro připojení k cílovému počítači.

Požadovaná pověření se ověřují v bráně Windows PowerShell Web Accessu. Tyto přihlašovací údaje musí být platnými uživatelskými účty na buď místní Windows PowerShell Web Accessu serveru brány, nebo ve službě Active Directory.

#### <a name="windows-powershell-web-access-authorization-rules"></a>Windows PowerShell Web Accessu autorizační pravidla

Po ověření uživatele v bráně Windows PowerShell Web Accessu zkontrolujte autorizační pravidla, chcete-li ověřit, jestli má uživatel přístup k požadovanému cílovému počítači. Po úspěšném ověření přihlašovacích údajů uživatele předají do cílového počítače.

Tato pravidla se vyhodnocují jenom po ověření uživatele bránou a před tím, než může dojít k ověření uživatele v cílovém počítači.

#### <a name="target-authentication-and-authorization-rules"></a>Cílové ověřování a autorizační pravidla

Poslední vrstva zabezpečení pro Windows PowerShell Web Access je konfigurace zabezpečení cílového počítače vlastní. Uživatelé musí mít odpovídající přístupová práva nakonfigurovaná v cílovém počítači a také ve Windows PowerShell Web Accessu autorizační pravidla, ke spuštění webové konzole Windows Powershellu, která ovlivňuje cílový počítač prostřednictvím Windows PowerShell Web Accessu.

Tato vrstva nabízí stejné mechanismy zabezpečení, které by vyhodnocovaly pokusy o připojení, pokud se uživatelé pokusili vytvořit vzdálené relace Windows Powershellu k cílovému počítači z v rámci prostředí Windows PowerShell spuštěním [Enter-PSSession](/powershell/module/microsoft.powershell.core/Enter-PSSession) nebo [New-PSSession](/powershell/module/microsoft.powershell.core/new-pssession) rutiny.

Ve výchozím nastavení použije Windows PowerShell Web Accessu primární uživatelské jméno a heslo pro ověřování u brány a cílovým počítačem. Webová přihlašovací stránce v části s názvem **volitelná nastavení připojení**, nabízí uživatelům možnost poskytnout jiná pověření pro cílový počítač, pokud jsou požadována. Pokud uživatel jiná pověření neposkytne, primární uživatelské jméno a heslo použitá pro připojení k bráně se použijí i pro připojení k cílovému počítači.

Autorizační pravidla se dají použít k povolení přístupu uživatelům ke konfiguraci konkrétní relace. Můžete vytvořit _prostředích runspace s omezeným_ nebo konfigurace relace pro Windows PowerShell Web Accessu, a povolit konkrétním uživatelům připojit pouze ke konkrétním konfiguracím relací při přihlášení k Windows PowerShell Web Accessu. Ke zjištění uživatelů, kteří mají přístup ke konkrétním koncovým bodům, můžete použít seznamy řízení přístupu (ACL), a přístup ke koncovému bodu můžete pro konkrétní skupinu uživatelů dál omezit použitím autorizačních pravidel popsaných v této části. Další informace o prostředí runspace s omezeným přístupem najdete v tématu [vytváření omezené prostředí runspace](https://msdn.microsoft.com/library/dn614668).

### <a name="configuring-authorization-rules"></a>Konfigurace autorizačních pravidel

Správci můžou chtít stejné autorizační pravidlo pro Windows PowerShell Web Accessu, kteří již je definována v jejich prostředí pro vzdálenou správu prostředí Windows PowerShell. První postup v této části popisuje, jak přidat pravidlo zabezpečené autorizace udělující přístup jednomu uživateli, přihlašujícímu se ke správě jednoho počítače v rámci konfigurace jedné relace. Druhý postup popisuje, jak odebrat autorizační pravidlo, které už není potřeba.

Pokud budete chtít povolit konkrétním uživatelům práci jenom v omezeném prostředí runspace ve Windows PowerShell Web Accessu pomocí vlastních konfigurací relací, vytvořte vlastní konfigurace relací předtím, než přidáte autorizační pravidla, která na ně odkazují. Rutiny Windows PowerShell Web Accessu nelze použít k vytvoření vlastních konfigurací relací. Další informace o vytváření vlastních konfigurací relací najdete v tématu [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configuration_files).

Rutiny Windows PowerShell Web Accessu podporují jeden zástupný znak – hvězdičku ( \* ). Zástupné znaky uvnitř řetězců se nepodporují. Na jednu položku (uživatele, počítače nebo konfigurace relací) použijte jednu hvězdičku.

> [!NOTE]
> Další způsoby použití autorizačních pravidel k udělení přístupu uživatelům a k zabezpečení prostředí Windows PowerShell Web Accessu, naleznete v části [Další příklady scénářů autorizační pravidlo](#other-authorization-rule-scenario-examples) v tomto tématu.

#### <a name="to-add-a-restrictive-authorization-rule"></a>Přidání omezujícího autorizačního pravidla

1. Proveďte jednu z následujících akcí otevřete relaci Windows Powershellu se zvýšenými uživatelskými právy.

   - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.

   - V Windows **Start** obrazovce, klikněte pravým tlačítkem na **prostředí Windows PowerShell**a potom klikněte na tlačítko **spustit jako správce**.

2. **Volitelný krok** pro omezení přístupu uživatelů s použitím konfigurací relace:

   Ověřte, že konfigurace relace, které chcete použít, už existují v pravidlech.

   V případě, že jste ještě nevytvořili, postupujte podle pokynů pro vytvoření konfigurací relace v [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configuration_files).

3. Toto autorizační pravidlo umožňuje konkrétní přístup uživatele k jednomu počítači v síti, ke kterým mají obvykle přístup, včetně přístupu ke konfiguraci konkrétní relace, které budou platit pro uživatele "™ potřeby typický skriptování a rutiny s. Zadejte následující příkaz a stiskněte klávesu **Enter**.

   ```
   Add-PswaAuthorizationRule -UserName <domain\user | computer\user> `
      -ComputerName <computer_name> -ConfigurationName <session_configuration_name>
   ```

   - V následujícím příkladu, uživateli se jménem _JSmith_ v _Contoso_ domény je udělen přístup ke správě počítače _Contoso_214_a používá konfiguraci relace s názvem _NewAdminsOnly_.

   ```powershell
   Add-PswaAuthorizationRule -UserName 'Contoso\JSmith' `
      -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly
   ```

4. Ověřte, zda byl vytvořen pravidla buď spuštěním **Get-PswaAuthorizationRule** rutiny nebo `Test-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName** <computer_name>`.
   Například `Test-PswaAuthorizationRule -UserName Contoso\\JSmith -ComputerName Contoso_214`.

#### <a name="to-remove-an-authorization-rule"></a>Odebrání autorizačního pravidla

1. Pokud relaci Windows Powershellu ještě není otevřený, najdete v kroku 1 postupu [přidání omezujícího autorizačního pravidla](#to-add-a-restrictive-authorization-rule) v této části.

2. Zadejte následující příkaz a stiskněte klávesu **Enter**, kde *ID pravidla* představuje jedinečné ID číslo pravidla, které chcete odebrat.

   ```
   Remove-PswaAuthorizationRule -ID <rule ID>
   ```

   Pokud ID číslo neznáte, ale znáte popisný název pravidla, které chcete odebrat, můžete použít název pravidla a zřetězit ho do rutiny `Remove-PswaAuthorizationRule` pro odebrání pravidla, jak můžete vidět v následujícím příkladu:

   ```
   Get-PswaAuthorizationRule `
      -RuleName <rule-name> | Remove-PswaAuthorizationRule
   ```

> [!NOTE]
> Zobrazí se výzva k potvrzení odstranění zadaného autorizačního pravidla; Pravidlo se odstraní po stisknutí klávesy **Enter**. Ujistěte se, že chcete odebrat autorizační pravidlo dřív, než spustíte rutinu `Remove-PswaAuthorizationRule`.

#### <a name="other-authorization-rule-scenario-examples"></a>Další příklady scénářů s autorizačními pravidly

Každou relaci prostředí Windows PowerShell používá konfiguraci relace Pokud není zadaná pro relaci, prostředí Windows PowerShell používá výchozí integrovanou konfiguraci relace prostředí Windows PowerShell, se označuje jako Microsoft.PowerShell. Výchozí konfigurace relace zahrnuje všechny rutiny, které jsou v počítači k dispozici. Správci můžou omezit přístup u všech počítačů tak, že definují konfiguraci relace prostředí runspace s omezeným přístupem (omezeným rozsahem rutin a úloh, které jejich koncoví uživatelé můžou provádět). Uživatel, který je udělen přístup k jednomu počítači s úplným jazykovým přístupem nebo jenom Vzdálená správa rutiny prostředí Windows PowerShell můžete připojení k ostatními počítačům, které jsou připojené k prvnímu počítači. Definování omezeném prostředí runspace můžete uživatelům zabránit v přístupu k jiným počítačům z jejich povoleného prostředí runspace prostředí Windows PowerShell a zvyšuje zabezpečení vašeho prostředí Windows PowerShell Web Accessu. Konfigurace relace můžete distribuovat (pomocí zásad skupiny) do všech počítačů, které chtějí správci zpřístupnit prostřednictvím Windows PowerShell Web Accessu. Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx). Toto jsou některé z příkladů tohoto scénáře.

- Správce vytvoří koncový bod, volá **Pswakoncovybod**, s prostředím runspace s omezeným přístupem s. Pak správce vytvoří pravidlo, `*,*,PswaEndpoint`a distribuuje koncový bod na jiné počítače. Toto pravidlo umožňuje všem uživatelům přístup ke všem počítačům s koncovým bodem **Pswakoncovybod**.
  Pokud se jedná o jediné autorizační pravidlo definované v sadě pravidel, nebudou počítače bez tohoto koncového bodu přístupné.

- Volá se na správce vytvořil koncový bod s prostředím runspace s omezeným přístupem s **Pswakoncovybod**a chce omezit přístup pro určité uživatele. Správce vytvoří skupinu uživatelů s názvem **podporauroven1**a definuje následující pravidlo: **podporauroven1,\*, Pswakoncovybod**. Pravidlo udělí všem uživatelům ve skupině **podporauroven1** přístup ke všem počítačům s **Pswakoncovybod** konfigurace. Podobně se dá omezit přístup ke konkrétní sadě počítačů.

- Někteří správci poskytují určitým uživatelům širší přístup než jiným. Správce například vytvoří dvě skupiny uživatelů **správci** a **Zakladnipodpora**. Správce taky vytvoří koncový bod s prostředím runspace s omezeným přístupem volána s **Pswakoncovybod**a definuje následující dvě pravidla: **Admins,\*,\***  a  **Zakladnipodpora,\*, Pswakoncovybod**. První pravidlo poskytuje všem uživatelům v **správce** skupiny přístup k počítačům a druhé pravidlo poskytuje všem uživatelům v **Zakladnipodpora** přístup jenom k těm počítačům s  **Pswakoncovybod**.

- Správce nastavil privátní testovací prostředí a chce umožnit všem oprávněným uživatelům v síti přístup ke všem počítačům v síti, ke kterým mají obvykle přístup, včetně přístupu ke všem konfiguracím relace, ke kterým obvykle přistupují. Protože se jedná o privátní testovací prostředí, správce vytvoří autorizační pravidlo, které není zabezpečené. – Správce spustí rutinu `Add-PswaAuthorizationRule * * *`, která používá zástupný znak **\*** k reprezentaci všech uživatelů, všech počítačů a všechny konfigurace. -Toto pravidlo je ekvivalentem tohoto: `Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *`.

  > [!NOTE]
  > Toto pravidlo se nedoporučuje v zabezpečeném prostředí a obchází vrstvu autorizační pravidlo zabezpečení poskytované službou Windows PowerShell Web Accessu.

- Správce musí povolit uživatelům, aby se mohli připojovat k cílovým počítačům v prostředí, které obsahuje pracovní skupiny a domény, kde se počítače pracovních skupin občas používají pro připojení k cílovým počítačům v doménách a počítače v doménách se příležitostně používají pro připojení k cílovým počítačům v pracovních skupinách. Správce má server brány, *PswaServer*, v pracovní skupině a cílový počítač *srv1.contoso.com* v doméně. Uživatel *Chris* je oprávněný místní uživatel na serveru brány pracovní skupiny a cílovým počítačem. Jeho uživatelské jméno na serveru pracovní skupiny je *Janlocal*; a jeho uživatelské jméno v cílovém počítači je *contoso\\chris*. Správce přidá následující pravidlo, aby Janovi autorizoval přístup k srv1.contoso.com.

```powershell
Add-PswaAuthorizationRule -userName PswaServer\chrisLocal `
   -computerName srv1.contoso.com -configurationName Microsoft.PowerShell
```

Předchozí příklad pravidla ověřuje Jana na serveru brány a potom autorizuje jeho přístup k *srv1*. Na stránce přihlášení musí Jan zadat druhou sadu pověření v **volitelná nastavení připojení** oblasti (*contoso\\chris*). Server brány použije další sadu pověření k jeho ověření v cílovém počítači *srv1.contoso.com*.

V předchozím scénáři Windows PowerShell Web Accessu vytvoří úspěšné připojení k cílovému počítači pouze po následující byly úspěšné a povolení aspoň jedním autorizačním pravidlem.

1. Ověřování na serveru brány pracovní skupiny přidáním uživatelského jména ve formátu *název_serveru*\\*uživatelské_jméno* do ověřovacího pravidla

2. Ověřování v cílovém počítači pomocí alternativních přihlašovacích údajů, které jsou součástí na stránce přihlášení **volitelná nastavení připojení** oblasti

   > [!NOTE]
   > Pokud jsou brána a cílové počítače v různých pracovních skupinách nebo doménách, musí se mezi těmito dvěma počítači pracovních skupin, dvěma doménami nebo pracovní skupinou a doménou vytvořit vztah důvěryhodnosti. Tento vztah se nedá nakonfigurovat pomocí rutin Windows PowerShell Web Accessu autorizačních pravidel. Autorizační pravidla nedefinují vztah důvěryhodnosti mezi počítači. Jenom autorizují uživatele, aby se mohli připojit ke konkrétním cílovým počítačům a konfiguracím relací. Další informace o tom, jak nakonfigurovat vztah důvěryhodnosti mezi různými doménami, najdete v části [vytváření domény a vztahy důvěryhodnosti doménové struktury](https://technet.microsoft.com/library/cc794775.aspx).
   > Další informace o tom, jak přidat do seznamu důvěryhodných hostitelů počítače v pracovních skupinách najdete v tématu [vzdálené správy přes správce serveru](https://technet.microsoft.com/library/dd759202.aspx).

### <a name="using-a-single-set-of-authorization-rules-for-multiple-sites"></a>Použití jedné sady autorizačních pravidel pro víc lokalit

Autorizační pravidla jsou uložená v souboru XML. Ve výchozím nastavení, je název cesty souboru XML `%windir%\Web\PowershellWebAccess\data\AuthorizationRules.xml`.

Cesta k souboru XML pravidla autorizace je uložena v **powwa.config** soubor, který se nachází v `%windir%\Web\PowershellWebAccess\data`. Správce musí změnit odkaz na výchozí cestu v **powwa.config** tak, aby odpovídala nebo požadavkům. Tím, že správce, chcete-li změnit umístění souboru umožňuje více bran Windows PowerShell Web Accessu používat stejná autorizační pravidla, pokud se taková konfigurace vyžaduje.

## <a name="session-management"></a>Správa relací

Ve výchozím nastavení Windows PowerShell Web Accessu omezuje uživateli jednou tři relace. Můžete upravit webovou aplikaci **web.config** souborů ve Správci služby IIS pro podporu jiný počet relací na uživatele. Cesta k **web.config** soubor je `$Env:Windir\Web\PowerShellWebAccess\wwwroot\Web.config`.

Ve výchozím nastavení je webový Server služby IIS restartování fondu aplikací v případě jakékoli změně nastavení nakonfigurovaná. Například, když se změní na restartování fondu aplikací **web.config** souboru. > protože **Windows PowerShell Web Accessu** stavy relací v paměti > uživatelé přihlásili k **Windows PowerShell Web Accessu** relace ke ztrátě jejich relací při restartování fondu aplikací.

### <a name="setting-default-parameters-on-the-sign-in-page"></a>Nastavení výchozích parametrů na přihlašovací stránce

Pokud vaše brána Windows PowerShell Web Accessu běží na Windows serveru 2012 R2, můžete nakonfigurovat výchozí hodnoty pro nastavení, které jsou zobrazeny na stránce pro přihlášení k Windows PowerShell Web Accessu. Hodnoty v můžete nakonfigurovat **web.config** soubor, který je popsaný v předchozím odstavci. Výchozí hodnoty pro nastavení přihlašovací stránky se nacházejí v **appSettings** část souboru web.config; následuje příklad **appSettings** oddílu. Platné hodnoty pro mnohá z těchto nastavení jsou stejné jako u odpovídajících parametrů [New-PSSession](https://technet.microsoft.com/library/hh849717.aspx) rutiny v prostředí Windows PowerShell.

Například `defaultApplicationName` klíč, jak je znázorněno v následující blok kódu, je hodnota **$PSSessionApplicationName** preferenční proměnné v cílovém počítači.

```xml
  <appSettings>
      <add key="maxSessionsAllowedPerUser" value="3"/>
      <add key="defaultPortNumber" value="5985"/>
      <add key="defaultSSLPortNumber" value="5986"/>
      <add key="defaultApplicationName" value="WSMAN"/>
      <add key="defaultUseSslSelection" value="0"/>
      <add key="defaultAuthenticationType" value="0"/>
      <add key="defaultAllowRedirection" value="0"/>
      <add key="defaultConfigurationName" value="Microsoft.PowerShell"/>
  </appSettings>
```

### <a name="time-outs-and-unplanned-disconnections"></a>Vypršení časových limitů a neplánovaná odpojení

Časový limit relací Windows PowerShell Web Accessu. Ve Windows PowerShell Web Accessu a systémem Windows Server 2012 se zobrazí zpráva vypršení časového limitu pro přihlášeného uživatele po 15 minutách nečinnosti relace. Pokud uživatel neodpoví během pěti minut po zobrazení zprávy o vypršení časového limitu, relace se ukončí a uživatel se odhlásí. Časové limity relací můžete změnit v nastaveních webu ve Správci služby IIS.

Ve Windows PowerShell Web Accessu a systémem Windows Server 2012 R2, vypršení časového limitu relace, ve výchozím nastavení, po 20 minutách nečinnosti. Pokud uživatelé odpojení z relací ve webové konzole z důvodu chyby sítě nebo jiných neplánovaných výpadků nebo chyb a ne kvůli tomu, že sami, relací Windows PowerShell Web Accessu nadále spouštět, připojený k cílové počítače, dokud nevyprší časový limit na zavřeli na straně klienta. Relace se odpojí buď po uplynutí výchozích 20 minut, nebo po vypršení časového limitu určeného správcem brány, podle toho, co je kratší.

Pokud server brány se systémem Windows Server 2012 R2, Windows PowerShell Web Accessu umožňuje uživatelům znovu připojit k uloženým relacím později, ale při chyby sítě, neplánované výpadky nebo jiné chyby odpojit relace, uživatelé nemůže zobrazit ani uložit relace, dokud se po vypršení časového limitu určeného brány má správce vypršelo.

## <a name="see-also"></a>Viz také

[Nainstalovat a používat Windows PowerShell Web Accessu](https://technet.microsoft.com/library/hh831611(v=ws.11).aspx)

[about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx)

[Windows PowerShell Web Access rutiny](cmdlets/web-access-cmdlets.md)

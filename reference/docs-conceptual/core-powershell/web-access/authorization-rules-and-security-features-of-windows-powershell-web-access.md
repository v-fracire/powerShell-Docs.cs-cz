---
ms.date: 2017-06-27
keywords: "rutiny prostředí PowerShell"
title: "Autorizační pravidla a funkce zabezpečení Windows PowerShell Web Accessu"
ms.openlocfilehash: 19e4aa1bb55178ec2634af0771afe2db5db3423c
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="authorization-rules-and-security-features-of-windows-powershell-web-access"></a>Autorizační pravidla a funkce zabezpečení Windows PowerShell Web Accessu

Aktualizované: Červen 24, 2013

Platí pro: Windows Server 2012 R2, Windows Server 2012

Windows PowerShell Web Access v systému Windows Server 2012 R2 a Windows Server 2012 má model omezující zabezpečení.
Uživatelé musí mít explicitně udělený přístup předtím, než může přihlásit k bráně Windows PowerShell Web Access a používat webovou konzolu prostředí Windows PowerShell.

## <a name="configuring-authorization-rules-and-site-security"></a>Konfigurace autorizačních pravidel a zabezpečení lokality

Po nainstalování Windows PowerShell Web Access a konfiguraci brány, uživatelé mohli otevřít přihlašovací stránku v prohlížeči, ale se nelze přihlásit, dokud správce Windows PowerShell Web Access explicitně neudělí přístup.
Řízení přístupu, Windows PowerShell Web Access"spravuje pomocí sady rutin prostředí Windows PowerShell, které jsou popsané v následující tabulce.
Neexistuje žádné srovnatelné grafické uživatelské rozhraní pro přidávání nebo správu autorizačních pravidel.
V tématu [rutiny prostředí Windows PowerShell Web Access](cmdlets/web-access-cmdlets.md).

Správci můžou definovat 0 -*n* pravidla ověřování pro Windows PowerShell Web Access.
Výchozí zabezpečení je víc omezující než povolující, nulový počet ověřovacích pravidel znamená, že uživatelé nemají k ničemu přístup.

[Add-PswaAuthorizationRule](cmdlets/add-pswaauthorizationrule.md) a [Test-PswaAuthorizationRule](cmdlets/test-pswaauthorizationrule.md) ve Windows serveru 2012 R2 obsahují parametr Credential, který umožňuje přidat a otestovat autorizační pravidla Windows PowerShell Web Access ze vzdálené počítače, nebo z v aktivní relaci Windows PowerShell Web Access.
Jako s jinými rutinami prostředí Windows PowerShell, které mají parametr Credential, můžete určit objekt PSCredential jako hodnotu parametru.
Chcete-li vytvořit objekt PSCredential obsahující pověření, které chcete předat do vzdáleného počítače, spusťte [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) rutiny.

Pravidla ověřování Windows PowerShell Web Access jsou povolená pravidla.
Každé pravidlo je definicí povolených připojení mezi uživateli, cílové počítače a konkrétní Windows PowerShellÂ [konfigurace relace](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) (také označuje jako koncové body nebo _prostředí runspace_) na zadané cílové počítače.
Vysvětlení na **prostředí runspace** najdete v části [začátku pomocí prostředí PowerShell prostředí runspace](https://blogs.technet.microsoft.com/heyscriptingguy/2015/11/26/beginning-use-of-powershell-runspaces-part-1/)

> **Poznámka k zabezpečení**
>
> Aby uživatel získal přístup, stačí, aby platilo jedno pravidlo.
Pokud má uživatel přístup k jednomu počítači s úplným jazykovým přístupem nebo přístup jenom k rutinami pro vzdálenou správu prostředí Windows PowerShell, z webové konzoly, uživatel může přihlásit (nebo směrování) do jiných počítačů, které jsou připojené k prvnímu cílovému počítači.
Nejbezpečnější způsob konfigurace Windows PowerShell Web Access je umožnit uživatelům přístup jenom k omezeným konfiguracím relací, které jim umožní splnit konkrétní úlohy, které by jinak museli provádět vzdáleně.

Rutiny v odkazuje [rutiny prostředí Windows PowerShell Web Access](cmdlets/web-access-cmdlets.md) umožňují vytvořit sadu pravidel přístupu, které se používají k autorizaci uživatele v bráně Windows PowerShell Web Access.
Pravidla se liší od seznamů ACL v cílovém počítači a poskytují další vrstvu zabezpečení webového přístupu.
Další informace o zabezpečení jsou popsané v následující části.

Pokud uživatelé nemůžou projít žádnou z předchozích vrstev, obdrží zprávu obecný "přístup byl odepřen" jim v okně prohlížeče.
I když se podrobnosti zabezpečení protokolují na serveru brány, koncoví uživatelé nevidí informace o tom, kolika vrstvami zabezpečení prošli a ve které vrstvě došlo k chybě přihlášení nebo ověření.

Další informace o konfiguraci autorizačních pravidel najdete v tématu [konfigurací autorizačních pravidel](#configuring-authorization-rules-and-site-security) v tomto tématu.

### <a name="security"></a>Zabezpečení

Model zabezpečení Windows PowerShell Web Access má čtyři vrstvy mezi koncovým uživatelem webové konzoly a cílový počítač.
Windows PowerShell Web Access správci mohou přidávat další vrstvy zabezpečení prostřednictvím další konfigurace v konzole Správce služby IIS.
Další informace o zabezpečení webů v konzole Správce služby IIS najdete v tématu [konfigurace zabezpečení webového serveru (IIS 7)](https://technet.microsoft.com/library/cc731278).
Další informace o službě IIS osvědčené postupy a brání útoky DOS, najdete v části [osvědčené postupy pro předcházení útokům na dostupnost služby](https://technet.microsoft.com/library/cc750213).
Správce může taky koupit a nainstalovat další maloobchodní software pro ověřování.

Následující tabulka popisuje čtyři vrstvy zabezpečení mezi koncovými uživateli a cílovými počítači.

|Úroveň|Vrstva|
|-|-|
|1|[funkce zabezpečení webového serveru IIS](#iis-web-server-security-features)|
|2|[ověřování založené na formulářích brány Windows powershell webový přístup](#windows-powershell-web-access-forms-based-gateway-authentication)|
|3|[Windows powershell web access autorizační pravidla](#windows-powershell-web-access-authorization-rules)|
|4|[Cíl ověřování a autorizační pravidla](#target-authentication-and-authorization-rules)|

Podrobné informace o každé vrstvě lze nalézt v těchto položek:

#### <a name="iis-web-server-security-features"></a>Funkce zabezpečení webového serveru IIS

Windows PowerShell Web Access uživatelé musí vždycky zadat uživatelské jméno a heslo k ověření své účty v bráně.
Však správce Windows PowerShell Web Access můžete také zapnout volitelné ověření klientského certifikátu zapnout nebo vypnout, najdete v tématu [nainstalovat a používat windows powershell web Accessu](install-and-use-windows-powershell-web-access.md) povolit testovací certifikát a novější, jak nakonfigurovat pravý certifikát).

Volitelná funkce klientského certifikátu vyžaduje, aby koncoví uživatelé měli kromě svých uživatelských jmen a hesel i platný klientský certifikát, a je součástí konfigurace webového serveru (IIS).
Pokud je vrstva klientského certifikátu povolená, přihlašovací stránce Windows PowerShell Web Access vyzve uživatele k poskytování platné certifikáty, než se vyhodnocují své přihlašovací údaje.
Ověření klientského certifikátu automaticky vyhledává klientský certifikát.
Pokud se platný certifikát nenajde, Windows PowerShell Web Access informuje uživatele, aby ho mohli poskytnout certifikát.
Pokud se najde platný klientský certifikát, Windows PowerShell Web Access otevře na stránce přihlášení pro uživatele pro poskytování svá uživatelská jména a hesla.

Toto je příkladem nastavení dalšího ověření zabezpečení, které nabízí Webový Server IIS.
Další informace o jiných funkcích zabezpečení služby IIS najdete v tématu [konfigurace zabezpečení webového serveru (IIS 7)](https://technet.microsoft.com/library/cc731278)

#### <a name="windows-powershell-web-access-forms-based-gateway-authentication"></a>Ověřování pomocí formulářů brány Windows PowerShell Web Access

Windows PowerShell Web Access přihlašovací stránka vyžaduje sadu pověření (uživatelské jméno a heslo) a nabízí uživatelům možnost poskytnout jiná pověření pro cílový počítač.
Pokud uživatel jiná pověření neposkytne, primární uživatelské jméno a heslo použitá pro připojení k bráně se použijí i pro připojení k cílovému počítači.

Požadovaná pověření se ověřují v bráně Windows PowerShell Web Access.
Tyto přihlašovací údaje musí být platné uživatelské účty na buď místní Windows PowerShell Web Access serveru brány, nebo ve službě Active Directory.

#### <a name="windows-powershell-web-access-authorization-rules"></a>Windows PowerShell Web Access autorizační pravidla

Po ověření uživatele v bráně Windows PowerShell Web Access zkontrolujte autorizační pravidla, chcete-li ověřit, zda má uživatel přístup k požadovanému cílovému počítači.
Po úspěšném ověření přihlašovacích údajů uživatele předají k cílovému počítači.

Tato pravidla se vyhodnocují jenom po ověření uživatele bránou a před tím, než může dojít k ověření uživatele v cílovém počítači.

#### <a name="target-authentication-and-authorization-rules"></a>Cílové ověřování a autorizační pravidla

Poslední vrstva zabezpečení pro Windows PowerShell Web Access je konfigurace cílového počítače vlastní zabezpečení.
Uživatelé musí mít příslušná přístupová práva nakonfigurovaná na cílovém počítači a také v autorizačních pravidlech Windows PowerShell Web Access, spustit webovou konzolu prostředí Windows PowerShell, která ovlivňuje cílový počítač prostřednictvím Windows PowerShell Web Access.

Tato vrstva nabízí stejné mechanismy zabezpečení, které by vyhodnocovaly pokusy o připojení, pokud se uživatelé pokusili vytvořit vzdálené relace prostředí Windows PowerShell k cílovému počítači z prostředí Windows PowerShell spuštěním [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Enter-PSSession) nebo [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/new-pssession) rutiny.

Ve výchozím nastavení používá Windows PowerShell Web Access primární uživatelské jméno a heslo pro ověřování na bráně a cílovým počítačem.
Webová přihlašovací stránce v části s názvem **volitelná nastavení připojení**, nabízí uživatelům možnost poskytnout jiná pověření pro cílový počítač, pokud jsou požadována.
Pokud uživatel neposkytne alternativní přihlašovací údaje, primární uživatelské jméno a heslo, které se používají k připojení k bráně se také používají k připojení k cílovému počítači.

Autorizační pravidla se dají použít k povolení přístupu uživatelům ke konfiguraci konkrétní relace.
Můžete vytvořit _omezený prostředí runspace_ nebo konfigurace relace pro Windows PowerShell Web Access a povolit konkrétním uživatelům se při přihlášení do Windows PowerShell Web Access připojit pouze ke konkrétním konfiguracím relací.
Můžete použít seznamy řízení přístupu (ACL) k určení uživatelů, kteří mají přístup ke konkrétním koncovým bodům a dále omezit přístup k koncový bod pro konkrétní skupinu uživatelů pomocí autorizačních pravidel popsaných v této části.
Další informace o prostředích runspace s omezeným přístupem najdete v tématu [vytváření omezené prostředí runspace](https://msdn.microsoft.com/en-us/library/dn614668).

### <a name="configuring-authorization-rules"></a>Konfigurace autorizačních pravidel

Správci můžou chtít stejné autorizační pravidlo pro Windows PowerShell Web Access uživatele, kteří již je definována v jejich prostředí pro vzdálenou správu prostředí Windows PowerShell.
První postup v této části popisuje, jak přidat pravidlo zabezpečené autorizace udělující přístup jednomu uživateli, přihlašujícímu se ke správě jednoho počítače a v rámci konfigurace jedné relace.
Druhý postup popisuje, jak odebrat autorizační pravidlo, které už není potřeba.

Pokud budete chtít povolit konkrétním uživatelům práci jenom v omezeném prostředí runspace ve Windows PowerShell Web Accessu pomocí vlastních konfigurací relace, vytvořte vlastní konfigurace relací předtím, než přidáte autorizační pravidla, která na ně odkazují.
Rutiny Windows PowerShell Web Access nelze použít k vytvoření vlastních konfigurací relací.
Další informace o vytváření vlastních konfigurací relací najdete v tématu [about_Session_Configuration_Files](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configuration_files).

Rutiny Windows PowerShell Web Access podporují jeden zástupný znak – hvězdičku ( \* ).
Zástupné znaky uvnitř řetězců se nepodporují. Na jednu položku (uživatele, počítače nebo konfigurace relací) použijte jednu hvězdičku.

> **Poznámka:**
>
> Další způsoby použití autorizačních pravidel pro udělení přístupu uživatelům a zabezpečení prostředí Windows PowerShell Web Access, najdete v tématu [Další příklady scénářů autorizační pravidlo](#other-authorization-rule-scenario-examples) v tomto tématu.

#### <a name="to-add-a-restrictive-authorization-rule"></a>Přidání omezujícího autorizačního pravidla

1. Proveďte jednu z následujících způsobů otevřete relaci prostředí Windows PowerShell se zvýšenými uživatelskými právy.

    - Na ploše Windows klikněte pravým tlačítkem na **prostředí Windows PowerShell** na hlavním panelu a pak klikněte na tlačítko **spustit jako správce**.

    - V systému Windows **spustit** obrazovky, klikněte pravým tlačítkem na **prostředí Windows PowerShell** a potom klikněte na **spustit jako správce**.

2. **Volitelný krok** pro omezení přístupu uživatelů s použitím konfigurací relace:

    Ověřte, že konfigurace relace, které chcete použít, již existuje ve vašich pravidlech.
Pokud se ještě nejsou vytvořené, použijte pokyny pro vytvoření konfigurací relace v [about_Session_Configuration_Files](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configuration_files).

3. Toto autorizační pravidlo umožňuje konkrétní přístup uživatele k jednomu počítači v síti, ke kterým mají obvykle přístup, včetně přístupu ke konfiguraci konkrétní relace, která je omezená na uživatele '™ s typické skriptování a rutiny potřebám. Zadejte následující příkaz a stiskněte klávesu **Enter**.

```powershell
Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>
```

  - V následujícím příkladu, uživateli se jménem _JSmith_ v _Contoso_ domény je uděleno oprávnění ke správě počítače _Contoso_214_a používá konfiguraci relace s názvem _NewAdminsOnly_.

```powershell
Add-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly
```

4. Ověřte, že pravidlo vytvořila spuštěním **Get-PswaAuthorizationRule** rutiny nebo **Test-PswaAuthorizationRule - UserName &lt;domény\\uživatele | počítače\\ Uživatel&gt; - ComputerName** &lt;název_počítače&gt;. Například **Test-PswaAuthorizationRule - UserName Contoso\\JSmith - ComputerName Contoso_214**.

#### <a name="to-remove-an-authorization-rule"></a>Odebrání autorizačního pravidla

1. Pokud relaci prostředí Windows PowerShell ještě není otevřené, najdete v kroku 1 tématu [přidání omezujícího autorizačního pravidla](#to-add-a-restrictive-authorization-rule) v této části.

2. Zadejte následující příkaz a stiskněte klávesu **Enter**, kde *pravidlo ID* představuje jedinečné ID číslo pravidla, které chcete odebrat.

```powershell
Remove-PswaAuthorizationRule -ID <rule ID>
```

Případně, pokud ID číslo neznáte, ale znáte popisný název pravidla, které chcete odebrat, můžete získat název pravidla a zřetězit ho do `Remove-PswaAuthorizationRule` rutiny pro odebrání pravidla, jak je znázorněno v následujícím příkladu: `Get-PswaAuthorizationRule -RuleName <rule-name> | Remove-PswaAuthorizationRule`.

>**Poznámka:**:
>
>Zobrazí se výzva k potvrzení odstranění zadaného autorizačního pravidla; Pravidlo se odstraní po stisknutí klávesy **Enter**. Ujistěte se, že chcete odebrat autorizační pravidlo dřív, než spustíte rutinu `Remove-PswaAuthorizationRule`.

#### <a name="other-authorization-rule-scenario-examples"></a>Další příklady scénářů s autorizačními pravidly

Každé relaci prostředí Windows PowerShell používá konfigurace relace; Pokud není určen pro relaci, prostředí Windows PowerShell používá výchozí integrovanou konfiguraci relace prostředí Windows PowerShell, označuje jako Microsoft.PowerShell. Výchozí konfigurace relace zahrnuje všechny rutiny, které jsou v počítači k dispozici. Správci můžou omezit přístup u všech počítačů tak, že definují konfiguraci relace prostředí runspace s omezeným přístupem (omezeným rozsahem rutin a úloh, které jejich koncoví uživatelé můžou provádět). Uživatel, který je udělen přístup k jednomu počítači s úplným jazykovým přístupem nebo jenom Vzdálená správa rutiny prostředí Windows PowerShell můžete připojit k jiné počítače, které jsou připojené k prvnímu počítači. Definování omezeném prostředí runspace může zabránit uživatelům v přístupu k jiným počítačům z jejich povoleného prostředí runspace prostředí Windows PowerShell a zvyšuje zabezpečení vašeho prostředí Windows PowerShell Web Access. Konfigurace relace můžete distribuovat (pomocí zásad skupiny) do všech počítačů, které chtějí správci zpřístupnit prostřednictvím Windows PowerShell Web Access. Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx).
Toto jsou některé z příkladů tohoto scénáře.

- Správce vytvoří koncový bod s názvem **Pswakoncovybod**, s omezeném prostředí runspace. Pak správce vytvoří pravidlo  **\*,\*, Pswakoncovybod**a distribuuje koncový bod do jiných počítačů. Toto pravidlo umožňuje všem uživatelům přistupovat ke všem počítačům s koncovým bodem **Pswakoncovybod**. Pokud se jedná o jediné autorizační pravidlo definované v sadě pravidel, nebudou počítače bez tohoto koncového bodu přístupné.

- Správce vytvořil koncový bod s prostředím runspace s omezeným přístupem s názvem **Pswakoncovybod**a chce omezit přístup k určitým uživatelům. Správce vytvoří skupinu uživatelů s názvem **podporauroven1**a definuje následující pravidlo: **podporauroven1,\*, Pswakoncovybod**. Pravidlo udělí všem uživatelům ve skupině **podporauroven1** přístup ke všem počítačům s **Pswakoncovybod** konfigurace. Podobně se dá omezit přístup ke konkrétní sadě počítačů.

- Někteří správci poskytují určitým uživatelům širší přístup než jiným. Správce například vytvoří dvě skupiny uživatelů, **Admins** a **Zakladnipodpora**. Správce taky vytvoří koncový bod s prostředím runspace s omezeným přístupem volána s **Pswakoncovybod**a definuje následující dvě pravidla: **Admins,\*,\***  a  **Zakladnipodpora,\*, Pswakoncovybod**. První pravidlo poskytuje všem uživatelům ve **správce** přístup ke všem počítačům a druhé pravidlo poskytuje všem uživatelům ve **Zakladnipodpora** přístup jenom k těm počítačům s  **Pswakoncovybod**.

- Správce nastavil privátní testovací prostředí a chce umožnit všem oprávněným uživatelům v síti přístup ke všem počítačům v síti, ke kterým mají obvykle přístup, včetně přístupu ke všem konfiguracím relace, ke kterým obvykle přistupují. Protože se jedná o privátní testovací prostředí, správce vytvoří autorizační pravidlo, které není zabezpečené.
  - Správce spustí rutinu `Add-PswaAuthorizationRule * * *`, která používá zástupný znak  **\***  k reprezentaci všech uživatelů, všechny počítače a všechny konfigurace.
  - Toto pravidlo je ekvivalentem tohoto: `Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *`.

  >**Poznámka:**:
  >
  >Toto pravidlo se nedoporučuje v zabezpečeném prostředí a obchází vrstvu zabezpečení poskytované Windows PowerShell Web Access autorizační pravidla.

- Správce musí povolit uživatelům, aby se mohli připojovat k cílovým počítačům v prostředí, které obsahuje pracovní skupiny a domény, kde se počítače pracovních skupin občas používají pro připojení k cílovým počítačům v doménách a počítače v doménách se příležitostně používají pro připojení k cílovým počítačům v pracovních skupinách. Správce má server brány, *PswaServer*, v pracovní skupině a cílový počítač *srv1.contoso.com* je v doméně. Uživatel *Jan* je oprávněný místní uživatel na serveru brány pracovní skupiny a cílovým počítačem. Jeho uživatelské jméno na serveru pracovní skupiny je *Janlocal*; a jeho uživatelské jméno v cílovém počítači je *contoso\\Jan*. Správce přidá následující pravidlo, aby Janovi autorizoval přístup k srv1.contoso.com.

```powershell
Add-PswaAuthorizationRule -userName PswaServer\chrisLocal -computerName srv1.contoso.com -configurationName Microsoft.PowerShell
```

Předchozí příklad pravidla ověřuje Jana na serveru brány a potom autorizuje jeho přístup k *srv1*. Na stránce přihlášení musí Jan zadat druhou sadu pověření v **volitelná nastavení připojení** oblasti (*contoso\\Jan*). Server brány použije další sadu pověření k jeho ověření v cílovém počítači, *srv1.contoso.com*.

V předchozím scénáři Windows PowerShell Web Access vytvoří úspěšné připojení k cílovému počítači pouze po následující byla úspěšná a povolení aspoň jedním autorizačním pravidlem.

1. Ověřování na serveru brány pracovní skupiny přidáním uživatelského jména ve formátu *název_serveru*\\*uživatelské_jméno* autorizační pravidlo

2. Ověřování v cílovém počítači pomocí alternativních přihlašovacích údajů, které jsou součástí na stránce přihlášení **volitelná nastavení připojení** oblasti

  >**Poznámka:**:
  >
  >Pokud jsou brána a cílové počítače v různých pracovních skupinách nebo doménách, musí se mezi těmito dvěma počítači pracovních skupin, dvěma doménami nebo pracovní skupinou a doménou vytvořit vztah důvěryhodnosti. Tento vztah nelze konfigurovat pomocí rutin Windows PowerShell Web Access autorizačních pravidel. Autorizační pravidla nedefinují vztah důvěryhodnosti mezi počítači. Jenom autorizují uživatele, aby se mohli připojit ke konkrétním cílovým počítačům a konfiguracím relací. Další informace o tom, jak konfigurovat vztah důvěryhodnosti mezi různými doménami, najdete v části [vytvoření domény a vztahy důvěryhodnosti doménové struktury](https://technet.microsoft.com/library/cc794775.aspx"). Další informace o tom, jak přidat do seznamu důvěryhodných hostitelů počítače v pracovních skupinách najdete v tématu [Vzdálená správa pomocí Správce serveru](https://technet.microsoft.com/library/dd759202.aspx)

### <a name="using-a-single-set-of-authorization-rules-for-multiple-sites"></a>Použití jedné sady autorizačních pravidel pro víc lokalit

Autorizační pravidla jsou uložená v souboru XML. Ve výchozím nastavení, je název cesty souboru XML _% windir %\\webové\\PowershellWebAccess\\data\\AuthorizationRules.xml_.

Cesta k souboru XML pravidla autorizace je uložena v **powwa.config** soubor, který se nachází v _% windir %\\webové\\PowershellWebAccess\\data_. Správce má flexibilně změnit odkaz na výchozí cestu v **powwa.config** tak, aby vyhovovala potřebám nebo požadavkům. Tím, že správce a změňte umístění souboru umožňuje více bran Windows PowerShell Web Access používat stejná autorizační pravidla, pokud taková konfigurace se požaduje.

## <a name="session-management"></a>Správa relací

Ve výchozím nastavení Windows PowerShell Web Access omezuje uživatele relací na tři najednou. Můžete upravit webové aplikace **web.config** soubor ve Správci služby IIS pro podporu jiný počet relací na uživatele.
Cesta k **web.config** soubor _$Env: Windir\\webové\\PowerShellWebAccess\\wwwroot\\Web.config_.

Ve výchozím nastavení je webový Server IIS nakonfigurovaná k restartování fondu aplikací, pokud jsou všechna nastavení upravit. Například když se změní na restartování fondu aplikací **web.config** souboru.
>Protože **Windows PowerShell Web Access** stavy relací v paměti používá, uživatelů přihlášených k **Windows PowerShell Web Access** relací ke ztrátě jejich relací při restartování fondu aplikací.

### <a name="setting-default-parameters-on-the-sign-in-page"></a>Nastavení výchozích parametrů na přihlašovací stránce

Pokud vaše brána Windows PowerShell Web Access běží na Windows Server 2012 R2, můžete nakonfigurovat výchozí hodnoty pro nastavení, která se zobrazí na přihlašovací stránce Windows PowerShell Web Access. Hodnoty v můžete nakonfigurovat **web.config** soubor, který je popsaný v předchozím odstavci. Výchozí hodnoty pro nastavení přihlašovací stránky se nacházejí v **appSettings** části souboru web.config; tady je příklad **appSettings** části. Platné hodnoty pro mnohá z těchto nastavení jsou stejné jako u odpovídajících parametrů [New-PSSession](https://technet.microsoft.com/library/hh849717.aspx) rutiny v prostředí Windows PowerShell.
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

Časový limit relace Windows PowerShell Web Access. V systému Windows PowerShell Web Access spuštěné v systému Windows Server 2012 se zobrazí zpráva Časový limit pro přihlášeného uživatele po 15 minutách nečinnosti relace. Pokud uživatel neodpoví během pěti minut po zobrazení zprávy o vypršení časového limitu, relace se ukončí a uživatel se odhlásí. Časové limity relací můžete změnit v nastaveních webu ve Správci služby IIS.

V systému Windows PowerShell Web Access systémem Windows Server 2012 R2, vypršení časového limitu relace, ve výchozím nastavení, po 20 minutách nečinnosti. Pokud uživatelé odpojení z relací ve webové konzole z důvodu chyby sítě nebo jiných neplánovaných výpadků nebo chyb a ne kvůli tomu, že relaci sami zavřeli, Windows PowerShell Web Access relací nadále spouštět, připojení k cílové počítače, dokud nevyprší časový limit na straně klienta. Relace se odpojí buď po uplynutí výchozích 20 minut, nebo po vypršení časového limitu určeného správcem brány, podle toho, co je kratší.

Pokud server brány se systémem Windows Server 2012 R2, Windows PowerShell Web Access umožňuje uživatelům znovu připojit k uloženým relacím později, ale když chyby sítě, neplánované výpadky nebo jiné chyby odpojit relace, uživatelé nemohou zobrazit ani znovu připojit k uložit relace, dokud nebude po vypršení časového limitu určeného bránou správce uplynula.

## <a name="see-also"></a>Viz také

- [Nainstalovat a používat Windows PowerShell Web Accessu](https://technet.microsoft.com/en-us/library/hh831611(v=ws.11).aspx)
- [about_Session_Configurations](https://technet.microsoft.com/library/dd819508.aspx)
- [Rutiny prostředí Windows PowerShell Web Access](cmdlets/web-access-cmdlets.md)

---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Konfigurace relace JEA
ms.openlocfilehash: 3e5a663be8e7aba09a2592c278224cd892c89a20
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190090"
---
# <a name="jea-session-configurations"></a>Konfigurace relace JEA

> Platí pro: prostředí Windows PowerShell 5.0

Koncový bod JEA je zaregistrován v systému pomocí vytvoření a registrace konfigurační soubor relace prostředí PowerShell v určitým způsobem.
Určení konfigurací relace *kdo* můžete použít JEA koncový bod a které rolí budou mít přístup k.
Budou také definovat globální nastavení, které platí pro všechny role uživatele v relaci JEA.

Toto téma popisuje postup vytvoření konfiguračního souboru relace prostředí PowerShell a zaregistrujte koncový bod JEA.

## <a name="create-a-session-configuration-file"></a>Vytvoření konfiguračního souboru relace

Chcete-li zaregistrovat koncový bod JEA, budete muset zadat, jak by měl být nakonfigurovaný tohoto koncového bodu.
Existuje řada možností vzít v úvahu zde nejdůležitější, z které toho, kdo má mít přístup ke koncovému bodu JEA, které role se jejich přiřazen, které identity JEA použije skrytě a co bude název koncového bodu JEA.
Tyto jsou pro všechna definovaná v konfiguračním souboru relace prostředí PowerShell, který je datový soubor prostředí PowerShell koncové s příponou .pssc.

Pokud chcete vytvořit konfigurační soubor kostru relace pro koncové body JEA, spusťte následující příkaz.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> Nejběžnější možnosti konfigurace jsou součástí souboru kostru ve výchozím nastavení.
> Použití `-Full` přepínač tak, aby vygenerované PSSC zahrnout všech příslušných nastavení.

Soubor konfigurace relace můžete otevřít v každém textovém editoru.
`-SessionType RestrictedRemoteServer` Pole označuje, že konfigurace relace bude používat JEA pro zabezpečené správy.
Relace nakonfigurovali tímto způsobem bude fungovat v [NoLanguage režimu](https://technet.microsoft.com/library/dn433292.aspx) a mít pouze následující příkazy 8 výchozí (a aliasy) k dispozici:

- Clear-Host (cls, zrušte zaškrtnutí)
- Ukončení-PSSession (exsn, ukončení)
- Get-Command (gcm)
- Get-FormatData
- Get-Help
- Objekt míry (měr)
- Odchozí výchozí
- Select-Object (vyberte)

Žádní zprostředkovatelé prostředí PowerShell jsou k dispozici, ani se, že všechny externí programy (spustitelné soubory, skripty atd.).

Existuje několik dalších polí, které můžete nakonfigurovat pro relaci JEA.
Že jsou popsané v následujících částech.

### <a name="choose-the-jea-identity"></a>Zvolte identitu JEA

Na pozadí musí JEA identity (účet) pro použití při spouštění příkazů připojeného uživatele.
Rozhodnete, které identity JEA použije v konfiguračním souboru relace.

#### <a name="local-virtual-account"></a>Místní virtuální účet

Pokud role nepodporuje tento koncový bod JEA se používají ke správě místního počítače a účet místního správce stačí ke spuštění příkazů úspěšně, byste měli nakonfigurovat JEA, aby používala účet místní virtuální.
Virtuální účty jsou dočasné účty, které jsou jedinečné pro konkrétního uživatele a pouze poslední dobu trvání relace prostředí PowerShell systému.
Na členském serveru nebo pracovní stanici, virtuální účty patří do místního počítače **správci** skupiny a mají přístup k většině systémové prostředky.
Na řadiči domény Active Directory, virtuální účty patří do domény **Domain Admins** skupiny.

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

Pokud role nepodporuje konfiguraci relace nevyžadují, aby takové široká oprávnění, Volitelně můžete zadat skupiny zabezpečení, do kterých budou virtuální účet patří.
Na členském serveru nebo pracovní stanici musí být určených skupinách zabezpečení místních skupin, nejsou skupiny z domény.

Pokud je zadána jedna nebo více skupin zabezpečení, bude virtuální účet už patřit do místní nebo doménové skupiny správců.

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

#### <a name="group-managed-service-account"></a>Účet spravované služby skupiny


Účet skupiny spravované služby (gMSA) pro scénářům, které vyžadují JEA uživatelům přístup k síťovým prostředkům, například další počítače nebo webové služby, je vhodnější identity použít.
účty gMSA získáte identitu domény, který můžete použít k ověřování na základě prostředků na libovolném počítači v rámci domény.
Práva poskytuje účet gMSA, je určen prostředky se připojujete.
Práva správce na všechny počítače nebo služby, nebudete mít automaticky, pokud správce počítače nebo služby se explicitně udělí oprávnění účtu gMSA oprávnění správce.

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

účty gMSA musí být použit pouze při přístupu k síťovým prostředkům jsou požadovány pro z několika důvodů:

- Je těžší vysledovat zpět akce na uživatele při použití účtu gMSA vzhledem k tomu, že každý uživatel sdílí stejnou identitu spustit jako. Musíte se prostudovat přepisy relace prostředí PowerShell a protokoly ke koordinaci uživatelů s jejich akce.

- Účet gMSA může mít přístup k mnoha síťovým prostředkům, které je připojující se uživatel nemusí přístup k. Vždy pokusí omezení skutečná oprávnění v relaci JEA podle Princip nejnižších nutných oprávnění.

> [!NOTE]
> Účty spravované služby skupiny jsou pouze k dispozici v systému Windows PowerShell 5.1 nebo novější a na počítačích připojených k doméně.


#### <a name="more-information-about-run-as-users"></a>Další informace o spouštění jako uživatele

Další informace o spuštění jako identit a jak se zohlednit do zabezpečení JEA relace najdete v [aspekty zabezpečení](security-considerations.md) článku.

### <a name="session-transcripts"></a>Přepisy relace

Doporučujeme nakonfigurovat JEA relace konfigurační soubor pro automaticky záznamů přepisy uživatelské relace.
Přepisy relace prostředí PowerShell obsahují informace o připojování uživateli spustit jako identity přiřazen, a spusťte příkazy uživatelem.
Mohou být užitečné auditování týmu, který potřebuje zjistit, kdo provedl konkrétní změny do systému.

Ke konfiguraci automatického přepis v konfiguračním souboru relace, zadejte cesta ke složce, kde by měly být uložené přepisy.

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

V zadané složce musí být nakonfigurovaný tak, aby uživatelé z úpravy nebo odstranění všech dat v něm.
Přepisy jsou zapsány do složky, pomocí účtu místního systému, který vyžaduje oprávnění ke čtení a zápisu do adresáře.
Standardní uživatelé musí mít žádný přístup ke složce a omezená sada správce zabezpečení mají mít přístup k auditu přepisy.

### <a name="user-drive"></a>Jednotka uživatele

Pokud vaši uživatelé připojující bude nutné zkopírovat soubory z koncového bodu JEA aby bylo možné spustit příkaz, můžete povolit disk uživatele v konfiguračním souboru relace.
Je jednotka uživatele [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) který se mapuje na jedinečné složku pro každý připojující se uživatel.
Tato složka slouží jako prostor pro ně kopírovat soubory do systému, nebo z nich bez bude mít přístup k systému souborů úplné nebo vystavení zprostředkovatele systému souborů.
Obsah jednotky uživatele je trvalé napříč relacemi, aby dokázala pojmout situacích, kde může přerušit připojení k síti.

```powershell
MountUserDrive = $true
```

Ve výchozím nastavení jednotka uživatele můžete uložit maximálně 50MB dat za uživatele.
Můžete omezit množství dat, může uživatel využít s *UserDriveMaximumSize* pole.

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

Pokud nechcete, aby se data na jednotce uživatele jako trvalé, můžete nakonfigurovat naplánovanou úlohu v systému, aby automaticky vyčistit složku každou noc.

> [!NOTE]
> Jednotka uživatele je pouze k dispozici v systému Windows PowerShell 5.1 nebo novější.

### <a name="role-definitions"></a>Definice rolí

Definice rolí v konfiguračním souboru relace definovat mapování *uživatelé* k *role*.
Každý uživatel nebo skupina součástí toto pole automaticky udělí oprávnění ke koncovému bodu JEA po jeho registraci.
Každý uživatel nebo skupina může být zahrnuta jako klíč v zatřiďovací tabulce pouze jednou, ale mohou být přiřazeny více rolí.
Název funkce role musí být název souboru funkce role, bez přípony .psrc.

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

Pokud uživatel patří do více než jedné skupiny v definici role, získají přístup k rolím jednotlivých.
Pokud dvě role uděluje přístup k stejné rutiny, bude udělen nejvíce projektovou sada parametrů pro uživatele.

Při zadávání místního uživatele nebo skupiny do pole definice role, nezapomeňte použít název počítače (ne *localhost* nebo *.*) před zpětné lomítko.
Název počítače můžete zkontrolovat zkontrolováním `$env:computername` proměnné.

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a>Pořadí hledání schopnosti role
Jak je znázorněno v příkladu nahoře, funkce role odkazuje plochý název (název souboru bez přípony) souboru funkce role.
Pokud jsou k dispozici v systému se stejným názvem ploché více možnosti role, prostředí PowerShell pomocí jeho pořadí implicitní hledání vyberte soubor schopností efektivní role.
Zruší **není** poskytnout přístup ke všem souborům schopnosti role se stejným názvem.

Používá JEA `$env:PSModulePath` proměnné prostředí můžete zjistit které cesty pro hledání souborů schopnosti role.
V každém z těchto cestách JEA bude hledat platný modulů prostředí PowerShell, které obsahují podsložku "RoleCapabilities".
Stejně jako u importu modulů, upřednostní JEA funkce role, které jsou součástí systému Windows k funkcím vlastní role se stejným názvem.
Pro všechny ostatní ke konfliktům s názvy přednost před je dáno pořadí, ve kterém Windows zjistí počet souborů v adresáři (není zaručena bezpečnost pro abecedy).
První soubor schopnosti role najít odpovídající požadovaný název se použije pro připojování uživatele.

Pořadí hledání schopnosti role není deterministický, pokud dvě nebo více možností role sdílejí stejný název, a proto je **důrazně doporučujeme** zkontrolujte možnosti role na počítači máte jedinečné názvy.

### <a name="conditional-access-rules"></a>Pravidla podmíněného přístupu

Všichni uživatelé a skupiny součástí RoleDefinitions pole jsou automaticky udělen přístup k JEA koncové body.
Pravidla podmíněného přístupu umožňují upřesnit tento přístup a vyžaduje, aby uživatel patří do skupiny další zabezpečení, které nemají vliv rolí, které jsou přiřazeny.
To může být užitečné, pokud chcete integrovat "jenom v čase" privilegovaný přístup k řešení pro správu, ověřování pomocí čipové karty nebo jiného řešení vícefaktorového ověřování s JEA.

Pravidla podmíněného přístupu jsou definovány v poli RequiredGroups v konfiguračním souboru relace.
Zde můžete zadat zatřiďovací tabulku (volitelně vnořená) používající 'A' a 'Nebo' klíčů můžete vytvořit vaše pravidla.
Tady jsou některé příklady, jak využít toto pole:

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

> [!NOTE]
> Pravidla podmíněného přístupu jsou pouze k dispozici v systému Windows PowerShell 5.1 nebo novější.

### <a name="other-properties"></a>Ostatní vlastnosti
Relace konfigurační soubory můžete také provést vše, co soubor schopnosti role mohou provádět pouze bez možnosti připojování uživatelům poskytnout přístup k jiné příkazy.
Pokud chcete povolit všem uživatelům přístup ke konkrétní rutiny, funkce nebo poskytovatelů, můžete tak učinit přímo do konfiguračního souboru relace.
Úplný seznam podporovaných vlastností v souboru konfigurace relace, spustit `Get-Help New-PSSessionConfigurationFile -Full`.

## <a name="testing-a-session-configuration-file"></a>Testování relace konfiguračního souboru

Můžete otestovat pomocí konfigurace relace [Test PSSessionConfigurationFile](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) rutiny.
Důrazně doporučujeme, abyste otestovali konfiguračního souboru relace, pokud jste upravili soubor pssc ručně pomocí textového editoru zajistit správnost syntaxe.
Pokud tento test neproběhne úspěšně relace konfigurační soubor, nebude moct se úspěšně zaregistroval v systému.

## <a name="sample-session-configuration-file"></a>Ukázkový soubor konfigurace relace

Níže je úplný příklad znázorňující způsob vytvoření a ověření konfigurace relace pro JEA.
Všimněte si, že jsou definice rolí vytvoří a uloží do `$roles` proměnná pro usnadnění práce a přehlednosti.
Není potřeba udělat.

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a>Aktualizace relace konfigurační soubory

Pokud potřebujete změnit vlastnosti konfigurace relace JEA, včetně mapování uživatelů na role, je nutné [zrušit registraci](register-jea.md#unregistering-jea-configurations) a [znovu zaregistrovat](register-jea.md) JEA konfigurace relace.
Při registraci znovu JEA konfigurace relace, použijte aktualizované prostředí PowerShell relace konfigurační soubor, který obsahuje požadované změny.

## <a name="next-steps"></a>Další kroky

- [Zaregistruje konfiguraci JEA](register-jea.md)
- [Autor JEA role](role-capabilities.md)
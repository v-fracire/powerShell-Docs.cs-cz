---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Konfigurace relace JEA
ms.openlocfilehash: 1b598522d43b2c1a26a739a67cee5181b21a7c32
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655459"
---
# <a name="jea-session-configurations"></a>Konfigurace relace JEA

> Platí pro: Windows PowerShell 5.0

Koncového bodu JEA je registrován v systému vytváření a registrací konfiguračního souboru relace prostředí PowerShell určitým způsobem.
Určení konfigurací relace *kdo* pomocí koncového bodu JEA a rolemi, které mají přístup k.
Také definují globální nastavení, které platí pro všechny role uživatele v relaci JEA.

Toto téma popisuje postup registrace koncového bodu JEA a vytvoření konfiguračního souboru relace Powershellu.

## <a name="create-a-session-configuration-file"></a>Vytvoření konfiguračního souboru relace

Aby bylo možné registrace koncového bodu JEA, je třeba zadat konfiguraci tohoto koncového bodu.
Existuje mnoho možností vzít v úvahu tady, nejdůležitější, o kterých toho, kteří mají mít přístup ke koncovému bodu JEA, které role bude, přiřadit, která identita JEA použije na pozadí a jaká bude název koncového bodu JEA.
Ty jsou všechny definovány v souboru konfigurace relace prostředí PowerShell, který je datový soubor prostředí PowerShell končící příponou .pssc.

Vytvoření konfiguračního souboru kostru relace u koncových bodů JEA, spusťte následující příkaz.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> Nejběžnější možnosti konfigurace jsou uvedeny v kostru souboru ve výchozím nastavení.
> Použití `-Full` přepínače zahrnout generované PSSC všech příslušných nastavení.

Soubor konfigurace relace můžete otevřít v libovolném textovém editoru.
`-SessionType RestrictedRemoteServer` Pole označuje, že konfigurace relace použije JEA pro zabezpečenou správu.
Relace tak budou fungovat v [NoLanguage režimu](https://technet.microsoft.com/library/dn433292.aspx) a obsahovat jenom následující příkazy 8 výchozí (a aliasy) k dispozici:

- Clear-Host (kompatibilní se specifikací, zrušte zaškrtnutí)
- Konec-PSSession (exsn, konec)
- Get – příkaz (gcm)
- Get-FormatData
- Get-Help
- Objekt míry (měření)
- Výchozí out-Buffer:
- Select-Object (výběr)

Žádní zprostředkovatelé prostředí PowerShell, jsou k dispozici, ani při že jakékoli vnější programy (spustitelné soubory, skripty atd.).

Existuje několik dalších polí, které můžete nakonfigurovat pro relaci JEA.
Tyto jsou popsané v následujících částech.

### <a name="choose-the-jea-identity"></a>Vyberte identitu funkce JEA

Na pozadí musí JEA identitu (účet) pro použití při spuštění příkazů připojeného uživatele.
Můžete rozhodnout, která identita JEA použije v konfiguračním souboru relace.

#### <a name="local-virtual-account"></a>Místní virtuální účet

Pokud role podporována tímto koncovým bodem JEA se používají ke správě místního počítače a účet místního správce stačí spustit příkazy úspěšně, měli byste nakonfigurovat JEA použít místní virtuální účet.
Virtuální účty jsou dočasné, které jsou jedinečné pro konkrétní uživatele a pouze poslední po dobu trvání jejich relace Powershellu.
Na členském serveru nebo pracovní stanici, virtuální účty patří do místního počítače **správci** skupiny a mají přístup k většině systémových prostředků.
Na řadič domény Active Directory virtuální účty patří do domény **Domain Admins** skupiny.

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

Pokud role podporuje konfiguraci relace nevyžadují, aby takové široká oprávnění, můžete volitelně zadat skupiny zabezpečení, ke kterým bude patřit virtuální účet.
Na členském serveru nebo pracovní stanici musí být určených skupinách zabezpečení místních skupin, nejsou skupiny z domény.

Pokud je zadána jedna nebo více skupin zabezpečení, virtuální účet se už nebude patřit do skupiny administrators místní nebo doménový.

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```
> [!NOTE]
> Virtuální účty jsou dočasně udělena přihlášení jako služba vpravo v zásadách zabezpečení místního serveru.  Pokud jeden z VirtualAccountGroups zadaný již byla udělena tato práva v zásadách, budou jednotlivé virtuální účet už přidávat a odebírat z této zásady.  To může být užitečné v situacích, jako jsou řadiče domény, ve kterém jsou úzce auditovat revize pro zásady zabezpečení řadiče domény.  To je k dispozici pouze ve Windows serveru 2016 a listopadu 2018 nebo novější kumulativní a 2019 systému Windows Server s 2019. ledna nebo pozdější kumulativní.

#### <a name="group-managed-service-account"></a>Účet spravované služby skupiny


Účet skupiny spravované služby (gMSA) pro scénářům, které vyžadují JEA uživateli přístup k síťovým prostředkům, jako jsou ostatní počítače nebo webové služby, je vhodnější identity používat.
účty gMSA poskytnout identitu domény, který slouží k ověřování na základě prostředků na jakýkoli počítač v rámci domény.
Práva získáte účtu gMSA se určuje podle zdroje se připojujete.
Práva správce na všechny počítače nebo služby nebudou mít automaticky, pokud správce počítače nebo služby se explicitně udělí oprávnění účtu gMSA oprávnění správce.

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'Domain\MyJEAgMSA'
```

účty gMSA by měla sloužit pouze při přístupu k síťovým prostředkům jsou požadovány pro z několika důvodů:

- Je obtížnější vysledovat zpět akce, které uživatele při použití účtu gMSA, protože každý uživatel sdílí stejnou identitu spustit jako. Je potřeba záznamy o studiu relace prostředí PowerShell a protokoly je možné korelovat s jejich akce uživatele.

- Účet gMSA může mít přístup k mnoha síťovým prostředkům, kterých je připojující se uživatel nemusí přístup k. Vždy pokusí omezení účinný oprávnění v relaci JEA postupovat podle principu nejnižší úrovně oprávnění.

> [!NOTE]
> Účty spravované služby skupiny jsou pouze k dispozici ve Windows PowerShell 5.1 nebo novější a na počítačích připojených k doméně.


#### <a name="more-information-about-run-as-users"></a>Další informace o spouštění jako uživatele

Další informace o spuštění jako identit a jak se zohlednit do zabezpečení JEA relace najdete v [aspekty zabezpečení](security-considerations.md) článku.

### <a name="session-transcripts"></a>Záznamy o studiu relace

Doporučuje konfiguraci relace JEA konfigurační soubor automaticky záznamu přepisy uživatelské relace.
Záznamy o studiu relace prostředí PowerShell obsahují informace o připojení uživatele spustit jako identity přiřazené, a příkazy se spouští podle uživatele.
Mohou být užitečné pro auditování týmu, který je potřeba pochopit, kdo provedl určité změny do systému.

Ke konfiguraci automatický přepis v konfiguračním souboru relací zadejte cestu ke složce, ve kterém by měly být uložené záznamy o studiu.

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

Zadaná složka musí být nakonfigurovaný zabránit uživatelům ve změnách nebo odstranění všech dat v něm.
Záznamy o studiu jsou zapsány do složky podle místní systémový účet, který vyžaduje oprávnění čtení a zápisu do adresáře.
Standardní uživatelé by měli mít přístup ke složce a omezenou sadu správci zabezpečení mají mít přístup k auditu záznamy o studiu.

### <a name="user-drive"></a>Jednotka uživatele

Pokud vaše připojujících se uživatelů bude nutné zkopírovat soubory z koncového bodu JEA Chcete-li spustit příkaz, můžete povolit disk uživatele v konfiguračním souboru relace.
Jednotka uživatele je [PSDrive](https://msdn.microsoft.com/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives) , který se mapuje na jedinečné složku pro každý připojující se uživatel.
Tato složka slouží jako místo jejich kopírování souborů ze systému, aniž by jim poskytne přístup k systému souborů úplné nebo vystavení poskytovatele FileSystem provider.
Obsah jednotky uživatele je trvalé napříč relacemi tak, aby vyhovovaly situací, ve kterém se můžou přerušit připojení k síti.

```powershell
MountUserDrive = $true
```

Ve výchozím nastavení jednotky uživatele můžete uložit maximálně 50MB dat za uživatele.
Můžete omezit množství dat uživatele můžou využívat s *UserDriveMaximumSize* pole.

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

Pokud nechcete, aby data na jednotce uživatele být trvalé, můžete nakonfigurovat naplánovanou úlohu na systém a automaticky vyčistit složku každou noc.

> [!NOTE]
> Jednotka uživatele je pouze k dispozici ve Windows PowerShell 5.1 nebo novější.

### <a name="role-definitions"></a>Definice rolí

Definice rolí v konfiguračním souboru relace definovat mapování *uživatelé* k *role*.
Každý uživatel nebo skupina součástí toto pole se automaticky udělí oprávnění do koncového bodu JEA po jeho registraci.
Každý uživatel nebo skupina může být zahrnut jako klíče zatřiďovací tabulky jenom jednou, ale je možné přiřadit víc rolí.
Název role funkce by měl být název souboru role funkce bez přípony .psrc.

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

Pokud uživatel patří do více než jedné skupiny v definici role, dostanou přístup k rolím jednotlivých.
Pokud dvě role udělit přístup ke stejné rutiny, udělí se nejvíce omezující sada parametrů pro uživatele.

Při zadávání v poli definice role místního uživatele nebo skupiny, nezapomeňte použít název počítače (nikoli *localhost* nebo *.*) před zpětným lomítkem.
Název počítače můžete zkontrolovat, že zkontrolujete `$env:computername` proměnné.

```powershell
RoleDefinitions = @{
    'MyComputerName\MyLocalGroup' = @{ RoleCapabilities = 'DnsAuditor' }
}
```

### <a name="role-capability-search-order"></a>Pořadí hledání funkce rolí
Jak je znázorněno v příkladu výše, funkce rolí odkazuje jednoduchý název (název souboru bez přípony) soubor funkce role.
Pokud více funkcí role jsou k dispozici v systému se stejným názvem, bez stromové struktury, prostředí PowerShell pomocí jeho pořadí implicitní hledání vyberte soubor funkce účinného role.
Bude **není** poskytnout přístup ke všem souborům funkce role se stejným názvem.

JEA používá `$env:PSModulePath` proměnnou prostředí k určení, které cesty kontrolovala soubory funkce role.
V rámci každé z těchto cest JEA bude hledat platný moduly Powershellu, které obsahují podsložku "RoleCapabilities".
Stejně jako u importu modulů JEA upřednostňuje funkce rolí, které jsou součástí Windows k funkcím vlastní role se stejným názvem.
Pro všechny ostatní konflikty názvů priorita je určen podle pořadí, ve kterém Windows zobrazí soubory v adresáři (není zaručena podle abecedy).
První soubor funkce role najít odpovídající požadovaný název se použije pro připojení uživatele.

Protože pořadí hledání funkce role není deterministický. Pokud dvě nebo více rolí možnosti sdílejí stejný název, je **důrazně doporučujeme** zajištění funkcí role na počítači máte jedinečné názvy.

### <a name="conditional-access-rules"></a>Pravidla podmíněného přístupu

Všichni uživatelé a skupiny součástí RoleDefinitions pole jsou automaticky udělen přístup do koncových bodů JEA.
Pravidla podmíněného přístupu umožňují Upřesnit tohoto přístupu a vyžadovat, aby uživatelé patří do skupiny další zabezpečení, které nemají vliv role, které jsou přiřazeny.
To může být užitečné, pokud chcete integrovat "počítačům v čase" privilegovaný přístup k řešení pro správu, ověřování pomocí čipové karty nebo jiného řešení vícefaktorového ověřování s JEA.

Pravidla podmíněného přístupu jsou definovány v poli RequiredGroups v konfiguračním souboru relace.
Tady můžete zadat zatřiďovací tabulku (volitelně vnořené), která používá "A" a "Nebo" klíče k vytvoření pravidla.
Tady je několik příkladů toho, jak využít toto pole:

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
> Pravidla podmíněného přístupu jsou pouze k dispozici ve Windows PowerShell 5.1 nebo novější.

### <a name="other-properties"></a>Další vlastnosti
Soubory konfigurace relace můžete také provést všechno, co soubor funkce role můžete provést pouze bez schopnost spojovací uživatelům poskytnout přístup na různé příkazy.
Pokud chcete povolit všem uživatelům přístup ke konkrétní rutiny, funkce nebo poskytovatelů, můžete tak učinit přímo v konfiguračním souboru relace.
Úplný seznam podporovaných vlastností v souboru konfigurace relace, spusťte `Get-Help New-PSSessionConfigurationFile -Full`.

## <a name="testing-a-session-configuration-file"></a>Testování souboru konfigurace relace

Můžete otestovat pomocí konfigurace relace [testovací PSSessionConfigurationFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) rutiny.
Důrazně doporučujeme, abyste otestovali konfiguračního souboru relace Pokud jste upravili soubor pssc ručně pomocí textového editoru k zajištění, že je syntaxe správná.
Pokud soubor konfigurace relace neprojde tímto testem, nebudete moci úspěšně zaregistrovat v systému.

## <a name="sample-session-configuration-file"></a>Ukázkový soubor konfigurace relace

Níže je úplný příklad ukazuje, jak vytvořit a ověřit konfiguraci relace pro JEA.
Všimněte si, že jsou vytvořeny a uloženy v definicích rolí `$roles` proměnné pro lepší čitelnost a pohodlí.
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

## <a name="updating-session-configuration-files"></a>Aktualizace relace konfiguračních souborů

Pokud potřebujete změnit vlastnosti konfigurace relace JEA, včetně mapování uživatelů k rolím, je nutné [zrušit registraci](register-jea.md#unregistering-jea-configurations) a [přeregistrovat](register-jea.md) JEA konfiguraci relace.
Při konfiguraci relace JEA přeregistrovat, použijte aktualizované prostředí PowerShell relace konfiguračního souboru, který obsahuje vaše požadované změny.

## <a name="next-steps"></a>Další kroky

- [Zaregistruje konfiguraci funkce JEA](register-jea.md)
- [Autor JEA role](role-capabilities.md)

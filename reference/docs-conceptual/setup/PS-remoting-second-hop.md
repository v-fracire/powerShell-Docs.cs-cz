---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Díky tomu druhé směrování vzdálené komunikace Powershellu
ms.openlocfilehash: 06ca43e3e0524d89ec6f66f6553c4c75072beaf3
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320699"
---
# <a name="making-the-second-hop-in-powershell-remoting"></a>Díky tomu druhé směrování vzdálené komunikace Powershellu

"Druhý segment směrování problém" odkazuje na situace nějak takto:

1. Jste přihlášeni k _Server_a_.
2. Z _Server_a_, spouští vzdálenou relaci prostředí PowerShell pro připojení k _ServerB_.
3. Příkaz můžete spustit na _ServerB_ prostřednictvím vaší vzdálené komunikace Powershellu relace pokusí získat přístup k prostředku na _ServerC_.
4. Přístup k prostředku na _ServerC_ byl odepřen, protože nejsou přihlašovací údaje, které jste použili k vytvoření relace vzdálené komunikace Powershellu předat z _ServerB_ k _ServerC_.

Existuje několik způsobů, jak tento problém vyřešit. V tomto tématu se podíváme na některé z nejoblíbenějších řešení problému druhý segment směrování.

## <a name="credssp"></a>CredSSP

Můžete použít [Credential Security Support Provider (CredSSP Credential)](https://msdn.microsoft.com/library/windows/desktop/bb931352.aspx) pro ověřování. CredSSP ukládá do mezipaměti přihlašovací údaje na vzdáleném serveru (_ServerB_), takže ho pomocí otevře až útoků využívajících krádež přihlašovacích údajů. Pokud je vzdálený počítač v ohrožení, útočník má přístup k přihlašovacím údajům uživatele. CredSSP je ve výchozím nastavení na klientských i serverových počítačích zakázána. Pouze v nejdůvěryhodnějším prostředí byste měli povolit zprostředkovatele CredSSP. Například správce domény připojení k řadiči domény, protože řadič domény je vysoce důvěryhodných.

Další informace o zajištění zabezpečení při použití ověřování CredSSP pro vzdálenou komunikaci prostředí PowerShell najdete v tématu [náhodného napadení zařízení: Mějte na paměti, CredSSP](https://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).

Další informace o útoků využívajících krádež přihlašovacích údajů najdete v tématu [útoky obrana proti útokům Pass-the-Hash (PtH) a dalším metodám krádeže přihlašovacích údajů](https://www.microsoft.com/en-us/download/details.aspx?id=36036).

Příklad toho, jak povolit a používat CredSSP pro vzdálenou komunikaci prostředí PowerShell, najdete v části [pomocí zprostředkovatele CredSSP pro vyřešení problému druhé směrování](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).

### <a name="pros"></a>Výhody

- Funguje to pro všechny servery s Windows serverem 2008 nebo novější.

### <a name="cons"></a>Nevýhody

- Má ohrožení zabezpečení.
- Vyžaduje konfiguraci rolí klienta a serveru.

## <a name="kerberos-delegation-unconstrained"></a>Delegování protokolu Kerberos (vstupy bez omezení)

Delegování protokolu Kerberos neomezeného lze také vytvořit druhý segment směrování. Tato metoda však poskytuje žádnou kontrolu, ve kterém se používají delegovaná pověření.

>**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** nastavenou vlastnost není možné delegovat. Další informace najdete v tématu [fokus zabezpečení: analyzování "Účet je citlivý a nelze jej delegovat" pro privilegované účty](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje pro ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Výhody

- Vyžaduje žádné speciální kódování.

### <a name="cons"></a>Nevýhody

- Druhé směrování pro WinRM nepodporuje.
- Poskytuje žádnou kontrolu nad tím, kde se používají přihlašovací údaje, vytváření ohrožení zabezpečení.

## <a name="kerberos-constrained-delegation"></a>Omezené delegování protokolu Kerberos

Chcete-li druhý segment směrování můžete použít starší verzi omezené delegování (ne založené na prostředcích).

>**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** nastavenou vlastnost není možné delegovat. Další informace najdete v tématu [fokus zabezpečení: analyzování "Účet je citlivý a nelze jej delegovat" pro privilegované účty](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje pro ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Výhody

- Vyžaduje žádné speciální kódování

### <a name="cons"></a>Nevýhody

- Druhé směrování pro WinRM nepodporuje.
- Musí být nakonfigurovaná na objektu služby Active Directory vzdáleného serveru (_ServerB_).
- Je omezená na jednu doménu. Nelze napříč doménami nebo doménovými strukturami.
- Vyžaduje oprávnění aktualizovat objekty a hlavní názvy služby (SPN).

## <a name="resource-based-kerberos-constrained-delegation"></a>Založené na prostředcích omezené delegování protokolu Kerberos

Pomocí protokolu Kerberos založené na prostředcích, omezené delegování (zavedená ve Windows serveru 2012), konfigurace delegování přihlašovacích údajů na objekt serveru, kde jsou umístěny prostředky.
V druhém scénáři segment směrování je popsáno výše, nakonfigurujete _ServerC_ určit, kde bude přijímat delegovaný přihlašovací údaje.

>**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** nastavenou vlastnost není možné delegovat. Další informace najdete v tématu [fokus zabezpečení: analyzování "Účet je citlivý a nelze jej delegovat" pro privilegované účty](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje pro ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Výhody

- Přihlašovací údaje se neukládají.
- Relativně jednoduchá konfigurace pomocí rutin prostředí PowerShell – žádné speciální kódování vyžaduje.
- Je vyžadován přístup žádné speciální domény.
- Funguje napříč doménami a doménovými strukturami.
- Kód Powershellu.

### <a name="cons"></a>Nevýhody

- Vyžaduje systém Windows Server 2012 nebo novější.
- Druhé směrování pro WinRM nepodporuje.
- Vyžaduje oprávnění aktualizovat objekty a hlavní názvy služby (SPN).

### <a name="example"></a>Příklad

Podívejme se na příklad, který konfiguruje prostředků na základě omezené delegování Powershellu _ServerC_ umožňující delegovaná pověření z _ServerB_.
Tento příklad předpokládá, že všechny servery se systémem Windows Server 2012 nebo novější, a aby existovala aspoň jeden řadič domény systému Windows Server 2012 každou doménu, pro kterou žádný ze serverů patří.

Než budete moct nakonfigurovat omezené delegování, je nutné přidat `RSAT-AD-PowerShell` funkcí k instalaci modulu Powershellu pro Active Directory a následným importem tohoto modulu do relace:

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirectory
```
Teď máte několik dostupných rutin **PrincipalsAllowedToDelegateToAccount** parametr:

```powershell
PS C:\> Get-Command -ParameterName PrincipalsAllowedToDelegateToAccount

CommandType Name                 ModuleName
----------- ----                 ----------
Cmdlet      New-ADComputer       ActiveDirectory
Cmdlet      New-ADServiceAccount ActiveDirectory
Cmdlet      New-ADUser           ActiveDirectory
Cmdlet      Set-ADComputer       ActiveDirectory
Cmdlet      Set-ADServiceAccount ActiveDirectory
Cmdlet      Set-ADUser           ActiveDirectory
```

**PrincipalsAllowedToDelegateToAccount** parametr nastaví atributu objektu služby Active Directory **msDS-AllowedToActOnBehalfOfOtherIdentity**, který obsahuje seznam řízení přístupu (ACL), který Určuje, účty, které mají oprávnění k delegování přihlašovacích údajů k souvisejícímu účtu (v našem příkladu bude účet počítače pro _Server_).

Nyní Pojďme vytvořit proměnné, použijeme k reprezentaci servery:

```powershell
# Set up variables for reuse
$ServerA = $env:COMPUTERNAME
$ServerB = Get-ADComputer -Identity ServerB
$ServerC = Get-ADComputer -Identity ServerC
```

Služba WinRM (a tedy vzdálené komunikace Powershellu) ve výchozím nastavení spustí jako účet počítače. Tohle je vidět pohledem **%{StartName/** vlastnost `winrm` služby:

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

Pro _ServerC_ povolit delegování v relaci vzdálené komunikace Powershellu na _ServerB_, jsme udělí přístup tak, že nastavíte **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ objekt počítače _ServerB_:

```powershell
# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB

# Check the value of the attribute directly
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access

# Check the value of the attribute indirectly
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

Kerberos [Key Distribution Center (KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) mezipaměti byl odepřen přístup pokusů (negativní mezipaměť) po dobu 15 minut. Pokud _ServerB_ dříve pokusil o přístup k _ServerC_, budete muset vymazat mezipaměť na _ServerB_ zavoláním následujícího příkazu:

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    klist purge -li 0x3e7
}
```

Může také restartování počítače, nebo počkejte aspoň 15 minut a vymažte mezipaměť.

Po vymazání mezipaměti můžete úspěšně spustit kód z _Server_a_ prostřednictvím _ServerB_ k _ServerC_:

```powershell
# Capture a credential
$cred = Get-Credential Contoso\Alice

# Test kerberos double hop
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {
    Test-Path \\$($using:ServerC.Name)\C$
    Get-Process lsass -ComputerName $($using:ServerC.Name)
    Get-EventLog -LogName System -Newest 3 -ComputerName $($using:ServerC.Name)
}
```

V tomto příkladu `$using` proměnná slouží k Ujistěte se, `$ServerC` proměnná viditelná pro _ServerB_. Další informace o `$using` proměnné, viz [about_Remote_Variables](https://technet.microsoft.com/library/jj149005.aspx).

Povolit více serverů pro delegování přihlašovacích údajů k _ServerC_, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametru u _ServerC_ na pole:

```powershell
# Set up variables for each server
$ServerB1 = Get-ADComputer -Identity ServerB1
$ServerB2 = Get-ADComputer -Identity ServerB2
$ServerB3 = Get-ADComputer -Identity ServerB3
$ServerC  = Get-ADComputer -Identity ServerC

# Grant resource-based Kerberos constrained delegation
Set-ADComputer -Identity $ServerC `
    -PrincipalsAllowedToDelegateToAccount @($ServerB1,$ServerB2,$ServerB3)
```

Pokud chcete, aby druhý segment směrování mezi doménami, přidejte plně kvalifikovaný název domény (FQDN) řadiče domény, domény, ke kterému _ServerB_ patří:

```powershell
# For ServerC in Contoso domain and ServerB in other domain
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com
$ServerC = Get-ADComputer -Identity ServerC
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

Možnost delegování přihlašovacích údajů k ServerC odebrat, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametru u _ServerC_ k `$null`:

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a>Informace o založené na prostředcích omezené delegování protokolu Kerberos

- [Co je nového v ověřování protokolem Kerberos](https://technet.microsoft.com/library/hh831747.aspx)
- [Jak Windows serveru 2012 usnadňuje bolest Kerberos omezeného delegování, část 1](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [Jak Windows serveru 2012 usnadňuje bolest Kerberos omezeného delegování, část 2](https://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [Principy Kerberos omezeného delegování pro nasazení Proxy aplikací Azure Active Directory s ověřováním Windows integrované](https://aka.ms/kcdpaper)
- [[MS-ADA2]: Active Directory schématu atributů M2.210 atribut msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/library/hh554126.aspx)
- [[MS-SFU]: rozšíření protokolu Kerberos: Service for User a protokolu 1.3.2 S4U2proxy omezeného delegování](https://msdn.microsoft.com/library/cc246079.aspx)
- [Prostředek na základě protokolu Kerberos omezeného delegování](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [Vzdálená správa bez použití PrincipalsAllowedToDelegateToAccount omezeného delegování](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a>PSSessionConfiguration pomocí RunAs

Konfigurace relace můžete vytvořit na _ServerB_ a nastavte jeho **RunAsCredential** parametru.

Informace o používání PSSessionConfiguration a spustit jako druhý segment směrování problém vyřešit, najdete v tématu [další řešení s více segmenty směrování vzdálené komunikace Powershellu](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).

### <a name="pros"></a>Výhody

- Funguje s jakýmkoli serverem s WMF 3.0 nebo novější.

### <a name="cons"></a>Nevýhody

- Vyžaduje konfiguraci **PSSessionConfiguration** a **RunAs** na každém serveru zprostředkující (_ServerB_).
- Vyžaduje heslo údržby, pokud používáte doménu **RunAs** účtu

## <a name="just-enough-administration-jea"></a>Funkce Just Enough Administration (JEA)

JEA umožňuje omezit, jaké příkazy můžete spustit správce během relace Powershellu. Slouží k jejich vyřešení druhý segment směrování.

Informace o JEA najdete v tématu [Just Enough Administration](https://docs.microsoft.com/powershell/jea/overview).

### <a name="pros"></a>Výhody

- Žádná Údržba heslo při používání virtuální účet.

### <a name="cons"></a>Nevýhody

- Vyžaduje WMF 5.0 nebo novější.
- Vyžaduje konfiguraci na každém serveru zprostředkující (_ServerB_).

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a>Předávat přihlašovací údaje uvnitř bloku skriptu Invoke-Command

Můžete předat pověření uvnitř **ScriptBlock** parametr volání [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) rutiny.

### <a name="pros"></a>Výhody

- Nevyžaduje server zvláštní konfiguraci.
- Funguje na jakémkoli serveru s WMF 2.0 nebo novější.

### <a name="cons"></a>Nevýhody

- Vyžaduje techniku nevhodnou kódu.
- Pokud používáte WMF 2.0, vyžaduje jinou syntaxi pro předávání argumentů do vzdálené relace.

### <a name="example"></a>Příklad

Následující příklad ukazuje, jak předávat přihlašovací údaje v **Invoke-Command** bloku skriptu:

```powershell
# This works without delegation, passing fresh creds
# Note $Using:Cred in nested request
$cred = Get-Credential Contoso\Administrator
Invoke-Command -ComputerName ServerB -Credential $cred -ScriptBlock {
    hostname
    Invoke-Command -ComputerName ServerC -Credential $Using:cred -ScriptBlock {hostname}
}
```

## <a name="see-also"></a>Viz taky

[Aspekty zabezpečení vzdálené komunikace PowerShellu](WinRMSecurity.md)
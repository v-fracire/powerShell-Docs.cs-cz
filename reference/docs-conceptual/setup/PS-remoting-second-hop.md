---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Vytváření druhé směrování v vzdálenou komunikaci prostředí PowerShell"
ms.openlocfilehash: 2518409369a75a49b975b9b944320c1878819421
ms.sourcegitcommit: 1a0a0928c1e3cae4e8df8d79b0737bd7ed6b4e47
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/21/2017
---
# <a name="making-the-second-hop-in-powershell-remoting"></a>Vytváření druhé směrování v vzdálenou komunikaci prostředí PowerShell

"Druhý směrování problém" odkazuje na situaci takto:

1. Jste přihlášeni k _Server_a_.
2. Z _Server_a_, spouští vzdálenou relaci prostředí PowerShell pro připojení k _ServerB_.
3. Příkaz spustíte v _ServerB_ prostřednictvím vaší vzdálenou komunikaci prostředí PowerShell relace pokusí o přístup k prostředku na _ServerC_.
4. Přístup k danému prostředku na _ServerC_ byl odepřen, protože jste použili k vytvoření relace vzdálenou komunikaci prostředí PowerShell přihlašovací údaje nejsou předat z _ServerB_ k _ServerC_.

Chcete-li vyřešit tento problém několika způsoby. V tomto tématu se podíváme řadu nejoblíbenější řešení druhý problém směrování.

## <a name="credssp"></a>CredSSP

Můžete použít [Credential Security Support Provider (CredSSP)](https://msdn.microsoft.com/en-us/library/windows/desktop/bb931352.aspx) pro ověřování. Zprostředkovatel CredSSP ukládá do mezipaměti přihlašovací údaje na vzdáleném serveru (_ServerB_), takže ho pomocí otevře až útoku krádeží přihlašovacích údajů. Pokud vzdálený počítač v ohrožení, útočník má přístup k přihlašovacím údajům uživatele. Ve výchozím nastavení v počítačích klient i server vypnutá CredSSP. Měli byste povolit zprostředkovatele CredSSP pouze v nejdůvěryhodnější prostředích. Například správce domény připojení k řadiči domény, protože řadič domény je vysoce důvěryhodný.

Další informace o potížích se zabezpečením při použití ověřování CredSSP pro vzdálenou komunikaci prostředí PowerShell najdete v tématu [náhodnému napadení: Pozor CredSSP](http://www.powershellmagazine.com/2014/03/06/accidental-sabotage-beware-of-credssp).

Další informace o útoku krádeží přihlašovacích údajů najdete v tématu [útoky omezení dopadu útoků Pass-the-Hash (PtH) a ostatní krádeží přihlašovacích údajů](https://www.microsoft.com/en-us/download/details.aspx?id=36036).

Příklad toho, jak povolit a používat ověřování CredSSP pro vzdálenou komunikaci prostředí PowerShell naleznete v části [pomocí zprostředkovatele CredSSP sekundu směrování problém vyřešit](https://blogs.technet.microsoft.com/heyscriptingguy/2012/11/14/enable-powershell-second-hop-functionality-with-credssp/).

### <a name="pros"></a>Výhody

- Funguje pro všechny servery se systémem Windows Server 2008 nebo novějším.

### <a name="cons"></a>Nevýhody

- Má slabší zabezpečení.
- Vyžaduje konfiguraci rolí klient i server.

## <a name="kerberos-delegation-unconstrained"></a>Delegování protokolu Kerberos (neomezeného)

Delegování protokolu Kerberos neomezeného můžete také použít k nastavení připojení přes další počítač. Tato metoda poskytuje však žádné řízení použití delegovanými přihlašovacími údaji.

>**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** sada vlastností není možné delegovat. Další informace najdete v tématu [fokus zabezpečení: analýzy 'Účet je citlivý a nelze jej delegovat' k privilegovaným účtům](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Výhody

- Vyžaduje žádné speciální kódování.

### <a name="cons"></a>Nevýhody

- Pro WinRM nepodporuje připojení přes další počítač.
- Poskytuje žádnou kontrolu nad použití přihlašovacích údajů, vytváření ohrožení zabezpečení.

## <a name="kerberos-constrained-delegation"></a>Omezené delegování protokolu Kerberos

Chcete-li druhé směrování můžete starší verze omezené delegování (není založené na prostředcích). 

>**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** sada vlastností není možné delegovat. Další informace najdete v tématu [fokus zabezpečení: analýzy 'Účet je citlivý a nelze jej delegovat' k privilegovaným účtům](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Výhody

- Vyžaduje žádné speciální kódování

### <a name="cons"></a>Nevýhody

- Pro WinRM nepodporuje připojení přes další počítač.
- Musí být nakonfigurované na objektu služby Active Directory vzdáleného serveru (_ServerB_).
- Omezeno na jednu doménu. Nelze napříč doménami nebo doménovými strukturami.
- Vyžaduje práva k aktualizaci objekty a hlavní názvy služby (SPN).

## <a name="resource-based-kerberos-constrained-delegation"></a>Na základě prostředků omezené delegování protokolu Kerberos

Pomocí protokolu Kerberos založené na prostředcích omezeného delegování (zavedená v systému Windows Server 2012), konfigurace delegování přihlašovacích údajů na objekt serveru, kde jsou umístěny prostředky.
Druhý scénář směrování popsané výše, nakonfigurujete _ServerC_ zadejte, kde bude přijímat delegované přihlašovací údaje.

>**Poznámka:** účtů služby Active Directory, které mají **účet je citlivý a nelze jej delegovat** sada vlastností není možné delegovat. Další informace najdete v tématu [fokus zabezpečení: analýzy 'Účet je citlivý a nelze jej delegovat' k privilegovaným účtům](https://blogs.technet.microsoft.com/poshchap/2015/05/01/security-focus-analysing-account-is-sensitive-and-cannot-be-delegated-for-privileged-accounts/) a [nástroje ověřování protokolu Kerberos a nastavení](https://technet.microsoft.com/library/cc738673(v=ws.10).aspx)

### <a name="pros"></a>Výhody

- Přihlašovací údaje se neukládají.
- Relativně jednoduchá konfigurace pomocí rutin prostředí PowerShell – žádné speciální kódování vyžaduje.
- Je vyžadován přístup žádné speciální domény.
- Funguje napříč doménami a doménovými strukturami.
- Kód prostředí PowerShell.

### <a name="cons"></a>Nevýhody

- Vyžaduje systém Windows Server 2012 nebo novějším.
- Pro WinRM nepodporuje připojení přes další počítač.
- Vyžaduje práva k aktualizaci objekty a hlavní názvy služby (SPN). 

### <a name="example"></a>Příklad

Podívejme se na příklad, který konfiguruje prostředků na základě omezené delegování prostředí PowerShell _ServerC_ umožňující delegovanými přihlašovacími údaji ze _ServerB_.
Tento příklad předpokládá, že všechny servery se systémem Windows Server 2012 nebo novější, a jestli je aspoň jeden řadič domény systému Windows Server 2012 každou doménu, do které žádné servery patří.

Než budete moct nakonfigurovat omezené delegování, je nutné přidat `RSAT-AD-PowerShell` funkci nainstalovat modul prostředí PowerShell služby Active Directory a potom tento modul importovat do relace:

```powershell
PS C:\> Add-WindowsFeature RSAT-AD-PowerShell

PS C:\> Import-Module ActiveDirector
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

**PrincipalsAllowedToDelegateToAccount** parametr nastaví atributu objektu služby Active Directory **msDS-AllowedToActOnBehalfOfOtherIdentity**, který obsahuje seznam řízení přístupu (ACL), Určuje, které účty mají oprávnění delegovat přihlašovací údaje pro přidružený účet (v našem příkladu bude účet počítače pro _Server_).

Nyní nastavíme proměnné použijeme představují servery:

```powershell
# Set up variables for reuse            
$ServerA = $env:COMPUTERNAME            
$ServerB = Get-ADComputer -Identity ServerB            
$ServerC = Get-ADComputer -Identity ServerC            
```

WinRM (a proto vzdálenou komunikaci prostředí PowerShell) ve výchozím nastavení spustí jako účet počítače. Můžete to vidět prohlížením **%{StartName/** vlastnost `winrm` služby:

```powershell
PS C:\> Get-WmiObject win32_service -filter 'name="winrm"' | Format-List StartName

StartName : NT AUTHORITY\NetworkService
```

Pro _ServerC_ na povolit delegování z relace vzdálenou komunikaci prostředí PowerShell _ServerB_, jsme udělí přístup nastavením **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ na objekt počítače z _ServerB_:

```powershell
# Grant resource-based Kerberos constrained delegation            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB            
            
# Check the value of the attribute directly            
$x = Get-ADComputer -Identity $ServerC -Properties msDS-AllowedToActOnBehalfOfOtherIdentity            
$x.'msDS-AllowedToActOnBehalfOfOtherIdentity'.Access            
            
# Check the value of the attribute indirectly            
Get-ADComputer -Identity $ServerC -Properties PrincipalsAllowedToDelegateToAccount
```

Protokolu Kerberos [Key Distribution (Center KDC)](https://msdn.microsoft.com/library/windows/desktop/aa378170(v=vs.85).aspx) mezipamětí odepřen pokusů o přístup (negativní mezipaměť) 15 minut. Pokud _ServerB_ dříve pokusil o přístup k _ServerC_, budete muset vymazat mezipaměť na _ServerB_ vyvoláním následující příkaz:

```powershell
Invoke-Command -ComputerName $ServerB.Name -Credential $cred -ScriptBlock {            
    klist purge -li 0x3e7            
}
```

Můžete také restartovat počítač, nebo počkejte alespoň 15 minut a vymažte mezipaměť.

Po vymazání mezipaměti, je možné úspěšně spustit kód z _Server_a_ prostřednictvím _ServerB_ k _ServerC_:

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

V tomto příkladu `$using` proměnná se používá k zajištění `$ServerC` proměnné, které jsou viditelné pro _ServerB_. Další informace o `$using` proměnné, viz [about_Remote_Variables](https://technet.microsoft.com/en-us/library/jj149005.aspx).

Povolit více serverů pro přihlašovací údaje pro delegování _ServerC_, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ do pole:

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

Pokud chcete, aby druhé směrování mezi doménami, přidejte plně kvalifikovaný název domény (FQDN) řadiče domény, domény, ke kterému _ServerB_ patří:

```powershell
# For ServerC in Contoso domain and ServerB in other domain            
$ServerB = Get-ADComputer -Identity ServerB -Server dc1.alpineskihouse.com            
$ServerC = Get-ADComputer -Identity ServerC            
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $ServerB
```

Chcete-li odebrat možnost delegovat přihlašovací údaje pro ServerC, nastavte hodnotu **PrincipalsAllowedToDelegateToAccount** parametr na _ServerC_ k `$null`:

```powershell
Set-ADComputer -Identity $ServerC -PrincipalsAllowedToDelegateToAccount $null
```

### <a name="information-on-resource-based-kerberos-constrained-delegation"></a>Informace o založené na prostředcích omezené delegování protokolu Kerberos

- [Co je nového v ověřování protokolem Kerberos](https://technet.microsoft.com/library/hh831747.aspx)
- [Jak Windows Server 2012 usnadňuje problémové Kerberos omezeného delegování, část 1](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-1)
- [Jak Windows Server 2012 usnadňuje problémové Kerberos omezeného delegování, část 2](http://windowsitpro.com/security/how-windows-server-2012-eases-pain-kerberos-constrained-delegation-part-2)
- [Principy protokolu Kerberos omezeného delegování pro nasazení Proxy aplikace služby Azure Active Directory pomocí integrovaného ověřování systému Windows](http://aka.ms/kcdpaper)
- [[MS-ADA2]: Active Directory schématu atributů M2.210 atribut msDS-AllowedToActOnBehalfOfOtherIdentity](https://msdn.microsoft.com/en-us/library/hh554126.aspx)
- [[MS-SFU]: rozšíření protokolu Kerberos: Service for User a protokolu 1.3.2 S4U2proxy omezeného delegování](https://msdn.microsoft.com/en-us/library/cc246079.aspx)
- [Prostředků na základě protokolu Kerberos omezeného delegování](https://blog.kloud.com.au/2013/07/11/kerberos-constrained-delegation/)
- [Vzdálená správa bez použití PrincipalsAllowedToDelegateToAccount omezeného delegování](https://blogs.msdn.microsoft.com/taylorb/2012/11/06/remote-administration-without-constrained-delegation-using-principalsallowedtodelegatetoaccount/)

## <a name="pssessionconfiguration-using-runas"></a>PSSessionConfiguration použitím RunAs

Konfigurace relace můžete vytvořit na _ServerB_ a nastavit jeho **RunAsCredential** parametr.

Informace o používání PSSessionConfiguration a RunAs druhý směrování problém vyřešit, najdete v článku [jiné řešení pro vzdálenou komunikaci prostředí PowerShell vícenásobného předávání](https://blogs.msdn.microsoft.com/sergey_babkins_blog/2015/03/18/another-solution-to-multi-hop-powershell-remoting/).

### <a name="pros"></a>Výhody

- Funguje s jakýmkoli serverem s WMF 3.0 nebo novější.

### <a name="cons"></a>Nevýhody

- Vyžaduje konfiguraci **PSSessionConfiguration** a **RunAs** na každém serveru, zprostředkující (_ServerB_).
- Vyžaduje heslo údržby, pokud používáte doménu **RunAs** účtu

## <a name="just-enough-administration-jea"></a>Akorát správy (JEA)

JEA umožňuje omezit jaké příkazy můžete spustit správce během relace prostředí PowerShell. Může sloužit k jejich vyřešení druhý směrování.

Informace o JEA najdete v tématu [právě dostatečně správy](https://docs.microsoft.com/en-us/powershell/jea/overview).

### <a name="pros"></a>Výhody

- Žádná Údržba heslo při použití virtuální účet.

### <a name="cons"></a>Nevýhody

- Vyžaduje WMF 5.0 nebo novější.
- Vyžaduje konfiguraci na každém serveru, zprostředkující (_ServerB_).

## <a name="pass-credentials-inside-an-invoke-command-script-block"></a>Předávat přihlašovací údaje uvnitř bloku skriptu Invoke-Command

Můžete předat pověření uvnitř **ScriptBlock** parametr volání [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) rutiny.

### <a name="pros"></a>Výhody

- Nevyžaduje konfiguraci speciální serveru.
- Funguje na všechny servery se spuštěným WMF 2.0 nebo novější.

### <a name="cons"></a>Nevýhody

- Vyžaduje technika nevhodných kódu.
- Pokud systém WMF 2.0, vyžaduje jinou syntaxi pro předání argumentů ke vzdálené relaci.

### <a name="example"></a>Příklad

Následující příklad ukazuje, jak předat přihlašovací údaje v **Invoke-Command** bloku skriptu:

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








 

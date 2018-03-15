---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: WinRMSecurity
ms.openlocfilehash: 0522844fded847a3fd45c1b3890a141357edb2b2
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="powershell-remoting-security-considerations"></a>Důležité informace o zabezpečení pro vzdálenou komunikaci prostředí PowerShell

Vzdálená komunikace prostředí PowerShell je doporučeným způsobem, jak spravovat systémy Windows. Ve výchozím nastavení v systému Windows Server 2012 R2 je povolena vzdálená komunikace prostředí PowerShell. Tento dokument popisuje aspekty zabezpečení, doporučení a osvědčené postupy při použití vzdálenou komunikaci prostředí PowerShell.

## <a name="what-is-powershell-remoting"></a>Co je Vzdálená komunikace prostředí PowerShell?

Používá vzdálenou komunikaci prostředí PowerShell [Vzdálená správa systému Windows (WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx), což je implementaci společnosti Microsoft [webové služby pro správu (WS-Management)](http://www.dmtf.org/sites/default/files/standards/documents/DSP0226_1.2.0.pdf) protokol, aby uživatelé mohli spustit prostředí PowerShell příkazy na vzdálených počítačích. Můžete najít další informace o používání vzdálenou komunikaci prostředí PowerShell v [spuštění vzdálené příkazy](https://technet.microsoft.com/library/dd819505.aspx).

Vzdálená komunikace prostředí PowerShell není stejná jako **ComputerName** parametru rutiny ji spustit na vzdáleném počítači, který používá vzdálené volání procedur (RPC) jako jeho základního protokolu.

## <a name="powershell-remoting-default-settings"></a>Výchozí nastavení vzdálenou komunikaci prostředí PowerShell

Vzdálená komunikace prostředí PowerShell (a WinRM) naslouchat na následující porty:

- HTTP: 5985
- HTTPS: 5986

Ve výchozím nastavení umožňuje vzdálenou komunikaci prostředí PowerShell připojení pouze z členy skupiny Administrators. Relace se spustí v kontextu uživatele, tak, aby všechny řízení přístupu operačního systému použít pro jednotlivé uživatele a skupiny nadále platí pro ně během připojení přes vzdálenou komunikaci prostředí PowerShell.

Výchozí pravidlo brány Windows Firewall pro vzdálenou komunikaci prostředí PowerShell v privátní síti, přijme všechna připojení. Výchozí pravidlo brány Windows Firewall na veřejných sítích, umožňuje vzdálenou komunikaci prostředí PowerShell připojení pouze z ve stejné podsíti. Budete muset explicitně změnit daného pravidla otevřít vzdálenou komunikaci prostředí PowerShell pro všechna připojení ve veřejné síti.

>**Upozornění:** pravidlo brány firewall pro veřejné sítě je určená k ochraně počítače z pokusy o potenciálně škodlivého externí připojení. Buďte opatrní při odebírání toto pravidlo.

## <a name="process-isolation"></a>Proces izolace

Používá vzdálenou komunikaci prostředí PowerShell [Vzdálená správa systému Windows (WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426) pro komunikaci mezi počítači. WinRM spuštěn jako služba pod účtem Network Service a vytvoří izolovaných procesech systémem jako uživatelské účty do instance hostitele prostředí PowerShell. Instance prostředí PowerShell spuštěna jako jeden uživatel nemá přístup k procesu spuštěného instance prostředí PowerShell jako jiný uživatel.

## <a name="event-logs-generated-by-powershell-remoting"></a>Protokoly událostí generovaných vzdálenou komunikaci prostředí PowerShell

FireEye poskytl dobrý souhrn protokoly událostí a dalších zabezpečení důkaz generované vzdálenou komunikaci prostředí PowerShell relace, která je k dispozici na  
[Útoky na odstranění příčin prostředí PowerShell](https://www.fireeye.com/content/dam/fireeye-www/global/en/solutions/pdfs/wp-lazanciyan-investigating-powershell-attacks.pdf).

## <a name="encryption-and-transport-protocols"></a>Šifrování a přenosu protokolů

Je vhodné zvážit zabezpečení připojení vzdálenou komunikaci prostředí PowerShell za dvou hledisek: počáteční ověřování a nepřetržitě komunikují. 

Bez ohledu na přenos protokol použitý (HTTP nebo HTTPS) vzdálenou komunikaci prostředí PowerShell vždy šifruje veškerou komunikaci po počáteční ověřování symetrickým klíčem relace AES 256.
    
### <a name="initial-authentication"></a>Počáteční ověřování

Ověřování potvrdí identitu klienta a serveru – v ideálním případě - serveru do klienta.
    
Pokud se klient připojí k doméně serveru pomocí názvu počítače (tj: server01, nebo server01.contoso.com), je výchozím ověřovacím protokolem [Kerberos](https://msdn.microsoft.com/library/windows/desktop/aa378747.aspx).
Protokol Kerberos zaručuje identity uživatele i identitu serveru bez odeslání žádné řazení opakovaně použitelné přihlašovacích údajů.

Pokud se klient připojuje k serveru domény pomocí jeho IP adresy nebo připojuje k serveru pracovní skupiny, není možné ověřování pomocí protokolu Kerberos. V takovém případě vzdálenou komunikaci prostředí PowerShell spoléhá na [ověřovací protokol NTLM](https://msdn.microsoft.com/library/windows/desktop/aa378749.aspx). Ověřovací protokol NTLM zaručuje bez odeslání žádné řazení přidělitelný přihlašovací údaje identity uživatele. K prokázání identity uživatele, protokol NTLM vyžaduje, že klient i server výpočetní klíče relace z hesla uživatele bez někdy výměna heslo samotné. Server obvykle neví heslo uživatele, takže komunikuje s řadiči domény, který znát heslo uživatele a vypočítá klíče relace pro server. 
      
Protokol NTLM, ale nezaručí identitu serveru. Stejně jako u všechny protokoly pro ověřování používat protokol NTLM, může útočník má přístup k účtu počítače připojené k doméně počítače vyvolání řadiče domény výpočetní NTLM-klíčem relace a zosobnit serveru.

Ověřování pomocí protokolu NTLM je ve výchozím nastavení zakázané, ale může být buď konfiguraci protokolu SSL na cílovém serveru nebo konfigurace nastavení WinRM TrustedHosts na straně klienta povoleno.
    
#### <a name="using-ssl-certificates-to-validate-server-identity-during-ntlm-based-connections"></a>Používání certifikátů SSL k ověření identity serveru během připojení pomocí protokolu NTLM

Vzhledem k tomu, že ověřovací protokol NTLM, nebude moct zajistit identity cílového serveru (pouze to, že zná již vaše heslo), můžete nakonfigurovat cílové servery používat protokol SSL pro vzdálenou komunikaci prostředí PowerShell. Přiřazení certifikát SSL k cílovému serveru (Pokud je vydaný certifikační autoritou, která klient také důvěřuje) umožňuje ověření protokolem NTLM, která zaručí identity uživatele i identitu serveru.
    
#### <a name="ignoring-ntlm-based-server-identity-errors"></a>Ignorování chyb identita serveru na základě protokolu NTLM
      
Pokud nasazení certifikát SSL k serveru pro připojení protokolu NTLM je nemožné, může potlačit výsledné chyby identity přidáním serveru do služby WinRM **TrustedHosts** seznamu. Upozorňujeme, že přidáte do seznamu TrustedHosts název serveru, který by se neměla považovat jako jakoukoli formu prohlášení o důvěryhodnost hostitelů sami – jsou jako ověřovací protokol NTLM nemůže zaručit, že je ve skutečnosti připojení k hostiteli hodláte připojit k.
Místo toho byste měli zvážit nastavení TrustedHosts být seznamu hostitelů, pro které chcete potlačit chybě, tím, že nelze ověřit identitu serveru.
    
    
### <a name="ongoing-communication"></a>Probíhající komunikace

Po dokončení počáteční ověřování [protokol vzdálenou komunikaci prostředí PowerShell](https://msdn.microsoft.com/en-us/library/dd357801.aspx) šifruje všechny probíhající komunikaci symetrickým klíčem relace AES 256.  


## <a name="making-the-second-hop"></a>Vytváření druhé směrování

Ve výchozím nastavení použije vzdálenou komunikaci prostředí PowerShell (Pokud je k dispozici) pomocí protokolu Kerberos nebo NTLM pro ověření. Obě tyto protokoly ověřování ke vzdálenému počítači bez odeslání přihlašovacích údajů k němu.
Toto je nejbezpečnější způsob ověření, ale protože vzdálený počítač nemá přihlašovacích údajů uživatele, nemůže přistupovat k jiným počítačům a službám jménem uživatele. To se označuje jako "druhý směrování problém".

K tomuto problému nedošlo několika způsoby. Popis těchto metod a výhody a nevýhody jednotlivých najdete v tématu [provedení připojení přes další počítač v vzdálenou komunikaci prostředí PowerShell](PS-remoting-second-hop.md).











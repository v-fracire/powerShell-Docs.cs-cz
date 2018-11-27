---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: WinRMSecurity
ms.openlocfilehash: 59717e4806857e6760de523335bbee6028da8e84
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320546"
---
# <a name="powershell-remoting-security-considerations"></a>Aspekty zabezpečení vzdálené komunikace Powershellu

Vzdálená komunikace Powershellu je doporučeným způsobem správy systémů Windows. Vzdálená komunikace Powershellu je povolené ve výchozím nastavení ve Windows serveru 2012 R2. Tento dokument popisuje otázky zabezpečení, doporučení a osvědčené postupy při použití vzdálené komunikace Powershellu.

## <a name="what-is-powershell-remoting"></a>Co je Vzdálená komunikace Powershellu?

Používá vzdálené komunikace Powershellu [Vzdálená správa Windows (WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx), což je implementace společnosti Microsoft [Web Services for Management (WS-Management)](https://www.dmtf.org/sites/default/files/standards/documents/DSP0226_1.2.0.pdf) protokol, chcete-li povolit uživatelům spustit prostředí PowerShell příkazy ve vzdálených počítačích. Můžete najít další informace o použití vzdálené komunikace Powershellu na [spouštění vzdálených příkazů](https://technet.microsoft.com/library/dd819505.aspx).

Vzdálená komunikace Powershellu není stejný jako při použití **ComputerName** parametru rutiny pro spuštění na vzdáleném počítači, který používá vzdálené volání procedur (RPC) jako jeho základní protokol.

## <a name="powershell-remoting-default-settings"></a>Výchozí nastavení vzdálené komunikace Powershellu

Vzdálená komunikace Powershellu (a WinRM) naslouchat následující porty:

- HTTP: 5985
- HTTPS: 5986

Ve výchozím nastavení umožňuje vzdálenou komunikaci prostředí PowerShell připojení pouze z členy skupiny Administrators. Relace jsou spouštěny v kontextu uživatele tak, aby všechny ovládací prvky přístupu operačního systému u jednotlivých uživatelů a skupin pokračovat v používání k nim připojeny přes vzdálenou komunikaci prostředí PowerShell.

Výchozí pravidlo brány Windows Firewall pro vzdálenou komunikaci prostředí PowerShell v privátní síti, přijme všechna připojení. Výchozí pravidlo brány Windows Firewall ve veřejných sítích, umožňuje vzdálené komunikace Powershellu připojení pouze z v rámci stejné podsíti. Je nutné explicitně změnit tímto pravidlem otevřít vzdálenou komunikaci prostředí PowerShell pro všechna připojení ve veřejné síti.

>**Upozornění:** pravidlo brány firewall pro veřejné sítě je určená k ochraně počítače před pokusy o potenciálně škodlivém externí připojení. Buďte opatrní při odebírání tohoto pravidla.

## <a name="process-isolation"></a>Izolace procesů

Používá vzdálené komunikace Powershellu [Vzdálená správa Windows (WinRM)](https://msdn.microsoft.com/library/windows/desktop/aa384426) pro komunikaci mezi počítači.
Služba WinRM běží jako služba pod účtem Network Service a vytvoří izolovaných procesech spuštěný jako uživatelské účty do instance hostitele prostředí PowerShell. Instance powershellu spouštěné jako jeden uživatel nemá přístup k procesu spuštěnému jako jiný uživatel instance prostředí PowerShell.

## <a name="event-logs-generated-by-powershell-remoting"></a>Protokoly událostí generované vzdálené komunikace Powershellu

Poskytuje dobrý přehled protokolů událostí a jiný doklad o zabezpečení generovaných relací vzdálené komunikace Powershellu, k dispozici na FireEye [vyšetřování útoků Powershellu](https://www.fireeye.com/content/dam/fireeye-www/global/en/solutions/pdfs/wp-lazanciyan-investigating-powershell-attacks.pdf).

## <a name="encryption-and-transport-protocols"></a>Šifrování a přenosu protokolů

Je dobré zvážit zabezpečení vzdálené komunikace Powershellu připojení za dvou hledisek: počáteční ověřování a nepřetržitě komunikují.

Bez ohledu na to, přenosový protokol používá (HTTP nebo HTTPS) vzdálené komunikace Powershellu vždy šifruje veškerá komunikace po počáteční ověřování symetrickým klíčem relace AES-256.

### <a name="initial-authentication"></a>Počáteční ověřování

Ověřování potvrdí identitu klienta a server – v ideálním případě - serveru do klienta.

Pokud se klient připojí k doméně serveru pomocí názvu počítače (například: server01, nebo server01.contoso.com), je výchozím ověřovacím protokolem [Kerberos](https://msdn.microsoft.com/library/windows/desktop/aa378747.aspx).
Protokol Kerberos zaručuje identity uživatele i identitu serveru bez odeslání jakýkoli druh opakovaně použitelné přihlašovací údaje.

Pokud se klient připojí k doméně serveru pomocí jeho IP adresu nebo se připojí k serveru pracovní skupiny, není možné ověřování pomocí protokolu Kerberos. V takovém případě využívá vzdálené komunikace Powershellu [ověřovací protokol NTLM](https://msdn.microsoft.com/library/windows/desktop/aa378749.aspx). Ověřovací protokol NTLM zaručuje identitu uživatele bez odeslání jakýkoli druh s možností delegování přihlašovacích údajů. K prokázání identity uživatele, vyžaduje protokol NTLM, že klient i server compute klíč relace z hesla uživatele bez někdy výměna heslo samotné. Server obvykle nezná heslo uživatele, tak komunikaci s řadičem domény, který znáte heslo uživatele a vypočítá klíč relace pro server.

Protokol NTLM, ale nezaručuje identity serveru. Stejně jako všechny protokoly pro ověřování pomocí protokolu NTLM, může vyvolat útočník s přístupem k účtu počítače připojené k doméně počítače řadiče domény compute NTLM klávesami relace a zosobnit serveru.

Ověřování pomocí protokolu NTLM je ve výchozím nastavení zakázané, ale může být buď konfiguraci protokolu SSL na cílovém serveru nebo konfigurace nastavení hlavního názvu služby WinRM TrustedHosts na straně klienta povoleno.

#### <a name="using-ssl-certificates-to-validate-server-identity-during-ntlm-based-connections"></a>Používání certifikátů SSL pro ověření identity serveru během připojení pomocí protokolu NTLM

Protože ověřování protokolu NTLM nemůže zajistit identita cílového serveru (pouze, že ji už zná heslo), můžete nakonfigurovat cílových serverů pro použití protokolu SSL pro vzdálenou komunikaci prostředí PowerShell. Přiřazení certifikátu SSL na cílový server (Pokud vydaného certifikační autoritou, která klient také vztahy důvěryhodnosti) umožňuje ověřování NTLM, které zaručují identity uživatele i identitu serveru.

#### <a name="ignoring-ntlm-based-server-identity-errors"></a>Ignorování chyb identita serveru na základě protokolu NTLM

Pokud nasazení certifikátu SSL k serveru pro připojení protokolu NTLM je nemožné, může potlačit výsledné chyby identity tak, že přidáte server do služby WinRM **TrustedHosts** seznamu. Mějte prosím na paměti, že přidání názvu serveru do seznamu TrustedHosts by neměla považovat za jakoukoli podobu příkazu důvěryhodnost hostitelů sami – jsou jako ověřovací protokol NTLM nemůže zaručit, že se skutečně připojujete k hostiteli hodláte připojit.
Místo toho byste měli zvážit TrustedHosts nastavení bude seznam hostitelů, pro které chcete potlačit chyby generované se nelze ověřit identitu serveru.


### <a name="ongoing-communication"></a>Probíhající komunikace

Po dokončení počáteční ověřování [protokolu vzdálené komunikace Powershellu](https://msdn.microsoft.com/library/dd357801.aspx) šifruje všechny probíhající komunikace symetrickým klíčem relace AES-256.


## <a name="making-the-second-hop"></a>Druhé směrování

Ve výchozím nastavení použije Vzdálená komunikace Powershellu (Pokud je k dispozici) pomocí protokolu Kerberos nebo NTLM pro ověření. Obě tyto protokoly ověřování ke vzdálenému počítači bez odeslání přihlašovacích údajů k němu.
Toto je nejbezpečnější způsob ověření, ale protože vzdálený počítač nemá žádné přihlašovací údaje uživatele, nemá přístup k jiným počítačům a službám v zastoupení uživatele.
To se označuje jako "druhý segment směrování problém".

Existuje několik způsobů, jak tomuto problému zabráníte tak. Popis těchto metod a profesionály v oboru a nevýhody jednotlivých najdete v tématu [– díky tomu druhé směrování vzdálené komunikace Powershellu](PS-remoting-second-hop.md).
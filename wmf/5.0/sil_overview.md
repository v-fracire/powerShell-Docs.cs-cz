---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: e7198999c17b5c0d77724a82b322e6485065225e
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/07/2018
ms.locfileid: "34482841"
---
# <a name="software-inventory-logging-sil"></a>Protokolování softwarového inventáře (SIL)

**Důležité:** *při instalaci WMF 5.0 na Server Windows Server 2012 R2, který je již spuštěna SIL, je nutné spuštěním rutiny Start-SilLogging po instalaci WMF, protože proces instalace se zastaví errantly Funkce protokolování inventáře softwaru.*

Protokolování inventáře softwaru pomáhá snižovat provozních nákladů na získávání přesných informací o softwaru společnosti Microsoft, které jsou nainstalovány místně na serveru, ale hlavně napříč mnoha servery v IT prostředí (za předpokladu, že je software nainstalován a spuštěn IT prostředí). Pokud má nějaký nastavený, můžete předávat tato data agregačnímu serveru a shromažďovat data protokolu na jednom místě pomocí jednotným, automatickým procesem.

Přestože můžete také protokolovat data inventáře softwaru přímým dotazováním každého počítače, protokolování inventáře softwaru díky využití architektury předávání (přes síť) iniciované na každém serveru umožňuje předcházet problémy zjišťování serveru, které jsou typické pro mnoho Inventář a asset scénářů správy softwarových. Protokolování inventáře softwaru se používá protokol SSL k zabezpečení dat, který je předávaných přes HTTPS do agregačního serveru. Ukládání dat v jednom místě snadněji manipuluje, snadněji se analyzují manipulaci a sdílené složky, pokud je to nezbytné.

Žádná tato data se společnosti Microsoft v rámci fungování funkce neodesílají. Data a funkce Protokolování inventáře softwaru jsou určené výhradně pro potřeby licencovaného vlastníka a správců serverového softwaru.

Další informace a dokumentaci o rutinách protokolování inventáře softwaru, najdete v části Windows Server 2012 R2 online prostředky v <http://technet.microsoft.com/library/dn383584.aspx>.

---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 4a2dfd651f1c74e7441e5f5e357c1c26453adc07
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="software-inventory-logging-sil"></a>(SIL) protokolování inventáře softwaru

** Důležité: ** *při instalaci WMF 5.0 na Server Windows Server 2012 R2, který je již spuštěna SIL, je nutné spuštěním rutiny Start-SilLogging po instalaci WMF, protože proces instalace se zastaví errantly softwaru Funkce protokolování inventáře.*

Protokolování inventáře softwaru pomáhá snižovat provozních nákladů na získávání přesných informací o softwaru společnosti Microsoft, které jsou nainstalovány místně na serveru, ale hlavně napříč mnoha servery v IT prostředí (za předpokladu, že je software nainstalován a spuštěn IT prostředí). Pokud má nějaký nastavený, můžete předávat tato data agregačnímu serveru a shromažďovat data protokolu na jednom místě pomocí jednotným, automatickým procesem.

Přestože můžete také protokolovat data inventáře softwaru přímým dotazováním každého počítače, protokolování inventáře softwaru díky využití architektury předávání (přes síť) iniciované na každém serveru umožňuje předcházet problémy zjišťování serveru, které jsou typické pro mnoho Inventář a asset scénářů správy softwarových. Protokolování inventáře softwaru se používá protokol SSL k zabezpečení dat, který je předávaných přes HTTPS do agregačního serveru. Ukládání dat v jednom místě snadněji manipuluje, snadněji se analyzují manipulaci a sdílené složky, pokud je to nezbytné.

Žádná tato data se společnosti Microsoft v rámci fungování funkce neodesílají. Data a funkce Protokolování inventáře softwaru jsou určené výhradně pro potřeby licencovaného vlastníka a správců serverového softwaru.

Další informace a dokumentaci o rutinách protokolování inventáře softwaru, najdete v části Windows Server 2012 R2 online prostředky v <http://technet.microsoft.com/library/dn383584.aspx>.


---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 4c2a3fb15b108f1a8e9fd271a620bcb1cb8c77ed
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="mof-documents-are-encrypted-by-default"></a>Ve výchozím nastavení jsou zašifrované dokumenty MOF

Konfigurace dokumenty obsahují citlivé informace. V předchozích verzích DSC bylo potřeba distribuovat a spravovat certifikáty při zabezpečování přihlašovacích údajů v konfiguraci. Pro mnoho bylo zatížení významné správy, i se všemi práce trvalo k tomu, které byly stále ponechaná na některé konfigurační informace, které není a nebylo zabezpečené.

Který je už tento případ, protože **všechny konfigurace ve výchozím nastavení jsou zabezpečené soubory MOF**. Žádné certifikáty nebo meta konfigurační nastavení, je potřeba. Kdykoli se konfigurace MOF je uložen na disk pomocí místní Configuration Manager (LCM) na cílový uzel, je zašifrovaná. Soubory MOF jsou šifrované pomocí [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx). **Poznámka:** soubory MOF generované konfigurační skript nejsou šifrovány.

**Příklad:** šifrování v režimu nabízení ![MOF šifrování](../images/MOF_Encryption.jpg)

Pokud už používáte metodu certifikát pro šifrování hesla nebo pokud potřebujete další zabezpečení pro hesla, [stávající metodu šifrování na základě certifikátů](https://msdn.microsoft.com/powershell/dsc/securemof) budou nadále fungovat. Výsledkem bude dokument MOF, který je plně zašifrované pomocí DPAPIs a dále používat hesla šifrované v něm.

Toto šifrování se vztahuje pouze na dokumenty MOF konfigurace (pending.mof, current.mof, previous.mof a částečné soubory MOF). Soubory MOF meta konfigurace jsou stále uložit ve formátu prostého textu, vzhledem k tomu, že obsahují menší pravděpodobně tajných klíčů.

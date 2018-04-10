---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 85982027ba1c967d3ec9b099300509cf5761807b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="mof-documents-are-encrypted-by-default"></a>Ve výchozím nastavení jsou zašifrované dokumenty MOF

Konfigurace dokumenty obsahují citlivé informace. V předchozích verzích DSC bylo potřeba distribuovat a spravovat certifikáty při zabezpečování přihlašovacích údajů v konfiguraci. Pro mnoho bylo zatížení významné správy, i se všemi práce trvalo k tomu, které byly stále ponechaná na některé konfigurační informace, které není a nebylo zabezpečené.

Který je už tento případ, protože **všechny konfigurace ve výchozím nastavení jsou zabezpečené soubory MOF**. Žádné certifikáty nebo meta konfigurační nastavení, je potřeba. Kdykoli se konfigurace MOF je uložen na disk pomocí místní Configuration Manager (LCM) na cílový uzel, je zašifrovaná. Soubory MOF jsou šifrované pomocí [DPAPI](https://msdn.microsoft.com/library/ms995355.aspx). **Poznámka:** soubory MOF generované konfigurační skript nejsou šifrovány.

**Příklad:** šifrování v režimu nabízení ![MOF šifrování](../images/MOF_Encryption.jpg)

Pokud už používáte metodu certifikát pro šifrování hesla nebo pokud potřebujete další zabezpečení pro hesla, [stávající metodu šifrování na základě certifikátů](https://msdn.microsoft.com/powershell/dsc/securemof) budou nadále fungovat. Výsledkem bude dokument MOF, který je plně zašifrované pomocí DPAPIs a dále používat hesla šifrované v něm.

Toto šifrování se vztahuje pouze na dokumenty MOF konfigurace (pending.mof, current.mof, previous.mof a částečné soubory MOF). Soubory MOF meta konfigurace jsou stále uložit ve formátu prostého textu, vzhledem k tomu, že obsahují menší pravděpodobně tajných klíčů.
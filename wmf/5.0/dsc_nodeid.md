---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 6d94de2d3f2c551219d8fbe5badb6e5bb913d796
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="separation-of-node-and-configuration-ids"></a>Oddělení ID uzlu od ID konfigurace

## <a name="overview"></a>Přehled

Aby bylo možné poskytnout více flexibilní a efektivní prostředí při používání DSC v režimu pro vyžádání obsahu, jsme přidali celou řadu funkcí v této verzi. Tyto funkce jsou určeny k umožňují flexibilně snadno nastavit a nasadit konfigurace napříč několika uzly, i když stále sledování stavu a vytváření sestav informace pro každý uzel zvlášť.
Tyto funkce jsou následující:

* Název konfigurace, které identifikuje konfigurace pro počítač. Tento název může být sdílen více cílové uzly
* ID agenta, které jedinečně identifikují jeden uzel
* Registrace krok, který dochází pouze při prvním cílový uzel připojuje k serveru vyžádané replikace

**Poznámka:** tyto funkce a funkce byly přidány a nenahrazují stávající funkce pro vyžádání obsahu a koncepty. Můžete použít tyto nové funkce nebo starší k novému serveru vyžádané replikace přesouvání v této verzi.

Další informace najdete v tématu [nastavení vyžadování klienta pomocí názvy konfigurace](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)
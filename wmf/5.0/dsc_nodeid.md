---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 5b9eea1c90bfd5a8cee3897d832bf7775a750308
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="separation-of-node-and-configuration-ids"></a>Oddělení uzlu a konfigurace ID

## <a name="overview"></a>Přehled

Aby bylo možné poskytnout více flexibilní a efektivní prostředí při používání DSC v režimu pro vyžádání obsahu, jsme přidali celou řadu funkcí v této verzi. Tyto funkce jsou určeny k umožňují flexibilně snadno nastavit a nasadit konfigurace napříč několika uzly, i když stále sledování stavu a vytváření sestav informace pro každý uzel zvlášť. Tyto funkce jsou následující:

* Název konfigurace, které identifikuje konfigurace pro počítač. Tento název může být sdílen více cílové uzly 
* ID agenta, které jedinečně identifikují jeden uzel
* Registrace krok, který dochází pouze při prvním cílový uzel připojuje k serveru vyžádané replikace

**Poznámka:** tyto funkce a funkce byly přidány a nenahrazují stávající funkce pro vyžádání obsahu a koncepty. Můžete použít tyto nové funkce nebo starší k novému serveru vyžádané replikace přesouvání v této verzi.

Další informace najdete v tématu [nastavení vyžadování klienta pomocí názvy konfigurace](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)


---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: eb84892525689b95f0577aecb6f142117e94f615
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="separation-of-configuration-resource-and-report-repositories"></a>Oddělení konfigurace, prostředků a sestav úložišť

V této verzi jsme umožňují všechny flexibilitu, že je potřeba pro vyžádání obsahu a sestavy na jeden nebo více serverů vyžádání DSC. Každý koncový bod může být definováno samostatně tak, aby konfigurace můžete načítat z jednoho umístění, prostředky z jiné a sestavy do ještě jiného umístění.

Další informace najdete v tématu [nastavení vyžadování klienta pomocí ID konfigurace](https://msdn.microsoft.com/powershell/dsc/pullclientconfigid) nebo [nastavení vyžadování klienta pomocí názvy konfigurace](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)
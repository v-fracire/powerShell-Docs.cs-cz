---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Klíč registru DSCAutomationHostEnabled
ms.openlocfilehash: 38e3189323c39a522b2ccad89f5cfcadf5e45616
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403645"
---
>Platí pro: Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>Klíč registru DSCAutomationHostEnabled

Použití DSC **DSCAutomationHostEnabled** klíče registru pod **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** umožňující konfiguraci počítače při prvním spuštění-.
DSCAutomationHostEnabled podporuje tří režimů:

|  Hodnota DSCAutomationHostEnabled  |  Popis   |
|---|---|
0 | Zakázat konfiguraci na počítači při spuštění. |
1 | Povolíte konfiguraci na počítači při spuštění. |
2 | Povolit konfiguraci počítače pouze v případě, že DSC je ve stavu čekající na vyřízení nebo aktuální. Tato hodnota je výchozí. |

## <a name="see-also"></a>Viz také

Příklad konfigurace spuštění při prvním spuštění – pomocí této funkce najdete v části [konfigurace virtuálních počítačů při prvním spuštění – s využitím DSC](bootstrapDsc.md).
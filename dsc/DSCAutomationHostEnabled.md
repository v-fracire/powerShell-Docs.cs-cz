---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Klíč registru DSCAutomationHostEnabled"
ms.openlocfilehash: e47c929b366f93738343eabc431aab5a4428352d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
>Platí pro: prostředí Windows PowerShell 5.0

# <a name="dscautomationhostenabled-registry-key"></a>Klíč registru DSCAutomationHostEnabled

Používá DSC **DSCAutomationHostEnabled** klíč registru v **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** umožňující konfiguraci počítače na počáteční spouštěcí up.
DSCAutomationHostEnabled podporuje tři režimy:

|  Hodnota DSCAutomationHostEnabled  |  Popis   | 
|---|---| 
0 | Konfigurace počítače na spouštěcí telefonického disable. |
1 | Povolit konfigurace při spuštění počítače. |
2 | Povolení konfigurace počítače pouze v případě DSC je ve stavu čekající na vyřízení nebo aktuální. Tato hodnota je výchozí. |

## <a name="see-also"></a>Viz také

Příklad použití této funkce na spuštění konfigurace při počáteční spouštěcí up, naleznete v části [konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC](bootstrapDsc.md).



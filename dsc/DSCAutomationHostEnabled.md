---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Klíč registru DSCAutomationHostEnabled
ms.openlocfilehash: 9fd71120b4959a7b14094922b453b05b217f3736
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
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
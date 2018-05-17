---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Přehled stavu konfigurace požadovaného prostředí Windows PowerShell
ms.openlocfilehash: c9069d7c9ce9c614330e36a42233b00363660a4b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="windows-powershell-desired-state-configuration-overview"></a>Přehled stavu konfigurace požadovaného prostředí Windows PowerShell

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

DSC je platforma pro správu v prostředí PowerShell, které umožňuje spravovat vaše IT a vývoj infrastruktury s konfigurací jako kód.

- Přehled obchodní výhody používání DSC, najdete v tématu [potřeby přehled stavu konfigurace pro rozhodují](decisionMaker.md).
- Přehled engineering výhody používání DSC, najdete v tématu [potřeby přehled stavu konfigurace pro techniky](DscForEngineers.md).
- Chcete-li začít rychle používat DSC, přečtěte si téma [DSC úvodní](quickStart.md).

## <a name="key-concepts"></a>Klíčové koncepty

DSC je deklarativní platforma používá pro konfiguraci, nasazení a Správa systémů. Obsahuje tři hlavní komponenty:

- [Konfigurace](configurations.md) jsou deklarativní skriptů prostředí PowerShell, které definují a konfigurace instance prostředků.
    Při spuštění konfigurace DSC (a prostředky volané konfigurace) bude jednoduše "bylo tak", zajistíte, že v systému existuje ve stavu nastíněny konfigurace.
    Konfigurace DSC se také idempotent: místní Configuration Manager (LCM) budou nadále počítače musí být nastaveny v ať stav konfigurace deklaruje.
- [Prostředky](resources.md) jsou součástí DSC "bylo tak". Obsahuje kód, který put a zachovat cíl konfigurace v zadaném stavu.
    Prostředky jsou umístěny v moduly Powershellu a je možné zapsat do modelu něco jako obecný jako soubor nebo procesu systému Windows nebo jako konkrétní jako server služby IIS nebo na virtuální počítač běží v Azure.
- [Místní Configuration Manager (LCM)](metaConfig.md) je modulem, podle kterého DSC usnadňuje interakce mezi prostředky a konfigurace.
    LCM pravidelně dotazuje systému pomocí tok řízení implementované prostředky k zajištění, že se zachová stav definovaný konfigurace.
    Pokud systém nemá dostatek stavu, LCM volá kód v prostředky usnadnit "," závislosti na konfiguraci.

## <a name="see-also"></a>Viz také

- [Konfigurace DSC](configurations.md)
- [Prostředky DSC](resources.md)
- [Konfigurace správce místní konfigurace](metaConfig.md)
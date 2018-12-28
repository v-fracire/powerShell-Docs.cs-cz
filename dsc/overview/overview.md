---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředí Windows PowerShell Desired State Configuration – přehled
ms.openlocfilehash: 3e4f0afa17ab60bfa98f1b86b9830462a7c8e1cf
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403831"
---
# <a name="windows-powershell-desired-state-configuration-overview"></a>Prostředí Windows PowerShell Desired State Configuration – přehled

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

DSC je platforma pro správu v prostředí PowerShell, které umožňuje spravovat vaši IT a rozvoj infrastruktury s konfigurací jako kód.

- Přehled o výhodách pro firmy pomocí DSC, naleznete v tématu [Desired State Configuration přehled pro pracovníky s rozhodovací pravomocí](decisionMaker.md).
- Přehled technických výhody používání DSC, naleznete v tématu [Desired State Configuration přehled pro techniky](DscForEngineers.md).
- Chcete-li začít rychle používat DSC, přečtěte si téma [rychlý start DSC](../quickstarts/website-quickstart.md).

## <a name="key-concepts"></a>Klíčové koncepty

DSC je deklarativní platforma sloužící ke konfiguraci, nasazení a správě systémů. Skládá se z tři hlavní komponenty:

- [Konfigurace](../configurations/configurations.md) jsou deklarativní Powershellové skripty, které definují a konfigurace instancí prostředků.
    Při spouštění konfigurace (DSC a prostředky volané konfiguraci) bude jednoduše "aby tak", zajištění, že v systému existuje ve stavu rozloženy modulem konfigurace.
    Konfigurace DSC se také idempotentní: místní Configuration Manageru (LCM) budou i nadále zajistit, že počítače jsou konfigurované v cokoli, co stavu konfigurace deklaruje.
- [Prostředky](../resources/resources.md) jsou součástí DSC "usnadňují tak". Obsahující kód, který put a zachovat cílovou konfigurace v zadaném stavu.
    Prostředky jsou umístěny v moduly Powershellu a je možné zapisovat na model něco jako obecný jako soubor nebo proces Windows nebo jako specifické jako server služby IIS nebo na virtuální počítač běží v Azure.
- [Místní Configuration Manageru (LCM)](../managing-nodes/metaConfig.md) je modul, podle kterého DSC usnadňuje interakce mezi prostředky a konfigurace.
    LCM se pravidelně dotazuje systému použití toku řízení implementované prostředky, abyste zajistili zachování stavu určené konfigurace.
    Pokud systém nemá dostatek stavu, LCM provede volání do kódu na prostředcích, které "usnadňují tak" závislosti na konfiguraci.

## <a name="see-also"></a>Viz také

- [Konfigurace DSC](../configurations/configurations.md)
- [Prostředky DSC](../resources/resources.md)
- [Konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md)

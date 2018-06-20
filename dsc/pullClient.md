---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Nastavení klienta vyžádání DSC
ms.openlocfilehash: 7f8758bd7145518e30e9c28b74d0db5d74dfaab3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186656"
---
# <a name="setting-up-a-dsc-pull-client"></a>Nastavení klienta vyžádání DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

> [!IMPORTANT]
> Server pro vyžádání obsahu (funkce systému Windows *DSC služby*) je podporované součásti systému Windows Server jsou však nejsou žádné plány, které nabízí nové funkce nebo funkce. Doporučujeme začít Přechod spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace s v systému Windows Server) nebo jedno z řešení komunity uvedené [zde](pullserver.md#community-solutions-for-pull-service).

Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadané adresu URL nebo soubor v umístění, kde může kontaktovat načítací server za účelem získání konfigurací a prostředků, a kde se má odeslat data sestavy.

Následující témata popisují postup nastavení klientů pro vyžádání obsahu:

* [Použití konfiguračních názvů k nastavení načítacího klienta](pullClientConfigNames.md)
* [Použití konfiguračních identifikátorů k nastavení načítacího klienta](pullClientConfigID.md)

> **Poznámka:**: Tato témata platí pro PowerShell 5.0. Vyžádání klientovi v prostředí PowerShell 4.0, naleznete v tématu [nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0](pullClientConfigID4.md).
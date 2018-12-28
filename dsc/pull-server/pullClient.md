---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Nastavení načítacího klienta DSC
ms.openlocfilehash: b7cd6dc0087eb8368c5467df4c3c7266ed704451
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403639"
---
# <a name="setting-up-a-dsc-pull-client"></a>Nastavení načítacího klienta DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

> [!IMPORTANT]
> Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce. Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).

Každý cílový uzel musí být v aplikaci pro použití režimu o přijetí změn a daném umístění adresu URL nebo soubor, kde může kontaktovat server o přijetí změn a získejte konfigurací a prostředků a by měla odeslat data sestavy.

Následující témata popisují postup nastavení klientů o přijetí změn:

* [Použití konfiguračních názvů k nastavení načítacího klienta](pullClientConfigNames.md)
* [Použití konfiguračních identifikátorů k nastavení načítacího klienta](pullClientConfigID.md)

> **Poznámka:**: Tato témata se vztahují na PowerShell 5.0. K nastavení načítacího klienta v Powershellu 4.0, najdete v článku [nastavení načítacího klienta použití konfiguračních identifikátorů v Powershellu 4.0](pullClientConfigID4.md).
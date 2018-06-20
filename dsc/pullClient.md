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
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="ca933-103">Nastavení klienta vyžádání DSC</span><span class="sxs-lookup"><span data-stu-id="ca933-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="ca933-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ca933-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca933-105">Server pro vyžádání obsahu (funkce systému Windows *DSC služby*) je podporované součásti systému Windows Server jsou však nejsou žádné plány, které nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="ca933-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="ca933-106">Doporučujeme začít Přechod spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace s v systému Windows Server) nebo jedno z řešení komunity uvedené [zde](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="ca933-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="ca933-107">Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadané adresu URL nebo soubor v umístění, kde může kontaktovat načítací server za účelem získání konfigurací a prostředků, a kde se má odeslat data sestavy.</span><span class="sxs-lookup"><span data-stu-id="ca933-107">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>

<span data-ttu-id="ca933-108">Následující témata popisují postup nastavení klientů pro vyžádání obsahu:</span><span class="sxs-lookup"><span data-stu-id="ca933-108">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="ca933-109">Použití konfiguračních názvů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="ca933-109">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="ca933-110">Použití konfiguračních identifikátorů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="ca933-110">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="ca933-111">**Poznámka:**: Tato témata platí pro PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="ca933-111">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="ca933-112">Vyžádání klientovi v prostředí PowerShell 4.0, naleznete v tématu [nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="ca933-112">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>
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
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="4d13b-103">Nastavení načítacího klienta DSC</span><span class="sxs-lookup"><span data-stu-id="4d13b-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="4d13b-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4d13b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d13b-105">Serveru vyžádané replikace (funkce Windows *DSC služby*) jsou podporované součástí Windows serveru ale žádné plány nabízí nové funkce nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="4d13b-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="4d13b-106">Doporučujeme přechod od skupinám spravované klientům [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (zahrnuje funkce nad rámec serveru vyžádané replikace v systému Windows Server) nebo jednoho z komunity řešení uvedené [tady](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="4d13b-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="4d13b-107">Každý cílový uzel musí být v aplikaci pro použití režimu o přijetí změn a daném umístění adresu URL nebo soubor, kde může kontaktovat server o přijetí změn a získejte konfigurací a prostředků a by měla odeslat data sestavy.</span><span class="sxs-lookup"><span data-stu-id="4d13b-107">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>

<span data-ttu-id="4d13b-108">Následující témata popisují postup nastavení klientů o přijetí změn:</span><span class="sxs-lookup"><span data-stu-id="4d13b-108">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="4d13b-109">Použití konfiguračních názvů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="4d13b-109">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="4d13b-110">Použití konfiguračních identifikátorů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="4d13b-110">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="4d13b-111">**Poznámka:**: Tato témata se vztahují na PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="4d13b-111">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="4d13b-112">K nastavení načítacího klienta v Powershellu 4.0, najdete v článku [nastavení načítacího klienta použití konfiguračních identifikátorů v Powershellu 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="4d13b-112">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>
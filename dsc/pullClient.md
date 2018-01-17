---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Nastavení klienta vyžádání DSC"
ms.openlocfilehash: 98a67b8d27eeb445bb70f75253ca31e12207d5bd
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="setting-up-a-dsc-pull-client"></a><span data-ttu-id="b7a3a-103">Nastavení klienta vyžádání DSC</span><span class="sxs-lookup"><span data-stu-id="b7a3a-103">Setting up a DSC pull client</span></span>

> <span data-ttu-id="b7a3a-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b7a3a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b7a3a-105">Každý cílový uzel musí být sdělili pro použití režimu vyžádání obsahu a zadané adresu URL nebo soubor v umístění, kde může kontaktovat načítací server za účelem získání konfigurací a prostředků, a kde se má odeslat data sestavy.</span><span class="sxs-lookup"><span data-stu-id="b7a3a-105">Each target node has to be told to use pull mode and given the URL or file location where it can contact the pull server to get configurations and resources, and where it should send report data.</span></span>


<span data-ttu-id="b7a3a-106">Následující témata popisují postup nastavení klientů pro vyžádání obsahu:</span><span class="sxs-lookup"><span data-stu-id="b7a3a-106">The following topics explain how to set up pull clients:</span></span>

* [<span data-ttu-id="b7a3a-107">Použití konfiguračních názvů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="b7a3a-107">Setting up a pull client using configuration names</span></span>](pullClientConfigNames.md)
* [<span data-ttu-id="b7a3a-108">Použití konfiguračních identifikátorů k nastavení načítacího klienta</span><span class="sxs-lookup"><span data-stu-id="b7a3a-108">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)

> <span data-ttu-id="b7a3a-109">**Poznámka:**: Tato témata platí pro PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="b7a3a-109">**Note**: These topics apply to PowerShell 5.0.</span></span> <span data-ttu-id="b7a3a-110">Vyžádání klientovi v prostředí PowerShell 4.0, naleznete v tématu [nastavení vyžadování klienta pomocí ID konfigurace v prostředí PowerShell 4.0](pullClientConfigID4.md).</span><span class="sxs-lookup"><span data-stu-id="b7a3a-110">To set up a pull client in PowerShell 4.0, see [Setting up a pull client using configuration ID in PowerShell 4.0](pullClientConfigID4.md).</span></span>


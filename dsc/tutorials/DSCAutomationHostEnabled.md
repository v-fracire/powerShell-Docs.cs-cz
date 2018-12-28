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
><span data-ttu-id="c28a9-103">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c28a9-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="c28a9-104">Klíč registru DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="c28a9-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="c28a9-105">Použití DSC **DSCAutomationHostEnabled** klíče registru pod **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** umožňující konfiguraci počítače při prvním spuštění-.</span><span class="sxs-lookup"><span data-stu-id="c28a9-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="c28a9-106">DSCAutomationHostEnabled podporuje tří režimů:</span><span class="sxs-lookup"><span data-stu-id="c28a9-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="c28a9-107">Hodnota DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="c28a9-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="c28a9-108">Popis</span><span class="sxs-lookup"><span data-stu-id="c28a9-108">Description</span></span>   |
|---|---|
<span data-ttu-id="c28a9-109">0</span><span class="sxs-lookup"><span data-stu-id="c28a9-109">0</span></span> | <span data-ttu-id="c28a9-110">Zakázat konfiguraci na počítači při spuštění.</span><span class="sxs-lookup"><span data-stu-id="c28a9-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="c28a9-111">1</span><span class="sxs-lookup"><span data-stu-id="c28a9-111">1</span></span> | <span data-ttu-id="c28a9-112">Povolíte konfiguraci na počítači při spuštění.</span><span class="sxs-lookup"><span data-stu-id="c28a9-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="c28a9-113">2</span><span class="sxs-lookup"><span data-stu-id="c28a9-113">2</span></span> | <span data-ttu-id="c28a9-114">Povolit konfiguraci počítače pouze v případě, že DSC je ve stavu čekající na vyřízení nebo aktuální.</span><span class="sxs-lookup"><span data-stu-id="c28a9-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="c28a9-115">Tato hodnota je výchozí.</span><span class="sxs-lookup"><span data-stu-id="c28a9-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="c28a9-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="c28a9-116">See Also</span></span>

<span data-ttu-id="c28a9-117">Příklad konfigurace spuštění při prvním spuštění – pomocí této funkce najdete v části [konfigurace virtuálních počítačů při prvním spuštění – s využitím DSC](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="c28a9-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>
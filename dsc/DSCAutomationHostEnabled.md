---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Klíč registru DSCAutomationHostEnabled
ms.openlocfilehash: 0cecbadc6802938cadb4ffb9745a23e6b98544be
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221965"
---
><span data-ttu-id="bd10e-103">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="bd10e-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="bd10e-104">Klíč registru DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="bd10e-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="bd10e-105">Používá DSC **DSCAutomationHostEnabled** klíč registru v **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** umožňující konfiguraci počítače na počáteční spouštěcí up.</span><span class="sxs-lookup"><span data-stu-id="bd10e-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="bd10e-106">DSCAutomationHostEnabled podporuje tři režimy:</span><span class="sxs-lookup"><span data-stu-id="bd10e-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="bd10e-107">Hodnota DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="bd10e-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="bd10e-108">Popis</span><span class="sxs-lookup"><span data-stu-id="bd10e-108">Description</span></span>   |
|---|---|
<span data-ttu-id="bd10e-109">0</span><span class="sxs-lookup"><span data-stu-id="bd10e-109">0</span></span> | <span data-ttu-id="bd10e-110">Konfigurace počítače na spouštěcí telefonického disable.</span><span class="sxs-lookup"><span data-stu-id="bd10e-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="bd10e-111">1</span><span class="sxs-lookup"><span data-stu-id="bd10e-111">1</span></span> | <span data-ttu-id="bd10e-112">Povolit konfigurace při spuštění počítače.</span><span class="sxs-lookup"><span data-stu-id="bd10e-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="bd10e-113">2</span><span class="sxs-lookup"><span data-stu-id="bd10e-113">2</span></span> | <span data-ttu-id="bd10e-114">Povolení konfigurace počítače pouze v případě DSC je ve stavu čekající na vyřízení nebo aktuální.</span><span class="sxs-lookup"><span data-stu-id="bd10e-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="bd10e-115">Tato hodnota je výchozí.</span><span class="sxs-lookup"><span data-stu-id="bd10e-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="bd10e-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="bd10e-116">See Also</span></span>

<span data-ttu-id="bd10e-117">Příklad použití této funkce na spuštění konfigurace při počáteční spouštěcí up, naleznete v části [konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="bd10e-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>
---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Klíč registru DSCAutomationHostEnabled"
ms.openlocfilehash: c58b7a8f2485ff02f09763749a3de8a75f882d19
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
><span data-ttu-id="be79d-103">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="be79d-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="be79d-104">Klíč registru DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="be79d-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="be79d-105">Používá DSC **DSCAutomationHostEnabled** klíč registru v **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** umožňující konfiguraci počítače na počáteční spouštěcí up.</span><span class="sxs-lookup"><span data-stu-id="be79d-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="be79d-106">DSCAutomationHostEnabled podporuje tři režimy:</span><span class="sxs-lookup"><span data-stu-id="be79d-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="be79d-107">Hodnota DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="be79d-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="be79d-108">Popis</span><span class="sxs-lookup"><span data-stu-id="be79d-108">Description</span></span>   | 
|---|---| 
<span data-ttu-id="be79d-109">0</span><span class="sxs-lookup"><span data-stu-id="be79d-109">0</span></span> | <span data-ttu-id="be79d-110">Konfigurace počítače na spouštěcí telefonického disable.</span><span class="sxs-lookup"><span data-stu-id="be79d-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="be79d-111">1</span><span class="sxs-lookup"><span data-stu-id="be79d-111">1</span></span> | <span data-ttu-id="be79d-112">Povolit konfigurace při spuštění počítače.</span><span class="sxs-lookup"><span data-stu-id="be79d-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="be79d-113">2</span><span class="sxs-lookup"><span data-stu-id="be79d-113">2</span></span> | <span data-ttu-id="be79d-114">Povolení konfigurace počítače pouze v případě DSC je ve stavu čekající na vyřízení nebo aktuální.</span><span class="sxs-lookup"><span data-stu-id="be79d-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="be79d-115">Tato hodnota je výchozí.</span><span class="sxs-lookup"><span data-stu-id="be79d-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="be79d-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="be79d-116">See Also</span></span>

<span data-ttu-id="be79d-117">Příklad použití této funkce na spuštění konfigurace při počáteční spouštěcí up, naleznete v části [konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="be79d-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>



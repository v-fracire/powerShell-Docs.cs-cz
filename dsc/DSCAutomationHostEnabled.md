---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Klíč registru DSCAutomationHostEnabled"
ms.openlocfilehash: e47c929b366f93738343eabc431aab5a4428352d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
><span data-ttu-id="91d28-103">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="91d28-103">Applies to: Windows PowerShell 5.0</span></span>

# <a name="dscautomationhostenabled-registry-key"></a><span data-ttu-id="91d28-104">Klíč registru DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="91d28-104">DSCAutomationHostEnabled registry key</span></span>

<span data-ttu-id="91d28-105">Používá DSC **DSCAutomationHostEnabled** klíč registru v **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** umožňující konfiguraci počítače na počáteční spouštěcí up.</span><span class="sxs-lookup"><span data-stu-id="91d28-105">DSC uses the **DSCAutomationHostEnabled** registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies** to enable configuration of the machine at initial boot-up.</span></span>
<span data-ttu-id="91d28-106">DSCAutomationHostEnabled podporuje tři režimy:</span><span class="sxs-lookup"><span data-stu-id="91d28-106">DSCAutomationHostEnabled supports three modes:</span></span>

|  <span data-ttu-id="91d28-107">Hodnota DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="91d28-107">DSCAutomationHostEnabled Value</span></span>  |  <span data-ttu-id="91d28-108">Popis</span><span class="sxs-lookup"><span data-stu-id="91d28-108">Description</span></span>   | 
|---|---| 
<span data-ttu-id="91d28-109">0</span><span class="sxs-lookup"><span data-stu-id="91d28-109">0</span></span> | <span data-ttu-id="91d28-110">Konfigurace počítače na spouštěcí telefonického disable.</span><span class="sxs-lookup"><span data-stu-id="91d28-110">Disable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="91d28-111">1</span><span class="sxs-lookup"><span data-stu-id="91d28-111">1</span></span> | <span data-ttu-id="91d28-112">Povolit konfigurace při spuštění počítače.</span><span class="sxs-lookup"><span data-stu-id="91d28-112">Enable configuring the machine at boot-up.</span></span> |
<span data-ttu-id="91d28-113">2</span><span class="sxs-lookup"><span data-stu-id="91d28-113">2</span></span> | <span data-ttu-id="91d28-114">Povolení konfigurace počítače pouze v případě DSC je ve stavu čekající na vyřízení nebo aktuální.</span><span class="sxs-lookup"><span data-stu-id="91d28-114">Enable configuring the machine only if DSC is in pending or current state.</span></span> <span data-ttu-id="91d28-115">Tato hodnota je výchozí.</span><span class="sxs-lookup"><span data-stu-id="91d28-115">This is the default value.</span></span> |

## <a name="see-also"></a><span data-ttu-id="91d28-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="91d28-116">See Also</span></span>

<span data-ttu-id="91d28-117">Příklad použití této funkce na spuštění konfigurace při počáteční spouštěcí up, naleznete v části [konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC](bootstrapDsc.md).</span><span class="sxs-lookup"><span data-stu-id="91d28-117">For an example of how to use this feature to run configurations at initial boot-up, see [Configure a virtual machines at initial boot-up by using DSC](bootstrapDsc.md).</span></span>



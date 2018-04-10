---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: d5ba6a5c5ba8ff54a4f4d6ba07cf04124baf65ef
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a><span data-ttu-id="dd480-102">Povolení pro identické duplicitní prostředky v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="dd480-102">Allowing for Identical Duplicate Resources in a Configuration</span></span>

<span data-ttu-id="dd480-103">DSC nemá povolit nebo zpracování konfliktní definice prostředků v rámci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="dd480-103">DSC does not allow or handle conflicting resource definitions within a configuration.</span></span> <span data-ttu-id="dd480-104">Namísto pokusu o vyřešení konfliktu, jednoduše dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="dd480-104">Instead of trying to resolve the conflict, it simply fails.</span></span> <span data-ttu-id="dd480-105">Jako opakované použití konfigurace se změní na více využité prostřednictvím složené prostředků, dojde častěji konflikty atd.</span><span class="sxs-lookup"><span data-stu-id="dd480-105">As configuration reuse becomes more utilized through composite resources, etc. conflicts will occur more often.</span></span> <span data-ttu-id="dd480-106">Když jsou identické konfliktní definice prostředků, DSC by měl být inteligentní a povolit to.</span><span class="sxs-lookup"><span data-stu-id="dd480-106">When conflicting resource definitions are identical, DSC should be smart and allow this.</span></span> <span data-ttu-id="dd480-107">V této verzi se podporujeme s více instancí prostředků, které mají stejné definice:</span><span class="sxs-lookup"><span data-stu-id="dd480-107">With this release, we support having multiple resource instances that have identical definitions:</span></span>

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

<span data-ttu-id="dd480-108">V předchozích verzích výsledkem bude, že je nainstalovaná kompilace se nezdařila z důvodu konfliktu mezi WindowsFeature FE_IIS a instancí WindowsFeature Worker_IIS pokusu zkontrolujte roli webovým serverem.</span><span class="sxs-lookup"><span data-stu-id="dd480-108">In previous releases, the result would be a failed compilation due to a conflict between the WindowsFeature FE_IIS and WindowsFeature Worker_IIS instances trying to ensure the 'Web-Server' role is installed.</span></span> <span data-ttu-id="dd480-109">Všimněte si, že *všechny* vlastnosti, které jsou právě konfigurovány jsou identické v těchto dvou konfiguracích.</span><span class="sxs-lookup"><span data-stu-id="dd480-109">Notice that *all* of the properties that are being configured are identical in these two configurations.</span></span> <span data-ttu-id="dd480-110">Vzhledem k tomu *všechny* vlastností v tyto dva prostředky jsou identické, výsledkem bude nyní úspěšné kompilace.</span><span class="sxs-lookup"><span data-stu-id="dd480-110">Since *all* of the properties in these two resources are identical, this will result in a successful compilation now.</span></span>

<span data-ttu-id="dd480-111">Pokud jsou jakékoli vlastnosti rozdíly mezi dva prostředky, se nebude se zvažovat identické a nebude kompilace:</span><span class="sxs-lookup"><span data-stu-id="dd480-111">If any of the properties are different between the two resources, they will not be considered identical and compilation will fail:</span></span>

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS
    {
        Ensure = 'Present'     # Ensure is Present here
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS
    {
        Ensure = 'Absent'      # Ensure property is Absent instead of Present
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

<span data-ttu-id="dd480-112">Tato velmi podobné konfigurace selže, protože WindowsFeature FE_IIS a prostředky WindowsFeature Worker_IIS již nejsou identické a proto dojít ke konfliktu.</span><span class="sxs-lookup"><span data-stu-id="dd480-112">This very similar configuration will fail because the WindowsFeature FE_IIS and the WindowsFeature Worker_IIS resources are no longer identical and therefore conflict.</span></span>
---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
title: "Poznámky k verzi WMF 5.1"
ms.openlocfilehash: ce9bc7791facfcc2cce9468689e88a26154bda7d
ms.sourcegitcommit: 3f49bd2e0b786e69c71393c00ad85d05a8466753
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/04/2017
---
# <a name="windows-management-framework-wmf-51-release-notes"></a><span data-ttu-id="9fbe5-103">Poznámky k verzi Windows Management Framework (WMF) 5.1</span><span class="sxs-lookup"><span data-stu-id="9fbe5-103">Windows Management Framework (WMF) 5.1 Release Notes</span></span> #

<span data-ttu-id="9fbe5-104">WMF 5.1 zahrnuje komponenty prostředí PowerShell, rozhraní WMI, WinRM a protokolování inventáře softwaru (SIL), které byly zveřejněny v systému Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9fbe5-104">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span>
<span data-ttu-id="9fbe5-105">WMF 5.1 se dá nainstalovat na Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 a 2012 R2 a nabízí několik vylepšení v porovnání s WMF 5.0 RTM, včetně:</span><span class="sxs-lookup"><span data-stu-id="9fbe5-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="9fbe5-106">Nové rutiny: místní uživatelé a skupiny; Get-ComputerInfo</span><span class="sxs-lookup"><span data-stu-id="9fbe5-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="9fbe5-107">PowerShellGet vylepšení patří vynucování podepsané moduly a instalace JEA moduly</span><span class="sxs-lookup"><span data-stu-id="9fbe5-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="9fbe5-108">PackageManagement přidaná podpora pro instalační program na základě EXE kontejnery, CBS instalace, soubor CAB balíčky</span><span class="sxs-lookup"><span data-stu-id="9fbe5-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="9fbe5-109">Ladění vylepšení pro třídy DSC a prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fbe5-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="9fbe5-110">Vylepšení zabezpečení, včetně vynucení katalogu podepsané moduly přichází ze serveru vyžádaných replikací a při použití rutiny PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="9fbe5-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="9fbe5-111">Odpovědi na počet uživatelských požadavků a problémů</span><span class="sxs-lookup"><span data-stu-id="9fbe5-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="9fbe5-112">**Důležité poznámky:**</span><span class="sxs-lookup"><span data-stu-id="9fbe5-112">**Important notes:**</span></span>

- <span data-ttu-id="9fbe5-113">**WMF 5.1 vyžaduje rozhraní .NET Framework 4.5.2** (nebo novější).</span><span class="sxs-lookup"><span data-stu-id="9fbe5-113">**WMF 5.1 requires the .NET Framework 4.5.2** (or above).</span></span> <span data-ttu-id="9fbe5-114">Instalace proběhne úspěšně, ale jsou některé klíčové funkce se nezdaří, pokud rozhraní .NET 4.5.2 (nebo novější) není nainstalována.</span><span class="sxs-lookup"><span data-stu-id="9fbe5-114">Installation will succeed, but key features will fail if .NET 4.5.2 (or above) is not installed.</span></span> <span data-ttu-id="9fbe5-115">Pokyny jsou k dispozici v [instalace a konfigurace 5.1 WMF ](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure) tématu.</span><span class="sxs-lookup"><span data-stu-id="9fbe5-115">Instructions are available in the [Install and Configure WMF 5.1 ](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure) topic.</span></span>
- <span data-ttu-id="9fbe5-116">WMF 5.1 náhled je nutné odinstalovat před instalací WMF 5.1 RTM.</span><span class="sxs-lookup"><span data-stu-id="9fbe5-116">WMF 5.1 Preview must be uninstalled before installing WMF 5.1 RTM.</span></span>
- <span data-ttu-id="9fbe5-117">WMF 5.1 může být nainstalovaná přímo přes WMF 5.0 nebo WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="9fbe5-117">WMF 5.1 may be installed directly over WMF 5.0 or WMF 4.0.</span></span>
- <span data-ttu-id="9fbe5-118">Je __nevyžaduje__ k instalaci WMF 4.0 před instalací WMF 5.1 v systému Windows 7 a Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="9fbe5-118">It is __not required__ to install WMF 4.0 prior to installing WMF 5.1 on Windows 7 and Windows Server 2008 R2.</span></span> <span data-ttu-id="9fbe5-119">Zda byl problém ve verzi WMF 5.1 Preview a byl vyřešen.</span><span class="sxs-lookup"><span data-stu-id="9fbe5-119">That was an issue for the WMF 5.1 Preview release, and has been resolved.</span></span>  



---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: "Poznámky k verzi WMF 5.1"
ms.openlocfilehash: fa3d9a3563ecf1bfc76d82b027641d19c9a4ff4e
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="windows-management-framework-wmf-51-release-notes"></a><span data-ttu-id="0512a-103">Poznámky k verzi Windows Management Framework (WMF) 5.1</span><span class="sxs-lookup"><span data-stu-id="0512a-103">Windows Management Framework (WMF) 5.1 Release Notes</span></span> #

<span data-ttu-id="0512a-104">WMF 5.1 zahrnuje komponenty prostředí PowerShell, rozhraní WMI, WinRM a protokolování inventáře softwaru (SIL), které byly zveřejněny v systému Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0512a-104">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory Logging (SIL) components that were released with Windows Server 2016.</span></span>
<span data-ttu-id="0512a-105">WMF 5.1 můžete instalovat na Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 a 2012 R2. Verze WMF 5.1 nabízí oproti WMF 5.0 RTM celou řadu vylepšení. Například:</span><span class="sxs-lookup"><span data-stu-id="0512a-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="0512a-106">Nové rutiny pro místní uživatelé a skupiny, Get-ComputerInfo</span><span class="sxs-lookup"><span data-stu-id="0512a-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="0512a-107">Vylepšení PowerShellGet zahrnuje vynucení podepsaných modulů a instalaci modulů JEA</span><span class="sxs-lookup"><span data-stu-id="0512a-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="0512a-108">Přidaná podpora funkce PackageManagement pro kontejnery, nastavení CBS, nastavení založené na souboru EXE a balíčky CAB</span><span class="sxs-lookup"><span data-stu-id="0512a-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="0512a-109">Vylepšené ladění pro třídy DSC a PowerShellu</span><span class="sxs-lookup"><span data-stu-id="0512a-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="0512a-110">Vylepšené zabezpečení, včetně vynucení modulů podepsaných v katalogu, které pocházejí ze serveru vyžádané replikace při používání rutin PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="0512a-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="0512a-111">Odpovědi na celou řadu požadavků a problémů uživatelů</span><span class="sxs-lookup"><span data-stu-id="0512a-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="0512a-112">**Důležité poznámky:**</span><span class="sxs-lookup"><span data-stu-id="0512a-112">**Important notes:**</span></span>

- <span data-ttu-id="0512a-113">**WMF 5.1 vyžaduje rozhraní .NET Framework 4.5.2** (nebo novější).</span><span class="sxs-lookup"><span data-stu-id="0512a-113">**WMF 5.1 requires the .NET Framework 4.5.2** (or above).</span></span> <span data-ttu-id="0512a-114">Instalace proběhne úspěšně, ale jsou některé klíčové funkce se nezdaří, pokud rozhraní .NET 4.5.2 (nebo novější) není nainstalována.</span><span class="sxs-lookup"><span data-stu-id="0512a-114">Installation will succeed, but key features will fail if .NET 4.5.2 (or above) is not installed.</span></span> <span data-ttu-id="0512a-115">Pokyny jsou k dispozici v [instalace a konfigurace 5.1 WMF ](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) tématu.</span><span class="sxs-lookup"><span data-stu-id="0512a-115">Instructions are available in the [Install and Configure WMF 5.1 ](https://msdn.microsoft.com/powershell/wmf/5.1/install-configure) topic.</span></span>
- <span data-ttu-id="0512a-116">WMF 5.1 náhled je nutné odinstalovat před instalací WMF 5.1 RTM.</span><span class="sxs-lookup"><span data-stu-id="0512a-116">WMF 5.1 Preview must be uninstalled before installing WMF 5.1 RTM.</span></span>
- <span data-ttu-id="0512a-117">WMF 5.1 může být nainstalovaná přímo přes WMF 5.0 nebo WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="0512a-117">WMF 5.1 may be installed directly over WMF 5.0 or WMF 4.0.</span></span>
- <span data-ttu-id="0512a-118">Je __nevyžaduje__ k instalaci WMF 4.0 před instalací WMF 5.1 v systému Windows 7 a Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="0512a-118">It is __not required__ to install WMF 4.0 prior to installing WMF 5.1 on Windows 7 and Windows Server 2008 R2.</span></span> <span data-ttu-id="0512a-119">Zda byl problém ve verzi WMF 5.1 Preview a byl vyřešen.</span><span class="sxs-lookup"><span data-stu-id="0512a-119">That was an issue for the WMF 5.1 Preview release, and has been resolved.</span></span>  



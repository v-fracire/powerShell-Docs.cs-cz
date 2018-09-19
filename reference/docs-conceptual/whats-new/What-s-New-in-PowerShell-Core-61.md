---
title: Co je nového v Powershellu Core 6.1
description: Nové funkce a změny v prostředí PowerShell Core 6.1
ms.date: 09/13/2018
ms.openlocfilehash: 5e2fe3c819ed638b2c14d7d40e08b7c32953147f
ms.sourcegitcommit: 59e568ac9fa8ba28e2c96932b7c84d4a855fed2f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46289221"
---
# <a name="whats-new-in-powershell-core-61"></a><span data-ttu-id="76103-103">Co je nového v Powershellu Core 6.1</span><span class="sxs-lookup"><span data-stu-id="76103-103">What's New in PowerShell Core 6.1</span></span>

<span data-ttu-id="76103-104">Níže je výběr některé hlavní nové funkce a změny, které byly zavedeny v prostředí PowerShell Core 6.1.</span><span class="sxs-lookup"><span data-stu-id="76103-104">Below is a selection of some of the major new features and changes that have been introduced in PowerShell Core 6.1.</span></span>

<span data-ttu-id="76103-105">K dispozici je také **tuny** z "nudné", která usnadňují rychlejší a stabilnější (plus velké a spoustu chyb) PowerShell!</span><span class="sxs-lookup"><span data-stu-id="76103-105">There's also **tons** of "boring stuff" that make PowerShell faster and more stable (plus lots and lots of bug fixes)!</span></span>
<span data-ttu-id="76103-106">Úplný seznam změn, podívejte se na naše [protokolu změn na Githubu](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="76103-106">For a full list of changes, check out our [changelog on GitHub](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).</span></span>

<span data-ttu-id="76103-107">A při říkáme si některé názvy, Děkujeme, že vám [všechny přispěvatelé komunit](https://github.com/PowerShell/PowerShell/graphs/contributors) , provedli tato verze je to možné.</span><span class="sxs-lookup"><span data-stu-id="76103-107">And while we call out some names below, thank you to [all of the community contributors](https://github.com/PowerShell/PowerShell/graphs/contributors) that made this release possible.</span></span>

## <a name="net-core-21"></a><span data-ttu-id="76103-108">.NET core 2.1</span><span class="sxs-lookup"><span data-stu-id="76103-108">.NET Core 2.1</span></span>

<span data-ttu-id="76103-109">PowerShell Core 6.1 přesunuta do .NET Core 2.1 poté, co byla [vydáno v květnu](https://blogs.msdn.microsoft.com/dotnet/2018/05/30/announcing-net-core-2-1/), což celou řadou vylepšení prostředí PowerShell, včetně:</span><span class="sxs-lookup"><span data-stu-id="76103-109">PowerShell Core 6.1 moved to .NET Core 2.1 after it was [released in May](https://blogs.msdn.microsoft.com/dotnet/2018/05/30/announcing-net-core-2-1/), resulting in a number of improvements to PowerShell, including:</span></span>

- <span data-ttu-id="76103-110">vylepšení výkonu (viz [níže](#performance-improvements))</span><span class="sxs-lookup"><span data-stu-id="76103-110">performance improvements (see [below](#performance-improvements))</span></span>
- <span data-ttu-id="76103-111">Podpora Alpine Linuxu (preview)</span><span class="sxs-lookup"><span data-stu-id="76103-111">Alpine Linux support (preview)</span></span>
- <span data-ttu-id="76103-112">[Podpora globálních nástroje .NET](/dotnet/core/tools/global-tools) – nadcházejících brzy do prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="76103-112">[.NET global tool support](/dotnet/core/tools/global-tools) - coming soon to PowerShell</span></span>
- [`Span<T>`](/dotnet/api/system.span-1?view=netcore-2.1)

## <a name="windows-compatibility-pack-for-net-core"></a><span data-ttu-id="76103-113">Windows Compatibility Pack for .NET Core</span><span class="sxs-lookup"><span data-stu-id="76103-113">Windows Compatibility Pack for .NET Core</span></span>

<span data-ttu-id="76103-114">Na Windows, dodávané týmu .NET [Windows Compatibility Pack for .NET Core](https://blogs.msdn.microsoft.com/dotnet/2017/11/16/announcing-the-windows-compatibility-pack-for-net-core/), odebrat sadu sestavení, které přidají několik rozhraní API zpět do .NET Core ve Windows.</span><span class="sxs-lookup"><span data-stu-id="76103-114">On Windows, the .NET team shipped the [Windows Compatibility Pack for .NET Core](https://blogs.msdn.microsoft.com/dotnet/2017/11/16/announcing-the-windows-compatibility-pack-for-net-core/), a set of assemblies that add a number of removed APIs back to .NET Core on Windows.</span></span>

<span data-ttu-id="76103-115">Přidali jsme Windows Compatibility Pack na verzi prostředí PowerShell Core 6.1 tak, aby všechny moduly nebo skripty, které pomocí těchto rozhraní API můžete spolehnout na nich nebudou dostupné.</span><span class="sxs-lookup"><span data-stu-id="76103-115">We've added the Windows Compatibility Pack to PowerShell Core 6.1 release so that any modules or scripts that use these APIs can rely on them being available.</span></span>

<span data-ttu-id="76103-116">PowerShell Core používat umožňuje Windows Compatibility Pack **více než 1900 rutiny, které se dodávají s Windows 10. října 2018 Update a Windows Server 2019**.</span><span class="sxs-lookup"><span data-stu-id="76103-116">The Windows Compatibility Pack enables PowerShell Core to use **more than 1900 cmdlets that ship with Windows 10 October 2018 Update and Windows Server 2019**.</span></span>

## <a name="support-for-application-whitelisting"></a><span data-ttu-id="76103-117">Podpora pro přidávání na seznam povolených aplikací</span><span class="sxs-lookup"><span data-stu-id="76103-117">Support for Application Whitelisting</span></span>

<span data-ttu-id="76103-118">PowerShell Core 6.1 má se podporuje Windows PowerShell 5.1 [Applockeru](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/applocker/applocker-overview) a [Device Guard](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control) seznamu povolených aplikací.</span><span class="sxs-lookup"><span data-stu-id="76103-118">PowerShell Core 6.1 has parity with Windows PowerShell 5.1 supporting [AppLocker](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/applocker/applocker-overview) and [Device Guard](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control) application whitelisting.</span></span>
<span data-ttu-id="76103-119">Přidávání na seznam povolených aplikací umožňuje podrobnou kontrolu nad jaké binární soubory jsou mohou být provedeny pomocí prostředí PowerShell použít [režim omezené jazyka](https://blogs.msdn.microsoft.com/powershell/2017/11/02/powershell-constrained-language-mode/).</span><span class="sxs-lookup"><span data-stu-id="76103-119">Application whitelisting allows granular control of what binaries are allowed to be executed used with PowerShell [Constrained Language mode](https://blogs.msdn.microsoft.com/powershell/2017/11/02/powershell-constrained-language-mode/).</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="76103-120">Vylepšení výkonu</span><span class="sxs-lookup"><span data-stu-id="76103-120">Performance improvements</span></span>

<span data-ttu-id="76103-121">Windows Powershellu 6.0 provedli několik vylepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="76103-121">PowerShell Core 6.0 made some significant performance improvements.</span></span>
<span data-ttu-id="76103-122">PowerShell Core 6.1 neustále zlepšuje rychlost určité operace.</span><span class="sxs-lookup"><span data-stu-id="76103-122">PowerShell Core 6.1 continues to improve the speed of certain operations.</span></span>

<span data-ttu-id="76103-123">Například `Group-Object` byla urychlí 66 %:</span><span class="sxs-lookup"><span data-stu-id="76103-123">For example, `Group-Object` has been sped up by 66%:</span></span>

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Group-Object }
```

|              | <span data-ttu-id="76103-124">Prostředí Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="76103-124">Windows PowerShell 5.1</span></span> | <span data-ttu-id="76103-125">PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="76103-125">PowerShell Core 6.0</span></span> | <span data-ttu-id="76103-126">PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="76103-126">PowerShell Core 6.1</span></span> |
|--------------|------------------------|---------------------|---------------------|
| <span data-ttu-id="76103-127">Doba (sek)</span><span class="sxs-lookup"><span data-stu-id="76103-127">Time (sec)</span></span>   | <span data-ttu-id="76103-128">25.178</span><span class="sxs-lookup"><span data-stu-id="76103-128">25.178</span></span>                 | <span data-ttu-id="76103-129">19.653</span><span class="sxs-lookup"><span data-stu-id="76103-129">19.653</span></span>              | <span data-ttu-id="76103-130">6.641</span><span class="sxs-lookup"><span data-stu-id="76103-130">6.641</span></span>               |
| <span data-ttu-id="76103-131">Zrychlení (%)</span><span class="sxs-lookup"><span data-stu-id="76103-131">Speed-up (%)</span></span> | <span data-ttu-id="76103-132">Neužívá se.</span><span class="sxs-lookup"><span data-stu-id="76103-132">N/A</span></span>                    | <span data-ttu-id="76103-133">% 21,9</span><span class="sxs-lookup"><span data-stu-id="76103-133">21.9%</span></span>               | <span data-ttu-id="76103-134">66.2 %</span><span class="sxs-lookup"><span data-stu-id="76103-134">66.2%</span></span>               |

<span data-ttu-id="76103-135">Obdobně řazení scénáře, jako je tato vylepšili o více než 15 %:</span><span class="sxs-lookup"><span data-stu-id="76103-135">Similarly, sorting scenarios like this one have improved by more than 15%:</span></span>

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Sort-Object }
```

|              | <span data-ttu-id="76103-136">Prostředí Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="76103-136">Windows PowerShell 5.1</span></span> | <span data-ttu-id="76103-137">PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="76103-137">PowerShell Core 6.0</span></span> | <span data-ttu-id="76103-138">PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="76103-138">PowerShell Core 6.1</span></span> |
|--------------|------------------------|---------------------|---------------------|
| <span data-ttu-id="76103-139">Doba (sek)</span><span class="sxs-lookup"><span data-stu-id="76103-139">Time (sec)</span></span>   | <span data-ttu-id="76103-140">12.170</span><span class="sxs-lookup"><span data-stu-id="76103-140">12.170</span></span>                 | <span data-ttu-id="76103-141">8.493</span><span class="sxs-lookup"><span data-stu-id="76103-141">8.493</span></span>               | <span data-ttu-id="76103-142">7.08</span><span class="sxs-lookup"><span data-stu-id="76103-142">7.08</span></span>                |
| <span data-ttu-id="76103-143">Zrychlení (%)</span><span class="sxs-lookup"><span data-stu-id="76103-143">Speed-up (%)</span></span> | <span data-ttu-id="76103-144">Neužívá se.</span><span class="sxs-lookup"><span data-stu-id="76103-144">N/A</span></span>                    | <span data-ttu-id="76103-145">30.2 %</span><span class="sxs-lookup"><span data-stu-id="76103-145">30.2%</span></span>               | <span data-ttu-id="76103-146">16.6 %</span><span class="sxs-lookup"><span data-stu-id="76103-146">16.6%</span></span>               |

<span data-ttu-id="76103-147">`Import-Csv` má také byla urychlí výrazně po regrese z prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76103-147">`Import-Csv` has also been sped up significantly after a regression from Windows PowerShell.</span></span>
<span data-ttu-id="76103-148">Test sdíleného svazku clusteru s 26,616 řádky a šest sloupců v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="76103-148">The following example uses a test CSV with 26,616 rows and six columns:</span></span>

```powershell
Measure-Command {$a = Import-Csv foo.csv}
```

|              | <span data-ttu-id="76103-149">Prostředí Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="76103-149">Windows PowerShell 5.1</span></span> | <span data-ttu-id="76103-150">PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="76103-150">PowerShell Core 6.0</span></span> | <span data-ttu-id="76103-151">PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="76103-151">PowerShell Core 6.1</span></span>    |
|--------------|------------------------|---------------------|------------------------|
| <span data-ttu-id="76103-152">Doba (sek)</span><span class="sxs-lookup"><span data-stu-id="76103-152">Time (sec)</span></span>   | <span data-ttu-id="76103-153">0.441</span><span class="sxs-lookup"><span data-stu-id="76103-153">0.441</span></span>                  | <span data-ttu-id="76103-154">1.069</span><span class="sxs-lookup"><span data-stu-id="76103-154">1.069</span></span>               | <span data-ttu-id="76103-155">0.268</span><span class="sxs-lookup"><span data-stu-id="76103-155">0.268</span></span>                  |
| <span data-ttu-id="76103-156">Zrychlení (%)</span><span class="sxs-lookup"><span data-stu-id="76103-156">Speed-up (%)</span></span> | <span data-ttu-id="76103-157">Neužívá se.</span><span class="sxs-lookup"><span data-stu-id="76103-157">N/A</span></span>                    | <span data-ttu-id="76103-158">-142.4 %</span><span class="sxs-lookup"><span data-stu-id="76103-158">-142.4%</span></span>             | <span data-ttu-id="76103-159">74.9 % (39.2 % WPS)</span><span class="sxs-lookup"><span data-stu-id="76103-159">74.9% (39.2% from WPS)</span></span> |

<span data-ttu-id="76103-160">A konečně, převodu z formátu JSON do `PSObject` má byla urychlí více než 50 % od prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76103-160">Lastly, conversion from JSON into `PSObject` has been sped up by more than 50% since Windows PowerShell.</span></span>
<span data-ttu-id="76103-161">Následující příklad používá soubor JSON ~ 2MB testu:</span><span class="sxs-lookup"><span data-stu-id="76103-161">The following example uses a ~2MB test JSON file:</span></span>

```powershell
Measure-Command {Get-Content .\foo.json | ConvertFrom-Json}
```

|              | <span data-ttu-id="76103-162">Prostředí Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="76103-162">Windows PowerShell 5.1</span></span> | <span data-ttu-id="76103-163">PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="76103-163">PowerShell Core 6.0</span></span> | <span data-ttu-id="76103-164">PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="76103-164">PowerShell Core 6.1</span></span>    |
|--------------|------------------------|---------------------|------------------------|
| <span data-ttu-id="76103-165">Doba (sek)</span><span class="sxs-lookup"><span data-stu-id="76103-165">Time (sec)</span></span>   | <span data-ttu-id="76103-166">0.259</span><span class="sxs-lookup"><span data-stu-id="76103-166">0.259</span></span>                  | <span data-ttu-id="76103-167">0.577</span><span class="sxs-lookup"><span data-stu-id="76103-167">0.577</span></span>               | <span data-ttu-id="76103-168">0,125</span><span class="sxs-lookup"><span data-stu-id="76103-168">0.125</span></span>                  |
| <span data-ttu-id="76103-169">Zrychlení (%)</span><span class="sxs-lookup"><span data-stu-id="76103-169">Speed-up (%)</span></span> | <span data-ttu-id="76103-170">Neužívá se.</span><span class="sxs-lookup"><span data-stu-id="76103-170">N/A</span></span>                    | <span data-ttu-id="76103-171">-122.8 %</span><span class="sxs-lookup"><span data-stu-id="76103-171">-122.8%</span></span>             | <span data-ttu-id="76103-172">78.3 % (51.7 % WPS)</span><span class="sxs-lookup"><span data-stu-id="76103-172">78.3% (51.7% from WPS)</span></span> |

## <a name="check-system32-for-compatible-in-box-modules-on-windows"></a><span data-ttu-id="76103-173">Zkontrolujte `system32` kompatibilní modulů integrované ve Windows</span><span class="sxs-lookup"><span data-stu-id="76103-173">Check `system32` for compatible in-box modules on Windows</span></span>

<span data-ttu-id="76103-174">V aktualizaci Windows 10 1809 a Windows Server 2019 jsme aktualizovali několik moduly Powershellu dodávané označit jako kompatibilní s PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="76103-174">In the Windows 10 1809 update and Windows Server 2019, we updated a number of in-box PowerShell modules to mark them as compatible with PowerShell Core.</span></span>

<span data-ttu-id="76103-175">Při spuštění PowerShell Core 6.1, bude automaticky obsahovat `$windir\System32` jako součást `PSModulePath` proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="76103-175">When PowerShell Core 6.1 starts up, it will automatically include `$windir\System32` as part of the `PSModulePath` environment variable.</span></span>
<span data-ttu-id="76103-176">Ale to zpřístupňuje pouze moduly, které `Get-Module` a `Import-Module` pokud jeho `CompatiblePSEdition` je označen jako kompatibilní se `Core`.</span><span class="sxs-lookup"><span data-stu-id="76103-176">However, it only exposes modules to `Get-Module` and `Import-Module` if its `CompatiblePSEdition` is marked as compatible with `Core`.</span></span>


```powershell
Get-Module -ListAvailable
```

> [!NOTE]
> <span data-ttu-id="76103-177">Může se zobrazit různé dostupné moduly v závislosti na tom, jaké role a funkce jsou nainstalovány.</span><span class="sxs-lookup"><span data-stu-id="76103-177">You may see different available modules depending on what roles and features are installed.</span></span>

```Output
...
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                                PSEdition ExportedCommands
---------- -------    ----                                --------- ----------------
Manifest   2.0.1.0    Appx                                Core,Desk {Add-AppxPackage, Get-AppxPackage, Get-AppxPacka...
Manifest   1.0.0.0    BitLocker                           Core,Desk {Unlock-BitLocker, Suspend-BitLocker, Resume-Bit...
Manifest   1.0.0.0    DnsClient                           Core,Desk {Resolve-DnsName, Clear-DnsClientCache, Get-DnsC...
Manifest   1.0.0.0    HgsDiagnostics                      Core,Desk {New-HgsTraceTarget, Get-HgsTrace, Get-HgsTraceF...
Binary     2.0.0.0    Hyper-V                             Core,Desk {Add-VMAssignableDevice, Add-VMDvdDrive, Add-VMF...
Binary     1.1        Hyper-V                             Core,Desk {Add-VMDvdDrive, Add-VMFibreChannelHba, Add-VMHa...
Manifest   2.0.0.0    NetAdapter                          Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetEventPacketCapture               Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                             Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                              Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                              Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                         Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam                       Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetWNV                              Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   2.0.0.0    TrustedPlatformModule               Core,Desk {Get-Tpm, Initialize-Tpm, Clear-Tpm, Unblock-Tpm...
...
```

<span data-ttu-id="76103-178">K zobrazení všech modulů pomocí toto chování můžete přepsat `-SkipEditionCheck` přepnout parametru.</span><span class="sxs-lookup"><span data-stu-id="76103-178">You can override this behavior to show all modules using the `-SkipEditionCheck` switch parameter.</span></span>
<span data-ttu-id="76103-179">Přidali jsme také `PSEdition` vlastnost do tabulkového výstupu.</span><span class="sxs-lookup"><span data-stu-id="76103-179">We've also added a `PSEdition` property to the table output.</span></span>

```powershell
Get-Module Net* -ListAvailable -SkipEditionCheck
```

```Output
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                        PSEdition ExportedCommands
---------- -------    ----                        --------- ----------------
Manifest   2.0.0.0    NetAdapter                  Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetConnection               Core,Desk {Get-NetConnectionProfile, Set-NetConnectionProf...
Manifest   1.0.0.0    NetDiagnostics              Desk      Get-NetView
Manifest   1.0.0.0    NetEventPacketCapture       Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                     Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                      Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                      Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                 Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam               Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetTCPIP                    Core,Desk {Get-NetIPAddress, Get-NetIPInterface, Get-NetIP...
Manifest   1.0.0.0    NetWNV                      Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   1.0.0.0    NetworkConnectivityStatus   Core,Desk {Get-DAConnectionStatus, Get-NCSIPolicyConfigura...
Manifest   1.0.0.0    NetworkSwitchManager        Core,Desk {Disable-NetworkSwitchEthernetPort, Enable-Netwo...
Manifest   1.0.0.0    NetworkTransition           Core,Desk {Add-NetIPHttpsCertBinding, Disable-NetDnsTransi...
```

<span data-ttu-id="76103-180">Další informace o tomto chování najdete [PowerShell RFC0025](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-PSCore6-and-Windows-Modules.md).</span><span class="sxs-lookup"><span data-stu-id="76103-180">For more information about this behavior, check out [PowerShell RFC0025](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-PSCore6-and-Windows-Modules.md).</span></span>

## <a name="markdown-cmdlets-and-rendering"></a><span data-ttu-id="76103-181">Rutiny markdown a vykreslování</span><span class="sxs-lookup"><span data-stu-id="76103-181">Markdown cmdlets and rendering</span></span>

<span data-ttu-id="76103-182">Markdown je standardní způsob vytváření dokumentů čitelné ve formátu prostého textu se základní formátování, které lze vykreslit do kódu HTML.</span><span class="sxs-lookup"><span data-stu-id="76103-182">Markdown is a standard for creating readable plaintext documents with basic formatting that can be rendered into HTML.</span></span>

<span data-ttu-id="76103-183">Přidali jsme některé rutiny v 6.1, která vám umožní převést a vykreslování Markdownu dokumentů v konzole, včetně:</span><span class="sxs-lookup"><span data-stu-id="76103-183">We've added some cmdlets in 6.1 that allow you to convert and render Markdown documents in the console, including:</span></span>

- `ConvertFrom-Markdown`
- `Get-MarkdownOption`
- `Set-MarkdownOption`
- `Show-Markdown`

<span data-ttu-id="76103-184">Například `Show-Markdown` vykreslí souboru Markdownu v konzole:</span><span class="sxs-lookup"><span data-stu-id="76103-184">For example, `Show-Markdown` renders a Markdown file in the console:</span></span>

![Příklad Markdownu show](./images/markdown_example.png)

<span data-ttu-id="76103-186">Další informace o tom, jak tyto rutiny fungují, přečtěte si [tento dokument RFC](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-Native-Markdown-Rendering.md).</span><span class="sxs-lookup"><span data-stu-id="76103-186">For more information about how these cmdlets work, check out [this RFC](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-Native-Markdown-Rendering.md).</span></span>

## <a name="experimental-feature-flags"></a><span data-ttu-id="76103-187">Příznaky experimentální funkce</span><span class="sxs-lookup"><span data-stu-id="76103-187">Experimental feature flags</span></span>

<span data-ttu-id="76103-188">Příznaky experimentální funkce povolit uživatele, aby na funkce, které nebyly byla dokončena.</span><span class="sxs-lookup"><span data-stu-id="76103-188">Experimental feature flags enable users to turn on features that haven't been finalized.</span></span>
<span data-ttu-id="76103-189">Tyto experimentální funkce nejsou podporované a může obsahovat chyby.</span><span class="sxs-lookup"><span data-stu-id="76103-189">These experimental features aren't supported and may have bugs.</span></span>

<span data-ttu-id="76103-190">Další informace o této funkci v [PowerShell RFC0029](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0029-Support-Experimental-Features.md).</span><span class="sxs-lookup"><span data-stu-id="76103-190">You can learn more about this feature in [PowerShell RFC0029](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0029-Support-Experimental-Features.md).</span></span>

## <a name="web-cmdlet-improvements"></a><span data-ttu-id="76103-191">Vylepšení webového rutiny</span><span class="sxs-lookup"><span data-stu-id="76103-191">Web cmdlet improvements</span></span>

<span data-ttu-id="76103-192">K [ @markekraus ](https://github.com/markekraus), celý slew vylepšení byly provedeny na náš web rutiny: [`Invoke-WebRequest`](/powershell/module/microsoft.powershell.utility/invoke-webrequest)</span><span class="sxs-lookup"><span data-stu-id="76103-192">Thanks to [@markekraus](https://github.com/markekraus), a whole slew of improvements have been made to our web cmdlets: [`Invoke-WebRequest`](/powershell/module/microsoft.powershell.utility/invoke-webrequest)</span></span>
<span data-ttu-id="76103-193">a [ `Invoke-RestMethod` ](/powershell/module/microsoft.powershell.utility/invoke-restmethod).</span><span class="sxs-lookup"><span data-stu-id="76103-193">and [`Invoke-RestMethod`](/powershell/module/microsoft.powershell.utility/invoke-restmethod).</span></span>

- <span data-ttu-id="76103-194">[Žádost o přijetí změn #6109](https://github.com/PowerShell/PowerShell/pull/6109) – výchozí kódování sady na UTF-8 pro `application-json` odpovědi</span><span class="sxs-lookup"><span data-stu-id="76103-194">[PR #6109](https://github.com/PowerShell/PowerShell/pull/6109) - default encoding set to UTF-8 for `application-json` responses</span></span>
- <span data-ttu-id="76103-195">[Žádost o přijetí změn #6018](https://github.com/PowerShell/PowerShell/pull/6018)  -  `-SkipHeaderValidation` parametr umožňující `Content-Type` hlavičky, které nejsou kompatibilní se standardy</span><span class="sxs-lookup"><span data-stu-id="76103-195">[PR #6018](https://github.com/PowerShell/PowerShell/pull/6018) - `-SkipHeaderValidation` parameter to allow `Content-Type` headers that aren't standards-compliant</span></span>
- <span data-ttu-id="76103-196">[Žádosti o přijetí změn #5972](https://github.com/PowerShell/PowerShell/pull/5972)  -  `Form` parametr pro podporu zjednodušená `multipart/form-data` podpory</span><span class="sxs-lookup"><span data-stu-id="76103-196">[PR #5972](https://github.com/PowerShell/PowerShell/pull/5972) - `Form` parameter to support simplified `multipart/form-data` support</span></span>
- <span data-ttu-id="76103-197">[Žádost o přijetí změn #6338](https://github.com/PowerShell/PowerShell/pull/6338) – vyhovují řadě požadavků a velkých a malých písmen zpracování klíčů relace</span><span class="sxs-lookup"><span data-stu-id="76103-197">[PR #6338](https://github.com/PowerShell/PowerShell/pull/6338) - Compliant, case-insensitive handling of relation keys</span></span>
- <span data-ttu-id="76103-198">[Žádost o přijetí změn #6447](https://github.com/PowerShell/PowerShell/pull/6447) – přidání `-Resume` parametr pro rutiny webových</span><span class="sxs-lookup"><span data-stu-id="76103-198">[PR #6447](https://github.com/PowerShell/PowerShell/pull/6447) - Add `-Resume` parameter for web cmdlets</span></span>

## <a name="remoting-improvements"></a><span data-ttu-id="76103-199">Vylepšení vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="76103-199">Remoting improvements</span></span>

### <a name="powershell-direct-tries-to-use-powershell-core-first"></a><span data-ttu-id="76103-200">Přímou službu PowerShell se pokusí nejprve použít PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="76103-200">PowerShell Direct tries to use PowerShell Core first</span></span>

<span data-ttu-id="76103-201">[Přímou službu PowerShell](/virtualization/hyper-v-on-windows/user-guide/powershell-direct) funkce je součástí prostředí PowerShell a technologie Hyper-V, který umožňuje připojení k virtuálnímu počítači s Hyper-V bez připojení k síti nebo jiné služby pro vzdálenou správu.</span><span class="sxs-lookup"><span data-stu-id="76103-201">[PowerShell Direct](/virtualization/hyper-v-on-windows/user-guide/powershell-direct) is a feature of PowerShell and Hyper-V that allows you to connect to a Hyper-V VM without network connectivity or other remote management services.</span></span>

<span data-ttu-id="76103-202">V minulosti přímou službu PowerShell připojené pomocí prostředí Windows PowerShell instance doručené pošty na virtuálním počítači.</span><span class="sxs-lookup"><span data-stu-id="76103-202">In the past, PowerShell Direct connected using the inbox Windows PowerShell instance on the VM.</span></span>
<span data-ttu-id="76103-203">Nyní, přímou službu PowerShell se nejprve pokusí připojit pomocí všechny dostupné `pwsh.exe` na `PATH` proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="76103-203">Now, PowerShell Direct first attempts to connect using any available `pwsh.exe` on the `PATH` environment variable.</span></span>
<span data-ttu-id="76103-204">Pokud `pwsh.exe` není k dispozici, přímou službu PowerShell spadne zpět na použití `powershell.exe`.</span><span class="sxs-lookup"><span data-stu-id="76103-204">If `pwsh.exe` isn't available, PowerShell Direct falls back to use `powershell.exe`.</span></span>

### <a name="enable-psremoting-now-creates-separate-remoting-endpoints-for-preview-versions"></a><span data-ttu-id="76103-205">`Enable-PSRemoting` nyní vytvoří samostatné vzdálené komunikace koncové body pro verze preview</span><span class="sxs-lookup"><span data-stu-id="76103-205">`Enable-PSRemoting` now creates separate remoting endpoints for preview versions</span></span>

<span data-ttu-id="76103-206">`Enable-PSRemoting` nyní vytvoří dvě konfigurace vzdálené komunikace relace:</span><span class="sxs-lookup"><span data-stu-id="76103-206">`Enable-PSRemoting` now creates two remoting session configurations:</span></span>

- <span data-ttu-id="76103-207">Jeden pro hlavní verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76103-207">One for the major version of PowerShell.</span></span> <span data-ttu-id="76103-208">Například`PowerShell.6`.</span><span class="sxs-lookup"><span data-stu-id="76103-208">For example,`PowerShell.6`.</span></span> <span data-ttu-id="76103-209">Tento koncový bod, který lze dovolávat napříč vedlejší verze aktualizace jako konfiguraci relace prostředí PowerShell 6 "celosystémovým"</span><span class="sxs-lookup"><span data-stu-id="76103-209">This endpoint that can be relied upon across minor version updates as the "system-wide" PowerShell 6 session configuration</span></span>
- <span data-ttu-id="76103-210">Jednu konfiguraci relace specifické pro verzi, například: `PowerShell.6.1.0`</span><span class="sxs-lookup"><span data-stu-id="76103-210">One version-specific session configuration, for example: `PowerShell.6.1.0`</span></span>

<span data-ttu-id="76103-211">Toto chování je užitečné, pokud chcete mít více verzí Powershellu 6 nainstalovaná a přístupná na stejném počítači.</span><span class="sxs-lookup"><span data-stu-id="76103-211">This behavior is useful if you want to have multiple PowerShell 6 versions installed and accessible on the same machine.</span></span>

<span data-ttu-id="76103-212">Kromě toho ve verzi preview verzí Powershellu teď mít své vlastní vzdálené komunikace konfiguracím relací po spuštění `Enable-PSRemoting` rutiny:</span><span class="sxs-lookup"><span data-stu-id="76103-212">Additionally, preview versions of PowerShell now get their own remoting session configurations after running the `Enable-PSRemoting` cmdlet:</span></span>

```powershell
C:\WINDOWS\system32> Enable-PSRemoting
```

<span data-ttu-id="76103-213">Výstup může lišit, pokud jste nenastavili WinRM před.</span><span class="sxs-lookup"><span data-stu-id="76103-213">Your output may be different if you haven't set up WinRM before.</span></span>

```Output
WinRM is already set up to receive requests on this computer.
WinRM is already set up for remote management on this computer.
```

<span data-ttu-id="76103-214">Pak můžete zobrazit samostatné konfigurace relace Powershellu ve verzi Preview a stabilní verze sestavení Powershellu 6 a u každé konkrétní verze.</span><span class="sxs-lookup"><span data-stu-id="76103-214">Then you can see separate PowerShell session configurations for the preview and stable builds of PowerShell 6, and for each specific version.</span></span>

```powershell
Get-PSSessionConfiguration
```

```Output
Name          : PowerShell.6.2-preview.1
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : PowerShell.6-preview
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6.1.0
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed
```

### <a name="userhostport-syntax-supported-for-ssh"></a><span data-ttu-id="76103-215">`user@host:port` Syntaxe podporovaných pro SSH</span><span class="sxs-lookup"><span data-stu-id="76103-215">`user@host:port` syntax supported for SSH</span></span>

<span data-ttu-id="76103-216">SSH klienti obvykle podporují připojovací řetězec ve formátu `user@host:port`.</span><span class="sxs-lookup"><span data-stu-id="76103-216">SSH clients typically support a connection string in the format `user@host:port`.</span></span>
<span data-ttu-id="76103-217">Přidání SSH jako protokol pro vzdálenou komunikaci prostředí PowerShell přidali jsme podporu pro tento formát připojovacího řetězce:</span><span class="sxs-lookup"><span data-stu-id="76103-217">With the addition of SSH as a protocol for PowerShell Remoting, we've added support for this format of connection string:</span></span>

`Enter-PSSession -HostName fooUser@ssh.contoso.com:2222`

## <a name="msi-option-to-add-explorer-shell-context-menu-on-windows"></a><span data-ttu-id="76103-218">Možnost Instalační služby MSI pro přidání místní nabídky prostředí Průzkumníka Windows</span><span class="sxs-lookup"><span data-stu-id="76103-218">MSI option to add explorer shell context menu on Windows</span></span>

<span data-ttu-id="76103-219">K [ @bergmeister ](https://github.com/bergmeister), teď můžete povolit kontextovou nabídku Windows.</span><span class="sxs-lookup"><span data-stu-id="76103-219">Thanks to [@bergmeister](https://github.com/bergmeister), now you can enable a context menu on Windows.</span></span> <span data-ttu-id="76103-220">Nyní můžete otevřít 6.1 prostředí PowerShell pro vaši instalaci systémová z libovolné složky v Průzkumníku Windows:</span><span class="sxs-lookup"><span data-stu-id="76103-220">Now you can open your system-wide installation of PowerShell 6.1 from any folder in the Windows Explorer:</span></span>

![Místní nabídka Shell pro PowerShell 6](./images/shell_context_menu.png)

## <a name="goodies"></a><span data-ttu-id="76103-222">Užitečné nástroje</span><span class="sxs-lookup"><span data-stu-id="76103-222">Goodies</span></span>

### <a name="run-as-administrator-in-the-windows-shortcut-jump-list"></a><span data-ttu-id="76103-223">"Spustit jako správce" v seznamu odkazů místní Windows</span><span class="sxs-lookup"><span data-stu-id="76103-223">"Run as Administrator" in the Windows shortcut jump list</span></span>

<span data-ttu-id="76103-224">K [ @bergmeister ](https://github.com/bergmeister), seznam odkazů na zástupce Powershellu Core teď obsahuje "Spustit jako správce":</span><span class="sxs-lookup"><span data-stu-id="76103-224">Thanks to [@bergmeister](https://github.com/bergmeister), the PowerShell Core shortcut's jump list now includes "Run as Administrator":</span></span>

![Spustit jako správce v seznamu skok PowerShell 6](./images/jumplist.png)

### <a name="cd---returns-to-previous-directory"></a><span data-ttu-id="76103-226">`cd -` Vrátí předchozí adresář</span><span class="sxs-lookup"><span data-stu-id="76103-226">`cd -` returns to previous directory</span></span>

```powershell
C:\Windows\System32> cd C:\
C:\> cd -
C:\Windows\System32>
```

<span data-ttu-id="76103-227">Nebo v Linuxu:</span><span class="sxs-lookup"><span data-stu-id="76103-227">Or on Linux:</span></span>

```ShellSession
PS /etc> cd /usr/bin
PS /usr/bin> cd -
PS /etc>
```

<span data-ttu-id="76103-228">Navíc `cd` a `cd --` změnit na `$HOME`.</span><span class="sxs-lookup"><span data-stu-id="76103-228">Also, `cd` and `cd --` change to `$HOME`.</span></span>

### `Test-Connection`

<span data-ttu-id="76103-229">K [ @iSazonov ](https://github.com/iSazonov), [ `Test-Connection` ](/powershell/module/microsoft.powershell.management/test-connection) rutiny má byla přenést do prostředí PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="76103-229">Thanks to [@iSazonov](https://github.com/iSazonov), the [`Test-Connection`](/powershell/module/microsoft.powershell.management/test-connection) cmdlet has been ported to PowerShell Core.</span></span>

### <a name="update-help-as-non-admin"></a><span data-ttu-id="76103-230">`Update-Help` jako bez oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="76103-230">`Update-Help` as non-admin</span></span>

<span data-ttu-id="76103-231">Zabývajících `Update-Help` už nebude potřeba spustit jako správce.</span><span class="sxs-lookup"><span data-stu-id="76103-231">By popular demand, `Update-Help` no longer needs to be run as an administrator.</span></span>
<span data-ttu-id="76103-232">`Update-Help` Teď výchozí ukládání nápovědy do složky s rozsahem uživatele.</span><span class="sxs-lookup"><span data-stu-id="76103-232">`Update-Help` now defaults to saving help to a user-scoped folder.</span></span>

### <a name="new-methodsproperties-on-pscustomobject"></a><span data-ttu-id="76103-233">Nové metody/vlastnosti `PSCustomObject`</span><span class="sxs-lookup"><span data-stu-id="76103-233">New methods/properties on `PSCustomObject`</span></span>

<span data-ttu-id="76103-234">K [ @iSazonov ](https://github.com/iSazonov), přidali jsme nové metody a vlastnosti, které chcete `PSCustomObject`.</span><span class="sxs-lookup"><span data-stu-id="76103-234">Thanks to [@iSazonov](https://github.com/iSazonov), we've added new methods and properties to `PSCustomObject`.</span></span>
<span data-ttu-id="76103-235">`PSCustomObject` nyní zahrnuje `Count` / `Length` vlastnost, která obsahuje počet položek.</span><span class="sxs-lookup"><span data-stu-id="76103-235">`PSCustomObject` now includes a `Count`/`Length` property that gives the number of items.</span></span>

<span data-ttu-id="76103-236">Oba tyto příklady vracejí `2` jako počet `PSCustomObjects` v kolekci.</span><span class="sxs-lookup"><span data-stu-id="76103-236">Both of these examples return `2` as the number of `PSCustomObjects` in the collection.</span></span>

```powershell
@(
[pscustomobject]@{foo = '1'},
[pscustomobject]@{bar = '2' }).Length
```

```powershell
@(
[pscustomobject]@{foo = '1'},
[pscustomobject]@{bar = '2' }).Count
```

<span data-ttu-id="76103-237">Tato práce zahrnuje také `ForEach` a `Where` metody, která umožňují jeho provoz a vyfiltrujte `PSCustomObject` položky:</span><span class="sxs-lookup"><span data-stu-id="76103-237">This work also includes `ForEach` and `Where` methods that allow you to operate and filter on `PSCustomObject` items:</span></span>

```powershell
@(
>> [pscustomobject]@{foo = 1},
>> [pscustomobject]@{foo = 2 }).ForEach({$_.foo+1})
```

```Output
2
3
```

```powershell
@(
>> [pscustomobject]@{foo = 1},
>> [pscustomobject]@{foo = 2 }).Where({$_.foo -gt 1})
```

```Output
foo
---
  2
```

### `Where-Object -Not`

<span data-ttu-id="76103-238">K @SimonWahlin, přidali jsme `-Not` parametr `Where-Object`.</span><span class="sxs-lookup"><span data-stu-id="76103-238">Thanks to @SimonWahlin, we've added the `-Not` parameter to `Where-Object`.</span></span>
<span data-ttu-id="76103-239">Teď můžete filtrovat objektu na kanál bez existuje, nebo hodnotu vlastnosti null nebo je prázdný.</span><span class="sxs-lookup"><span data-stu-id="76103-239">Now you can filter an object at the pipeline for the non-existence of a property, or a null/empty property value.</span></span>

<span data-ttu-id="76103-240">Tento příkaz například vrátí všechny služby, které nemají definované všechny závislé služby:</span><span class="sxs-lookup"><span data-stu-id="76103-240">For example, this command returns all services that don't have any dependent services defined:</span></span>

```powershell
Get-Service | Where-Object -Not DependentServices
```

### <a name="new-modulemanifest-creates-a-bom-less-utf-8-document"></a><span data-ttu-id="76103-241">`New-ModuleManifest` Vytvoří dokument bez BOM kódování UTF-8</span><span class="sxs-lookup"><span data-stu-id="76103-241">`New-ModuleManifest` creates a BOM-less UTF-8 document</span></span>

<span data-ttu-id="76103-242">Přesun věnovat bez BOM kódování UTF-8 v Powershellu 6.0, jsme aktualizovali `New-ModuleManifest` rutina pro vytvoření dokumentu bez BOM kódování UTF-8 namísto UTF-16, jeden.</span><span class="sxs-lookup"><span data-stu-id="76103-242">Given our move to BOM-less UTF-8 in PowerShell 6.0, we've updated the `New-ModuleManifest` cmdlet to create a BOM-less UTF-8 document instead of a UTF-16 one.</span></span>

### <a name="conversions-from-psmethod-to-delegate"></a><span data-ttu-id="76103-243">Převody z PSMethod delegáta</span><span class="sxs-lookup"><span data-stu-id="76103-243">Conversions from PSMethod to Delegate</span></span>

<span data-ttu-id="76103-244">K [ @powercode ](https://github.com/powercode), teď podporujeme převodu `PSMethod` delegátovi.</span><span class="sxs-lookup"><span data-stu-id="76103-244">Thanks to [@powercode](https://github.com/powercode), we now support the conversion of a `PSMethod` into a delegate.</span></span>
<span data-ttu-id="76103-245">Díky tomu můžete provést třeba k předávání `PSMethod` `[M]::DoubleStrLen` jako hodnotu delegáta do `[M]::AggregateString`:</span><span class="sxs-lookup"><span data-stu-id="76103-245">This allows you to do things like passing `PSMethod` `[M]::DoubleStrLen` as a delegate value into `[M]::AggregateString`:</span></span>

```powershell
class M {
    static [int] DoubleStrLen([string] $value) { return 2 * $value.Length }

    static [long] AggregateString([string[]] $values, [func[string, int]] $selector) {
        [long] $res = 0
        foreach($s in $values){
            $res += $selector.Invoke($s)
        }
        return $res
    }
}

[M]::AggregateString((gci).Name, [M]::DoubleStrLen)
```

<span data-ttu-id="76103-246">Další informace o této změně, projděte si [žádosti o přijetí změn #5287](https://github.com/PowerShell/PowerShell/pull/5287).</span><span class="sxs-lookup"><span data-stu-id="76103-246">For more info on this change, check out [PR #5287](https://github.com/PowerShell/PowerShell/pull/5287).</span></span>

### <a name="standard-deviation-in-measure-object"></a><span data-ttu-id="76103-247">Směrodatná odchylka `Measure-Object`</span><span class="sxs-lookup"><span data-stu-id="76103-247">Standard deviation in `Measure-Object`</span></span>

<span data-ttu-id="76103-248">K [ @CloudyDino ](https://github.com/CloudyDino), přidali jsme `StandardDeviation` vlastnost `Measure-Object`:</span><span class="sxs-lookup"><span data-stu-id="76103-248">Thanks to [@CloudyDino](https://github.com/CloudyDino), we've added a `StandardDeviation` property to `Measure-Object`:</span></span>

```powershell
Get-Process | Measure-Object -Property CPU -AllStats
```

```Output
Count             : 308
Average           : 31.3720576298701
Sum               : 9662.59375
Maximum           : 4416.046875
Minimum           :
StandardDeviation : 264.389544720926
Property          : CPU
```

### `GetPfxCertificate -Password`

<span data-ttu-id="76103-249">K [ @maybe-hello-world ](https://github.com/maybe-hello-world), `Get-PfxCertificate` má teď `Password` parametr, který přijímá `SecureString`.</span><span class="sxs-lookup"><span data-stu-id="76103-249">Thanks to [@maybe-hello-world](https://github.com/maybe-hello-world), `Get-PfxCertificate` now has the `Password` parameter, which takes a `SecureString`.</span></span> <span data-ttu-id="76103-250">To umožňuje používat neinteraktivně:</span><span class="sxs-lookup"><span data-stu-id="76103-250">This allows you to use it non-interactively:</span></span>

```powershell
$certFile = '\\server\share\pwd-protected.pfx'
$certPass = Read-Host -AsSecureString -Prompt 'Enter the password for certificate: '

$certThumbPrint = (Get-PfxCertificate -FilePath $certFile -Password $certPass ).ThumbPrint
```

### <a name="removal-of-the-more-function"></a><span data-ttu-id="76103-251">Odebrání `more` – funkce</span><span class="sxs-lookup"><span data-stu-id="76103-251">Removal of the `more` function</span></span>

<span data-ttu-id="76103-252">V minulosti, prostředí PowerShell dodané funkci v Windows volá `more` , která zabalena `more.com`.</span><span class="sxs-lookup"><span data-stu-id="76103-252">In the past, PowerShell shipped a function on Windows called `more` that wrapped `more.com`.</span></span>
<span data-ttu-id="76103-253">Tato funkce se odebralo.</span><span class="sxs-lookup"><span data-stu-id="76103-253">That function has now been removed.</span></span>

<span data-ttu-id="76103-254">Také `help` funkce změněn, aby používal `more.com` na Windows nebo v systému výchozí operátor určené `$env:PAGER` na platformách než Windows.</span><span class="sxs-lookup"><span data-stu-id="76103-254">Also the `help` function changed to use `more.com` on Windows, or the system's default pager specified by `$env:PAGER` on non-Windows platforms.</span></span>

### <a name="cd-drivename-now-returns-users-to-the-current-working-directory-in-that-drive"></a><span data-ttu-id="76103-255">`cd DriveName:` nyní vrátí uživatele do aktuálního pracovního adresáře na tomto disku</span><span class="sxs-lookup"><span data-stu-id="76103-255">`cd DriveName:` now returns users to the current working directory in that drive</span></span>

<span data-ttu-id="76103-256">Dříve, pomocí `Set-Location` nebo `cd` se vraťte do PSDrive uživatelům odesílat výchozí umístění pro tuto jednotku.</span><span class="sxs-lookup"><span data-stu-id="76103-256">Previously, using `Set-Location` or `cd` to return to a PSDrive sent users to the default location for that drive.</span></span>

<span data-ttu-id="76103-257">K [ @mcbobke ](https://github.com/mcbobke), uživatelům se nyní odesílají na poslední známé aktuální pracovní adresář pro danou relaci.</span><span class="sxs-lookup"><span data-stu-id="76103-257">Thanks to [@mcbobke](https://github.com/mcbobke), users are now sent to the last known current working directory for that session.</span></span>

### <a name="windows-powershell-type-accelerators"></a><span data-ttu-id="76103-258">Akcelerátory typ prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="76103-258">Windows PowerShell type accelerators</span></span>

<span data-ttu-id="76103-259">V prostředí Windows PowerShell jsme zahrnuli následující typ akcelerátory usnadnit práci s jejich odpovídající typy:</span><span class="sxs-lookup"><span data-stu-id="76103-259">In Windows PowerShell, we included the following type accelerators to make it easier to work with their respective types:</span></span>

- <span data-ttu-id="76103-260">`[adsi]`: `System.DirectoryServices.DirectoryEntry`</span><span class="sxs-lookup"><span data-stu-id="76103-260">`[adsi]`: `System.DirectoryServices.DirectoryEntry`</span></span>
- <span data-ttu-id="76103-261">`[adsisearcher]`: `System.DirectoryServices.DirectorySearcher`</span><span class="sxs-lookup"><span data-stu-id="76103-261">`[adsisearcher]`: `System.DirectoryServices.DirectorySearcher`</span></span>
- <span data-ttu-id="76103-262">`[wmi]`: `System.Management.ManagementObject`</span><span class="sxs-lookup"><span data-stu-id="76103-262">`[wmi]`: `System.Management.ManagementObject`</span></span>
- <span data-ttu-id="76103-263">`[wmiclass]`: `System.Management.ManagementClass`</span><span class="sxs-lookup"><span data-stu-id="76103-263">`[wmiclass]`: `System.Management.ManagementClass`</span></span>
- <span data-ttu-id="76103-264">`[wmisearcher]`: `System.Management.ManagementObjectSearcher`</span><span class="sxs-lookup"><span data-stu-id="76103-264">`[wmisearcher]`: `System.Management.ManagementObjectSearcher`</span></span>

<span data-ttu-id="76103-265">Tyto klávesové zkratky typu nejsou zahrnuty v Powershellu 6, ale byly přidány do prostředí PowerShell 6.1 a systémem Windows.</span><span class="sxs-lookup"><span data-stu-id="76103-265">These type accelerators were not included in PowerShell 6, but have been added to PowerShell 6.1 running on Windows.</span></span>

<span data-ttu-id="76103-266">Tyto typy jsou užitečné pro snadné vytváření AD a objekty rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="76103-266">These types are useful in easily constructing AD and WMI objects.</span></span>

<span data-ttu-id="76103-267">Například můžete zadávat dotazy pomocí protokolu LDAP:</span><span class="sxs-lookup"><span data-stu-id="76103-267">For example, you can query using LDAP:</span></span>

```powershell
[adsi]'LDAP://CN=FooUse,OU=People,DC=contoso,DC=com'
```

<span data-ttu-id="76103-268">Následující příklad vytvoří objekt Win32_OperatingSystem CIM:</span><span class="sxs-lookup"><span data-stu-id="76103-268">Following example creates a Win32_OperatingSystem CIM object:</span></span>

```powershell
[wmi]"Win32_OperatingSystem=@"
```

```Output
SystemDirectory : C:\WINDOWS\system32
Organization    : Contoso IT
BuildNumber     : 18234
RegisteredUser  : Contoso Corp.
SerialNumber    : 12345-67890-ABCDE-F0123
Version         : 10.0.18234
```

<span data-ttu-id="76103-269">V tomto příkladu vrátí objekt ManagementClass Win32_OperatingSystem třídy.</span><span class="sxs-lookup"><span data-stu-id="76103-269">This example returns a ManagementClass object for Win32_OperatingSystem class.</span></span>

```powershell
[wmiclass]"Win32_OperatingSystem"
```

```Output
   NameSpace: ROOT\cimv2

Name                                Methods              Properties
----                                -------              ----------
Win32_OperatingSystem               {Reboot, Shutdown... {BootDevice, BuildNumber, BuildType, Caption...}
```

### <a name="-lp-alias-for-all--literalpath-parameters"></a><span data-ttu-id="76103-270">`-lp` alias pro všechny `-LiteralPath` parametry</span><span class="sxs-lookup"><span data-stu-id="76103-270">`-lp` alias for all `-LiteralPath` parameters</span></span>

<span data-ttu-id="76103-271">K [ @kvprasoon ](https://github.com/kvprasoon), nyní je k dispozici alias parametru `-lp` pro všechny integrované rutiny Powershellu, které mají `-LiteralPath` parametru.</span><span class="sxs-lookup"><span data-stu-id="76103-271">Thanks to [@kvprasoon](https://github.com/kvprasoon), we now have a parameter alias `-lp` for all the built-in PowerShell cmdlets that have a `-LiteralPath` parameter.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="76103-272">Rozbíjející změny v</span><span class="sxs-lookup"><span data-stu-id="76103-272">Breaking Changes</span></span>

### <a name="msi-based-installation-paths-on-windows"></a><span data-ttu-id="76103-273">Instalace pomocí MSI cesty ve Windows</span><span class="sxs-lookup"><span data-stu-id="76103-273">MSI-based installation paths on Windows</span></span>

<span data-ttu-id="76103-274">Na Windows nyní balíček MSI instaluje do následujícího umístění:</span><span class="sxs-lookup"><span data-stu-id="76103-274">On Windows, the MSI package now installs to the following path:</span></span>

- <span data-ttu-id="76103-275">`$env:ProgramFiles\PowerShell\6\` pro stabilní instalaci 6.x</span><span class="sxs-lookup"><span data-stu-id="76103-275">`$env:ProgramFiles\PowerShell\6\` for the stable installation of 6.x</span></span>
- <span data-ttu-id="76103-276">`$env:ProgramFiles\PowerShell\6-preview\` pro instalaci preview 6.x</span><span class="sxs-lookup"><span data-stu-id="76103-276">`$env:ProgramFiles\PowerShell\6-preview\` for the preview installation of 6.x</span></span>

<span data-ttu-id="76103-277">Tato změna zajišťuje PowerShell Core může být aktualizován/obsluhovány pomocí Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="76103-277">This change ensures that PowerShell Core can be updated/serviced by Microsoft Update.</span></span>

<span data-ttu-id="76103-278">Další informace, podívejte se na [PowerShell RFC0026](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0026-MSI-Installation-Path.md).</span><span class="sxs-lookup"><span data-stu-id="76103-278">For more information, check out [PowerShell RFC0026](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0026-MSI-Installation-Path.md).</span></span>

### <a name="telemetry-can-only-be-disabled-with-an-environment-variable"></a><span data-ttu-id="76103-279">Telemetrie se dá deaktivovat jenom s proměnnou prostředí</span><span class="sxs-lookup"><span data-stu-id="76103-279">Telemetry can only be disabled with an environment variable</span></span>

<span data-ttu-id="76103-280">PowerShell Core odesílá základní telemetrická data do Microsoftu při jeho spuštění.</span><span class="sxs-lookup"><span data-stu-id="76103-280">PowerShell Core sends basic telemetry data to Microsoft when it is launched.</span></span> <span data-ttu-id="76103-281">Data obsahují název operačního systému, verze operačního systému a verze prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76103-281">The data includes the OS name, OS version, and PowerShell version.</span></span> <span data-ttu-id="76103-282">Tato data umožňují nám lépe pochopit prostředí, ve kterém se používá prostředí PowerShell a umožňuje nám to určit prioritu nových funkcí a oprav.</span><span class="sxs-lookup"><span data-stu-id="76103-282">This data allows us to better understand the environments where PowerShell is used and enables us to prioritize new features and fixes.</span></span>

<span data-ttu-id="76103-283">Odhlásit z této telemetrická data, nastavte proměnnou prostředí `POWERSHELL_TELEMETRY_OPTOUT` k `true`, `yes`, nebo `1`.</span><span class="sxs-lookup"><span data-stu-id="76103-283">To opt-out of this telemetry, set the environment variable `POWERSHELL_TELEMETRY_OPTOUT` to `true`, `yes`, or `1`.</span></span> <span data-ttu-id="76103-284">Odstranění souboru už nadále nepodporujeme `DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` zakázat telemetrii.</span><span class="sxs-lookup"><span data-stu-id="76103-284">We no longer support deletion of the file `DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` to disable telemetry.</span></span>

### <a name="disallowed-basic-auth-over-http-in-powershell-remoting-on-unix-platforms"></a><span data-ttu-id="76103-285">Zakázané základního ověřování prostřednictvím protokolu HTTP při vzdálené komunikaci Powershellu na platformách systému Unix</span><span class="sxs-lookup"><span data-stu-id="76103-285">Disallowed Basic Auth over HTTP in PowerShell Remoting on Unix platforms</span></span>

<span data-ttu-id="76103-286">Zabránit používání nešifrované přenosy, vzdálené komunikace Powershellu na platformy Unix nyní vyžaduje použití protokolu NTLM nebo Negotiate, nebo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="76103-286">To prevent the use of unencrypted traffic, PowerShell Remoting on Unix platforms now requires usage of NTLM/Negotiate or HTTPS.</span></span>

<span data-ttu-id="76103-287">Další informace o těchto změnách, přečtěte si [žádosti o přijetí změn #6799](https://github.com/PowerShell/PowerShell/pull/6799).</span><span class="sxs-lookup"><span data-stu-id="76103-287">For more information on these changes, check out [PR #6799](https://github.com/PowerShell/PowerShell/pull/6799).</span></span>

### <a name="removed-visualbasic-as-a-supported-language-in-add-type"></a><span data-ttu-id="76103-288">Odebrat `VisualBasic` jako podporovaný jazyk v Add-Type</span><span class="sxs-lookup"><span data-stu-id="76103-288">Removed `VisualBasic` as a supported language in Add-Type</span></span>

<span data-ttu-id="76103-289">V minulosti by mohla kompilaci kódu pomocí jazyka Visual Basic `Add-Type` rutiny.</span><span class="sxs-lookup"><span data-stu-id="76103-289">In the past, you could compile Visual Basic code using the `Add-Type` cmdlet.</span></span>
<span data-ttu-id="76103-290">Jen zřídka se používá jazyka Visual Basic s `Add-Type`.</span><span class="sxs-lookup"><span data-stu-id="76103-290">Visual Basic was rarely used with `Add-Type`.</span></span> <span data-ttu-id="76103-291">Odebrali jsme tato změna povede ke zmenšení velikosti prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76103-291">We removed this feature to reduce the size of PowerShell.</span></span>

### <a name="cleaned-up-uses-of-commandtypesworkflow-and-workflowinfocleaned"></a><span data-ttu-id="76103-292">Vyčištění použití `CommandTypes.Workflow` a `WorkflowInfoCleaned`</span><span class="sxs-lookup"><span data-stu-id="76103-292">Cleaned up uses of `CommandTypes.Workflow` and `WorkflowInfoCleaned`</span></span>

<span data-ttu-id="76103-293">Další informace o těchto změnách, přečtěte si [žádosti o přijetí změn #6708](https://github.com/PowerShell/PowerShell/pull/6708).</span><span class="sxs-lookup"><span data-stu-id="76103-293">For more information on these changes, check out [PR #6708](https://github.com/PowerShell/PowerShell/pull/6708).</span></span>

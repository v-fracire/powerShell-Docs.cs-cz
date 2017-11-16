---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
title: "Vylepšení konzoly v WMF 5.1"
ms.openlocfilehash: b0859191ea310c9b73fe9f255d7f256a1cc1af1f
ms.sourcegitcommit: fee03bb9802222078c8d5f6c8efb0698024406ed
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/27/2017
---
# <a name="console-improvements-in-wmf-51"></a><span data-ttu-id="e0c7c-103">Vylepšení konzoly v WMF 5.1#</span><span class="sxs-lookup"><span data-stu-id="e0c7c-103">Console Improvements in WMF 5.1#</span></span>

## <a name="powershell-console-improvements"></a><span data-ttu-id="e0c7c-104">Vylepšení konzoly prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0c7c-104">PowerShell console improvements</span></span>

<span data-ttu-id="e0c7c-105">Powershell.exe v WMF 5.1 provedly lepší konzoly následující změny:</span><span class="sxs-lookup"><span data-stu-id="e0c7c-105">The following changes have been made to powershell.exe in WMF 5.1 to improve the console experience:</span></span>

###<a name="vt100-support"></a><span data-ttu-id="e0c7c-106">Podpora VT100</span><span class="sxs-lookup"><span data-stu-id="e0c7c-106">VT100 support</span></span>

<span data-ttu-id="e0c7c-107">Přidání podpory pro Windows 10 [VT100 řídicí sekvence](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="e0c7c-107">Windows 10 added support for [VT100 escape sequences](https://msdn.microsoft.com/en-us/library/windows/desktop/mt638032(v=vs.85).aspx).</span></span>
<span data-ttu-id="e0c7c-108">Prostředí PowerShell bude ignorovat určité VT100 formátování řídicí sekvence při výpočtu šířky tabulky.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-108">PowerShell will ignore certain VT100 formatting escape sequences when calculating table widths.</span></span>

<span data-ttu-id="e0c7c-109">Prostředí PowerShell také přidat nové rozhraní API, který lze použít při formátování kódu k určení, jestli VT100 podporovaná.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-109">PowerShell also added a new API that can be used in formatting code to determine if VT100 is supported.</span></span> <span data-ttu-id="e0c7c-110">Příklad:</span><span class="sxs-lookup"><span data-stu-id="e0c7c-110">For example:</span></span>

```
if ($host.UI.SupportsVirtualTerminal)
{
    $esc = [char]0x1b
    "A yellow ${esc}[93mhello${esc}[0m"
}
else
{
    "A default hello"
}
```
<span data-ttu-id="e0c7c-111">Zde je úplná [příklad](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) který slouží k zvýrazněte odpovídá řetězci vyberte.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-111">Here is a complete [example](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) that can be used to highlight matches from Select-String.</span></span>
<span data-ttu-id="e0c7c-112">Uložit v příkladu v souboru s názvem `MatchInfo.format.ps1xml`, pokud chcete používat, v profilu nebo jinde, spusťte `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-112">Save the example in a file named `MatchInfo.format.ps1xml`, then to use it, in your profile or elsewhere, run `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span></span>

<span data-ttu-id="e0c7c-113">Všimněte si, že VT100 řídicí sekvence jsou podporovány pouze v počínaje systémem Windows 10 Anniversary aktualizace; v předchozích verzích systému nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-113">Note that VT100 escape sequences are only supported starting with the Windows 10 Anniversary update; they are not supported on earlier systems.</span></span>   

### <a name="vi-mode-support-in-psreadline"></a><span data-ttu-id="e0c7c-114">Podpora režimu VI v PSReadline</span><span class="sxs-lookup"><span data-stu-id="e0c7c-114">Vi mode support in PSReadline</span></span>

<span data-ttu-id="e0c7c-115">[PSReadline](https://github.com/lzybkr/PSReadLine) přidá podporu vi režimu.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-115">[PSReadline](https://github.com/lzybkr/PSReadLine) adds support for vi mode.</span></span> <span data-ttu-id="e0c7c-116">Chcete-li použít režim vi, spusťte `Set-PSReadlineOption -EditMode Vi`.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-116">To use vi mode, run `Set-PSReadlineOption -EditMode Vi`.</span></span>

### <a name="redirected-stdin-with-interactive-input"></a><span data-ttu-id="e0c7c-117">Přesměrovaného stdin – s interaktivní vstup</span><span class="sxs-lookup"><span data-stu-id="e0c7c-117">Redirected stdin with interactive input</span></span> 

<span data-ttu-id="e0c7c-118">V dřívějších verzích, spouštění prostředí PowerShell s `powershell -File -` nebyla nutná, pokud byl přesměrován stdin – a chcete zadat příkazy interaktivně.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-118">In earlier versions, starting PowerShell with `powershell -File -` was required when stdin was redirected and you wanted to enter commands interactively.</span></span>

<span data-ttu-id="e0c7c-119">S WMF 5.1, tento obtížné zjistit, že je možnost už nebude potřeba.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-119">With WMF 5.1, this hard to discover option is no longer necessary.</span></span> <span data-ttu-id="e0c7c-120">Prostředí PowerShell můžete spustit bez jakékoli možnosti, například `powershell`.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-120">You can start PowerShell without any options, e.g. `powershell`.</span></span>

<span data-ttu-id="e0c7c-121">Všimněte si, že PSReadline v současné době nepodporuje přesměrování stdin a integrované příkazového řádku úpravy zkušenosti s přesměrovaného stdin je velmi omezené, například nejsou funkční klávesy se šipkami.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-121">Note that PSReadline does not currently support redirected stdin, and the built-in command-line editing experience with redirected stdin is extremely limited, for example, arrow keys don't work.</span></span> <span data-ttu-id="e0c7c-122">Budoucích vydání systému PSReadline by měl tento problém vyřešit.</span><span class="sxs-lookup"><span data-stu-id="e0c7c-122">A future release of PSReadline should address this issue.</span></span>   

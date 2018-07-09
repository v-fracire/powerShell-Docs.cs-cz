---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
title: Vylepšení konzoly ve WMF 5.1
ms.openlocfilehash: a8e82e2f973916c2ed5007eba90ee6f2b7a9a769
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892922"
---
# <a name="console-improvements-in-wmf-51"></a><span data-ttu-id="1cc76-103">Vylepšení konzoly ve WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="1cc76-103">Console Improvements in WMF 5.1</span></span>

## <a name="powershell-console-improvements"></a><span data-ttu-id="1cc76-104">Vylepšení konzoly Powershellu</span><span class="sxs-lookup"><span data-stu-id="1cc76-104">PowerShell console improvements</span></span>

<span data-ttu-id="1cc76-105">Byly provedeny následující změny k powershell.exe ve WMF 5.1 na zlepšení uživatelského rozhraní konzoly:</span><span class="sxs-lookup"><span data-stu-id="1cc76-105">The following changes have been made to powershell.exe in WMF 5.1 to improve the console experience:</span></span>

### <a name="vt100-support"></a><span data-ttu-id="1cc76-106">Podpora VT100</span><span class="sxs-lookup"><span data-stu-id="1cc76-106">VT100 support</span></span>

<span data-ttu-id="1cc76-107">Přidání podpory pro Windows 10 [VT100 řídicí sekvence](/windows/console/console-virtual-terminal-sequences).</span><span class="sxs-lookup"><span data-stu-id="1cc76-107">Windows 10 added support for [VT100 escape sequences](/windows/console/console-virtual-terminal-sequences).</span></span>
<span data-ttu-id="1cc76-108">Prostředí PowerShell bude ignorovat určité VT100 formátování řídicí sekvence při výpočtu šířky tabulky.</span><span class="sxs-lookup"><span data-stu-id="1cc76-108">PowerShell will ignore certain VT100 formatting escape sequences when calculating table widths.</span></span>

<span data-ttu-id="1cc76-109">Prostředí PowerShell také přidali nová rozhraní API, které lze použít při formátování kódu k určení, jestli je podporovaná VT100.</span><span class="sxs-lookup"><span data-stu-id="1cc76-109">PowerShell also added a new API that can be used in formatting code to determine if VT100 is supported.</span></span>
<span data-ttu-id="1cc76-110">Příklad:</span><span class="sxs-lookup"><span data-stu-id="1cc76-110">For example:</span></span>

```powershell
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

<span data-ttu-id="1cc76-111">Tady je úplný [příklad](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) , který lze použít ke zvýraznění shody z `Select-String`.</span><span class="sxs-lookup"><span data-stu-id="1cc76-111">Here is a complete [example](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7) that can be used to highlight matches from `Select-String`.</span></span>
<span data-ttu-id="1cc76-112">Uložit v příkladu v souboru s názvem `MatchInfo.format.ps1xml`, pokud chcete použít, v profilu nebo jinde, spusťte `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span><span class="sxs-lookup"><span data-stu-id="1cc76-112">Save the example in a file named `MatchInfo.format.ps1xml`, then to use it, in your profile or elsewhere, run `Update-FormatData -Prepend MatchInfo.format.ps1xml`.</span></span>

<span data-ttu-id="1cc76-113">Všimněte si, že sekvence escape VT100 podporují jenom od verze Windows 10 Anniversary update; nejsou podporovány v předchozích verzích systému.</span><span class="sxs-lookup"><span data-stu-id="1cc76-113">Note that VT100 escape sequences are only supported starting with the Windows 10 Anniversary update; they are not supported on earlier systems.</span></span>

### <a name="vi-mode-support-in-psreadline"></a><span data-ttu-id="1cc76-114">Podpora režimu VI v PSReadline</span><span class="sxs-lookup"><span data-stu-id="1cc76-114">Vi mode support in PSReadline</span></span>

<span data-ttu-id="1cc76-115">[PSReadline](https://github.com/lzybkr/PSReadLine) přidává podporu pro režim editoru vi.</span><span class="sxs-lookup"><span data-stu-id="1cc76-115">[PSReadline](https://github.com/lzybkr/PSReadLine) adds support for vi mode.</span></span> <span data-ttu-id="1cc76-116">Pokud chcete použít režim vi, spusťte `Set-PSReadlineOption -EditMode Vi`.</span><span class="sxs-lookup"><span data-stu-id="1cc76-116">To use vi mode, run `Set-PSReadlineOption -EditMode Vi`.</span></span>

### <a name="redirected-stdin-with-interactive-input"></a><span data-ttu-id="1cc76-117">Přesměrované stdin s interaktivní vstup</span><span class="sxs-lookup"><span data-stu-id="1cc76-117">Redirected stdin with interactive input</span></span>

<span data-ttu-id="1cc76-118">V dřívějších verzích spuštění Powershellu s `powershell -File -` byla požadována, když byl přesměrován stdin a chcete zadat příkazy interaktivně.</span><span class="sxs-lookup"><span data-stu-id="1cc76-118">In earlier versions, starting PowerShell with `powershell -File -` was required when stdin was redirected and you wanted to enter commands interactively.</span></span>

<span data-ttu-id="1cc76-119">S WMF 5.1, tomto je obtížné zjistit, že možnost již není nezbytné.</span><span class="sxs-lookup"><span data-stu-id="1cc76-119">With WMF 5.1, this hard to discover option is no longer necessary.</span></span>
<span data-ttu-id="1cc76-120">Prostředí PowerShell můžete spustit bez jakýchkoli možností, například `powershell`.</span><span class="sxs-lookup"><span data-stu-id="1cc76-120">You can start PowerShell without any options, e.g. `powershell`.</span></span>

<span data-ttu-id="1cc76-121">Všimněte si, že PSReadline v současné době nepodporuje přesměrováno stdin a integrované prostředí příkazového řádku úprav s přesměrovaného stdin je velmi omezené, třeba klávesy se šipkami nefungují.</span><span class="sxs-lookup"><span data-stu-id="1cc76-121">Note that PSReadline does not currently support redirected stdin, and the built-in command-line editing experience with redirected stdin is extremely limited, for example, arrow keys don't work.</span></span>
<span data-ttu-id="1cc76-122">Příští verzi PSReadline by měla tento problém vyřešit.</span><span class="sxs-lookup"><span data-stu-id="1cc76-122">A future release of PSReadline should address this issue.</span></span>
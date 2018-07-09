---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Vylepšení Powershellového jádra ve WMF 5.1
ms.openlocfilehash: 738f72b910de7d44f48309013237d523d0dd40a4
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892888"
---
# <a name="powershell-engine-improvements"></a><span data-ttu-id="11717-103">Vylepšení Powershellového jádra</span><span class="sxs-lookup"><span data-stu-id="11717-103">PowerShell Engine Improvements</span></span>

<span data-ttu-id="11717-104">Následující vylepšení modul PowerShell core je implementovaná v WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="11717-104">The following improvements to the core PowerShell engine have been implemented in WMF 5.1:</span></span>

## <a name="performance"></a><span data-ttu-id="11717-105">Výkon</span><span class="sxs-lookup"><span data-stu-id="11717-105">Performance</span></span>

<span data-ttu-id="11717-106">V některých důležitých oblastech se zvýšil výkon:</span><span class="sxs-lookup"><span data-stu-id="11717-106">Performance has improved in some important areas:</span></span>

- <span data-ttu-id="11717-107">Spuštění</span><span class="sxs-lookup"><span data-stu-id="11717-107">Startup</span></span>
- <span data-ttu-id="11717-108">Zřetězení příkazů do rutin jako `ForEach-Object` a `Where-Object` je přibližně 50 % rychlejší</span><span class="sxs-lookup"><span data-stu-id="11717-108">Pipelining to cmdlets like `ForEach-Object` and `Where-Object` is approximately 50% faster</span></span>

<span data-ttu-id="11717-109">Některé příklad vylepšení (výsledky mohou lišit v závislosti na hardwaru):</span><span class="sxs-lookup"><span data-stu-id="11717-109">Some example improvements (your results may vary depending on your hardware):</span></span>

| <span data-ttu-id="11717-110">Scénář</span><span class="sxs-lookup"><span data-stu-id="11717-110">Scenario</span></span> | <span data-ttu-id="11717-111">5.0 doba (ms)</span><span class="sxs-lookup"><span data-stu-id="11717-111">5.0 Time (ms)</span></span> | <span data-ttu-id="11717-112">5.1 doba (ms)</span><span class="sxs-lookup"><span data-stu-id="11717-112">5.1 Time (ms)</span></span> |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | <span data-ttu-id="11717-113">900</span><span class="sxs-lookup"><span data-stu-id="11717-113">900</span></span> | <span data-ttu-id="11717-114">250</span><span class="sxs-lookup"><span data-stu-id="11717-114">250</span></span> |
| <span data-ttu-id="11717-115">První někdy spustit prostředí PowerShell: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="11717-115">First ever PowerShell run: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="11717-116">30000</span><span class="sxs-lookup"><span data-stu-id="11717-116">30000</span></span> | <span data-ttu-id="11717-117">13000</span><span class="sxs-lookup"><span data-stu-id="11717-117">13000</span></span> |
| <span data-ttu-id="11717-118">Vytvořená mezipaměť analýzy příkazu: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="11717-118">Command analysis cache built: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="11717-119">7000</span><span class="sxs-lookup"><span data-stu-id="11717-119">7000</span></span> | <span data-ttu-id="11717-120">520</span><span class="sxs-lookup"><span data-stu-id="11717-120">520</span></span> |
| <code>1..1000000 &#124; % { }</code> | <span data-ttu-id="11717-121">1400</span><span class="sxs-lookup"><span data-stu-id="11717-121">1400</span></span> | <span data-ttu-id="11717-122">750</span><span class="sxs-lookup"><span data-stu-id="11717-122">750</span></span> |

> [!Note]
> <span data-ttu-id="11717-123">Jednu změnu související se spouštěcí může mít vliv na některé nepodporované scénáře.</span><span class="sxs-lookup"><span data-stu-id="11717-123">One change related to startup might impact some unsupported scenarios.</span></span>
> <span data-ttu-id="11717-124">Prostředí PowerShell již načte soubory `$pshome\*.ps1xml` – tyto soubory byly převedeny do jazyka C#, aby některý soubor a režie procesoru zpracování souboru XML soubory.</span><span class="sxs-lookup"><span data-stu-id="11717-124">PowerShell no longer reads the files `$pshome\*.ps1xml` -- these files have been converted to C# to avoid some file and CPU overhead of processing the XML files.</span></span>
> <span data-ttu-id="11717-125">Soubory stále existují podpoře V2 side-by-side, takže pokud změníte obsah souboru, to nebude mít žádný vliv na V5, pouze V2.</span><span class="sxs-lookup"><span data-stu-id="11717-125">The files still exist to support V2 side-by-side, so if you change the file contents, it will not have any effect to V5, only V2.</span></span>
> <span data-ttu-id="11717-126">Všimněte si, že změna obsah těchto souborů se nikdy podporovaný scénář.</span><span class="sxs-lookup"><span data-stu-id="11717-126">Note that changing the contents of these files was never a supported scenario.</span></span>

<span data-ttu-id="11717-127">Další viditelné změnou je, jak Powershellu uloží exportované příkazy a další informace pro moduly, které jsou nainstalované v systému.</span><span class="sxs-lookup"><span data-stu-id="11717-127">Another visible change is how PowerShell caches the exported commands and other information for modules that are installed on a system.</span></span>
<span data-ttu-id="11717-128">Dříve byla tato mezipaměť uložen v adresáři `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span><span class="sxs-lookup"><span data-stu-id="11717-128">Previously, this cache was stored in the directory `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span></span>
<span data-ttu-id="11717-129">Ve WMF 5.1 mezipaměť je jeden soubor `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="11717-129">In WMF 5.1, the cache is a single file `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="11717-130">Zobrazit [modul analýzy mezipaměti](scenarios-features.md#module-analysis-cache) další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="11717-130">See [Module Analysis Cache](scenarios-features.md#module-analysis-cache) for more details.</span></span>
---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: Modul prostředí PowerShell vylepšení v WMF 5.1
ms.openlocfilehash: 3c69c4e13f64683f743eb78b0c9e177ff5b3a771
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
#<a name="powershell-engine-improvements"></a><span data-ttu-id="065f7-103">Vylepšení modul prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="065f7-103">PowerShell Engine Improvements</span></span>

<span data-ttu-id="065f7-104">Následující vylepšení k modulu jádra prostředí PowerShell je implementovaná v WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="065f7-104">The following improvements to the core PowerShell engine have been implemented in WMF 5.1:</span></span>


## <a name="performance"></a><span data-ttu-id="065f7-105">Výkon</span><span class="sxs-lookup"><span data-stu-id="065f7-105">Performance</span></span> ##

<span data-ttu-id="065f7-106">Výkon je vyšší, v některé důležité oblasti:</span><span class="sxs-lookup"><span data-stu-id="065f7-106">Performance has improved in some important areas:</span></span>

- <span data-ttu-id="065f7-107">Spuštění</span><span class="sxs-lookup"><span data-stu-id="065f7-107">Startup</span></span>
- <span data-ttu-id="065f7-108">Zřetězení příkazů do rutin jako ForEach-Object a Where-Object je přibližně 50 % rychlejší</span><span class="sxs-lookup"><span data-stu-id="065f7-108">Pipelining to cmdlets like ForEach-Object and Where-Object is approximately 50% faster</span></span>

<span data-ttu-id="065f7-109">Některé příklad vylepšení (výsledky se liší v závislosti na hardwaru):</span><span class="sxs-lookup"><span data-stu-id="065f7-109">Some example improvements (your results may vary depending on your hardware):</span></span>

| <span data-ttu-id="065f7-110">Scénář</span><span class="sxs-lookup"><span data-stu-id="065f7-110">Scenario</span></span> | <span data-ttu-id="065f7-111">5.0 čas (ms)</span><span class="sxs-lookup"><span data-stu-id="065f7-111">5.0 Time (ms)</span></span> | <span data-ttu-id="065f7-112">5.1 čas (ms)</span><span class="sxs-lookup"><span data-stu-id="065f7-112">5.1 Time (ms)</span></span> |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | <span data-ttu-id="065f7-113">900</span><span class="sxs-lookup"><span data-stu-id="065f7-113">900</span></span> | <span data-ttu-id="065f7-114">250</span><span class="sxs-lookup"><span data-stu-id="065f7-114">250</span></span> |
| <span data-ttu-id="065f7-115">První někdy spustit prostředí PowerShell: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="065f7-115">First ever PowerShell run: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="065f7-116">30000</span><span class="sxs-lookup"><span data-stu-id="065f7-116">30000</span></span> | <span data-ttu-id="065f7-117">13000</span><span class="sxs-lookup"><span data-stu-id="065f7-117">13000</span></span> |
| <span data-ttu-id="065f7-118">Příkaz analysis mezipaměti vytvořené: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="065f7-118">Command analysis cache built: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="065f7-119">7000</span><span class="sxs-lookup"><span data-stu-id="065f7-119">7000</span></span> | <span data-ttu-id="065f7-120">520</span><span class="sxs-lookup"><span data-stu-id="065f7-120">520</span></span> |
| <code>1..1000000 &#124; % { }</code> | <span data-ttu-id="065f7-121">1400</span><span class="sxs-lookup"><span data-stu-id="065f7-121">1400</span></span> | <span data-ttu-id="065f7-122">750</span><span class="sxs-lookup"><span data-stu-id="065f7-122">750</span></span> |

> <span data-ttu-id="065f7-123">Všimněte si, že jeden změnu související s spuštění může mít vliv na některé nepodporované scénáře.</span><span class="sxs-lookup"><span data-stu-id="065f7-123">Note One change related to startup might impact some unsupported scenarios.</span></span>
> <span data-ttu-id="065f7-124">Prostředí PowerShell již načte soubory `$pshome\*.ps1xml` – tyto soubory byly převedeny na C# předejdete některých souborů a zatížení procesoru z zpracování jazyka XML souborů.</span><span class="sxs-lookup"><span data-stu-id="065f7-124">PowerShell no longer reads the files `$pshome\*.ps1xml` -- these files have been converted to C# to avoid some file and CPU overhead of processing the XML files.</span></span>
<span data-ttu-id="065f7-125">Soubory stále existují na podporu V2-souběžného, takže pokud změníte obsah souboru, se nebude mít žádný vliv na V5 pouze V2.</span><span class="sxs-lookup"><span data-stu-id="065f7-125">The files still exist to support V2 side-by-side, so if you change the file contents, it will not have any effect to V5, only V2.</span></span>
<span data-ttu-id="065f7-126">Všimněte si, že změna obsah těchto souborů se nikdy podporovaném scénáři.</span><span class="sxs-lookup"><span data-stu-id="065f7-126">Note that changing the contents of these files was never a supported scenario.</span></span>

<span data-ttu-id="065f7-127">Jiné viditelné změny je, jak prostředí PowerShell ukládá do mezipaměti, exportovaný příkazy a další informace pro moduly, které jsou nainstalované v systému.</span><span class="sxs-lookup"><span data-stu-id="065f7-127">Another visible change is how PowerShell caches the exported commands and other information for modules that are installed on a system.</span></span>
<span data-ttu-id="065f7-128">Dřív byla tato mezipaměť uložené v adresáři `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span><span class="sxs-lookup"><span data-stu-id="065f7-128">Previously, this cache was stored in the directory `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span></span>
<span data-ttu-id="065f7-129">V WMF 5.1 mezipaměť je jeden soubor `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span><span class="sxs-lookup"><span data-stu-id="065f7-129">In WMF 5.1, the cache is a single file `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="065f7-130">V tématu [modulu Analysis mezipaměti](scenarios-features.md#module-analysis-cache) další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="065f7-130">See [Module Analysis Cache](scenarios-features.md#module-analysis-cache) for more details.</span></span>
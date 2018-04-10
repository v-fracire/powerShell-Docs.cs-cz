---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: psgallery_scriptanalyzer_rule_profile
ms.openlocfilehash: ff575ab56f07312658d111bccd7793b64ac071ea
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="scriptanazlyer-rule-profile-for-gallery"></a><span data-ttu-id="de97a-103">Pravidlo ScriptAnazlyer profil pro galerie</span><span class="sxs-lookup"><span data-stu-id="de97a-103">ScriptAnazlyer Rule Profile for Gallery</span></span>
<span data-ttu-id="de97a-104">K zajištění kvality položek, které jsou publikovány do Galerie prostředí PowerShell, spustíme [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) pravidla, která určí, jestli jsou veškerá porušení zásad ve skriptech odeslána.</span><span class="sxs-lookup"><span data-stu-id="de97a-104">To ensure the quality of items published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="de97a-105">Můžete najít seznam pravidel, které běží na ScriptAnalyzer [GitHub stránce](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="de97a-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="de97a-106">Pokud máte jakékoli obavy týkající se pravidla, že používáme, obraťte se na správce Galerie prostředí PowerShell nebo otevřít problém pro ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="de97a-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="de97a-107">ScriptAnalyzer výsledky se zobrazí na každé stránce jednotlivé položky v galerii v příští verzi.</span><span class="sxs-lookup"><span data-stu-id="de97a-107">ScriptAnalyzer results will be displayed on each individual item page in Gallery in the coming release.</span></span> <span data-ttu-id="de97a-108">Doporučujeme vlastníci položky ke kontrole jejich položky a ujistěte se, že neexistují žádné závažné chyby v publikované položky.</span><span class="sxs-lookup"><span data-stu-id="de97a-108">We encourage item owners to check their items to make sure there are no severe errors in published items.</span></span>
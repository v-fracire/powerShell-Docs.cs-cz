---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_scriptanalyzer_rule_profile
ms.openlocfilehash: b178f198c9643fb39a6499d7e957cfd0d848c52d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="scriptanazlyer-rule-profile-for-gallery"></a><span data-ttu-id="8280d-103">Pravidlo ScriptAnazlyer profil pro galerie</span><span class="sxs-lookup"><span data-stu-id="8280d-103">ScriptAnazlyer Rule Profile for Gallery</span></span>
<span data-ttu-id="8280d-104">K zajištění kvality položek, které jsou publikovány do Galerie prostředí PowerShell, spustíme [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) pravidla, která určí, jestli jsou veškerá porušení zásad ve skriptech odeslána.</span><span class="sxs-lookup"><span data-stu-id="8280d-104">To ensure the quality of items published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="8280d-105">Můžete najít seznam pravidel, které běží na ScriptAnalyzer [GitHub stránce](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="8280d-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="8280d-106">Pokud máte jakékoli obavy týkající se pravidla, že používáme, obraťte se na správce Galerie prostředí PowerShell nebo otevřít problém pro ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="8280d-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="8280d-107">ScriptAnalyzer výsledky se zobrazí na každé stránce jednotlivé položky v galerii v příští verzi.</span><span class="sxs-lookup"><span data-stu-id="8280d-107">ScriptAnalyzer results will be displayed on each individual item page in Gallery in the coming release.</span></span> <span data-ttu-id="8280d-108">Doporučujeme vlastníci položky ke kontrole jejich položky a ujistěte se, že neexistují žádné závažné chyby v publikované položky.</span><span class="sxs-lookup"><span data-stu-id="8280d-108">We encourage item owners to check their items to make sure there are no severe errors in published items.</span></span>


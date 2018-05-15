---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Profil ScriptAnazlyer pravidlo pro galerie
ms.openlocfilehash: 74eab49e4c4a546655451ef21b30cfcafaeb9584
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="scriptanazlyer-rule-profile-for-gallery"></a><span data-ttu-id="5607b-103">Profil ScriptAnazlyer pravidlo pro galerie</span><span class="sxs-lookup"><span data-stu-id="5607b-103">ScriptAnazlyer rule profile for Gallery</span></span>

<span data-ttu-id="5607b-104">K zajištění kvality položek, které jsou publikovány do Galerie prostředí PowerShell, spustíme [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) pravidla, která určí, jestli jsou veškerá porušení zásad ve skriptech odeslána.</span><span class="sxs-lookup"><span data-stu-id="5607b-104">To ensure the quality of items published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="5607b-105">Můžete najít seznam pravidel, které běží na ScriptAnalyzer [GitHub stránce](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="5607b-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="5607b-106">Pokud máte jakékoli obavy týkající se pravidla, že používáme, obraťte se na správce Galerie prostředí PowerShell nebo otevřít problém pro ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="5607b-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="5607b-107">ScriptAnalyzer výsledky se zobrazí na každé stránce jednotlivé položky v galerii v příští verzi.</span><span class="sxs-lookup"><span data-stu-id="5607b-107">ScriptAnalyzer results will be displayed on each individual item page in Gallery in the coming release.</span></span> <span data-ttu-id="5607b-108">Doporučujeme vlastníci položky ke kontrole jejich položky a ujistěte se, že neexistují žádné závažné chyby v publikované položky.</span><span class="sxs-lookup"><span data-stu-id="5607b-108">We encourage item owners to check their items to make sure there are no severe errors in published items.</span></span>
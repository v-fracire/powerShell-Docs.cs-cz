---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Profil ScriptAnalyzer pravidlo pro galerii
ms.openlocfilehash: d91a88981cc2f3269a1f8b6ee864f8333a2f097c
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002492"
---
# <a name="scriptanalyzer-rule-profile-for-gallery"></a><span data-ttu-id="c671e-103">Profil ScriptAnalyzer pravidlo pro galerii</span><span class="sxs-lookup"><span data-stu-id="c671e-103">ScriptAnalyzer rule profile for Gallery</span></span>

<span data-ttu-id="c671e-104">Pro zajištění kvality balíčků publikována do Galerie prostředí PowerShell, zajišťuje každodenní provoz [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) pravidla, která určí, jestli je veškerá porušení zásad jak ve skriptech odeslání.</span><span class="sxs-lookup"><span data-stu-id="c671e-104">To ensure the quality of packages published to PowerShell Gallery, we run [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) rules to determine if there are any violations in the scripts submitted.</span></span>

<span data-ttu-id="c671e-105">Můžete najít seznam pravidel spouštíme na ScriptAnalyzer [stránku Githubu](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span><span class="sxs-lookup"><span data-stu-id="c671e-105">You can find the list of rules we are running on ScriptAnalyzer [GitHub page](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).</span></span>
<span data-ttu-id="c671e-106">Pokud máte jakékoli obavy týkající se pravidel, že používáme, obraťte se na správce Galerie prostředí PowerShell, nebo otevřete problém pro ScriptAnalzyer.</span><span class="sxs-lookup"><span data-stu-id="c671e-106">If you have any concerns regarding the rules we are running, please contact PowerShell Gallery Administrators, or open an issue for ScriptAnalzyer.</span></span>

<span data-ttu-id="c671e-107">ScriptAnalyzer výsledky se zobrazí na každé stránce nějakém balíčku v galerii v nadcházející verzi.</span><span class="sxs-lookup"><span data-stu-id="c671e-107">ScriptAnalyzer results will be displayed on each individual package page in Gallery in the coming release.</span></span> <span data-ttu-id="c671e-108">Doporučujeme vlastníky balíčku Zkontrolujte své balíčky, abyste měli jistotu, že zde nejsou žádné závažné chyby v publikované balíčky.</span><span class="sxs-lookup"><span data-stu-id="c671e-108">We encourage package owners to check their packages to make sure there are no severe errors in published packages.</span></span>

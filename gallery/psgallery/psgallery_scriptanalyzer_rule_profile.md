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
# <a name="scriptanazlyer-rule-profile-for-gallery"></a>Pravidlo ScriptAnazlyer profil pro galerie
K zajištění kvality položek, které jsou publikovány do Galerie prostředí PowerShell, spustíme [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) pravidla, která určí, jestli jsou veškerá porušení zásad ve skriptech odeslána.

Můžete najít seznam pravidel, které běží na ScriptAnalyzer [GitHub stránce](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).
Pokud máte jakékoli obavy týkající se pravidla, že používáme, obraťte se na správce Galerie prostředí PowerShell nebo otevřít problém pro ScriptAnalzyer.

ScriptAnalyzer výsledky se zobrazí na každé stránce jednotlivé položky v galerii v příští verzi. Doporučujeme vlastníci položky ke kontrole jejich položky a ujistěte se, že neexistují žádné závažné chyby v publikované položky.
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
# <a name="scriptanalyzer-rule-profile-for-gallery"></a>Profil ScriptAnalyzer pravidlo pro galerii

Pro zajištění kvality balíčků publikována do Galerie prostředí PowerShell, zajišťuje každodenní provoz [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) pravidla, která určí, jestli je veškerá porušení zásad jak ve skriptech odeslání.

Můžete najít seznam pravidel spouštíme na ScriptAnalyzer [stránku Githubu](https://github.com/PowerShell/PSScriptAnalyzer/blob/development/Engine/Settings/PSGallery.psd1).
Pokud máte jakékoli obavy týkající se pravidel, že používáme, obraťte se na správce Galerie prostředí PowerShell, nebo otevřete problém pro ScriptAnalzyer.

ScriptAnalyzer výsledky se zobrazí na každé stránce nějakém balíčku v galerii v nadcházející verzi. Doporučujeme vlastníky balíčku Zkontrolujte své balíčky, abyste měli jistotu, že zde nejsou žádné závažné chyby v publikované balíčky.

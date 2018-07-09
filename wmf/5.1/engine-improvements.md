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
# <a name="powershell-engine-improvements"></a>Vylepšení Powershellového jádra

Následující vylepšení modul PowerShell core je implementovaná v WMF 5.1:

## <a name="performance"></a>Výkon

V některých důležitých oblastech se zvýšil výkon:

- Spuštění
- Zřetězení příkazů do rutin jako `ForEach-Object` a `Where-Object` je přibližně 50 % rychlejší

Některé příklad vylepšení (výsledky mohou lišit v závislosti na hardwaru):

| Scénář | 5.0 doba (ms) | 5.1 doba (ms) |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | 900 | 250 |
| První někdy spustit prostředí PowerShell: `powershell -command "Unknown-Command"` | 30000 | 13000 |
| Vytvořená mezipaměť analýzy příkazu: `powershell -command "Unknown-Command"` | 7000 | 520 |
| <code>1..1000000 &#124; % { }</code> | 1400 | 750 |

> [!Note]
> Jednu změnu související se spouštěcí může mít vliv na některé nepodporované scénáře.
> Prostředí PowerShell již načte soubory `$pshome\*.ps1xml` – tyto soubory byly převedeny do jazyka C#, aby některý soubor a režie procesoru zpracování souboru XML soubory.
> Soubory stále existují podpoře V2 side-by-side, takže pokud změníte obsah souboru, to nebude mít žádný vliv na V5, pouze V2.
> Všimněte si, že změna obsah těchto souborů se nikdy podporovaný scénář.

Další viditelné změnou je, jak Powershellu uloží exportované příkazy a další informace pro moduly, které jsou nainstalované v systému.
Dříve byla tato mezipaměť uložen v adresáři `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.
Ve WMF 5.1 mezipaměť je jeden soubor `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
Zobrazit [modul analýzy mezipaměti](scenarios-features.md#module-analysis-cache) další podrobnosti.
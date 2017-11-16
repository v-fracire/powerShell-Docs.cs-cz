---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
title: "Modul prostředí PowerShell vylepšení v WMF 5.1"
ms.openlocfilehash: 6c8000ccfc59ab46de95dc4f67161e12a5a41199
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
#<a name="powershell-engine-improvements"></a>Vylepšení modul prostředí PowerShell

Následující vylepšení k modulu jádra prostředí PowerShell je implementovaná v WMF 5.1:


## <a name="performance"></a>Výkon ##

Výkon je vyšší, v některé důležité oblasti:

- Spuštění
- Zřetězení příkazů do rutin jako ForEach-Object a Where-Object je přibližně 50 % rychlejší 

Některé příklad vylepšení (výsledky se liší v závislosti na hardwaru): 

| Scénář | 5.0 čas (ms) | 5.1 čas (ms) |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | 900 | 250 |
| První někdy spustit prostředí PowerShell:`powershell -command "Unknown-Command"` | 30000 | 13000 |
| Příkaz analysis mezipaměti vytvořené:`powershell -command "Unknown-Command"` | 7000 | 520 |
| <code>1..1000000 &#124; % { }</code> | 1400 | 750 |
  
> Všimněte si, že jeden změnu související s spuštění může mít vliv na některé nepodporované scénáře. 
> Prostředí PowerShell již načte soubory `$pshome\*.ps1xml` – tyto soubory byly převedeny na C# předejdete některých souborů a zatížení procesoru z zpracování jazyka XML souborů. 
Soubory stále existují na podporu V2-souběžného, takže pokud změníte obsah souboru, se nebude mít žádný vliv na V5 pouze V2. 
Všimněte si, že změna obsah těchto souborů se nikdy podporovaném scénáři.

Jiné viditelné změny je, jak prostředí PowerShell ukládá do mezipaměti, exportovaný příkazy a další informace pro moduly, které jsou nainstalované v systému. Dřív byla tato mezipaměť uložené v adresáři `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`. V WMF 5.1 mezipaměť je jeden soubor `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
V tématu [modulu Analysis mezipaměti](scenarios-features.md#module-analysis-cache) další podrobnosti.


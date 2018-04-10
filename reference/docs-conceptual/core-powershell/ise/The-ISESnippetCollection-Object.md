---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISESnippetCollection
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: bd5ed4a1f15e0a398b7c6a17f0071cad889be4a7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-isesnippetcollection-object"></a>Objekt ISESnippetCollection

**ISESnippetCollection** objektu je kolekce **ISESnippet** objekty. Kolekce souborů, který je přidružený **PowerShellTab** objektu je členem této třídy. Příkladem je **$psISE.CurrentPowerShellTab.Files** kolekce.

## <a name="methods"></a>Metody

### <a name="load-filepathname-"></a>Load\( FilePathName \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

Načítání. snippets.ps1xml soubor, který obsahuje vlastní fragmenty kódu. Nejjednodušší způsob, jak vytvářet fragmenty je pomocí rutiny New-IseSnippet, které automaticky uloží je do složky profilu, aby se načíst při každém spuštění Windows PowerShell ISE.

**FilePathName** – řetězec cestu a název souboru. snippets.ps1xml soubor, který obsahuje definice fragment kódu.

```powershell
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) 'Snippets\MySnips.snippets.ps1xml' $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)
```

## <a name="see-also"></a>Viz také

- [ISESnippetObject](The-ISESnippetObject.md)
- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)
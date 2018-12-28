---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISESnippetCollection
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: bd5ed4a1f15e0a398b7c6a17f0071cad889be4a7
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404096"
---
# <a name="the-isesnippetcollection-object"></a>Objekt ISESnippetCollection

**ISESnippetCollection** objektu je kolekce **ISESnippet** objekty. Kolekce souborů, který je přidružen **PowerShellTab** objektu je členem této třídy. Příkladem je **$psISE.CurrentPowerShellTab.Files** kolekce.

## <a name="methods"></a>Metody

### <a name="load-filepathname-"></a>Zatížení\( FilePathName \)

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Načítání. snippets.ps1xml soubor, který obsahuje uživatelské fragmenty kódu. Nejjednodušší způsob, jak vytvořit fragmenty kódu se pomocí rutiny New-IseSnippet, které automaticky uloží je do složky profilu tak, že jsou načteny při každém spuštění Windows PowerShell ISE.

**FilePathName** – řetězec cesty a názvu do souboru. snippets.ps1xml soubor, který obsahuje definice fragment kódu.

```powershell
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) 'Snippets\MySnips.snippets.ps1xml' $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)
```

## <a name="see-also"></a>Viz také

- [Objekt ISESnippetObject](The-ISESnippetObject.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)
---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISESnippetCollection
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: b19c5b5c88f7c8bd0d0c466c7861fa9288bdc7a2
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="the-isesnippetcollection-object"></a>Objekt ISESnippetCollection
  **ISESnippetCollection** objektu je kolekce **ISESnippet** objekty. Kolekce souborů, který je přidružený **PowerShellTab** objektu je členem této třídy. Příkladem je **$psISE.CurrentPowerShellTab.Files** kolekce.

## <a name="methods"></a>Metody

### <a name="load-filepathname-"></a>Zatížení\( FilePathName\)
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Načítání. snippets.ps1xml soubor, který obsahuje vlastní fragmenty kódu. Nejjednodušší způsob, jak vytvářet fragmenty je pomocí rutiny New-IseSnippet, které automaticky uloží je do složky profilu, aby se načíst při každém spuštění Windows PowerShell ISE.

 **FilePathName** – řetězec cestu a název souboru. snippets.ps1xml soubor, který obsahuje definice fragment kódu.

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## <a name="see-also"></a>Viz také
- [ISESnippetObject](The-ISESnippetObject.md) 
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)

  

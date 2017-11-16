---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: 6112f5252d2d1e868092da4a6cd04feb1875b597
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2017
---
# <a name="the-isesnippetobject"></a>ISESnippetObject
  **ISESnippet** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISESnippet. Členové **$psISE.CurrentPowerShellTab.Snippets** kolekce jsou všechny příklady **ISESnippet** objekty. Nejjednodušší způsob, jak vytvořit fragment je použití [New-IseSnippet &#91; PSITPro5_ISE &#93; ](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) rutiny.

## <a name="properties"></a>Properties

### <a name="author"></a>Autor
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Vlastnost jen pro čtení, získá jméno autora fragmentu.

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

### <a name="codefragment"></a>CodeFragment
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Vlastnost jen pro čtení, získá fragment kódu, který má být vložen do editoru.

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

### <a name="shortcut"></a>Zástupce
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích. 

 Vlastnost jen pro čtení, který získá Windows klávesové zkratky pro položku nabídky.

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a>Viz také
- [Objekt ISESnippetCollection](The-ISESnippetCollection-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)

  

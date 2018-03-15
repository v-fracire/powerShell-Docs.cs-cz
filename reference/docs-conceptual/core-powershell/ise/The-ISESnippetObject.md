---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: f1b023291826d5568eb8bdf5a898a00228825276
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="the-isesnippetobject"></a>Objekt ISESnippetObject
  **ISESnippet** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISESnippet. Členové **$psISE.CurrentPowerShellTab.Snippets** kolekce jsou všechny příklady **ISESnippet** objekty. Nejjednodušší způsob, jak vytvořit fragment je použití [New-IseSnippet&#91;PSITPro5_ISE&#93; ](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) rutiny.

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
- [Účelem ISE Windows PowerShell skriptování objektový Model](purpose-of-the-windows-powershell-ise-scripting-object-model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)

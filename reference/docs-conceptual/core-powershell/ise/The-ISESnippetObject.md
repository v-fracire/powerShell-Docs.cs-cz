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
# <a name="the-isesnippetobject"></a><span data-ttu-id="4bb4e-103">ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="4bb4e-103">The ISESnippetObject</span></span>
  <span data-ttu-id="4bb4e-104">**ISESnippet** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISESnippet.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-104">An **ISESnippet** object is an instance of the Microsoft.PowerShell.Host.ISE.ISESnippet class.</span></span> <span data-ttu-id="4bb4e-105">Členové **$psISE.CurrentPowerShellTab.Snippets** kolekce jsou všechny příklady **ISESnippet** objekty.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-105">The members of the **$psISE.CurrentPowerShellTab.Snippets** collection are all examples of **ISESnippet** objects.</span></span> <span data-ttu-id="4bb4e-106">Nejjednodušší způsob, jak vytvořit fragment je použití [New-IseSnippet &#91; PSITPro5_ISE &#93; ](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) rutiny.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-106">The easiest way to create a snippet is to use the [New-IseSnippet&#91;PSITPro5_ISE&#93;](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) cmdlet.</span></span>

## <a name="properties"></a><span data-ttu-id="4bb4e-107">Properties</span><span class="sxs-lookup"><span data-stu-id="4bb4e-107">Properties</span></span>

### <a name="author"></a><span data-ttu-id="4bb4e-108">Autor</span><span class="sxs-lookup"><span data-stu-id="4bb4e-108">Author</span></span>
  <span data-ttu-id="4bb4e-109">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="4bb4e-110">Vlastnost jen pro čtení, získá jméno autora fragmentu.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-110">The read-only property that gets the name of the author of the snippet.</span></span>

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

### <a name="codefragment"></a><span data-ttu-id="4bb4e-111">CodeFragment</span><span class="sxs-lookup"><span data-stu-id="4bb4e-111">CodeFragment</span></span>
  <span data-ttu-id="4bb4e-112">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-112">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="4bb4e-113">Vlastnost jen pro čtení, získá fragment kódu, který má být vložen do editoru.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-113">The read-only property that gets the code fragment to be inserted into the editor.</span></span>

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

### <a name="shortcut"></a><span data-ttu-id="4bb4e-114">Zástupce</span><span class="sxs-lookup"><span data-stu-id="4bb4e-114">Shortcut</span></span>
  <span data-ttu-id="4bb4e-115">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-115">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="4bb4e-116">Vlastnost jen pro čtení, který získá Windows klávesové zkratky pro položku nabídky.</span><span class="sxs-lookup"><span data-stu-id="4bb4e-116">The read-only property that gets the Windows keyboard shortcut for the menu item.</span></span>

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a><span data-ttu-id="4bb4e-117">Viz také</span><span class="sxs-lookup"><span data-stu-id="4bb4e-117">See Also</span></span>
- [<span data-ttu-id="4bb4e-118">Objekt ISESnippetCollection</span><span class="sxs-lookup"><span data-stu-id="4bb4e-118">The ISESnippetCollection Object</span></span>](The-ISESnippetCollection-Object.md) 
- [<span data-ttu-id="4bb4e-119">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="4bb4e-119">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="4bb4e-120">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="4bb4e-120">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="4bb4e-121">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="4bb4e-121">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  

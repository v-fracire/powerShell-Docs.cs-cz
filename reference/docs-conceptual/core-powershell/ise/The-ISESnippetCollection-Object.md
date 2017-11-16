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
# <a name="the-isesnippetcollection-object"></a><span data-ttu-id="3a43a-103">Objekt ISESnippetCollection</span><span class="sxs-lookup"><span data-stu-id="3a43a-103">The ISESnippetCollection Object</span></span>
  <span data-ttu-id="3a43a-104">**ISESnippetCollection** objektu je kolekce **ISESnippet** objekty.</span><span class="sxs-lookup"><span data-stu-id="3a43a-104">The **ISESnippetCollection** object is a collection of **ISESnippet** objects.</span></span> <span data-ttu-id="3a43a-105">Kolekce souborů, který je přidružený **PowerShellTab** objektu je členem této třídy.</span><span class="sxs-lookup"><span data-stu-id="3a43a-105">The files collection that is associated with a **PowerShellTab** object is a member of this class.</span></span> <span data-ttu-id="3a43a-106">Příkladem je **$psISE.CurrentPowerShellTab.Files** kolekce.</span><span class="sxs-lookup"><span data-stu-id="3a43a-106">An example is the **$psISE.CurrentPowerShellTab.Files** collection.</span></span>

## <a name="methods"></a><span data-ttu-id="3a43a-107">Metody</span><span class="sxs-lookup"><span data-stu-id="3a43a-107">Methods</span></span>

### <a name="load-filepathname-"></a><span data-ttu-id="3a43a-108">Zatížení\( FilePathName\)</span><span class="sxs-lookup"><span data-stu-id="3a43a-108">Load\( FilePathName \)</span></span>
  <span data-ttu-id="3a43a-109">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="3a43a-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="3a43a-110">Načítání. snippets.ps1xml soubor, který obsahuje vlastní fragmenty kódu.</span><span class="sxs-lookup"><span data-stu-id="3a43a-110">Loads a .snippets.ps1xml file that contains user-defined snippets.</span></span> <span data-ttu-id="3a43a-111">Nejjednodušší způsob, jak vytvářet fragmenty je pomocí rutiny New-IseSnippet, které automaticky uloží je do složky profilu, aby se načíst při každém spuštění Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="3a43a-111">The easiest way to create snippets is to use the New-IseSnippet cmdlet, which automatically stores them in your profile folder so that they are loaded every time that you start Windows PowerShell ISE.</span></span>

 <span data-ttu-id="3a43a-112">**FilePathName** – řetězec cestu a název souboru. snippets.ps1xml soubor, který obsahuje definice fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="3a43a-112">**FilePathName** - String The path and file name to a .snippets.ps1xml file that contains snippet definitions.</span></span>

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## <a name="see-also"></a><span data-ttu-id="3a43a-113">Viz také</span><span class="sxs-lookup"><span data-stu-id="3a43a-113">See Also</span></span>
- [<span data-ttu-id="3a43a-114">ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="3a43a-114">The ISESnippetObject</span></span>](The-ISESnippetObject.md) 
- [<span data-ttu-id="3a43a-115">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="3a43a-115">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="3a43a-116">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="3a43a-116">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="3a43a-117">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="3a43a-117">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  

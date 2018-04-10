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
# <a name="the-isesnippetcollection-object"></a><span data-ttu-id="c72a6-103">Objekt ISESnippetCollection</span><span class="sxs-lookup"><span data-stu-id="c72a6-103">The ISESnippetCollection Object</span></span>

<span data-ttu-id="c72a6-104">**ISESnippetCollection** objektu je kolekce **ISESnippet** objekty.</span><span class="sxs-lookup"><span data-stu-id="c72a6-104">The **ISESnippetCollection** object is a collection of **ISESnippet** objects.</span></span> <span data-ttu-id="c72a6-105">Kolekce souborů, který je přidružený **PowerShellTab** objektu je členem této třídy.</span><span class="sxs-lookup"><span data-stu-id="c72a6-105">The files collection that is associated with a **PowerShellTab** object is a member of this class.</span></span> <span data-ttu-id="c72a6-106">Příkladem je **$psISE.CurrentPowerShellTab.Files** kolekce.</span><span class="sxs-lookup"><span data-stu-id="c72a6-106">An example is the **$psISE.CurrentPowerShellTab.Files** collection.</span></span>

## <a name="methods"></a><span data-ttu-id="c72a6-107">Metody</span><span class="sxs-lookup"><span data-stu-id="c72a6-107">Methods</span></span>

### <a name="load-filepathname-"></a><span data-ttu-id="c72a6-108">Load\( FilePathName \)</span><span class="sxs-lookup"><span data-stu-id="c72a6-108">Load\( FilePathName \)</span></span>

<span data-ttu-id="c72a6-109">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="c72a6-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="c72a6-110">Načítání. snippets.ps1xml soubor, který obsahuje vlastní fragmenty kódu.</span><span class="sxs-lookup"><span data-stu-id="c72a6-110">Loads a .snippets.ps1xml file that contains user-defined snippets.</span></span> <span data-ttu-id="c72a6-111">Nejjednodušší způsob, jak vytvářet fragmenty je pomocí rutiny New-IseSnippet, které automaticky uloží je do složky profilu, aby se načíst při každém spuštění Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="c72a6-111">The easiest way to create snippets is to use the New-IseSnippet cmdlet, which automatically stores them in your profile folder so that they are loaded every time that you start Windows PowerShell ISE.</span></span>

<span data-ttu-id="c72a6-112">**FilePathName** – řetězec cestu a název souboru. snippets.ps1xml soubor, který obsahuje definice fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="c72a6-112">**FilePathName** - String The path and file name to a .snippets.ps1xml file that contains snippet definitions.</span></span>

```powershell
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) 'Snippets\MySnips.snippets.ps1xml' $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)
```

## <a name="see-also"></a><span data-ttu-id="c72a6-113">Viz také</span><span class="sxs-lookup"><span data-stu-id="c72a6-113">See Also</span></span>

- [<span data-ttu-id="c72a6-114">ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="c72a6-114">The ISESnippetObject</span></span>](The-ISESnippetObject.md)
- [<span data-ttu-id="c72a6-115">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="c72a6-115">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="c72a6-116">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="c72a6-116">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEFileCollection
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: eb4b2784820cbe51f662fd2fd945d8760ef9dbff
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404107"
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="438c8-103">Objekt ISEFileCollection</span><span class="sxs-lookup"><span data-stu-id="438c8-103">The ISEFileCollection Object</span></span>

<span data-ttu-id="438c8-104">**ISEFileCollection** objektu je kolekce **ISEFile** objekty.</span><span class="sxs-lookup"><span data-stu-id="438c8-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="438c8-105">Příkladem je $psISE.CurrentPowerShellTab.Files kolekce.</span><span class="sxs-lookup"><span data-stu-id="438c8-105">An example is the $psISE.CurrentPowerShellTab.Files collection.</span></span>

## <a name="methods"></a><span data-ttu-id="438c8-106">Metody</span><span class="sxs-lookup"><span data-stu-id="438c8-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="438c8-107">Přidat\( \[fullPath\] \)</span><span class="sxs-lookup"><span data-stu-id="438c8-107">Add\( \[fullPath\] \)</span></span>

<span data-ttu-id="438c8-108">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="438c8-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="438c8-109">Vytvoří a vrátí nový soubor bez názvu a přidá jej do kolekce.</span><span class="sxs-lookup"><span data-stu-id="438c8-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="438c8-110">**IsUntitled** vlastnost souboru nově vytvořeného **$true**.</span><span class="sxs-lookup"><span data-stu-id="438c8-110">The **IsUntitled** property of the newly created file is **$true**.</span></span>

<span data-ttu-id="438c8-111">**\[fullPath\]**  – volitelný řetězec plně zadaná cesta k souboru.</span><span class="sxs-lookup"><span data-stu-id="438c8-111">**\[fullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="438c8-112">Je vygenerována výjimka, pokud zahrnete **fullPath** parametr a relativní cesty, nebo pokud používáte název souboru místo úplné cesty.</span><span class="sxs-lookup"><span data-stu-id="438c8-112">An exception is generated if you include the **fullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a><span data-ttu-id="438c8-113">Odebrat\( souboru \[platnost\] \)</span><span class="sxs-lookup"><span data-stu-id="438c8-113">Remove\( File, \[Force\] \)</span></span>

<span data-ttu-id="438c8-114">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="438c8-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="438c8-115">Odebere zadaný soubor z aktuálního PowerShell tab.</span><span class="sxs-lookup"><span data-stu-id="438c8-115">Removes a specified file from the current PowerShell tab.</span></span>

<span data-ttu-id="438c8-116">**Soubor** – The ISEFile řetězec souboru, který chcete odebrat z kolekce.</span><span class="sxs-lookup"><span data-stu-id="438c8-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="438c8-117">Pokud soubor nebyl uložen, tato metoda vyvolá výjimku.</span><span class="sxs-lookup"><span data-stu-id="438c8-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="438c8-118">Použití **vynutit** přepnout parametr pro vynucení odebrání neuloženého souboru.</span><span class="sxs-lookup"><span data-stu-id="438c8-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

<span data-ttu-id="438c8-119">**\[Platnost\]**  – volitelný logický-li nastavena na **$true**, udělí oprávnění, odeberte soubor i v případě, že nebyla uložena po poslední použití.</span><span class="sxs-lookup"><span data-stu-id="438c8-119">**\[Force\]** - optional Boolean If set to **$true**, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="438c8-120">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="438c8-120">The default is **$false**.</span></span>

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="438c8-121">SetSelectedFile\( selectedFile \)</span><span class="sxs-lookup"><span data-stu-id="438c8-121">SetSelectedFile\( selectedFile \)</span></span>

<span data-ttu-id="438c8-122">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="438c8-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="438c8-123">Vybere soubor, který je určen **selectedFile** parametru.</span><span class="sxs-lookup"><span data-stu-id="438c8-123">Selects the file that is specified by the **selectedFile** parameter.</span></span>

<span data-ttu-id="438c8-124">**selectedFile** – Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile soubor, který chcete vybrat.</span><span class="sxs-lookup"><span data-stu-id="438c8-124">**selectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a><span data-ttu-id="438c8-125">Viz také</span><span class="sxs-lookup"><span data-stu-id="438c8-125">See Also</span></span>

- [<span data-ttu-id="438c8-126">Objekt ISEFile</span><span class="sxs-lookup"><span data-stu-id="438c8-126">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="438c8-127">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="438c8-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="438c8-128">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="438c8-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
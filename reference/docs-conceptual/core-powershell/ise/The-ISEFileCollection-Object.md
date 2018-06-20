---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEFileCollection
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: eb4b2784820cbe51f662fd2fd945d8760ef9dbff
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953085"
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="82f3c-103">Objekt ISEFileCollection</span><span class="sxs-lookup"><span data-stu-id="82f3c-103">The ISEFileCollection Object</span></span>

<span data-ttu-id="82f3c-104">**ISEFileCollection** objektu je kolekce **ISEFile** objekty.</span><span class="sxs-lookup"><span data-stu-id="82f3c-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="82f3c-105">Příkladem je $psISE.CurrentPowerShellTab.Files kolekce.</span><span class="sxs-lookup"><span data-stu-id="82f3c-105">An example is the $psISE.CurrentPowerShellTab.Files collection.</span></span>

## <a name="methods"></a><span data-ttu-id="82f3c-106">Metody</span><span class="sxs-lookup"><span data-stu-id="82f3c-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="82f3c-107">Přidat\( \[fullPath\] \)</span><span class="sxs-lookup"><span data-stu-id="82f3c-107">Add\( \[fullPath\] \)</span></span>

<span data-ttu-id="82f3c-108">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="82f3c-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="82f3c-109">Vytvoří a vrátí nové bez názvu souboru a přidá do kolekce.</span><span class="sxs-lookup"><span data-stu-id="82f3c-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="82f3c-110">**IsUntitled** vlastnost nově vytvořený soubor je **$true**.</span><span class="sxs-lookup"><span data-stu-id="82f3c-110">The **IsUntitled** property of the newly created file is **$true**.</span></span>

<span data-ttu-id="82f3c-111">**\[fullPath\]**  – volitelný řetězec plně zadaná cesta k souboru.</span><span class="sxs-lookup"><span data-stu-id="82f3c-111">**\[fullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="82f3c-112">Pokud zahrnete, bude vygenerována výjimka **fullPath** parametr a relativní cesta, nebo pokud použijete název souboru místo úplné cesty.</span><span class="sxs-lookup"><span data-stu-id="82f3c-112">An exception is generated if you include the **fullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a><span data-ttu-id="82f3c-113">Odebrat\( souboru \[platnost\] \)</span><span class="sxs-lookup"><span data-stu-id="82f3c-113">Remove\( File, \[Force\] \)</span></span>

<span data-ttu-id="82f3c-114">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="82f3c-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="82f3c-115">Odebere zadaný soubor z aktuální karta prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82f3c-115">Removes a specified file from the current PowerShell tab.</span></span>

<span data-ttu-id="82f3c-116">**Soubor** -ISEFile řetězec souboru, který chcete odebrat z kolekce.</span><span class="sxs-lookup"><span data-stu-id="82f3c-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="82f3c-117">Pokud soubor nebyl uložen, tato metoda vyvolá výjimku.</span><span class="sxs-lookup"><span data-stu-id="82f3c-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="82f3c-118">Použití **vynutit** přepínač parametru Vynutit odstranění neuložené souboru.</span><span class="sxs-lookup"><span data-stu-id="82f3c-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

<span data-ttu-id="82f3c-119">**\[Platnost\]**  -volitelné Boolean Pokud nastavit **$true**, uděluje oprávnění k odebrání souboru i v případě, že ještě nebyl uložen po posledního použití.</span><span class="sxs-lookup"><span data-stu-id="82f3c-119">**\[Force\]** - optional Boolean If set to **$true**, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="82f3c-120">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="82f3c-120">The default is **$false**.</span></span>

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="82f3c-121">SetSelectedFile\( selectedFile \)</span><span class="sxs-lookup"><span data-stu-id="82f3c-121">SetSelectedFile\( selectedFile \)</span></span>

<span data-ttu-id="82f3c-122">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="82f3c-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="82f3c-123">Vybere soubor, který je zadán **selectedFile** parametr.</span><span class="sxs-lookup"><span data-stu-id="82f3c-123">Selects the file that is specified by the **selectedFile** parameter.</span></span>

<span data-ttu-id="82f3c-124">**selectedFile** -ISEFile Microsoft.PowerShell.Host.ISE.ISEFile souboru, který chcete vybrat.</span><span class="sxs-lookup"><span data-stu-id="82f3c-124">**selectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a><span data-ttu-id="82f3c-125">Viz také</span><span class="sxs-lookup"><span data-stu-id="82f3c-125">See Also</span></span>

- [<span data-ttu-id="82f3c-126">Objekt ISEFile</span><span class="sxs-lookup"><span data-stu-id="82f3c-126">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="82f3c-127">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="82f3c-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="82f3c-128">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="82f3c-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
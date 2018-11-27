---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEFile
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 24549720b8bc35435882533b0eb138de432ede65
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320869"
---
# <a name="the-isefile-object"></a><span data-ttu-id="56f78-103">Objekt ISEFile</span><span class="sxs-lookup"><span data-stu-id="56f78-103">The ISEFile Object</span></span>

<span data-ttu-id="56f78-104">**ISEFile** objekt představuje soubor ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="56f78-104">An **ISEFile** object represents a file in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="56f78-105">Je instancí třídy Microsoft.PowerShell.Host.ISE.ISEFile.</span><span class="sxs-lookup"><span data-stu-id="56f78-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span> <span data-ttu-id="56f78-106">Toto téma obsahuje seznam členů metody a vlastnosti člena.</span><span class="sxs-lookup"><span data-stu-id="56f78-106">This topic lists its member methods and member properties.</span></span> <span data-ttu-id="56f78-107">**$PsISE.CurrentFile** a všechny instance třídy Microsoft.PowerShell.Host.ISE.ISEFile jsou soubory v kolekci souborů v Powershellové karty.</span><span class="sxs-lookup"><span data-stu-id="56f78-107">The **$psISE.CurrentFile** and the files in the Files collection in a PowerShell tab are all instances of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span>

## <a name="methods"></a><span data-ttu-id="56f78-108">Metody</span><span class="sxs-lookup"><span data-stu-id="56f78-108">Methods</span></span>

### <a name="save-saveencoding-"></a><span data-ttu-id="56f78-109">Uložit\( \[saveEncoding\] \)</span><span class="sxs-lookup"><span data-stu-id="56f78-109">Save\( \[saveEncoding\] \)</span></span>

<span data-ttu-id="56f78-110">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-111">Uloží soubor na disk.</span><span class="sxs-lookup"><span data-stu-id="56f78-111">Saves the file to disk.</span></span>

<span data-ttu-id="56f78-112">**\[saveEncoding\]**  – volitelné [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) znak kódování parametru má být použit pro uloženého souboru.</span><span class="sxs-lookup"><span data-stu-id="56f78-112">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="56f78-113">Výchozí hodnota je **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="56f78-113">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="56f78-114">Výjimky</span><span class="sxs-lookup"><span data-stu-id="56f78-114">Exceptions</span></span>

- <span data-ttu-id="56f78-115">**System.IO.IOException**: soubor nelze uložit.</span><span class="sxs-lookup"><span data-stu-id="56f78-115">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a><span data-ttu-id="56f78-116">Uložit jako\(název souboru, \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="56f78-116">SaveAs\(filename, \[saveEncoding\]\)</span></span>

<span data-ttu-id="56f78-117">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-118">Uloží soubor s názvem zadaného souboru a kódování.</span><span class="sxs-lookup"><span data-stu-id="56f78-118">Saves the file with the specified file name and encoding.</span></span>

<span data-ttu-id="56f78-119">**Název souboru** -String název se použije k uložení souboru.</span><span class="sxs-lookup"><span data-stu-id="56f78-119">**filename** - String The name to be used to save the file.</span></span>

<span data-ttu-id="56f78-120">**\[saveEncoding\]**  – volitelné [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) znak kódování parametru má být použit pro uloženého souboru.</span><span class="sxs-lookup"><span data-stu-id="56f78-120">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="56f78-121">Výchozí hodnota je **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="56f78-121">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="56f78-122">Výjimky</span><span class="sxs-lookup"><span data-stu-id="56f78-122">Exceptions</span></span>

- <span data-ttu-id="56f78-123">**System.ArgumentNullException**: **filename** parametr má hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="56f78-123">**System.ArgumentNullException**: The **filename** parameter is null.</span></span>
- <span data-ttu-id="56f78-124">**System.ArgumentException**: **filename** parametru je prázdný.</span><span class="sxs-lookup"><span data-stu-id="56f78-124">**System.ArgumentException**: The **filename** parameter is empty.</span></span>
- <span data-ttu-id="56f78-125">**System.IO.IOException**: soubor nelze uložit.</span><span class="sxs-lookup"><span data-stu-id="56f78-125">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a><span data-ttu-id="56f78-126">Properties</span><span class="sxs-lookup"><span data-stu-id="56f78-126">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="56f78-127">DisplayName</span><span class="sxs-lookup"><span data-stu-id="56f78-127">DisplayName</span></span>

<span data-ttu-id="56f78-128">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-128">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-129">Vlastnost jen pro čtení, která vrací řetězec, který obsahuje zobrazovaný název tohoto souboru.</span><span class="sxs-lookup"><span data-stu-id="56f78-129">The read-only property that gets the string that contains the display name of this file.</span></span> <span data-ttu-id="56f78-130">Název se zobrazí na **souboru** kartě v horní části editoru.</span><span class="sxs-lookup"><span data-stu-id="56f78-130">The name is shown on the **File** tab at the top of the editor.</span></span> <span data-ttu-id="56f78-131">Přítomnost hvězdičku \( \* \) na konci názvu označuje, že soubor obsahuje změny, které nebyly uloženy.</span><span class="sxs-lookup"><span data-stu-id="56f78-131">The presence of an asterisk \(\*\) at the end of the name indicates that the file has changes that have not been saved.</span></span>

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a><span data-ttu-id="56f78-132">Editor</span><span class="sxs-lookup"><span data-stu-id="56f78-132">Editor</span></span>

<span data-ttu-id="56f78-133">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-133">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-134">Vlastnost jen pro čtení, který získá [editoru objektu](The-ISEEditor-Object.md) , která je použita pro zadaný soubor.</span><span class="sxs-lookup"><span data-stu-id="56f78-134">The read-only property that gets the [editor object](The-ISEEditor-Object.md) that is used for the specified file.</span></span>

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a><span data-ttu-id="56f78-135">Kódování</span><span class="sxs-lookup"><span data-stu-id="56f78-135">Encoding</span></span>

<span data-ttu-id="56f78-136">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-137">Vlastnost jen pro čtení, která získá původní kódování souboru.</span><span class="sxs-lookup"><span data-stu-id="56f78-137">The read-only property that gets the original file encoding.</span></span> <span data-ttu-id="56f78-138">Jedná se **System.Text.Encoding** objektu.</span><span class="sxs-lookup"><span data-stu-id="56f78-138">This is a **System.Text.Encoding** object.</span></span>

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a><span data-ttu-id="56f78-139">FullPath</span><span class="sxs-lookup"><span data-stu-id="56f78-139">FullPath</span></span>

<span data-ttu-id="56f78-140">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-141">Vlastnost jen pro čtení, která vrací řetězec, který určuje úplnou cestu otevřený soubor.</span><span class="sxs-lookup"><span data-stu-id="56f78-141">The read-only property that gets the string that specifies the full path of the opened file.</span></span>

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a><span data-ttu-id="56f78-142">IsSaved</span><span class="sxs-lookup"><span data-stu-id="56f78-142">IsSaved</span></span>

<span data-ttu-id="56f78-143">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-144">Jen pro čtení logická vlastnost, která vrací **$true** Pokud byl uložen soubor po jeho poslední úpravy.</span><span class="sxs-lookup"><span data-stu-id="56f78-144">The read-only Boolean property that returns **$true** if the file has been saved after it was last modified.</span></span>

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a><span data-ttu-id="56f78-145">IsUntitled</span><span class="sxs-lookup"><span data-stu-id="56f78-145">IsUntitled</span></span>

<span data-ttu-id="56f78-146">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="56f78-146">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="56f78-147">Vlastnost jen pro čtení, který vrací **$true** Pokud soubor nikdy nebyla zadána názvu.</span><span class="sxs-lookup"><span data-stu-id="56f78-147">The read-only property that returns **$true** if the file has never been given a title.</span></span>

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a><span data-ttu-id="56f78-148">Viz také</span><span class="sxs-lookup"><span data-stu-id="56f78-148">See Also</span></span>

- [<span data-ttu-id="56f78-149">ISEFileCollectionObject</span><span class="sxs-lookup"><span data-stu-id="56f78-149">The ISEFileCollectionObject</span></span>](The-ISEFileCollection-Object.md)
- [<span data-ttu-id="56f78-150">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="56f78-150">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="56f78-151">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="56f78-151">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
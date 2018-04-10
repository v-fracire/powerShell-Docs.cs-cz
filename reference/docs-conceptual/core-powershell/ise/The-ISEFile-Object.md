---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEFile
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 276e8f04a827e18999b5b3ecb08f47de4f4b23b1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-isefile-object"></a>Objekt ISEFile

**ISEFile** je soubor v systému Windows PowerShell® Integrované skriptovací prostředí (ISE). Je instance třídy Microsoft.PowerShell.Host.ISE.ISEFile. Toto téma uvádí jeho člen metod a vlastností člena. **$PsISE.CurrentFile** a všechny instance třídy Microsoft.PowerShell.Host.ISE.ISEFile jsou soubory v kolekci soubory na kartě prostředí PowerShell.

## <a name="methods"></a>Metody

### <a name="save-saveencoding-"></a>Uložit\( \[saveEncoding\] \)

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Uloží soubor na disk.

**\[saveEncoding\]**  – volitelné [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) znakem volitelný parametr, který se má použít pro uložený soubor kódování. Výchozí hodnota je **UTF8**.

### <a name="exceptions"></a>Výjimky

- **System.IO.IOException**: soubor nelze uložit.

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a>SaveAs\(filename, \[saveEncoding\]\)

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Kódování a uloží soubor s názvem zadaného souboru.

**Název souboru** -String název, který se má použít k uložení souboru.

**\[saveEncoding\]**  – volitelné [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) znakem volitelný parametr, který se má použít pro uložený soubor kódování. Výchozí hodnota je **UTF8**.

### <a name="exceptions"></a>Výjimky

- **System.ArgumentNullException**: **filename** parametr má hodnotu null.
- **System.ArgumentException**: **filename** parametr je prázdný.
- **System.IO.IOException**: soubor nelze uložit.

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a>Properties

### <a name="displayname"></a>DisplayName

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá řetězec, který obsahuje zobrazovaný název tohoto souboru. Název se zobrazí na **souboru** v horní části editoru. Přítomnost hvězdičku \( \* \) na konci názvu označuje, že soubor obsahuje změny, které nebyly uloženy.

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a>Editor

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá [editoru objektu](The-ISEEditor-Object.md) používané pro zadaný soubor.

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a>Kódování

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, získá původní kódování souborů. Toto je **System.Text.Encoding** objektu.

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a>FullPath

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnost jen pro čtení, který získá řetězec, který určuje úplnou cestu otevřený soubor.

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a>IsSaved

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Jen pro čtení logická hodnota vlastnosti, která vrací **$true** Pokud byl uložen soubor po jeho poslední změny.

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a>IsUntitled

Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

Vlastnosti jen pro čtení, která vrací **$true** Pokud soubor nikdy nebyla zadána název.

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a>Viz také

- [The ISEFileCollectionObject](The-ISEFileCollection-Object.md)
- [Účelem ISE Windows PowerShell skriptování objektový Model](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)
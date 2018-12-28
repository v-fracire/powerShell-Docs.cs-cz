---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEFile
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 24549720b8bc35435882533b0eb138de432ede65
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403839"
---
# <a name="the-isefile-object"></a>Objekt ISEFile

**ISEFile** objekt představuje soubor ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE). Je instancí třídy Microsoft.PowerShell.Host.ISE.ISEFile. Toto téma obsahuje seznam členů metody a vlastnosti člena. **$PsISE.CurrentFile** a všechny instance třídy Microsoft.PowerShell.Host.ISE.ISEFile jsou soubory v kolekci souborů v Powershellové karty.

## <a name="methods"></a>Metody

### <a name="save-saveencoding-"></a>Uložit\( \[saveEncoding\] \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Uloží soubor na disk.

**\[saveEncoding\]**  – volitelné [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) znak kódování parametru má být použit pro uloženého souboru. Výchozí hodnota je **UTF8**.

### <a name="exceptions"></a>Výjimky

- **System.IO.IOException**: Soubor nelze uložit.

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a>Uložit jako\(název souboru, \[saveEncoding\]\)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Uloží soubor s názvem zadaného souboru a kódování.

**Název souboru** -String název se použije k uložení souboru.

**\[saveEncoding\]**  – volitelné [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) znak kódování parametru má být použit pro uloženého souboru. Výchozí hodnota je **UTF8**.

### <a name="exceptions"></a>Výjimky

- **System.ArgumentNullException**: **Filename** parametr má hodnotu null.
- **System.ArgumentException**: **Filename** parametru je prázdný.
- **System.IO.IOException**: Soubor nelze uložit.

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a>Properties

### <a name="displayname"></a>DisplayName

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která vrací řetězec, který obsahuje zobrazovaný název tohoto souboru. Název se zobrazí na **souboru** kartě v horní části editoru. Přítomnost hvězdičku \( \* \) na konci názvu označuje, že soubor obsahuje změny, které nebyly uloženy.

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a>Editor

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který získá [editoru objektu](The-ISEEditor-Object.md) , která je použita pro zadaný soubor.

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a>Kódování

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která získá původní kódování souboru. Jedná se **System.Text.Encoding** objektu.

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a>FullPath

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, která vrací řetězec, který určuje úplnou cestu otevřený soubor.

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a>IsSaved

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Jen pro čtení logická vlastnost, která vrací **$true** Pokud byl uložen soubor po jeho poslední úpravy.

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a>IsUntitled

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vlastnost jen pro čtení, který vrací **$true** Pokud soubor nikdy nebyla zadána názvu.

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a>Viz také

- [ISEFileCollectionObject](The-ISEFileCollection-Object.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)
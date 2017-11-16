---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEFile
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: a1fbd48e872684cc578adb03f52430eabdc54c2c
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="the-isefile-object"></a>Objekt ISEFile
  **ISEFile** je soubor v systému Windows PowerShell® Integrované skriptovací prostředí (ISE). Je instance třídy Microsoft.PowerShell.Host.ISE.ISEFile. Toto téma uvádí jeho člen metod a vlastností člena. **$PsISE.CurrentFile** a všechny instance třídy Microsoft.PowerShell.Host.ISE.ISEFile jsou soubory v kolekci soubory na kartě prostředí PowerShell.

## <a name="methods"></a>Metody

### <a name="save-saveencoding-"></a>Uložit\( \[saveEncoding\]\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Uloží soubor na disk.

 **\[saveEncoding\]**  – volitelné [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) znakem volitelný parametr, který se má použít pro uložený soubor kódování. Výchozí hodnota je **UTF8**.

 **Výjimky**
 -   **System.IO.IOException**: soubor nelze uložit.

```
# Save the file using the default encoding (UTF8)
$psIse.CurrentFile.Save()

# Save the file as ASCII.
$psIse.CurrentFile.Save( [System.Text.Encoding]::ASCII )

# Gets the current encoding.
$myfile=$psIse.CurrentFile
$myfile.Encoding

```

### <a name="saveasfilename-saveencoding"></a>Uložit jako\(filename, \[saveEncoding\]\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Kódování a uloží soubor s názvem zadaného souboru.

 **Název souboru** -String název, který se má použít k uložení souboru.

 **\[saveEncoding\]**  – volitelné [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) znakem volitelný parametr, který se má použít pro uložený soubor kódování. Výchozí hodnota je **UTF8**.

 **Výjimky**
 -   **System.ArgumentNullException**: **filename** parametr má hodnotu null.

- **System.ArgumentException**: **filename** parametr je prázdný.

- **System.IO.IOException**: soubor nelze uložit.

```
# Save the file with a full path and name. 
$fullpath = "c:\temp\newname.txt"
$psIse.CurrentFile.SaveAs($fullPath) 
# Save the file with a full path and name and explicitly as UTF8. 
$psIse.CurrentFile.SaveAs( $fullPath, [System.Text.Encoding]::UTF8 )

```

## <a name="properties"></a>Properties

### <a name="displayname"></a>DisplayName
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.

 Vlastnost jen pro čtení, který získá řetězec, který obsahuje zobrazovaný název tohoto souboru. Název se zobrazí na **souboru** v horní části editoru. Přítomnost hvězdičku \( \* \) na konci názvu označuje, že soubor obsahuje změny, které nebyly uloženy.

```
# Shows the display name of the file.
$psIse.CurrentFile.DisplayName

```

### <a name="editor"></a>Editor
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá [editoru objektu](The-ISEEditor-Object.md) používané pro zadaný soubor.

```
# Gets the editor and the text.
$psIse.CurrentFile.Editor.Text

```

### <a name="encoding"></a>Kódování
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, získá původní kódování souborů. Toto je **System.Text.Encoding** objektu.

```
# Shows the encoding for the file. 
$psIse.CurrentFile.Encoding

```

### <a name="fullpath"></a>FullPath
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnost jen pro čtení, který získá řetězec, který určuje úplnou cestu otevřený soubor.

```
# Shows the full path for the file. 
$psIse.CurrentFile.FullPath

```

### <a name="issaved"></a>IsSaved
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Jen pro čtení logická hodnota vlastnosti, která vrací **$true** Pokud byl uložen soubor po jeho poslední změny.

```
# Determines whether the file has been saved since it was last modified.
$myfile=$psIse.CurrentFile
$myfile.IsSaved

```

### <a name="isuntitled"></a>IsUntitled
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vlastnosti jen pro čtení, která vrací **$true** Pokud soubor nikdy nebyla zadána název.

```
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled

```

## <a name="see-also"></a>Viz také
- [ISEFileCollectionObject](The-ISEFileCollection-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)

---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEFileCollection
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: 60bf4dae33f3a71c31e7fdbed0f4fd6ab27a8bd1
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="the-isefilecollection-object"></a>Objekt ISEFileCollection
  **ISEFileCollection** objektu je kolekce **ISEFile** objekty. Příkladem je $psISE.CurrentPowerShellTab.Files kolekce.

## <a name="methods"></a>Metody

### <a name="add-fullpath-"></a>Přidat\( \[fullPath\]\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vytvoří a vrátí nové bez názvu souboru a přidá do kolekce. **IsUntitled** vlastnost nově vytvořený soubor je **$true**.

 **\[fullPath\]**  – volitelný řetězec plně zadaná cesta k souboru. Pokud zahrnete, bude vygenerována výjimka **fullPath** parametr a relativní cesta, nebo pokud použijete název souboru místo úplné cesty.

```
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")

```

### <a name="remove-file-force-"></a>Odebrat\( souboru \[Force\]\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Odebere zadaný soubor z aktuální karta prostředí PowerShell.

 **Soubor** -ISEFile řetězec souboru, který chcete odebrat z kolekce. Pokud soubor nebyl uložen, tato metoda vyvolá výjimku. Použití **vynutit** přepínač parametru Vynutit odstranění neuložené souboru.

 **\[Platnost\]**  -volitelné Boolean Pokud nastavit **$true**, uděluje oprávnění k odebrání souboru i v případě, že ještě nebyl uložen po posledního použití. Výchozí hodnota je **$false**.

```
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a>SetSelectedFile\( selectedFile\)
  Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější. 

 Vybere soubor, který je zadán **selectedFile** parametr.

 **selectedFile** -ISEFile Microsoft.PowerShell.Host.ISE.ISEFile souboru, který chcete vybrat.

```

# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)

```

## <a name="see-also"></a>Viz také
- [Objekt ISEFile](The-ISEFile-Object.md) 
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)

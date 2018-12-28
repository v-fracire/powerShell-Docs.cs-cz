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
# <a name="the-isefilecollection-object"></a>Objekt ISEFileCollection

**ISEFileCollection** objektu je kolekce **ISEFile** objekty. Příkladem je $psISE.CurrentPowerShellTab.Files kolekce.

## <a name="methods"></a>Metody

### <a name="add-fullpath-"></a>Přidat\( \[fullPath\] \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vytvoří a vrátí nový soubor bez názvu a přidá jej do kolekce. **IsUntitled** vlastnost souboru nově vytvořeného **$true**.

**\[fullPath\]**  – volitelný řetězec plně zadaná cesta k souboru. Je vygenerována výjimka, pokud zahrnete **fullPath** parametr a relativní cesty, nebo pokud používáte název souboru místo úplné cesty.

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a>Odebrat\( souboru \[platnost\] \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Odebere zadaný soubor z aktuálního PowerShell tab.

**Soubor** – The ISEFile řetězec souboru, který chcete odebrat z kolekce. Pokud soubor nebyl uložen, tato metoda vyvolá výjimku. Použití **vynutit** přepnout parametr pro vynucení odebrání neuloženého souboru.

**\[Platnost\]**  – volitelný logický-li nastavena na **$true**, udělí oprávnění, odeberte soubor i v případě, že nebyla uložena po poslední použití. Výchozí hodnota je **$false**.

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a>SetSelectedFile\( selectedFile \)

Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.

Vybere soubor, který je určen **selectedFile** parametru.

**selectedFile** – Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile soubor, který chcete vybrat.

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a>Viz také

- [Objekt ISEFile](The-ISEFile-Object.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)
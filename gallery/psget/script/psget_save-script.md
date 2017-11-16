---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Uložení skriptu"
ms.openlocfilehash: 7b692d33e3f86a89505b8d37c0da4177f3dff2c2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="save-script"></a>Uložení skriptu

Umožňuje uložit skript rutiny a projděte si soubor skriptu uložením do zadaného umístění.

## <a name="description"></a>Popis

Uložení skriptu rutina uloží zadaný skript.

## <a name="cmdlet-syntax"></a>Syntaxe rutin

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Uložení skriptu](http://go.microsoft.com/fwlink/?LinkId=619786)

## <a name="example-commands"></a>Příklady příkazů

### <a name="example-1-save-a-script-from-a-repository"></a>Příklad 1: Uložte skript z úložiště
Tento příkaz uloží nejnovější verzi skriptu Fabrikam-ClientScript z GalleryINT úložiště do místní složky C:\ScriptSharingDemo

```powershell
Save-Script -Name Fabrikam-ClientScript -Repository GalleryINT -Path C:\ScriptSharingDemo
```

### <a name="example-2-save-a-version-of-a-script-by-piping-from-the-find-script-cmdlet"></a>Příklad 2: Uložení verze skriptu pomocí zřetězení z rutiny najít skriptu

První příkaz vyhledá verzi 1.5 Fabrikam ClientScript z úložiště GalleryINT a uloží ji do složky C:\ScriptSharingDemo

V druhém příkazu ověří metadata uložený skript.

```powershell
Find-Script -Name Fabrikam-ClientScript -Repository GalleryINT -RequiredVersion 1.5 | Save-Script -Path C:\\ScriptSharingDemo
Test-ScriptFileInfo C:\\ScriptSharingDemo\\Fabrikam-ClientScript.ps1

Version Name Author Description
------- ---- ------ -----------
1.5 Fabrikam-ClientScript manikb Description for the Fabrikam-ClientScript script
```


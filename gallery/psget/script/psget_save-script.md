---
ms.date: 10/17/2017
contributor: keithb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Save-Script
ms.openlocfilehash: 67697fc0e70fb31cad9ad5ae7ce01debef160b81
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="save-script"></a>Save-Script

Umožňuje uložit skript rutiny a projděte si soubor skriptu uložením do zadaného umístění.

## <a name="description"></a>Popis

Uložení skriptu rutina uloží zadaný skript.

## <a name="cmdlet-syntax"></a>Syntaxe rutin

```powershell
Get-Command -Name Save-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Save-Script](http://go.microsoft.com/fwlink/?LinkId=619786)

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

### <a name="example-3-save-a-prerelease-version-of-a-script-from-a-repository"></a>Příklad 3: Uložení předprodejní verze skriptu z úložiště
Tento příkaz uloží nejnovější verzi skriptu Fabrikam-ClientScript z GalleryINT úložiště do místní složky C:\ScriptSharingDemo

```powershell
Save-Script -Name Fabrikam-ClientScript -Path C:\ScriptSharingDemo -AllowPrerelease
```
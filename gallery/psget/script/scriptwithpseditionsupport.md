---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: scriptwithpseditionsupport
ms.openlocfilehash: 18ce2d729199e0587ef92993db7fec44ef744ec7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="script-with-compatible-powershell-editions"></a>Skript se kompatibilní verze prostředí PowerShell
Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.

- **Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.
- **Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.

Používaná verze PowerShellu je uvedena ve vlastnosti PSEdition parametru $PSVersionTable.
```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

Autoři skriptů můžou zabránit provedení skriptu, pokud skript neběží v kompatibilní edici PowerShellu, pomocí parametru PSEdition v příkazu #requires.
```powershell
Set-Content C:\script.ps1 -Value "#requires -PSEdition Core
Get-Process -Name PowerShell"
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a "#requires" statement for PowerShell Core edition. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

Uživatelé Galerie prostředí PowerShell najdete seznam skripty, které jsou podporovány na konkrétní verzi prostředí PowerShell.
Skripty bez PSEdition_Desktop a PSEditon_Core jsou považovány za bez problémů fungují na edice Desktop prostředí PowerShell.

```powershell

# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEditon_Desktop

# Find scripts supported on PowerShell Core editions
Find-Script -Tag PSEditon_Core

```

## <a name="more-details"></a>Další informace
### <a name="modules-with-pseditionsmodulemodulewithpseditionsupportmd"></a>[Moduly s PSEditions](../module/modulewithpseditionsupport.md)
### <a name="pseditions-support-on-powershellgallerypsgallerypsgallerypseditionsmd"></a>[Podpora PSEditions na PowerShellGallery](../../psgallery/psgallery_pseditions.md)
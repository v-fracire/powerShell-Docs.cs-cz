---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Skript s kompatibilní edice Powershellu
ms.openlocfilehash: e364879f611429a8583e550fb7704431e456fbb1
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655272"
---
# <a name="script-with-compatible-powershell-editions"></a>Skript s kompatibilní edice Powershellu

Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.

- **Desktop Edition:** Založený na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na plných edicích Windows, jako je jádro serveru a Windows Desktop.

- **Core Edition:** Založená na prostředí .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na edicích Windows, jako je Nano Server a Windows IoT nízké nároky.

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

Autoři skriptů můžou skript zabránit ve spuštění, pokud neběží v kompatibilní edici powershellu, pomocí parametru PSEdition v `#requires` příkazu.

```powershell
Set-Content C:\script.ps1 -Value "#requires -PSEdition Core
Get-Process -Name PowerShell"
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a "#requires" statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

Galerie prostředí PowerShell uživatelé najdou seznam skripty, které jsou podporovány na konkrétní edici Powershellu.
Skripty bez PSEdition_Desktop a PSEdition_Core značek jsou považovány za fungovat správně v prostředí PowerShell Desktop edition.

```powershell
# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEdition_Desktop

# Find scripts supported on PowerShell Core edition
Find-Script -Tag PSEdition_Core
```

## <a name="more-details"></a>Další podrobnosti

- [Moduly s PSEditions](module-psedition-support.md)
- [Podpora PSEditions na PowerShellGallery](../how-to/finding-packages/searching-by-compatibility.md)

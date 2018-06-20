---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutiny, psget
title: Skript se kompatibilní verze prostředí PowerShell
ms.openlocfilehash: 27b50be4e99b6c6b8fa089d1d4a436a27eeb17c9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219245"
---
# <a name="script-with-compatible-powershell-editions"></a><span data-ttu-id="4ff36-103">Skript se kompatibilní verze prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ff36-103">Script with compatible PowerShell editions</span></span>

<span data-ttu-id="4ff36-104">Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.</span><span class="sxs-lookup"><span data-stu-id="4ff36-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="4ff36-105">**Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="4ff36-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="4ff36-106">**Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="4ff36-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="4ff36-107">Používaná verze PowerShellu je uvedena ve vlastnosti PSEdition parametru $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="4ff36-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>

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

<span data-ttu-id="4ff36-108">Autoři skriptů můžou zabránit provedení skriptu, pokud skript neběží v kompatibilní edici PowerShellu, pomocí parametru PSEdition v příkazu #requires.</span><span class="sxs-lookup"><span data-stu-id="4ff36-108">Script authors can prevent a script from executing unless it is run on a compatible edition of PowerShell using the PSEdition parameter on a #requires statement.</span></span>

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

<span data-ttu-id="4ff36-109">Uživatelé Galerie prostředí PowerShell najdete seznam skripty, které jsou podporovány na konkrétní verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ff36-109">PowerShell Gallery users can find the list of scripts supported on a specific PowerShell Edition.</span></span>
<span data-ttu-id="4ff36-110">Skripty bez PSEdition_Desktop a PSEditon_Core jsou považovány za bez problémů fungují na edice Desktop prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ff36-110">Scripts without PSEdition_Desktop and PSEditon_Core are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell

# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEditon_Desktop

# Find scripts supported on PowerShell Core editions
Find-Script -Tag PSEditon_Core

```

## <a name="more-details"></a><span data-ttu-id="4ff36-111">Další informace</span><span class="sxs-lookup"><span data-stu-id="4ff36-111">More details</span></span>

- [<span data-ttu-id="4ff36-112">Moduly s PSEditions</span><span class="sxs-lookup"><span data-stu-id="4ff36-112">Modules with PSEditions</span></span>](module-psedition-support.md)
- [<span data-ttu-id="4ff36-113">Podpora PSEditions na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="4ff36-113">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-items/searching-by-psedition.md)
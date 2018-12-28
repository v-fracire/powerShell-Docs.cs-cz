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
# <a name="script-with-compatible-powershell-editions"></a><span data-ttu-id="69301-103">Skript s kompatibilní edice Powershellu</span><span class="sxs-lookup"><span data-stu-id="69301-103">Script with compatible PowerShell editions</span></span>

<span data-ttu-id="69301-104">Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.</span><span class="sxs-lookup"><span data-stu-id="69301-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="69301-105">**Desktop Edition:** Založený na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na plných edicích Windows, jako je jádro serveru a Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="69301-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>

- <span data-ttu-id="69301-106">**Core Edition:** Založená na prostředí .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze Powershellu spouštěné na edicích Windows, jako je Nano Server a Windows IoT nízké nároky.</span><span class="sxs-lookup"><span data-stu-id="69301-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="69301-107">Používaná verze PowerShellu je uvedena ve vlastnosti PSEdition parametru $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="69301-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>

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

<span data-ttu-id="69301-108">Autoři skriptů můžou skript zabránit ve spuštění, pokud neběží v kompatibilní edici powershellu, pomocí parametru PSEdition v `#requires` příkazu.</span><span class="sxs-lookup"><span data-stu-id="69301-108">Script authors can prevent a script from executing unless it is run on a compatible edition of PowerShell using the PSEdition parameter on a `#requires` statement.</span></span>

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

<span data-ttu-id="69301-109">Galerie prostředí PowerShell uživatelé najdou seznam skripty, které jsou podporovány na konkrétní edici Powershellu.</span><span class="sxs-lookup"><span data-stu-id="69301-109">PowerShell Gallery users can find the list of scripts supported on a specific PowerShell Edition.</span></span>
<span data-ttu-id="69301-110">Skripty bez PSEdition_Desktop a PSEdition_Core značek jsou považovány za fungovat správně v prostředí PowerShell Desktop edition.</span><span class="sxs-lookup"><span data-stu-id="69301-110">Scripts without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop edition.</span></span>

```powershell
# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEdition_Desktop

# Find scripts supported on PowerShell Core edition
Find-Script -Tag PSEdition_Core
```

## <a name="more-details"></a><span data-ttu-id="69301-111">Další podrobnosti</span><span class="sxs-lookup"><span data-stu-id="69301-111">More details</span></span>

- [<span data-ttu-id="69301-112">Moduly s PSEditions</span><span class="sxs-lookup"><span data-stu-id="69301-112">Modules with PSEditions</span></span>](module-psedition-support.md)
- [<span data-ttu-id="69301-113">Podpora PSEditions na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="69301-113">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-packages/searching-by-compatibility.md)

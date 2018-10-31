---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Instalace modulu PowerShellGet
ms.openlocfilehash: 5c51cb1c7ea2538cc5f8503ce6c5d80edda70e15
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002214"
---
# <a name="installing-powershellget"></a><span data-ttu-id="fce9f-103">Instalace modulu PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="fce9f-103">Installing PowerShellGet</span></span>

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a><span data-ttu-id="fce9f-104">Správce balíčků PowerShellGet je modul dodávané v následujících verzích</span><span class="sxs-lookup"><span data-stu-id="fce9f-104">PowerShellGet is an in-box module in the following releases</span></span>

- <span data-ttu-id="fce9f-105">[Windows 10](https://www.microsoft.com/windows) nebo novější</span><span class="sxs-lookup"><span data-stu-id="fce9f-105">[Windows 10](https://www.microsoft.com/windows) or newer</span></span>
- <span data-ttu-id="fce9f-106">[Windows Server 2016](/windows-server/windows-server) nebo novější</span><span class="sxs-lookup"><span data-stu-id="fce9f-106">[Windows Server 2016](/windows-server/windows-server) or newer</span></span>
- <span data-ttu-id="fce9f-107">[Windows Management Frameworku (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) nebo novější</span><span class="sxs-lookup"><span data-stu-id="fce9f-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/download/details.aspx?id=50395) or newer</span></span>
- [<span data-ttu-id="fce9f-108">PowerShell 6</span><span class="sxs-lookup"><span data-stu-id="fce9f-108">PowerShell 6</span></span>](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a><span data-ttu-id="fce9f-109">Získání modulu PowerShellGet pro prostředí PowerShell verze 3.0 a 4.0</span><span class="sxs-lookup"><span data-stu-id="fce9f-109">Get PowerShellGet module for PowerShell versions 3.0 and 4.0</span></span>

- [<span data-ttu-id="fce9f-110">PackageManagement MSI</span><span class="sxs-lookup"><span data-stu-id="fce9f-110">PackageManagement MSI</span></span>](https://www.microsoft.com/download/details.aspx?id=51451)

## <a name="get-the-latest-version-from-powershell-gallery"></a><span data-ttu-id="fce9f-111">Získat nejnovější verzi z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="fce9f-111">Get the latest version from PowerShell Gallery</span></span>

- <span data-ttu-id="fce9f-112">Před aktualizací modulu PowerShellGet, by měla vždy nainstalujte si nejnovějšího zprostředkovatele Nuget.</span><span class="sxs-lookup"><span data-stu-id="fce9f-112">Before updating PowerShellGet, you should always install the latest Nuget provider.</span></span> <span data-ttu-id="fce9f-113">Chcete-li to mohli udělat, spusťte následující v relaci Powershellu se zvýšenými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="fce9f-113">To do that, run the following in an elevated PowerShell session.</span></span>

  ```powershell
  Install-PackageProvider Nuget –Force
  Exit
  ```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a><span data-ttu-id="fce9f-114">U systémů pomocí prostředí PowerShell 5.0 (nebo novější) můžete nainstalovat nejnovější modul PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="fce9f-114">For systems with PowerShell 5.0 (or newer) you can install the latest PowerShellGet</span></span>

- <span data-ttu-id="fce9f-115">Chcete-li to provést ve Windows 10, Windows serveru 2016, všechny systémy s WMF 5.0 nebo 5.1 nainstalované nebo jakéhokoli systému pomocí prostředí PowerShell 6, spusťte následující příkazy z relace Powershellu se zvýšenými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="fce9f-115">To do this on Windows 10, Windows Server 2016, any system with WMF 5.0 or 5.1 installed, or any system with PowerShell 6, run the following commands from an elevated PowerShell session.</span></span>

  ```powershell
  Install-Module –Name PowerShellGet –Force
  Exit
  ```

- <span data-ttu-id="fce9f-116">Použití `Update-Module` získat novější verze.</span><span class="sxs-lookup"><span data-stu-id="fce9f-116">Use `Update-Module` to get newer versions.</span></span>

  ```powershell
  Update-Module -Name PowerShellGet
  Exit
  ```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpswwwmicrosoftcomdownloaddetailsaspxid51451"></a><span data-ttu-id="fce9f-117">Pro systémy s Powershellem 3 nebo 4 prostředí PowerShell, který jste nainstalovali [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)</span><span class="sxs-lookup"><span data-stu-id="fce9f-117">For systems running PowerShell 3 or PowerShell 4, that have installed the [PackageManagement MSI](https://www.microsoft.com/download/details.aspx?id=51451)</span></span>

- <span data-ttu-id="fce9f-118">Použijte následující rutiny Správce balíčků PowerShellGet z relace Powershellu se zvýšenými oprávněními na moduly uložit do místního adresáře</span><span class="sxs-lookup"><span data-stu-id="fce9f-118">Use below PowerShellGet cmdlet from an elevated PowerShell session to save the modules to a local directory</span></span>

  ```powershell
  Save-Module PowerShellGet -Path C:\LocalFolder
  Exit
  ```

- <span data-ttu-id="fce9f-119">Ujistěte se, že Správce balíčků PowerShellGet a PackageManagment moduly nejsou načtené v jiných procesech.</span><span class="sxs-lookup"><span data-stu-id="fce9f-119">Ensure that PowerShellGet and PackageManagment modules are not loaded in any other processes.</span></span>
- <span data-ttu-id="fce9f-120">Odstraňte obsah `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` a `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` složek.</span><span class="sxs-lookup"><span data-stu-id="fce9f-120">Delete contents of `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` and  `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` folders.</span></span>
- <span data-ttu-id="fce9f-121">Znovu otevřete konzoly PS se zvýšenými oprávněními a spusťte následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="fce9f-121">Re-open the PS Console with elevated permissions then run the following commands.</span></span>

  ```powershell
  Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
  Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
  ```

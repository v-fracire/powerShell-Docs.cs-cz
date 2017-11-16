---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Získat modul PowerShellGet"
ms.openlocfilehash: a5a323b17709e519ec57623a9dd7499e591bbed5
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
<a name="get-powershellget-module"></a><span data-ttu-id="22f12-103">Získat modul PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="22f12-103">Get PowerShellGet Module</span></span>
========================

### <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a><span data-ttu-id="22f12-104">PowerShellGet je modul integrované v následujících verzích</span><span class="sxs-lookup"><span data-stu-id="22f12-104">PowerShellGet is an in-box module in the following releases</span></span>
- <span data-ttu-id="22f12-105">[Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10) nebo novější</span><span class="sxs-lookup"><span data-stu-id="22f12-105">[Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10) or newer</span></span>
- <span data-ttu-id="22f12-106">[Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/get-started/windows-server-2016) nebo novější</span><span class="sxs-lookup"><span data-stu-id="22f12-106">[Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/get-started/windows-server-2016) or newer</span></span>
- <span data-ttu-id="22f12-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) nebo novější</span><span class="sxs-lookup"><span data-stu-id="22f12-107">[Windows Management Framework (WMF) 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) or newer</span></span>
- [<span data-ttu-id="22f12-108">Prostředí PowerShell 6</span><span class="sxs-lookup"><span data-stu-id="22f12-108">PowerShell 6</span></span>](https://github.com/PowerShell/PowerShell/releases)

### <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a><span data-ttu-id="22f12-109">Získat PowerShellGet modul prostředí PowerShell verze 3.0 a 4.0</span><span class="sxs-lookup"><span data-stu-id="22f12-109">Get PowerShellGet module for PowerShell versions 3.0 and 4.0</span></span>
- [<span data-ttu-id="22f12-110">PackageManagement MSI</span><span class="sxs-lookup"><span data-stu-id="22f12-110">PackageManagement MSI</span></span>](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409) 

### <a name="get-the-latest-version-from-powershell-gallery"></a><span data-ttu-id="22f12-111">Získat nejnovější verzi z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="22f12-111">Get the latest version from PowerShell Gallery</span></span>

- <span data-ttu-id="22f12-112">Před aktualizací PowerShellGet, byste měli vždycky nainstalovat nejnovější zprostředkovatel Nuget.</span><span class="sxs-lookup"><span data-stu-id="22f12-112">Before updating PowerShellGet, you should always install the latest Nuget provider.</span></span> <span data-ttu-id="22f12-113">K tomu, spusťte následující příkazy v relaci prostředí PowerShell zvýšenými oprávněními.</span><span class="sxs-lookup"><span data-stu-id="22f12-113">To do that, run the following in an elevated PowerShell session.</span></span>
```powershell
Install-PackageProvider Nuget –Force
Exit
```

#### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a><span data-ttu-id="22f12-114">Pro systémy s PowerShell 5.0 (nebo novější) můžete nainstalovat nejnovější PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="22f12-114">For systems with PowerShell 5.0 (or newer) you can install the latest PowerShellGet</span></span> 
- <span data-ttu-id="22f12-115">Chcete-li to provést ve Windows 10, Windows Server 2016, všechny systémy s WMF 5.0 nebo 5.1 nainstalována nebo jakéhokoli systému pomocí prostředí PowerShell 6, spusťte následující příkazy z zvýšenými relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22f12-115">To do this on Windows 10, Windows Server 2016, any system with WMF 5.0 or 5.1 installed, or any system with PowerShell 6, run the following commands from an elevated PowerShell session.</span></span>
```powershell
Install-Module –Name PowerShellGet –Force
Exit
```

- <span data-ttu-id="22f12-116">Aktualizace modulu použijte k získání novější verze.</span><span class="sxs-lookup"><span data-stu-id="22f12-116">Use Update-Module to get newer versions.</span></span>
```powershell
Update-Module -Name PowerShellGet
Exit
```

#### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpgomicrosoftcomfwlinklinkid746217clcid0x409"></a><span data-ttu-id="22f12-117">Pro systémy s operačním systémem prostředí PowerShell 3 nebo 4 prostředí PowerShell, který jste nainstalovali [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="22f12-117">For systems running PowerShell 3 or PowerShell 4, that have installed the [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)</span></span>

- <span data-ttu-id="22f12-118">K uložení moduly do místního adresáře použijte následující rutinu PowerShellGet z zvýšenými relace prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="22f12-118">Use below PowerShellGet cmdlet from an elevated PowerShell session to save the modules to a local directory</span></span>

```powershell
Save-Module PowerShellGet -Path C:\LocalFolder
Exit
```

- <span data-ttu-id="22f12-119">Ujistěte se, že moduly PowerShellGet a PackageManagment nenačtou v jiné procesy.</span><span class="sxs-lookup"><span data-stu-id="22f12-119">Ensure that PowerShellGet and PackageManagment modules are not loaded in any other processes.</span></span>
- <span data-ttu-id="22f12-120">Odstraňte obsah `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` a `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` složek.</span><span class="sxs-lookup"><span data-stu-id="22f12-120">Delete contents of `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` and  `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` folders.</span></span>
- <span data-ttu-id="22f12-121">Znovu otevřete konzolu PS se zvýšenými oprávněními a spusťte následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="22f12-121">Re-open the PS Console with elevated permissions then run the following commands.</span></span>

```powershell
Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
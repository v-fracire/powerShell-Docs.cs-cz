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
<a name="get-powershellget-module"></a>Získat modul PowerShellGet
========================

### <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a>PowerShellGet je modul integrované v následujících verzích
- [Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10) nebo novější
- [Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/get-started/windows-server-2016) nebo novější
- [Windows Management Framework (WMF) 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) nebo novější
- [Prostředí PowerShell 6](https://github.com/PowerShell/PowerShell/releases)

### <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a>Získat PowerShellGet modul prostředí PowerShell verze 3.0 a 4.0
- [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409) 

### <a name="get-the-latest-version-from-powershell-gallery"></a>Získat nejnovější verzi z Galerie prostředí PowerShell

- Před aktualizací PowerShellGet, byste měli vždycky nainstalovat nejnovější zprostředkovatel Nuget. K tomu, spusťte následující příkazy v relaci prostředí PowerShell zvýšenými oprávněními.
```powershell
Install-PackageProvider Nuget –Force
Exit
```

#### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a>Pro systémy s PowerShell 5.0 (nebo novější) můžete nainstalovat nejnovější PowerShellGet 
- Chcete-li to provést ve Windows 10, Windows Server 2016, všechny systémy s WMF 5.0 nebo 5.1 nainstalována nebo jakéhokoli systému pomocí prostředí PowerShell 6, spusťte následující příkazy z zvýšenými relace prostředí PowerShell.
```powershell
Install-Module –Name PowerShellGet –Force
Exit
```

- Aktualizace modulu použijte k získání novější verze.
```powershell
Update-Module -Name PowerShellGet
Exit
```

#### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpgomicrosoftcomfwlinklinkid746217clcid0x409"></a>Pro systémy s operačním systémem prostředí PowerShell 3 nebo 4 prostředí PowerShell, který jste nainstalovali [PackageManagement MSI](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

- K uložení moduly do místního adresáře použijte následující rutinu PowerShellGet z zvýšenými relace prostředí PowerShell

```powershell
Save-Module PowerShellGet -Path C:\LocalFolder
Exit
```

- Ujistěte se, že moduly PowerShellGet a PackageManagment nenačtou v jiné procesy.
- Odstraňte obsah `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` a `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` složek.
- Znovu otevřete konzolu PS se zvýšenými oprávněními a spusťte následující příkazy.

```powershell
Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
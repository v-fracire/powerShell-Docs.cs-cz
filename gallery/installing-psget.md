---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Instalace modulu PowerShellGet
ms.openlocfilehash: c385f7fbf6b688a11face9c3ebf4e6475a7b4c33
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893956"
---
# <a name="installing-powershellget"></a>Instalace modulu PowerShellGet

## <a name="powershellget-is-an-in-box-module-in-the-following-releases"></a>Správce balíčků PowerShellGet je modul dodávané v následujících verzích

- [Windows 10](https://www.microsoft.com/en-us/windows) nebo novější
- [Windows Server 2016](/windows-server/windows-server) nebo novější
- [Windows Management Frameworku (WMF) 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) nebo novější
- [PowerShell 6](https://github.com/PowerShell/PowerShell/releases)

## <a name="get-powershellget-module-for-powershell-versions-30-and-40"></a>Získání modulu PowerShellGet pro prostředí PowerShell verze 3.0 a 4.0

- [PackageManagement MSI](https://www.microsoft.com/en-us/download/details.aspx?id=51451)

## <a name="get-the-latest-version-from-powershell-gallery"></a>Získat nejnovější verzi z Galerie prostředí PowerShell

- Před aktualizací modulu PowerShellGet, by měla vždy nainstalujte si nejnovějšího zprostředkovatele Nuget. Chcete-li to mohli udělat, spusťte následující v relaci Powershellu se zvýšenými oprávněními.

  ```powershell
  Install-PackageProvider Nuget –Force
  Exit
  ```

### <a name="for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget"></a>U systémů pomocí prostředí PowerShell 5.0 (nebo novější) můžete nainstalovat nejnovější modul PowerShellGet

- Chcete-li to provést ve Windows 10, Windows serveru 2016, všechny systémy s WMF 5.0 nebo 5.1 nainstalované nebo jakéhokoli systému pomocí prostředí PowerShell 6, spusťte následující příkazy z relace Powershellu se zvýšenými oprávněními.

  ```powershell
  Install-Module –Name PowerShellGet –Force
  Exit
  ```

- Použití `Update-Module` získat novější verze.

  ```powershell
  Update-Module -Name PowerShellGet
  Exit
  ```

### <a name="for-systems-running-powershell-3-or-powershell-4-that-have-installed-the-packagemanagement-msihttpswwwmicrosoftcomen-usdownloaddetailsaspxid51451"></a>Pro systémy s Powershellem 3 nebo 4 prostředí PowerShell, který jste nainstalovali [PackageManagement MSI](https://www.microsoft.com/en-us/download/details.aspx?id=51451)

- Použijte následující rutiny Správce balíčků PowerShellGet z relace Powershellu se zvýšenými oprávněními na moduly uložit do místního adresáře

  ```powershell
  Save-Module PowerShellGet -Path C:\LocalFolder
  Exit
  ```

- Ujistěte se, že Správce balíčků PowerShellGet a PackageManagment moduly nejsou načtené v jiných procesech.
- Odstraňte obsah `$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\` a `$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\` složek.
- Znovu otevřete konzoly PS se zvýšenými oprávněními a spusťte následující příkazy.

  ```powershell
  Copy-Item "C:\LocalFolder\PowerShellGet\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PowerShellGet\" -Recurse -Force
  Copy-Item "C:\LocalFolder\PackageManagement\*" "$env:ProgramFiles\WindowsPowerShell\Modules\PackageManagement\" -Recurse -Force
  ```
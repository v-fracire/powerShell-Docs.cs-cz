---
title: Vzdálená komunikace WSMan (WS-Management) v PowerShellu Core
description: Vzdálená komunikace v prostředí PowerShell Core pomocí WSMan
ms.date: 08/06/2018
ms.openlocfilehash: ce58ed88f59f32b0f83951e55de36e829f7fa3f4
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587342"
---
# <a name="ws-management-wsman-remoting-in-powershell-core"></a>Vzdálená komunikace WSMan (WS-Management) v PowerShellu Core

## <a name="instructions-to-create-a-remoting-endpoint"></a>Pokyny k vytvoření koncového bodu vzdálené komunikace

Balíček PowerShell Core pro Windows zahrnuje modul plug-in WinRM (`pwrshplugin.dll`) a instalační skript (`Install-PowerShellRemoting.ps1`) v `$PSHome`.
Tyto soubory prostředí PowerShell tak, aby přijímal příchozí připojení vzdáleného prostředí PowerShell, když svůj koncový bod je zadán povolit.

### <a name="motivation"></a>Motivace

Instalace powershellu mohou vytvořit relace prostředí PowerShell na vzdálených počítačích pomocí `New-PSSession` a `Enter-PSSession`.
Který umožňuje přijímat příchozí připojení vzdáleného prostředí PowerShell, musí uživatel vytvořit koncový bod vzdálené komunikace služby WinRM.
Jedná se o explicitní vyjádřit výslovný souhlas scénář Pokud uživatel spustí instalaci PowerShellRemoting.ps1 vytvořte koncový bod služby WinRM.
Instalační skript je krátkodobé řešení, dokud přidáme další funkce k `Enable-PSRemoting` provést stejnou akci.
Další podrobnosti najdete v tématu problém [#1193](https://github.com/PowerShell/PowerShell/issues/1193).

### <a name="script-actions"></a>Akce skriptů

Skript

1. Vytvoří adresář pro modul plug-in v rámci %windir%\System32\PowerShell
1. Zkopíruje pwrshplugin.dll do tohoto umístění
1. Generuje konfigurační soubor
1. Registry to modulu plug-in pomocí WinRM

### <a name="registration"></a>Registrace

Skript je třeba spustit v relaci prostředí PowerShell na úrovni správce a běží ve dvou režimech.

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a>Spuštění instance prostředí PowerShell, které se budou registrovat

```powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a>Spustit jiná instance prostředí PowerShell jménem instanci, která k registraci

```powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>"
```

Příklad:

```powershell
Set-Location -Path 'C:\Program Files\PowerShell\6.0.0\'
.\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0\"
```

**Poznámka:** registrační skript vzdálené komunikace restartuje WinRM, takže všechny existující PSRP relace bude ukončena ihned po spuštění skriptu. Pokud během vzdálené relace, to se ukončí připojení.

## <a name="how-to-connect-to-the-new-endpoint"></a>Jak se připojit k nový koncový bod

Vytvořit relaci Powershellu se nový koncový bod prostředí PowerShell zadáním `-ConfigurationName "some endpoint name"`. Pokud chcete připojit k instanci prostředí PowerShell jako v předchozím příkladu, použijte buď:

```powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0"
```

Všimněte si, že `New-PSSession` a `Enter-PSSession` volání, které neurčují `-ConfigurationName` se zaměří na výchozí koncový bod prostředí PowerShell, `microsoft.powershell`.
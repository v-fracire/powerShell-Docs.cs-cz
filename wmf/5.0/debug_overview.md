---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: dee5e8206c61d79faadf8573a82c74d4ac0fb8e0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="improvements-in-powershell-script-debugging"></a>Vylepšené ladění powershellového skriptu

Množství vylepšení byly provedeny v prostředí PowerShell 5.0 zdokonalování ladění:

## <a name="break-all"></a>Rozdělit všechny

Konzole PowerShell a Windows PowerShell ISE teď umožňují rozdělit na ladicí program ke spouštění skriptů. Toto funguje ve místních i vzdálených relací.

V konzole, stiskněte klávesu **Ctrl + Break**.

V integrovaném Skriptovacím, stiskněte klávesu **Ctrl + B**, nebo použijte **ladění -> Rozdělit všechny** příkazu nabídky.

## <a name="remote-debugging-and-remote-file-editing-in-windows-powershell-ise"></a>Vzdálené ladění a vzdálené úpravy souborů v systému Windows PowerShell ISE

Windows PowerShell ISE nyní umožňuje otevírat a upravovat soubory ve vzdálené relaci spuštěním příkazu PSEdit.
Například můžete otevřít soubor pro úpravy z příkazového řádku v relaci vzdálené následujícím způsobem:

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

Kromě toho teď můžete upravit a uložit změny v ke vzdálenému souboru, který se automaticky otevře v systému Windows PowerShell ISE při průchodu zarážky.
Nyní můžete ladění soubor skriptu, který běží na vzdáleném počítači, upravte soubor opravte chybu a pak znovu spusťte upravené skriptu.

## <a name="advanced-script-debugging"></a>Ladění pokročilé skriptů

Existují nové, pokročilé funkce ladění, které umožňují připojení k libovolnému procesu místního počítače, který načetl prostředí Windows PowerShell a ladění libovolný prostředí runspace v tomto procesu.

### <a name="runspace-debugging"></a>Ladění prostředí runspace

Byly přidané nové rutiny, které umožňují seznamu aktuální prostředí runspace v procesu a připojení v konzole pro prostředí Windows PowerShell nebo ISE ladicí program k tohoto prostředí runspace pro ladění skriptů:

-   Get-Runspace
-   Debug-Runspace
-   Enable-RunspaceDebug
-   Disable-RunspaceDebug
-   Get-RunspaceDebug

### <a name="attach-to-process-hosting-powershell"></a>Připojit k procesu hostování prostředí PowerShell

Nyní můžete připojit k libovolnému počítače procesu, který má prostředí Windows PowerShell načíst. To uděláte tak, že zadáte do interaktivní relace v procesu, podobně jako na tom, jak zadat do interaktivní vzdálené relace spuštěním rutiny Enter-PSSession:

-   Enter-PSHostProcess
-   Exit-PSHostProcess
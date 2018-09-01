---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Použití proměnných k ukládání objektů
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: f4254199facb914c68a487b281b30070c35550a1
ms.sourcegitcommit: c170a1608d20d3c925d79c35fa208f650d014146
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2018
ms.locfileid: "43353214"
---
# <a name="using-variables-to-store-objects"></a>Použití proměnných k ukládání objektů

Prostředí PowerShell funguje s objekty. Prostředí PowerShell vám umožňuje vytvoření pojmenovaných objektů, které jsou známé jako proměnné.
Názvy proměnných může obsahovat alfanumerické znaky může znak podtržítka. Při použití v prostředí PowerShell, proměnná je vždy určena pomocí \$ znak následovaný název proměnné.

## <a name="creating-a-variable"></a>Vytváření proměnných

Zadejte platný název proměnné, můžete vytvořit proměnnou:

```
PS> $loc
PS>
```

V tomto příkladu vrátí žádný výsledek, protože `$loc` nemá žádnou hodnotu. Můžete vytvořit proměnnou a přiřaďte mu hodnotu do jednoho kroku. Prostředí PowerShell vytvoří pouze proměnné, pokud neexistuje.
V opačném případě přiřazuje zadanou hodnotu existující proměnné. Následující příklad uloží aktuální umístění do proměnné `$loc`:

```powershell
$loc = Get-Location
```

Prostředí PowerShell když zadáte tento příkaz nezobrazí se žádný výstup. Prostředí PowerShell odešle výstup "Get-Location" `$loc`. V prostředí PowerShell posílá data, která není přiřazené nebo je přesměrován na obrazovku. Zadáním `$loc` zobrazuje aktuální umístění:

```
PS> $loc

Path
----
C:\temp
```

Můžete použít `Get-Member` k zobrazení informací o obsahu proměnné. `Get-Member` ukazuje, že `$loc` je **PathInfo** objektu, stejně jako výstup z `Get-Location`:

```powershell
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

## <a name="manipulating-variables"></a>Manipulace s proměnné

PowerShell nabízí několik příkazy pro manipulaci s proměnné. Úplný seznam ve formě čitelné zobrazíte zadáním příkazu:

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

Prostředí PowerShell také vytvoří několik proměnných definovaných systémem. Můžete použít `Remove-Variable` rutina pro odebrání proměnné, které nejsou řízeny pomocí prostředí PowerShell, z aktuální relace. Zadejte následující příkaz pro vymazání všech proměnných:

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

Po spuštění předchozího příkazu `Get-Variable` rutina ukazuje systémové proměnné prostředí PowerShell.

Prostředí PowerShell také vytvoří proměnné jednotku. Chcete-li zobrazit všechny proměnné prostředí PowerShell pomocí proměnné jednotky použijte následující příklad:

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a>Použití proměnných cmd.exe

Prostředí PowerShell můžete použít stejné proměnné prostředí, která je k dispozici pro jakýkoli proces Windows, včetně **cmd.exe**. Tyto proměnné jsou vystaveny prostřednictvím jednotku s názvem `env:`. Tyto proměnné můžete zobrazit zadáním následujícího příkazu:

```powershell
Get-ChildItem env:
```

Standardní `*-Variable` rutin nejsou navržené pro práci s proměnnými prostředí. Proměnné prostředí jsou přístupné pomocí `env:` předponu jednotky. Například **adresáře % SystemRoot %** proměnné v **cmd.exe** obsahuje název kořenového adresáře operačního systému. V Powershellu, použijte `$env:SystemRoot` pro přístup k stejnou hodnotu.

```
PS> $env:SystemRoot
C:\WINDOWS
```

Můžete také vytvořit a upravit proměnné prostředí z v rámci prostředí PowerShell. Proměnné prostředí v Powershellu použijte stejná pravidla pro proměnné prostředí použít jinde v operačním systému. Následující příklad vytvoří novou proměnnou prostředí:

```powershell
$env:LIB_PATH='/usr/local/lib'
```

I když není vyžadována, je běžné, že názvy proměnných prostředí použít všechna velká písmena.
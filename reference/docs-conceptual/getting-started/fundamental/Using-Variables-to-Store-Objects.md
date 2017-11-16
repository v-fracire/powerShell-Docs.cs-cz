---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Použití proměnných do úložiště objektů"
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: 9a95d421fa2686608a565987c16fecc41c3c6d20
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/13/2017
---
# <a name="using-variables-to-store-objects"></a>Použití proměnných do úložiště objektů
PowerShell funguje s objekty. Prostředí PowerShell umožňuje vytvářet proměnné, které jsou v podstatě s názvem objektů, aby byla zachována výstup pro pozdější použití. Pokud se používají k práci s proměnné v jiných nutný Pamatujte, že proměnné prostředí PowerShell jsou objekty, nikoli textu.

Proměnné jsou vždy zadaný počáteční znak $ a může obsahovat alfanumerické znaky nebo podtržítko jejich názvy.

### <a name="creating-a-variable"></a>Vytvoření proměnné
Zadejte platný název proměnné, můžete vytvořit proměnnou:

```
PS> $loc
PS>
```

Tento příkaz vrátí žádný výsledek protože **$loc** nemá hodnotu. Můžete vytvořit proměnnou a přiřaďte mu hodnotu do jednoho kroku. Prostředí PowerShell vytvoří proměnnou pouze, pokud neexistuje; jinak přiřadí zadanou hodnotu existující proměnné. K uložení vaše aktuální umístění v proměnné **$loc**, zadejte:

```
$loc = Get-Location
```

Neexistuje žádný výstup se zobrazí, když zadáte tento příkaz, protože výstup posílá místní $ V prostředí PowerShell je zobrazený výstup vedlejším účinkem skutečnost, že data, která není jinak směrované, vždy se odešlou do obrazovky. Zadáním $loc zobrazí vaše aktuální umístění:

```
PS> $loc

Path
----
C:\temp
```

Můžete použít **Get-člen** zobrazíte informace o obsahu proměnných. Potrubí $loc členovi Get vám ukáže, že je **PathInfo** objekt, stejně jako výstup z Get-umístění:

```
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

### <a name="manipulating-variables"></a>Manipulace s proměnné
Prostředí PowerShell obsahuje několik příkazů k manipulaci s proměnné. Úplný seznam v čitelné podoby zobrazíte zadáním příkazu:

```
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

Kromě proměnné, které vytvoříte v aktuální relaci prostředí PowerShell existuje několik proměnné definované v systému. Můžete použít **Remove-Variable** rutiny vyčistit všechny proměnné, které nejsou řízené prostředí PowerShell. Zadejte následující příkaz k vymazání všech proměnných:

```
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

Vznikne tak výzvu k potvrzení, které vidíte níže.

```
Confirm
Are you sure you want to perform this action?
Performing operation "Remove Variable" on Target "Name: Error".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):A
```

Pokud pak spustíte **Get-Variable** rutiny, zobrazí se zbývající proměnné prostředí PowerShell. Vzhledem k tomu, že je také proměnná jednotku prostředí PowerShell, můžete také zobrazit všechny proměnné prostředí PowerShell zadáním:

```
Get-ChildItem variable:
```

### <a name="using-cmdexe-variables"></a>Použití proměnných Cmd.exe
I když prostředí PowerShell není Cmd.exe, běží v prostředí shell příkazového a stejné proměnné, které jsou k dispozici v jakémkoli prostředí, můžete použít v systému Windows. Tyto proměnné se zveřejňují přes jednotku s názvem **env**:. Tyto proměnné můžete zobrazit zadáním:

```
Get-ChildItem env:
```

I když standardní rutiny proměnné nejsou navrženy pro práci s **env:** proměnné, stále můžete například vytvořit zadáním **env:** předponu. Například informace o kořenový adresář operačního systému, můžete použít příkazového prostředí **% SystemRoot %** proměnnou z prostředí PowerShell zadáním:

```
PS> $env:SystemRoot
C:\WINDOWS
```

Můžete také vytvořit a upravit proměnné prostředí z prostředí PowerShell. Proměnné prostředí, které jsou k němu přistupovat z prostředí Windows PowerShell požadavkům normální pravidla pro proměnné prostředí jinde v systému Windows.


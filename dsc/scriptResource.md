---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC skriptu prostředků"
ms.openlocfilehash: 3824cbf48d980069b923d91e1fa24739e5d4e617
ms.sourcegitcommit: 378c7ed4e8c8c1c5fe71417b9ba672a4c990630b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/05/2018
---
# <a name="dsc-script-resource"></a>DSC skriptu prostředků

 
> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**Skriptu** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke spuštění blocích skriptu prostředí Windows PowerShell na cílové uzly. `Script` Prostředek má `GetScript`, `SetScript`, a `TestScript` vlastnosti. Tyto vlastnosti musí být nastaven na skript bloky, které poběží na každý cílový uzel. 

`GetScript` Bloku skriptu by měla vrátit zatřiďovací tabulku představující stav aktuálního uzlu. Zatřiďovací tabulky musí obsahovat jenom jeden klíč `Result` a hodnota musí být typu `String`. Není potřeba nic vrátit. DSC nic se neděje s výstup tento blok skriptu.

`TestScript` Bloku skriptu měli zjistit, pokud má být změněn na aktuální uzel. Měla by vrátit `$true` Pokud je aktuální uzel. Měla by vrátit `$false` Pokud konfigurace uzlu je zastaralý a by měl být aktualizován `SetScript` bloku skriptu. `TestScript` Bloku skriptu je volána metodou DSC.

`SetScript` Bloku skriptu by měl změnit uzlu. Je volána metodou DSC, pokud `TestScript` blokovat vrátit `$false`.

Pokud budete muset použít proměnné z vaší konfigurační skript v `GetScript`, `TestScript`, nebo `SetScript` bloky skriptu, použijte `$using:` oboru (dole najdete příklad).


## <a name="syntax"></a>Syntaxe

```
Script [string] #ResourceName
{
    GetScript = [string]
    SetScript = [string]
    TestScript = [string]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   | 
|---|---| 
| GetScript| Poskytuje blok skriptu prostředí Windows PowerShell, který je spuštěn při vyvolání [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx) rutiny. Tento blok musí vracet zatřiďovací tabulku. Zatřiďovací tabulky musí obsahovat jenom jeden klíč **výsledek** a hodnota musí být typu **řetězec**.| 
| SetScript| Poskytuje blok skriptu prostředí Windows PowerShell. Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny **TestScript** bloku spustí první. Pokud **TestScript** blokovat vrátí **$false**, **SetScript** bloku se spustí. Pokud **TestScript** blokovat vrátí **$true**, **SetScript** bloku se nespustí.| 
| TestScript| Poskytuje blok skriptu prostředí Windows PowerShell. Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) spuštění rutiny, tento blok. Vrátí-li **$false**, spustí SetScript bloku. Vrátí-li **$true**, SetScript bloku se nespustí. **TestScript** bloku poběží i v případě vyvolání [Test DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) rutiny. V takovém případě však **SetScript** bloku nebude spouštět, bez ohledu na to, co hodnotu TestScript blokovat vrátí. **TestScript** bloku musí vracet hodnotu True, pokud skutečné konfigurace odpovídá aktuální konfigurace požadovaného stavu a na hodnotu False, pokud neodpovídá. (Aktuální konfigurace požadovaného stavu je poslední konfigurace použity na uzlu, který používá DSC.)| 
| přihlašovací údaje| Určuje pověření sloužící ke spuštění tohoto skriptu, pokud je třeba zadat pověření.| 
| dependsOn| Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba **ResourceName** a její typ je **ResourceType**, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.

## <a name="example-1"></a>Příklad 1
```powershell
Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script ScriptExample
    {
        SetScript = 
        { 
            $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
            $sw.WriteLine("Some sample string")
            $sw.Close()
        }
        TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
        GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }          
    }
}
```

## <a name="example-2"></a>Příklad 2
```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Script UpdateConfigurationVersion
    {
        GetScript = { 
            $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
            return @{ 'Result' = "$currentVersion" }
        }          
        TestScript = { 
            $state = $GetScript
            if( $state['Result'] -eq $using:version )
            {
                Write-Verbose -Message ('{0} -eq {1}' -f $state['Result'],$using:version)
                return $true
            }
            Write-Verbose -Message ('Version up-to-date: {0}' -f $using:version)
            return $false
        }
        SetScript = { 
            $using:version | Set-Content -Path (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
        }
    }
}
```

Tento prostředek je zapisování konfigurace do textového souboru. Tato verze je dostupná v klientském počítači, ale není na všech uzlech, tak musí být předán ke každému `Script` blocích skriptu prostředku v prostředí PowerShell na `using` oboru. Při generování uzlu MOF souboru, hodnota `$version` proměnnou je pro čtení z textového souboru v klientském počítači. Nahradí DSC `$using:version` proměnné v každý skript blokovat s hodnotou `$version` proměnné.


---
ms.date: 08/24/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Script
ms.openlocfilehash: ef84239820a44aab2a028f7f0fe17653a851b72e
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048169"
---
# <a name="dsc-script-resource"></a>Prostředek DSC Script

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.x

**Skript** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro spuštění bloky skriptu prostředí Windows PowerShell na cílové uzly. **Skript** prostředků používá `GetScript`, `SetScript`, a `TestScript` vlastnosti, které obsahují bloky skriptu definujete k provedení odpovídající DSC stavu operace.

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

> [!NOTE]
> `GetScript`, `TestScript`, A `SetScript` bloky jsou uloženy jako řetězce.

## <a name="properties"></a>Properties

|Vlastnost|Popis|
|--------|-----------|
|GetScript|Blok skriptu, který vrací aktuální stav tohoto uzlu.|
|SetScript|Blok skriptu, který používá DSC pro vynucování dodržování předpisů, pokud uzel není v požadovaném stavu.|
|TestScript|Blok skriptu, který určuje, zda je uzel v požadovaném stavu.|
|Přihlašovací údaje| Určuje přihlašovací údaje používat pro spouštění tohoto skriptu, pokud se vyžadují přihlašovací údaje.|
|DependsOn| Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.

### <a name="getscript"></a>GetScript

DSC nepoužívá výstup z `GetScript`. [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration) spustí rutinu `GetScript` načíst aktuální stav uzlu. Návratová hodnota není zapotřebí ve směru z `GetScript`. Pokud zadáte návratovou hodnotu, musí být `hashtable` obsahující **výsledek** klíč, jehož hodnota je `String`.

### <a name="testscript"></a>TestScript

`TestScript` Provádí DSC k určení, zda `SetScript` by se měl spustit. Pokud `TestScript` vrátí `$false`, provede DSC `SetScript` Chcete-li převést uzel zpět do požadovaného stavu. Musí vrátit `boolean` hodnotu. Výsledkem `$true` označuje, zda je uzel kompatibilní a `SetScript` by neměla provést.

[Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) spustí rutinu `TestScript` načíst dodržování předpisů uzly s **skript** prostředky. V takovém případě však `SetScript` nespustí, bez ohledu na to, co `TestScript` blokovat vrátí.

> [!NOTE]
> Veškerý výstup z vaší `TestScript` je součástí jeho návratovou hodnotu. Prostředí PowerShell interpretuje nepotlačená výstup jako nenulová, což znamená, že vaše `TestScript` vrátí `$true` bez ohledu na stav vašeho uzlu.
> Výsledkem nepředvídatelné výsledky, počet falešně pozitivních výsledků a způsobí, že potíže při odstraňování problémů.

### <a name="setscript"></a>SetScript

`SetScript` Upraví uzel, který má enfore požadovaného stavu. Je volána metodou DSC, pokud `TestScript` skript vrátí bloku `$false`. `SetScript` By měl mít žádnou návratovou hodnotu.

## <a name="examples"></a>Příklady

### <a name="example-1-write-sample-text-using-a-script-resource"></a>Příklad 1: Zapsat text v ukázce pomocí skriptu prostředků

V tomto příkladu ověřuje existenci `C:\TempFolder\TestFile.txt` na každém uzlu. Pokud neexistuje, vytvoří pomocí `SetScript`. `GetScript` Vrátí obsah souboru a jeho návratovou hodnotu není používán.

```powershell
Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script ScriptExample
        {
            SetScript = {
                $sw = New-Object System.IO.StreamWriter("C:\TempFolder\TestFile.txt")
                $sw.WriteLine("Some sample string")
                $sw.Close()
            }
            TestScript = { Test-Path "C:\TempFolder\TestFile.txt" }
            GetScript = { @{ Result = (Get-Content C:\TempFolder\TestFile.txt) } }
        }
    }
}
```

### <a name="example-2-compare-version-information-using-a-script-resource"></a>Příklad 2: Porovnejte informace o verzi použitím skriptu prostředků

Tento příklad načte *kompatibilní* informace o verzi z textového souboru na vývojovém počítači a uloží jej do `$version` proměnné. Při generování souboru MOF uzlu DSC nahradí `$using:version` blokovat proměnné do každého skriptu s hodnotou `$version` proměnné. Během provádění *kompatibilní* verze je uložený v textovém souboru na každém uzlu a porovnání a aktualizovat na další spuštění.

```powershell
$version = Get-Content 'version.txt'

Configuration ScriptTest
{
    Import-DscResource –ModuleName 'PSDesiredStateConfiguration'

    Node localhost
    {
        Script UpdateConfigurationVersion
        {
            GetScript = {
                $currentVersion = Get-Content (Join-Path -Path $env:SYSTEMDRIVE -ChildPath 'version.txt')
                return @{ 'Result' = "$currentVersion" }
            }
            TestScript = {
                # Create and invoke a scriptblock using the $GetScript automatic variable, which contains a string representation of the GetScript.
                $state = [scriptblock]::Create($GetScript).Invoke()

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
}
```
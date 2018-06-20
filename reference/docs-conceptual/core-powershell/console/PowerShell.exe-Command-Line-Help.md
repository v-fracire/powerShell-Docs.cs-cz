---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Nápověda k příkazovém řádku programu PowerShell.exe
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 60b6a7e310821a4092b0972b7abbdae0e2d5f738
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952575"
---
# <a name="powershellexe-command-line-help"></a>Nápověda příkazového řádku PowerShell.exe

Můžete použít PowerShell.exe pro spuštění relace prostředí PowerShell z příkazového řádku jiné nástroje, jako je například Cmd.exe, nebo použijte na příkazovém řádku prostředí PowerShell se nová relace. Chcete-li přizpůsobit relace použití parametrů.

## <a name="syntax"></a>Syntaxe

```syntax
PowerShell[.exe]
       [-Command { - | <script-block> [-args <arg-array>]
                     | <string> [<CommandParameters>] } ]
       [-EncodedCommand <Base64EncodedCommand>]
       [-ExecutionPolicy <ExecutionPolicy>]
       [-File <FilePath> [<Args>]]
       [-InputFormat {Text | XML}]
       [-Mta]
       [-NoExit]
       [-NoLogo]
       [-NonInteractive]
       [-NoProfile]
       [-OutputFormat {Text | XML}]
       [-PSConsoleFile <FilePath> | -Version <PowerShell version>]
       [-Sta]
       [-WindowStyle <style>]

PowerShell[.exe] -Help | -? | /?
```

## <a name="parameters"></a>Parameters

### <a name="-encodedcommand-base64encodedcommand"></a>-EncodedCommand <Base64EncodedCommand>

Přijme řetězec s kódováním base-64 verze příkazu. Tento parametr použijte odeslat příkazy prostředí PowerShell, které vyžadují uvozovek komplexní nebo složené závorky.

### <a name="-executionpolicy-executionpolicy"></a>-ExecutionPolicy <ExecutionPolicy>

Nastaví výchozí zásadu spouštění pro aktuální relaci a uloží ho do $env: PSExecutionPolicyPreference proměnné prostředí. Tento parametr nezmění zásady spouštění prostředí PowerShell, který je nastavený v registru. Informace o zásady spouštění prostředí PowerShell, včetně seznamu platné hodnoty, najdete v článku [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

### <a name="-file-filepath-parameters"></a>-Soubor <FilePath> \[ <Parameters>]

Spustí zadaný skript v oboru místní ("tečkou Source"), tak, aby funkce a proměnné, které vytvoří skript jsou k dispozici v aktuální relaci. Zadejte cestu souboru skriptu a parametry. **Soubor** musí být poslední parametr v příkazu, protože všechny znaky zadali po **souboru** název parametru se interpretují jako cestu souboru skriptu, za nímž následuje parametry skriptu a jejich hodnoty.

Můžete zahrnout parametry skriptu a parametr hodnoty hodnotu **souboru** parametr. Příklad: `-File .\Get-Script.ps1 -Domain Central` Všimněte si, že se předávají parametry předané do skriptu jako literál řetězce (po interpretace aktuální prostředí).
Například pokud jste v cmd.exe a chcete předat hodnot proměnných prostředí, je by použít syntaxi cmd.exe: `powershell -File .\test.ps1 -Sample %windir%` Pokud byste chtěli použít syntaxe Powershellu, pak v tomto příkladu by váš skript přijímat literálové "$env: windir" a není hodnota této proměnné prostředí: `powershell -File .\test.ps1 -Sample $env:windir`

Obvykle přepínač parametry skriptu jsou buď zahrnuty nebo tento parametr vynechán. Například následující příkaz používá **všechny** parametr Get-Script.ps1 souboru skriptu: `-File .\Get-Script.ps1 -All`

### <a name="-inputformat-text--xml"></a>\-InputFormat {Text | XML}

Popisuje formát data odeslaná do prostředí PowerShell. Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaných CLIXML format).

### <a name="-mta"></a>-Mta

Spustí se prostředí PowerShell pomocí Vícevláknová typu apartment. Tento parametr je zavedená v prostředí PowerShell 3.0. Single-threaded apartment (STA) v prostředí PowerShell 3.0, je výchozí. Vícevláknové apartment (MTA) v prostředí PowerShell 2.0, je výchozí.

### <a name="-noexit"></a>-NoExit

Po spuštění příkazů neexistuje.

### <a name="-nologo"></a>-NoLogo

Skryje Banner informující o autorských právech při spuštění.

### <a name="-noninteractive"></a>-Neinteraktivní

Nepředstavuje interaktivní výzvu uživateli.

### <a name="-noprofile"></a>-NoProfile

Nenačte profilem prostředí PowerShell.

### <a name="-outputformat-text--xml"></a>-OutputFormat {Text | XML}

Určuje způsob formátování výstupu z prostředí PowerShell. Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaných CLIXML format).

### <a name="-psconsolefile-filepath"></a>-PSConsoleFile <FilePath>

Zavede zadaný soubor konzoly prostředí PowerShell. Zadejte cestu a název souboru konzoly. Chcete-li vytvořit soubor konzoly, použijte [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) rutiny v prostředí PowerShell.

### <a name="-sta"></a>-Sta

Spustí single-threaded apartment pomocí prostředí PowerShell. Single-threaded apartment (STA) v prostředí PowerShell 3.0, je výchozí. Vícevláknové apartment (MTA) v prostředí PowerShell 2.0, je výchozí.

### <a name="-version-powershell-version"></a>-Version <PowerShell Version>

Spustí zadaný verzi prostředí PowerShell. V systému musí nainstalovat verzi, která zadáte. Pokud je v počítači nainstalováno prostředí PowerShell 3.0, platné hodnoty jsou "2.0" a "3.0". Výchozí hodnota je "3.0".

Pokud není nainstalováno prostředí PowerShell 3.0, je jedinou platnou hodnotou "2.0". Další hodnoty jsou ignorovány.

Další informace najdete v tématu "[instalace prostředí Windows PowerShell](../../setup/installing-windows-powershell.md)".

### <a name="-windowstyle-window-style"></a>-Styl_okna <Window style>

Nastavuje styl okna pro relaci. Platné hodnoty jsou normální, Minimized, Maximized a Hidden.

### <a name="-command"></a>– Příkaz

Provede zadaných příkazů (a žádné parametry) jako kdyby byly zadány na příkazovém řádku prostředí PowerShell a potom ukončí, pokud je zadaný parametr NoExit.
V podstatě jakýkoli text po `-Command` se odešle jako jednoho příkazového řádku prostředí PowerShell (to se liší od jak `-File` zpracovává parametry odeslaných do skriptu).

Hodnota příkazu může být "-", řetězec. nebo blok skriptu. Pokud je hodnota příkazu "-", ze standardní vstupní jsou přečteny text příkazu.

Bloky Script musí být uzavřena do složených závorek ({}). Blok skriptu můžete zadat, pouze pokud spuštěn PowerShell.exe v prostředí PowerShell. Výsledky skriptu se vrátí do nadřazené prostředí jako deserializovat objekty jazyka XML, ne živé objekty.

Pokud je hodnota příkazu řetězec, **příkaz** musí být poslední parametr v příkazu, protože žádné znaky zadali po příkazu se interpretují jako argumenty příkazu.

Zápis řetězec, který spouští příkaz prostředí PowerShell, použijte formát:

```powershell
"& {<command>}"
```

kde uvozovky označuje řetězec a invoke operátor (&) způsobí, že příkaz má být proveden.

### <a name="-help---"></a>-Help,-?, /?

Zobrazí tuto zprávu. Pokud jsou zadáním příkazu PowerShell.exe v prostředí PowerShell, předřazení parametry příkazu pomlčku (-), není dopředné lomítko (/). Můžete buď pomlčku nebo lomítkem v Cmd.exe.

> [!NOTE]
> Poznámka k řešení potíží: V prostředí PowerShell 2.0, od verze LastExitCode 0xc0000142 některé programy v prostředí Windows PowerShell konzoly selže.

## <a name="examples"></a>PŘÍKLADY

```powershell
# Create a new PowerShell session and load a saved console file
PowerShell -PSConsoleFile sqlsnapin.psc1

# Create a new PowerShell V2 session with text input, XML output, and no logo
PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

# Execute a PowerShell Command in a session
PowerShell -Command "Get-EventLog -LogName security"

# Run a script block in a session
PowerShell -Command {Get-EventLog -LogName security}

# An alternate way to run a command in a new session
PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```
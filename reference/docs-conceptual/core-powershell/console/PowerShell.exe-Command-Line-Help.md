---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Nápověda k příkazovém řádku programu PowerShell.exe
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 0a11ebb11d29adf5853c232b3aa10bc72f92bf0c
ms.sourcegitcommit: 03c7672ee72698fe88a73e99702ceaadf87e702f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/15/2018
ms.locfileid: "51691826"
---
# <a name="powershellexe-command-line-help"></a>Nápověda k příkazovému řádku PowerShell.exe

Můžete použít PowerShell.exe pro spuštění relace Powershellu z příkazového řádku jiný nástroj, jako je například Cmd.exe, nebo pomocí příkazového řádku Powershellu a spusťte novou relaci. Pomocí parametrů můžete přizpůsobit relace.

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

Přijímá verze řetězce s kódováním base-64 příkaz. Tento parametr použijte k odeslání příkazů Powershellu, které vyžadují komplexní uvozovek nebo složených závorek.

### <a name="-executionpolicy-executionpolicy"></a>-ExecutionPolicy <ExecutionPolicy>

Nastaví výchozí zásadu spouštění pro aktuální relaci a uloží ji $env: PSExecutionPolicyPreference proměnné prostředí. Tento parametr nedojde ke změně zásady spouštění prostředí PowerShell, který je nastaven v registru. Informace o zásady spouštění prostředí PowerShell, včetně seznamu platných hodnot najdete v části [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

### <a name="-file-filepath-parameters"></a>-Soubor <FilePath> \[ <Parameters>]

Spustí zadaný skript v místním oboru ("dot opensourcového vizualizačního"), tak, že funkce a proměnné, které skript vytvoří jsou k dispozici v aktuální relaci. Zadejte cestu k souboru skriptu a parametry. **Soubor** musí být poslední parametr v příkazu. Všechny hodnoty zadané po **– soubor** parametr je interpretován jako skript cesta k souboru a parametry předány do skriptu.

Parametry předané do skriptu jsou předány jako literál řetězce po vyhodnocení aktuálního prostředí. Například pokud jsou v cmd.exe a chcete k předání hodnot proměnných prostředí, můžete využít cmd.exe syntaxe: `powershell.exe -File .\test.ps1 -TestParam %windir%`

Naproti tomu systémem `powershell.exe -File .\test.ps1 -TestParam $env:windir` ve výsledcích cmd.exe ve skriptu, který přijímá řetězcový literál `$env:windir` protože nemá žádný speciální význam aktuální prostředí cmd.exe.
`$env:windir` Styl odkaz na proměnnou prostředí _můžete_ použít uvnitř `-Command` parametr, vzhledem k tomu, že se bude interpretovat jako kód Powershellu.

### <a name="-inputformat-text--xml"></a>\-InputFormat {Text | XML}

Popisuje Formát odesílání dat do prostředí PowerShell. Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaný formát je CLIXML).

### <a name="-mta"></a>-Mta

Spuštění Powershellu pomocí vícevláknového objektu apartment. Tento parametr se používá v prostředí PowerShell 3.0. Jednovláknový apartment (STA) v prostředí PowerShell 3.0, je výchozí nastavení. Vícevláknového objektu apartment (MTA) v prostředí PowerShell 2.0 je výchozí nastavení.

### <a name="-noexit"></a>-NoExit

Nelze ukončit po spuštění po spuštění příkazů.

### <a name="-nologo"></a>-NoLogo

Skryje o autorských právech nápisu při spuštění.

### <a name="-noninteractive"></a>-Neinteraktivní

Není k dispozici interaktivní výzvu uživateli.

### <a name="-noprofile"></a>-NoProfile

Nelze načíst profil prostředí PowerShell.

### <a name="-outputformat-text--xml"></a>-OutputFormat {Text | XML}

Určuje, jak je formátovaný výstup z Powershellu. Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaný formát je CLIXML).

### <a name="-psconsolefile-filepath"></a>-PSConsoleFile <FilePath>

Zavede zadaný soubor konzoly Powershellu. Zadejte cestu a název souboru konzoly. Chcete-li vytvořit soubor konzoly, použijte [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) rutiny v prostředí PowerShell.

### <a name="-sta"></a>-Sta

Spuštění Powershellu pomocí jednovláknový apartment. Jednovláknový apartment (STA) v prostředí PowerShell 3.0, je výchozí nastavení. Vícevláknového objektu apartment (MTA) v prostředí PowerShell 2.0 je výchozí nastavení.

### <a name="-version-powershell-version"></a>-Version <PowerShell Version>

Spustí určenou verzi prostředí PowerShell. V systému musí být nainstalovaná verze, který zadáte. Pokud prostředí PowerShell 3.0 je nainstalována v počítači, platné hodnoty jsou "2.0" a "3.0". Výchozí hodnota je "3.0".

Pokud není nainstalovaný PowerShell 3.0, jediná platná hodnota je "2.0". Další hodnoty jsou ignorovány.

Další informace najdete v tématu [instalace prostředí Windows PowerShell](../../setup/installing-windows-powershell.md).

### <a name="-windowstyle-window-style"></a>-WindowStyle <Window style>

Nastaví styl okna pro relaci. Platné hodnoty jsou Normal, Minimized, Maximized a skryté.

### <a name="-command"></a>-– Příkaz

Provede zadané příkazy (s žádné parametry), jakoby byly zadány v příkazovém řádku prostředí PowerShell.
Po spuštění, prostředí PowerShell ukončí, pokud **NoExit** je zadán parametr.
Žádný text po `-Command` se odešle jako jeden příkazový řádek powershellu.
Tím se liší od stlaní `-File` zpracovává parametry předány skriptu.

Hodnota `-Command` může být "-", řetězec nebo blok skriptu.
Výsledky příkazu se vrátí do nadřazené prostředí jako deserializovaný objekty jazyka XML, ne živé objekty.

Pokud hodnota `-Command` je "-", text příkazu je pro čtení ze standardního vstupu.

Pokud hodnota `-Command` je řetězec, **příkaz** _musí_ být poslední parametr zadán, protože žádné znaky zadali po příkazu jsou interpretovány jako argumenty příkazu.

**Příkaz** parametr lze zadat pouze blok skriptu pro spuštění při poznáte hodnotu předanou `-Command` jako typ vlastnost ScriptBlock.
Toto je _pouze_ možné při spuštění PowerShell.exe z jiného hostitele prostředí PowerShell.
Hostování ScriptBlock typu mohou být obsaženy v existujícím proměnné, vrácený z výrazu nebo analyzovaný pomocí prostředí PowerShell jako blok skriptu literálů ve složených závorkách `{}`, před předáním PowerShell.exe.

Na cmd.exe, není i bloku skriptu (nebo ScriptBlock typu), takže hodnota předaná **příkaz** bude _vždy_ bude řetězec.
Můžete napsat jenom blok skriptu do řetězce, ale místo prováděný se budou chovat přesně jako by jste ji zadali typické řádku prostředí PowerShell, tisk obsahu skript blokování zpět vám.

Předán řetězec `-Command` stále se spustí jako PowerShell, takže složených závorek bloku skriptu se často nevyžadují na prvním místě při spuštění z cmd.exe.
K provedení bloku skriptu vložené definované uvnitř řetězce, [operátor volání](/powershell/module/microsoft.powershell.core/about/about_operators#call-operator-) `&` lze použít:

```console
"& {<command>}"
```

### <a name="-help---"></a>-Help,-?, /?

Ukazuje syntaxi powershell.exe. Pokud se zadáním příkazu PowerShell.exe v prostředí PowerShell, předřaďte parametry příkazu s pomlčkou (-), ne lomítkem (/). Můžete v Cmd.exe pomlčkou nebo lomítkem.

> [!NOTE]
> Poznámka k řešení potíží: V prostředí PowerShell 2.0, počínaje některé programy ve Windows Powershellu, nelze LastExitCode 0xc0000142.

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

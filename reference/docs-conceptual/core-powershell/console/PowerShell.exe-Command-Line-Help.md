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
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="a3834-103">Nápověda příkazového řádku PowerShell.exe</span><span class="sxs-lookup"><span data-stu-id="a3834-103">PowerShell.exe Command-Line Help</span></span>

<span data-ttu-id="a3834-104">Můžete použít PowerShell.exe pro spuštění relace prostředí PowerShell z příkazového řádku jiné nástroje, jako je například Cmd.exe, nebo použijte na příkazovém řádku prostředí PowerShell se nová relace.</span><span class="sxs-lookup"><span data-stu-id="a3834-104">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="a3834-105">Chcete-li přizpůsobit relace použití parametrů.</span><span class="sxs-lookup"><span data-stu-id="a3834-105">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="a3834-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a3834-106">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="a3834-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="a3834-107">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="a3834-108">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="a3834-108">-EncodedCommand <Base64EncodedCommand></span></span>

<span data-ttu-id="a3834-109">Přijme řetězec s kódováním base-64 verze příkazu.</span><span class="sxs-lookup"><span data-stu-id="a3834-109">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="a3834-110">Tento parametr použijte odeslat příkazy prostředí PowerShell, které vyžadují uvozovek komplexní nebo složené závorky.</span><span class="sxs-lookup"><span data-stu-id="a3834-110">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="a3834-111">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="a3834-111">-ExecutionPolicy <ExecutionPolicy></span></span>

<span data-ttu-id="a3834-112">Nastaví výchozí zásadu spouštění pro aktuální relaci a uloží ho do $env: PSExecutionPolicyPreference proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="a3834-112">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="a3834-113">Tento parametr nezmění zásady spouštění prostředí PowerShell, který je nastavený v registru.</span><span class="sxs-lookup"><span data-stu-id="a3834-113">This parameter does not change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="a3834-114">Informace o zásady spouštění prostředí PowerShell, včetně seznamu platné hodnoty, najdete v článku [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="a3834-114">For information about PowerShell execution policies, including a list of valid values, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="a3834-115">-Soubor <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="a3834-115">-File <FilePath> \[<Parameters>]</span></span>

<span data-ttu-id="a3834-116">Spustí zadaný skript v oboru místní ("tečkou Source"), tak, aby funkce a proměnné, které vytvoří skript jsou k dispozici v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="a3834-116">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="a3834-117">Zadejte cestu souboru skriptu a parametry.</span><span class="sxs-lookup"><span data-stu-id="a3834-117">Enter the script file path and any parameters.</span></span> <span data-ttu-id="a3834-118">**Soubor** musí být poslední parametr v příkazu, protože všechny znaky zadali po **souboru** název parametru se interpretují jako cestu souboru skriptu, za nímž následuje parametry skriptu a jejich hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a3834-118">**File** must be the last parameter in the command, because all characters typed after the **File** parameter name are interpreted as the script file path followed by the script parameters and their values.</span></span>

<span data-ttu-id="a3834-119">Můžete zahrnout parametry skriptu a parametr hodnoty hodnotu **souboru** parametr.</span><span class="sxs-lookup"><span data-stu-id="a3834-119">You can include the parameters of a script, and parameter values, in the value of the **File** parameter.</span></span> <span data-ttu-id="a3834-120">Příklad: `-File .\Get-Script.ps1 -Domain Central` Všimněte si, že se předávají parametry předané do skriptu jako literál řetězce (po interpretace aktuální prostředí).</span><span class="sxs-lookup"><span data-stu-id="a3834-120">For example: `-File .\Get-Script.ps1 -Domain Central` Note that parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span>
<span data-ttu-id="a3834-121">Například pokud jste v cmd.exe a chcete předat hodnot proměnných prostředí, je by použít syntaxi cmd.exe: `powershell -File .\test.ps1 -Sample %windir%` Pokud byste chtěli použít syntaxe Powershellu, pak v tomto příkladu by váš skript přijímat literálové "$env: windir" a není hodnota této proměnné prostředí: `powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="a3834-121">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` If you were to use PowerShell syntax, then in this example your script would receive the literal "$env:windir" and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

<span data-ttu-id="a3834-122">Obvykle přepínač parametry skriptu jsou buď zahrnuty nebo tento parametr vynechán.</span><span class="sxs-lookup"><span data-stu-id="a3834-122">Typically, the switch parameters of a script are either included or omitted.</span></span> <span data-ttu-id="a3834-123">Například následující příkaz používá **všechny** parametr Get-Script.ps1 souboru skriptu: `-File .\Get-Script.ps1 -All`</span><span class="sxs-lookup"><span data-stu-id="a3834-123">For example, the following command uses the **All** parameter of the Get-Script.ps1 script file: `-File .\Get-Script.ps1 -All`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="a3834-124">\-InputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="a3834-124">\-InputFormat {Text | XML}</span></span>

<span data-ttu-id="a3834-125">Popisuje formát data odeslaná do prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-125">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="a3834-126">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaných CLIXML format).</span><span class="sxs-lookup"><span data-stu-id="a3834-126">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="a3834-127">-Mta</span><span class="sxs-lookup"><span data-stu-id="a3834-127">-Mta</span></span>

<span data-ttu-id="a3834-128">Spustí se prostředí PowerShell pomocí Vícevláknová typu apartment.</span><span class="sxs-lookup"><span data-stu-id="a3834-128">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="a3834-129">Tento parametr je zavedená v prostředí PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="a3834-129">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="a3834-130">Single-threaded apartment (STA) v prostředí PowerShell 3.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="a3834-130">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="a3834-131">Vícevláknové apartment (MTA) v prostředí PowerShell 2.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="a3834-131">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="a3834-132">-NoExit</span><span class="sxs-lookup"><span data-stu-id="a3834-132">-NoExit</span></span>

<span data-ttu-id="a3834-133">Po spuštění příkazů neexistuje.</span><span class="sxs-lookup"><span data-stu-id="a3834-133">Does not exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="a3834-134">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="a3834-134">-NoLogo</span></span>

<span data-ttu-id="a3834-135">Skryje Banner informující o autorských právech při spuštění.</span><span class="sxs-lookup"><span data-stu-id="a3834-135">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="a3834-136">-Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="a3834-136">-NonInteractive</span></span>

<span data-ttu-id="a3834-137">Nepředstavuje interaktivní výzvu uživateli.</span><span class="sxs-lookup"><span data-stu-id="a3834-137">Does not present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="a3834-138">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="a3834-138">-NoProfile</span></span>

<span data-ttu-id="a3834-139">Nenačte profilem prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-139">Does not load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="a3834-140">-OutputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="a3834-140">-OutputFormat {Text | XML}</span></span>

<span data-ttu-id="a3834-141">Určuje způsob formátování výstupu z prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-141">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="a3834-142">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaných CLIXML format).</span><span class="sxs-lookup"><span data-stu-id="a3834-142">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="a3834-143">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="a3834-143">-PSConsoleFile <FilePath></span></span>

<span data-ttu-id="a3834-144">Zavede zadaný soubor konzoly prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-144">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="a3834-145">Zadejte cestu a název souboru konzoly.</span><span class="sxs-lookup"><span data-stu-id="a3834-145">Enter the path and name of the console file.</span></span> <span data-ttu-id="a3834-146">Chcete-li vytvořit soubor konzoly, použijte [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) rutiny v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-146">To create a console file, use the [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="a3834-147">-Sta</span><span class="sxs-lookup"><span data-stu-id="a3834-147">-Sta</span></span>

<span data-ttu-id="a3834-148">Spustí single-threaded apartment pomocí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-148">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="a3834-149">Single-threaded apartment (STA) v prostředí PowerShell 3.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="a3834-149">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="a3834-150">Vícevláknové apartment (MTA) v prostředí PowerShell 2.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="a3834-150">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="a3834-151">-Version <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="a3834-151">-Version <PowerShell Version></span></span>

<span data-ttu-id="a3834-152">Spustí zadaný verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-152">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="a3834-153">V systému musí nainstalovat verzi, která zadáte.</span><span class="sxs-lookup"><span data-stu-id="a3834-153">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="a3834-154">Pokud je v počítači nainstalováno prostředí PowerShell 3.0, platné hodnoty jsou "2.0" a "3.0".</span><span class="sxs-lookup"><span data-stu-id="a3834-154">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="a3834-155">Výchozí hodnota je "3.0".</span><span class="sxs-lookup"><span data-stu-id="a3834-155">The default value is "3.0".</span></span>

<span data-ttu-id="a3834-156">Pokud není nainstalováno prostředí PowerShell 3.0, je jedinou platnou hodnotou "2.0".</span><span class="sxs-lookup"><span data-stu-id="a3834-156">If PowerShell 3.0 is not installed, the only valid value is "2.0".</span></span> <span data-ttu-id="a3834-157">Další hodnoty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="a3834-157">Other values are ignored.</span></span>

<span data-ttu-id="a3834-158">Další informace najdete v tématu "[instalace prostředí Windows PowerShell](../../setup/installing-windows-powershell.md)".</span><span class="sxs-lookup"><span data-stu-id="a3834-158">For more information, see "[Installing Windows PowerShell](../../setup/installing-windows-powershell.md)".</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="a3834-159">-Styl_okna <Window style></span><span class="sxs-lookup"><span data-stu-id="a3834-159">-WindowStyle <Window style></span></span>

<span data-ttu-id="a3834-160">Nastavuje styl okna pro relaci.</span><span class="sxs-lookup"><span data-stu-id="a3834-160">Sets the window style for the session.</span></span> <span data-ttu-id="a3834-161">Platné hodnoty jsou normální, Minimized, Maximized a Hidden.</span><span class="sxs-lookup"><span data-stu-id="a3834-161">Valid values are Normal, Minimized, Maximized and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="a3834-162">– Příkaz</span><span class="sxs-lookup"><span data-stu-id="a3834-162">-Command</span></span>

<span data-ttu-id="a3834-163">Provede zadaných příkazů (a žádné parametry) jako kdyby byly zadány na příkazovém řádku prostředí PowerShell a potom ukončí, pokud je zadaný parametr NoExit.</span><span class="sxs-lookup"><span data-stu-id="a3834-163">Executes the specified commands (and any parameters) as though they were typed at the PowerShell command prompt, and then exits, unless the NoExit parameter is specified.</span></span>
<span data-ttu-id="a3834-164">V podstatě jakýkoli text po `-Command` se odešle jako jednoho příkazového řádku prostředí PowerShell (to se liší od jak `-File` zpracovává parametry odeslaných do skriptu).</span><span class="sxs-lookup"><span data-stu-id="a3834-164">Essentially, any text after `-Command` is sent as a single command line to PowerShell (this is different from how `-File` handles parameters sent to a script).</span></span>

<span data-ttu-id="a3834-165">Hodnota příkazu může být "-", řetězec.</span><span class="sxs-lookup"><span data-stu-id="a3834-165">The value of Command can be "-", a string.</span></span> <span data-ttu-id="a3834-166">nebo blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="a3834-166">or a script block.</span></span> <span data-ttu-id="a3834-167">Pokud je hodnota příkazu "-", ze standardní vstupní jsou přečteny text příkazu.</span><span class="sxs-lookup"><span data-stu-id="a3834-167">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="a3834-168">Bloky Script musí být uzavřena do složených závorek ({}).</span><span class="sxs-lookup"><span data-stu-id="a3834-168">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="a3834-169">Blok skriptu můžete zadat, pouze pokud spuštěn PowerShell.exe v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3834-169">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="a3834-170">Výsledky skriptu se vrátí do nadřazené prostředí jako deserializovat objekty jazyka XML, ne živé objekty.</span><span class="sxs-lookup"><span data-stu-id="a3834-170">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="a3834-171">Pokud je hodnota příkazu řetězec, **příkaz** musí být poslední parametr v příkazu, protože žádné znaky zadali po příkazu se interpretují jako argumenty příkazu.</span><span class="sxs-lookup"><span data-stu-id="a3834-171">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="a3834-172">Zápis řetězec, který spouští příkaz prostředí PowerShell, použijte formát:</span><span class="sxs-lookup"><span data-stu-id="a3834-172">To write a string that runs a PowerShell command, use the format:</span></span>

```powershell
"& {<command>}"
```

<span data-ttu-id="a3834-173">kde uvozovky označuje řetězec a invoke operátor (&) způsobí, že příkaz má být proveden.</span><span class="sxs-lookup"><span data-stu-id="a3834-173">where the quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="a3834-174">-Help,-?, /?</span><span class="sxs-lookup"><span data-stu-id="a3834-174">-Help, -?, /?</span></span>

<span data-ttu-id="a3834-175">Zobrazí tuto zprávu.</span><span class="sxs-lookup"><span data-stu-id="a3834-175">Shows this message.</span></span> <span data-ttu-id="a3834-176">Pokud jsou zadáním příkazu PowerShell.exe v prostředí PowerShell, předřazení parametry příkazu pomlčku (-), není dopředné lomítko (/).</span><span class="sxs-lookup"><span data-stu-id="a3834-176">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="a3834-177">Můžete buď pomlčku nebo lomítkem v Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="a3834-177">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="a3834-178">Poznámka k řešení potíží: V prostředí PowerShell 2.0, od verze LastExitCode 0xc0000142 některé programy v prostředí Windows PowerShell konzoly selže.</span><span class="sxs-lookup"><span data-stu-id="a3834-178">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="a3834-179">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="a3834-179">EXAMPLES</span></span>

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
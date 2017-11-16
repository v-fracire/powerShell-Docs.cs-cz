---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "PowerShell.exe nápovědu příkazového řádku"
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 262c21e44e509746314ed44d91bb3de16a4b854b
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="5db6b-103">Nápověda příkazového řádku PowerShell.exe</span><span class="sxs-lookup"><span data-stu-id="5db6b-103">PowerShell.exe Command-Line Help</span></span>
<span data-ttu-id="5db6b-104">relaci prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-104">a Windows PowerShell session.</span></span> <span data-ttu-id="5db6b-105">Můžete použít PowerShell.exe pro spuštění relace prostředí PowerShell z příkazového řádku jiné nástroje, jako je například Cmd.exe, nebo použijte na příkazovém řádku prostředí PowerShell se nová relace.</span><span class="sxs-lookup"><span data-stu-id="5db6b-105">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="5db6b-106">Chcete-li přizpůsobit relace použití parametrů.</span><span class="sxs-lookup"><span data-stu-id="5db6b-106">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="5db6b-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="5db6b-107">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="5db6b-108">Parameters</span><span class="sxs-lookup"><span data-stu-id="5db6b-108">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="5db6b-109">-EncodedCommand<Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="5db6b-109">-EncodedCommand <Base64EncodedCommand></span></span>
<span data-ttu-id="5db6b-110">Přijme řetězec s kódováním base-64 verze příkazu.</span><span class="sxs-lookup"><span data-stu-id="5db6b-110">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="5db6b-111">Tento parametr použijte odeslat příkazy prostředí PowerShell, které vyžadují uvozovek komplexní nebo složené závorky.</span><span class="sxs-lookup"><span data-stu-id="5db6b-111">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="5db6b-112">-ExecutionPolicy<ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="5db6b-112">-ExecutionPolicy <ExecutionPolicy></span></span>
<span data-ttu-id="5db6b-113">Nastaví výchozí zásadu spouštění pro aktuální relaci a uloží ho do $env: PSExecutionPolicyPreference proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="5db6b-113">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="5db6b-114">Tento parametr nezmění zásady spouštění prostředí PowerShell, který je nastavený v registru.</span><span class="sxs-lookup"><span data-stu-id="5db6b-114">This parameter does not change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="5db6b-115">Informace o zásady spouštění prostředí PowerShell, včetně seznamu platné hodnoty najdete v části about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170).</span><span class="sxs-lookup"><span data-stu-id="5db6b-115">For information about PowerShell execution policies, including a list of valid values, see about_Execution_Policies (http://go.microsoft.com/fwlink/?LinkID=135170).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="5db6b-116">-Soubor <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="5db6b-116">-File <FilePath> \[<Parameters>]</span></span>
<span data-ttu-id="5db6b-117">Spustí zadaný skript v oboru místní ("tečkou Source"), tak, aby funkce a proměnné, které vytvoří skript jsou k dispozici v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="5db6b-117">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="5db6b-118">Zadejte cestu souboru skriptu a parametry.</span><span class="sxs-lookup"><span data-stu-id="5db6b-118">Enter the script file path and any parameters.</span></span> <span data-ttu-id="5db6b-119">**Soubor** musí být poslední parametr v příkazu, protože všechny znaky zadali po **souboru** název parametru se interpretují jako cestu souboru skriptu, za nímž následuje parametry skriptu a jejich hodnoty.</span><span class="sxs-lookup"><span data-stu-id="5db6b-119">**File** must be the last parameter in the command, because all characters typed after the **File** parameter name are interpreted as the script file path followed by the script parameters and their values.</span></span>

<span data-ttu-id="5db6b-120">Můžete zahrnout parametry skriptu a parametr hodnoty hodnotu **souboru** parametr.</span><span class="sxs-lookup"><span data-stu-id="5db6b-120">You can include the parameters of a script, and parameter values, in the value of the **File** parameter.</span></span> <span data-ttu-id="5db6b-121">Příklad: `-File .\Get-Script.ps1 -Domain Central` Všimněte si, že se předávají parametry předané do skriptu jako literál řetězce (po interpretace aktuální prostředí).</span><span class="sxs-lookup"><span data-stu-id="5db6b-121">For example: `-File .\Get-Script.ps1 -Domain Central` Note that parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span>
<span data-ttu-id="5db6b-122">Například pokud jste v cmd.exe a chcete předat hodnot proměnných prostředí, je by použít syntaxi cmd.exe: `powershell -File .\test.ps1 -Sample %windir%` Pokud byste chtěli použít syntaxe Powershellu, pak v tomto příkladu by váš skript přijímat literálové "$env: windir" a není hodnota této proměnné prostředí:`powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="5db6b-122">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` If you were to use PowerShell syntax, then in this example your script would receive the literal "$env:windir" and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

<span data-ttu-id="5db6b-123">Obvykle přepínač parametry skriptu jsou buď zahrnuty nebo tento parametr vynechán.</span><span class="sxs-lookup"><span data-stu-id="5db6b-123">Typically, the switch parameters of a script are either included or omitted.</span></span> <span data-ttu-id="5db6b-124">Například následující příkaz používá **všechny** parametr Get-Script.ps1 souboru skriptu:`-File .\Get-Script.ps1 -All`</span><span class="sxs-lookup"><span data-stu-id="5db6b-124">For example, the following command uses the **All** parameter of the Get-Script.ps1 script file: `-File .\Get-Script.ps1 -All`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="5db6b-125">\-InputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="5db6b-125">\-InputFormat {Text | XML}</span></span>
<span data-ttu-id="5db6b-126">Popisuje formát data odeslaná do prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-126">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="5db6b-127">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaných CLIXML format).</span><span class="sxs-lookup"><span data-stu-id="5db6b-127">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="5db6b-128">-Mta</span><span class="sxs-lookup"><span data-stu-id="5db6b-128">-Mta</span></span>
<span data-ttu-id="5db6b-129">Spustí se prostředí PowerShell pomocí Vícevláknová typu apartment.</span><span class="sxs-lookup"><span data-stu-id="5db6b-129">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="5db6b-130">Tento parametr je zavedená v prostředí PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="5db6b-130">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="5db6b-131">Single-threaded apartment (STA) v prostředí PowerShell 3.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="5db6b-131">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="5db6b-132">Vícevláknové apartment (MTA) v prostředí PowerShell 2.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="5db6b-132">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="5db6b-133">-NoExit</span><span class="sxs-lookup"><span data-stu-id="5db6b-133">-NoExit</span></span>
<span data-ttu-id="5db6b-134">Po spuštění příkazů neexistuje.</span><span class="sxs-lookup"><span data-stu-id="5db6b-134">Does not exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="5db6b-135">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="5db6b-135">-NoLogo</span></span>
<span data-ttu-id="5db6b-136">Skryje Banner informující o autorských právech při spuštění.</span><span class="sxs-lookup"><span data-stu-id="5db6b-136">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="5db6b-137">-Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="5db6b-137">-NonInteractive</span></span>
<span data-ttu-id="5db6b-138">Nepředstavuje interaktivní výzvu uživateli.</span><span class="sxs-lookup"><span data-stu-id="5db6b-138">Does not present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="5db6b-139">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="5db6b-139">-NoProfile</span></span>
<span data-ttu-id="5db6b-140">Nenačte profilem prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-140">Does not load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="5db6b-141">-OutputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="5db6b-141">-OutputFormat {Text | XML}</span></span>
<span data-ttu-id="5db6b-142">Určuje způsob formátování výstupu z prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-142">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="5db6b-143">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaných CLIXML format).</span><span class="sxs-lookup"><span data-stu-id="5db6b-143">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="5db6b-144">-PSConsoleFile<FilePath></span><span class="sxs-lookup"><span data-stu-id="5db6b-144">-PSConsoleFile <FilePath></span></span>
<span data-ttu-id="5db6b-145">Zavede zadaný soubor konzoly prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-145">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="5db6b-146">Zadejte cestu a název souboru konzoly.</span><span class="sxs-lookup"><span data-stu-id="5db6b-146">Enter the path and name of the console file.</span></span> <span data-ttu-id="5db6b-147">Chcete-li vytvořit soubor konzoly, použijte [Export konzoly](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef) rutiny v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-147">To create a console file, use the [Export-Console](https://technet.microsoft.com/en-us/library/4bab1c02-9e61-4aaf-9957-11d1934ef4ef) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="5db6b-148">Sta –</span><span class="sxs-lookup"><span data-stu-id="5db6b-148">-Sta</span></span>
<span data-ttu-id="5db6b-149">Spustí single-threaded apartment pomocí prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-149">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="5db6b-150">Single-threaded apartment (STA) v prostředí PowerShell 3.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="5db6b-150">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="5db6b-151">Vícevláknové apartment (MTA) v prostředí PowerShell 2.0, je výchozí.</span><span class="sxs-lookup"><span data-stu-id="5db6b-151">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="5db6b-152">-Version<PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="5db6b-152">-Version <PowerShell Version></span></span>
<span data-ttu-id="5db6b-153">Spustí zadaný verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-153">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="5db6b-154">V systému musí nainstalovat verzi, která zadáte.</span><span class="sxs-lookup"><span data-stu-id="5db6b-154">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="5db6b-155">Pokud je v počítači nainstalováno prostředí PowerShell 3.0, platné hodnoty jsou "2.0" a "3.0".</span><span class="sxs-lookup"><span data-stu-id="5db6b-155">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="5db6b-156">Výchozí hodnota je "3.0".</span><span class="sxs-lookup"><span data-stu-id="5db6b-156">The default value is "3.0".</span></span>

<span data-ttu-id="5db6b-157">Pokud není nainstalováno prostředí PowerShell 3.0, je jedinou platnou hodnotou "2.0".</span><span class="sxs-lookup"><span data-stu-id="5db6b-157">If PowerShell 3.0 is not installed, the only valid value is "2.0".</span></span> <span data-ttu-id="5db6b-158">Další hodnoty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="5db6b-158">Other values are ignored.</span></span>

<span data-ttu-id="5db6b-159">Další informace najdete v tématu "Instalace prostředí PowerShell" v [Začínáme s prostředím PowerShell [staré MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd).</span><span class="sxs-lookup"><span data-stu-id="5db6b-159">For more information, see "Installing PowerShell" in the [Getting Started with PowerShell [OLD MSDN]](https://technet.microsoft.com/en-us/library/69555d95-b481-43e1-86e7-b46d68b3e2dd).</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="5db6b-160">-Styl_okna<Window style></span><span class="sxs-lookup"><span data-stu-id="5db6b-160">-WindowStyle <Window style></span></span>
<span data-ttu-id="5db6b-161">Nastavuje styl okna pro relaci.</span><span class="sxs-lookup"><span data-stu-id="5db6b-161">Sets the window style for the session.</span></span> <span data-ttu-id="5db6b-162">Platné hodnoty jsou normální, Minimized, Maximized a Hidden.</span><span class="sxs-lookup"><span data-stu-id="5db6b-162">Valid values are Normal, Minimized, Maximized and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="5db6b-163">– Příkaz</span><span class="sxs-lookup"><span data-stu-id="5db6b-163">-Command</span></span>
<span data-ttu-id="5db6b-164">Provede zadaných příkazů (a žádné parametry) jako kdyby byly zadány na příkazovém řádku prostředí PowerShell a potom ukončí, pokud je zadaný parametr NoExit.</span><span class="sxs-lookup"><span data-stu-id="5db6b-164">Executes the specified commands (and any parameters) as though they were typed at the PowerShell command prompt, and then exits, unless the NoExit parameter is specified.</span></span>
<span data-ttu-id="5db6b-165">V podstatě jakýkoli text po `-Command` se odešle jako jednoho příkazového řádku prostředí PowerShell (to se liší od jak `-File` zpracovává parametry odeslaných do skriptu).</span><span class="sxs-lookup"><span data-stu-id="5db6b-165">Essentially, any text after `-Command` is sent as a single command line to PowerShell (this is different from how `-File` handles parameters sent to a script).</span></span>

<span data-ttu-id="5db6b-166">Hodnota příkazu může být "-", řetězec.</span><span class="sxs-lookup"><span data-stu-id="5db6b-166">The value of Command can be "-", a string.</span></span> <span data-ttu-id="5db6b-167">nebo blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="5db6b-167">or a script block.</span></span> <span data-ttu-id="5db6b-168">Pokud je hodnota příkazu "-", ze standardní vstupní jsou přečteny text příkazu.</span><span class="sxs-lookup"><span data-stu-id="5db6b-168">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="5db6b-169">Bloky Script musí být uzavřena do složených závorek ({}).</span><span class="sxs-lookup"><span data-stu-id="5db6b-169">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="5db6b-170">Blok skriptu můžete zadat, pouze pokud spuštěn PowerShell.exe v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5db6b-170">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="5db6b-171">Výsledky skriptu se vrátí do nadřazené prostředí jako deserializovat objekty jazyka XML, ne živé objekty.</span><span class="sxs-lookup"><span data-stu-id="5db6b-171">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="5db6b-172">Pokud je hodnota příkazu řetězec, **příkaz** musí být poslední parametr v příkazu, protože žádné znaky zadali po příkazu se interpretují jako argumenty příkazu.</span><span class="sxs-lookup"><span data-stu-id="5db6b-172">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="5db6b-173">Zápis řetězec, který spouští příkaz prostředí PowerShell, použijte formát:</span><span class="sxs-lookup"><span data-stu-id="5db6b-173">To write a string that runs a PowerShell command, use the format:</span></span>

```
"& {<command>}"
```

<span data-ttu-id="5db6b-174">kde uvozovky označuje řetězec a invoke operátor (&) způsobí, že příkaz má být proveden.</span><span class="sxs-lookup"><span data-stu-id="5db6b-174">where the quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="5db6b-175">-Help,-?, /?</span><span class="sxs-lookup"><span data-stu-id="5db6b-175">-Help, -?, /?</span></span>
<span data-ttu-id="5db6b-176">Zobrazí tuto zprávu.</span><span class="sxs-lookup"><span data-stu-id="5db6b-176">Shows this message.</span></span> <span data-ttu-id="5db6b-177">Pokud jsou zadáním příkazu PowerShell.exe v prostředí PowerShell, předřazení parametry příkazu pomlčku (-), není dopředné lomítko (/).</span><span class="sxs-lookup"><span data-stu-id="5db6b-177">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="5db6b-178">Můžete buď pomlčku nebo lomítkem v Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="5db6b-178">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="5db6b-179">Poznámka k řešení potíží: V prostředí PowerShell 2.0, od verze LastExitCode 0xc0000142 některé programy v prostředí Windows PowerShell konzoly selže.</span><span class="sxs-lookup"><span data-stu-id="5db6b-179">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="5db6b-180">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="5db6b-180">EXAMPLES</span></span>

```
# Create a new PowerShell session and load a saved console file
PowerShell -PSConsoleFile sqlsnapin.psc1

# Create a new PowerShell V2 session with text input, XML output, and no logo
PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

# Execute a Powerhell Command in a session
PowerShell -Command "Get-EventLog -LogName security"

# Run a script block in a session
PowerShell -Command {Get-EventLog -LogName security}

# An alternate wayh to run a command in a new session
PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```


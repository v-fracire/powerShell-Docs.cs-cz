---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Nápověda k příkazovém řádku programu PowerShell.exe
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: c7f35511e876e8e5189d8a2b949555603d43f731
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133873"
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="724a4-103">Nápověda k příkazovému řádku PowerShell.exe</span><span class="sxs-lookup"><span data-stu-id="724a4-103">PowerShell.exe Command-Line Help</span></span>

<span data-ttu-id="724a4-104">Můžete použít PowerShell.exe pro spuštění relace Powershellu z příkazového řádku jiný nástroj, jako je například Cmd.exe, nebo pomocí příkazového řádku Powershellu a spusťte novou relaci.</span><span class="sxs-lookup"><span data-stu-id="724a4-104">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="724a4-105">Pomocí parametrů můžete přizpůsobit relace.</span><span class="sxs-lookup"><span data-stu-id="724a4-105">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="724a4-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="724a4-106">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="724a4-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="724a4-107">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="724a4-108">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="724a4-108">-EncodedCommand <Base64EncodedCommand></span></span>

<span data-ttu-id="724a4-109">Přijímá verze řetězce s kódováním base-64 příkaz.</span><span class="sxs-lookup"><span data-stu-id="724a4-109">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="724a4-110">Tento parametr použijte k odeslání příkazů Powershellu, které vyžadují komplexní uvozovek nebo složených závorek.</span><span class="sxs-lookup"><span data-stu-id="724a4-110">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="724a4-111">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="724a4-111">-ExecutionPolicy <ExecutionPolicy></span></span>

<span data-ttu-id="724a4-112">Nastaví výchozí zásadu spouštění pro aktuální relaci a uloží ji $env: PSExecutionPolicyPreference proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="724a4-112">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="724a4-113">Tento parametr nedojde ke změně zásady spouštění prostředí PowerShell, který je nastaven v registru.</span><span class="sxs-lookup"><span data-stu-id="724a4-113">This parameter doesn't change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="724a4-114">Informace o zásady spouštění prostředí PowerShell, včetně seznamu platných hodnot najdete v části [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="724a4-114">For information about PowerShell execution policies, including a list of valid values, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="724a4-115">-Soubor <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="724a4-115">-File <FilePath> \[<Parameters>]</span></span>

<span data-ttu-id="724a4-116">Spustí zadaný skript v místním oboru ("dot opensourcového vizualizačního"), tak, že funkce a proměnné, které skript vytvoří jsou k dispozici v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="724a4-116">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="724a4-117">Zadejte cestu k souboru skriptu a parametry.</span><span class="sxs-lookup"><span data-stu-id="724a4-117">Enter the script file path and any parameters.</span></span> <span data-ttu-id="724a4-118">**Soubor** musí být poslední parametr v příkazu.</span><span class="sxs-lookup"><span data-stu-id="724a4-118">**File** must be the last parameter in the command.</span></span> <span data-ttu-id="724a4-119">Všechny hodnoty zadané po **– soubor** parametr je interpretován jako skript cesta k souboru a parametry předány do skriptu.</span><span class="sxs-lookup"><span data-stu-id="724a4-119">All values typed after the **-File** parameter are interpreted as the script file path and parameters passed to that script.</span></span>

<span data-ttu-id="724a4-120">Parametry předané do skriptu jsou předány jako literál řetězce (po vyhodnocení aktuálního prostředí).</span><span class="sxs-lookup"><span data-stu-id="724a4-120">Parameters passed to the script are passed as literal strings (after interpretation by the current shell).</span></span> <span data-ttu-id="724a4-121">Například, pokud jsou v cmd.exe a chcete k předání hodnot proměnných prostředí, můžete využít cmd.exe syntaxe: `powershell -File .\test.ps1 -Sample %windir%` skript v tomto příkladu přijímá řetězcový literál `$env:windir` a nikoli hodnotu této proměnné prostředí: `powershell -File .\test.ps1 -Sample $env:windir`</span><span class="sxs-lookup"><span data-stu-id="724a4-121">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell -File .\test.ps1 -Sample %windir%` In this example, the script receives the literal string `$env:windir` and not the value of that environmental variable: `powershell -File .\test.ps1 -Sample $env:windir`</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="724a4-122">\-InputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="724a4-122">\-InputFormat {Text | XML}</span></span>

<span data-ttu-id="724a4-123">Popisuje Formát odesílání dat do prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="724a4-123">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="724a4-124">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaný formát je CLIXML).</span><span class="sxs-lookup"><span data-stu-id="724a4-124">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="724a4-125">-Mta</span><span class="sxs-lookup"><span data-stu-id="724a4-125">-Mta</span></span>

<span data-ttu-id="724a4-126">Spuštění Powershellu pomocí vícevláknového objektu apartment.</span><span class="sxs-lookup"><span data-stu-id="724a4-126">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="724a4-127">Tento parametr se používá v prostředí PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="724a4-127">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="724a4-128">Jednovláknový apartment (STA) v prostředí PowerShell 3.0, je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="724a4-128">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="724a4-129">Vícevláknového objektu apartment (MTA) v prostředí PowerShell 2.0 je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="724a4-129">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="724a4-130">-NoExit</span><span class="sxs-lookup"><span data-stu-id="724a4-130">-NoExit</span></span>

<span data-ttu-id="724a4-131">Nelze ukončit po spuštění po spuštění příkazů.</span><span class="sxs-lookup"><span data-stu-id="724a4-131">Doesn't exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="724a4-132">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="724a4-132">-NoLogo</span></span>

<span data-ttu-id="724a4-133">Skryje o autorských právech nápisu při spuštění.</span><span class="sxs-lookup"><span data-stu-id="724a4-133">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="724a4-134">-Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="724a4-134">-NonInteractive</span></span>

<span data-ttu-id="724a4-135">Není k dispozici interaktivní výzvu uživateli.</span><span class="sxs-lookup"><span data-stu-id="724a4-135">Doesn't present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="724a4-136">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="724a4-136">-NoProfile</span></span>

<span data-ttu-id="724a4-137">Nelze načíst profil prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="724a4-137">Doesn't load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="724a4-138">-OutputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="724a4-138">-OutputFormat {Text | XML}</span></span>

<span data-ttu-id="724a4-139">Určuje, jak je formátovaný výstup z Powershellu.</span><span class="sxs-lookup"><span data-stu-id="724a4-139">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="724a4-140">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaný formát je CLIXML).</span><span class="sxs-lookup"><span data-stu-id="724a4-140">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="724a4-141">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="724a4-141">-PSConsoleFile <FilePath></span></span>

<span data-ttu-id="724a4-142">Zavede zadaný soubor konzoly Powershellu.</span><span class="sxs-lookup"><span data-stu-id="724a4-142">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="724a4-143">Zadejte cestu a název souboru konzoly.</span><span class="sxs-lookup"><span data-stu-id="724a4-143">Enter the path and name of the console file.</span></span> <span data-ttu-id="724a4-144">Chcete-li vytvořit soubor konzoly, použijte [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) rutiny v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="724a4-144">To create a console file, use the [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="724a4-145">-Sta</span><span class="sxs-lookup"><span data-stu-id="724a4-145">-Sta</span></span>

<span data-ttu-id="724a4-146">Spuštění Powershellu pomocí jednovláknový apartment.</span><span class="sxs-lookup"><span data-stu-id="724a4-146">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="724a4-147">Jednovláknový apartment (STA) v prostředí PowerShell 3.0, je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="724a4-147">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="724a4-148">Vícevláknového objektu apartment (MTA) v prostředí PowerShell 2.0 je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="724a4-148">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="724a4-149">-Version <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="724a4-149">-Version <PowerShell Version></span></span>

<span data-ttu-id="724a4-150">Spustí určenou verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="724a4-150">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="724a4-151">V systému musí být nainstalovaná verze, který zadáte.</span><span class="sxs-lookup"><span data-stu-id="724a4-151">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="724a4-152">Pokud prostředí PowerShell 3.0 je nainstalována v počítači, platné hodnoty jsou "2.0" a "3.0".</span><span class="sxs-lookup"><span data-stu-id="724a4-152">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="724a4-153">Výchozí hodnota je "3.0".</span><span class="sxs-lookup"><span data-stu-id="724a4-153">The default value is "3.0".</span></span>

<span data-ttu-id="724a4-154">Pokud není nainstalovaný PowerShell 3.0, jediná platná hodnota je "2.0".</span><span class="sxs-lookup"><span data-stu-id="724a4-154">If PowerShell 3.0 isn't installed, the only valid value is "2.0".</span></span> <span data-ttu-id="724a4-155">Další hodnoty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="724a4-155">Other values are ignored.</span></span>

<span data-ttu-id="724a4-156">Další informace najdete v tématu [instalace prostředí Windows PowerShell](../../setup/installing-windows-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="724a4-156">For more information, see [Installing Windows PowerShell](../../setup/installing-windows-powershell.md).</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="724a4-157">-WindowStyle <Window style></span><span class="sxs-lookup"><span data-stu-id="724a4-157">-WindowStyle <Window style></span></span>

<span data-ttu-id="724a4-158">Nastaví styl okna pro relaci.</span><span class="sxs-lookup"><span data-stu-id="724a4-158">Sets the window style for the session.</span></span> <span data-ttu-id="724a4-159">Platné hodnoty jsou Normal, Minimized, Maximized a skryté.</span><span class="sxs-lookup"><span data-stu-id="724a4-159">Valid values are Normal, Minimized, Maximized, and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="724a4-160">-– Příkaz</span><span class="sxs-lookup"><span data-stu-id="724a4-160">-Command</span></span>

<span data-ttu-id="724a4-161">Provede zadané příkazy (s žádné parametry), jakoby byly zadány v příkazovém řádku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="724a4-161">Executes the specified commands (with any parameters) as though they were typed at the PowerShell command prompt.</span></span> <span data-ttu-id="724a4-162">Po spuštění, prostředí PowerShell ukončí, pokud `-NoExit` je zadán parametr.</span><span class="sxs-lookup"><span data-stu-id="724a4-162">After execution, PowerShell exits unless the `-NoExit` parameter is specified.</span></span>
<span data-ttu-id="724a4-163">Žádný text po `-Command` se odešle jako jeden příkazový řádek powershellu.</span><span class="sxs-lookup"><span data-stu-id="724a4-163">Any text after `-Command` is sent as a single command line to PowerShell.</span></span> <span data-ttu-id="724a4-164">Tím se liší od stlaní `-File` zpracovává parametry předány skriptu.</span><span class="sxs-lookup"><span data-stu-id="724a4-164">This is different from how `-File` handles parameters sent to a script.</span></span>

<span data-ttu-id="724a4-165">Hodnota příkazu může být "-", řetězec.</span><span class="sxs-lookup"><span data-stu-id="724a4-165">The value of Command can be "-", a string.</span></span> <span data-ttu-id="724a4-166">nebo blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="724a4-166">or a script block.</span></span> <span data-ttu-id="724a4-167">Pokud je hodnota příkazu "-", text příkazu je pro čtení ze standardního vstupu.</span><span class="sxs-lookup"><span data-stu-id="724a4-167">If the value of Command is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="724a4-168">Bloky skriptu musí být uzavřen ve složených závorkách ({}).</span><span class="sxs-lookup"><span data-stu-id="724a4-168">Script blocks must be enclosed in braces ({}).</span></span> <span data-ttu-id="724a4-169">Blok skriptu můžete zadat, pouze při spuštění PowerShell.exe v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="724a4-169">You can specify a script block only when running PowerShell.exe in PowerShell.</span></span> <span data-ttu-id="724a4-170">Výsledky skriptu se vrátí do nadřazené prostředí jako deserializovaný objekty jazyka XML, ne živé objekty.</span><span class="sxs-lookup"><span data-stu-id="724a4-170">The results of the script are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="724a4-171">Pokud je řetězec, hodnota příkazu **příkaz** musí být poslední parametr v příkazu, protože žádné znaky zadali po příkazu jsou interpretovány jako argumenty příkazu.</span><span class="sxs-lookup"><span data-stu-id="724a4-171">If the value of Command is a string, **Command** must be the last parameter in the command, because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="724a4-172">Pokud chcete zapsat řetězec, který se spustí příkaz prostředí PowerShell, použijte formát:</span><span class="sxs-lookup"><span data-stu-id="724a4-172">To write a string that runs a PowerShell command, use the format:</span></span>

```powershell
"& {<command>}"
```

<span data-ttu-id="724a4-173">Uvozovky značí řetězce a vyvolat – operátor (&) způsobí, že příkaz má být proveden.</span><span class="sxs-lookup"><span data-stu-id="724a4-173">The quotation marks indicate a string and the invoke operator (&) causes the command to be executed.</span></span>

### <a name="-help---"></a><span data-ttu-id="724a4-174">-Help,-?, /?</span><span class="sxs-lookup"><span data-stu-id="724a4-174">-Help, -?, /?</span></span>

<span data-ttu-id="724a4-175">Ukazuje syntaxi powershell.exe.</span><span class="sxs-lookup"><span data-stu-id="724a4-175">Shows the syntax of powershell.exe.</span></span> <span data-ttu-id="724a4-176">Pokud se zadáním příkazu PowerShell.exe v prostředí PowerShell, předřaďte parametry příkazu s pomlčkou (-), ne lomítkem (/).</span><span class="sxs-lookup"><span data-stu-id="724a4-176">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="724a4-177">Můžete v Cmd.exe pomlčkou nebo lomítkem.</span><span class="sxs-lookup"><span data-stu-id="724a4-177">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="724a4-178">Poznámka k řešení potíží: V prostředí PowerShell 2.0, počínaje některé programy ve Windows Powershellu, nelze LastExitCode 0xc0000142.</span><span class="sxs-lookup"><span data-stu-id="724a4-178">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="724a4-179">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="724a4-179">EXAMPLES</span></span>

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

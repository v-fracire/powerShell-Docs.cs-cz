---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Nápověda k příkazovém řádku programu PowerShell.exe
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
ms.openlocfilehash: 0a11ebb11d29adf5853c232b3aa10bc72f92bf0c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403701"
---
# <a name="powershellexe-command-line-help"></a><span data-ttu-id="4881f-103">Nápověda k příkazovému řádku PowerShell.exe</span><span class="sxs-lookup"><span data-stu-id="4881f-103">PowerShell.exe Command-Line Help</span></span>

<span data-ttu-id="4881f-104">Můžete použít PowerShell.exe pro spuštění relace Powershellu z příkazového řádku jiný nástroj, jako je například Cmd.exe, nebo pomocí příkazového řádku Powershellu a spusťte novou relaci.</span><span class="sxs-lookup"><span data-stu-id="4881f-104">You can use PowerShell.exe to start a PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the PowerShell command line to start a new session.</span></span> <span data-ttu-id="4881f-105">Pomocí parametrů můžete přizpůsobit relace.</span><span class="sxs-lookup"><span data-stu-id="4881f-105">Use the parameters to customize the session.</span></span>

## <a name="syntax"></a><span data-ttu-id="4881f-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4881f-106">Syntax</span></span>

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

## <a name="parameters"></a><span data-ttu-id="4881f-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="4881f-107">Parameters</span></span>

### <a name="-encodedcommand-base64encodedcommand"></a><span data-ttu-id="4881f-108">-EncodedCommand <Base64EncodedCommand></span><span class="sxs-lookup"><span data-stu-id="4881f-108">-EncodedCommand <Base64EncodedCommand></span></span>

<span data-ttu-id="4881f-109">Přijímá verze řetězce s kódováním base-64 příkaz.</span><span class="sxs-lookup"><span data-stu-id="4881f-109">Accepts a base-64-encoded string version of a command.</span></span> <span data-ttu-id="4881f-110">Tento parametr použijte k odeslání příkazů Powershellu, které vyžadují komplexní uvozovek nebo složených závorek.</span><span class="sxs-lookup"><span data-stu-id="4881f-110">Use this parameter to submit commands to PowerShell that require complex quotation marks or curly braces.</span></span>

### <a name="-executionpolicy-executionpolicy"></a><span data-ttu-id="4881f-111">-ExecutionPolicy <ExecutionPolicy></span><span class="sxs-lookup"><span data-stu-id="4881f-111">-ExecutionPolicy <ExecutionPolicy></span></span>

<span data-ttu-id="4881f-112">Nastaví výchozí zásadu spouštění pro aktuální relaci a uloží ji $env: PSExecutionPolicyPreference proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="4881f-112">Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable.</span></span> <span data-ttu-id="4881f-113">Tento parametr nedojde ke změně zásady spouštění prostředí PowerShell, který je nastaven v registru.</span><span class="sxs-lookup"><span data-stu-id="4881f-113">This parameter doesn't change the PowerShell execution policy that is set in the registry.</span></span> <span data-ttu-id="4881f-114">Informace o zásady spouštění prostředí PowerShell, včetně seznamu platných hodnot najdete v části [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="4881f-114">For information about PowerShell execution policies, including a list of valid values, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

### <a name="-file-filepath-parameters"></a><span data-ttu-id="4881f-115">-Soubor <FilePath> \[ <Parameters>]</span><span class="sxs-lookup"><span data-stu-id="4881f-115">-File <FilePath> \[<Parameters>]</span></span>

<span data-ttu-id="4881f-116">Spustí zadaný skript v místním oboru ("dot opensourcového vizualizačního"), tak, že funkce a proměnné, které skript vytvoří jsou k dispozici v aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="4881f-116">Runs the specified script in the local scope ("dot-sourced"), so that the functions and variables that the script creates are available in the current session.</span></span> <span data-ttu-id="4881f-117">Zadejte cestu k souboru skriptu a parametry.</span><span class="sxs-lookup"><span data-stu-id="4881f-117">Enter the script file path and any parameters.</span></span> <span data-ttu-id="4881f-118">**Soubor** musí být poslední parametr v příkazu.</span><span class="sxs-lookup"><span data-stu-id="4881f-118">**File** must be the last parameter in the command.</span></span> <span data-ttu-id="4881f-119">Všechny hodnoty zadané po **– soubor** parametr je interpretován jako skript cesta k souboru a parametry předány do skriptu.</span><span class="sxs-lookup"><span data-stu-id="4881f-119">All values typed after the **-File** parameter are interpreted as the script file path and parameters passed to that script.</span></span>

<span data-ttu-id="4881f-120">Parametry předané do skriptu jsou předány jako literál řetězce po vyhodnocení aktuálního prostředí.</span><span class="sxs-lookup"><span data-stu-id="4881f-120">Parameters passed to the script are passed as literal strings, after interpretation by the current shell.</span></span> <span data-ttu-id="4881f-121">Například pokud jsou v cmd.exe a chcete k předání hodnot proměnných prostředí, můžete využít cmd.exe syntaxe: `powershell.exe -File .\test.ps1 -TestParam %windir%`</span><span class="sxs-lookup"><span data-stu-id="4881f-121">For example, if you are in cmd.exe and want to pass an environment variable value, you would use the cmd.exe syntax: `powershell.exe -File .\test.ps1 -TestParam %windir%`</span></span>

<span data-ttu-id="4881f-122">Naproti tomu systémem `powershell.exe -File .\test.ps1 -TestParam $env:windir` ve výsledcích cmd.exe ve skriptu, který přijímá řetězcový literál `$env:windir` protože nemá žádný speciální význam aktuální prostředí cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="4881f-122">In contrast, running `powershell.exe -File .\test.ps1 -TestParam $env:windir` in cmd.exe results in the script receiving the literal string `$env:windir` because it has no special meaning to the current cmd.exe shell.</span></span>
<span data-ttu-id="4881f-123">`$env:windir` Styl odkaz na proměnnou prostředí _můžete_ použít uvnitř `-Command` parametr, vzhledem k tomu, že se bude interpretovat jako kód Powershellu.</span><span class="sxs-lookup"><span data-stu-id="4881f-123">The `$env:windir` style of environment variable reference _can_ be used inside a `-Command` parameter, since there it will be interpreted as PowerShell code.</span></span>

### <a name="-inputformat-text--xml"></a><span data-ttu-id="4881f-124">\-InputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="4881f-124">\-InputFormat {Text | XML}</span></span>

<span data-ttu-id="4881f-125">Popisuje Formát odesílání dat do prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4881f-125">Describes the format of data sent to PowerShell.</span></span> <span data-ttu-id="4881f-126">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaný formát je CLIXML).</span><span class="sxs-lookup"><span data-stu-id="4881f-126">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-mta"></a><span data-ttu-id="4881f-127">-Mta</span><span class="sxs-lookup"><span data-stu-id="4881f-127">-Mta</span></span>

<span data-ttu-id="4881f-128">Spuštění Powershellu pomocí vícevláknového objektu apartment.</span><span class="sxs-lookup"><span data-stu-id="4881f-128">Starts PowerShell using a multi-threaded apartment.</span></span> <span data-ttu-id="4881f-129">Tento parametr se používá v prostředí PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="4881f-129">This parameter is introduced in PowerShell 3.0.</span></span> <span data-ttu-id="4881f-130">Jednovláknový apartment (STA) v prostředí PowerShell 3.0, je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="4881f-130">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="4881f-131">Vícevláknového objektu apartment (MTA) v prostředí PowerShell 2.0 je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="4881f-131">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-noexit"></a><span data-ttu-id="4881f-132">-NoExit</span><span class="sxs-lookup"><span data-stu-id="4881f-132">-NoExit</span></span>

<span data-ttu-id="4881f-133">Nelze ukončit po spuštění po spuštění příkazů.</span><span class="sxs-lookup"><span data-stu-id="4881f-133">Doesn't exit after running startup commands.</span></span>

### <a name="-nologo"></a><span data-ttu-id="4881f-134">-NoLogo</span><span class="sxs-lookup"><span data-stu-id="4881f-134">-NoLogo</span></span>

<span data-ttu-id="4881f-135">Skryje o autorských právech nápisu při spuštění.</span><span class="sxs-lookup"><span data-stu-id="4881f-135">Hides the copyright banner at startup.</span></span>

### <a name="-noninteractive"></a><span data-ttu-id="4881f-136">-Neinteraktivní</span><span class="sxs-lookup"><span data-stu-id="4881f-136">-NonInteractive</span></span>

<span data-ttu-id="4881f-137">Není k dispozici interaktivní výzvu uživateli.</span><span class="sxs-lookup"><span data-stu-id="4881f-137">Doesn't present an interactive prompt to the user.</span></span>

### <a name="-noprofile"></a><span data-ttu-id="4881f-138">-NoProfile</span><span class="sxs-lookup"><span data-stu-id="4881f-138">-NoProfile</span></span>

<span data-ttu-id="4881f-139">Nelze načíst profil prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4881f-139">Doesn't load the PowerShell profile.</span></span>

### <a name="-outputformat-text--xml"></a><span data-ttu-id="4881f-140">-OutputFormat {Text | XML}</span><span class="sxs-lookup"><span data-stu-id="4881f-140">-OutputFormat {Text | XML}</span></span>

<span data-ttu-id="4881f-141">Určuje, jak je formátovaný výstup z Powershellu.</span><span class="sxs-lookup"><span data-stu-id="4881f-141">Determines how output from PowerShell is formatted.</span></span> <span data-ttu-id="4881f-142">Platné hodnoty jsou "Text" (textové řetězce) nebo "XML" (serializovaný formát je CLIXML).</span><span class="sxs-lookup"><span data-stu-id="4881f-142">Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).</span></span>

### <a name="-psconsolefile-filepath"></a><span data-ttu-id="4881f-143">-PSConsoleFile <FilePath></span><span class="sxs-lookup"><span data-stu-id="4881f-143">-PSConsoleFile <FilePath></span></span>

<span data-ttu-id="4881f-144">Zavede zadaný soubor konzoly Powershellu.</span><span class="sxs-lookup"><span data-stu-id="4881f-144">Loads the specified PowerShell console file.</span></span> <span data-ttu-id="4881f-145">Zadejte cestu a název souboru konzoly.</span><span class="sxs-lookup"><span data-stu-id="4881f-145">Enter the path and name of the console file.</span></span> <span data-ttu-id="4881f-146">Chcete-li vytvořit soubor konzoly, použijte [ `Export-Console` ](/powershell/module/Microsoft.PowerShell.Core/Export-Console) rutiny v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4881f-146">To create a console file, use the [`Export-Console`](/powershell/module/Microsoft.PowerShell.Core/Export-Console) cmdlet in PowerShell.</span></span>

### <a name="-sta"></a><span data-ttu-id="4881f-147">-Sta</span><span class="sxs-lookup"><span data-stu-id="4881f-147">-Sta</span></span>

<span data-ttu-id="4881f-148">Spuštění Powershellu pomocí jednovláknový apartment.</span><span class="sxs-lookup"><span data-stu-id="4881f-148">Starts PowerShell using a single-threaded apartment.</span></span> <span data-ttu-id="4881f-149">Jednovláknový apartment (STA) v prostředí PowerShell 3.0, je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="4881f-149">In PowerShell 3.0, single-threaded apartment (STA) is the default.</span></span> <span data-ttu-id="4881f-150">Vícevláknového objektu apartment (MTA) v prostředí PowerShell 2.0 je výchozí nastavení.</span><span class="sxs-lookup"><span data-stu-id="4881f-150">In PowerShell 2.0, multi-threaded apartment (MTA) is the default.</span></span>

### <a name="-version-powershell-version"></a><span data-ttu-id="4881f-151">-Version <PowerShell Version></span><span class="sxs-lookup"><span data-stu-id="4881f-151">-Version <PowerShell Version></span></span>

<span data-ttu-id="4881f-152">Spustí určenou verzi prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4881f-152">Starts the specified version of PowerShell.</span></span> <span data-ttu-id="4881f-153">V systému musí být nainstalovaná verze, který zadáte.</span><span class="sxs-lookup"><span data-stu-id="4881f-153">The version that you specify must be installed on the system.</span></span> <span data-ttu-id="4881f-154">Pokud prostředí PowerShell 3.0 je nainstalována v počítači, platné hodnoty jsou "2.0" a "3.0".</span><span class="sxs-lookup"><span data-stu-id="4881f-154">If PowerShell 3.0 is installed on the computer, valid values are "2.0" and "3.0".</span></span> <span data-ttu-id="4881f-155">Výchozí hodnota je "3.0".</span><span class="sxs-lookup"><span data-stu-id="4881f-155">The default value is "3.0".</span></span>

<span data-ttu-id="4881f-156">Pokud není nainstalovaný PowerShell 3.0, jediná platná hodnota je "2.0".</span><span class="sxs-lookup"><span data-stu-id="4881f-156">If PowerShell 3.0 isn't installed, the only valid value is "2.0".</span></span> <span data-ttu-id="4881f-157">Další hodnoty jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="4881f-157">Other values are ignored.</span></span>

<span data-ttu-id="4881f-158">Další informace najdete v tématu [instalace prostředí Windows PowerShell](../../setup/installing-windows-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4881f-158">For more information, see [Installing Windows PowerShell](../../setup/installing-windows-powershell.md).</span></span>

### <a name="-windowstyle-window-style"></a><span data-ttu-id="4881f-159">-WindowStyle <Window style></span><span class="sxs-lookup"><span data-stu-id="4881f-159">-WindowStyle <Window style></span></span>

<span data-ttu-id="4881f-160">Nastaví styl okna pro relaci.</span><span class="sxs-lookup"><span data-stu-id="4881f-160">Sets the window style for the session.</span></span> <span data-ttu-id="4881f-161">Platné hodnoty jsou Normal, Minimized, Maximized a skryté.</span><span class="sxs-lookup"><span data-stu-id="4881f-161">Valid values are Normal, Minimized, Maximized, and Hidden.</span></span>

### <a name="-command"></a><span data-ttu-id="4881f-162">-– Příkaz</span><span class="sxs-lookup"><span data-stu-id="4881f-162">-Command</span></span>

<span data-ttu-id="4881f-163">Provede zadané příkazy (s žádné parametry), jakoby byly zadány v příkazovém řádku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4881f-163">Executes the specified commands (with any parameters) as though they were typed at the PowerShell command prompt.</span></span>
<span data-ttu-id="4881f-164">Po spuštění, prostředí PowerShell ukončí, pokud **NoExit** je zadán parametr.</span><span class="sxs-lookup"><span data-stu-id="4881f-164">After execution, PowerShell exits unless the **NoExit** parameter is specified.</span></span>
<span data-ttu-id="4881f-165">Žádný text po `-Command` se odešle jako jeden příkazový řádek powershellu.</span><span class="sxs-lookup"><span data-stu-id="4881f-165">Any text after `-Command` is sent as a single command line to PowerShell.</span></span>
<span data-ttu-id="4881f-166">Tím se liší od stlaní `-File` zpracovává parametry předány skriptu.</span><span class="sxs-lookup"><span data-stu-id="4881f-166">This is different from how `-File` handles parameters sent to a script.</span></span>

<span data-ttu-id="4881f-167">Hodnota `-Command` může být "-", řetězec nebo blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="4881f-167">The value of `-Command` can be "-", a string, or a script block.</span></span>
<span data-ttu-id="4881f-168">Výsledky příkazu se vrátí do nadřazené prostředí jako deserializovaný objekty jazyka XML, ne živé objekty.</span><span class="sxs-lookup"><span data-stu-id="4881f-168">The results of the command are returned to the parent shell as deserialized XML objects, not live objects.</span></span>

<span data-ttu-id="4881f-169">Pokud hodnota `-Command` je "-", text příkazu je pro čtení ze standardního vstupu.</span><span class="sxs-lookup"><span data-stu-id="4881f-169">If the value of `-Command` is "-", the command text is read from standard input.</span></span>

<span data-ttu-id="4881f-170">Pokud hodnota `-Command` je řetězec, **příkaz** _musí_ být poslední parametr zadán, protože žádné znaky zadali po příkazu jsou interpretovány jako argumenty příkazu.</span><span class="sxs-lookup"><span data-stu-id="4881f-170">When the value of `-Command` is a string, **Command** _must_ be the last parameter specified because any characters typed after the command are interpreted as the command arguments.</span></span>

<span data-ttu-id="4881f-171">**Příkaz** parametr lze zadat pouze blok skriptu pro spuštění při poznáte hodnotu předanou `-Command` jako typ vlastnost ScriptBlock.</span><span class="sxs-lookup"><span data-stu-id="4881f-171">The **Command** parameter only accepts a script block for execution when it can recognize the value passed to `-Command` as a ScriptBlock type.</span></span>
<span data-ttu-id="4881f-172">Toto je _pouze_ možné při spuštění PowerShell.exe z jiného hostitele prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4881f-172">This is _only_ possible when running PowerShell.exe from another PowerShell host.</span></span>
<span data-ttu-id="4881f-173">Hostování ScriptBlock typu mohou být obsaženy v existujícím proměnné, vrácený z výrazu nebo analyzovaný pomocí prostředí PowerShell jako blok skriptu literálů ve složených závorkách `{}`, před předáním PowerShell.exe.</span><span class="sxs-lookup"><span data-stu-id="4881f-173">The ScriptBlock type may be contained in an existing variable, returned from an expression, or parsed by the PowerShell host as a literal script block enclosed in curly braces `{}`, before being passed to PowerShell.exe.</span></span>

<span data-ttu-id="4881f-174">Na cmd.exe, není i bloku skriptu (nebo ScriptBlock typu), takže hodnota předaná **příkaz** bude _vždy_ bude řetězec.</span><span class="sxs-lookup"><span data-stu-id="4881f-174">In cmd.exe, there is no such thing as a script block (or ScriptBlock type), so the value passed to **Command** will _always_ be a string.</span></span>
<span data-ttu-id="4881f-175">Můžete napsat jenom blok skriptu do řetězce, ale místo prováděný se budou chovat přesně jako by jste ji zadali typické řádku prostředí PowerShell, tisk obsahu skript blokování zpět vám.</span><span class="sxs-lookup"><span data-stu-id="4881f-175">You can write a script block inside the string, but instead of being executed it will behave exactly as though you typed it at a typical PowerShell prompt, printing the contents of the script block back out to you.</span></span>

<span data-ttu-id="4881f-176">Předán řetězec `-Command` stále se spustí jako PowerShell, takže složených závorek bloku skriptu se často nevyžadují na prvním místě při spuštění z cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="4881f-176">A string passed to `-Command` will still be executed as PowerShell, so the script block curly braces are often not required in the first place when running from cmd.exe.</span></span>
<span data-ttu-id="4881f-177">K provedení bloku skriptu vložené definované uvnitř řetězce, [operátor volání](/powershell/module/microsoft.powershell.core/about/about_operators#call-operator-) `&` lze použít:</span><span class="sxs-lookup"><span data-stu-id="4881f-177">To execute an inline script block defined inside a string, the [call operator](/powershell/module/microsoft.powershell.core/about/about_operators#call-operator-) `&` can be used:</span></span>

```console
"& {<command>}"
```

### <a name="-help---"></a><span data-ttu-id="4881f-178">-Help,-?, /?</span><span class="sxs-lookup"><span data-stu-id="4881f-178">-Help, -?, /?</span></span>

<span data-ttu-id="4881f-179">Ukazuje syntaxi powershell.exe.</span><span class="sxs-lookup"><span data-stu-id="4881f-179">Shows the syntax of powershell.exe.</span></span> <span data-ttu-id="4881f-180">Pokud se zadáním příkazu PowerShell.exe v prostředí PowerShell, předřaďte parametry příkazu s pomlčkou (-), ne lomítkem (/).</span><span class="sxs-lookup"><span data-stu-id="4881f-180">If you are typing a PowerShell.exe command in PowerShell, prepend the command parameters with a hyphen (-), not a forward slash (/).</span></span> <span data-ttu-id="4881f-181">Můžete v Cmd.exe pomlčkou nebo lomítkem.</span><span class="sxs-lookup"><span data-stu-id="4881f-181">You can use either a hyphen or forward slash in Cmd.exe.</span></span>

> [!NOTE]
> <span data-ttu-id="4881f-182">Poznámka k řešení problémů: V prostředí PowerShell 2.0 počínaje některé programy ve Windows Powershellu, nelze LastExitCode 0xc0000142.</span><span class="sxs-lookup"><span data-stu-id="4881f-182">Troubleshooting Note: In PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.</span></span>

## <a name="examples"></a><span data-ttu-id="4881f-183">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="4881f-183">EXAMPLES</span></span>

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

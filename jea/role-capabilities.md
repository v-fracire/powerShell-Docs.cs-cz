---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Role funkce JEA
ms.openlocfilehash: bd0a995adc60e50049ff99d6b23e7c2aeb745a18
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522935"
---
# <a name="jea-role-capabilities"></a><span data-ttu-id="f6087-103">Role funkce JEA</span><span class="sxs-lookup"><span data-stu-id="f6087-103">JEA Role Capabilities</span></span>

> <span data-ttu-id="f6087-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f6087-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="f6087-105">Při vytváření koncového bodu JEA, budete muset definovat jeden nebo více "funkce rolí" které popisují *co* někdo můžete provést v relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="f6087-105">When creating a JEA endpoint, you will need to define one or more "role capabilities" which describe *what* someone can do in a JEA session.</span></span>
<span data-ttu-id="f6087-106">Funkce role je PowerShell datový soubor s příponou .psrc, který obsahuje seznam všech rutin, funkcí, poskytovatelů a externích programů, které by měly být k dispozici připojování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="f6087-106">A role capability is a PowerShell data file with the .psrc extension that lists all the cmdlets, functions, providers, and external programs that should be made available to connecting users.</span></span>

<span data-ttu-id="f6087-107">Toto téma popisuje, jak vytvořit soubor prostředí PowerShell role funkce JEA uživatelům.</span><span class="sxs-lookup"><span data-stu-id="f6087-107">This topic describes how to create a PowerShell role capability file for your JEA users.</span></span>

## <a name="determine-which-commands-to-allow"></a><span data-ttu-id="f6087-108">Určit, které příkazy umožňující</span><span class="sxs-lookup"><span data-stu-id="f6087-108">Determine which commands to allow</span></span>

<span data-ttu-id="f6087-109">Prvním krokem při vytváření souboru funkce role, je rozmyslet, co uživatelé, kteří mají přiřazenou roli potřebovat přístup k.</span><span class="sxs-lookup"><span data-stu-id="f6087-109">The first step when creating a role capability file is to consider what the users who are assigned the role will need access to.</span></span>
<span data-ttu-id="f6087-110">Tyto požadavky proces shromažďování může chvíli trvat, ale je velmi důležité proces.</span><span class="sxs-lookup"><span data-stu-id="f6087-110">This requirements gathering process can take a while, but it is a very important process.</span></span>
<span data-ttu-id="f6087-111">Udělení přístupu uživatelům ke příliš málo rutiny a funkce je můžete zabránit v získání jejich práci.</span><span class="sxs-lookup"><span data-stu-id="f6087-111">Giving users access to too few cmdlets and functions can prevent them from getting their job done.</span></span>
<span data-ttu-id="f6087-112">Povolení přístupu k příliš mnoho funkcí a rutiny může vést k provádění více, než jste chtěli s jejich oprávněními implicitní správce oslabení postoj vaší zabezpečení uživatele.</span><span class="sxs-lookup"><span data-stu-id="f6087-112">Allowing access to too many cmdlets and functions can lead to users doing more than you intended with their implicit admin privileges, weakening your security stance.</span></span>

<span data-ttu-id="f6087-113">Jak přejít o tomto procesu bude záviset na vaší organizace a cíle, ale následující tipy mohou pomoci zajistit, že jste na správné cestě.</span><span class="sxs-lookup"><span data-stu-id="f6087-113">How you go about this process will depend on your organization and goals, however the following tips can help ensure you're on the right path.</span></span>

1. <span data-ttu-id="f6087-114">**Identifikujte** příkazy uživatelé používají k dokončení jejich úloh.</span><span class="sxs-lookup"><span data-stu-id="f6087-114">**Identify** the commands users are using to get their jobs done.</span></span> <span data-ttu-id="f6087-115">To může zahrnovat zjištění pracovníky IT, kontrolu skriptů pro automatizaci nebo analýza protokolů nebo záznamy o studiu relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6087-115">This may involve surveying IT staff, checking automation scripts, or analyzing PowerShell session transcripts or logs.</span></span>
2. <span data-ttu-id="f6087-116">**Aktualizace** pomocí nástroje příkazového řádku a Powershellu ekvivalenty, kde je to možné, pro nejlepší auditování a možnostmi přizpůsobení JEA.</span><span class="sxs-lookup"><span data-stu-id="f6087-116">**Update** use of command line tools to PowerShell equivalents, where possible, for the best auditing and JEA customization experience.</span></span> <span data-ttu-id="f6087-117">Jako posunutím jako nativní rutin prostředí PowerShell a funkce v sadě nástrojů JEA nemůže omezovat externích programů.</span><span class="sxs-lookup"><span data-stu-id="f6087-117">External programs cannot be constrained as granularly as native PowerShell cmdlets and functions in JEA.</span></span>
3. <span data-ttu-id="f6087-118">**Omezit** oboru rutin, pokud je nutné jenom povolit určité parametry nebo hodnoty parametrů.</span><span class="sxs-lookup"><span data-stu-id="f6087-118">**Restrict** the scope of the cmdlets if necessary to only allow specific parameters or parameter values.</span></span> <span data-ttu-id="f6087-119">To je zvlášť důležité, pokud uživatelé by měli být pouze možnost spravovat součástí systému.</span><span class="sxs-lookup"><span data-stu-id="f6087-119">This is particularly important if users should only be able to manage part of a system.</span></span>
4. <span data-ttu-id="f6087-120">**Vytvoření** vlastní funkce k nahrazení komplexní příkazy nebo příkazy, které je obtížné zachovat v sadě nástrojů JEA.</span><span class="sxs-lookup"><span data-stu-id="f6087-120">**Create** custom functions to replace complex commands or commands which are difficult to constrain in JEA.</span></span> <span data-ttu-id="f6087-121">Jednoduché funkce, která zabalí komplexní příkaz nebo použije další ověřovací logiku můžou nabízet další ovládací prvek pro zjednodušení správci a koncových uživatelů.</span><span class="sxs-lookup"><span data-stu-id="f6087-121">A simple function that wraps a complex command or applies additional validation logic can offer additional control for admins and end-user simplicity.</span></span>
5. <span data-ttu-id="f6087-122">**Test** s vymezeným oborem seznam povolených příkazů s vaší uživatele a/nebo Automatizace služeb a podle potřeby upravte.</span><span class="sxs-lookup"><span data-stu-id="f6087-122">**Test** the scoped list of allowable commands with your users and/or automation services and adjust as necessary.</span></span>

<span data-ttu-id="f6087-123">Je dobré si uvědomit, že příkazy v relaci JEA jsou často oprávněními spustit správce (nebo jinak se zvýšenými oprávněními).</span><span class="sxs-lookup"><span data-stu-id="f6087-123">It is important to remember that commands in a JEA session are often run with admin (or otherwise elevated) privileges.</span></span>
<span data-ttu-id="f6087-124">Pozor, výběr dostupných příkazech je důležité zajistit, že koncového bodu JEA neumožňuje připojení uživatelů ke zvýšení svých oprávnění.</span><span class="sxs-lookup"><span data-stu-id="f6087-124">Careful selection of available commands is important to ensure the JEA endpoint does not allow the connecting user to elevate their permissions.</span></span>
<span data-ttu-id="f6087-125">Níže je několik příkladů příkazů, které můžete použít speciálně Pokud může ve stavu bez omezení.</span><span class="sxs-lookup"><span data-stu-id="f6087-125">Below are some examples of commands that can be used maliciously if allowed in an unconstrained state.</span></span>
<span data-ttu-id="f6087-126">Všimněte si, že to není vyčerpávající seznam a slouží pouze jako výchozí bod vytvořených.</span><span class="sxs-lookup"><span data-stu-id="f6087-126">Note that this is not an exhaustive list and should only be used as a cautionary starting point.</span></span>

### <a name="examples-of-potentially-dangerous-commands"></a><span data-ttu-id="f6087-127">Příklady potenciálně nebezpečných příkazů</span><span class="sxs-lookup"><span data-stu-id="f6087-127">Examples of potentially dangerous commands</span></span>

<span data-ttu-id="f6087-128">Riziko</span><span class="sxs-lookup"><span data-stu-id="f6087-128">Risk</span></span> | <span data-ttu-id="f6087-129">Příklad</span><span class="sxs-lookup"><span data-stu-id="f6087-129">Example</span></span> | <span data-ttu-id="f6087-130">Související příkazy</span><span class="sxs-lookup"><span data-stu-id="f6087-130">Related commands</span></span>
-----|---------|-----------------
<span data-ttu-id="f6087-131">Udělení oprávnění správce, aby vynechat JEA je připojující se uživatel</span><span class="sxs-lookup"><span data-stu-id="f6087-131">Granting the connecting user admin privileges to bypass JEA</span></span> | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | <span data-ttu-id="f6087-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span><span class="sxs-lookup"><span data-stu-id="f6087-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span></span>
<span data-ttu-id="f6087-133">Spuštění libovolného kódu, jako je například malware, zneužití nebo vlastní skripty pro obejití ochrany</span><span class="sxs-lookup"><span data-stu-id="f6087-133">Running arbitrary code, such as malware, exploits, or custom scripts to bypass protections</span></span> | `Start-Process -FilePath '\\san\share\malware.exe'` | <span data-ttu-id="f6087-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span><span class="sxs-lookup"><span data-stu-id="f6087-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span></span>

## <a name="create-a-role-capability-file"></a><span data-ttu-id="f6087-135">Vytvořte soubor funkce rolí</span><span class="sxs-lookup"><span data-stu-id="f6087-135">Create a role capability file</span></span>

<span data-ttu-id="f6087-136">Můžete vytvořit nový soubor funkce role prostředí PowerShell s [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f6087-136">You can create a new PowerShell role capability file with the [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) cmdlet.</span></span>

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

<span data-ttu-id="f6087-137">Výsledný soubor funkce role můžete otevřít v textovém editoru a upravit tak, aby bylo možné požadované příkazy pro danou roli.</span><span class="sxs-lookup"><span data-stu-id="f6087-137">The resulting role capability file can be opened in a text editor and modified to allow the desired commands for the role.</span></span>
<span data-ttu-id="f6087-138">V nápovědě k prostředí PowerShell obsahuje několik příkladů konfigurace souboru.</span><span class="sxs-lookup"><span data-stu-id="f6087-138">The PowerShell help documentation contains several examples of how you can configure the file.</span></span>

### <a name="allowing-powershell-cmdlets-and-functions"></a><span data-ttu-id="f6087-139">Povolení funkcí a rutin prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6087-139">Allowing PowerShell cmdlets and functions</span></span>

<span data-ttu-id="f6087-140">K autorizaci uživatelů ke spouštění rutin prostředí PowerShell nebo funkce, přidejte do polí VisbibleCmdlets nebo VisibleFunctions název rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="f6087-140">To authorize users to run PowerShell cmdlets or functions, add the cmdlet or function name to the VisbibleCmdlets or VisibleFunctions fields.</span></span>
<span data-ttu-id="f6087-141">Pokud si nejste jisti, zda je příkazu rutiny nebo funkce, můžete spustit `Get-Command <name>` a zkontrolujte vlastnost "CommandType" ve výstupu.</span><span class="sxs-lookup"><span data-stu-id="f6087-141">If you aren't sure whether a command is a cmdlet or function, you can run `Get-Command <name>` and check the "CommandType" property in the output.</span></span>

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

<span data-ttu-id="f6087-142">Obor konkrétní rutiny nebo funkce je někdy příliš široké pro potřeby vašich uživatelů.</span><span class="sxs-lookup"><span data-stu-id="f6087-142">Sometimes the scope of a specific cmdlet or function is too broad for your users' needs.</span></span>
<span data-ttu-id="f6087-143">Správce DNS, například požaduje pravděpodobně pouze k restartování služby DNS.</span><span class="sxs-lookup"><span data-stu-id="f6087-143">A DNS admin, for example, probably only needs access to restart the DNS service.</span></span>
<span data-ttu-id="f6087-144">V prostředí s více tenanty, kde jsou tenanti udělen přístup k samoobslužné správy nástroje třeba tenantů omezit na správu pomocí svoje vlastní prostředky.</span><span class="sxs-lookup"><span data-stu-id="f6087-144">In a multi-tenant environment where tenants are granted access to self-service management tools, tenants should be limited to managing with their own resources.</span></span>
<span data-ttu-id="f6087-145">Pro tyto případy můžete omezit, jaké parametry jsou přístupné z rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="f6087-145">For these cases, you can restrict which parameters are exposed from the cmdlet or function.</span></span>

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

<span data-ttu-id="f6087-146">V pokročilejších scénářích budete také muset omezení hodnot, které někdo můžete zadat tyto parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-146">In more advanced scenarios, you may also need to restrict which values someone can supply to these parameters.</span></span>
<span data-ttu-id="f6087-147">Funkce rolí umožňují definovat sadu povolených hodnot nebo vzor regulárního výrazu, který je vyhodnocován pro určení, jestli je povolený daný vstup.</span><span class="sxs-lookup"><span data-stu-id="f6087-147">Role capabilities let you define a set of allowed values or a regular expression pattern that is evaluated to determine if a given input is allowed.</span></span>

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> <span data-ttu-id="f6087-148">[Společné parametry prostředí PowerShell](https://technet.microsoft.com/library/hh847884.aspx) jsou vždy povoleny, i když můžete omezit dostupné parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-148">The [common PowerShell parameters](https://technet.microsoft.com/library/hh847884.aspx) are always allowed, even if you restrict the available parameters.</span></span>
> <span data-ttu-id="f6087-149">Neměli uvedete explicitně je v poli parametrů.</span><span class="sxs-lookup"><span data-stu-id="f6087-149">You should not explicitly list them in the Parameters field.</span></span>

<span data-ttu-id="f6087-150">Následující tabulka popisuje různé způsoby, jak můžete přizpůsobit viditelné rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="f6087-150">The table below describes the various ways you can customize a visible cmdlet or function.</span></span>
<span data-ttu-id="f6087-151">Můžete kombinovat a párovat některý níže VisibleCmdlets pole.</span><span class="sxs-lookup"><span data-stu-id="f6087-151">You can mix and match any of the below in the VisibleCmdlets field.</span></span>

<span data-ttu-id="f6087-152">Příklad</span><span class="sxs-lookup"><span data-stu-id="f6087-152">Example</span></span>                                                                                      | <span data-ttu-id="f6087-153">Případ použití</span><span class="sxs-lookup"><span data-stu-id="f6087-153">Use case</span></span>
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
<span data-ttu-id="f6087-154">`'My-Func'` nebo `@{ Name = 'My-Func' }`</span><span class="sxs-lookup"><span data-stu-id="f6087-154">`'My-Func'` or `@{ Name = 'My-Func' }`</span></span>                                                       | <span data-ttu-id="f6087-155">Umožňuje uživateli spustit `My-Func` bez jakýchkoli omezení na parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-155">Allows the user to run `My-Func` without any restrictions on the parameters.</span></span>
`'MyModule\My-Func'`                                                                         | <span data-ttu-id="f6087-156">Umožňuje uživateli spustit `My-Func` z modulu `MyModule` bez jakýchkoli omezení na parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-156">Allows the user to run `My-Func` from the module `MyModule` without any restrictions on the parameters.</span></span>
`'My-*'`                                                                                     | <span data-ttu-id="f6087-157">Umožňuje uživateli spustit libovolné rutiny nebo funkce s příkaz `My`.</span><span class="sxs-lookup"><span data-stu-id="f6087-157">Allows the user to run any cmdlet or function with the verb `My`.</span></span>
`'*-Func'`                                                                                   | <span data-ttu-id="f6087-158">Umožňuje uživateli spustit libovolné rutiny nebo funkce s podstatným jménem `Func`.</span><span class="sxs-lookup"><span data-stu-id="f6087-158">Allows the user to run any cmdlet or function with the noun `Func`.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | <span data-ttu-id="f6087-159">Umožňuje uživateli spustit `My-Func` s `Param1` a/nebo `Param2` parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-159">Allows the user to run `My-Func` with the `Param1` and/or `Param2` parameters.</span></span> <span data-ttu-id="f6087-160">Libovolná hodnota mohou být poskytnuty parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-160">Any value can be supplied to the parameters.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | <span data-ttu-id="f6087-161">Umožňuje uživateli spustit `My-Func` s `Param1` parametru.</span><span class="sxs-lookup"><span data-stu-id="f6087-161">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="f6087-162">Parametr lze zadat pouze "Hodnota1" a "Hodnota2".</span><span class="sxs-lookup"><span data-stu-id="f6087-162">Only "Value1" and "Value2" can be supplied to the parameter.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | <span data-ttu-id="f6087-163">Umožňuje uživateli spustit `My-Func` s `Param1` parametru.</span><span class="sxs-lookup"><span data-stu-id="f6087-163">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="f6087-164">Předat parametru můžete zadat libovolnou hodnotu od "contoso".</span><span class="sxs-lookup"><span data-stu-id="f6087-164">Any value starting with "contoso" can be supplied to the parameter.</span></span>


> [!WARNING]
> <span data-ttu-id="f6087-165">Osvědčené postupy zabezpečení nedoporučujeme používat zástupné znaky, při definování viditelné rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="f6087-165">For best security practices, it is not recommended to use wildcards when defining visible cmdlets or functions.</span></span>
> <span data-ttu-id="f6087-166">Místo toho by měly explicitně uvádět každé důvěryhodné příkaz, kterým zajistíte, že žádné další příkazy, které sdílejí stejné schéma pojmenování neúmyslně oprávnění.</span><span class="sxs-lookup"><span data-stu-id="f6087-166">Instead, you should explicitly list each trusted command to ensure no other commands that share the same naming scheme are unintentionally authorized.</span></span>

<span data-ttu-id="f6087-167">ValidatePattern i ValidateSet nelze použít stejnou rutinu nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="f6087-167">You cannot apply both a ValidatePattern and ValidateSet to the same cmdlet or function.</span></span>

<span data-ttu-id="f6087-168">Pokud ano, přepíše ValidatePattern ValidateSet.</span><span class="sxs-lookup"><span data-stu-id="f6087-168">If you do, the ValidatePattern will override the ValidateSet.</span></span>

<span data-ttu-id="f6087-169">Další informace o ValidatePattern, projděte si [to *Hey, Scripting Guy!!* příspěvku](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) a [regulární výrazy Powershellu](https://technet.microsoft.com/library/hh847880.aspx) referenční obsah.</span><span class="sxs-lookup"><span data-stu-id="f6087-169">For more information about ValidatePattern, check out [this *Hey, Scripting Guy!* post](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) and the [PowerShell Regular Expressions](https://technet.microsoft.com/library/hh847880.aspx) reference content.</span></span>

### <a name="allowing-external-commands-and-powershell-scripts"></a><span data-ttu-id="f6087-170">Povolení externího příkazy a skripty prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6087-170">Allowing external commands and PowerShell scripts</span></span>

<span data-ttu-id="f6087-171">Umožňuje uživatelům spouštět spustitelné soubory a skripty prostředí PowerShell (.ps1) v relaci JEA budete muset přidat do každého programu v poli VisibleExternalCommands úplnou cestu.</span><span class="sxs-lookup"><span data-stu-id="f6087-171">To allow users to run executables and PowerShell scripts (.ps1) in a JEA session, you have to add the full path to each program in the VisibleExternalCommands field.</span></span>

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

<span data-ttu-id="f6087-172">Doporučujeme, kde je to možné, používat PowerShell rutinu/funkce ekvivalenty externí spustitelné soubory, které autorizujete, protože budete mít kontrolu nad tím, které jsou povoleny parametry s functions rutiny prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6087-172">It is advised, where possible, to use PowerShell cmdlet/function equivalents of any external executables you authorize since you have control over which parameters are allowed with PowerShell cmdlets/functions.</span></span>

<span data-ttu-id="f6087-173">Mnoho spustitelných souborů bylo možné číst aktuální stav a pak ji změňte právě tím, že poskytuje různé parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-173">Many executables allow you to both read the current state and then change it just by providing different parameters.</span></span>

<span data-ttu-id="f6087-174">Představte si třeba roli správce serveru soubor, který chcete zkontrolovat, které sdílené síťové složky, které jsou hostované v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="f6087-174">For example, consider the role of a file server admin who wants to check which network shares are hosted by the local machine.</span></span>
<span data-ttu-id="f6087-175">Zkontrolujte jedním ze způsobů je použít `net share`.</span><span class="sxs-lookup"><span data-stu-id="f6087-175">One way to check is to use `net share`.</span></span>
<span data-ttu-id="f6087-176">Nicméně umožňuje net.exe je velmi nebezpečné, protože správce stejně snadno použít příkaz získat oprávnění správce s `net group Administrators unprivilegedjeauser /add`.</span><span class="sxs-lookup"><span data-stu-id="f6087-176">However, allowing net.exe is very dangerous becuase the admin could just as easily use the command to gain admin privileges with `net group Administrators unprivilegedjeauser /add`.</span></span>
<span data-ttu-id="f6087-177">Lepším řešením je povolit [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) která dosáhne stejného výsledku, ale má mnohem více omezený rozsah.</span><span class="sxs-lookup"><span data-stu-id="f6087-177">A better approach is to allow [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) which achieves the same result but has a much more limited scope.</span></span>

<span data-ttu-id="f6087-178">Při provádění externích příkazů k dispozici uživatelům v relaci JEA, vždy zadejte úplnou cestu ke spustitelnému souboru k zajištění s podobným názvem (a potenciálně malicous) aplikace umístěn jinde v systému nejsou vykonány místo.</span><span class="sxs-lookup"><span data-stu-id="f6087-178">When making external commands available to users in a JEA session, always specify the complete path to the executable to ensure a similarly named (and potentially malicous) program placed elsewhere on the system does not get executed instead.</span></span>

### <a name="allowing-access-to-powershell-providers"></a><span data-ttu-id="f6087-179">Povolení přístupu ke zprostředkovatelům prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6087-179">Allowing access to PowerShell providers</span></span>

<span data-ttu-id="f6087-180">Ve výchozím nastavení nejsou k dispozici v relacích JEA žádní zprostředkovatelé prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6087-180">By default, no PowerShell providers are available in JEA sessions.</span></span>

<span data-ttu-id="f6087-181">To je především pro snížení rizika citlivé informace a nastavení konfigurace se starším připojující se uživatel.</span><span class="sxs-lookup"><span data-stu-id="f6087-181">This is primarily to reduce the risk of sensitive information and configuration settings being disclosed to the connecting user.</span></span>

<span data-ttu-id="f6087-182">Pokud je to nezbytné, můžete povolit přístup ke zprostředkovatelům Powershellu pomocí `VisibleProviders` příkazu.</span><span class="sxs-lookup"><span data-stu-id="f6087-182">When necessary, you can allow access to the PowerShell providers using the `VisibleProviders` command.</span></span>
<span data-ttu-id="f6087-183">Úplný seznam poskytovatelů, spouštění `Get-PSProvider`.</span><span class="sxs-lookup"><span data-stu-id="f6087-183">For a full list of providers, run `Get-PSProvider`.</span></span>

```powershell
VisibleProviders = 'Registry'
```

<span data-ttu-id="f6087-184">Pro jednoduché úlohy, které vyžadují přístup k systému souborů, registry, úložiště certifikátů nebo jiných citlivých poskytovatelů může také být vhodné zápis vlastní funkce, který spolupracuje s poskytovateli jménem uživatele.</span><span class="sxs-lookup"><span data-stu-id="f6087-184">For simple tasks that require access to the file system, registry, certificate store, or other sensitive providers, you can also consider writing a custom function that works with the provider on the user's behalf.</span></span>
<span data-ttu-id="f6087-185">Funkce, rutiny a externích programů, které jsou k dispozici v relaci JEA nejsou v souladu s stejná omezení jako JEA – jakýkoli poskytovatel přístupem ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="f6087-185">Functions, cmdlets, and external programs that are available in a JEA session are not subject to the same constraints as JEA -- they can access any provider by default.</span></span>
<span data-ttu-id="f6087-186">Také zvážit použití [uživatele jednotky](session-configurations.md#user-drive) při kopírování souborů do/z koncového bodu JEA je povinný.</span><span class="sxs-lookup"><span data-stu-id="f6087-186">Also consider using the [user drive](session-configurations.md#user-drive) when copying files to/from a JEA endpoint is required.</span></span>

### <a name="creating-custom-functions"></a><span data-ttu-id="f6087-187">Vytvoření vlastní funkce</span><span class="sxs-lookup"><span data-stu-id="f6087-187">Creating custom functions</span></span>

<span data-ttu-id="f6087-188">Můžete vytvářet vlastní funkce v souboru funkce role pro zjednodušení složitých úloh pro koncové uživatele.</span><span class="sxs-lookup"><span data-stu-id="f6087-188">You can author custom functions in a role capability file to simplify complex tasks for your end users.</span></span>
<span data-ttu-id="f6087-189">Vlastní funkce jsou také užitečné, pokud požadujete pokročilé ověřovací logiku pro hodnoty parametru rutiny.</span><span class="sxs-lookup"><span data-stu-id="f6087-189">Custom functions are also useful when you require advanced validation logic for cmdlet parameter values.</span></span>
<span data-ttu-id="f6087-190">Můžete psát jednoduché funkce **FunctionDefinitions** pole:</span><span class="sxs-lookup"><span data-stu-id="f6087-190">You can write simple functions in the **FunctionDefinitions** field:</span></span>

```powershell
VisibleFunctions = 'Get-TopProcess'

FunctionDefinitions = @{
    Name = 'Get-TopProcess'

    ScriptBlock = {
        param($Count = 10)

        Get-Process | Sort-Object -Property CPU -Descending | Microsoft.PowerShell.Utility\Select-Object -First $Count
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="f6087-191">Nezapomeňte si přidat název své vlastní funkce pro **VisibleFunctions** pole, aby mohla být užívána uživateli JEA.</span><span class="sxs-lookup"><span data-stu-id="f6087-191">Don't forget to add the name of your custom functions to the **VisibleFunctions** field so they can be run by the JEA users.</span></span>


<span data-ttu-id="f6087-192">Text (bloku skriptu) vlastní funkce se spustí v režimu výchozí jazyk pro systém a není předmětem omezení JEA na jazyk.</span><span class="sxs-lookup"><span data-stu-id="f6087-192">The body (script block) of custom functions runs in the default language mode for the system and is not subject to JEA's language constraints.</span></span>
<span data-ttu-id="f6087-193">To znamená, že funkce můžete přístup k systému souborů a registru a spouštět příkazy, které nebyly nastavena jako viditelná v souboru funkce role.</span><span class="sxs-lookup"><span data-stu-id="f6087-193">This means that functions can access the file system and registry, and run commands that were not made visible in the role capability file.</span></span>
<span data-ttu-id="f6087-194">Snažte se vyhnout, což libovolný kód ke spuštění, při použití parametrů a vyhnout se vstup uživatele zřetězení příkazů přímo do rutiny jako `Invoke-Expression`.</span><span class="sxs-lookup"><span data-stu-id="f6087-194">Take care to avoid allowing arbitrary code to be run when using parameters and avoid piping user input directly into cmdlets like `Invoke-Expression`.</span></span>

<span data-ttu-id="f6087-195">V předchozím příkladu si povšimněte, který modul plně kvalifikovaný název (FQMN) `Microsoft.PowerShell.Utility\Select-Object` byl použit místo zkrácený `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="f6087-195">In the above example, you will notice that the fully qualified module name (FQMN) `Microsoft.PowerShell.Utility\Select-Object` was used instead of the shorthand `Select-Object`.</span></span>
<span data-ttu-id="f6087-196">Funkce definované v souborech schopností role jsou pořád v souladu s rozsahu JEA relací, což zahrnuje funkce proxy JEA vytvoří omezit stávající příkazy.</span><span class="sxs-lookup"><span data-stu-id="f6087-196">Functions defined in role capability files are still subject to the scope of JEA sessions, which includes the proxy functions JEA creates to constrain existing commands.</span></span>

<span data-ttu-id="f6087-197">Select-Object je výchozím omezením rutiny ve všech relacích JEA, který neumožňuje vyberte libovolné vlastnosti u objektů.</span><span class="sxs-lookup"><span data-stu-id="f6087-197">Select-Object is a default, constrained cmdlet in all JEA sessions that doesn't allow you to select arbitrary properties on objects.</span></span>
<span data-ttu-id="f6087-198">Bez omezení Select-Object používat ve funkcích, musí explicitně vyžádat toto plně implementováno zadáním FQMN.</span><span class="sxs-lookup"><span data-stu-id="f6087-198">To use the unconstrained Select-Object in functions, you must explicitly request the full implementation by specifying the FQMN.</span></span>
<span data-ttu-id="f6087-199">Všechny rutiny omezené v relaci JEA produkovány stejné chování při vyvolání z funkce, v Powershellu [příkaz prioritu](https://msdn.microsoft.com/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span><span class="sxs-lookup"><span data-stu-id="f6087-199">Any constrained cmdlet in a JEA session will exhibit the same behavior when invoked from a function, in line with PowerShell's [command precedence](https://msdn.microsoft.com/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span></span>

<span data-ttu-id="f6087-200">Pokud vytváříte velké množství vlastních funkcí, může být jednodušší umístit je do [modul skriptu Powershellu](https://msdn.microsoft.com/library/dd878340(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="f6087-200">If you are writing a lot of custom functions, it may be easier to put them in a [PowerShell Script Module](https://msdn.microsoft.com/library/dd878340(v=vs.85).aspx).</span></span>
<span data-ttu-id="f6087-201">Potom můžete provést tyto funkce viditelné v relaci JEA pomocí pole VisibleFunctions stejně, jako byste s moduly integrované nebo od jiného výrobce.</span><span class="sxs-lookup"><span data-stu-id="f6087-201">You can then make those functions visible in the JEA session using the VisibleFunctions field like you would with built-in and third party modules.</span></span>

## <a name="place-role-capabilities-in-a-module"></a><span data-ttu-id="f6087-202">Funkce rolí místo v modulu</span><span class="sxs-lookup"><span data-stu-id="f6087-202">Place role capabilities in a module</span></span>

<span data-ttu-id="f6087-203">Aby Powershellu k vyhledání souboru funkce role musí být uložen ve složce "RoleCapabilities" v modulu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6087-203">In order for PowerShell to find a role capability file, it must be stored in a "RoleCapabilities" folder in a PowerShell module.</span></span>
<span data-ttu-id="f6087-204">Modul mohou být uloženy v jakékoli složce součástí `$env:PSModulePath` proměnné prostředí, ale by neměly umístěte do System32 (vyhrazeno pro integrované moduly) nebo složce kde nedůvěryhodném, připojení uživatelů může upravit soubory.</span><span class="sxs-lookup"><span data-stu-id="f6087-204">The module can be stored in any folder included in the `$env:PSModulePath` environment variable, however you should not place it in System32 (reserved for built-in modules) or a folder where the untrusted, connecting users could modify the files.</span></span>
<span data-ttu-id="f6087-205">Níže je příklad vytvoření základní modul skriptu Powershellu s názvem *ContosoJEA* v cestě "Program Files".</span><span class="sxs-lookup"><span data-stu-id="f6087-205">Below is an example of creating a basic PowerShell script module called *ContosoJEA* in the "Program Files" path.</span></span>

```powershell
# Create a folder for the module
$modulePath = Join-Path $env:ProgramFiles "WindowsPowerShell\Modules\ContosoJEA"
New-Item -ItemType Directory -Path $modulePath

# Create an empty script module and module manifest. At least one file in the module folder must have the same name as the folder itself.
New-Item -ItemType File -Path (Join-Path $modulePath "ContosoJEAFunctions.psm1")
New-ModuleManifest -Path (Join-Path $modulePath "ContosoJEA.psd1") -RootModule "ContosoJEAFunctions.psm1"

# Create the RoleCapabilities folder and copy in the PSRC file
$rcFolder = Join-Path $modulePath "RoleCapabilities"
New-Item -ItemType Directory $rcFolder
Copy-Item -Path .\MyFirstJEARole.psrc -Destination $rcFolder
```

<span data-ttu-id="f6087-206">Zobrazit [Principy modul Powershellu](https://msdn.microsoft.com/library/dd878324.aspx) Další informace o moduly Powershellu, modul manifesty a proměnnou prostředí PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="f6087-206">See [Understanding a PowerShell Module](https://msdn.microsoft.com/library/dd878324.aspx) for more information about PowerShell modules, module manifests, and the PSModulePath environment variable.</span></span>

## <a name="updating-role-capabilities"></a><span data-ttu-id="f6087-207">Aktualizace funkcí role</span><span class="sxs-lookup"><span data-stu-id="f6087-207">Updating role capabilities</span></span>


<span data-ttu-id="f6087-208">Soubor funkce role můžete kdykoli aktualizovat jednoduše ukládají se změny do souboru funkce role.</span><span class="sxs-lookup"><span data-stu-id="f6087-208">You can update a role capability file at any time by simply saving changes to the role capability file.</span></span>
<span data-ttu-id="f6087-209">Všechny nové relace JEA spuštěna po aktualizaci role funkce bude odrážet revidovaná funkce.</span><span class="sxs-lookup"><span data-stu-id="f6087-209">Any new JEA sessions started after the role capability has been updated will reflect the revised capabilities.</span></span>

<span data-ttu-id="f6087-210">To se dělá tak důležitý řízení přístupu ke složce funkce role.</span><span class="sxs-lookup"><span data-stu-id="f6087-210">This is why controlling access to the role capabilities folder is so important.</span></span>
<span data-ttu-id="f6087-211">Pouze vysoce důvěryhodných správců měl změnit soubory funkce role.</span><span class="sxs-lookup"><span data-stu-id="f6087-211">Only highly trusted administrators should be able to change role capability files.</span></span>
<span data-ttu-id="f6087-212">Pokud je nedůvěryhodný uživatel může změnit soubory funkce role, se můžete snadno sám si udělit přístup do rutin, které zajistí, aby zvýšení svých oprávnění.</span><span class="sxs-lookup"><span data-stu-id="f6087-212">If an untrusted user can change role capability files, they can easily give themselves access to cmdlets which allow them to elevate their privileges.</span></span>


<span data-ttu-id="f6087-213">Pro správce chtějí uzamčení přístupu k funkcím role zajistěte, aby že Local System má přístup pro čtení souborů funkce role a moduly obsahující.</span><span class="sxs-lookup"><span data-stu-id="f6087-213">For administrators looking to lock down access to the role capabilities, ensure Local System has read access to the role capability files and containing modules.</span></span>

## <a name="how-role-capabilities-are-merged"></a><span data-ttu-id="f6087-214">Jak jsou sloučeny funkcí role</span><span class="sxs-lookup"><span data-stu-id="f6087-214">How role capabilities are merged</span></span>

<span data-ttu-id="f6087-215">Uživatelé lze udělit přístup k více funkcí role při zadávání JEA relace v závislosti na roli mapování [relace konfigurační soubor](session-configurations.md).</span><span class="sxs-lookup"><span data-stu-id="f6087-215">Users can be granted access to multiple role capabilities when they enter a JEA session depending on the role mappings in the [session configuration file](session-configurations.md).</span></span>
<span data-ttu-id="f6087-216">Pokud k tomu dojde, pokusí se JEA dát uživateli *největšími* sadu příkazů, které jsou povolené všechny role.</span><span class="sxs-lookup"><span data-stu-id="f6087-216">When this happens, JEA tries to give the user the *most permissive* set of commands allowed by any of the roles.</span></span>

<span data-ttu-id="f6087-217">**VisibleCmdlets a VisibleFunctions**</span><span class="sxs-lookup"><span data-stu-id="f6087-217">**VisibleCmdlets and VisibleFunctions**</span></span>

<span data-ttu-id="f6087-218">Většina komplexní logiku sloučení ovlivňuje rutiny a funkce, které mohou mít své parametry a jejich hodnoty v sadě nástrojů JEA omezené.</span><span class="sxs-lookup"><span data-stu-id="f6087-218">The most complex merge logic affects cmdlets and functions, which can have their parameters and parameter values limited in JEA.</span></span>

<span data-ttu-id="f6087-219">Pravidla jsou následující:</span><span class="sxs-lookup"><span data-stu-id="f6087-219">The rules are as follows:</span></span>

1. <span data-ttu-id="f6087-220">Pokud rutiny jsou dostupná jenom v jedné roli, bude viditelné pro uživatele s omezeními příslušný parametr.</span><span class="sxs-lookup"><span data-stu-id="f6087-220">If a cmdlet is only made visible in one role, it will be visible to the user with any applicable parameter constraints.</span></span>
2. <span data-ttu-id="f6087-221">Pokud rutiny jsou dostupná ve více než jednu roli, a Každá role má stejná omezení na rutinu, bude rutina viditelné pro uživatele s těmito omezeními.</span><span class="sxs-lookup"><span data-stu-id="f6087-221">If a cmdlet is made visible in more than one role, and each role has the same constraints on the cmdlet, the cmdlet will be visible to the user with those constraints.</span></span>
3. <span data-ttu-id="f6087-222">Pokud rutiny jsou dostupná ve více než jednu roli, a každou roli umožňuje jinou sadu parametrů, rutiny a všechny parametry definovat v rámci každé role budou viditelné pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="f6087-222">If a cmdlet is made visible in more than one role, and each role allows a different set of parameters, the cmdlet and all of the parameters defined across every role will be visible to the user.</span></span> <span data-ttu-id="f6087-223">Pokud jedna role nemá omezení pro parametry, povolí se všechny parametry.</span><span class="sxs-lookup"><span data-stu-id="f6087-223">If one role doesn't have constraints on the parameters, all parameters will be allowed.</span></span>
4. <span data-ttu-id="f6087-224">Pokud jednu roli definuje sadu ověřit nebo ověřit model pro parametr rutiny, a jinou roli umožňuje parametru ale neomezuje hodnoty parametrů, ověřit set nebo vzor se bude ignorovat.</span><span class="sxs-lookup"><span data-stu-id="f6087-224">If one role defines a validate set or validate pattern for a cmdlet parameter, and the other role allows the parameter but does not constrain the parameter values, the validate set or pattern will be ignored.</span></span>
5. <span data-ttu-id="f6087-225">Pokud sada validate je definována pro stejný parametr rutiny ve více než jednu roli, povolí se všechny hodnoty ze všech sad ověřit.</span><span class="sxs-lookup"><span data-stu-id="f6087-225">If a validate set is defined for the same cmdlet parameter in more than one role, all values from all validate sets will be allowed.</span></span>
6. <span data-ttu-id="f6087-226">Je-li ověřit vzor je definován pro stejný parametr rutiny ve více než jednu roli, povolí se všechny hodnoty, které se shodují s některým z tyto vzory se dají.</span><span class="sxs-lookup"><span data-stu-id="f6087-226">If a validate pattern is defined for the same cmdlet parameter in more than one role, any values that match any of the patterns will be allowed.</span></span>
7. <span data-ttu-id="f6087-227">Je-li ověřit sada je definována v jedné nebo více rolím a ověřit vzor je definován v jiné roli pro stejný parametr rutiny, je ignorován sady ověřit a pravidlo (6) se vztahuje na zbývající vzory ověřit.</span><span class="sxs-lookup"><span data-stu-id="f6087-227">If a validate set is defined in one or more roles, and a validate pattern is defined in another role for the same cmdlet parameter, the validate set is ignored and rule (6) applies to the remaining validate patterns.</span></span>

<span data-ttu-id="f6087-228">Níže je příklad, jak jsou sloučeny role podle těchto pravidel:</span><span class="sxs-lookup"><span data-stu-id="f6087-228">Below is an example of how roles are merged according to these rules:</span></span>

```powershell
# Role A Visible Cmdlets
$roleA = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client' } }
}

# Role B Visible Cmdlets
$roleB = @{
    VisibleCmdlets = @{ Name = 'Get-Service'; Parameters = @{ Name = 'DisplayName'; ValidatePattern = 'DNS.*' } },
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Server' } }
}

# Resulting permisisons for a user who belongs to both role A and B
# - The constraint in role B for the DisplayName parameter on Get-Service is ignored becuase of rule #4
# - The ValidateSets for Restart-Service are merged because both roles use ValidateSet on the same parameter per rule #5
$mergedAandB = @{
    VisibleCmdlets = 'Get-Service',
                     @{ Name = 'Restart-Service'; Parameters = @{ Name = 'DisplayName'; ValidateSet = 'DNS Client', 'DNS Server' } }
}
```



<span data-ttu-id="f6087-229">**VisibleExternalCommands ScriptsToProcess VisibleAliases VisibleProviders,**</span><span class="sxs-lookup"><span data-stu-id="f6087-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span></span>

<span data-ttu-id="f6087-230">Všechna ostatní pole v souboru funkce role se jednoduše přidají do kumulativní sadu povolených externích příkazů, aliasy, poskytovatelů a spouštěcí skripty.</span><span class="sxs-lookup"><span data-stu-id="f6087-230">All other fields in the role capability file are simply added to a cumulative set of allowable external commands, aliases, providers, and startup scripts.</span></span>
<span data-ttu-id="f6087-231">Příkaz, alias, zprostředkovatel nebo skriptu, které jsou k dispozici v jedné role funkce bude k dispozici uživateli JEA.</span><span class="sxs-lookup"><span data-stu-id="f6087-231">Any command, alias, provider, or script available in one role capability will be available to the JEA user.</span></span>

<span data-ttu-id="f6087-232">Dejte pozor, abyste Ujistěte se, že kombinovanou sadu poskytovatelů z jedné role, funkce a rutiny/funkce/příkazy z jiného Nepovolit připojujících se uživatelů neúmyslnému přístupu k systémovým prostředkům.</span><span class="sxs-lookup"><span data-stu-id="f6087-232">Be careful to ensure that the combined set of providers from one role capability and cmdlets/functions/commands from another do not allow connecting users unintentional access to system resources.</span></span>
<span data-ttu-id="f6087-233">Například pokud jedna role umožňuje `Remove-Item` rutina a další umožňuje `FileSystem` poskytovatele, vystavujete se riziku JEA uživatele odstraní libovolné soubory ve vašem počítači.</span><span class="sxs-lookup"><span data-stu-id="f6087-233">For example, if one role allows the `Remove-Item` cmdlet and another allows the `FileSystem` provider, you are at risk of a JEA user deleting arbitrary files on your computer.</span></span>
<span data-ttu-id="f6087-234">Další informace o určení efektivní oprávnění uživatelů najdete v [auditování JEA tématu](audit-and-report.md).</span><span class="sxs-lookup"><span data-stu-id="f6087-234">Additional information about identifying users' effective permissions can be found in the [auditing JEA topic](audit-and-report.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6087-235">Další kroky</span><span class="sxs-lookup"><span data-stu-id="f6087-235">Next steps</span></span>

- [<span data-ttu-id="f6087-236">Vytvoření konfiguračního souboru relace</span><span class="sxs-lookup"><span data-stu-id="f6087-236">Create a session configuration file</span></span>](session-configurations.md)
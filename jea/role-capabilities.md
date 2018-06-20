---
ms.date: 06/12/2017
keywords: jea, prostředí powershell, zabezpečení
title: Možnosti JEA Role
ms.openlocfilehash: 0531baa284e66a42a162329ea20ecfdca6d0b526
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190532"
---
# <a name="jea-role-capabilities"></a><span data-ttu-id="c5bd1-103">Možnosti JEA Role</span><span class="sxs-lookup"><span data-stu-id="c5bd1-103">JEA Role Capabilities</span></span>

> <span data-ttu-id="c5bd1-104">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c5bd1-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="c5bd1-105">Při vytváření koncový bod JEA, budete muset definovat jeden nebo více "role možnosti", které popisují *co* někdo můžete provést v relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-105">When creating a JEA endpoint, you will need to define one or more "role capabilities" which describe *what* someone can do in a JEA session.</span></span>
<span data-ttu-id="c5bd1-106">Funkce role je prostředí PowerShell datový soubor s příponou .psrc obsahující seznam všech rutin, funkce, zprostředkovatele a externí programy, které má být k dispozici až po připojení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-106">A role capability is a PowerShell data file with the .psrc extension that lists all the cmdlets, functions, providers, and external programs that should be made available to connecting users.</span></span>

<span data-ttu-id="c5bd1-107">Toto téma popisuje, jak vytvořit soubor prostředí PowerShell role schopnosti pro vaše uživatele JEA.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-107">This topic describes how to create a PowerShell role capability file for your JEA users.</span></span>

## <a name="determine-which-commands-to-allow"></a><span data-ttu-id="c5bd1-108">Určit, které příkazy umožňující</span><span class="sxs-lookup"><span data-stu-id="c5bd1-108">Determine which commands to allow</span></span>

<span data-ttu-id="c5bd1-109">Prvním krokem při vytváření souboru funkce role, je rozmyslet, co budou uživatelé, kteří mají přiřazenou roli potřebují přístup k.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-109">The first step when creating a role capability file is to consider what the users who are assigned the role will need access to.</span></span>
<span data-ttu-id="c5bd1-110">Požadavky na tento proces shromažďování může chvíli trvat, ale je velmi důležité procesu.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-110">This requirements gathering process can take a while, but it is a very important process.</span></span>
<span data-ttu-id="c5bd1-111">Udělení přístupu uživatelům ke příliš málo rutiny a funkce je můžete zabránit v získání své práci.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-111">Giving users access to too few cmdlets and functions can prevent them from getting their job done.</span></span>
<span data-ttu-id="c5bd1-112">Povolení přístupu k příliš mnoho rutiny a funkce může vést k provádění více, než jste zamýšleli s jejich oprávněními implicitní správce oslabení vaší potřebujete zabezpečení uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-112">Allowing access to too many cmdlets and functions can lead to users doing more than you intended with their implicit admin privileges, weakening your security stance.</span></span>

<span data-ttu-id="c5bd1-113">Jak přejdete o tomto procesu bude záviset na vaší organizace a cíle, ale následující tipy může pomoci zajistit, že jste na správné cestě.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-113">How you go about this process will depend on your organization and goals, however the following tips can help ensure you're on the right path.</span></span>

1. <span data-ttu-id="c5bd1-114">**Identifikovat** příkazy uživatelé používají pro své práci.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-114">**Identify** the commands users are using to get their jobs done.</span></span> <span data-ttu-id="c5bd1-115">To může zahrnovat průzkumu IT oddělení, kontrola skripty pro automatizaci nebo analýza přepisy relace prostředí PowerShell nebo protokoly.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-115">This may involve surveying IT staff, checking automation scripts, or analyzing PowerShell session transcripts or logs.</span></span>
2. <span data-ttu-id="c5bd1-116">**Aktualizace** pomocí nástroje příkazového řádku pro prostředí PowerShell ekvivalenty, kde je to možné, nejlepší auditování a JEA přizpůsobení prostředí.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-116">**Update** use of command line tools to PowerShell equivalents, where possible, for the best auditing and JEA customization experience.</span></span> <span data-ttu-id="c5bd1-117">Externí programy nemůže být omezen jako granularly jako nativní rutiny prostředí PowerShell a funkce v sadě nástrojů JEA.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-117">External programs cannot be constrained as granularly as native PowerShell cmdlets and functions in JEA.</span></span>
3. <span data-ttu-id="c5bd1-118">**Omezit** oboru rutin, pokud nezbytné jenom povolit konkrétní parametry nebo hodnoty parametru.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-118">**Restrict** the scope of the cmdlets if necessary to only allow specific parameters or parameter values.</span></span> <span data-ttu-id="c5bd1-119">To je zvlášť důležité, pokud uživatelé by měli být jenom moct spravovat součást systému.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-119">This is particularly important if users should only be able to manage part of a system.</span></span>
4. <span data-ttu-id="c5bd1-120">**Vytvoření** nahradit komplexní příkazy nebo příkazy, které je obtížné omezit v sadě nástrojů JEA vlastní funkce.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-120">**Create** custom functions to replace complex commands or commands which are difficult to constrain in JEA.</span></span> <span data-ttu-id="c5bd1-121">Jednoduché funkci, která zabalí komplexní příkaz nebo vztahuje další ověřovací logiku nabízí další ovládací prvek pro jednoduchost admins a koncového uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-121">A simple function that wraps a complex command or applies additional validation logic can offer additional control for admins and end-user simplicity.</span></span>
5. <span data-ttu-id="c5bd1-122">**Test** vymezená seznam povolených příkazů s uživatele nebo Automatizace služby a podle potřeby upravte.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-122">**Test** the scoped list of allowable commands with your users and/or automation services and adjust as necessary.</span></span>

<span data-ttu-id="c5bd1-123">Je důležité si pamatovat, že příkazy v relaci JEA jsou často oprávnění spustit s správce (nebo jinak zvýšených oprávnění).</span><span class="sxs-lookup"><span data-stu-id="c5bd1-123">It is important to remember that commands in a JEA session are often run with admin (or otherwise elevated) privileges.</span></span>
<span data-ttu-id="c5bd1-124">Pozor, výběr dostupné příkazy je důležité zajistit, že koncový bod JEA neumožňuje je připojující se uživatel zvýšit svá oprávnění.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-124">Careful selection of available commands is important to ensure the JEA endpoint does not allow the connecting user to elevate their permissions.</span></span>
<span data-ttu-id="c5bd1-125">Níže jsou příklady příkazů, které mohou být používány neoprávněnému pokud povolený neomezeným stavu.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-125">Below are some examples of commands that can be used maliciously if allowed in an unconstrained state.</span></span>
<span data-ttu-id="c5bd1-126">Všimněte si, že to není vyčerpávající seznam a musí být použit pouze jako vytvořených počáteční bod.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-126">Note that this is not an exhaustive list and should only be used as a cautionary starting point.</span></span>

### <a name="examples-of-potentially-dangerous-commands"></a><span data-ttu-id="c5bd1-127">Příklady potenciálně nebezpečná příkazy</span><span class="sxs-lookup"><span data-stu-id="c5bd1-127">Examples of potentially dangerous commands</span></span>

<span data-ttu-id="c5bd1-128">Riziko</span><span class="sxs-lookup"><span data-stu-id="c5bd1-128">Risk</span></span> | <span data-ttu-id="c5bd1-129">Příklad</span><span class="sxs-lookup"><span data-stu-id="c5bd1-129">Example</span></span> | <span data-ttu-id="c5bd1-130">Související příkazy</span><span class="sxs-lookup"><span data-stu-id="c5bd1-130">Related commands</span></span>
-----|---------|-----------------
<span data-ttu-id="c5bd1-131">Udělení oprávnění správce obejít JEA je připojující se uživatel</span><span class="sxs-lookup"><span data-stu-id="c5bd1-131">Granting the connecting user admin privileges to bypass JEA</span></span> | `Add-LocalGroupMember -Member 'CONTOSO\jdoe' -Group 'Administrators'` | <span data-ttu-id="c5bd1-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span><span class="sxs-lookup"><span data-stu-id="c5bd1-132">`Add-ADGroupMember`, `Add-LocalGroupMember`, `net.exe`, `dsadd.exe`</span></span>
<span data-ttu-id="c5bd1-133">Spuštění libovolné kódu, například malware, zneužití nebo vlastní skripty obejít ochrany</span><span class="sxs-lookup"><span data-stu-id="c5bd1-133">Running arbitrary code, such as malware, exploits, or custom scripts to bypass protections</span></span> | `Start-Process -FilePath '\\san\share\malware.exe'` | <span data-ttu-id="c5bd1-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span><span class="sxs-lookup"><span data-stu-id="c5bd1-134">`Start-Process`, `New-Service`, `Invoke-Item`, `Invoke-WmiMethod`, `Invoke-CimMethod`, `Invoke-Expression`, `Invoke-Command`, `New-ScheduledTask`, `Register-ScheduledJob`</span></span>

## <a name="create-a-role-capability-file"></a><span data-ttu-id="c5bd1-135">Vytvořte soubor schopnosti role</span><span class="sxs-lookup"><span data-stu-id="c5bd1-135">Create a role capability file</span></span>

<span data-ttu-id="c5bd1-136">Můžete vytvořit nový soubor schopnosti role prostředí PowerShell s [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-136">You can create a new PowerShell role capability file with the [New-PSRoleCapabilityFile](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSRoleCapabilityFile) cmdlet.</span></span>

```powershell
New-PSRoleCapabilityFile -Path .\MyFirstJEARole.psrc
```

<span data-ttu-id="c5bd1-137">Výsledný soubor schopnosti role lze otevřít v textovém editoru a upravit tak, aby povolit požadované příkazy pro roli.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-137">The resulting role capability file can be opened in a text editor and modified to allow the desired commands for the role.</span></span>
<span data-ttu-id="c5bd1-138">V nápovědě k prostředí PowerShell obsahuje několik příkladů, jak nakonfigurovat soubor.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-138">The PowerShell help documentation contains several examples of how you can configure the file.</span></span>

### <a name="allowing-powershell-cmdlets-and-functions"></a><span data-ttu-id="c5bd1-139">Povolení funkcí a rutiny prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5bd1-139">Allowing PowerShell cmdlets and functions</span></span>

<span data-ttu-id="c5bd1-140">Povolit uživatelům spustit rutiny prostředí PowerShell nebo funkce, přidejte název rutiny nebo funkce na VisbibleCmdlets nebo VisibleFunctions pole.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-140">To authorize users to run PowerShell cmdlets or functions, add the cmdlet or function name to the VisbibleCmdlets or VisibleFunctions fields.</span></span>
<span data-ttu-id="c5bd1-141">Pokud si nejste jisti, zda je příkaz rutiny nebo funkce, můžete spustit `Get-Command <name>` a zkontrolujte vlastnost "CommandType" ve výstupu.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-141">If you aren't sure whether a command is a cmdlet or function, you can run `Get-Command <name>` and check the "CommandType" property in the output.</span></span>

```powershell
VisibleCmdlets = 'Restart-Computer', 'Get-NetIPAddress'
```

<span data-ttu-id="c5bd1-142">Někdy rozsah konkrétní rutiny nebo funkce je příliš široké potřebám vašich uživatelů.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-142">Sometimes the scope of a specific cmdlet or function is too broad for your users' needs.</span></span>
<span data-ttu-id="c5bd1-143">Správce DNS, například pravděpodobně pouze potřebám přístup k restartování služby DNS.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-143">A DNS admin, for example, probably only needs access to restart the DNS service.</span></span>
<span data-ttu-id="c5bd1-144">Prostředí s více klientů, kde klienti mají přístup k nástroje pro správu samoobslužné služby musí být klienti omezená Správa s vlastní prostředky.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-144">In a multi-tenant environment where tenants are granted access to self-service management tools, tenants should be limited to managing with their own resources.</span></span>
<span data-ttu-id="c5bd1-145">U těchto případech můžete omezit, parametry, které jsou zveřejněné z rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-145">For these cases, you can restrict which parameters are exposed from the cmdlet or function.</span></span>

```powershell

VisibleCmdlets = @{ Name = 'Restart-Computer'; Parameters = @{ Name = 'Name' }}

```

<span data-ttu-id="c5bd1-146">V pokročilejších scénářích může také muset omezení hodnot, které můžete zadat někdo na tyto parametry.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-146">In more advanced scenarios, you may also need to restrict which values someone can supply to these parameters.</span></span>
<span data-ttu-id="c5bd1-147">Funkce role umožňují definovat sadu povolených hodnot nebo vzor regulárního výrazu, který se vyhodnotí pro určení, zda daný vstup povolen.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-147">Role capabilities let you define a set of allowed values or a regular expression pattern that is evaluated to determine if a given input is allowed.</span></span>

```powershell
VisibleCmdlets = @{ Name = 'Restart-Service'; Parameters = @{ Name = 'Name'; ValidateSet = 'Dns', 'Spooler' }},
                 @{ Name = 'Start-Website'; Parameters = @{ Name = 'Name'; ValidatePattern = 'HR_*' }}
```

> [!NOTE]
> <span data-ttu-id="c5bd1-148">[Společné parametry prostředí PowerShell](https://technet.microsoft.com/library/hh847884.aspx) jsou vždy povoleny, i v případě, že omezíte dostupné parametry.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-148">The [common PowerShell parameters](https://technet.microsoft.com/library/hh847884.aspx) are always allowed, even if you restrict the available parameters.</span></span>
> <span data-ttu-id="c5bd1-149">Můžete neměl by obsahovat explicitně je v poli parametrů.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-149">You should not explicitly list them in the Parameters field.</span></span>

<span data-ttu-id="c5bd1-150">Následující tabulka popisuje různé způsoby, kterými můžete přizpůsobit viditelné rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-150">The table below describes the various ways you can customize a visible cmdlet or function.</span></span>
<span data-ttu-id="c5bd1-151">Můžete kombinovat a párovat některé z níže VisibleCmdlets pole.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-151">You can mix and match any of the below in the VisibleCmdlets field.</span></span>

<span data-ttu-id="c5bd1-152">Příklad</span><span class="sxs-lookup"><span data-stu-id="c5bd1-152">Example</span></span>                                                                                      | <span data-ttu-id="c5bd1-153">Případ použití</span><span class="sxs-lookup"><span data-stu-id="c5bd1-153">Use case</span></span>
---------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------
<span data-ttu-id="c5bd1-154">`'My-Func'` nebo `@{ Name = 'My-Func' }`</span><span class="sxs-lookup"><span data-stu-id="c5bd1-154">`'My-Func'` or `@{ Name = 'My-Func' }`</span></span>                                                       | <span data-ttu-id="c5bd1-155">Umožňuje uživateli spustit `My-Func` bez jakýchkoli omezení na parametry.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-155">Allows the user to run `My-Func` without any restrictions on the parameters.</span></span>
`'MyModule\My-Func'`                                                                         | <span data-ttu-id="c5bd1-156">Umožňuje uživateli spustit `My-Func` z modulu `MyModule` bez jakýchkoli omezení na parametry.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-156">Allows the user to run `My-Func` from the module `MyModule` without any restrictions on the parameters.</span></span>
`'My-*'`                                                                                     | <span data-ttu-id="c5bd1-157">Umožňuje uživateli spustit všechny rutiny nebo funkce s příkazem `My`.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-157">Allows the user to run any cmdlet or function with the verb `My`.</span></span>
`'*-Func'`                                                                                   | <span data-ttu-id="c5bd1-158">Umožňuje uživateli spustit všechny rutiny nebo funkce s podstatným jménem `Func`.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-158">Allows the user to run any cmdlet or function with the noun `Func`.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'}, @{ Name = 'Param2' }}`               | <span data-ttu-id="c5bd1-159">Umožňuje uživateli spustit `My-Func` s `Param1` nebo `Param2` parametry.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-159">Allows the user to run `My-Func` with the `Param1` and/or `Param2` parameters.</span></span> <span data-ttu-id="c5bd1-160">Na parametry můžete zadat libovolnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-160">Any value can be supplied to the parameters.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidateSet = 'Value1', 'Value2' }}`  | <span data-ttu-id="c5bd1-161">Umožňuje uživateli spustit `My-Func` s `Param1` parametr.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-161">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="c5bd1-162">Pro parametr lze zadat pouze "Hodnota1" a "Hodnota2".</span><span class="sxs-lookup"><span data-stu-id="c5bd1-162">Only "Value1" and "Value2" can be supplied to the parameter.</span></span>
`@{ Name = 'My-Func'; Parameters = @{ Name = 'Param1'; ValidatePattern = 'contoso.*' }}`     | <span data-ttu-id="c5bd1-163">Umožňuje uživateli spustit `My-Func` s `Param1` parametr.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-163">Allows the user to run `My-Func` with the `Param1` parameter.</span></span> <span data-ttu-id="c5bd1-164">Parametru můžete zadat libovolnou hodnotu od "contoso".</span><span class="sxs-lookup"><span data-stu-id="c5bd1-164">Any value starting with "contoso" can be supplied to the parameter.</span></span>


> [!WARNING]
> <span data-ttu-id="c5bd1-165">Osvědčené postupy zabezpečení nedoporučujeme používat zástupné znaky při definování viditelné rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-165">For best security practices, it is not recommended to use wildcards when defining visible cmdlets or functions.</span></span>
> <span data-ttu-id="c5bd1-166">Místo toho byste měli explicitně uvést každého důvěryhodné příkazu k zajištění, že žádné další příkazy, které sdílejí stejné schéma pojmenování jsou neúmyslně oprávnění.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-166">Instead, you should explicitly list each trusted command to ensure no other commands that share the same naming scheme are unintentionally authorized.</span></span>

<span data-ttu-id="c5bd1-167">ValidatePattern i ValidateSet nelze použít na stejné rutiny nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-167">You cannot apply both a ValidatePattern and ValidateSet to the same cmdlet or function.</span></span>

<span data-ttu-id="c5bd1-168">Pokud ano, přepíše ValidatePattern ValidateSet.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-168">If you do, the ValidatePattern will override the ValidateSet.</span></span>

<span data-ttu-id="c5bd1-169">Další informace o ValidatePattern, podívejte se na [to *blogu Hey, Scripting Guy!* post](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) a [prostředí PowerShell regulární výrazy](https://technet.microsoft.com/library/hh847880.aspx) odkazovat na obsah.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-169">For more information about ValidatePattern, check out [this *Hey, Scripting Guy!* post](https://blogs.technet.microsoft.com/heyscriptingguy/2011/01/11/validate-powershell-parameters-before-running-the-script/) and the [PowerShell Regular Expressions](https://technet.microsoft.com/library/hh847880.aspx) reference content.</span></span>

### <a name="allowing-external-commands-and-powershell-scripts"></a><span data-ttu-id="c5bd1-170">Povolení externí příkazy a skripty prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5bd1-170">Allowing external commands and PowerShell scripts</span></span>

<span data-ttu-id="c5bd1-171">Povolit uživatelům spouštět spustitelné soubory a skripty prostředí PowerShell (.ps1) v relaci JEA, budete muset přidat úplnou cestu pro každý program v poli VisibleExternalCommands.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-171">To allow users to run executables and PowerShell scripts (.ps1) in a JEA session, you have to add the full path to each program in the VisibleExternalCommands field.</span></span>

```powershell
VisibleExternalCommands = 'C:\Windows\System32\whoami.exe', 'C:\Program Files\Contoso\Scripts\UpdateITSoftware.ps1'
```

<span data-ttu-id="c5bd1-172">Doporučujeme, kde je to možné, používat ekvivalenty rutiny nebo funkce prostředí PowerShell externí spustitelné soubory, které autorizujete vzhledem k tomu, že budete mít kontrolu nad niž jsou povolené parametry pomocí rutin prostředí PowerShell nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-172">It is advised, where possible, to use PowerShell cmdlet/function equivalents of any external executables you authorize since you have control over which parameters are allowed with PowerShell cmdlets/functions.</span></span>

<span data-ttu-id="c5bd1-173">Mnoho spustitelných souborů umožňují číst aktuální stav a pak ji změňte právě tím, že poskytuje různé parametry.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-173">Many executables allow you to both read the current state and then change it just by providing different parameters.</span></span>

<span data-ttu-id="c5bd1-174">Představte si třeba roli správce na serveru soubor, který chce zkontrolujte, které síťové sdílené složky jsou hostované v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-174">For example, consider the role of a file server admin who wants to check which network shares are hosted by the local machine.</span></span>
<span data-ttu-id="c5bd1-175">Jeden způsob kontroly je použití `net share`.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-175">One way to check is to use `net share`.</span></span>
<span data-ttu-id="c5bd1-176">Však umožňuje net.exe je velmi nebezpečné, protože správce stejným způsobem použít příkaz k získání oprávnění správce s `net group Administrators unprivilegedjeauser /add`.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-176">However, allowing net.exe is very dangerous becuase the admin could just as easily use the command to gain admin privileges with `net group Administrators unprivilegedjeauser /add`.</span></span>
<span data-ttu-id="c5bd1-177">Lepším řešením je povolit [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) která dosáhne stejného výsledku, ale má mnohem omezenější obor.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-177">A better approach is to allow [Get-SmbShare](https://technet.microsoft.com/library/jj635704.aspx) which achieves the same result but has a much more limited scope.</span></span>

<span data-ttu-id="c5bd1-178">Při provádění externích příkazů k dispozici uživatelům v relaci JEA, vždycky zadejte úplnou cestu ke spustitelnému souboru, aby nebudou program s podobným názvem (a potenciálně malicous) umístěny jinde v systému místo provedeny.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-178">When making external commands available to users in a JEA session, always specify the complete path to the executable to ensure a similarly named (and potentially malicous) program placed elsewhere on the system does not get executed instead.</span></span>

### <a name="allowing-access-to-powershell-providers"></a><span data-ttu-id="c5bd1-179">Povolení přístupu k zprostředkovatelé prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5bd1-179">Allowing access to PowerShell providers</span></span>

<span data-ttu-id="c5bd1-180">Ve výchozím nastavení jsou k dispozici v relacích JEA žádní zprostředkovatelé prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-180">By default, no PowerShell providers are available in JEA sessions.</span></span>

<span data-ttu-id="c5bd1-181">Toto je primárně pro snížení rizika citlivé informace a nastavení konfigurace, které se budou mít přístup k připojování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-181">This is primarily to reduce the risk of sensitive information and configuration settings being disclosed to the connecting user.</span></span>

<span data-ttu-id="c5bd1-182">Pokud je to nezbytné, můžete povolit přístup k poskytovateli prostředí PowerShell pomocí `VisibleProviders` příkaz.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-182">When necessary, you can allow access to the PowerShell providers using the `VisibleProviders` command.</span></span>
<span data-ttu-id="c5bd1-183">Úplný seznam poskytovatelů, spouštění `Get-PSProvider`.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-183">For a full list of providers, run `Get-PSProvider`.</span></span>

```powershell
VisibleProviders = 'Registry'
```

<span data-ttu-id="c5bd1-184">Jednoduché úlohy, které vyžadují přístup k systému souborů, registru, úložiště certifikátů nebo jiných citlivých poskytovatelů byste také zvážit, zápis vlastní funkci, která funguje s poskytovatelem jménem uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-184">For simple tasks that require access to the file system, registry, certificate store, or other sensitive providers, you can also consider writing a custom function that works with the provider on the user's behalf.</span></span>
<span data-ttu-id="c5bd1-185">Funkce, rutiny a externí programy, které jsou k dispozici v relaci JEA nejsou stejné omezující jako JEA – získají přístup k libovolného zprostředkovatele ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-185">Functions, cmdlets, and external programs that are available in a JEA session are not subject to the same constraints as JEA -- they can access any provider by default.</span></span>
<span data-ttu-id="c5bd1-186">Také zvažte použití [uživatele jednotky](session-configurations.md#user-drive) při kopírování souborů do nebo z koncového bodu JEA je požadovaná.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-186">Also consider using the [user drive](session-configurations.md#user-drive) when copying files to/from a JEA endpoint is required.</span></span>

### <a name="creating-custom-functions"></a><span data-ttu-id="c5bd1-187">Vytvoření vlastní funkce</span><span class="sxs-lookup"><span data-stu-id="c5bd1-187">Creating custom functions</span></span>

<span data-ttu-id="c5bd1-188">Můžete vytvářet vlastní funkce v souboru schopnosti role ke zjednodušení složité úlohy pro koncové uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-188">You can author custom functions in a role capability file to simplify complex tasks for your end users.</span></span>
<span data-ttu-id="c5bd1-189">Vlastní funkce jsou také užitečné, pokud požadujete pokročilé ověřovací logiku pro hodnoty parametru rutiny.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-189">Custom functions are also useful when you require advanced validation logic for cmdlet parameter values.</span></span>
<span data-ttu-id="c5bd1-190">Psát jednoduché funkce **FunctionDefinitions** pole:</span><span class="sxs-lookup"><span data-stu-id="c5bd1-190">You can write simple functions in the **FunctionDefinitions** field:</span></span>

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
> <span data-ttu-id="c5bd1-191">Nezapomeňte přidat název své vlastní funkce pro **VisibleFunctions** pole proto může být spuštěna uživatelem JEA.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-191">Don't forget to add the name of your custom functions to the **VisibleFunctions** field so they can be run by the JEA users.</span></span>


<span data-ttu-id="c5bd1-192">Text (bloku skriptu) vlastní funkce se spustí v režimu výchozí jazyk pro systém a nevztahují na JEA jazyková omezení.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-192">The body (script block) of custom functions runs in the default language mode for the system and is not subject to JEA's language constraints.</span></span>
<span data-ttu-id="c5bd1-193">To znamená, že funkce můžete přístup k systému souborů a registr a spustit příkazy, které nebyly v souboru schopnosti role dostupná.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-193">This means that functions can access the file system and registry, and run commands that were not made visible in the role capability file.</span></span>
<span data-ttu-id="c5bd1-194">Ujistěte se, aby se zabránilo povolení libovolný kód ke spuštění při použití parametrů a vyhnout se vstup uživatele zřetězení přímo do rutiny jako `Invoke-Expression`.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-194">Take care to avoid allowing arbitrary code to be run when using parameters and avoid piping user input directly into cmdlets like `Invoke-Expression`.</span></span>

<span data-ttu-id="c5bd1-195">Ve výše uvedeném příkladu bude zjistíte, že název plně kvalifikovaného modulu (FQMN) `Microsoft.PowerShell.Utility\Select-Object` byl použit místo zkrácený `Select-Object`.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-195">In the above example, you will notice that the fully qualified module name (FQMN) `Microsoft.PowerShell.Utility\Select-Object` was used instead of the shorthand `Select-Object`.</span></span>
<span data-ttu-id="c5bd1-196">Funkce definované v souborech schopnosti role se stále vztahují oboru JEA relace, která zahrnuje funkce proxy JEA vytvoří omezit existující příkazy.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-196">Functions defined in role capability files are still subject to the scope of JEA sessions, which includes the proxy functions JEA creates to constrain existing commands.</span></span>

<span data-ttu-id="c5bd1-197">Select-Object je výchozí, omezené rutinu v všechny JEA relace, která neumožňuje můžete vybrat libovolný vlastnosti u objektů.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-197">Select-Object is a default, constrained cmdlet in all JEA sessions that doesn't allow you to select arbitrary properties on objects.</span></span>
<span data-ttu-id="c5bd1-198">Pokud chcete používat funkce neomezeným Select-Object, musíte explicitně požádat o úplnou implementaci, zadáním FQMN.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-198">To use the unconstrained Select-Object in functions, you must explicitly request the full implementation by specifying the FQMN.</span></span>
<span data-ttu-id="c5bd1-199">Všechny rutiny omezené v relaci JEA bude mít květy stejné chování při vyvolání z funkce, souladu Powershellu [příkaz přednost před](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span><span class="sxs-lookup"><span data-stu-id="c5bd1-199">Any constrained cmdlet in a JEA session will exhibit the same behavior when invoked from a function, in line with PowerShell's [command precedence](https://msdn.microsoft.com/en-us/powershell/reference/3.0/microsoft.powershell.core/about/about_command_precedence).</span></span>

<span data-ttu-id="c5bd1-200">Pokud píšete spoustu vlastní funkce, může být snazší jejich umístění [modulu skriptu prostředí PowerShell](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="c5bd1-200">If you are writing a lot of custom functions, it may be easier to put them in a [PowerShell Script Module](https://msdn.microsoft.com/en-us/library/dd878340(v=vs.85).aspx).</span></span>
<span data-ttu-id="c5bd1-201">Pak můžete provést tyto funkce viditelné v relaci JEA pomocí pole VisibleFunctions jako s moduly předdefinované a třetích stran.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-201">You can then make those functions visible in the JEA session using the VisibleFunctions field like you would with built-in and third party modules.</span></span>

## <a name="place-role-capabilities-in-a-module"></a><span data-ttu-id="c5bd1-202">Umístěte role funkce v modulu</span><span class="sxs-lookup"><span data-stu-id="c5bd1-202">Place role capabilities in a module</span></span>

<span data-ttu-id="c5bd1-203">Aby PowerShell najít soubor funkce role musí být uložen ve složce "RoleCapabilities" v modulu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-203">In order for PowerShell to find a role capability file, it must be stored in a "RoleCapabilities" folder in a PowerShell module.</span></span>
<span data-ttu-id="c5bd1-204">Modul můžou být uložená v libovolné složky součástí `$env:PSModulePath` proměnné prostředí, ale neměli umístěte do System32 (vyhrazené pro integrované moduly) nebo do složky kde nedůvěryhodná, připojení uživatelů může upravit soubory.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-204">The module can be stored in any folder included in the `$env:PSModulePath` environment variable, however you should not place it in System32 (reserved for built-in modules) or a folder where the untrusted, connecting users could modify the files.</span></span>
<span data-ttu-id="c5bd1-205">Dole je příklad vytvoření základní modul skriptu prostředí PowerShell s názvem *ContosoJEA* v cestě "Program Files".</span><span class="sxs-lookup"><span data-stu-id="c5bd1-205">Below is an example of creating a basic PowerShell script module called *ContosoJEA* in the "Program Files" path.</span></span>

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

<span data-ttu-id="c5bd1-206">V tématu [pochopení modul PowerShell](https://msdn.microsoft.com/en-us/library/dd878324.aspx) Další informace o moduly, modul manifesty a proměnnou prostředí PSModulePath prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-206">See [Understanding a PowerShell Module](https://msdn.microsoft.com/en-us/library/dd878324.aspx) for more information about PowerShell modules, module manifests, and the PSModulePath environment variable.</span></span>

## <a name="updating-role-capabilities"></a><span data-ttu-id="c5bd1-207">Aktualizace role možnosti</span><span class="sxs-lookup"><span data-stu-id="c5bd1-207">Updating role capabilities</span></span>


<span data-ttu-id="c5bd1-208">Soubor schopnosti role můžete kdykoli aktualizovat jednoduše ukládání změn do souboru funkce role.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-208">You can update a role capability file at any time by simply saving changes to the role capability file.</span></span>
<span data-ttu-id="c5bd1-209">Všechny nové relace JEA spustit po aktualizaci schopnosti role se projeví revidovaný možnosti.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-209">Any new JEA sessions started after the role capability has been updated will reflect the revised capabilities.</span></span>

<span data-ttu-id="c5bd1-210">Z tohoto důvodu řízení přístupu ke složce Možnosti role je tak důležité.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-210">This is why controlling access to the role capabilities folder is so important.</span></span>
<span data-ttu-id="c5bd1-211">Pouze vysoce důvěryhodných správců, byste měli mít měnit soubory funkce role.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-211">Only highly trusted administrators should be able to change role capability files.</span></span>
<span data-ttu-id="c5bd1-212">Pokud nedůvěryhodné uživatel může změnit soubory funkce role, můžete snadno uvedou sami přístup do rutin, které mohly zvýšit jejich oprávnění.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-212">If an untrusted user can change role capability files, they can easily give themselves access to cmdlets which allow them to elevate their privileges.</span></span>


<span data-ttu-id="c5bd1-213">Pro správce chtějí uzamčení přístup k funkcím role zajistěte, aby že místní systém má přístup pro čtení k souborům schopnosti role a obsahující moduly.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-213">For administrators looking to lock down access to the role capabilities, ensure Local System has read access to the role capability files and containing modules.</span></span>

## <a name="how-role-capabilities-are-merged"></a><span data-ttu-id="c5bd1-214">Způsob role možnosti sloučení</span><span class="sxs-lookup"><span data-stu-id="c5bd1-214">How role capabilities are merged</span></span>

<span data-ttu-id="c5bd1-215">Uživatele můžete mít udělen přístup k více možností role při jejich zadejte JEA relaci v závislosti na roli mapování na [relace konfigurační soubor](session-configurations.md).</span><span class="sxs-lookup"><span data-stu-id="c5bd1-215">Users can be granted access to multiple role capabilities when they enter a JEA session depending on the role mappings in the [session configuration file](session-configurations.md).</span></span>
<span data-ttu-id="c5bd1-216">V takovém případě se pokusí uživateli přidělit JEA *nejvíce projektovou* sadu příkazů, které jsou povolené žádné role.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-216">When this happens, JEA tries to give the user the *most permissive* set of commands allowed by any of the roles.</span></span>

<span data-ttu-id="c5bd1-217">**VisibleCmdlets a VisibleFunctions**</span><span class="sxs-lookup"><span data-stu-id="c5bd1-217">**VisibleCmdlets and VisibleFunctions**</span></span>

<span data-ttu-id="c5bd1-218">Většina komplexní logiku sloučení ovlivňuje rutiny a funkce, což může mít jejich parametrů a hodnoty parametrů v sadě nástrojů JEA omezené.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-218">The most complex merge logic affects cmdlets and functions, which can have their parameters and parameter values limited in JEA.</span></span>

<span data-ttu-id="c5bd1-219">Pravidla jsou následující:</span><span class="sxs-lookup"><span data-stu-id="c5bd1-219">The rules are as follows:</span></span>

1. <span data-ttu-id="c5bd1-220">Pokud rutiny jsou dostupná pouze v jedné role, bude viditelné pro uživatele s omezeními použít parametr.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-220">If a cmdlet is only made visible in one role, it will be visible to the user with any applicable parameter constraints.</span></span>
2. <span data-ttu-id="c5bd1-221">Pokud rutiny jsou dostupná ve více než jedné role, a Každá role má stejné omezení u rutinu, bude rutina viditelné pro uživatele s těmito omezeními.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-221">If a cmdlet is made visible in more than one role, and each role has the same constraints on the cmdlet, the cmdlet will be visible to the user with those constraints.</span></span>
3. <span data-ttu-id="c5bd1-222">Pokud rutiny jsou dostupná ve více než jedné role, a každou roli umožňuje jinou sadu parametrů, rutiny a všechny parametry definované v každé role budou viditelné pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-222">If a cmdlet is made visible in more than one role, and each role allows a different set of parameters, the cmdlet and all of the parameters defined across every role will be visible to the user.</span></span> <span data-ttu-id="c5bd1-223">Pokud jednu roli nemá omezení pro parametry, budou mít povolený všechny parametry.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-223">If one role doesn't have constraints on the parameters, all parameters will be allowed.</span></span>
4. <span data-ttu-id="c5bd1-224">Pokud jedna role definuje sadu ověřením nebo ověřením vzor pro parametr rutiny, a jinou roli umožňuje parametr, ale neuvádělo hodnoty parametrů, ověřit sady nebo vzor se budou ignorovat.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-224">If one role defines a validate set or validate pattern for a cmdlet parameter, and the other role allows the parameter but does not constrain the parameter values, the validate set or pattern will be ignored.</span></span>
5. <span data-ttu-id="c5bd1-225">Pokud sadu ověřením definovaná pro parametr rutiny ve více než jedné role, všechny hodnoty ze všech sad ověřením bude možné.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-225">If a validate set is defined for the same cmdlet parameter in more than one role, all values from all validate sets will be allowed.</span></span>
6. <span data-ttu-id="c5bd1-226">Pokud vzor ověřením definovaná pro parametr rutiny ve více než jedné role, všechny hodnoty, které odpovídají některé vzory bude možné.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-226">If a validate pattern is defined for the same cmdlet parameter in more than one role, any values that match any of the patterns will be allowed.</span></span>
7. <span data-ttu-id="c5bd1-227">Pokud sadu ověřením je definována v jedné nebo více rolí, a ověřit vzor je definována v jiné role pro parametr stejné rutiny, je ignorován sadu ověřením a pravidlo (6) se vztahuje na zbývající vzory ověřením.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-227">If a validate set is defined in one or more roles, and a validate pattern is defined in another role for the same cmdlet parameter, the validate set is ignored and rule (6) applies to the remaining validate patterns.</span></span>

<span data-ttu-id="c5bd1-228">Dole je příklad způsob sloučení rolí podle těchto pravidel:</span><span class="sxs-lookup"><span data-stu-id="c5bd1-228">Below is an example of how roles are merged according to these rules:</span></span>

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



<span data-ttu-id="c5bd1-229">**VisibleExternalCommands ScriptsToProcess VisibleAliases, VisibleProviders,**</span><span class="sxs-lookup"><span data-stu-id="c5bd1-229">**VisibleExternalCommands, VisibleAliases, VisibleProviders, ScriptsToProcess**</span></span>

<span data-ttu-id="c5bd1-230">Všechna pole v souboru schopnosti role jsou jednoduše přidat do kumulativní sadu povolených externích příkazů, aliasy, poskytovatelů a spouštění skriptů.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-230">All other fields in the role capability file are simply added to a cumulative set of allowable external commands, aliases, providers, and startup scripts.</span></span>
<span data-ttu-id="c5bd1-231">Příkaz, alias, zprostředkovatele nebo skriptu, které jsou k dispozici v jedné role funkce bude k dispozici pro uživatele JEA.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-231">Any command, alias, provider, or script available in one role capability will be available to the JEA user.</span></span>

<span data-ttu-id="c5bd1-232">Dávejte pozor, abyste ověřili, že kombinovanou sadu zprostředkovatelů z jednoho schopnosti role a rutiny nebo funkce nebo příkazy z jiné neumožňuje, aby uživatelé připojující neúmyslnému přístupu k systémovým prostředkům.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-232">Be careful to ensure that the combined set of providers from one role capability and cmdlets/functions/commands from another do not allow connecting users unintentional access to system resources.</span></span>
<span data-ttu-id="c5bd1-233">Například, pokud umožňuje jednu roli `Remove-Item` rutina a jiné umožňuje `FileSystem` poskytovatele, jsou hrozí JEA uživatel odstraní libovolné soubory ve vašem počítači.</span><span class="sxs-lookup"><span data-stu-id="c5bd1-233">For example, if one role allows the `Remove-Item` cmdlet and another allows the `FileSystem` provider, you are at risk of a JEA user deleting arbitrary files on your computer.</span></span>
<span data-ttu-id="c5bd1-234">Další informace o identifikaci skutečná oprávnění uživatelů lze najít v [auditování JEA tématu](audit-and-report.md).</span><span class="sxs-lookup"><span data-stu-id="c5bd1-234">Additional information about identifying users' effective permissions can be found in the [auditing JEA topic](audit-and-report.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5bd1-235">Další kroky</span><span class="sxs-lookup"><span data-stu-id="c5bd1-235">Next steps</span></span>

- [<span data-ttu-id="c5bd1-236">Vytvoření konfiguračního souboru relace</span><span class="sxs-lookup"><span data-stu-id="c5bd1-236">Create a session configuration file</span></span>](session-configurations.md)
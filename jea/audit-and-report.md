---
ms.date: 06/12/2017
keywords: jea, powershell, zabezpečení
title: Auditování a vytváření sestav funkce jea
ms.openlocfilehash: 2388c735840d8d3683aa8bc9869b9fb0371e5902
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851216"
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="df689-103">Auditování a vytváření sestav funkce jea</span><span class="sxs-lookup"><span data-stu-id="df689-103">Auditing and Reporting on JEA</span></span>

> <span data-ttu-id="df689-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="df689-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="df689-105">Po nasazení funkce JEA, budete pravidelně auditujte konfigurace JEA.</span><span class="sxs-lookup"><span data-stu-id="df689-105">After you've deployed JEA, you will want to regularly audit the JEA configuration.</span></span>
<span data-ttu-id="df689-106">To vám pomůže vyhodnotit správných lidí máte přístup ke koncovému bodu JEA a pokud jsou stále vhodné jejich přiřazených rolí.</span><span class="sxs-lookup"><span data-stu-id="df689-106">This will help you assess if the correct people have access to the JEA endpoint and if their assigned roles are still appropriate.</span></span>

<span data-ttu-id="df689-107">Toto téma popisuje různé způsoby, jak je můžete auditovat koncového bodu JEA.</span><span class="sxs-lookup"><span data-stu-id="df689-107">This topic describes the various ways you can audit a JEA endpoint.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="df689-108">Najít registrovaný JEA relace na počítači</span><span class="sxs-lookup"><span data-stu-id="df689-108">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="df689-109">Chcete-li zkontrolovat, které JEA relací jsou registrované na počítači, použijte [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="df689-109">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

<span data-ttu-id="df689-110">Efektivní oprávnění pro koncový bod služby jsou uvedeny ve vlastnosti "Oprávnění".</span><span class="sxs-lookup"><span data-stu-id="df689-110">The effective rights for the endpoint are listed in the "Permission" property.</span></span>
<span data-ttu-id="df689-111">Tito uživatelé mají práva k připojení ke koncovému bodu JEA, ale které role (a při rozšíření i pro příkazy) ke kterým mají přístup se určuje podle pole "RoleDefinitions" v [relace konfigurační soubor](session-configurations.md) , která byla použita k registraci koncový bod.</span><span class="sxs-lookup"><span data-stu-id="df689-111">These users have the right to connect to the JEA endpoint, but which roles (and, by extension, commands) they have access to is determined by the "RoleDefinitions" field in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span>

<span data-ttu-id="df689-112">Můžete si vyzkoušet mapování role v registrovaných koncového bodu JEA tak, že rozbalíte data ve vlastnosti "RoleDefinitions".</span><span class="sxs-lookup"><span data-stu-id="df689-112">You can evaluate the role mappings in a registered JEA endpoint by expanding the data in the "RoleDefinitions" property.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="df689-113">Hledání funkcí role k dispozici na počítači</span><span class="sxs-lookup"><span data-stu-id="df689-113">Find available role capabilities on the machine</span></span>

<span data-ttu-id="df689-114">Soubory pro funkce role pouze použije JEA v případě jsou uložené ve složce "RoleCapabilities" na platný modul prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df689-114">Role capability files will only be used by JEA if they are stored in a "RoleCapabilities" folder inside a valid PowerShell module.</span></span>
<span data-ttu-id="df689-115">Všechny role funkce k dispozici v počítači najdete tak, že seznam dostupných modulů.</span><span class="sxs-lookup"><span data-stu-id="df689-115">You can find all role capabilities available on a computer by searching the list of available modules.</span></span>

```powershell
function Find-LocalRoleCapability {
    $results = @()

    # Find modules with a "RoleCapabilities" subfolder and add any PSRC files to the result set
    Get-Module -ListAvailable | ForEach-Object {
        $psrcpath = Join-Path -Path $_.ModuleBase -ChildPath 'RoleCapabilities'
        if (Test-Path $psrcpath) {
            $results += Get-ChildItem -Path $psrcpath -Filter *.psrc
        }
    }

    # Format the results nicely to make it easier to read
    $results | Select-Object @{ Name = 'Name'; Expression = { $_.Name.TrimEnd('.psrc') }}, @{ Name = 'Path'; Expression = { $_.FullName }} | Sort-Object Name
}
```

> [!NOTE]
> <span data-ttu-id="df689-116">Pořadí výsledky z této funkce není nutně pořadí, ve kterém bude vybrána funkce rolí, pokud více funkcí role sdílely stejný název.</span><span class="sxs-lookup"><span data-stu-id="df689-116">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="df689-117">Zkontrolujte efektivní oprávnění pro konkrétního uživatele</span><span class="sxs-lookup"><span data-stu-id="df689-117">Check effective rights for a specific user</span></span>

<span data-ttu-id="df689-118">Po nastavení koncového bodu JEA můžete chtít zkontrolovat, které příkazy v relaci JEA jsou k dispozici pro konkrétního uživatele.</span><span class="sxs-lookup"><span data-stu-id="df689-118">Once you have set up a JEA endpoint, you may want to check which commands are available to a specific user in a JEA session.</span></span>
<span data-ttu-id="df689-119">Můžete použít [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) výčet všech příkazů pro uživatele by šlo spustit relaci JEA s jejich aktuální členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="df689-119">You can use [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) to enumerate all of the commands applicable to a user if they were to start a JEA session with their current group memberships.</span></span>
<span data-ttu-id="df689-120">Výstup `Get-PSSessionCapability` stejná jako zadaný uživatel spustí `Get-Command -CommandType All` v relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="df689-120">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="df689-121">Pokud uživatelé nejsou trvalé členy skupin, které by jim udělit další práva JEA, tuto rutinu nemusí odrážet tato další oprávnění.</span><span class="sxs-lookup"><span data-stu-id="df689-121">If your users are not permanent members of groups which would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span>
<span data-ttu-id="df689-122">To je obvykle tak při použití systémů správy privilegovaného přístupu just-in-time umožníte uživatelům dočasně patřit do skupiny zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="df689-122">This is typically the case when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span>
<span data-ttu-id="df689-123">Vždy pečlivě vyhodnoťte mapování uživatelů k rolím a obsah rolí, které se ujistěte se, že uživatelé jsou pouze získal přístup k minimální množství potřeba úspěšně vykonávat svoji práci.</span><span class="sxs-lookup"><span data-stu-id="df689-123">Always carefully evaluate the mapping of users to roles and the contents of each role to ensure users are only getting access to the least amount of commands needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="df689-124">Protokoly událostí prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="df689-124">PowerShell event logs</span></span>

<span data-ttu-id="df689-125">Pokud jste povolili modul a/nebo skript blokování protokolování v systému, budete moci vyhledat události v protokolu událostí Windows pro každý příkaz, který uživatel spustili v jejich JEA relace.</span><span class="sxs-lookup"><span data-stu-id="df689-125">If you enabled module and/or script block logging on the system, you will be able to find events in the Windows event logs for each command a user ran in their JEA sessions.</span></span>
<span data-ttu-id="df689-126">K vyhledání těchto událostí, otevřete Prohlížeč událostí Windows, přejděte na **Microsoft-Windows-PowerShell/Operational** protokolu událostí a vyhledejte události s ID události **4104**.</span><span class="sxs-lookup"><span data-stu-id="df689-126">To find these events, open the Windows Event Viewer, navigate to the **Microsoft-Windows-PowerShell/Operational** event log, and look for events with event ID **4104**.</span></span>

<span data-ttu-id="df689-127">Každá položka protokolu událostí budou zahrnovat informace o relaci, ve kterém jste příkaz spustili.</span><span class="sxs-lookup"><span data-stu-id="df689-127">Each event log entry will include information about the session in which the command was run.</span></span>
<span data-ttu-id="df689-128">JEA relacích, to obsahuje důležité informace o **ConnectedUser**, což je skutečné uživatele, který vytvořil JEA relace, stejně jako **Spustit_jako_uživatel** který identifikuje účet používaný JEA k Spusťte příkaz.</span><span class="sxs-lookup"><span data-stu-id="df689-128">For JEA sessions, this includes important information about the **ConnectedUser**, which is the actual user who created the JEA session, as well as the **RunAsUser** which identifies the account JEA used to execute the command.</span></span>
<span data-ttu-id="df689-129">Protokoly událostí aplikace se zobrazí změny podle Spustit_jako_uživatel, takže nutnosti přepisů nebo povoleno protokolování modulu/script je důležité mít možnost vysledovat vyvolání konkrétní příkaz zpět na uživatele.</span><span class="sxs-lookup"><span data-stu-id="df689-129">Application event logs will show changes being made by the RunAsUser, so having transcripts or module/script logging enabled is crucial to be able to trace a specific command invocation back to a user.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="df689-130">Protokoly událostí aplikace</span><span class="sxs-lookup"><span data-stu-id="df689-130">Application event logs</span></span>

<span data-ttu-id="df689-131">Při spuštění příkazu v relaci JEA vstupující do interakce s externí aplikace nebo služba může tyto aplikace protokolování událostí ve službě vlastní protokoly událostí.</span><span class="sxs-lookup"><span data-stu-id="df689-131">When you run a command in a JEA session that interacts with an external application or service, those applications may log events to their own event logs.</span></span>
<span data-ttu-id="df689-132">Na rozdíl od Powershellu protokoly a záznamy o studiu jiné mechanismy protokolování nebude zachytávat připojeného uživatele relace JEA a místo toho pouze zaznamená virtuálního uživatele spustit jako nebo účet skupiny spravované služby.</span><span class="sxs-lookup"><span data-stu-id="df689-132">Unlike PowerShell logs and transcripts, other logging mechanisms will not capture the connected user of the JEA session, and will instead only log the virtual run-as user or group managed service account.</span></span>
<span data-ttu-id="df689-133">Aby bylo možné zjistit, kdo spustil příkaz, musíte poradit [relace přepisu](#session-transcripts) nebo prostředí PowerShell protokoly událostí je možné korelovat s čas a prostředky uživatele zobrazeného v protokolu událostí aplikace.</span><span class="sxs-lookup"><span data-stu-id="df689-133">In order to determine who ran the command, you will need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="df689-134">Služba WinRM protokol také vám může pomoci sladit spustit jako uživatele v protokolu událostí aplikace s připojující se uživatel.</span><span class="sxs-lookup"><span data-stu-id="df689-134">The WinRM log can also help you correlate run as users in an application event log with the connecting user.</span></span>
<span data-ttu-id="df689-135">ID události **193** v **vzdálené správy Microsoft-Windows-Windows/Operational** protokolování záznamů identifikátor zabezpečení (SID) a účet název připojení na uživatele a spusťte jako uživatel pokaždé, když JEA je vytvořena relace.</span><span class="sxs-lookup"><span data-stu-id="df689-135">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user every time a JEA session is created.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="df689-136">Záznamy o studiu relace</span><span class="sxs-lookup"><span data-stu-id="df689-136">Session transcripts</span></span>

<span data-ttu-id="df689-137">Pokud jste nakonfigurovali JEA řádné záznamy o studiu vytvořit pro každou relaci uživatele, text kopie každé uživatelské akce se uloží do zadané složky.</span><span class="sxs-lookup"><span data-stu-id="df689-137">If you configured JEA to create a transcript for each user session, a text copy of every user's actions will be stored in the specified folder.</span></span>

<span data-ttu-id="df689-138">Chcete-li najít všechny adresáře přepisu, spusťte následující příkaz jako správce na počítači nakonfigurované JEA:</span><span class="sxs-lookup"><span data-stu-id="df689-138">To find all transcript directories, run the following command as an administrator on the computer configured with JEA:</span></span>

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="df689-139">Každý přepisu se spustí s informacemi o čas spuštění relace, který uživatel připojený k relaci a která identita JEA byl přiřazen k nim.</span><span class="sxs-lookup"><span data-stu-id="df689-139">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="df689-140">V těle přepisu zaznamenaných informací o jednotlivých příkazech, které uživatel vyvolat.</span><span class="sxs-lookup"><span data-stu-id="df689-140">In the body of the transcript, information is logged about each command the user invoked.</span></span>
<span data-ttu-id="df689-141">Syntaxe příkazu, který spustil uživatel není k dispozici v relacích JEA kvůli způsobu, jakým jsou transformovány příkazy pro vzdálenou komunikaci prostředí PowerShell, ale stále můžete určit, účinný příkaz, který se spustil.</span><span class="sxs-lookup"><span data-stu-id="df689-141">The exact syntax of the command the user ran is unavailable in JEA sessions due to the way commands are transformed for PowerShell remoting, however you can still determine the effective command that was executed.</span></span>
<span data-ttu-id="df689-142">Níže je přepisu příklad fragmentu kódu od uživatele s `Get-Service Dns` v relaci JEA:</span><span class="sxs-lookup"><span data-stu-id="df689-142">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="df689-143">Pro každý příkaz, který uživatel spustí "CommandInvocation" řádku, bude napsán, popisující rutina nebo funkce uživatel vyvolat.</span><span class="sxs-lookup"><span data-stu-id="df689-143">For each command a user runs, a "CommandInvocation" line will be written, describing the cmdlet or function the user invoked.</span></span>
<span data-ttu-id="df689-144">ParameterBindings postupujte podle jednotlivých CommandInvocation oznámením o každý parametr a hodnotu, která byla zadána pomocí příkazu.</span><span class="sxs-lookup"><span data-stu-id="df689-144">ParameterBindings follow each CommandInvocation to tell you about each parameter and value that was supplied with the command.</span></span>
<span data-ttu-id="df689-145">V příkladu výše uvidíte, že zadaný parametr, který byl "Name" hodnota "Dns" pro rutinu "Get-Service".</span><span class="sxs-lookup"><span data-stu-id="df689-145">In the above example, you can see that the parameter "Name" was supplied the value "Dns" for the "Get-Service" cmdlet.</span></span>

<span data-ttu-id="df689-146">Výstupní každý příkaz, spustí se tím taky CommandInvocation, obvykle na out-Buffer: výchozí.</span><span class="sxs-lookup"><span data-stu-id="df689-146">The output of each command will also trigger a CommandInvocation, usually to Out-Default.</span></span>
<span data-ttu-id="df689-147">InputObject Out-Default je vrácenou příkazem Objekt prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df689-147">The InputObject of Out-Default is the PowerShell object returned from the command.</span></span>
<span data-ttu-id="df689-148">Podrobnosti tohoto objektu jsou zobrazeny po zadání několika řádků níže, úzce tak napodobuje co byste viděli uživatele.</span><span class="sxs-lookup"><span data-stu-id="df689-148">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="df689-149">Viz taky</span><span class="sxs-lookup"><span data-stu-id="df689-149">See also</span></span>

- [<span data-ttu-id="df689-150">*Prostředí PowerShell ♥ modrý tým* blogový příspěvek o zabezpečení</span><span class="sxs-lookup"><span data-stu-id="df689-150">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

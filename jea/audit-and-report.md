---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, prostředí powershell, zabezpečení"
title: "Auditování a vytváření sestav na JEA"
ms.openlocfilehash: 60bc7a4213c75735628207bb21078bf90f7b1ca3
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="cb427-103">Auditování a vytváření sestav na JEA</span><span class="sxs-lookup"><span data-stu-id="cb427-103">Auditing and Reporting on JEA</span></span>

> <span data-ttu-id="cb427-104">Platí pro: prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="cb427-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="cb427-105">Poté, co nasadíte JEA, budete chtít pravidelně audit JEA konfigurace.</span><span class="sxs-lookup"><span data-stu-id="cb427-105">After you've deployed JEA, you will want to regularly audit the JEA configuration.</span></span>
<span data-ttu-id="cb427-106">To vám pomůže vyhodnotit, pokud oprávnění uživatelé mají přístup ke koncovému bodu JEA a jejich přiřazené role jsou stále vhodné.</span><span class="sxs-lookup"><span data-stu-id="cb427-106">This will help you assess if the correct people have access to the JEA endpoint and if their assigned roles are still appropriate.</span></span>

<span data-ttu-id="cb427-107">Toto téma popisuje různé způsoby, kterými můžete auditovat koncový bod JEA.</span><span class="sxs-lookup"><span data-stu-id="cb427-107">This topic describes the various ways you can audit a JEA endpoint.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="cb427-108">Najít registrovaný JEA relací na počítači</span><span class="sxs-lookup"><span data-stu-id="cb427-108">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="cb427-109">Chcete-li zkontrolovat, které JEA relací jsou registrované na počítači, použijte [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) rutiny.</span><span class="sxs-lookup"><span data-stu-id="cb427-109">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

<span data-ttu-id="cb427-110">Efektivní práva pro koncový bod jsou uvedeny ve vlastnosti "Oprávnění".</span><span class="sxs-lookup"><span data-stu-id="cb427-110">The effective rights for the endpoint are listed in the "Permission" property.</span></span>
<span data-ttu-id="cb427-111">Tito uživatelé mají práva k připojení k JEA koncového bodu, ale které role (a při rozšíření příkazy) mají přístup je určen v poli "RoleDefinitions" [relace konfigurační soubor](session-configurations.md) která byla použita k registraci koncový bod.</span><span class="sxs-lookup"><span data-stu-id="cb427-111">These users have the right to connect to the JEA endpoint, but which roles (and, by extension, commands) they have access to is determined by the "RoleDefinitions" field in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span>

<span data-ttu-id="cb427-112">Mapování role na koncový bod registrovaný JEA můžete vyhodnotit rozšířením dat ve vlastnosti "RoleDefinitions".</span><span class="sxs-lookup"><span data-stu-id="cb427-112">You can evaluate the role mappings in a registered JEA endpoint by expanding the data in the "RoleDefinitions" property.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="cb427-113">Najít možnosti dostupné role na počítači</span><span class="sxs-lookup"><span data-stu-id="cb427-113">Find available role capabilities on the machine</span></span>

<span data-ttu-id="cb427-114">Soubory schopnosti role se použít pomocí JEA jen v případě, že jsou uložené ve složce "RoleCapabilities" uvnitř platný modul prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb427-114">Role capability files will only be used by JEA if they are stored in a "RoleCapabilities" folder inside a valid PowerShell module.</span></span>
<span data-ttu-id="cb427-115">Všechny role možnosti dostupné v počítači můžete najít tak, že seznamu dostupných modulů.</span><span class="sxs-lookup"><span data-stu-id="cb427-115">You can find all role capabilities available on a computer by searching the list of available modules.</span></span>

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
> <span data-ttu-id="cb427-116">Pořadí výsledky z tato funkce není nutně pořadí, ve kterém bude vybrána funkce role, pokud více možností role sdílejí stejný název.</span><span class="sxs-lookup"><span data-stu-id="cb427-116">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="cb427-117">Zaškrtněte políčko efektivní práva pro konkrétního uživatele</span><span class="sxs-lookup"><span data-stu-id="cb427-117">Check effective rights for a specific user</span></span>

<span data-ttu-id="cb427-118">Jakmile nastavíte koncový bod JEA, můžete zkontrolovat, které příkazy v relaci JEA jsou k dispozici pro konkrétního uživatele.</span><span class="sxs-lookup"><span data-stu-id="cb427-118">Once you have set up a JEA endpoint, you may want to check which commands are available to a specific user in a JEA session.</span></span>
<span data-ttu-id="cb427-119">Můžete použít [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) výčet všechny příkazy pro uživatele, pokud by byly spustit relaci JEA s jejich aktuální členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="cb427-119">You can use [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) to enumerate all of the commands applicable to a user if they were to start a JEA session with their current group memberships.</span></span>
<span data-ttu-id="cb427-120">Výstup `Get-PSSessionCapability` je shodná s zadaný uživatel, který spouští `Get-Command -CommandType All` v relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="cb427-120">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="cb427-121">Pokud vaši uživatelé nejsou členy skupin, které by jim udělit další práva JEA, tato rutina nemusí odrážet tato další oprávnění.</span><span class="sxs-lookup"><span data-stu-id="cb427-121">If your users are not permanent members of groups which would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span>
<span data-ttu-id="cb427-122">To je obvykle případ, kdy pomocí systémy správy privilegovaného přístupu za běhu, aby uživatelé mohli dočasně patří do skupiny zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="cb427-122">This is typically the case when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span>
<span data-ttu-id="cb427-123">Vždycky pečlivě vyhodnoťte mapování uživatelů k rolím a obsah každou roli, aby uživatelé jsou pouze získávají přístup k minimem příkazy potřebné pro svou práci úspěšně.</span><span class="sxs-lookup"><span data-stu-id="cb427-123">Always carefully evaluate the mapping of users to roles and the contents of each role to ensure users are only getting access to the least amount of commands needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="cb427-124">Protokoly událostí prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb427-124">PowerShell event logs</span></span>

<span data-ttu-id="cb427-125">Pokud jste povolili modulu nebo skriptu bloku protokolování v systému, bude možné najít události v protokolech událostí systému Windows pro každý příkaz, který uživatel spustil v jejich JEA relace.</span><span class="sxs-lookup"><span data-stu-id="cb427-125">If you enabled module and/or script block logging on the system, you will be able to find events in the Windows event logs for each command a user ran in their JEA sessions.</span></span>
<span data-ttu-id="cb427-126">Pokud chcete vyhledat tyto události, otevřete Prohlížeč událostí systému Windows, přejděte na **Microsoft-Windows-PowerShell/Operational** protokol událostí a podívejte se na události s ID události **4104**.</span><span class="sxs-lookup"><span data-stu-id="cb427-126">To find these events, open the Windows Event Viewer, navigate to the **Microsoft-Windows-PowerShell/Operational** event log, and look for events with event ID **4104**.</span></span>

<span data-ttu-id="cb427-127">Každá položka protokolu událostí bude obsahovat informace o relaci, ve kterém byl spuštěn příkaz.</span><span class="sxs-lookup"><span data-stu-id="cb427-127">Each event log entry will include information about the session in which the command was run.</span></span>
<span data-ttu-id="cb427-128">Pro relace JEA to zahrnuje důležité informace o **ConnectedUser**, což je skutečný uživatele, který vytvořil JEA relace, společně s **Spustit_jako_uživatel** který identifikuje účet JEA použitý k spustíte příkaz.</span><span class="sxs-lookup"><span data-stu-id="cb427-128">For JEA sessions, this includes important information about the **ConnectedUser**, which is the actual user who created the JEA session, as well as the **RunAsUser** which identifies the account JEA used to execute the command.</span></span>
<span data-ttu-id="cb427-129">Záznamy událostí aplikace se zobrazí změny podle Spustit_jako_uživatel, takže s přepisy nebo skriptování či modulu protokolování je zásadní moct trasování volání konkrétní příkaz zpět na uživatele.</span><span class="sxs-lookup"><span data-stu-id="cb427-129">Application event logs will show changes being made by the RunAsUser, so having transcripts or module/script logging enabled is crucial to be able to trace a specific command invocation back to a user.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="cb427-130">Záznamy událostí aplikace</span><span class="sxs-lookup"><span data-stu-id="cb427-130">Application event logs</span></span>

<span data-ttu-id="cb427-131">Při spuštění příkazu v relaci JEA, která interaguje s externí aplikace nebo služba, mohou tyto aplikace protokolování událostí do své vlastní protokoly událostí.</span><span class="sxs-lookup"><span data-stu-id="cb427-131">When you run a command in a JEA session that interacts with an external application or service, those applications may log events to their own event logs.</span></span>
<span data-ttu-id="cb427-132">Na rozdíl od protokoly prostředí PowerShell a přepisy jiným mechanismem protokolování nebude zachytávat připojených uživatelů JEA relace a bude místo toho pouze virtuální spustit jako účet uživatele nebo skupiny spravované služby.</span><span class="sxs-lookup"><span data-stu-id="cb427-132">Unlike PowerShell logs and transcripts, other logging mechanisms will not capture the connected user of the JEA session, and will instead only log the virtual run-as user or group managed service account.</span></span>
<span data-ttu-id="cb427-133">Aby bylo možné zjistit, kdo příkaz spustili, budete muset obrátit [relace přepis](#session-transcripts) nebo korelovat protokoly událostí prostředí PowerShell s a uživatel vidět v protokolu událostí aplikace.</span><span class="sxs-lookup"><span data-stu-id="cb427-133">In order to determine who ran the command, you will need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="cb427-134">WinRM protokolu rovněž umožňuje korelovat spustit jako uživatele v protokolu událostí aplikace s připojující se uživatel.</span><span class="sxs-lookup"><span data-stu-id="cb427-134">The WinRM log can also help you correlate run as users in an application event log with the connecting user.</span></span>
<span data-ttu-id="cb427-135">ID události **193** v **Operational vzdálené správy Microsoft-Windows-Windows** protokolování záznamů identifikátor zabezpečení (SID) a účet name pro připojování uživatele a spustit jako uživatele pokaždé, když JEA relace je vytvořena.</span><span class="sxs-lookup"><span data-stu-id="cb427-135">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user every time a JEA session is created.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="cb427-136">Přepisy relace</span><span class="sxs-lookup"><span data-stu-id="cb427-136">Session transcripts</span></span>

<span data-ttu-id="cb427-137">Pokud jste nakonfigurovali JEA k vytvoření přepis pro každou relaci uživatele, text kopii každého uživatele akce se uloží v zadané složce.</span><span class="sxs-lookup"><span data-stu-id="cb427-137">If you configured JEA to create a transcript for each user session, a text copy of every user's actions will be stored in the specified folder.</span></span>

<span data-ttu-id="cb427-138">Pokud chcete najít všechny adresáře přepis, spusťte následující příkaz v počítači jako správce konfigurace JEA:</span><span class="sxs-lookup"><span data-stu-id="cb427-138">To find all transcript directories, run the following command as an administrator on the computer configured with JEA:</span></span>

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="cb427-139">Každý přepis začíná informace o čas spuštění relace, které uživatel připojený k relaci a které identity JEA byl přiřazen k nim.</span><span class="sxs-lookup"><span data-stu-id="cb427-139">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="cb427-140">V těle zápis je do něj protokolují informace o každém příkazu uživatel vyvolat.</span><span class="sxs-lookup"><span data-stu-id="cb427-140">In the body of the transcript, information is logged about each command the user invoked.</span></span>
<span data-ttu-id="cb427-141">Přesná syntaxe příkazu, který spustil uživatele je k dispozici v relacích JEA z důvodu způsob, jakým jsou transformovány příkazy pro vzdálenou komunikaci prostředí PowerShell, ale stále můžete určit efektivní příkaz, který byl proveden.</span><span class="sxs-lookup"><span data-stu-id="cb427-141">The exact syntax of the command the user ran is unavailable in JEA sessions due to the way commands are transformed for PowerShell remoting, however you can still determine the effective command that was executed.</span></span>
<span data-ttu-id="cb427-142">Níže je fragment kódu příklad přepis od uživatele s `Get-Service Dns` v relaci JEA:</span><span class="sxs-lookup"><span data-stu-id="cb427-142">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="cb427-143">U každého příkazu, který uživatel spustí řádek "CommandInvocation" bude zapsán, popisující rutinu nebo funkce uživatel vyvolat.</span><span class="sxs-lookup"><span data-stu-id="cb427-143">For each command a user runs, a "CommandInvocation" line will be written, describing the cmdlet or function the user invoked.</span></span>
<span data-ttu-id="cb427-144">ParameterBindings podle jednotlivých CommandInvocation získat informace o jednotlivých parametr a hodnotu, která byla zadaná pomocí příkazu.</span><span class="sxs-lookup"><span data-stu-id="cb427-144">ParameterBindings follow each CommandInvocation to tell you about each parameter and value that was supplied with the command.</span></span>
<span data-ttu-id="cb427-145">V předchozím příkladu uvidíte, že parametr, který byl "Název" poskytnutá hodnota "Dns" pro rutinu "Get-Service".</span><span class="sxs-lookup"><span data-stu-id="cb427-145">In the above example, you can see that the parameter "Name" was supplied the value "Dns" for the "Get-Service" cmdlet.</span></span>

<span data-ttu-id="cb427-146">Výstup každé příkazu se také aktivuje CommandInvocation, obvykle odesílací výchozí.</span><span class="sxs-lookup"><span data-stu-id="cb427-146">The output of each command will also trigger a CommandInvocation, usually to Out-Default.</span></span> <span data-ttu-id="cb427-147">InputObject Out-Default je objekt prostředí PowerShell vrátí z příkazu.</span><span class="sxs-lookup"><span data-stu-id="cb427-147">The InputObject of Out-Default is the PowerShell object returned from the command.</span></span>
<span data-ttu-id="cb427-148">Podrobnosti tohoto objektu se tisknou pár řádků níže úzce mimicking, co by mohli vidět uživatele.</span><span class="sxs-lookup"><span data-stu-id="cb427-148">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="cb427-149">Viz taky</span><span class="sxs-lookup"><span data-stu-id="cb427-149">See also</span></span>

- [<span data-ttu-id="cb427-150">Akce auditování uživatele v relaci JEA</span><span class="sxs-lookup"><span data-stu-id="cb427-150">Audit user actions in a JEA session</span></span>](audit-and-report.md)
- [<span data-ttu-id="cb427-151">*Prostředí PowerShell ♥ týmem Blue* příspěvku na blogu na zabezpečení</span><span class="sxs-lookup"><span data-stu-id="cb427-151">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)


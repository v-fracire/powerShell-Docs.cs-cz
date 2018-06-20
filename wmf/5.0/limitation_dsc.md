---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 76aa4a372602d78e013b2138eb6409304a4dfb76
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190056"
---
# <a name="desired-state-configuration-dsc-known-issues-and-limitations"></a><span data-ttu-id="ea7f1-102">Konfigurace požadovaného stavu (DSC) – známé problémy a omezení</span><span class="sxs-lookup"><span data-stu-id="ea7f1-102">Desired State Configuration (DSC) Known Issues and Limitations</span></span>

<a name="breaking-change-certificates-used-to-encryptdecrypt-passwords-in-dsc-configurations-may-not-work-after-installing-wmf-50-rtm"></a><span data-ttu-id="ea7f1-103">Narušující změny: Certifikáty používané k šifrování a dešifrování hesla v konfiguracích DSC nemusí fungovat po instalaci WMF 5.0 RTM</span><span class="sxs-lookup"><span data-stu-id="ea7f1-103">Breaking Change: Certificates used to encrypt/decrypt passwords in DSC configurations may not work after installing WMF 5.0 RTM</span></span>
--------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="ea7f1-104">Ve verzích WMF 4.0 a WMF 5.0 Preview DSC nepovolí hesla v konfiguraci pro o délce maximálně 121 znaků.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-104">In WMF 4.0 and WMF 5.0 Preview releases, DSC would not allow passwords in the configuration to be of length more than 121 characters.</span></span> <span data-ttu-id="ea7f1-105">DSC byla vynucení použít krátký hesla i v případě, že byl potřeby náročná a silné heslo.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-105">DSC was forcing to use short passwords even if lengthy and strong password was desired.</span></span> <span data-ttu-id="ea7f1-106">Tato změna narušující umožňuje hesla, aby se o libovolné délce v konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-106">This breaking change allows passwords to be of arbitrary length in the DSC configuration.</span></span>

<span data-ttu-id="ea7f1-107">**Řešení:** znovu vytvořit certifikát s využití šifrování dat nebo šifrování klíče a použití klíče pro rozšířené šifrování dokumentů (1.3.6.1.4.1.311.80.1).</span><span class="sxs-lookup"><span data-stu-id="ea7f1-107">**Resolution:** Re-create the certificate with Data Encipherment or Key Encipherment Key usage, and Document Encryption Enhanced Key usage (1.3.6.1.4.1.311.80.1).</span></span> <span data-ttu-id="ea7f1-108">Článku na webu TechNet <https://technet.microsoft.com/library/dn807171.aspx> obsahuje další informace.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-108">Technet article <https://technet.microsoft.com/library/dn807171.aspx> has more information.</span></span>


<a name="dsc-cmdlets-may-fail-after-installing-wmf-50-rtm"></a><span data-ttu-id="ea7f1-109">Po instalaci WMF 5.0 RTM, může selhat rutiny DSC</span><span class="sxs-lookup"><span data-stu-id="ea7f1-109">DSC cmdlets may fail after installing WMF 5.0 RTM</span></span>
------------------------------------------------------------------------------------
<span data-ttu-id="ea7f1-110">Spuštění DscConfiguration a ostatní rutiny DSC může selhat po instalaci WMF 5.0 RTM, s následující chybou:</span><span class="sxs-lookup"><span data-stu-id="ea7f1-110">Start-DscConfiguration and other DSC cmdlets may fail after installing WMF 5.0 RTM with the following error:</span></span>
```powershell
    LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
    + CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 6
    + PSComputerName : localhost
```

<span data-ttu-id="ea7f1-111">**Řešení:** odstranit DSCEngineCache.mof spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):</span><span class="sxs-lookup"><span data-stu-id="ea7f1-111">**Resolution:** Delete DSCEngineCache.mof by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```


<a name="dsc-cmdlets-may-not-work-if-wmf-50-rtm-is-installed-on-top-of-wmf-50-production-preview"></a><span data-ttu-id="ea7f1-112">Rutiny DSC nemusí fungovat, pokud WMF 5.0 RTM již je nainstalován na WMF 5.0 produkční Preview</span><span class="sxs-lookup"><span data-stu-id="ea7f1-112">DSC cmdlets may not work if WMF 5.0 RTM is installed on top of WMF 5.0 Production Preview</span></span>
------------------------------------------------------
<span data-ttu-id="ea7f1-113">**Řešení:** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):</span><span class="sxs-lookup"><span data-stu-id="ea7f1-113">**Resolution:** Run the following command in an elevated PowerShell session (run as administrator):</span></span>
```powershell
    mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```


<a name="lcm-can-go-into-an-unstable-state-while-using-get-dscconfiguration-in-debugmode"></a><span data-ttu-id="ea7f1-114">LCM můžete přejít do nestabilním stavu, při použití Get-DscConfiguration v režim DebugMode</span><span class="sxs-lookup"><span data-stu-id="ea7f1-114">LCM can go into an unstable state while using Get-DscConfiguration in DebugMode</span></span>
-------------------------------------------------------------------------------

<span data-ttu-id="ea7f1-115">Pokud LCM v režim DebugMode, kombinace kláves CTRL + C zastavit zpracování Get-DscConfiguration může způsobit LCM přejdete do nestabilním stavu takové této většinu rutin DSC nefungují.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-115">If LCM is in DebugMode, pressing CTRL+C to stop the processing of Get-DscConfiguration can cause LCM to go into an unstable state such that majority of DSC cmdlets won’t work.</span></span>

<span data-ttu-id="ea7f1-116">**Řešení:** není při ladění rutiny Get-DscConfiguration stisknutím CTRL + C.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-116">**Resolution:** Don’t press CTRL+C while debugging Get-DscConfiguration cmdlet.</span></span>


<a name="stop-dscconfiguration-may-hang-in-debugmode"></a><span data-ttu-id="ea7f1-117">Stop-DscConfiguration může přestat reagovat v režim DebugMode</span><span class="sxs-lookup"><span data-stu-id="ea7f1-117">Stop-DscConfiguration may hang in DebugMode</span></span>
------------------------------------------------------------------------------------------------------------------------
<span data-ttu-id="ea7f1-118">Pokud LCM v režim DebugMode, zastavte DscConfiguration může přestat reagovat při pokusu o zastavení operace pomocí Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="ea7f1-118">If LCM is in DebugMode, Stop-DscConfiguration may hang while trying to stop an operation started by Get-DscConfiguration</span></span>

<span data-ttu-id="ea7f1-119">**Řešení:** ukončete ladění operaci Get-DscConfiguration spouštěné, jak je uvedeno v části "[prostředky DSC ladění](https://msdn.microsoft.com/powershell/dsc/debugresource)'.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-119">**Resolution:** Finish the debugging of the operation started by Get-DscConfiguration as outlined in section ‘[Debugging DSC resources](https://msdn.microsoft.com/powershell/dsc/debugresource)’.</span></span>


<a name="no-verbose-error-messages-are-shown-in-debugmode"></a><span data-ttu-id="ea7f1-120">Žádné podrobné chybové zprávy se zobrazují v režim DebugMode</span><span class="sxs-lookup"><span data-stu-id="ea7f1-120">No Verbose Error Messages are shown in DebugMode</span></span>
-----------------------------------------------------------------------------------
<span data-ttu-id="ea7f1-121">Pokud LCM v režim DebugMode, zobrazí se žádné podrobné chybové zprávy z prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-121">If LCM is in DebugMode, no verbose error messages are displayed from DSC Resources.</span></span>

<span data-ttu-id="ea7f1-122">**Řešení:** zakázat *režim DebugMode* zobrazíte podrobné zprávy z prostředku</span><span class="sxs-lookup"><span data-stu-id="ea7f1-122">**Resolution:** Disable *DebugMode* to see verbose messages from the resource</span></span>


<a name="invoke-dscresource-operations-cannot-be-retrieved-by-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="ea7f1-123">Vyvolání DscResource operace nelze načíst pomocí rutiny Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="ea7f1-123">Invoke-DscResource operations cannot be retrieved by Get-DscConfigurationStatus cmdlet</span></span>
--------------------------------------------------------------------------------------
<span data-ttu-id="ea7f1-124">Po pomocí rutiny Invoke-DscResource přímo volat metody jakémukoli prostředku, nemohou být načteni prostřednictvím Get-DscConfigurationStatus záznamy takové operaci později.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-124">After using Invoke-DscResource cmdlet to directly invoke any resource’s methods, the records of such operation cannot be retrieved through Get-DscConfigurationStatus at a later time.</span></span>

<span data-ttu-id="ea7f1-125">**Řešení:** None.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-125">**Resolution:** None.</span></span>


<a name="get-dscconfigurationstatus-returns-pull-cycle-operations-as-type-consistency"></a><span data-ttu-id="ea7f1-126">Operace Get-DscConfigurationStatus vrátí stažení cyklus jako typ *konzistence*</span><span class="sxs-lookup"><span data-stu-id="ea7f1-126">Get-DscConfigurationStatus returns pull cycle operations as type *Consistency*</span></span>
---------------------------------------------------------------------------------
<span data-ttu-id="ea7f1-127">Uzel je nastavena na režimu aktualizace vyžádání obsahu, pro každou vyžádanou operaci provést, rutina Get-DscConfigurationStatus sestavy typ operace jako *konzistence* místo *počáteční*</span><span class="sxs-lookup"><span data-stu-id="ea7f1-127">When a node is set to PULL refresh mode, for each pull operation performed, Get-DscConfigurationStatus cmdlet reports the operation type as *Consistency* instead of *Initial*</span></span>

<span data-ttu-id="ea7f1-128">**Řešení:** None.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-128">**Resolution:** None.</span></span>

<a name="invoke-dscresource-cmdlet-does-not-return-message-in-the-order-they-were-produced"></a><span data-ttu-id="ea7f1-129">Rutina Invoke-DscResource nevrací zprávy v pořadí, ve kterém jejich výroby</span><span class="sxs-lookup"><span data-stu-id="ea7f1-129">Invoke-DscResource cmdlet does not return message in the order they were produced</span></span>
---------------------------------------------------------------------------------
<span data-ttu-id="ea7f1-130">Rutina Invoke-DscResource nevrací podrobné nastavení, upozornění, a chybové zprávy v pořadí, ve kterém byly vytvořeny LCM nebo prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-130">The Invoke-DscResource cmdlet does not return verbose, warning, and error messages in the order they were produced by LCM or the DSC resource.</span></span>

<span data-ttu-id="ea7f1-131">**Řešení:** None.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-131">**Resolution:** None.</span></span>


<a name="dsc-resources-cannot-be-debugged-easily-when-used-with-invoke-dscresource"></a><span data-ttu-id="ea7f1-132">Prostředky DSC nelze snadno ladit, pokud se používá s Invoke-DscResource</span><span class="sxs-lookup"><span data-stu-id="ea7f1-132">DSC Resources cannot be debugged easily when used with Invoke-DscResource</span></span>
-----------------------------------------------------------------------
<span data-ttu-id="ea7f1-133">Pokud LCM běží v režimu ladění (najdete v části [prostředky DSC ladění](https://msdn.microsoft.com/powershell/dsc/debugresource) podrobnosti), rutiny Invoke-DscResource neposkytuje informace o prostředí runspace pro připojení k pro ladění.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-133">When LCM is running in debug mode (see [Debugging DSC resources](https://msdn.microsoft.com/powershell/dsc/debugresource) for more details), Invoke-DscResource cmdlet does not give information about runspace to connect to for debugging.</span></span>
<span data-ttu-id="ea7f1-134">**Řešení:** vyhledat a připojit k pomocí rutin prostředí runspace **Get-PSHostProcessInfo**, **Enter PSHostProcess** , **Get-prostředí Runspace** a **Ladění Runspace** k ladění prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-134">**Resolution:** Discover and attach to the runspace using cmdlets **Get-PSHostProcessInfo**, **Enter-PSHostProcess** , **Get-Runspace** and **Debug-Runspace** to debug the DSC resource.</span></span>

```powershell
# Find all the processes hosting PowerShell
Get-PSHostProcessInfo

ProcessName ProcessId AppDomainName
----------- --------- -------------
powershell 3932 DefaultAppDomain
powershell_ise 2304 DefaultAppDomain
WmiPrvSE 3396 DscPsPluginWkr_AppDomain

# Enter the process that is hosting DSC engine (WMI process with DscPsPluginWkr_Appdomain)
Enter-PSHostProcess -Id 3396 -AppDomainName DscPsPluginWkr_AppDomain

# Find all the available rusnspaces in that process
Get-Runspace

Id Name ComputerName Type State Availability
-- ---- ------------ ---- ----- ------------
2 Runspace2 localhost Local Opened InBreakpoint
5 RemoteHost localhost Local Opened Busy

# Debug the runspace that is in **InBreakpoint** availability state
Debug-Runspace -Id 2
```


<a name="various-partial-configuration-documents-for-same-node-cannot-have-identical-resource-names"></a><span data-ttu-id="ea7f1-135">Různé dokumentů částečné konfigurace pro stejný uzel nemůže mít názvy identické prostředků</span><span class="sxs-lookup"><span data-stu-id="ea7f1-135">Various Partial Configuration documents for same node cannot have identical resource names</span></span>
------------------------------------------------------------------------------------------

<span data-ttu-id="ea7f1-136">Pro několik částečné konfigurace, které jsou nasazeny do jednoho uzlu spusťte identické názvy prostředků příčina chyby čas.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-136">For several partial configurations that are deployed onto a single node, identical names of resources cause run time error.</span></span>

<span data-ttu-id="ea7f1-137">**Řešení:** v různých konfigurací. částečné používat jiné názvy pro i stejné prostředky.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-137">**Resolution:** Use different names for even same resources in different partial configurations.</span></span>


<a name="start-dscconfiguration-useexisting-does-not-work-with--credential"></a><span data-ttu-id="ea7f1-138">Spuštění DscConfiguration – UseExisting nefunguje s - přihlašovacích údajů</span><span class="sxs-lookup"><span data-stu-id="ea7f1-138">Start-DscConfiguration –UseExisting does not work with -Credential</span></span>
------------------------------------------------------------------

<span data-ttu-id="ea7f1-139">Při použití s parametrem – UseExisting Start-DscConfiguration – přihlašovací údaje parametr je ignorován.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-139">When using Start-DscConfiguration with –UseExisting parameter, the –Credential parameter is ignored.</span></span> <span data-ttu-id="ea7f1-140">DSC používá výchozí identitu procesu pokračovat operaci.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-140">DSC uses default process identity to proceed the operation.</span></span> <span data-ttu-id="ea7f1-141">To způsobí, že chyby pokračovat na vzdáleném uzlu se potřeby různých přihlašovacích údajů.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-141">This causes error when a different credential is needed to proceed on remote node.</span></span>

<span data-ttu-id="ea7f1-142">**Řešení:** použití CIM relace pro vzdálené operace DSC:</span><span class="sxs-lookup"><span data-stu-id="ea7f1-142">**Resolution:** Use CIM session for remote DSC operations:</span></span>
```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```


<a name="ipv6-addresses-as-node-names-in-dsc-configurations"></a><span data-ttu-id="ea7f1-143">Adresy IPv6 jako názvy uzlů v konfiguracích DSC</span><span class="sxs-lookup"><span data-stu-id="ea7f1-143">IPv6 Addresses as Node Names in DSC configurations</span></span>
--------------------------------------------------
<span data-ttu-id="ea7f1-144">Adresy IPv6 jako názvy ve skriptech konfigurace DSC nejsou v této verzi podporovány.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-144">IPv6 addresses as node names in DSC configuration scripts are not supported in this release.</span></span>

<span data-ttu-id="ea7f1-145">**Řešení:** None.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-145">**Resolution:** None.</span></span>


<a name="debugging-of-class-based-dsc-resources"></a><span data-ttu-id="ea7f1-146">Ladění prostředky založené na třídě DSC</span><span class="sxs-lookup"><span data-stu-id="ea7f1-146">Debugging of Class-Based DSC Resources</span></span>
--------------------------------------
<span data-ttu-id="ea7f1-147">V této verzi nepodporuje ladění založené na třídě prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-147">Debugging of class-based DSC Resources is not supported in this release.</span></span>

<span data-ttu-id="ea7f1-148">**Řešení:** None.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-148">**Resolution:** None.</span></span>


<a name="variables--functions-defined-in-script-scope-in-dsc-class-based-resource-are-not-preserved-across-multiple-calls-to-a-dsc-resource"></a><span data-ttu-id="ea7f1-149">Proměnné & funkcí definovaných v oboru $script v prostředek DSC založené na třídě nejsou zachována napříč více volání prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="ea7f1-149">Variables & Functions defined in $script scope in DSC Class-Based Resource are not preserved across multiple calls to a DSC Resource</span></span>
-------------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="ea7f1-150">Více po sobě jdoucí volání počáteční DSCConfiguration se nezdaří, pokud je konfigurace pomocí jakékoli založené na třídě prostředku, který má proměnné nebo funkce, které jsou definované v oboru $script.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-150">Multiple consecutive calls to Start-DSCConfiguration will fail if configuration is using any class-based resource which has variables or functions defined in $script scope.</span></span>

<span data-ttu-id="ea7f1-151">**Řešení:** definovat všechny proměnné a funkce v vlastní třídy prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-151">**Resolution:** Define all variables and functions in DSC Resource class itself.</span></span> <span data-ttu-id="ea7f1-152">No $script obor proměnné nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-152">No $script scope variables/functions.</span></span>


<a name="dsc-resource-debugging-when-a-resource-is-using-psdscrunascredential"></a><span data-ttu-id="ea7f1-153">Když prostředek používá PSDscRunAsCredential ladění prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="ea7f1-153">DSC Resource Debugging when a resource is using PSDscRunAsCredential</span></span>
----------------------------------------------------------------------
<span data-ttu-id="ea7f1-154">Ladění prostředků DSC, když používá prostředku *PSDscRunAsCredential* vlastnosti v konfiguraci není suported v této verzi.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-154">DSC Resource debugging when a resource is using the *PSDscRunAsCredential* property in the configuration is not suported in this release.</span></span>

<span data-ttu-id="ea7f1-155">**Řešení:** None.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-155">**Resolution:** None.</span></span>


<a name="psdscrunascredential-is-not-supported-for-dsc-composite-resources"></a><span data-ttu-id="ea7f1-156">PsDscRunAsCredential není podporována pro složené prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="ea7f1-156">PsDscRunAsCredential is not supported for DSC Composite Resources</span></span>
----------------------------------------------------------------

<span data-ttu-id="ea7f1-157">**Řešení:** vlastnost použití pověření, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-157">**Resolution:** Use Credential property if available.</span></span> <span data-ttu-id="ea7f1-158">Příklad ServiceSet a WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="ea7f1-158">Example ServiceSet and WindowsFeatureSet</span></span>


<a name="get-dscresource--syntax-does-not-reflect-psdscrunascredential-correctly"></a><span data-ttu-id="ea7f1-159">*Get-DscResource-syntaxe* nezohledňuje PsDscRunAsCredential správně</span><span class="sxs-lookup"><span data-stu-id="ea7f1-159">*Get-DscResource -Syntax* does not reflect PsDscRunAsCredential correctly</span></span>
-------------------------------------------------------------------------
<span data-ttu-id="ea7f1-160">Get-DscResource-syntaxe nezohledňuje PsDscRunAsCredential správně při prostředků označí je jako povinné nebo ji nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-160">Get-DscResource -Syntax does not reflect PsDscRunAsCredential correctly when resource marks it as mandatory or does not support it.</span></span>

<span data-ttu-id="ea7f1-161">**Řešení:** None.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-161">**Resolution:** None.</span></span> <span data-ttu-id="ea7f1-162">Ale vytváření konfigurace (ISE) v odráží správných metadat o PsDscRunAsCredential vlastnosti při použití technologie IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-162">However, authoring configuration in ISE reflects correct metadata about PsDscRunAsCredential property when using IntelliSense.</span></span>


<a name="windowsoptionalfeature-is-not-available-in-windows-7"></a><span data-ttu-id="ea7f1-163">WindowsOptionalFeature není k dispozici v systému Windows 7</span><span class="sxs-lookup"><span data-stu-id="ea7f1-163">WindowsOptionalFeature is not available in Windows 7</span></span>
-----------------------------------------------------

<span data-ttu-id="ea7f1-164">Prostředek WindowsOptionalFeature DSC není k dispozici v systému Windows 7.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-164">The WindowsOptionalFeature DSC resource is not available in Windows 7.</span></span> <span data-ttu-id="ea7f1-165">Tento prostředek vyžaduje modulu DISM a rutin DISM, které jsou k dispozici od verze Windows 8 a novější verze operačního systému Windows.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-165">This resource requires the DISM module, and DISM cmdlets that are available starting in Windows 8 and newer releases of the Windows operating system.</span></span>

<a name="for-class-based-dsc-resources-import-dscresource--moduleversion-may-not-work-as-expected"></a><span data-ttu-id="ea7f1-166">Pro prostředky založené na třídě DSC Import DscResource - ModuleVersion nemusí fungovat podle očekávání</span><span class="sxs-lookup"><span data-stu-id="ea7f1-166">For Class-based DSC resources, Import-DscResource -ModuleVersion may not work as expected</span></span>
------------------------------------------------------------------------------------------
<span data-ttu-id="ea7f1-167">Pokud je uzel kompilace více verze založené na třídě DSC prostředků modulu, `Import-DscResource -ModuleVersion` vyberte není zadaná verze a výsledků v následujících došlo k chybě kompilace.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-167">If the compilation node has multiple version of a class-based DSC resource module, `Import-DscResource -ModuleVersion` does not pick the specified version and results in following compilation error.</span></span>

```
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s): "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

<span data-ttu-id="ea7f1-168">**Řešení:** importovat požadovaná verze definováním *ModuleSpecification* do objektu `-ModuleName` s `RequiredVersion` klíč zadaný následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="ea7f1-168">**Resolution:** Import the required version by defining the *ModuleSpecification* object to the `-ModuleName` with `RequiredVersion` key specified as follows:</span></span>
``` PowerShell
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}
```

<a name="some-dsc-resources-like-registry-resource-may-start-to-take-a-long-time-to-process-the-request"></a><span data-ttu-id="ea7f1-169">Některé prostředky DSC jako registru prostředku může začít trvat dlouhou dobu zpracování žádosti.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-169">Some DSC resources like registry resource may start to take a long time to process the request.</span></span>
--------------------------------------------------------------------------------------------------------------------------------

<span data-ttu-id="ea7f1-170">**Resolution1:** vytvoření plánu úlohy, která pravidelně vyčistí následující složku.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-170">**Resolution1:** Create a schedule task that cleans up the following folder periodically.</span></span>
``` PowerShell
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis
```

<span data-ttu-id="ea7f1-171">**Resolution2:** změnit konfiguraci DSC vyčistěte *CommandAnalysis* složky na konci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="ea7f1-171">**Resolution2:** Change the DSC configuration to clean up the *CommandAnalysis* folder at the end of the configuration.</span></span>
``` PowerShell
Configuration $configName
{

   # User Data
    Registry SetRegisteredOwner
    {
        Ensure = 'Present'
        Force = $True
        Key = $Node.RegisteredKey
        ValueName = $Node.RegisteredOwnerValue
        ValueType = 'String'
        ValueData = $Node.RegisteredOwnerData
    }
    #
    # Script to delete the config
    #
    script DeleteCommandAnalysisCache
    {
        DependsOn="[Registry]SetRegisteredOwner"
        getscript="@{}"
        testscript = 'Remove-Item -Path $env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis -Force -Recurse -ErrorAction SilentlyContinue -ErrorVariable ev | out-null;$true'
        setscript = '$true'
    }
}
```

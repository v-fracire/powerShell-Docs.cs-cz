---
ms.date: 08/14/2018
keywords: rutiny prostředí PowerShell
title: Spuštění vzdálených příkazů
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 2001b5509acde6ec4259bb1442944958a67aa66f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404057"
---
# <a name="running-remote-commands"></a><span data-ttu-id="17928-103">Spuštění vzdálených příkazů</span><span class="sxs-lookup"><span data-stu-id="17928-103">Running Remote Commands</span></span>

<span data-ttu-id="17928-104">Příkazy můžete spustit na jednom nebo stovky počítačů pomocí jediného příkazu prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17928-104">You can run commands on one or hundreds of computers with a single PowerShell command.</span></span> <span data-ttu-id="17928-105">Prostředí Windows PowerShell podporuje vzdálený přístup pomocí různých technologií, včetně služby WMI, RPC a WS-Management.</span><span class="sxs-lookup"><span data-stu-id="17928-105">Windows PowerShell supports remote computing by using various technologies, including WMI, RPC, and WS-Management.</span></span>

<span data-ttu-id="17928-106">PowerShell Core podporuje rozhraní WMI, WS-Management a vzdálenou komunikaci SSH.</span><span class="sxs-lookup"><span data-stu-id="17928-106">PowerShell Core supports WMI, WS-Management, and SSH remoting.</span></span> <span data-ttu-id="17928-107">RPC se už nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="17928-107">RPC is no longer supported.</span></span>

<span data-ttu-id="17928-108">Další informace o vzdálené komunikace v prostředí PowerShell Core najdete v následujících článcích:</span><span class="sxs-lookup"><span data-stu-id="17928-108">For more information about remoting in PowerShell Core, see the following articles:</span></span>

- <span data-ttu-id="17928-109">[SSH vzdálené komunikace v Powershellu Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="17928-109">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="17928-110">[Vzdálená komunikace WSMan v Powershellu Core][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="17928-110">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="windows-powershell-remoting-without-configuration"></a><span data-ttu-id="17928-111">Vzdálená komunikace Windows Powershellu bez konfigurace</span><span class="sxs-lookup"><span data-stu-id="17928-111">Windows PowerShell Remoting Without Configuration</span></span>

<span data-ttu-id="17928-112">Mnoho rutin prostředí Windows PowerShell mají parametr ComputerName, který vám umožní shromažďovat data a nastavení na jeden nebo více vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="17928-112">Many Windows PowerShell cmdlets have the ComputerName parameter that enables you to collect data and change settings on one or more remote computers.</span></span> <span data-ttu-id="17928-113">Tyto rutiny použít různé komunikační protokoly a fungovat ve všech operačních systémech Windows bez žádnou zvláštní konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="17928-113">These cmdlets use varying communication protocols and work on all Windows operating systems without any special configuration.</span></span>

<span data-ttu-id="17928-114">Tyto rutiny zahrnují:</span><span class="sxs-lookup"><span data-stu-id="17928-114">These cmdlets include:</span></span>

- [<span data-ttu-id="17928-115">Restart-Computer</span><span class="sxs-lookup"><span data-stu-id="17928-115">Restart-Computer</span></span>](/powershell/module/microsoft.powershell.management/restart-computer)
- [<span data-ttu-id="17928-116">Test připojení</span><span class="sxs-lookup"><span data-stu-id="17928-116">Test-Connection</span></span>](/powershell/module/microsoft.powershell.management/test-connection)
- [<span data-ttu-id="17928-117">Clear-EventLog</span><span class="sxs-lookup"><span data-stu-id="17928-117">Clear-EventLog</span></span>](/powershell/module/microsoft.powershell.management/clear-eventlog)
- [<span data-ttu-id="17928-118">Get-EventLog</span><span class="sxs-lookup"><span data-stu-id="17928-118">Get-EventLog</span></span>](/powershell/module/microsoft.powershell.management/get-eventlog)
- [<span data-ttu-id="17928-119">Get-HotFix</span><span class="sxs-lookup"><span data-stu-id="17928-119">Get-HotFix</span></span>](/powershell/module/microsoft.powershell.management/get-hotfix)
- [<span data-ttu-id="17928-120">Get-Process</span><span class="sxs-lookup"><span data-stu-id="17928-120">Get-Process</span></span>](/powershell/module/microsoft.powershell.management/get-process)
- [<span data-ttu-id="17928-121">Get-Service</span><span class="sxs-lookup"><span data-stu-id="17928-121">Get-Service</span></span>](/powershell/module/microsoft.powershell.management/get-service)
- [<span data-ttu-id="17928-122">Nastavení služby</span><span class="sxs-lookup"><span data-stu-id="17928-122">Set-Service</span></span>](/powershell/module/microsoft.powershell.management/set-service)
- [<span data-ttu-id="17928-123">Get-WinEvent</span><span class="sxs-lookup"><span data-stu-id="17928-123">Get-WinEvent</span></span>](/powershell/module/microsoft.powershell.diagnostics/get-winevent)
- [<span data-ttu-id="17928-124">Get-WmiObject</span><span class="sxs-lookup"><span data-stu-id="17928-124">Get-WmiObject</span></span>](/powershell/module/microsoft.powershell.management/get-wmiobject)

<span data-ttu-id="17928-125">Rutiny, které podporují vzdálené komunikace bez speciální konfigurace obvykle mít parametr ComputerName a nemáte parametr relace.</span><span class="sxs-lookup"><span data-stu-id="17928-125">Typically, cmdlets that support remoting without special configuration have the ComputerName parameter and don't have the Session parameter.</span></span> <span data-ttu-id="17928-126">Chcete-li tyto rutiny najdete v relaci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="17928-126">To find these cmdlets in your session, type:</span></span>

```powershell
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a><span data-ttu-id="17928-127">Vzdálená komunikace Windows Powershellu</span><span class="sxs-lookup"><span data-stu-id="17928-127">Windows PowerShell Remoting</span></span>

<span data-ttu-id="17928-128">Pomocí protokolu WS-Management, umožňuje vzdálenou komunikaci Windows Powershellu můžete spouštět jakékoli příkazy prostředí Windows PowerShell na jeden nebo více vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="17928-128">Using the WS-Management protocol, Windows PowerShell remoting lets you run any Windows PowerShell command on one or more remote computers.</span></span> <span data-ttu-id="17928-129">Můžete navázat trvalé připojení, spouštění interaktivních relací a spouštět skripty na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="17928-129">You can establish persistent connections, start interactive sessions, and run scripts on remote computers.</span></span>

<span data-ttu-id="17928-130">Pokud chcete použít vzdálenou komunikaci prostředí Windows PowerShell, musí být vzdálený počítač nakonfigurovaný pro vzdálenou správu.</span><span class="sxs-lookup"><span data-stu-id="17928-130">To use Windows PowerShell remoting, the remote computer must be configured for remote management.</span></span>
<span data-ttu-id="17928-131">Další informace, včetně pokynů, najdete v části [vzdálené požadavky](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).</span><span class="sxs-lookup"><span data-stu-id="17928-131">For more information, including instructions, see [About Remote Requirements](/powershell/module/microsoft.powershell.core/about/about_remote_requirements).</span></span>

<span data-ttu-id="17928-132">Po nakonfigurování vzdálenou komunikaci prostředí Windows PowerShell, jsou k dispozici, mnoho strategií vzdálené komunikace.</span><span class="sxs-lookup"><span data-stu-id="17928-132">Once you have configured Windows PowerShell remoting, many remoting strategies are available to you.</span></span>
<span data-ttu-id="17928-133">Tento článek uvádí jenom některé z nich.</span><span class="sxs-lookup"><span data-stu-id="17928-133">This article lists just a few of them.</span></span> <span data-ttu-id="17928-134">Další informace najdete v tématu [o vzdálené](/powershell/module/microsoft.powershell.core/about/about_remote).</span><span class="sxs-lookup"><span data-stu-id="17928-134">For more information, see [About Remote](/powershell/module/microsoft.powershell.core/about/about_remote).</span></span>

### <a name="start-an-interactive-session"></a><span data-ttu-id="17928-135">Spuštění interaktivní relace</span><span class="sxs-lookup"><span data-stu-id="17928-135">Start an Interactive Session</span></span>

<span data-ttu-id="17928-136">Chcete-li spustit interaktivní relaci s jeden vzdálený počítač, použijte [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17928-136">To start an interactive session with a single remote computer, use the [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) cmdlet.</span></span>
<span data-ttu-id="17928-137">Například spuštění interaktivní relace Server01 na vzdáleném počítači, zadejte:</span><span class="sxs-lookup"><span data-stu-id="17928-137">For example, to start an interactive session with the Server01 remote computer, type:</span></span>

```powershell
Enter-PSSession Server01
```

<span data-ttu-id="17928-138">Příkazový řádek se změny zobrazily název vzdáleného počítače.</span><span class="sxs-lookup"><span data-stu-id="17928-138">The command prompt changes to display the name of the remote computer.</span></span> <span data-ttu-id="17928-139">Všechny příkazy, které zadáte v příkazovém řádku spustit na vzdáleném počítači a výsledky se zobrazí v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="17928-139">Any commands that you type at the prompt run on the remote computer and the results are displayed on the local computer.</span></span>

<span data-ttu-id="17928-140">Pokud chcete ukončit interaktivní relace, zadejte:</span><span class="sxs-lookup"><span data-stu-id="17928-140">To end the interactive session, type:</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="17928-141">Další informace o rutinách Enter-PSSession a ukončení relace PSSession najdete v článku:</span><span class="sxs-lookup"><span data-stu-id="17928-141">For more information about the Enter-PSSession and Exit-PSSession cmdlets, see:</span></span>

- [<span data-ttu-id="17928-142">Enter-PSSession</span><span class="sxs-lookup"><span data-stu-id="17928-142">Enter-PSSession</span></span>](/powershell/module/microsoft.powershell.core/enter-pssession)
- [<span data-ttu-id="17928-143">Ukončení relace PSSession</span><span class="sxs-lookup"><span data-stu-id="17928-143">Exit-PSSession</span></span>](/powershell/module/microsoft.powershell.core/exit-pssession)

### <a name="run-a-remote-command"></a><span data-ttu-id="17928-144">Spustit vzdálený příkaz</span><span class="sxs-lookup"><span data-stu-id="17928-144">Run a Remote Command</span></span>

<span data-ttu-id="17928-145">Chcete-li spustit příkaz na jeden nebo více počítačů, použijte [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17928-145">To run a command on one or more computers, use the [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) cmdlet.</span></span> <span data-ttu-id="17928-146">Chcete-li například spustit [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) v Server01 a Server02 vzdálenými počítači, zadejte příkaz:</span><span class="sxs-lookup"><span data-stu-id="17928-146">For example, to run a [Get-UICulture](/powershell/module/microsoft.powershell.utility/get-uiculture) command on the Server01 and Server02 remote computers, type:</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

<span data-ttu-id="17928-147">Výstup se vrací do vašeho počítače.</span><span class="sxs-lookup"><span data-stu-id="17928-147">The output is returned to your computer.</span></span>

```output
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```

### <a name="run-a-script"></a><span data-ttu-id="17928-148">Spuštění skriptu</span><span class="sxs-lookup"><span data-stu-id="17928-148">Run a Script</span></span>

<span data-ttu-id="17928-149">Pro spuštění skriptu na jeden nebo více vzdálených počítačích, použít parametr FilePath `Invoke-Command` rutiny.</span><span class="sxs-lookup"><span data-stu-id="17928-149">To run a script on one or many remote computers, use the FilePath parameter of the `Invoke-Command` cmdlet.</span></span> <span data-ttu-id="17928-150">Skript musí být přístupné pro místního počítače.</span><span class="sxs-lookup"><span data-stu-id="17928-150">The script must be on or accessible to your local computer.</span></span> <span data-ttu-id="17928-151">Výsledky jsou vráceny do místního počítače.</span><span class="sxs-lookup"><span data-stu-id="17928-151">The results are returned to your local computer.</span></span>

<span data-ttu-id="17928-152">Například následující příkaz spustí skript DiskCollect.ps1 na vzdálených počítačích, Server01 a Server02.</span><span class="sxs-lookup"><span data-stu-id="17928-152">For example, the following command runs the DiskCollect.ps1 script on the remote computers, Server01 and Server02.</span></span>

```powershell
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

### <a name="establish-a-persistent-connection"></a><span data-ttu-id="17928-153">Navázat trvalé připojení</span><span class="sxs-lookup"><span data-stu-id="17928-153">Establish a Persistent Connection</span></span>

<span data-ttu-id="17928-154">Použití `New-PSSession` rutina pro vytvoření trvalého relace na vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="17928-154">Use the `New-PSSession` cmdlet to create a persistent session on a remote computer.</span></span> <span data-ttu-id="17928-155">Následující příklad vytvoří na Server01 a Server02 vzdálené relace.</span><span class="sxs-lookup"><span data-stu-id="17928-155">The following example creates remote sessions on Server01 and Server02.</span></span> <span data-ttu-id="17928-156">Objekty relace jsou uloženy v `$s` proměnné.</span><span class="sxs-lookup"><span data-stu-id="17928-156">The session objects are stored in the `$s` variable.</span></span>

```powershell
$s = New-PSSession -ComputerName Server01, Server02
```

<span data-ttu-id="17928-157">Teď, když jsou vytvořeny na relace, můžete spouštět jakékoli příkazy v nich.</span><span class="sxs-lookup"><span data-stu-id="17928-157">Now that the sessions are established, you can run any command in them.</span></span> <span data-ttu-id="17928-158">A protože relací jsou trvalé, můžete shromažďovat data z jednoho příkazu a použít v jiné příkazu.</span><span class="sxs-lookup"><span data-stu-id="17928-158">And because the sessions are persistent, you can collect data from one command and use it in another command.</span></span>

<span data-ttu-id="17928-159">Například následující příkaz spustí příkaz Get-HotFix v relacích $s proměnné a uloží výsledky do $h proměnné.</span><span class="sxs-lookup"><span data-stu-id="17928-159">For example, the following command runs a Get-HotFix command in the sessions in the $s variable and it saves the results in the $h variable.</span></span> <span data-ttu-id="17928-160">$H proměnná je vytvořená ve všech relacích v $s, ale neexistuje v místní relaci.</span><span class="sxs-lookup"><span data-stu-id="17928-160">The $h variable is created in each of the sessions in $s, but it doesn't exist in the local session.</span></span>

```powershell
Invoke-Command -Session $s {$h = Get-HotFix}
```

<span data-ttu-id="17928-161">Teď můžete použít data v `$h` proměnné s jinými příkazy ve stejné relaci.</span><span class="sxs-lookup"><span data-stu-id="17928-161">Now you can use the data in the `$h` variable with other commands in the same session.</span></span> <span data-ttu-id="17928-162">Výsledky se zobrazí v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="17928-162">The results are displayed on the local computer.</span></span> <span data-ttu-id="17928-163">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17928-163">For example:</span></span>

```powershell
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a><span data-ttu-id="17928-164">Pokročilé vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="17928-164">Advanced Remoting</span></span>

<span data-ttu-id="17928-165">Vzdálená správa prostředí Windows PowerShell začíná právě tady.</span><span class="sxs-lookup"><span data-stu-id="17928-165">Windows PowerShell remote management just begins here.</span></span> <span data-ttu-id="17928-166">Pomocí rutiny nainstalované pomocí prostředí Windows PowerShell můžete vytvořit a nakonfigurovat vzdálené relace z konců místních a vzdálených vytvářet přizpůsobené a s omezeným přístupem relace, umožňuje uživatelům importovat příkazy ze vzdálené relace, které skutečně běží. implicitně na vzdálenou relaci, nakonfigurujte zabezpečení vzdálené relace a spoustu dalších věcí.</span><span class="sxs-lookup"><span data-stu-id="17928-166">By using the cmdlets installed with Windows PowerShell, you can establish and configure remote sessions both from the local and remote ends, create customized and restricted sessions, allow users to import commands from a remote session that actually run implicitly on the remote session, configure the security of a remote session, and much more.</span></span>

<span data-ttu-id="17928-167">Prostředí Windows PowerShell obsahuje poskytovatele služby WSMan.</span><span class="sxs-lookup"><span data-stu-id="17928-167">Windows PowerShell includes a WSMan provider.</span></span> <span data-ttu-id="17928-168">Vytvoří poskytovatele `WSMAN:` jednotky, ve kterém můžete procházet hierarchii konfigurovat nastavení pro místní i vzdálené počítače.</span><span class="sxs-lookup"><span data-stu-id="17928-168">The provider creates a `WSMAN:` drive that lets you navigate through a hierarchy of configuration settings on the local computer and remote computers.</span></span>

<span data-ttu-id="17928-169">Další informace o poskytovateli WSMan najdete v tématu [WSMan poskytovatele](https://technet.microsoft.com/library/dd819476.aspx) a [o WS-Management – rutiny](/powershell/module/microsoft.powershell.core/about/about_ws-management_cmdlets), nebo v konzole Windows Powershellu zadejte `Get-Help wsman`.</span><span class="sxs-lookup"><span data-stu-id="17928-169">For more information about the WSMan provider, see [WSMan Provider](https://technet.microsoft.com/library/dd819476.aspx) and [About WS-Management Cmdlets](/powershell/module/microsoft.powershell.core/about/about_ws-management_cmdlets), or in the Windows PowerShell console, type `Get-Help wsman`.</span></span>

<span data-ttu-id="17928-170">Další informace viz:</span><span class="sxs-lookup"><span data-stu-id="17928-170">For more information, see:</span></span>

- [<span data-ttu-id="17928-171">Informace o vzdálené – nejčastější dotazy</span><span class="sxs-lookup"><span data-stu-id="17928-171">About Remote FAQ</span></span>](https://technet.microsoft.com/library/dd315359.aspx)
- [<span data-ttu-id="17928-172">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="17928-172">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="17928-173">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="17928-173">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)

<span data-ttu-id="17928-174">Vzdálená komunikace vyřešení problémů, najdete v části [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).</span><span class="sxs-lookup"><span data-stu-id="17928-174">For help with remoting errors, see [about_Remote_Troubleshooting](https://technet.microsoft.com/library/dd347642.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="17928-175">Viz také</span><span class="sxs-lookup"><span data-stu-id="17928-175">See Also</span></span>

- [<span data-ttu-id="17928-176">about_Remote</span><span class="sxs-lookup"><span data-stu-id="17928-176">about_Remote</span></span>](https://technet.microsoft.com/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [<span data-ttu-id="17928-177">about_Remote_FAQ</span><span class="sxs-lookup"><span data-stu-id="17928-177">about_Remote_FAQ</span></span>](https://technet.microsoft.com/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [<span data-ttu-id="17928-178">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="17928-178">about_Remote_Requirements</span></span>](https://technet.microsoft.com/library/da213949-134c-4741-b307-81f4492ba1bd)
- [<span data-ttu-id="17928-179">about_Remote_Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="17928-179">about_Remote_Troubleshooting</span></span>](https://technet.microsoft.com/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [<span data-ttu-id="17928-180">about_PSSessions</span><span class="sxs-lookup"><span data-stu-id="17928-180">about_PSSessions</span></span>](https://technet.microsoft.com/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [<span data-ttu-id="17928-181">about_WS-Management_Cmdlets</span><span class="sxs-lookup"><span data-stu-id="17928-181">about_WS-Management_Cmdlets</span></span>](https://technet.microsoft.com/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [<span data-ttu-id="17928-182">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="17928-182">Invoke-Command</span></span>](/powershell/module/microsoft.powershell.core/invoke-command)
- [<span data-ttu-id="17928-183">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="17928-183">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)
- [<span data-ttu-id="17928-184">Nová relace PSSession</span><span class="sxs-lookup"><span data-stu-id="17928-184">New-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821498)
- [<span data-ttu-id="17928-185">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="17928-185">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="17928-186">Poskytovatel služby WSMan</span><span class="sxs-lookup"><span data-stu-id="17928-186">WSMan Provider</span></span>](https://technet.microsoft.com/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

[wsman-remoting]: WSMan-Remoting-in-PowerShell-Core.md
[ssh-remoting]: SSH-Remoting-in-PowerShell-Core.md
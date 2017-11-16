---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Spouštění vzdálených příkazů"
ms.assetid: d6938b56-7dc8-44ba-b4d4-cd7b169fd74d
ms.openlocfilehash: 5cf9690b8fe4549a99186f172cb6f0de156a4dea
ms.sourcegitcommit: c5251755c4442487f99ff74fadf7e37bbf039089
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/18/2017
---
# <a name="running-remote-commands"></a><span data-ttu-id="c35d8-103">Spouštění vzdálených příkazů</span><span class="sxs-lookup"><span data-stu-id="c35d8-103">Running Remote Commands</span></span>
<span data-ttu-id="c35d8-104">Příkazy můžete spustit na jednom nebo stovky počítačů pomocí jednoho příkazu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c35d8-104">You can run commands on one or hundreds of computers with a single Windows PowerShell command.</span></span> <span data-ttu-id="c35d8-105">Prostředí Windows PowerShell podporuje vzdálený přístup pomocí různých technologií, včetně WS-Management, rozhraní WMI a RPC.</span><span class="sxs-lookup"><span data-stu-id="c35d8-105">Windows PowerShell supports remote computing by using various technologies, including WMI, RPC, and WS-Management.</span></span>

## <a name="remoting-without-configuration"></a><span data-ttu-id="c35d8-106">Vzdálená komunikace bez konfigurace</span><span class="sxs-lookup"><span data-stu-id="c35d8-106">Remoting Without Configuration</span></span>
<span data-ttu-id="c35d8-107">Mnoho rutin prostředí Windows PowerShell mít parametr ComputerName, která umožňuje shromažďování dat a změňte nastavení na jeden nebo více vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="c35d8-107">Many Windows PowerShell cmdlets have the ComputerName parameter that enables you to collect data and change settings on one or more remote computers.</span></span> <span data-ttu-id="c35d8-108">Používají různé technologie komunikace a mnoho pracovních na všechny operační systémy Windows, které podporuje prostředí Windows PowerShell bez žádnou zvláštní konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="c35d8-108">They use a variety of communication technologies and many work on all Windows operating systems that Windows PowerShell supports without any special configuration.</span></span>

<span data-ttu-id="c35d8-109">Zahrnout tyto rutiny:</span><span class="sxs-lookup"><span data-stu-id="c35d8-109">These cmdlets include:</span></span>
* [<span data-ttu-id="c35d8-110">Restartování počítače</span><span class="sxs-lookup"><span data-stu-id="c35d8-110">Restart-Computer</span></span>](https://go.microsoft.com/fwlink/?LinkId=821625)
* [<span data-ttu-id="c35d8-111">Test připojení</span><span class="sxs-lookup"><span data-stu-id="c35d8-111">Test-Connection</span></span>](https://go.microsoft.com/fwlink/?LinkId=821646)
* [<span data-ttu-id="c35d8-112">Clear – protokolu událostí</span><span class="sxs-lookup"><span data-stu-id="c35d8-112">Clear-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821568)
* [<span data-ttu-id="c35d8-113">Get-protokolu událostí</span><span class="sxs-lookup"><span data-stu-id="c35d8-113">Get-EventLog</span></span>](https://go.microsoft.com/fwlink/?LinkId=821585)
* [<span data-ttu-id="c35d8-114">Get-oprav HotFix</span><span class="sxs-lookup"><span data-stu-id="c35d8-114">Get-HotFix</span></span>](https://go.microsoft.com/fwlink/?LinkId=821586)
  - [<span data-ttu-id="c35d8-115">Get-Process</span><span class="sxs-lookup"><span data-stu-id="c35d8-115">Get-Process</span></span>](https://go.microsoft.com/fwlink/?linkid=821590)
* [<span data-ttu-id="c35d8-116">Get-Service</span><span class="sxs-lookup"><span data-stu-id="c35d8-116">Get-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821593)
* [<span data-ttu-id="c35d8-117">Nastavení služby</span><span class="sxs-lookup"><span data-stu-id="c35d8-117">Set-Service</span></span>](https://go.microsoft.com/fwlink/?LinkId=821633)
* [<span data-ttu-id="c35d8-118">Get-WinEvent.</span><span class="sxs-lookup"><span data-stu-id="c35d8-118">Get-WinEvent</span></span>](https://go.microsoft.com/fwlink/?linkid=821529)
* [<span data-ttu-id="c35d8-119">Get-WmiObject</span><span class="sxs-lookup"><span data-stu-id="c35d8-119">Get-WmiObject</span></span>](https://go.microsoft.com/fwlink/?LinkId=821595)

<span data-ttu-id="c35d8-120">Rutiny, které podporují vzdálené komunikace bez zvláštní konfiguraci obvykle mají parametr ComputerName a nemají parametr relace.</span><span class="sxs-lookup"><span data-stu-id="c35d8-120">Typically, cmdlets that support remoting without special configuration have the ComputerName parameter and do not have the Session parameter.</span></span> <span data-ttu-id="c35d8-121">Chcete-li v relaci najít tyto rutiny, zadejte:</span><span class="sxs-lookup"><span data-stu-id="c35d8-121">To find these cmdlets in your session, type:</span></span>

```
Get-Command | where { $_.parameters.keys -contains "ComputerName" -and $_.parameters.keys -notcontains "Session"}
```

## <a name="windows-powershell-remoting"></a><span data-ttu-id="c35d8-122">Vzdálenou komunikaci Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c35d8-122">Windows PowerShell Remoting</span></span>
<span data-ttu-id="c35d8-123">Vzdálená komunikace prostředí Windows PowerShell, který používá protokol WS-Management, vám umožní spustit libovolný příkaz prostředí Windows PowerShell na jeden nebo více vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="c35d8-123">Windows PowerShell remoting, which uses the WS-Management protocol, lets you run any Windows PowerShell command on one or many remote computers.</span></span> <span data-ttu-id="c35d8-124">Umožňuje vytvořit trvalé připojení, spusťte interaktivní relace 1:1 a spouštět skripty ve více počítačích.</span><span class="sxs-lookup"><span data-stu-id="c35d8-124">It lets you establish persistent connections, start 1:1 interactive sessions, and run scripts on multiple computers.</span></span>

<span data-ttu-id="c35d8-125">Pokud chcete použít vzdálenou komunikaci prostředí Windows PowerShell, musí být vzdálený počítač konfigurován pro vzdálenou správu.</span><span class="sxs-lookup"><span data-stu-id="c35d8-125">To use Windows PowerShell remoting, the remote computer must be configured for remote management.</span></span> <span data-ttu-id="c35d8-126">Další informace, včetně pokynů, najdete v části [vzdálené požadavky](https://technet.microsoft.com/en-us/library/dd315349.aspx).</span><span class="sxs-lookup"><span data-stu-id="c35d8-126">For more information, including instructions, see [About Remote Requirements](https://technet.microsoft.com/en-us/library/dd315349.aspx).</span></span>

<span data-ttu-id="c35d8-127">Po dokončení konfigurace vzdálené komunikace Windows Powershellu jsou dostupné mnoho strategií vzdálené komunikace.</span><span class="sxs-lookup"><span data-stu-id="c35d8-127">After you have configured Windows PowerShell remoting, many remoting strategies are available to you.</span></span> <span data-ttu-id="c35d8-128">Zbývající část tohoto dokumentu jsou uvedeny jen některé z nich.</span><span class="sxs-lookup"><span data-stu-id="c35d8-128">The remainder of this document lists just a few of them.</span></span> <span data-ttu-id="c35d8-129">Další informace najdete v tématu [o vzdálené](https://technet.microsoft.com/en-us/library/dd347744.aspx) a [o vzdálené – nejčastější dotazy](https://technet.microsoft.com/en-us/library/dd347744.aspx).</span><span class="sxs-lookup"><span data-stu-id="c35d8-129">For more information, see [About Remote](https://technet.microsoft.com/en-us/library/dd347744.aspx) and [About Remote FAQ](https://technet.microsoft.com/en-us/library/dd347744.aspx).</span></span>

### <a name="start-an-interactive-session"></a><span data-ttu-id="c35d8-130">Spusťte interaktivní relace.</span><span class="sxs-lookup"><span data-stu-id="c35d8-130">Start an Interactive Session</span></span>
<span data-ttu-id="c35d8-131">Spusťte interaktivní relace s jeden vzdálený počítač pomocí [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c35d8-131">To start an interactive session with a single remote computer, use the [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) cmdlet.</span></span>
<span data-ttu-id="c35d8-132">Například spuštění interaktivní relace na vzdáleném počítači Server01, zadejte:</span><span class="sxs-lookup"><span data-stu-id="c35d8-132">For example, to start an interactive session with the Server01 remote computer, type:</span></span>

```
Enter-PSSession Server01
```

<span data-ttu-id="c35d8-133">Změny příkazového řádku a zobrazí se název počítače, do které jste připojeni.</span><span class="sxs-lookup"><span data-stu-id="c35d8-133">The command prompt changes to display the name of the computer to which you are connected.</span></span> <span data-ttu-id="c35d8-134">Od toho všechny příkazy, které zadejte v příkazovém řádku spusťte na vzdáleném počítači a výsledky jsou zobrazeny v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="c35d8-134">From then on, any commands that you type at the prompt run on the remote computer and the results are displayed on the local computer.</span></span>

<span data-ttu-id="c35d8-135">Chcete-li ukončit interaktivní relace, zadejte:</span><span class="sxs-lookup"><span data-stu-id="c35d8-135">To end the interactive session, type:</span></span>

```
Exit-PSSession
```

<span data-ttu-id="c35d8-136">Další informace o rutinách Enter-PSSession a ukončení-PSSession najdete v tématu [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) a [ukončení-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span><span class="sxs-lookup"><span data-stu-id="c35d8-136">For more information about the Enter-PSSession and Exit-PSSession cmdlets, see [Enter-PSSession](https://go.microsoft.com/fwlink/?LinkId=821477) and [Exit-PSSession](https://go.microsoft.com/fwlink/?LinkID=821478).</span></span>

### <a name="run-a-remote-command"></a><span data-ttu-id="c35d8-137">Spuštění vzdáleného příkazu</span><span class="sxs-lookup"><span data-stu-id="c35d8-137">Run a Remote Command</span></span>
<span data-ttu-id="c35d8-138">Chcete-li spustit libovolný příkaz na jeden nebo více vzdálených počítačích, použijte [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c35d8-138">To run any command on one or many remote computers, use the [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493) cmdlet.</span></span>
<span data-ttu-id="c35d8-139">Chcete-li například spustit [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) na Server01 a Server02 vzdálených počítačích, zadejte příkaz:</span><span class="sxs-lookup"><span data-stu-id="c35d8-139">For example, to run a [Get-UICulture](https://go.microsoft.com/fwlink/?LinkId=821806) command on the Server01 and Server02 remote computers, type:</span></span>

```
Invoke-Command -ComputerName Server01, Server02 -ScriptBlock {Get-UICulture}
```

<span data-ttu-id="c35d8-140">Výstup se vrací do vašeho počítače.</span><span class="sxs-lookup"><span data-stu-id="c35d8-140">The output is returned to your computer.</span></span>

```
LCID    Name     DisplayName               PSComputerName
----    ----     -----------               --------------
1033    en-US    English (United States)   server01.corp.fabrikam.com
1033    en-US    English (United States)   server02.corp.fabrikam.com
```
<span data-ttu-id="c35d8-141">Další informace o rutinu Invoke-Command najdete v tématu [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="c35d8-141">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="run-a-script"></a><span data-ttu-id="c35d8-142">Spustit skript</span><span class="sxs-lookup"><span data-stu-id="c35d8-142">Run a Script</span></span>
<span data-ttu-id="c35d8-143">Chcete-li spustit skript na jeden nebo více vzdálených počítačích, použijte parametr FilePath rutiny Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="c35d8-143">To run a script on one or many remote computers, use the FilePath parameter of the Invoke-Command cmdlet.</span></span> <span data-ttu-id="c35d8-144">Skript musí být na nebo přístupné pro místního počítače.</span><span class="sxs-lookup"><span data-stu-id="c35d8-144">The script must be on or accessible to your local computer.</span></span> <span data-ttu-id="c35d8-145">Výsledky jsou vráceny do místního počítače.</span><span class="sxs-lookup"><span data-stu-id="c35d8-145">The results are returned to your local computer.</span></span>

<span data-ttu-id="c35d8-146">Například následující příkaz spustí skript DiskCollect.ps1 na vzdálených počítačích Server01 a Server02.</span><span class="sxs-lookup"><span data-stu-id="c35d8-146">For example, the following command runs the DiskCollect.ps1 script on the Server01 and Server02 remote computers.</span></span>

```
Invoke-Command -ComputerName Server01, Server02 -FilePath c:\Scripts\DiskCollect.ps1
```

<span data-ttu-id="c35d8-147">Další informace o rutinu Invoke-Command najdete v tématu [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span><span class="sxs-lookup"><span data-stu-id="c35d8-147">For more information about the Invoke-Command cmdlet, see [Invoke-Command](https://go.microsoft.com/fwlink/?LinkId=821493).</span></span>

### <a name="establish-a-persistent-connection"></a><span data-ttu-id="c35d8-148">Trvalé připojení</span><span class="sxs-lookup"><span data-stu-id="c35d8-148">Establish a Persistent Connection</span></span>
<span data-ttu-id="c35d8-149">Pokud chcete spustit řadu související příkazy, které sdílet data, vytvoření relace na vzdáleném počítači a pak spusťte příkazy v relaci, kterou vytvoříte pomocí rutiny Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="c35d8-149">To run a series of related commands that share data, create a session on the remote computer and then use the Invoke-Command cmdlet to run commands in the session that you create.</span></span> <span data-ttu-id="c35d8-150">Pokud chcete vytvořit vzdálené relace, použijte rutinu New-PSSession.</span><span class="sxs-lookup"><span data-stu-id="c35d8-150">To create a remote session, use the New-PSSession cmdlet.</span></span>

<span data-ttu-id="c35d8-151">Například následující příkaz vytvoří relaci vzdálené počítače Server01 a jiná relace vzdáleného počítače Server02.</span><span class="sxs-lookup"><span data-stu-id="c35d8-151">For example, the following command creates a remote session on the Server01 computer and another remote session on the Server02 computer.</span></span> <span data-ttu-id="c35d8-152">Objekty relace ukládá v proměnné $s.</span><span class="sxs-lookup"><span data-stu-id="c35d8-152">It saves the session objects in the $s variable.</span></span>

```
$s = New-PSSession -ComputerName Server01, Server02
```

<span data-ttu-id="c35d8-153">Teď, když jsou určeny k relacím, můžete v nich spustit libovolný příkaz.</span><span class="sxs-lookup"><span data-stu-id="c35d8-153">Now that the sessions are established, you can run any command in them.</span></span> <span data-ttu-id="c35d8-154">A protože relací jsou trvalé, můžete shromažďování dat do jednoho příkazu a použít ho v následující příkaz.</span><span class="sxs-lookup"><span data-stu-id="c35d8-154">And because the sessions are persistent, you can collect data in one command and use it in a subsequent command.</span></span>

<span data-ttu-id="c35d8-155">Například následující příkaz spustí příkaz Get-opravu HotFix v relacích v $s proměnné a uloží výsledky v $h proměnné.</span><span class="sxs-lookup"><span data-stu-id="c35d8-155">For example, the following command runs a Get-HotFix command in the sessions in the $s variable and it saves the results in the $h variable.</span></span> <span data-ttu-id="c35d8-156">Proměnná $h je vytvořen v každé z relací v $s, ale neexistuje v místní relaci.</span><span class="sxs-lookup"><span data-stu-id="c35d8-156">The $h variable is created in each of the sessions in $s, but it does not exist in the local session.</span></span>

```
Invoke-Command -Session $s {$h = Get-HotFix}
```

<span data-ttu-id="c35d8-157">Nyní můžete v proměnné $h v dalších příkazech, jako je třeba následující data.</span><span class="sxs-lookup"><span data-stu-id="c35d8-157">Now you can use the data in the $h variable in subsequent commands, such as the following one.</span></span> <span data-ttu-id="c35d8-158">Výsledky jsou zobrazeny v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="c35d8-158">The results are displayed on the local computer.</span></span>

```
Invoke-Command -Session $s {$h | where {$_.InstalledBy -ne "NTAUTHORITY\SYSTEM"}}
```

### <a name="advanced-remoting"></a><span data-ttu-id="c35d8-159">Pokročilé vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="c35d8-159">Advanced Remoting</span></span>
<span data-ttu-id="c35d8-160">Vzdálená správa prostředí Windows PowerShell začíná právě tady.</span><span class="sxs-lookup"><span data-stu-id="c35d8-160">Windows PowerShell remote management just begins here.</span></span> <span data-ttu-id="c35d8-161">Pomocí rutin nainstalován pomocí prostředí Windows PowerShell můžete vytvořit a nakonfigurovat vzdálené relace z místních i vzdálených zakončení, vytvoření relace přizpůsobené a s omezeným přístupem, povolte uživatelům importovat příkazy ze vzdálené relace, které ve skutečnosti spuštěna implicitně na ke vzdálené relaci, nakonfigurujte zabezpečení vzdálené relace a mnoho dalšího.</span><span class="sxs-lookup"><span data-stu-id="c35d8-161">By using the cmdlets installed with Windows PowerShell, you can establish and configure remote sessions both from the local and remote ends, create customized and restricted sessions, allow users to import commands from a remote session that actually run implicitly on the remote session, configure the security of a remote session, and much more.</span></span>

<span data-ttu-id="c35d8-162">Pro usnadnění konfigurace vzdáleného, prostředí Windows PowerShell obsahuje poskytovatele WSMan.</span><span class="sxs-lookup"><span data-stu-id="c35d8-162">To facilitate remote configuration, Windows PowerShell includes a WSMan provider.</span></span> <span data-ttu-id="c35d8-163">WSMAN: jednotku, která se vytvoří zprostředkovatel umožňuje procházet hierarchie konfigurační nastavení v místním počítači a vzdálených počítačů.</span><span class="sxs-lookup"><span data-stu-id="c35d8-163">The WSMAN: drive that the provider creates lets you navigate through a hierarchy of configuration settings on the local computer and remote computers.</span></span>
<span data-ttu-id="c35d8-164">Další informace o poskytovateli WSMan najdete v tématu [WSMan zprostředkovatele](https://technet.microsoft.com/en-us/library/dd819476.aspx) a [o rutiny WS-Management](https://technet.microsoft.com/en-us/library/dd819481.aspx), nebo v konzole Windows PowerShell, zadejte "Get-Help wsman".</span><span class="sxs-lookup"><span data-stu-id="c35d8-164">For more information about the WSMan provider, see  [WSMan Provider](https://technet.microsoft.com/en-us/library/dd819476.aspx) and [About WS-Management Cmdlets](https://technet.microsoft.com/en-us/library/dd819481.aspx), or in the Windows PowerShell console, type "Get-Help wsman".</span></span>

<span data-ttu-id="c35d8-165">Další informace viz:</span><span class="sxs-lookup"><span data-stu-id="c35d8-165">For more information, see:</span></span>
- [<span data-ttu-id="c35d8-166">O vzdálené – nejčastější dotazy</span><span class="sxs-lookup"><span data-stu-id="c35d8-166">About Remote FAQ</span></span>](https://technet.microsoft.com/en-us/library/dd315359.aspx)
- [<span data-ttu-id="c35d8-167">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="c35d8-167">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="c35d8-168">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="c35d8-168">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)

<span data-ttu-id="c35d8-169">Pomoc s chybami vzdálenou komunikaci, najdete v tématu [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span><span class="sxs-lookup"><span data-stu-id="c35d8-169">For help with remoting errors, see [about_Remote_Troubleshooting](https://technet.microsoft.com/en-us/library/dd347642.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="c35d8-170">Viz také</span><span class="sxs-lookup"><span data-stu-id="c35d8-170">See Also</span></span>
- [<span data-ttu-id="c35d8-171">about_Remote</span><span class="sxs-lookup"><span data-stu-id="c35d8-171">about_Remote</span></span>](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)
- [<span data-ttu-id="c35d8-172">about_Remote_FAQ</span><span class="sxs-lookup"><span data-stu-id="c35d8-172">about_Remote_FAQ</span></span>](https://technet.microsoft.com/en-us/library/e23702fd-9415-4a98-9975-390a4d3adc42)
- [<span data-ttu-id="c35d8-173">about_Remote_Requirements</span><span class="sxs-lookup"><span data-stu-id="c35d8-173">about_Remote_Requirements</span></span>](https://technet.microsoft.com/en-us/library/da213949-134c-4741-b307-81f4492ba1bd)
- [<span data-ttu-id="c35d8-174">about_Remote_Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c35d8-174">about_Remote_Troubleshooting</span></span>](https://technet.microsoft.com/en-us/library/2f890148-8578-49ed-85ea-79a489dd6317)
- [<span data-ttu-id="c35d8-175">about_PSSessions</span><span class="sxs-lookup"><span data-stu-id="c35d8-175">about_PSSessions</span></span>](https://technet.microsoft.com/en-us/library/7a9b4e0e-fa1b-47b0-92f6-6e2995d70acb)
- [<span data-ttu-id="c35d8-176">about_WS Management_Cmdlets</span><span class="sxs-lookup"><span data-stu-id="c35d8-176">about_WS-Management_Cmdlets</span></span>](https://technet.microsoft.com/en-us/library/6ed3370a-ea10-45a5-9493-696aeace27ed)
- [<span data-ttu-id="c35d8-177">Invoke-Command</span><span class="sxs-lookup"><span data-stu-id="c35d8-177">Invoke-Command</span></span>](https://go.microsoft.com/fwlink/?LinkId=821493)
- [<span data-ttu-id="c35d8-178">Import-PSSession</span><span class="sxs-lookup"><span data-stu-id="c35d8-178">Import-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821821)
- [<span data-ttu-id="c35d8-179">Nový PSSession</span><span class="sxs-lookup"><span data-stu-id="c35d8-179">New-PSSession</span></span>](https://go.microsoft.com/fwlink/?LinkId=821498)
- [<span data-ttu-id="c35d8-180">Register-PSSessionConfiguration</span><span class="sxs-lookup"><span data-stu-id="c35d8-180">Register-PSSessionConfiguration</span></span>](https://go.microsoft.com/fwlink/?LinkId=821508)
- [<span data-ttu-id="c35d8-181">Zprostředkovatel služby WSMan</span><span class="sxs-lookup"><span data-stu-id="c35d8-181">WSMan Provider</span></span>](https://technet.microsoft.com/en-us/library/66fe1241-e08f-49ca-832f-a84c33ca8735)

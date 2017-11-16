---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Instalace sady SDK Windows PowerShell
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: c6acba828e469e716c80603ec2432176652a7280
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="installing-the-windows-powershell-sdk"></a><span data-ttu-id="305d6-103">Instalace sady SDK Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="305d6-103">Installing the Windows PowerShell SDK</span></span>

<span data-ttu-id="305d6-104">Následující téma popisuje postup instalace sady SDK prostředí PowerShell v různých verzích systému Windows.</span><span class="sxs-lookup"><span data-stu-id="305d6-104">The following topic describes how to install the PowerShell SDK on different versions of Windows.</span></span>

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a><span data-ttu-id="305d6-105">Instalace prostředí Windows PowerShell 3.0 SDK pro Windows 8 a Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="305d6-105">Installing Windows PowerShell 3.0 SDK for Windows 8 and Windows Server 2012</span></span>

<span data-ttu-id="305d6-106">Prostředí Windows PowerShell 3.0 je automaticky nainstalován ve Windows 8 a Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="305d6-106">Windows PowerShell 3.0 is automatically installed with Windows 8 and Windows Server 2012.</span></span>
<span data-ttu-id="305d6-107">Kromě toho můžete stáhnout a nainstalovat referenční sestavení pro prostředí Windows PowerShell 3.0 jako součást sady Windows 8 SDK.</span><span class="sxs-lookup"><span data-stu-id="305d6-107">In addition, you can download and install the reference assemblies for Windows PowerShell 3.0 as part of the Windows 8 SDK.</span></span>
<span data-ttu-id="305d6-108">Tyto sestavení umožňují zápisu rutiny, zprostředkovatele a hostitelských aplikací pro Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="305d6-108">These assemblies allow you to write cmdlets, providers, and host programs for Windows PowerShell 3.0.</span></span>
<span data-ttu-id="305d6-109">Když instalujete Windows SDK pro Windows 8, sestavení prostředí Windows PowerShell jsou automaticky nainstalovány do složky referenční sestavení, ve \Program soubory (x86) \Reference Assemblies\Microsoft\WindowsPowerShell\3.0.</span><span class="sxs-lookup"><span data-stu-id="305d6-109">When you install the Windows SDK for Windows 8, the Windows PowerShell assemblies are automatically installed in the reference assembly folder, in \Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0.</span></span>
<span data-ttu-id="305d6-110">Další informace najdete v tématu [stažení serveru Windows 8 SDK](http://msdn.microsoft.com/windows/hardware/hh852363.aspx).</span><span class="sxs-lookup"><span data-stu-id="305d6-110">For more information, see the [Windows 8 SDK download site](http://msdn.microsoft.com/windows/hardware/hh852363.aspx).</span></span>
<span data-ttu-id="305d6-111">Prostředí Windows PowerShell, ukázky kódu jsou k dispozici v centru vývoj.</span><span class="sxs-lookup"><span data-stu-id="305d6-111">Windows PowerShell code samples are also available on the Development Center.</span></span>
<span data-ttu-id="305d6-112">Další informace naleznete na stránce ukázka plochy kódu na [webu Dev center](http://code.msdn.microsoft.com/windowsdesktop/).</span><span class="sxs-lookup"><span data-stu-id="305d6-112">For more information, see the Desktop code sample page on the [Dev center site](http://code.msdn.microsoft.com/windowsdesktop/).</span></span>

<span data-ttu-id="305d6-113">Kromě toho prostředí Windows PowerShell 3.0 je zpětně kompatibilní s Windows PowerShell 2.0 SDK, který zahrnuje několik ukázky kódu.</span><span class="sxs-lookup"><span data-stu-id="305d6-113">In addition, Windows PowerShell 3.0 is backwards-compatible with the Windows PowerShell 2.0 SDK, which includes a number of code samples.</span></span>
<span data-ttu-id="305d6-114">Další informace o tom, jak stáhnout sadu SDK Windows PowerShell 2.0 najdete níže.</span><span class="sxs-lookup"><span data-stu-id="305d6-114">For more information on how to download the Windows PowerShell 2.0 SDK, see below.</span></span>
<span data-ttu-id="305d6-115">(Všimněte si, že ukázky 2.0 kódu jsou kompatibilní s Windows 8 a Windows PowerShell 3.0, nelze nainstalovat prostředí Windows PowerShell 2.0 na platformě Windows 8.)</span><span class="sxs-lookup"><span data-stu-id="305d6-115">(Note that while the 2.0 code samples are compatible with Windows 8 and Windows PowerShell 3.0, you cannot install Windows PowerShell 2.0 on a Windows 8 platform.)</span></span>

##<a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a><span data-ttu-id="305d6-116">Instalace prostředí Windows PowerShell 3.0 SDK pro systém Windows 7 a Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="305d6-116">Installing Windows PowerShell 3.0 SDK for Windows 7 and Windows Server 2008 R2</span></span>

<span data-ttu-id="305d6-117">Windows 7 a Windows Server 2008 R2 nainstalována automaticky prostředí PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="305d6-117">Windows 7 and Windows Server 2008 R2 automatically have PowerShell 2.0 installed.</span></span>
<span data-ttu-id="305d6-118">Kromě toho můžete nainstalovat prostředí PowerShell 3.0 v těchto systémech.</span><span class="sxs-lookup"><span data-stu-id="305d6-118">In addition, you can install PowerShell 3.0 on these systems.</span></span>
<span data-ttu-id="305d6-119">(Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).).</span><span class="sxs-lookup"><span data-stu-id="305d6-119">(For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).).</span></span>
<span data-ttu-id="305d6-120">Jak je popsáno výše, můžete taky nainstalovat sadu SDK Windows 8 na Windows 7 a Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="305d6-120">As described above, you can also install the Windows 8 SDK on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a><span data-ttu-id="305d6-121">Instalace prostředí Windows PowerShell 2.0 SDK pro systém Windows 7, Vista, XP, Server 2003 a Server 2008</span><span class="sxs-lookup"><span data-stu-id="305d6-121">Installing Windows PowerShell 2.0 SDK for Windows 7, Vista, XP, Server 2003, and Server 2008</span></span>

<span data-ttu-id="305d6-122">Windows PowerShell 2.0 SDK poskytuje referenční sestavení potřebná k zápisu rutiny, zprostředkovatele a hostování aplikace a poskytuje C# ukázkový kód, který lze použít jako výchozí bod, abyste před zahájením psaní kódu.</span><span class="sxs-lookup"><span data-stu-id="305d6-122">The Windows PowerShell 2.0 SDK provides the reference assemblies needed to write cmdlets, providers, and hosting applications, and it provides C# sample code that can be used as the starting point when you begin writing code.</span></span>

<span data-ttu-id="305d6-123">Chcete-li instalovat tuto sadu SDK, přečtěte si téma [Windows PowerShell 2.0 SDK](http://go.microsoft.com/fwlink/?LinkId=184611).</span><span class="sxs-lookup"><span data-stu-id="305d6-123">To install this SDK, see [Windows PowerShell 2.0 SDK](http://go.microsoft.com/fwlink/?LinkId=184611).</span></span>

## <a name="reference-assemblies"></a><span data-ttu-id="305d6-124">Odkaz na sestavení</span><span class="sxs-lookup"><span data-stu-id="305d6-124">Reference assemblies</span></span>

<span data-ttu-id="305d6-125">Referenční sestavení jsou ve výchozím nastavení nainstalován v následujícím umístění: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span><span class="sxs-lookup"><span data-stu-id="305d6-125">Reference assemblies are installed in the following location by default: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span></span>

> <span data-ttu-id="305d6-126">**Poznámka:**: kód, který se zkompiluje proti sestavení prostředí Windows PowerShell 2.0 nelze načíst do instalace prostředí Windows PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="305d6-126">**Note**: Code that is compiled against the Windows PowerShell 2.0 assemblies cannot be loaded into Windows PowerShell 1.0 installations.</span></span>
><span data-ttu-id="305d6-127">Kód, který se zkompiluje proti sestavení prostředí Windows PowerShell 1.0 však může být načtena do instalace prostředí Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="305d6-127">However, code that is compiled against the Windows PowerShell 1.0 assemblies can be loaded into Windows PowerShell 2.0 installations.</span></span>

## <a name="samples"></a><span data-ttu-id="305d6-128">Ukázky</span><span class="sxs-lookup"><span data-stu-id="305d6-128">Samples</span></span>

<span data-ttu-id="305d6-129">Ukázky kódu jsou standardně nainstalované v následujícím umístění: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span><span class="sxs-lookup"><span data-stu-id="305d6-129">Code samples are installed in the following location by default: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span></span>

<span data-ttu-id="305d6-130">Následující části obsahují stručný popis, jaké jsou jednotlivé vzorky.</span><span class="sxs-lookup"><span data-stu-id="305d6-130">The following sections provide a brief description of what each sample does.</span></span>

## <a name="cmdlet-samples"></a><span data-ttu-id="305d6-131">Ukázky rutiny</span><span class="sxs-lookup"><span data-stu-id="305d6-131">Cmdlet samples</span></span>
<span data-ttu-id="305d6-132">**GetProcessSample01**</span><span class="sxs-lookup"><span data-stu-id="305d6-132">**GetProcessSample01**</span></span>

<span data-ttu-id="305d6-133">Ukazuje, jak napsat jednoduchý rutinu, která načte všechny procesy v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="305d6-133">Shows how to write a simple cmdlet that gets all the processes on the local computer.</span></span>

<span data-ttu-id="305d6-134">**GetProcessSample02**</span><span class="sxs-lookup"><span data-stu-id="305d6-134">**GetProcessSample02**</span></span>

<span data-ttu-id="305d6-135">Ukazuje, jak přidat parametry do rutiny.</span><span class="sxs-lookup"><span data-stu-id="305d6-135">Shows how to add parameters to the cmdlet.</span></span>
<span data-ttu-id="305d6-136">Rutina trvá jeden nebo více názvů proces a vrátí odpovídající procesy.</span><span class="sxs-lookup"><span data-stu-id="305d6-136">The cmdlet takes one or more process names and returns the matching processes.</span></span>

<span data-ttu-id="305d6-137">**GetProcessSample03**</span><span class="sxs-lookup"><span data-stu-id="305d6-137">**GetProcessSample03**</span></span>

<span data-ttu-id="305d6-138">Ukazuje, jak přidat parametry, které přijímají vstup z kanálu.</span><span class="sxs-lookup"><span data-stu-id="305d6-138">Shows how to add parameters that accept input from the pipeline.</span></span>

<span data-ttu-id="305d6-139">**GetProcessSample04**</span><span class="sxs-lookup"><span data-stu-id="305d6-139">**GetProcessSample04**</span></span>

<span data-ttu-id="305d6-140">Ukazuje, jak se budou zpracovávat chyby nonterminating.</span><span class="sxs-lookup"><span data-stu-id="305d6-140">Shows how to handle nonterminating errors.</span></span>

<span data-ttu-id="305d6-141">**GetProcessSample05**</span><span class="sxs-lookup"><span data-stu-id="305d6-141">**GetProcessSample05**</span></span>

<span data-ttu-id="305d6-142">Ukazuje, jak zobrazit seznam procesů, zadaný.</span><span class="sxs-lookup"><span data-stu-id="305d6-142">Shows how to display a list of specified processes.</span></span>

<span data-ttu-id="305d6-143">**SelectObject –**</span><span class="sxs-lookup"><span data-stu-id="305d6-143">**SelectObject**</span></span>

<span data-ttu-id="305d6-144">Ukazuje, jak napsat filtru vybrat pouze určité objekty.</span><span class="sxs-lookup"><span data-stu-id="305d6-144">Shows how to write a filter to select only certain objects.</span></span>

<span data-ttu-id="305d6-145">**SelectString**</span><span class="sxs-lookup"><span data-stu-id="305d6-145">**SelectString**</span></span>

<span data-ttu-id="305d6-146">Ukazuje, jak pro hledání souborů pro zadaný vzory.</span><span class="sxs-lookup"><span data-stu-id="305d6-146">Shows how to search files for specified patterns.</span></span>

<span data-ttu-id="305d6-147">**StopProcessSample01**</span><span class="sxs-lookup"><span data-stu-id="305d6-147">**StopProcessSample01**</span></span>

<span data-ttu-id="305d6-148">Ukazuje, jak implementovat *PassThru* parametr a jak požádat o zpětnou vazbu od uživatelů voláním [ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx) a [ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="305d6-148">Shows how to implement a *PassThru* parameter, and how to request user feedback by calls to the [ShouldProcess](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldprocess.aspx) and [ShouldContinue](https://technet.microsoft.com/library/system.management.automation.cmdlet.shouldcontinue.aspx) methods.</span></span>
<span data-ttu-id="305d6-149">Zadejte uživatele *PassThru* parametr, když chtějí vynutit se rutina mohla vrátit objekt,</span><span class="sxs-lookup"><span data-stu-id="305d6-149">Users specify the *PassThru* parameter when they want to force the cmdlet to return an object,</span></span>

<span data-ttu-id="305d6-150">**StopProcessSample02**</span><span class="sxs-lookup"><span data-stu-id="305d6-150">**StopProcessSample02**</span></span>

<span data-ttu-id="305d6-151">Ukazuje, jak zastavit konkrétní proces.</span><span class="sxs-lookup"><span data-stu-id="305d6-151">Shows how to stop a specific process.</span></span>

<span data-ttu-id="305d6-152">**StopProcessSample03**</span><span class="sxs-lookup"><span data-stu-id="305d6-152">**StopProcessSample03**</span></span>

<span data-ttu-id="305d6-153">Ukazuje, jak deklarovat aliasy pro parametry a jak podporovat zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="305d6-153">Shows how to declare aliases for parameters and how to support wildcards.</span></span>

<span data-ttu-id="305d6-154">**StopProcessSample04**</span><span class="sxs-lookup"><span data-stu-id="305d6-154">**StopProcessSample04**</span></span>

<span data-ttu-id="305d6-155">Ukazuje, jak deklarovat sad parametrů, objekt, který rutina používá jako vstup a postup, zadejte parametr výchozí nastavení používá.</span><span class="sxs-lookup"><span data-stu-id="305d6-155">Shows how to declare parameter sets, the object that the cmdlet takes as input, and how to specify the default parameter set to use.</span></span>

## <a name="remoting-samples"></a><span data-ttu-id="305d6-156">Ukázky vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="305d6-156">Remoting samples</span></span>

<span data-ttu-id="305d6-157">**RemoteRunspace01**</span><span class="sxs-lookup"><span data-stu-id="305d6-157">**RemoteRunspace01**</span></span>

<span data-ttu-id="305d6-158">Ukazuje, jak vytvořit vzdálené prostředí runspace, který se používá k navázání připojení ke vzdálené.</span><span class="sxs-lookup"><span data-stu-id="305d6-158">Shows how to create a remote runspace that is used to establish a remote connection.</span></span>

<span data-ttu-id="305d6-159">**RemoteRunspacePool01**</span><span class="sxs-lookup"><span data-stu-id="305d6-159">**RemoteRunspacePool01**</span></span>

<span data-ttu-id="305d6-160">Ukazuje, jak vytvořit fond vzdálené prostředí runspace a jak souběžně spustit více příkazů pomocí tohoto fondu.</span><span class="sxs-lookup"><span data-stu-id="305d6-160">Shows how to construct a remote runspace pool and how to run multiple commands concurrently by using this pool.</span></span>

<span data-ttu-id="305d6-161">**Serialization01**</span><span class="sxs-lookup"><span data-stu-id="305d6-161">**Serialization01**</span></span>

<span data-ttu-id="305d6-162">Ukazuje, jak existující třídy rozhraní .NET a ujistěte se, že se zachovají informace z vybraných veřejných vlastností této třídy v serializaci nebo deserializaci.</span><span class="sxs-lookup"><span data-stu-id="305d6-162">Shows how to look at an existing .NET class and make sure that information from selected public properties of this class is preserved across serialization/deserialization.</span></span>

<span data-ttu-id="305d6-163">**Serialization02**</span><span class="sxs-lookup"><span data-stu-id="305d6-163">**Serialization02**</span></span>

<span data-ttu-id="305d6-164">Ukazuje, jak existující třídy rozhraní .NET a ujistěte se, že se zachovají informace z instance této třídy v serializaci nebo deserializaci když informace nejsou k dispozici v veřejné vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="305d6-164">Shows how to look at an existing .NET class and make sure that information from instance of this class is preserved across serialization/deserialization when the information is not available in public properties of the class.</span></span>

<span data-ttu-id="305d6-165">**Serialization03**</span><span class="sxs-lookup"><span data-stu-id="305d6-165">**Serialization03**</span></span>

<span data-ttu-id="305d6-166">Ukazuje, jak existující třídy rozhraní .NET a ujistěte se, že jsou instance této třídy a odvozených tříd deserializovat (rehydrated) do provozu objekty .NET.</span><span class="sxs-lookup"><span data-stu-id="305d6-166">Shows how to look at an existing .NET class and make sure that instances of this class and of derived classes are deserialized (rehydrated) into live .NET objects.</span></span>

## <a name="event-samples"></a><span data-ttu-id="305d6-167">Ukázky událostí</span><span class="sxs-lookup"><span data-stu-id="305d6-167">Event samples</span></span>

<span data-ttu-id="305d6-168">**Event01**</span><span class="sxs-lookup"><span data-stu-id="305d6-168">**Event01**</span></span>

<span data-ttu-id="305d6-169">Ukazuje, jak vytvořit rutinu pro registraci události odvozené z ObjectEventRegistrationBase.</span><span class="sxs-lookup"><span data-stu-id="305d6-169">Shows how to create a cmdlet for event registration by deriving from ObjectEventRegistrationBase.</span></span>

<span data-ttu-id="305d6-170">**Event02**</span><span class="sxs-lookup"><span data-stu-id="305d6-170">**Event02**</span></span>

<span data-ttu-id="305d6-171">Ukazuje, jak k ukazuje, jak k přijímání oznámení o události prostředí Windows PowerShell, které se generují ve vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="305d6-171">Shows how to shows how to receive notifications of Windows PowerShell events that are generated on remote computers.</span></span>
<span data-ttu-id="305d6-172">Používá událost PSEventReceived vystavenou přes [prostředí Runspace](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx) třídy.</span><span class="sxs-lookup"><span data-stu-id="305d6-172">It uses the PSEventReceived event exposed through the [Runspace](https://technet.microsoft.com/library/system.management.automation.runspaces.runspace.aspx) class.</span></span>

## <a name="hosting-application-samples"></a><span data-ttu-id="305d6-173">Hostování aplikace ukázky</span><span class="sxs-lookup"><span data-stu-id="305d6-173">Hosting application samples</span></span>

<span data-ttu-id="305d6-174">**Runspace01**</span><span class="sxs-lookup"><span data-stu-id="305d6-174">**Runspace01**</span></span>

<span data-ttu-id="305d6-175">Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třídy ke spuštění [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutiny synchronně.</span><span class="sxs-lookup"><span data-stu-id="305d6-175">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run the [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet synchronously.</span></span>
<span data-ttu-id="305d6-176">[Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutina vrátí [proces](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý proces, který běží v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="305d6-176">The [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer.</span></span>

<span data-ttu-id="305d6-177">**Runspace02**</span><span class="sxs-lookup"><span data-stu-id="305d6-177">**Runspace02**</span></span>

<span data-ttu-id="305d6-178">Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třídy ke spuštění [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) a [řazení objektu](http://go.microsoft.com/fwlink/?LinkID=113403) rutiny synchronně.</span><span class="sxs-lookup"><span data-stu-id="305d6-178">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run the [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) and [Sort-Object](http://go.microsoft.com/fwlink/?LinkID=113403) cmdlets synchronously.</span></span>
<span data-ttu-id="305d6-179">[Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutina vrátí [proces](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý zpracování spuštěna v místním počítači a objekt řazení seřadí objekty na základě jejich [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) vlastnost.</span><span class="sxs-lookup"><span data-stu-id="305d6-179">The [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer, and the Sort-Object sorts the objects based on their [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) property.</span></span>
<span data-ttu-id="305d6-180">Výsledky z těchto příkazů se zobrazí pomocí [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="305d6-180">The results of these commands is displayed by using a [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) control.</span></span>

<span data-ttu-id="305d6-181">**Runspace03**</span><span class="sxs-lookup"><span data-stu-id="305d6-181">**Runspace03**</span></span>

<span data-ttu-id="305d6-182">Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třída synchronně spustit skript a jak se budou zpracovávat chyby neukončující.</span><span class="sxs-lookup"><span data-stu-id="305d6-182">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run a script synchronously, and how to handle non-terminating errors.</span></span>
<span data-ttu-id="305d6-183">Skript přijímá seznam názvů proces a potom načte těchto procesů.</span><span class="sxs-lookup"><span data-stu-id="305d6-183">The script receives a list of process names and then retrieves those processes.</span></span>
<span data-ttu-id="305d6-184">Výsledky skriptu, včetně všech jiných ukončován chyb, které byly generovány při spuštění skriptu, jsou zobrazeny v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="305d6-184">The results of the script, including any non-terminating errors that were generated when running the script, are displayed in a console window.</span></span>

<span data-ttu-id="305d6-185">**Runspace04**</span><span class="sxs-lookup"><span data-stu-id="305d6-185">**Runspace04**</span></span>

<span data-ttu-id="305d6-186">Ukazuje, jak používat [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) třídy ke spuštění příkazů a jak catch ukončující chyby, které se vyvolá, když spustíte příkaz.</span><span class="sxs-lookup"><span data-stu-id="305d6-186">Shows how to use the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) class to run commands, and how to catch terminating errors that are thrown when running the commands.</span></span>
<span data-ttu-id="305d6-187">Dva příkazy se spouštějí a poslední příkaz se předá parametr argument, který není platný.</span><span class="sxs-lookup"><span data-stu-id="305d6-187">Two commands are run, and the last command is passed a parameter argument that is not valid.</span></span>
<span data-ttu-id="305d6-188">V důsledku toho jsou vráceny žádné objekty a je vyvolána ukončující chyba.</span><span class="sxs-lookup"><span data-stu-id="305d6-188">As a result, no objects are returned and a terminating error is thrown.</span></span>

<span data-ttu-id="305d6-189">**Runspace05**</span><span class="sxs-lookup"><span data-stu-id="305d6-189">**Runspace05**</span></span>

<span data-ttu-id="305d6-190">Ukazuje, jak přidat modul snap-in k [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektu, aby rutiny modulu snap-in k dispozici, když je otevřen prostředí runspace.</span><span class="sxs-lookup"><span data-stu-id="305d6-190">Shows how to add a snap-in to an [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) object so that the cmdlet of the snap-in is available when the runspace is opened.</span></span>
<span data-ttu-id="305d6-191">Modul snap-in poskytuje rutiny Get-Proc (definované [GetProcessSample01 ukázka](https://technet.microsoft.com/library/ff602028.aspx)) je synchronně spustit pomocí [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektu.</span><span class="sxs-lookup"><span data-stu-id="305d6-191">The snap-in provides a Get-Proc cmdlet (defined by the [GetProcessSample01 Sample](https://technet.microsoft.com/library/ff602028.aspx)) that is run synchronously by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="305d6-192">**Runspace06**</span><span class="sxs-lookup"><span data-stu-id="305d6-192">**Runspace06**</span></span>

<span data-ttu-id="305d6-193">Popisuje postup pro přidání modulu do [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektu tak, aby modul je načtena, když je otevřen prostředí runspace.</span><span class="sxs-lookup"><span data-stu-id="305d6-193">Shows how to add a module to an [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) object so that the module is loaded when the runspace is opened.</span></span>
<span data-ttu-id="305d6-194">Modul poskytuje rutiny Get-Proc (definované [GetProcessSample02 ukázka](https://technet.microsoft.com/library/ff602027.aspx)) je synchronně spustit pomocí [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektu.</span><span class="sxs-lookup"><span data-stu-id="305d6-194">The module provides a Get-Proc cmdlet (defined by the [GetProcessSample02 Sample](https://technet.microsoft.com/library/ff602027.aspx)) that is run synchronously by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="305d6-195">**Runspace07**</span><span class="sxs-lookup"><span data-stu-id="305d6-195">**Runspace07**</span></span>

<span data-ttu-id="305d6-196">Ukazuje, jak vytvořit prostředí runspace a pak použít rutin dvě synchronně pomocí tohoto prostředí runspace [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objektu.</span><span class="sxs-lookup"><span data-stu-id="305d6-196">Shows how to create a runspace, and then use that runspace to run two cmdlets synchronously by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="305d6-197">**Runspace08**</span><span class="sxs-lookup"><span data-stu-id="305d6-197">**Runspace08**</span></span>

<span data-ttu-id="305d6-198">Ukazuje, jak přidat příkazy a argumenty do kanálu nástroje [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objekt a jak spouštět příkazy synchronně.</span><span class="sxs-lookup"><span data-stu-id="305d6-198">Shows how to add commands and arguments to the pipeline of a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object and how to run the commands synchronously.</span></span>

<span data-ttu-id="305d6-199">**Runspace09**</span><span class="sxs-lookup"><span data-stu-id="305d6-199">**Runspace09**</span></span>

<span data-ttu-id="305d6-200">Ukazuje, jak přidat skript do kanálu nástroje [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) objekt a postupy pro spuštění skriptu asynchronně.</span><span class="sxs-lookup"><span data-stu-id="305d6-200">Shows how to add a script to the pipeline of a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object and how to run the script asynchronously.</span></span>
<span data-ttu-id="305d6-201">Události se používají pro zpracování výstup skriptu.</span><span class="sxs-lookup"><span data-stu-id="305d6-201">Events are used to handle the output of the script.</span></span>

<span data-ttu-id="305d6-202">**Runspace10**</span><span class="sxs-lookup"><span data-stu-id="305d6-202">**Runspace10**</span></span>

<span data-ttu-id="305d6-203">Ukazuje, jak vytvořit počáteční relace do výchozího stavu postup přidání rutiny [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), jak vytvořit prostředí runspace, který používá stav relace počáteční a jak spustit pomocí příkazu [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx)objektu.</span><span class="sxs-lookup"><span data-stu-id="305d6-203">Shows how to create a default initial session state, how to add a cmdlet to the [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx), how to create a runspace that uses the initial session state, and how to run the command by using a [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) object.</span></span>

<span data-ttu-id="305d6-204">**Runspace11**</span><span class="sxs-lookup"><span data-stu-id="305d6-204">**Runspace11**</span></span>

<span data-ttu-id="305d6-205">Ukazuje, jak používat [ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx) třídy za účelem vytvoření příkaz proxy serveru, který volá existující rutiny, ale omezuje sadu parametrů, k dispozici.</span><span class="sxs-lookup"><span data-stu-id="305d6-205">Shows how to use the [ProxyCommand](https://technet.microsoft.com/library/system.management.automation.proxycommand.aspx) class to create a proxy command that calls an existing cmdlet, but restricts the set of available parameters.</span></span>
<span data-ttu-id="305d6-206">Příkaz proxy serveru se pak přidá do stavu počáteční relace, který se používá k vytvoření omezené prostředí runspace.</span><span class="sxs-lookup"><span data-stu-id="305d6-206">The proxy command is then added to an initial session state that is used to create a constrained runspace.</span></span>
<span data-ttu-id="305d6-207">To znamená, že uživatel může přistupovat k funkcím rutiny pouze pomocí příkazu proxy.</span><span class="sxs-lookup"><span data-stu-id="305d6-207">This means that the user can access the functionality of the cmdlet only through the proxy command.</span></span>

<span data-ttu-id="305d6-208">**PowerShell01**</span><span class="sxs-lookup"><span data-stu-id="305d6-208">**PowerShell01**</span></span>

<span data-ttu-id="305d6-209">Ukazuje, jak vytvořit omezené prostředí runspace pomocí [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) objektu.</span><span class="sxs-lookup"><span data-stu-id="305d6-209">Shows how to create a constrained runspace using an [InitialSessionState](https://technet.microsoft.com/library/system.management.automation.runspaces.initialsessionstate.aspx) object.</span></span>

<span data-ttu-id="305d6-210">**PowerShell02**</span><span class="sxs-lookup"><span data-stu-id="305d6-210">**PowerShell02**</span></span>

<span data-ttu-id="305d6-211">Ukazuje, jak používat prostředí runspace fondu současně spustit více příkazů.</span><span class="sxs-lookup"><span data-stu-id="305d6-211">Shows how to use a runspace pool to run multiple commands concurrently.</span></span>

## <a name="host-samples"></a><span data-ttu-id="305d6-212">Ukázky hostitele</span><span class="sxs-lookup"><span data-stu-id="305d6-212">Host samples</span></span>

<span data-ttu-id="305d6-213">**Host01**</span><span class="sxs-lookup"><span data-stu-id="305d6-213">**Host01**</span></span>

<span data-ttu-id="305d6-214">Ukazuje, jak implementovat hostitelskou aplikaci, která používá vlastní hostitel.</span><span class="sxs-lookup"><span data-stu-id="305d6-214">Shows how to implement a host application that uses a custom host.</span></span>
<span data-ttu-id="305d6-215">V této ukázce je vytvořena prostředí runspace, která používá vlastní hostitel a potom [prostředí PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) rozhraní API slouží k spustit skript, který volá "Ukončete".</span><span class="sxs-lookup"><span data-stu-id="305d6-215">In this sample a runspace is created that uses the custom host, and then the [PowerShell](https://technet.microsoft.com/library/system.management.automation.powershell.aspx) API is used to run a script that calls "exit".</span></span>
<span data-ttu-id="305d6-216">Hostitelskou aplikaci pak porovná výstup skriptu a zobrazí výsledky.</span><span class="sxs-lookup"><span data-stu-id="305d6-216">The host application then looks at the output of the script and prints out the results.</span></span>

<span data-ttu-id="305d6-217">**Host02**</span><span class="sxs-lookup"><span data-stu-id="305d6-217">**Host02**</span></span>

<span data-ttu-id="305d6-218">Ukazuje, jak psát aplikace hostitele používající modul runtime prostředí Windows PowerShell společně s implementace vlastního hostitele.</span><span class="sxs-lookup"><span data-stu-id="305d6-218">Shows how to write a host application that uses the Windows PowerShell runtime along with a custom host implementation.</span></span>
<span data-ttu-id="305d6-219">Hostitelskou aplikaci nastaví hostitele jazykovou verzi, němčina, spustí [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) rutiny a zobrazí výsledky podle by zobrazovat pomocí pwrsh.exe a potom vytiskne aktuální datum a čas v němčině.</span><span class="sxs-lookup"><span data-stu-id="305d6-219">The host application sets the host culture to German, runs the [Get-Process](http://go.microsoft.com/fwlink/?LinkId=113324) cmdlet and displays the results as you would see them by using pwrsh.exe, and then prints out the current data and time in German.</span></span>

<span data-ttu-id="305d6-220">**Host03**</span><span class="sxs-lookup"><span data-stu-id="305d6-220">**Host03**</span></span>

<span data-ttu-id="305d6-221">Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="305d6-221">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>

<span data-ttu-id="305d6-222">**Host04**</span><span class="sxs-lookup"><span data-stu-id="305d6-222">**Host04**</span></span>

<span data-ttu-id="305d6-223">Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="305d6-223">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="305d6-224">Tato aplikace hostitele také podporuje zobrazování výzev, které umožní uživateli zadat více možností.</span><span class="sxs-lookup"><span data-stu-id="305d6-224">This host application also supports displaying prompts that allow the user to specify multiple choices.</span></span>

<span data-ttu-id="305d6-225">**Host05**</span><span class="sxs-lookup"><span data-stu-id="305d6-225">**Host05**</span></span>

<span data-ttu-id="305d6-226">Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="305d6-226">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="305d6-227">Tato aplikace hostitele taky podporuje volání vzdálených počítačů pomocí [Enter-PsSession](http://go.microsoft.com/fwlink/?LinkId=135210) a [ukončení-PsSession](http://go.microsoft.com/fwlink/?LinkId=135212) rutiny.</span><span class="sxs-lookup"><span data-stu-id="305d6-227">This host application also supports calls to remote computers by using the [Enter-PsSession](http://go.microsoft.com/fwlink/?LinkId=135210) and [Exit-PsSession](http://go.microsoft.com/fwlink/?LinkId=135212) cmdlets.</span></span>

<span data-ttu-id="305d6-228">**Host06**</span><span class="sxs-lookup"><span data-stu-id="305d6-228">**Host06**</span></span>

<span data-ttu-id="305d6-229">Ukazuje, jak sestavit aplikaci Interaktivní hostitele pomocí konzoly, která čte příkazy z příkazového řádku, provede příkazy a potom zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="305d6-229">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="305d6-230">Kromě toho tato ukázka pomocí rozhraní API Tokenizátor Určuje barvu textu, který je zadaný uživatel.</span><span class="sxs-lookup"><span data-stu-id="305d6-230">In addition, this sample uses the Tokenizer APIs to specify the color of the text that is entered by the user.</span></span>

## <a name="provider-samples"></a><span data-ttu-id="305d6-231">Ukázky zprostředkovatele</span><span class="sxs-lookup"><span data-stu-id="305d6-231">Provider samples</span></span>

<span data-ttu-id="305d6-232">**AccessDBProviderSample01**</span><span class="sxs-lookup"><span data-stu-id="305d6-232">**AccessDBProviderSample01**</span></span>

<span data-ttu-id="305d6-233">Ukazuje, jak deklarovat zprostředkovatele třídu, která pochází přímo z [CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx) třídy.</span><span class="sxs-lookup"><span data-stu-id="305d6-233">Shows how to declare a provider class that derives directly from the [CmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.cmdletprovider.aspx) class.</span></span>
<span data-ttu-id="305d6-234">Je zde uveden pouze pro úplnost.</span><span class="sxs-lookup"><span data-stu-id="305d6-234">It is included here only for completeness.</span></span>

<span data-ttu-id="305d6-235">**AccessDBProviderSample02**</span><span class="sxs-lookup"><span data-stu-id="305d6-235">**AccessDBProviderSample02**</span></span>

<span data-ttu-id="305d6-236">Ukazuje, jak přepsat [NewDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx) a [RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx) metody pro podporu volání rutiny New-PSDrive a PSDrive odebrat.</span><span class="sxs-lookup"><span data-stu-id="305d6-236">Shows how to overwrite the [NewDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.newdrive.aspx) and [RemoveDrive](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.removedrive.aspx) methods to support calls to the New-PSDrive and Remove-PSDrive cmdlets.</span></span>
<span data-ttu-id="305d6-237">Třída zprostředkovatele v této ukázce je odvozena z [DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx) třídy.</span><span class="sxs-lookup"><span data-stu-id="305d6-237">The provider class in this sample derives from the [DriveCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.drivecmdletprovider.aspx) class.</span></span>

<span data-ttu-id="305d6-238">**AccessDBProviderSample03**</span><span class="sxs-lookup"><span data-stu-id="305d6-238">**AccessDBProviderSample03**</span></span>

<span data-ttu-id="305d6-239">Ukazuje, jak přepsat [GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx) a [SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx) metody pro podporu volání rutiny Get-Item a sadu položek.</span><span class="sxs-lookup"><span data-stu-id="305d6-239">Shows how to overwrite the [GetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.getitem.aspx) and [SetItem](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.setitem.aspx) methods to support calls to the Get-Item and Set-Item cmdlets.</span></span>
<span data-ttu-id="305d6-240">Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) třídy.</span><span class="sxs-lookup"><span data-stu-id="305d6-240">The provider class in this sample derives from the [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) class.</span></span>

<span data-ttu-id="305d6-241">**AccessDBProviderSample04**</span><span class="sxs-lookup"><span data-stu-id="305d6-241">**AccessDBProviderSample04**</span></span>

<span data-ttu-id="305d6-242">Ukazuje, jak k přepsání metody kontejner pro podporu volání Copy-Item, Get-ChildItem, nové položky a rutiny Remove-položky.</span><span class="sxs-lookup"><span data-stu-id="305d6-242">Shows how to overwrite container methods to support calls to the Copy-Item, Get-ChildItem, New-Item, and Remove-Item cmdlets.</span></span>
<span data-ttu-id="305d6-243">Tyto metody by měla být implementována, pokud úložiště dat obsahuje položky, které jsou kontejnery.</span><span class="sxs-lookup"><span data-stu-id="305d6-243">These methods should be implemented when the data store contains items that are containers.</span></span>
<span data-ttu-id="305d6-244">Kontejner je skupina podřízené položky v rámci běžných nadřazené položky.</span><span class="sxs-lookup"><span data-stu-id="305d6-244">A container is a group of child items under a common parent item.</span></span>
<span data-ttu-id="305d6-245">Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) třídy.</span><span class="sxs-lookup"><span data-stu-id="305d6-245">The provider class in this sample derives from the [ItemCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.itemcmdletprovider.aspx) class.</span></span>

<span data-ttu-id="305d6-246">**AccessDBProviderSample05**</span><span class="sxs-lookup"><span data-stu-id="305d6-246">**AccessDBProviderSample05**</span></span>

<span data-ttu-id="305d6-247">Ukazuje, jak k přepsání metody kontejner pro podporu volání rutiny přesunout položku a připojení k cestě.</span><span class="sxs-lookup"><span data-stu-id="305d6-247">Shows how to overwrite container methods to support calls to the Move-Item and Join-Path cmdlets.</span></span>
<span data-ttu-id="305d6-248">Tyto metody by měla být implementována, pokud uživatel musí přesunout položky do kontejneru, a v případě úložiště dat obsahuje vnořené kontejnery.</span><span class="sxs-lookup"><span data-stu-id="305d6-248">These methods should be implemented when the user needs to move items within a container and if the data store contains nested containers.</span></span>
<span data-ttu-id="305d6-249">Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) třídy.</span><span class="sxs-lookup"><span data-stu-id="305d6-249">The provider class in this sample derives from the [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) class.</span></span>

<span data-ttu-id="305d6-250">**AccessDBProviderSample06**</span><span class="sxs-lookup"><span data-stu-id="305d6-250">**AccessDBProviderSample06**</span></span>

<span data-ttu-id="305d6-251">Ukazuje, jak k přepsání obsahu metody pro podporu volání Clear-obsahu, Get-obsahu a obsahu sady rutin.</span><span class="sxs-lookup"><span data-stu-id="305d6-251">Shows how to overwrite content methods to support calls to the Clear-Content, Get-Content, and Set-Content cmdlets.</span></span>
<span data-ttu-id="305d6-252">Tyto metody by měla být implementována, když uživatel potřebuje ke správě obsahu položek v úložišti.</span><span class="sxs-lookup"><span data-stu-id="305d6-252">These methods should be implemented when the user needs to manage the content of the items in the data store.</span></span>
<span data-ttu-id="305d6-253">Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) třídy ale implementuje [IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx) rozhraní.</span><span class="sxs-lookup"><span data-stu-id="305d6-253">The provider class in this sample derives from the [NavigationCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider.aspx) class, and it implements the [IContentCmdletProvider](https://technet.microsoft.com/library/system.management.automation.provider.icontentcmdletprovider.aspx) interface.</span></span>


---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Instalace sady SDK Windows PowerShellu
ms.assetid: c3636b45-61aa-4720-85f0-58312c4fc8f9
ms.openlocfilehash: fa876bac0c1afac24f93d11dd2e7ecfb1165cf5f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893534"
---
# <a name="installing-the-windows-powershell-sdk"></a><span data-ttu-id="495a2-103">Instalace sady SDK Windows PowerShellu</span><span class="sxs-lookup"><span data-stu-id="495a2-103">Installing the Windows PowerShell SDK</span></span>

<span data-ttu-id="495a2-104">Následující téma popisuje, jak nainstalovat sadu SDK prostředí PowerShell v různých verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="495a2-104">The following topic describes how to install the PowerShell SDK on different versions of Windows.</span></span>

## <a name="installing-windows-powershell-30-sdk-for-windows-8-and-windows-server-2012"></a><span data-ttu-id="495a2-105">Instalace prostředí Windows PowerShell 3.0 SDK pro Windows 8 a Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="495a2-105">Installing Windows PowerShell 3.0 SDK for Windows 8 and Windows Server 2012</span></span>

<span data-ttu-id="495a2-106">Windows PowerShell 3.0 je automaticky nainstalován se systémem Windows 8 a Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="495a2-106">Windows PowerShell 3.0 is automatically installed with Windows 8 and Windows Server 2012.</span></span>
<span data-ttu-id="495a2-107">Kromě toho můžete stáhnout a nainstalovat referenční sestavení pro Windows PowerShell 3.0 jako součást sady SDK pro Windows 8.</span><span class="sxs-lookup"><span data-stu-id="495a2-107">In addition, you can download and install the reference assemblies for Windows PowerShell 3.0 as part of the Windows 8 SDK.</span></span>
<span data-ttu-id="495a2-108">Tato sestavení umožňuje psát rutiny, poskytovatelů a hostitele aplikací pro Windows PowerShell 3.0.</span><span class="sxs-lookup"><span data-stu-id="495a2-108">These assemblies allow you to write cmdlets, providers, and host programs for Windows PowerShell 3.0.</span></span>
<span data-ttu-id="495a2-109">Když instalujete Windows SDK pro Windows 8, sestavení prostředí Windows PowerShell jsou automaticky nainstalovány ve složce odkaz na sestavení v `\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0`.</span><span class="sxs-lookup"><span data-stu-id="495a2-109">When you install the Windows SDK for Windows 8, the Windows PowerShell assemblies are automatically installed in the reference assembly folder, in `\Program Files (x86)\Reference Assemblies\Microsoft\WindowsPowerShell\3.0`.</span></span>
<span data-ttu-id="495a2-110">Další informace najdete v tématu [serveru pro Windows 8 SDK stahování](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive).</span><span class="sxs-lookup"><span data-stu-id="495a2-110">For more information, see the [Windows 8 SDK download site](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive).</span></span>
<span data-ttu-id="495a2-111">Ukázky kódu v prostředí Windows PowerShell jsou k dispozici také na Centrum pro vývoj.</span><span class="sxs-lookup"><span data-stu-id="495a2-111">Windows PowerShell code samples are also available on the Development Center.</span></span>
<span data-ttu-id="495a2-112">Další informace najdete v tématu ukázkové desktopové znakovou stránku na [webu Dev center](https://code.msdn.microsoft.com:443/windowsdesktop/).</span><span class="sxs-lookup"><span data-stu-id="495a2-112">For more information, see the Desktop code sample page on the [Dev center site](https://code.msdn.microsoft.com:443/windowsdesktop/).</span></span>

<span data-ttu-id="495a2-113">Kromě toho Windows PowerShell 3.0 je zpětně kompatibilní se sadou SDK Windows Powershellu 2.0, která zahrnuje celou řadu ukázek kódu.</span><span class="sxs-lookup"><span data-stu-id="495a2-113">In addition, Windows PowerShell 3.0 is backwards-compatible with the Windows PowerShell 2.0 SDK, which includes a number of code samples.</span></span>
<span data-ttu-id="495a2-114">Další informace o tom, jak stáhnout sadu SDK Windows Powershellu 2.0 najdete níže.</span><span class="sxs-lookup"><span data-stu-id="495a2-114">For more information on how to download the Windows PowerShell 2.0 SDK, see below.</span></span>
<span data-ttu-id="495a2-115">(Všimněte si, že ukázky kódu 2.0 jsou kompatibilní se systémem Windows 8 a Windows PowerShell 3.0, nelze nainstalovat Windows PowerShell 2.0 na platformě Windows 8.)</span><span class="sxs-lookup"><span data-stu-id="495a2-115">(Note that while the 2.0 code samples are compatible with Windows 8 and Windows PowerShell 3.0, you cannot install Windows PowerShell 2.0 on a Windows 8 platform.)</span></span>

## <a name="installing-windows-powershell-30-sdk-for-windows-7-and-windows-server-2008-r2"></a><span data-ttu-id="495a2-116">Instalace prostředí Windows PowerShell 3.0 SDK pro Windows 7 a Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="495a2-116">Installing Windows PowerShell 3.0 SDK for Windows 7 and Windows Server 2008 R2</span></span>

<span data-ttu-id="495a2-117">Windows 7 a Windows Server 2008 R2 mít automaticky nainstalovanou prostředí PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="495a2-117">Windows 7 and Windows Server 2008 R2 automatically have PowerShell 2.0 installed.</span></span>
<span data-ttu-id="495a2-118">Kromě toho můžete nainstalovat prostředí PowerShell 3.0 v těchto systémech.</span><span class="sxs-lookup"><span data-stu-id="495a2-118">In addition, you can install PowerShell 3.0 on these systems.</span></span>
<span data-ttu-id="495a2-119">(Další informace najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).).</span><span class="sxs-lookup"><span data-stu-id="495a2-119">(For more information, see [Installing Windows PowerShell](Installing-Windows-PowerShell.md).).</span></span>
<span data-ttu-id="495a2-120">Jak je popsáno výše, můžete také nainstalovat sady SDK Windows 8 na Windows 7 a Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="495a2-120">As described above, you can also install the Windows 8 SDK on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="installing-windows-powershell-20-sdk-for-windows-7-vista-xp-server-2003-and-server-2008"></a><span data-ttu-id="495a2-121">Instalace prostředí Windows PowerShell 2.0 SDK pro Windows 7, Vista, XP, Server 2003 a Server 2008</span><span class="sxs-lookup"><span data-stu-id="495a2-121">Installing Windows PowerShell 2.0 SDK for Windows 7, Vista, XP, Server 2003, and Server 2008</span></span>

<span data-ttu-id="495a2-122">Sady SDK Windows Powershellu 2.0 poskytuje referenční sestavení potřebná k zápisu rutiny, poskytovatelů a hostování aplikací, a poskytuje C# ukázkového kódu, který může sloužit jako výchozí bod, když začnete psát kód.</span><span class="sxs-lookup"><span data-stu-id="495a2-122">The Windows PowerShell 2.0 SDK provides the reference assemblies needed to write cmdlets, providers, and hosting applications, and it provides C# sample code that can be used as the starting point when you begin writing code.</span></span>

<span data-ttu-id="495a2-123">Instalaci této sady SDK najdete v tématu [sady SDK Windows Powershellu 2.0](http://www.microsoft.com/en-us/download/details.aspx?id=2560).</span><span class="sxs-lookup"><span data-stu-id="495a2-123">To install this SDK, see [Windows PowerShell 2.0 SDK](http://www.microsoft.com/en-us/download/details.aspx?id=2560).</span></span>

## <a name="reference-assemblies"></a><span data-ttu-id="495a2-124">Referenční sestavení</span><span class="sxs-lookup"><span data-stu-id="495a2-124">Reference assemblies</span></span>

<span data-ttu-id="495a2-125">Referenční sestavení jsou ve výchozím nastavení nainstalován v následujícím umístění: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span><span class="sxs-lookup"><span data-stu-id="495a2-125">Reference assemblies are installed in the following location by default: `c:\Program Files\Reference Assemblies\Microsoft\WindowsPowerShell\V1.0`.</span></span>

> [!NOTE] 
> <span data-ttu-id="495a2-126">Kód, který je zkompilován proti sestavení Windows PowerShell 2.0 nelze načíst do zařízení Windows PowerShell 1.0.</span><span class="sxs-lookup"><span data-stu-id="495a2-126">Code that is compiled against the Windows PowerShell 2.0 assemblies cannot be loaded into Windows PowerShell 1.0 installations.</span></span>
> <span data-ttu-id="495a2-127">Nicméně kód, který je zkompilován proti sestavení Windows PowerShell 1.0 je možné načíst do instalace Windows PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="495a2-127">However, code that is compiled against the Windows PowerShell 1.0 assemblies can be loaded into Windows PowerShell 2.0 installations.</span></span>

## <a name="samples"></a><span data-ttu-id="495a2-128">Ukázky</span><span class="sxs-lookup"><span data-stu-id="495a2-128">Samples</span></span>

<span data-ttu-id="495a2-129">Ukázky kódu jsou nainstalovány v následujícím umístění ve výchozím nastavení: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span><span class="sxs-lookup"><span data-stu-id="495a2-129">Code samples are installed in the following location by default: `C:\Program Files\Microsoft SDKs\Windows\v7.0\Samples\sysmgmt\WindowsPowerShell\`.</span></span>

<span data-ttu-id="495a2-130">Následující části obsahují stručný popis toho, co dělá každý vzorek.</span><span class="sxs-lookup"><span data-stu-id="495a2-130">The following sections provide a brief description of what each sample does.</span></span>

## <a name="cmdlet-samples"></a><span data-ttu-id="495a2-131">Rutiny ukázky</span><span class="sxs-lookup"><span data-stu-id="495a2-131">Cmdlet samples</span></span>

### <a name="getprocesssample01"></a><span data-ttu-id="495a2-132">GetProcessSample01</span><span class="sxs-lookup"><span data-stu-id="495a2-132">GetProcessSample01</span></span>

<span data-ttu-id="495a2-133">Ukazuje, jak napsat jednoduchý rutinu, která získá všechny procesy na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="495a2-133">Shows how to write a simple cmdlet that gets all the processes on the local computer.</span></span>

### <a name="getprocesssample02"></a><span data-ttu-id="495a2-134">GetProcessSample02</span><span class="sxs-lookup"><span data-stu-id="495a2-134">GetProcessSample02</span></span>

<span data-ttu-id="495a2-135">Ukazuje, jak přidat parametry do rutiny.</span><span class="sxs-lookup"><span data-stu-id="495a2-135">Shows how to add parameters to the cmdlet.</span></span>
<span data-ttu-id="495a2-136">Rutina převezme jeden nebo více názvů proces a vrátí odpovídajících procesů.</span><span class="sxs-lookup"><span data-stu-id="495a2-136">The cmdlet takes one or more process names and returns the matching processes.</span></span>

### <a name="getprocesssample03"></a><span data-ttu-id="495a2-137">GetProcessSample03</span><span class="sxs-lookup"><span data-stu-id="495a2-137">GetProcessSample03</span></span>

<span data-ttu-id="495a2-138">Ukazuje, jak přidat parametry, které přijímají vstup z kanálu.</span><span class="sxs-lookup"><span data-stu-id="495a2-138">Shows how to add parameters that accept input from the pipeline.</span></span>

### <a name="getprocesssample04"></a><span data-ttu-id="495a2-139">GetProcessSample04</span><span class="sxs-lookup"><span data-stu-id="495a2-139">GetProcessSample04</span></span>

<span data-ttu-id="495a2-140">Ukazuje, jak zpracovávat neukončující chyby.</span><span class="sxs-lookup"><span data-stu-id="495a2-140">Shows how to handle nonterminating errors.</span></span>

### <a name="getprocesssample05"></a><span data-ttu-id="495a2-141">GetProcessSample05</span><span class="sxs-lookup"><span data-stu-id="495a2-141">GetProcessSample05</span></span>

<span data-ttu-id="495a2-142">Ukazuje, jak zobrazit seznam konkrétních procesů.</span><span class="sxs-lookup"><span data-stu-id="495a2-142">Shows how to display a list of specified processes.</span></span>

### <a name="selectobject"></a><span data-ttu-id="495a2-143">SelectObject –</span><span class="sxs-lookup"><span data-stu-id="495a2-143">SelectObject</span></span>

<span data-ttu-id="495a2-144">Ukazuje, jak napsat filtru vybrat pouze určité objekty.</span><span class="sxs-lookup"><span data-stu-id="495a2-144">Shows how to write a filter to select only certain objects.</span></span>

### <a name="selectstring"></a><span data-ttu-id="495a2-145">SelectString</span><span class="sxs-lookup"><span data-stu-id="495a2-145">SelectString</span></span>

<span data-ttu-id="495a2-146">Ukazuje, jak pro hledání souborů pro zadanou vzory.</span><span class="sxs-lookup"><span data-stu-id="495a2-146">Shows how to search files for specified patterns.</span></span>

### <a name="stopprocesssample01"></a><span data-ttu-id="495a2-147">StopProcessSample01</span><span class="sxs-lookup"><span data-stu-id="495a2-147">StopProcessSample01</span></span>

<span data-ttu-id="495a2-148">Ukazuje, jak implementovat *PassThru* parametr a jak si vyžádat zpětnou vazbu uživatelů pomocí volání [ShouldProcess](/dotnet/api/system.management.automation.cmdlet.shouldprocess) a [ShouldContinue](/dotnet/api/system.management.automation.cmdlet.shouldcontinue) metody.</span><span class="sxs-lookup"><span data-stu-id="495a2-148">Shows how to implement a *PassThru* parameter, and how to request user feedback by calls to the [ShouldProcess](/dotnet/api/system.management.automation.cmdlet.shouldprocess) and [ShouldContinue](/dotnet/api/system.management.automation.cmdlet.shouldcontinue) methods.</span></span>
<span data-ttu-id="495a2-149">Uživatelé *PassThru* parametr, když chtějí vynutit rutinu k vrácení objektu,</span><span class="sxs-lookup"><span data-stu-id="495a2-149">Users specify the *PassThru* parameter when they want to force the cmdlet to return an object,</span></span>

### <a name="stopprocesssample02"></a><span data-ttu-id="495a2-150">StopProcessSample02</span><span class="sxs-lookup"><span data-stu-id="495a2-150">StopProcessSample02</span></span>

<span data-ttu-id="495a2-151">Ukazuje, jak zastavit konkrétní proces.</span><span class="sxs-lookup"><span data-stu-id="495a2-151">Shows how to stop a specific process.</span></span>

### <a name="stopprocesssample03"></a><span data-ttu-id="495a2-152">StopProcessSample03</span><span class="sxs-lookup"><span data-stu-id="495a2-152">StopProcessSample03</span></span>

<span data-ttu-id="495a2-153">Ukazuje, jak deklarovat aliasy pro parametry a jak podporovat zástupné znaky.</span><span class="sxs-lookup"><span data-stu-id="495a2-153">Shows how to declare aliases for parameters and how to support wildcards.</span></span>

### <a name="stopprocesssample04"></a><span data-ttu-id="495a2-154">StopProcessSample04</span><span class="sxs-lookup"><span data-stu-id="495a2-154">StopProcessSample04</span></span>

<span data-ttu-id="495a2-155">Ukazuje, jak deklarovat sad parametrů, objekt, který rutina přijímá jako vstup a jak určit výchozí parametr nastaveno pro použití.</span><span class="sxs-lookup"><span data-stu-id="495a2-155">Shows how to declare parameter sets, the object that the cmdlet takes as input, and how to specify the default parameter set to use.</span></span>

## <a name="remoting-samples"></a><span data-ttu-id="495a2-156">Ukázky vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="495a2-156">Remoting samples</span></span>

### <a name="remoterunspace01"></a><span data-ttu-id="495a2-157">RemoteRunspace01</span><span class="sxs-lookup"><span data-stu-id="495a2-157">RemoteRunspace01</span></span>

<span data-ttu-id="495a2-158">Ukazuje, jak vytvořit vzdálené prostředí runspace, který se používá k navázání vzdáleného připojení.</span><span class="sxs-lookup"><span data-stu-id="495a2-158">Shows how to create a remote runspace that is used to establish a remote connection.</span></span>

### <a name="remoterunspacepool01"></a><span data-ttu-id="495a2-159">RemoteRunspacePool01</span><span class="sxs-lookup"><span data-stu-id="495a2-159">RemoteRunspacePool01</span></span>

<span data-ttu-id="495a2-160">Ukazuje, jak vytvořit fond vzdálené prostředí runspace a o tom, jak souběžně spustit více příkazů pomocí tohoto fondu.</span><span class="sxs-lookup"><span data-stu-id="495a2-160">Shows how to construct a remote runspace pool and how to run multiple commands concurrently by using this pool.</span></span>

### <a name="serialization01"></a><span data-ttu-id="495a2-161">Serialization01</span><span class="sxs-lookup"><span data-stu-id="495a2-161">Serialization01</span></span>

<span data-ttu-id="495a2-162">Ukazuje, jak podívejte se na existující třídy .NET a ujistěte se, že se uchovají informace z vybraných veřejných vlastností této třídy v serializaci nebo deserializaci.</span><span class="sxs-lookup"><span data-stu-id="495a2-162">Shows how to look at an existing .NET class and make sure that information from selected public properties of this class is preserved across serialization/deserialization.</span></span>

### <a name="serialization02"></a><span data-ttu-id="495a2-163">Serialization02</span><span class="sxs-lookup"><span data-stu-id="495a2-163">Serialization02</span></span>

<span data-ttu-id="495a2-164">Ukazuje, jak existující třídy .NET a ujistěte se, že se uchovají informace z instance této třídy v serializaci/deserializaci když informace nejsou k dispozici ve veřejné vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="495a2-164">Shows how to look at an existing .NET class and make sure that information from instance of this class is preserved across serialization/deserialization when the information is not available in public properties of the class.</span></span>

### <a name="serialization03"></a><span data-ttu-id="495a2-165">Serialization03</span><span class="sxs-lookup"><span data-stu-id="495a2-165">Serialization03</span></span>

<span data-ttu-id="495a2-166">Ukazuje, jak podívejte se na existující třídy .NET a ujistěte se, že jsou instance této třídy a odvozených tříd deserializovat (rehydrated) do živých objektů .NET.</span><span class="sxs-lookup"><span data-stu-id="495a2-166">Shows how to look at an existing .NET class and make sure that instances of this class and of derived classes are deserialized (rehydrated) into live .NET objects.</span></span>

## <a name="event-samples"></a><span data-ttu-id="495a2-167">Ukázky událostí</span><span class="sxs-lookup"><span data-stu-id="495a2-167">Event samples</span></span>

### <a name="event01"></a><span data-ttu-id="495a2-168">Event01</span><span class="sxs-lookup"><span data-stu-id="495a2-168">Event01</span></span>

<span data-ttu-id="495a2-169">Ukazuje, jak vytvořit odvozené z ObjectEventRegistrationBase rutinu pro registraci na událost.</span><span class="sxs-lookup"><span data-stu-id="495a2-169">Shows how to create a cmdlet for event registration by deriving from ObjectEventRegistrationBase.</span></span>

### <a name="event02"></a><span data-ttu-id="495a2-170">Event02</span><span class="sxs-lookup"><span data-stu-id="495a2-170">Event02</span></span>

<span data-ttu-id="495a2-171">Ukazuje, jak do ukazuje, jak k přijímání oznámení o události prostředí Windows PowerShell, které jsou generovány ve vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="495a2-171">Shows how to shows how to receive notifications of Windows PowerShell events that are generated on remote computers.</span></span>
<span data-ttu-id="495a2-172">Využívá událost PSEventReceived prostřednictvím [prostředí Runspace](/dotnet/api/system.management.automation.runspaces.runspace) třídy.</span><span class="sxs-lookup"><span data-stu-id="495a2-172">It uses the PSEventReceived event exposed through the [Runspace](/dotnet/api/system.management.automation.runspaces.runspace) class.</span></span>

## <a name="hosting-application-samples"></a><span data-ttu-id="495a2-173">Hostování aplikace ukázky</span><span class="sxs-lookup"><span data-stu-id="495a2-173">Hosting application samples</span></span>

### <a name="runspace01"></a><span data-ttu-id="495a2-174">Runspace01</span><span class="sxs-lookup"><span data-stu-id="495a2-174">Runspace01</span></span>

<span data-ttu-id="495a2-175">Ukazuje způsob použití [PowerShell](/dotnet/api/system.management.automation.powershell) má třída spustit [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutiny synchronně.</span><span class="sxs-lookup"><span data-stu-id="495a2-175">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet synchronously.</span></span>
<span data-ttu-id="495a2-176">[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutina vrací [procesu](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý proces běžící na místním počítači.</span><span class="sxs-lookup"><span data-stu-id="495a2-176">The [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer.</span></span>

### <a name="runspace02"></a><span data-ttu-id="495a2-177">Runspace02</span><span class="sxs-lookup"><span data-stu-id="495a2-177">Runspace02</span></span>

<span data-ttu-id="495a2-178">Ukazuje způsob použití [PowerShell](/dotnet/api/system.management.automation.powershell) má třída spustit [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) a [Sort-Object](/powershell/module/Microsoft.PowerShell.Utility/Sort-Object) rutiny synchronně.</span><span class="sxs-lookup"><span data-stu-id="495a2-178">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) and [Sort-Object](/powershell/module/Microsoft.PowerShell.Utility/Sort-Object) cmdlets synchronously.</span></span>
<span data-ttu-id="495a2-179">[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutina vrací [procesu](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objekty pro každý proces běžící na místním počítači a `Sort-Object` řadí objekty, na základě jejich [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) Vlastnost.</span><span class="sxs-lookup"><span data-stu-id="495a2-179">The [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet returns [Process](https://technet.microsoft.com/library/system.diagnostics.process.aspx) objects for each process running on the local computer, and the `Sort-Object` sorts the objects based on their [Id](https://technet.microsoft.com/library/system.diagnostics.process.id.aspx) property.</span></span>
<span data-ttu-id="495a2-180">Zobrazí se výsledky z těchto příkazů pomocí [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="495a2-180">The results of these commands is displayed by using a [DataGridView](https://technet.microsoft.com/library/system.windows.forms.datagridview.aspx) control.</span></span>

### <a name="runspace03"></a><span data-ttu-id="495a2-181">Runspace03</span><span class="sxs-lookup"><span data-stu-id="495a2-181">Runspace03</span></span>

<span data-ttu-id="495a2-182">Ukazuje způsob použití [Powershellu](/dotnet/api/system.management.automation.powershell) má třída spustit skript synchronně a jak zacházet s neukončujícími chybami.</span><span class="sxs-lookup"><span data-stu-id="495a2-182">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run a script synchronously, and how to handle non-terminating errors.</span></span>
<span data-ttu-id="495a2-183">Skript získá seznam názvů procesu a potom načte těchto procesů.</span><span class="sxs-lookup"><span data-stu-id="495a2-183">The script receives a list of process names and then retrieves those processes.</span></span>
<span data-ttu-id="495a2-184">Výsledky ze skriptu, včetně neukončující chyby, které byly generovány při spuštění skriptu, se zobrazí v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="495a2-184">The results of the script, including any non-terminating errors that were generated when running the script, are displayed in a console window.</span></span>

### <a name="runspace04"></a><span data-ttu-id="495a2-185">Runspace04</span><span class="sxs-lookup"><span data-stu-id="495a2-185">Runspace04</span></span>

<span data-ttu-id="495a2-186">Ukazuje způsob použití [Powershellu](/dotnet/api/system.management.automation.powershell) má třída spustit příkazy a jak catch ukončující chyby, které jsou vyvolány při spuštění příkazů.</span><span class="sxs-lookup"><span data-stu-id="495a2-186">Shows how to use the [PowerShell](/dotnet/api/system.management.automation.powershell) class to run commands, and how to catch terminating errors that are thrown when running the commands.</span></span>
<span data-ttu-id="495a2-187">Dva příkazy jsou spouštěny a poslední příkaz je předán jako parametr argument, který není platný.</span><span class="sxs-lookup"><span data-stu-id="495a2-187">Two commands are run, and the last command is passed a parameter argument that is not valid.</span></span>
<span data-ttu-id="495a2-188">V důsledku toho jsou vráceny žádné objekty a dojde k ukončující chybě je vyvolána výjimka.</span><span class="sxs-lookup"><span data-stu-id="495a2-188">As a result, no objects are returned and a terminating error is thrown.</span></span>

### <a name="runspace05"></a><span data-ttu-id="495a2-189">Runspace05</span><span class="sxs-lookup"><span data-stu-id="495a2-189">Runspace05</span></span>

<span data-ttu-id="495a2-190">Ukazuje, jak přidat modulu snap-in [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektu tak, aby rutiny modulu snap-in k dispozici při otevření prostředí runspace.</span><span class="sxs-lookup"><span data-stu-id="495a2-190">Shows how to add a snap-in to an [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) object so that the cmdlet of the snap-in is available when the runspace is opened.</span></span>
<span data-ttu-id="495a2-191">Modul snap-in poskytuje rutiny Get-Proc (určené [GetProcessSample01 ukázkové](https://technet.microsoft.com/library/ff602028.aspx)), který běží synchronně pomocí [Powershellu](/dotnet/api/system.management.automation.powershell) objektu.</span><span class="sxs-lookup"><span data-stu-id="495a2-191">The snap-in provides a Get-Proc cmdlet (defined by the [GetProcessSample01 Sample](https://technet.microsoft.com/library/ff602028.aspx)) that is run synchronously by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace06"></a><span data-ttu-id="495a2-192">Runspace06</span><span class="sxs-lookup"><span data-stu-id="495a2-192">Runspace06</span></span>

<span data-ttu-id="495a2-193">Ukazuje, jak přidat modul do [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektu tak, aby modul je načten při otevření prostředí runspace.</span><span class="sxs-lookup"><span data-stu-id="495a2-193">Shows how to add a module to an [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) object so that the module is loaded when the runspace is opened.</span></span>
<span data-ttu-id="495a2-194">Tento modul obsahuje rutiny Get-Proc (určené [GetProcessSample02 ukázkové](https://technet.microsoft.com/library/ff602027.aspx)), který běží synchronně pomocí [prostředí PowerShell](/dotnet/api/system.management.automation.powershell) objektu.</span><span class="sxs-lookup"><span data-stu-id="495a2-194">The module provides a Get-Proc cmdlet (defined by the [GetProcessSample02 Sample](https://technet.microsoft.com/library/ff602027.aspx)) that is run synchronously by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace07"></a><span data-ttu-id="495a2-195">Runspace07</span><span class="sxs-lookup"><span data-stu-id="495a2-195">Runspace07</span></span>

<span data-ttu-id="495a2-196">Ukazuje, jak vytvořit prostředí runspace a pak pomocí tohoto prostředí runspace spustíte dvě rutiny synchronně s použitím [Powershellu](/dotnet/api/system.management.automation.powershell) objektu.</span><span class="sxs-lookup"><span data-stu-id="495a2-196">Shows how to create a runspace, and then use that runspace to run two cmdlets synchronously by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace08"></a><span data-ttu-id="495a2-197">Runspace08</span><span class="sxs-lookup"><span data-stu-id="495a2-197">Runspace08</span></span>

<span data-ttu-id="495a2-198">Ukazuje, jak přidat do kanálu z příkazů a argumentů [Powershellu](/dotnet/api/system.management.automation.powershell) objekt a jak spouštět příkazy synchronně.</span><span class="sxs-lookup"><span data-stu-id="495a2-198">Shows how to add commands and arguments to the pipeline of a [PowerShell](/dotnet/api/system.management.automation.powershell) object and how to run the commands synchronously.</span></span>

### <a name="runspace09"></a><span data-ttu-id="495a2-199">Runspace09</span><span class="sxs-lookup"><span data-stu-id="495a2-199">Runspace09</span></span>

<span data-ttu-id="495a2-200">Ukazuje, jak přidat skript do kanálu nástroje [Powershellu](/dotnet/api/system.management.automation.powershell) objekt a jak spustit skript asynchronně.</span><span class="sxs-lookup"><span data-stu-id="495a2-200">Shows how to add a script to the pipeline of a [PowerShell](/dotnet/api/system.management.automation.powershell) object and how to run the script asynchronously.</span></span>
<span data-ttu-id="495a2-201">Události se používají ke zpracování výstup skriptu.</span><span class="sxs-lookup"><span data-stu-id="495a2-201">Events are used to handle the output of the script.</span></span>

### <a name="runspace10"></a><span data-ttu-id="495a2-202">Runspace10</span><span class="sxs-lookup"><span data-stu-id="495a2-202">Runspace10</span></span>

<span data-ttu-id="495a2-203">Ukazuje, jak vytvořit počáteční relace do výchozího stavu přidání rutiny [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate), jak vytvořit prostředí runspace, který používá stav relace počáteční a jak spustit pomocí příkazu [Powershellu](/dotnet/api/system.management.automation.powershell)objektu.</span><span class="sxs-lookup"><span data-stu-id="495a2-203">Shows how to create a default initial session state, how to add a cmdlet to the [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate), how to create a runspace that uses the initial session state, and how to run the command by using a [PowerShell](/dotnet/api/system.management.automation.powershell) object.</span></span>

### <a name="runspace11"></a><span data-ttu-id="495a2-204">Runspace11</span><span class="sxs-lookup"><span data-stu-id="495a2-204">Runspace11</span></span>

<span data-ttu-id="495a2-205">Ukazuje způsob použití [ProxyCommand](/dotnet/api/system.management.automation.proxycommand) třídy za účelem vytvoření příkaz proxy server, který volá existující rutiny, ale omezuje sadu parametrů k dispozici.</span><span class="sxs-lookup"><span data-stu-id="495a2-205">Shows how to use the [ProxyCommand](/dotnet/api/system.management.automation.proxycommand) class to create a proxy command that calls an existing cmdlet, but restricts the set of available parameters.</span></span>
<span data-ttu-id="495a2-206">Příkaz proxy se pak přidá do stavu počáteční relace, který se používá k vytvoření omezené prostředí runspace.</span><span class="sxs-lookup"><span data-stu-id="495a2-206">The proxy command is then added to an initial session state that is used to create a constrained runspace.</span></span>
<span data-ttu-id="495a2-207">To znamená, že má uživatel přístup funkci rutiny pouze prostřednictvím příkazu proxy serveru.</span><span class="sxs-lookup"><span data-stu-id="495a2-207">This means that the user can access the functionality of the cmdlet only through the proxy command.</span></span>

### <a name="powershell01"></a><span data-ttu-id="495a2-208">PowerShell01</span><span class="sxs-lookup"><span data-stu-id="495a2-208">PowerShell01</span></span>

<span data-ttu-id="495a2-209">Ukazuje, jak vytvořit prostředí runspace omezené použití [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) objektu.</span><span class="sxs-lookup"><span data-stu-id="495a2-209">Shows how to create a constrained runspace using an [InitialSessionState](/dotnet/api/system.management.automation.runspaces.initialsessionstate) object.</span></span>

### <a name="powershell02"></a><span data-ttu-id="495a2-210">PowerShell02</span><span class="sxs-lookup"><span data-stu-id="495a2-210">PowerShell02</span></span>

<span data-ttu-id="495a2-211">Ukazuje, jak používat prostředí runspace fond jak souběžně spustit více příkazů.</span><span class="sxs-lookup"><span data-stu-id="495a2-211">Shows how to use a runspace pool to run multiple commands concurrently.</span></span>

## <a name="host-samples"></a><span data-ttu-id="495a2-212">Ukázky hostitele</span><span class="sxs-lookup"><span data-stu-id="495a2-212">Host samples</span></span>

### <a name="host01"></a><span data-ttu-id="495a2-213">Host01</span><span class="sxs-lookup"><span data-stu-id="495a2-213">Host01</span></span>

<span data-ttu-id="495a2-214">Ukazuje, jak implementovat hostitelskou aplikaci, která používá vlastního hostitele.</span><span class="sxs-lookup"><span data-stu-id="495a2-214">Shows how to implement a host application that uses a custom host.</span></span>
<span data-ttu-id="495a2-215">V této ukázce se vytvoří prostředí runspace, který používá vlastního hostitele a pak [Powershellu](/dotnet/api/system.management.automation.powershell) rozhraní API se používá ke spuštění skriptu, který volá "ukončit".</span><span class="sxs-lookup"><span data-stu-id="495a2-215">In this sample a runspace is created that uses the custom host, and then the [PowerShell](/dotnet/api/system.management.automation.powershell) API is used to run a script that calls "exit".</span></span>
<span data-ttu-id="495a2-216">Hostitelská aplikace potom vypadá výstup skriptu a vypíše výsledky.</span><span class="sxs-lookup"><span data-stu-id="495a2-216">The host application then looks at the output of the script and prints out the results.</span></span>

### <a name="host02"></a><span data-ttu-id="495a2-217">Host02</span><span class="sxs-lookup"><span data-stu-id="495a2-217">Host02</span></span>

<span data-ttu-id="495a2-218">Ukazuje, jak psát aplikace hostitele, který používá modul runtime Windows PowerShell společně s implementace vlastního hostitele.</span><span class="sxs-lookup"><span data-stu-id="495a2-218">Shows how to write a host application that uses the Windows PowerShell runtime along with a custom host implementation.</span></span>
<span data-ttu-id="495a2-219">Hostitelská aplikace nastaví jazykovou verzi hostitele na němčinu, spustí [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) rutiny a zobrazí výsledky jako zobrazoval se vám je pomocí pwrsh.exe a pak vytiskne aktuální datum a čas v němčině.</span><span class="sxs-lookup"><span data-stu-id="495a2-219">The host application sets the host culture to German, runs the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet and displays the results as you would see them by using pwrsh.exe, and then prints out the current data and time in German.</span></span>

### <a name="host03"></a><span data-ttu-id="495a2-220">Host03</span><span class="sxs-lookup"><span data-stu-id="495a2-220">Host03</span></span>

<span data-ttu-id="495a2-221">Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="495a2-221">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>

### <a name="host04"></a><span data-ttu-id="495a2-222">Host04</span><span class="sxs-lookup"><span data-stu-id="495a2-222">Host04</span></span>

<span data-ttu-id="495a2-223">Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="495a2-223">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="495a2-224">Tato hostitelská aplikace podporuje také zobrazování výzev, které umožňují uživateli zadat více možností.</span><span class="sxs-lookup"><span data-stu-id="495a2-224">This host application also supports displaying prompts that allow the user to specify multiple choices.</span></span>

### <a name="host05"></a><span data-ttu-id="495a2-225">Hostitel05</span><span class="sxs-lookup"><span data-stu-id="495a2-225">Host05</span></span>

<span data-ttu-id="495a2-226">Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="495a2-226">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="495a2-227">Tato hostitelská aplikace podporuje také volání vzdálených počítačích pomocí [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) a [ukončení relace PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) rutiny.</span><span class="sxs-lookup"><span data-stu-id="495a2-227">This host application also supports calls to remote computers by using the [Enter-PsSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) and [Exit-PsSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) cmdlets.</span></span>

### <a name="host06"></a><span data-ttu-id="495a2-228">Host06</span><span class="sxs-lookup"><span data-stu-id="495a2-228">Host06</span></span>

<span data-ttu-id="495a2-229">Ukazuje, jak sestavit interaktivní hostitel konzolové aplikace, která načítá příkazy z příkazového řádku, provede příkazy a poté zobrazí výsledky do konzoly.</span><span class="sxs-lookup"><span data-stu-id="495a2-229">Shows how to build an interactive console-based host application that reads commands from the command line, executes the commands, and then displays the results to the console.</span></span>
<span data-ttu-id="495a2-230">Kromě toho tato ukázka používá rozhraní API pro Tokenizátor pro určení barvy textu, který je zadané uživatelem.</span><span class="sxs-lookup"><span data-stu-id="495a2-230">In addition, this sample uses the Tokenizer APIs to specify the color of the text that is entered by the user.</span></span>

## <a name="provider-samples"></a><span data-ttu-id="495a2-231">Ukázky poskytovatele</span><span class="sxs-lookup"><span data-stu-id="495a2-231">Provider samples</span></span>

### <a name="accessdbprovidersample01"></a><span data-ttu-id="495a2-232">AccessDBProviderSample01</span><span class="sxs-lookup"><span data-stu-id="495a2-232">AccessDBProviderSample01</span></span>

<span data-ttu-id="495a2-233">Ukazuje, jak deklarovat třídu poskytovatele, který je odvozen přímo z [CmdletProvider](/dotnet/api/system.management.automation.provider.cmdletprovider) třídy.</span><span class="sxs-lookup"><span data-stu-id="495a2-233">Shows how to declare a provider class that derives directly from the [CmdletProvider](/dotnet/api/system.management.automation.provider.cmdletprovider) class.</span></span>
<span data-ttu-id="495a2-234">Je zde zahrnuta pouze pro úplnost.</span><span class="sxs-lookup"><span data-stu-id="495a2-234">It is included here only for completeness.</span></span>

### <a name="accessdbprovidersample02"></a><span data-ttu-id="495a2-235">AccessDBProviderSample02</span><span class="sxs-lookup"><span data-stu-id="495a2-235">AccessDBProviderSample02</span></span>

<span data-ttu-id="495a2-236">Ukazuje, jak přepsat [NewDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.newdrive) a [RemoveDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.removedrive) metody pro podporu volání `New-PSDrive` a `Remove-PSDrive` rutiny.</span><span class="sxs-lookup"><span data-stu-id="495a2-236">Shows how to overwrite the [NewDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.newdrive) and [RemoveDrive](/dotnet/api/system.management.automation.provider.drivecmdletprovider.removedrive) methods to support calls to the `New-PSDrive` and `Remove-PSDrive` cmdlets.</span></span>
<span data-ttu-id="495a2-237">Třída zprostředkovatele v této ukázce je odvozena z [DriveCmdletProvider](/dotnet/api/system.management.automation.provider.drivecmdletprovider) třídy.</span><span class="sxs-lookup"><span data-stu-id="495a2-237">The provider class in this sample derives from the [DriveCmdletProvider](/dotnet/api/system.management.automation.provider.drivecmdletprovider) class.</span></span>

### <a name="accessdbprovidersample03"></a><span data-ttu-id="495a2-238">AccessDBProviderSample03</span><span class="sxs-lookup"><span data-stu-id="495a2-238">AccessDBProviderSample03</span></span>

<span data-ttu-id="495a2-239">Ukazuje, jak přepsat [GetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.getitem) a [SetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.setitem) metody pro podporu volání `Get-Item` a `Set-Item` rutiny.</span><span class="sxs-lookup"><span data-stu-id="495a2-239">Shows how to overwrite the [GetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.getitem) and [SetItem](/dotnet/api/system.management.automation.provider.itemcmdletprovider.setitem) methods to support calls to the `Get-Item` and `Set-Item` cmdlets.</span></span>
<span data-ttu-id="495a2-240">Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) třídy.</span><span class="sxs-lookup"><span data-stu-id="495a2-240">The provider class in this sample derives from the [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) class.</span></span>

### <a name="accessdbprovidersample04"></a><span data-ttu-id="495a2-241">AccessDBProviderSample04</span><span class="sxs-lookup"><span data-stu-id="495a2-241">AccessDBProviderSample04</span></span>

<span data-ttu-id="495a2-242">Ukazuje, jak přepsat metody kontejneru pro podporu volání `Copy-Item`, `Get-ChildItem`, `New-Item`, a `Remove-Item` rutiny.</span><span class="sxs-lookup"><span data-stu-id="495a2-242">Shows how to overwrite container methods to support calls to the `Copy-Item`, `Get-ChildItem`, `New-Item`, and `Remove-Item` cmdlets.</span></span>
<span data-ttu-id="495a2-243">Tyto metody by měla být implementována, pokud úložiště dat obsahuje položky, které jsou kontejnery.</span><span class="sxs-lookup"><span data-stu-id="495a2-243">These methods should be implemented when the data store contains items that are containers.</span></span>
<span data-ttu-id="495a2-244">Kontejner je skupina podřízených položek v části společné nadřazené položky.</span><span class="sxs-lookup"><span data-stu-id="495a2-244">A container is a group of child items under a common parent item.</span></span>
<span data-ttu-id="495a2-245">Třída zprostředkovatele v této ukázce je odvozena z [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) třídy.</span><span class="sxs-lookup"><span data-stu-id="495a2-245">The provider class in this sample derives from the [ItemCmdletProvider](/dotnet/api/system.management.automation.provider.itemcmdletprovider) class.</span></span>

### <a name="accessdbprovidersample05"></a><span data-ttu-id="495a2-246">AccessDBProviderSample05</span><span class="sxs-lookup"><span data-stu-id="495a2-246">AccessDBProviderSample05</span></span>

<span data-ttu-id="495a2-247">Ukazuje, jak přepsat metody kontejneru pro podporu volání `Move-Item` a `Join-Path` rutiny.</span><span class="sxs-lookup"><span data-stu-id="495a2-247">Shows how to overwrite container methods to support calls to the `Move-Item` and `Join-Path` cmdlets.</span></span>
<span data-ttu-id="495a2-248">Tyto metody by měla být implementována, když uživatel potřebuje pro přesun položek v rámci kontejneru, a pokud úložiště dat obsahuje vnořené kontejnery.</span><span class="sxs-lookup"><span data-stu-id="495a2-248">These methods should be implemented when the user needs to move items within a container and if the data store contains nested containers.</span></span>
<span data-ttu-id="495a2-249">Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) třídy.</span><span class="sxs-lookup"><span data-stu-id="495a2-249">The provider class in this sample derives from the [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) class.</span></span>

### <a name="accessdbprovidersample06"></a><span data-ttu-id="495a2-250">AccessDBProviderSample06</span><span class="sxs-lookup"><span data-stu-id="495a2-250">AccessDBProviderSample06</span></span>

<span data-ttu-id="495a2-251">Ukazuje, jak přepsat obsah metody pro podporu volání `Clear-Content`, `Get-Content`, a `Set-Content` rutiny.</span><span class="sxs-lookup"><span data-stu-id="495a2-251">Shows how to overwrite content methods to support calls to the `Clear-Content`, `Get-Content`, and `Set-Content` cmdlets.</span></span>
<span data-ttu-id="495a2-252">Tyto metody by měla být implementována, když uživatel potřebuje pro správu obsahu položky dat v úložišti.</span><span class="sxs-lookup"><span data-stu-id="495a2-252">These methods should be implemented when the user needs to manage the content of the items in the data store.</span></span>
<span data-ttu-id="495a2-253">Třída zprostředkovatele v této ukázce je odvozena z [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) a implementuje [IContentCmdletProvider](/dotnet/api/system.management.automation.provider.icontentcmdletprovider) rozhraní.</span><span class="sxs-lookup"><span data-stu-id="495a2-253">The provider class in this sample derives from the [NavigationCmdletProvider](/dotnet/api/system.management.automation.provider.navigationcmdletprovider) class, and it implements the [IContentCmdletProvider](/dotnet/api/system.management.automation.provider.icontentcmdletprovider) interface.</span></span>
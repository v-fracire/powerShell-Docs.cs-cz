---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa služeb
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: f3231d1922568e552534f3d3face3864d1610d65
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30951194"
---
# <a name="managing-services"></a><span data-ttu-id="eb697-103">Správa služeb</span><span class="sxs-lookup"><span data-stu-id="eb697-103">Managing Services</span></span>

<span data-ttu-id="eb697-104">Existují osm rutin služby základní určených pro širokou škálu úloh služby.</span><span class="sxs-lookup"><span data-stu-id="eb697-104">There are eight core Service cmdlets, designed for a wide range of service tasks .</span></span> <span data-ttu-id="eb697-105">Podíváme se pouze na zobrazení a změna stavu spuštění pro služby, ale seznam rutin služby můžete získat pomocí **Get-Help \&#42;-Service**, a může najít informace o všech rutin služby pomocí **Get-Help < název rutiny >**, jako například **Get-Help novou službu**.</span><span class="sxs-lookup"><span data-stu-id="eb697-105">We will look only at listing and changing running state for services, but you can get a list Service cmdlets by using **Get-Help \&#42;-Service**, and you can find information about each Service cmdlet by using **Get-Help<Cmdlet-Name>**, such as **Get-Help New-Service**.</span></span>

## <a name="getting-services"></a><span data-ttu-id="eb697-106">Než služeb</span><span class="sxs-lookup"><span data-stu-id="eb697-106">Getting Services</span></span>

<span data-ttu-id="eb697-107">Služby v místním nebo vzdáleném počítači můžete získat pomocí **Get-Service** rutiny.</span><span class="sxs-lookup"><span data-stu-id="eb697-107">You can get the services on a local or remote computer by using the **Get-Service** cmdlet.</span></span> <span data-ttu-id="eb697-108">Stejně jako u **Get-Process**pomocí **Get-Service** příkaz bez parametrů vrátí všechny služby.</span><span class="sxs-lookup"><span data-stu-id="eb697-108">As with **Get-Process**, using the **Get-Service** command without parameters returns all services.</span></span> <span data-ttu-id="eb697-109">Můžete filtrovat podle názvu, i pomocí hvězdičky jako zástupný znak:</span><span class="sxs-lookup"><span data-stu-id="eb697-109">You can filter by name, even using an asterisk as a wildcard:</span></span>

```
PS> Get-Service -Name se*

Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="eb697-110">Protože to není vždy zřejmé novinky skutečné název pro službu, můžete zjistit, že budete muset najít služby podle zobrazovaného názvu.</span><span class="sxs-lookup"><span data-stu-id="eb697-110">Because it is not always obvious what the real name for the service is, you may find you need to find services by display name.</span></span> <span data-ttu-id="eb697-111">To provedete pomocí konkrétní název, pomocí zástupných znaků nebo pomocí seznamu názvů zobrazení:</span><span class="sxs-lookup"><span data-stu-id="eb697-111">You can do this by specific name, using wildcards, or using a list of display names:</span></span>

```
PS> Get-Service -DisplayName se*

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center

PS> Get-Service -DisplayName ServiceLayer,Server

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="eb697-112">Parametr ComputerName rutiny Get-Service můžete získat službu na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="eb697-112">You can use the ComputerName parameter of the Get-Service cmdlet to get the services on remote computers.</span></span> <span data-ttu-id="eb697-113">Parametr ComputerName přijme více hodnot a zástupné znaky, abyste získali služeb ve více počítačích jedním příkazem.</span><span class="sxs-lookup"><span data-stu-id="eb697-113">The ComputerName parameter accepts multiple values and wildcard characters, so you can get the services on multiple computers with a single command.</span></span> <span data-ttu-id="eb697-114">Například následující příkaz získá služby ve vzdáleném počítači Server01.</span><span class="sxs-lookup"><span data-stu-id="eb697-114">For example, the following command gets the services on the Server01 remote computer.</span></span>

```powershell
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a><span data-ttu-id="eb697-115">Získávání vyžaduje a závislých služeb</span><span class="sxs-lookup"><span data-stu-id="eb697-115">Getting Required and Dependent Services</span></span>

<span data-ttu-id="eb697-116">Rutina Get-Service má dva parametry, které jsou velmi užitečné v součásti pro správu služby.</span><span class="sxs-lookup"><span data-stu-id="eb697-116">The Get-Service cmdlet has two parameters that are very useful in service administration.</span></span> <span data-ttu-id="eb697-117">Parametr DependentServices získá služby, které závisejí na službě.</span><span class="sxs-lookup"><span data-stu-id="eb697-117">The DependentServices parameter gets services that depend on the service.</span></span> <span data-ttu-id="eb697-118">Parametr RequiredServices získá služby, na kterých závisí tato služba.</span><span class="sxs-lookup"><span data-stu-id="eb697-118">The RequiredServices parameter gets services upon which this service depends.</span></span>

<span data-ttu-id="eb697-119">Tyto parametry se zobrazí pouze hodnoty DependentServices a ServicesDependedOn (alias = RequiredServices) vlastnosti System.ServiceProcess.ServiceController objektu, který vrátí Get-Service, ale zjednodušit příkazy a ujistěte se, získávání Tyto informace mnohem jednodušší.</span><span class="sxs-lookup"><span data-stu-id="eb697-119">These parameters just display the values of the DependentServices and ServicesDependedOn (alias=RequiredServices) properties of the System.ServiceProcess.ServiceController object that Get-Service returns, but they simplify commands and make getting this information much simpler.</span></span>

<span data-ttu-id="eb697-120">Následující příkaz získá služby, které LanmanWorkstation služba vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="eb697-120">The following command gets the services that the LanmanWorkstation service requires.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices

Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

<span data-ttu-id="eb697-121">Následující příkaz získá služby, které vyžadují službu LanmanWorkstation.</span><span class="sxs-lookup"><span data-stu-id="eb697-121">The following command gets the services that require the LanmanWorkstation service.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -DependentServices

Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

<span data-ttu-id="eb697-122">Můžete získat i všechny služby, které mají závislosti.</span><span class="sxs-lookup"><span data-stu-id="eb697-122">You can even get all services that have dependencies.</span></span> <span data-ttu-id="eb697-123">Tento příkaz nepodporuje právě, a pak používá rutinu Format-Table pro zobrazení stavu, název, RequiredServices a DependentServices vlastnosti služeb v počítači.</span><span class="sxs-lookup"><span data-stu-id="eb697-123">The following command does just that, and then it uses the Format-Table cmdlet to display the Status, Name, RequiredServices and DependentServices properties of the services on the computer.</span></span>

```powershell
Get-Service -Name * | Where-Object {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a><span data-ttu-id="eb697-124">Zastavení, spuštění, pozastavení a restartování služby</span><span class="sxs-lookup"><span data-stu-id="eb697-124">Stopping, Starting, Suspending, and Restarting Services</span></span>
<span data-ttu-id="eb697-125">Všechny rutiny služby mají stejné obecné formuláře.</span><span class="sxs-lookup"><span data-stu-id="eb697-125">The Service cmdlets all have the same general form.</span></span> <span data-ttu-id="eb697-126">Služby lze zadat běžný název nebo zobrazovaný název a proveďte seznamy a zástupné znaky jako hodnoty.</span><span class="sxs-lookup"><span data-stu-id="eb697-126">Services can be specified by common name or display name, and take lists and wildcards as values.</span></span> <span data-ttu-id="eb697-127">Chcete-li zastavit služby zařazování tisku, použijte:</span><span class="sxs-lookup"><span data-stu-id="eb697-127">To stop the print spooler, use:</span></span>

```powershell
Stop-Service -Name spooler
```

<span data-ttu-id="eb697-128">Služba zařazování tisku spustit po je zastaven, použijte:</span><span class="sxs-lookup"><span data-stu-id="eb697-128">To start the print spooler after it is stopped, use:</span></span>

```powershell
Start-Service -Name spooler
```

<span data-ttu-id="eb697-129">Pozastavení služby zařazování tisku, použijte:</span><span class="sxs-lookup"><span data-stu-id="eb697-129">To suspend the print spooler, use:</span></span>

```powershell
Suspend-Service -Name spooler
```

<span data-ttu-id="eb697-130">**Restart-Service** rutiny funguje stejným způsobem jako u ostatních rutin služby, ale ukážeme některé příklady složitější pro ni.</span><span class="sxs-lookup"><span data-stu-id="eb697-130">The **Restart-Service** cmdlet works in the same manner as the other Service cmdlets, but we will show some more complex examples for it.</span></span> <span data-ttu-id="eb697-131">V nejjednodušší použití zadejte název služby:</span><span class="sxs-lookup"><span data-stu-id="eb697-131">In the simplest use, you specify the name of the service:</span></span>

```
PS> Restart-Service -Name spooler

WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

<span data-ttu-id="eb697-132">Si všimnete, získat opakovaných upozornění o zařazování tisku spuštění.</span><span class="sxs-lookup"><span data-stu-id="eb697-132">You will notice that you get a repeated warning message about the Print Spooler starting up.</span></span> <span data-ttu-id="eb697-133">Při provádění operace služby, který nějakou dobu trvá, prostředí Windows PowerShell vás upozorní, že se stále pokouší o provedení úlohy.</span><span class="sxs-lookup"><span data-stu-id="eb697-133">When you perform a service operation that takes some time, Windows PowerShell will notify you that it is still attempting to perform the task.</span></span>

<span data-ttu-id="eb697-134">Pokud chcete restartovat víc služeb, můžete získat seznam služeb, filtrovat je a pak proveďte restartování:</span><span class="sxs-lookup"><span data-stu-id="eb697-134">If you want to restart multiple services, you can get a list of services, filter them, and then perform the restart:</span></span>

```
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service

WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

<span data-ttu-id="eb697-135">Tyto rutiny služby není parametr ComputerName, ale je bylo možné spouštět ve vzdáleném počítači pomocí rutiny Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="eb697-135">These Service cmdlets do not have a ComputerName parameter, but you can run them on a remote computer by using the Invoke-Command cmdlet.</span></span> <span data-ttu-id="eb697-136">Například následující příkaz restartuje službu zařazování tisku ve vzdáleném počítači Server01.</span><span class="sxs-lookup"><span data-stu-id="eb697-136">For example, the following command restarts the Spooler service on the Server01 remote computer.</span></span>

```powershell
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a><span data-ttu-id="eb697-137">Vlastnosti nastavení služby</span><span class="sxs-lookup"><span data-stu-id="eb697-137">Setting Service Properties</span></span>

<span data-ttu-id="eb697-138">Rutina Set-Service změní vlastnosti služby v místním nebo vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="eb697-138">The Set-Service cmdlet changes the properties of a service on a local or remote computer.</span></span> <span data-ttu-id="eb697-139">Vzhledem k tomu, že stav služby je vlastnost, můžete tuto rutinu spuštění, zastavení a pozastavení služby.</span><span class="sxs-lookup"><span data-stu-id="eb697-139">Because the service status is a property, you can use this cmdlet to start, stop, and suspend a service.</span></span> <span data-ttu-id="eb697-140">Rutina Set-Service má také StartupType parametr, který vám umožní změnit typ spuštění služby.</span><span class="sxs-lookup"><span data-stu-id="eb697-140">The Set-Service cmdlet also has a StartupType parameter that lets you change the service startup type.</span></span>

<span data-ttu-id="eb697-141">Chcete-li používat nastavení služby ve Windows Vista a novějších verzích systému Windows, otevřete prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".</span><span class="sxs-lookup"><span data-stu-id="eb697-141">To use Set-Service on Windows Vista and later versions of Windows, open Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="eb697-142">Další informace najdete v tématu [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="eb697-142">For more information, see [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>

## <a name="see-also"></a><span data-ttu-id="eb697-143">Viz také</span><span class="sxs-lookup"><span data-stu-id="eb697-143">See Also</span></span>

- <span data-ttu-id="eb697-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span><span class="sxs-lookup"><span data-stu-id="eb697-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span></span>
- <span data-ttu-id="eb697-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="eb697-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>
- <span data-ttu-id="eb697-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span><span class="sxs-lookup"><span data-stu-id="eb697-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span></span>
- <span data-ttu-id="eb697-147">[Pozastavení služby [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span><span class="sxs-lookup"><span data-stu-id="eb697-147">[Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span></span>
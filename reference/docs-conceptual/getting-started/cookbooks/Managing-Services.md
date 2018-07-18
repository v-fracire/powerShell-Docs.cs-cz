---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa služeb
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: e2388f5d73a320a69faae0772c8403a7d77f8b52
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094166"
---
# <a name="managing-services"></a><span data-ttu-id="c77aa-103">Správa služeb</span><span class="sxs-lookup"><span data-stu-id="c77aa-103">Managing Services</span></span>

<span data-ttu-id="c77aa-104">Nejsou k dispozici osm jader rutiny, navržená pro širokou škálu úloh služby.</span><span class="sxs-lookup"><span data-stu-id="c77aa-104">There are eight core Service cmdlets, designed for a wide range of service tasks .</span></span> <span data-ttu-id="c77aa-105">Se podíváme jenom na zobrazení a změna stavu spuštění pro služby, ale můžete získat seznam rutin služby pomocí **Get-Help \*– služba**, a informace o všech rutin služby můžete najít pomocí  **Get-Help \<název rutiny\>**, jako například **Get-Help novou službu**.</span><span class="sxs-lookup"><span data-stu-id="c77aa-105">We will look only at listing and changing running state for services, but you can get a list of Service cmdlets by using **Get-Help \*-Service**, and you can find information about each Service cmdlet by using **Get-Help \<Cmdlet-Name\>**, such as **Get-Help New-Service**.</span></span>

## <a name="getting-services"></a><span data-ttu-id="c77aa-106">Získání služby</span><span class="sxs-lookup"><span data-stu-id="c77aa-106">Getting Services</span></span>

<span data-ttu-id="c77aa-107">Služby na místním nebo vzdáleném počítači můžete získat pomocí **Get-Service** rutiny.</span><span class="sxs-lookup"><span data-stu-id="c77aa-107">You can get the services on a local or remote computer by using the **Get-Service** cmdlet.</span></span> <span data-ttu-id="c77aa-108">Stejně jako u **Get-Process**, použije **Get-Service** příkaz bez parametrů vrátí všechny služby.</span><span class="sxs-lookup"><span data-stu-id="c77aa-108">As with **Get-Process**, using the **Get-Service** command without parameters returns all services.</span></span> <span data-ttu-id="c77aa-109">Můžete filtrovat podle názvu, dokonce i pomocí hvězdičky jako zástupný znak:</span><span class="sxs-lookup"><span data-stu-id="c77aa-109">You can filter by name, even using an asterisk as a wildcard:</span></span>

```
PS> Get-Service -Name se*

Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

<span data-ttu-id="c77aa-110">Protože není vždy zřejmé novinky o reálný název služby, může se stát, že je nutné vyhledat podle zobrazovaného názvu služby.</span><span class="sxs-lookup"><span data-stu-id="c77aa-110">Because it is not always obvious what the real name for the service is, you may find you need to find services by display name.</span></span> <span data-ttu-id="c77aa-111">Máte to podle konkrétního názvu pomocí zástupných znaků, nebo pomocí seznamu zobrazované názvy:</span><span class="sxs-lookup"><span data-stu-id="c77aa-111">You can do this by specific name, using wildcards, or using a list of display names:</span></span>

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

<span data-ttu-id="c77aa-112">Parametru ComputerName rutiny Get-Service můžete použít k získání služby na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="c77aa-112">You can use the ComputerName parameter of the Get-Service cmdlet to get the services on remote computers.</span></span> <span data-ttu-id="c77aa-113">Parametr ComputerName přijímá více hodnot a zástupné znaky, abyste se mohli služeb ve více počítačích pomocí jediného příkazu.</span><span class="sxs-lookup"><span data-stu-id="c77aa-113">The ComputerName parameter accepts multiple values and wildcard characters, so you can get the services on multiple computers with a single command.</span></span> <span data-ttu-id="c77aa-114">Například v následujícím příkazu je získán služby na vzdáleném počítači Server01.</span><span class="sxs-lookup"><span data-stu-id="c77aa-114">For example, the following command gets the services on the Server01 remote computer.</span></span>

```powershell
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a><span data-ttu-id="c77aa-115">Získání požadovaných a závislé služby</span><span class="sxs-lookup"><span data-stu-id="c77aa-115">Getting Required and Dependent Services</span></span>

<span data-ttu-id="c77aa-116">Rutina Get-Service má dva parametry, které jsou velmi užitečné při správy služeb.</span><span class="sxs-lookup"><span data-stu-id="c77aa-116">The Get-Service cmdlet has two parameters that are very useful in service administration.</span></span> <span data-ttu-id="c77aa-117">Parametr DependentServices získá služeb, které závisí na službě.</span><span class="sxs-lookup"><span data-stu-id="c77aa-117">The DependentServices parameter gets services that depend on the service.</span></span> <span data-ttu-id="c77aa-118">Parametr RequiredServices získá služeb, na které závisí tato služba.</span><span class="sxs-lookup"><span data-stu-id="c77aa-118">The RequiredServices parameter gets services upon which this service depends.</span></span>

<span data-ttu-id="c77aa-119">Tyto parametry se zobrazí pouze hodnoty DependentServices a ServicesDependedOn (alias = RequiredServices) vlastnosti objektu System.ServiceProcess.ServiceController zjednodušující Get-služba vrátí hodnotu, ale příkazy a ujistěte se, získání Tyto informace mnohem jednodušší.</span><span class="sxs-lookup"><span data-stu-id="c77aa-119">These parameters just display the values of the DependentServices and ServicesDependedOn (alias=RequiredServices) properties of the System.ServiceProcess.ServiceController object that Get-Service returns, but they simplify commands and make getting this information much simpler.</span></span>

<span data-ttu-id="c77aa-120">V následujícím příkazu je získán služby, které vyžaduje služba LanmanWorkstation.</span><span class="sxs-lookup"><span data-stu-id="c77aa-120">The following command gets the services that the LanmanWorkstation service requires.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices

Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

<span data-ttu-id="c77aa-121">V následujícím příkazu je získán služby, které vyžaduje služba LanmanWorkstation.</span><span class="sxs-lookup"><span data-stu-id="c77aa-121">The following command gets the services that require the LanmanWorkstation service.</span></span>

```
PS> Get-Service -Name LanmanWorkstation -DependentServices

Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

<span data-ttu-id="c77aa-122">Dokonce můžete získat všechny služby, které mají závislosti.</span><span class="sxs-lookup"><span data-stu-id="c77aa-122">You can even get all services that have dependencies.</span></span> <span data-ttu-id="c77aa-123">Právě tohle dělá následující příkaz a poté použije rutinu Format-Table k zobrazení stavu, název, RequiredServices a DependentServices vlastnosti služeb v počítači.</span><span class="sxs-lookup"><span data-stu-id="c77aa-123">The following command does just that, and then it uses the Format-Table cmdlet to display the Status, Name, RequiredServices and DependentServices properties of the services on the computer.</span></span>

```powershell
Get-Service -Name * | Where-Object {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a><span data-ttu-id="c77aa-124">Zastavení, spuštění, pozastavení a restartování služeb</span><span class="sxs-lookup"><span data-stu-id="c77aa-124">Stopping, Starting, Suspending, and Restarting Services</span></span>
<span data-ttu-id="c77aa-125">Všechny rutiny služby mají stejný obecný tvar.</span><span class="sxs-lookup"><span data-stu-id="c77aa-125">The Service cmdlets all have the same general form.</span></span> <span data-ttu-id="c77aa-126">Služby je možné zadat tak běžný název nebo zobrazovaný název a seznamy a zástupné znaky jako hodnoty.</span><span class="sxs-lookup"><span data-stu-id="c77aa-126">Services can be specified by common name or display name, and take lists and wildcards as values.</span></span> <span data-ttu-id="c77aa-127">K zastavení služby zařazování tisku, použijte:</span><span class="sxs-lookup"><span data-stu-id="c77aa-127">To stop the print spooler, use:</span></span>

```powershell
Stop-Service -Name spooler
```

<span data-ttu-id="c77aa-128">Chcete-li spustit službu zařazování tisku, jakmile je zastaven, použijte:</span><span class="sxs-lookup"><span data-stu-id="c77aa-128">To start the print spooler after it is stopped, use:</span></span>

```powershell
Start-Service -Name spooler
```

<span data-ttu-id="c77aa-129">Pozastavení služby zařazování tisku, použijte:</span><span class="sxs-lookup"><span data-stu-id="c77aa-129">To suspend the print spooler, use:</span></span>

```powershell
Suspend-Service -Name spooler
```

<span data-ttu-id="c77aa-130">**Restart-Service** rutiny funguje stejným způsobem jako u jiných rutin služby, ale ukážeme některé příklady složitější pro něj.</span><span class="sxs-lookup"><span data-stu-id="c77aa-130">The **Restart-Service** cmdlet works in the same manner as the other Service cmdlets, but we will show some more complex examples for it.</span></span> <span data-ttu-id="c77aa-131">V nejjednodušší použití zadejte název služby:</span><span class="sxs-lookup"><span data-stu-id="c77aa-131">In the simplest use, you specify the name of the service:</span></span>

```
PS> Restart-Service -Name spooler

WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

<span data-ttu-id="c77aa-132">Můžete si všimnout, získejte opakované zpráva upozornění o zařazování tisku spuštění.</span><span class="sxs-lookup"><span data-stu-id="c77aa-132">You will notice that you get a repeated warning message about the Print Spooler starting up.</span></span> <span data-ttu-id="c77aa-133">Při provádění operace služby, která se nějakou dobu trvá, prostředí Windows PowerShell vás upozorní, že se stále pokouší o provedení úlohy.</span><span class="sxs-lookup"><span data-stu-id="c77aa-133">When you perform a service operation that takes some time, Windows PowerShell will notify you that it is still attempting to perform the task.</span></span>

<span data-ttu-id="c77aa-134">Pokud chcete restartovat víc služeb, můžete získat seznam služeb, filtrovat je a pak proveďte restart:</span><span class="sxs-lookup"><span data-stu-id="c77aa-134">If you want to restart multiple services, you can get a list of services, filter them, and then perform the restart:</span></span>

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

<span data-ttu-id="c77aa-135">Tyto rutiny služby nemají parametr ComputerName, můžete je ale spustit ve vzdáleném počítači pomocí rutiny Invoke-Command.</span><span class="sxs-lookup"><span data-stu-id="c77aa-135">These Service cmdlets do not have a ComputerName parameter, but you can run them on a remote computer by using the Invoke-Command cmdlet.</span></span> <span data-ttu-id="c77aa-136">Například následující příkaz restartuje službu zařazování tisku na vzdáleném počítači Server01.</span><span class="sxs-lookup"><span data-stu-id="c77aa-136">For example, the following command restarts the Spooler service on the Server01 remote computer.</span></span>

```powershell
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a><span data-ttu-id="c77aa-137">Nastavení vlastnosti služby</span><span class="sxs-lookup"><span data-stu-id="c77aa-137">Setting Service Properties</span></span>

<span data-ttu-id="c77aa-138">Rutina Set-Service změní vlastnosti služby na místním nebo vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="c77aa-138">The Set-Service cmdlet changes the properties of a service on a local or remote computer.</span></span> <span data-ttu-id="c77aa-139">Vzhledem k tomu, že stav služby je vlastnost, můžete použít tuto rutinu pro spuštění, zastavení a pozastavení služby.</span><span class="sxs-lookup"><span data-stu-id="c77aa-139">Because the service status is a property, you can use this cmdlet to start, stop, and suspend a service.</span></span> <span data-ttu-id="c77aa-140">Rutina Set-Service má také parametr typ spuštění, která umožňuje změnit typ spuštění služby.</span><span class="sxs-lookup"><span data-stu-id="c77aa-140">The Set-Service cmdlet also has a StartupType parameter that lets you change the service startup type.</span></span>

<span data-ttu-id="c77aa-141">Pokud chcete použít nastavení služby ve Windows Vista a novějších verzích Windows, otevřete prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".</span><span class="sxs-lookup"><span data-stu-id="c77aa-141">To use Set-Service on Windows Vista and later versions of Windows, open Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="c77aa-142">Další informace najdete v tématu [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="c77aa-142">For more information, see [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>

## <a name="see-also"></a><span data-ttu-id="c77aa-143">Viz také</span><span class="sxs-lookup"><span data-stu-id="c77aa-143">See Also</span></span>

- <span data-ttu-id="c77aa-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span><span class="sxs-lookup"><span data-stu-id="c77aa-144">[Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)</span></span>
- <span data-ttu-id="c77aa-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span><span class="sxs-lookup"><span data-stu-id="c77aa-145">[Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)</span></span>
- <span data-ttu-id="c77aa-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span><span class="sxs-lookup"><span data-stu-id="c77aa-146">[Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)</span></span>
- <span data-ttu-id="c77aa-147">[Pozastavit – služba [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span><span class="sxs-lookup"><span data-stu-id="c77aa-147">[Suspend-Service [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)</span></span>
---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Pomocí DSC na Nano Server"
ms.openlocfilehash: 7427d6bb7644f513b9b523f284109f5ae0f8ef27
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="using-dsc-on-nano-server"></a><span data-ttu-id="18b2f-103">Pomocí DSC na Nano Server</span><span class="sxs-lookup"><span data-stu-id="18b2f-103">Using DSC on Nano Server</span></span>

> <span data-ttu-id="18b2f-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="18b2f-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="18b2f-105">**DSC na Nano Server** je volitelný balíček v `NanoServer\Packages` složky na médiu systému Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="18b2f-105">**DSC on Nano Server** is an optional package in the `NanoServer\Packages` folder of the Windows Server 2016 media.</span></span> <span data-ttu-id="18b2f-106">Balíček lze nainstalovat, když vytvoříte virtuální pevný disk pro Nano Server tak, že zadáte **Microsoft NanoServer DSC balíček** jako hodnotu **balíčky** parametr **New-NanoServerImage**  funkce.</span><span class="sxs-lookup"><span data-stu-id="18b2f-106">The package can be installed when you create a VHD for a Nano Server by specifying **Microsoft-NanoServer-DSC-Package** as the value of the **Packages** parameter of the **New-NanoServerImage** function.</span></span> <span data-ttu-id="18b2f-107">Například pokud vytváříte virtuální pevný disk pro virtuální počítač, příkaz vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="18b2f-107">For example, if you are creating a VHD for a virtual machine, the command would look like the following:</span></span>

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

<span data-ttu-id="18b2f-108">Informace o instalaci a použití Nano Server a také jak spravovat Nano Server s vzdálenou komunikaci prostředí PowerShell najdete v tématu [Začínáme s Nano Server](https://technet.microsoft.com/en-us/library/mt126167.aspx).</span><span class="sxs-lookup"><span data-stu-id="18b2f-108">For information about installing and using Nano Server, as well as how to manage Nano Server with PowerShell Remoting, see [Getting Started with Nano Server](https://technet.microsoft.com/en-us/library/mt126167.aspx).</span></span>


## <a name="dsc-features-available-on-nano-server"></a><span data-ttu-id="18b2f-109">DSC funkce dostupné na Nano Server</span><span class="sxs-lookup"><span data-stu-id="18b2f-109">DSC features available on Nano Server</span></span>

 <span data-ttu-id="18b2f-110">Protože Nano Server podporuje omezenou sadu rozhraní API ve srovnání s plnou verzí systému Windows Server, DSC na Nano Server nemá úplné funkčně rovnocenné s DSC na úplné SKU prozatím spuštěna.</span><span class="sxs-lookup"><span data-stu-id="18b2f-110">Because Nano Server supports only a limited set of APIs compared to a full version of Windows Server, DSC on Nano Server does not have full functional parity with DSC running on full SKUs for the time being.</span></span> <span data-ttu-id="18b2f-111">DSC na Nano Server je v active vývoj a ještě není funkce dokončení.</span><span class="sxs-lookup"><span data-stu-id="18b2f-111">DSC on Nano Server is in active development and is not yet feature complete.</span></span>
 
 <span data-ttu-id="18b2f-112">Následující funkce DSC jsou aktuálně k dispozici na Nano Server:</span><span class="sxs-lookup"><span data-stu-id="18b2f-112">The following DSC features are currently available on Nano Server:</span></span> 


* <span data-ttu-id="18b2f-113">Režimech nabízení a vyžadování</span><span class="sxs-lookup"><span data-stu-id="18b2f-113">Both push and pull modes</span></span>

* <span data-ttu-id="18b2f-114">Všechny rutiny DSC, které existují na plnou verzi Windows serveru, včetně následujících:</span><span class="sxs-lookup"><span data-stu-id="18b2f-114">All DSC cmdlets that exist on a full version of Windows Server, including the following:</span></span> 
  * [<span data-ttu-id="18b2f-115">Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="18b2f-115">Get-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/en-us/library/dn407378.aspx)
  * [<span data-ttu-id="18b2f-116">Set-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="18b2f-116">Set-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/en-us/library/dn521621.aspx)   
  * [<span data-ttu-id="18b2f-117">Enable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="18b2f-117">Enable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [<span data-ttu-id="18b2f-118">Disable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="18b2f-118">Disable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517872.aspx)       
  * [<span data-ttu-id="18b2f-119">Počáteční DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="18b2f-119">Start-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [<span data-ttu-id="18b2f-120">Stop-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="18b2f-120">Stop-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [<span data-ttu-id="18b2f-121">Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="18b2f-121">Get-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [<span data-ttu-id="18b2f-122">Test-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="18b2f-122">Test-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407382.aspx)      
  * [<span data-ttu-id="18b2f-123">Publish-DscConfiguraiton</span><span class="sxs-lookup"><span data-stu-id="18b2f-123">Publish-DscConfiguraiton</span></span>](https://technet.microsoft.com/en-us/library/mt517875.aspx) 
  * [<span data-ttu-id="18b2f-124">Update-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="18b2f-124">Update-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [<span data-ttu-id="18b2f-125">Obnovení DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="18b2f-125">Restore-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [<span data-ttu-id="18b2f-126">Remove-DscConfigurationDocument</span><span class="sxs-lookup"><span data-stu-id="18b2f-126">Remove-DscConfigurationDocument</span></span>](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [<span data-ttu-id="18b2f-127">Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="18b2f-127">Get-DscConfigurationStatus</span></span>](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [<span data-ttu-id="18b2f-128">Vyvolání DscResource</span><span class="sxs-lookup"><span data-stu-id="18b2f-128">Invoke-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [<span data-ttu-id="18b2f-129">Najít DscResource</span><span class="sxs-lookup"><span data-stu-id="18b2f-129">Find-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [<span data-ttu-id="18b2f-130">Get-DscResource</span><span class="sxs-lookup"><span data-stu-id="18b2f-130">Get-DscResource</span></span>](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [<span data-ttu-id="18b2f-131">New-DscChecksum</span><span class="sxs-lookup"><span data-stu-id="18b2f-131">New-DscChecksum</span></span>](https://technet.microsoft.com/en-us/library/dn521622.aspx)    

* <span data-ttu-id="18b2f-132">Kompilování konfigurace (viz [konfigurace DSC](configurations.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-132">Compiling configurations (see [DSC configurations](configurations.md))</span></span>

  <span data-ttu-id="18b2f-133">**Problém:** šifrování hesla (viz [zabezpečení souboru MOF](securemof.md)) během konfigurace kompilace nefunguje.</span><span class="sxs-lookup"><span data-stu-id="18b2f-133">**Issue:** Password encryption (see [Securing the MOF File](securemof.md)) during configuration compilation doesn't work.</span></span>

* <span data-ttu-id="18b2f-134">Kompilování metaconfigurations (viz [konfigurace správce místní konfigurace](metaConfig.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-134">Compiling metaconfigurations (see [Configuring the Local Configuration Manager](metaConfig.md))</span></span>

* <span data-ttu-id="18b2f-135">Systémem prostředků v kontextu uživatele (viz [DSC spuštěná s pověřeními uživatele (Spustit jako)](runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-135">Running a resource under user context (see [Running DSC with user credentials (RunAs)](runAsUser.md))</span></span>

* <span data-ttu-id="18b2f-136">Prostředky na základě – třída (najdete v části [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](authoringResourceClass.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-136">Class-based resources (see [Writing a custom DSC resource with PowerShell classes](authoringResourceClass.md))</span></span>

* <span data-ttu-id="18b2f-137">Ladění prostředků DSC (viz [prostředky DSC ladění](debugresource.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-137">Debugging of DSC resources (see [Debugging DSC resources](debugresource.md))</span></span>
  
  <span data-ttu-id="18b2f-138">**Problém:** nefunguje, pokud prostředek používá PsDscRunAsCredential (viz [DSC spuštěná s pověřeními uživatele](runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-138">**Issue:** Doesn't work if a resource is using PsDscRunAsCredential (see [Running DSC with user credentials](runAsUser.md))</span></span>

* [<span data-ttu-id="18b2f-139">Určení závislostí mezi uzly</span><span class="sxs-lookup"><span data-stu-id="18b2f-139">Specifying cross-node dependencies</span></span>](crossNodeDependencies.md) 

* [<span data-ttu-id="18b2f-140">Správa verzí prostředků</span><span class="sxs-lookup"><span data-stu-id="18b2f-140">Resource versioning</span></span>](sxsResource.md)

* <span data-ttu-id="18b2f-141">Vyžádání klienta (konfigurace a prostředků) (v tématu [nastavení vyžadování klienta pomocí názvy konfigurace](pullClientConfigNames.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-141">Pull client (configurations & resources) (see [Setting up a pull client using configuration names](pullClientConfigNames.md))</span></span>

* [<span data-ttu-id="18b2f-142">Částečné konfigurace (pull a push)</span><span class="sxs-lookup"><span data-stu-id="18b2f-142">Partial configurations (pull & push)</span></span>](partialConfigs.md)

* [<span data-ttu-id="18b2f-143">Vytváření sestav na server vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="18b2f-143">Reporting to pull server</span></span>](reportServer.md) 

* <span data-ttu-id="18b2f-144">Šifrování MOF</span><span class="sxs-lookup"><span data-stu-id="18b2f-144">MOF encryption</span></span>

* <span data-ttu-id="18b2f-145">Protokolování událostí</span><span class="sxs-lookup"><span data-stu-id="18b2f-145">Event logging</span></span>

* <span data-ttu-id="18b2f-146">Generování sestav služby Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="18b2f-146">Azure Automation DSC reporting</span></span>

* <span data-ttu-id="18b2f-147">Prostředky, které jsou plně funkční</span><span class="sxs-lookup"><span data-stu-id="18b2f-147">Resources that are fully functional</span></span>
  * [<span data-ttu-id="18b2f-148">Archiv</span><span class="sxs-lookup"><span data-stu-id="18b2f-148">Archive</span></span>](archiveResource.md)
  * [<span data-ttu-id="18b2f-149">Prostředí</span><span class="sxs-lookup"><span data-stu-id="18b2f-149">Environment</span></span>](environmentResource.md)
  * [<span data-ttu-id="18b2f-150">Soubor</span><span class="sxs-lookup"><span data-stu-id="18b2f-150">File</span></span>](fileResource.md)
  * [<span data-ttu-id="18b2f-151">Protokolu</span><span class="sxs-lookup"><span data-stu-id="18b2f-151">Log</span></span>](logResource.md)
  * <span data-ttu-id="18b2f-152">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="18b2f-152">ProcessSet</span></span>
  * [<span data-ttu-id="18b2f-153">Registru</span><span class="sxs-lookup"><span data-stu-id="18b2f-153">Registry</span></span>](registryResource.md)
  * [<span data-ttu-id="18b2f-154">Skript</span><span class="sxs-lookup"><span data-stu-id="18b2f-154">Script</span></span>](scriptResource.md)
  * <span data-ttu-id="18b2f-155">WindowsPackageCab</span><span class="sxs-lookup"><span data-stu-id="18b2f-155">WindowsPackageCab</span></span>
  * [<span data-ttu-id="18b2f-156">WindowsProcess</span><span class="sxs-lookup"><span data-stu-id="18b2f-156">WindowsProcess</span></span>](windowsProcessResource.md)
  * <span data-ttu-id="18b2f-157">WaitForAll (viz [určení závislostí mezi uzly](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-157">WaitForAll (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="18b2f-158">WaitForAny (viz [určení závislostí mezi uzly](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-158">WaitForAny (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="18b2f-159">WaitForSome (viz [určení závislostí mezi uzly](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="18b2f-159">WaitForSome (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>

* <span data-ttu-id="18b2f-160">Prostředky, které jsou částečně funkční</span><span class="sxs-lookup"><span data-stu-id="18b2f-160">Resources that are partially functional</span></span>
  * [<span data-ttu-id="18b2f-161">Skupina</span><span class="sxs-lookup"><span data-stu-id="18b2f-161">Group</span></span>](groupResource.md)
  * <span data-ttu-id="18b2f-162">GroupSet</span><span class="sxs-lookup"><span data-stu-id="18b2f-162">GroupSet</span></span>
  
  <span data-ttu-id="18b2f-163">**Problém:** výše prostředků nezdaří, pokud je konkrétní instanci volala dvakrát (spouštění dvakrát stejnou konfiguraci)</span><span class="sxs-lookup"><span data-stu-id="18b2f-163">**Issue:** Above resources fail if specific instance is called twice (running the same configuration twice)</span></span>
  
  * [<span data-ttu-id="18b2f-164">Služby</span><span class="sxs-lookup"><span data-stu-id="18b2f-164">Service</span></span>](serviceResource.md)
  * <span data-ttu-id="18b2f-165">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="18b2f-165">ServiceSet</span></span>
  
  <span data-ttu-id="18b2f-166">**Problém:** funguje jenom pro spuštění nebo zastavení služby (stav).</span><span class="sxs-lookup"><span data-stu-id="18b2f-166">**Issue:** Only works for starting/stopping (status) service.</span></span> <span data-ttu-id="18b2f-167">Selže, pokud se jeden pokusí změnit další atributy služby jako startuptype, přihlašovací údaje, popis atd...</span><span class="sxs-lookup"><span data-stu-id="18b2f-167">Fails, if one tries to change other service attributes like startuptype, credentials, description etc..</span></span> <span data-ttu-id="18b2f-168">Vyvolána chyba je podobná:</span><span class="sxs-lookup"><span data-stu-id="18b2f-168">The error thrown is similar to:</span></span>
  
  <span data-ttu-id="18b2f-169">*Nelze najít typ [management.managementobject]: Ověřte, že je načteno sestavení obsahující tohoto typu.*</span><span class="sxs-lookup"><span data-stu-id="18b2f-169">*Cannot find type [management.managementobject]: verify that the assembly containing this type is loaded.*</span></span>
  
* <span data-ttu-id="18b2f-170">Prostředky, které nejsou funkční</span><span class="sxs-lookup"><span data-stu-id="18b2f-170">Resources that are not functional</span></span>
  * [<span data-ttu-id="18b2f-171">Uživatel</span><span class="sxs-lookup"><span data-stu-id="18b2f-171">User</span></span>](userResource.md)
  

## <a name="dsc-features-not-available-on-nano-server"></a><span data-ttu-id="18b2f-172">DSC funkce není k dispozici v Nano Server</span><span class="sxs-lookup"><span data-stu-id="18b2f-172">DSC features not available on Nano Server</span></span>

<span data-ttu-id="18b2f-173">Následující funkce DSC nejsou momentálně k dispozici na Nano Server:</span><span class="sxs-lookup"><span data-stu-id="18b2f-173">The following DSC features are not currently available on Nano Server:</span></span>

* <span data-ttu-id="18b2f-174">Dešifrování MOF dokument s šifrované Změna hesla</span><span class="sxs-lookup"><span data-stu-id="18b2f-174">Decrypting MOF document with encrypted password(s)</span></span> 
* <span data-ttu-id="18b2f-175">Vyžádání obsahu Server--nemůžete nastavit aktuálně na server vyžádané replikace v Nano Server</span><span class="sxs-lookup"><span data-stu-id="18b2f-175">Pull Server--you cannot currently set up a pull server on Nano Server</span></span>
* <span data-ttu-id="18b2f-176">Všechno, co se nenachází v seznamu funkce funguje</span><span class="sxs-lookup"><span data-stu-id="18b2f-176">Anything that is not in the list of feature works</span></span>

## <a name="using-custom-dsc-resources-on-nano-server"></a><span data-ttu-id="18b2f-177">Pomocí vlastní prostředky DSC v Nano Server</span><span class="sxs-lookup"><span data-stu-id="18b2f-177">Using custom DSC resources on Nano Server</span></span>
 
<span data-ttu-id="18b2f-178">Z důvodu omezenou sadu rozhraní API systému Windows a CLR knihovny k dispozici na serveru Nano prostředků DSC, které fungují na plnou verzi Windows CLR nemusí pracovat na Nano Server.</span><span class="sxs-lookup"><span data-stu-id="18b2f-178">Due to a limited sets of Windows APIs and CLR libraries available on Nano Server, DSC resources that work on the full CLR version of Windows do not necessarily work on Nano Server.</span></span> <span data-ttu-id="18b2f-179">Dokončení začátku do konce testování před nasazením jakékoli vlastní prostředky DSC v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="18b2f-179">Complete end-to-end testing before deploying any DSC custom resources to a production environment.</span></span>

## <a name="see-also"></a><span data-ttu-id="18b2f-180">Viz také</span><span class="sxs-lookup"><span data-stu-id="18b2f-180">See Also</span></span>
- [<span data-ttu-id="18b2f-181">Začínáme s Nano Server</span><span class="sxs-lookup"><span data-stu-id="18b2f-181">Getting Started with Nano Server</span></span>](https://technet.microsoft.com/en-us/library/mt126167.aspx)


---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Použití platformy DSC na Nano Serveru
ms.openlocfilehash: 9e26c525b48e8656a3479db9c0a760eaeb8cf58a
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="using-dsc-on-nano-server"></a><span data-ttu-id="eff05-103">Použití platformy DSC na Nano Serveru</span><span class="sxs-lookup"><span data-stu-id="eff05-103">Using DSC on Nano Server</span></span>

> <span data-ttu-id="eff05-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="eff05-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="eff05-105">**DSC na Nano Server** je volitelný balíček v `NanoServer\Packages` složky na médiu systému Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="eff05-105">**DSC on Nano Server** is an optional package in the `NanoServer\Packages` folder of the Windows Server 2016 media.</span></span> <span data-ttu-id="eff05-106">Balíček lze nainstalovat, když vytvoříte virtuální pevný disk pro Nano Server tak, že zadáte **Microsoft NanoServer DSC balíček** jako hodnotu **balíčky** parametr **New-NanoServerImage**  funkce.</span><span class="sxs-lookup"><span data-stu-id="eff05-106">The package can be installed when you create a VHD for a Nano Server by specifying **Microsoft-NanoServer-DSC-Package** as the value of the **Packages** parameter of the **New-NanoServerImage** function.</span></span> <span data-ttu-id="eff05-107">Například pokud vytváříte virtuální pevný disk pro virtuální počítač, příkaz vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="eff05-107">For example, if you are creating a VHD for a virtual machine, the command would look like the following:</span></span>

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

<span data-ttu-id="eff05-108">Informace o instalaci a použití Nano Server a také jak spravovat Nano Server s vzdálenou komunikaci prostředí PowerShell najdete v tématu [Začínáme s Nano Server](https://technet.microsoft.com/library/mt126167.aspx).</span><span class="sxs-lookup"><span data-stu-id="eff05-108">For information about installing and using Nano Server, as well as how to manage Nano Server with PowerShell Remoting, see [Getting Started with Nano Server](https://technet.microsoft.com/library/mt126167.aspx).</span></span>


## <a name="dsc-features-available-on-nano-server"></a><span data-ttu-id="eff05-109">DSC funkce dostupné na Nano Server</span><span class="sxs-lookup"><span data-stu-id="eff05-109">DSC features available on Nano Server</span></span>

 <span data-ttu-id="eff05-110">Protože Nano Server podporuje omezenou sadu rozhraní API ve srovnání s plnou verzí systému Windows Server, DSC na Nano Server nemá úplné funkčně rovnocenné s DSC na úplné SKU prozatím spuštěna.</span><span class="sxs-lookup"><span data-stu-id="eff05-110">Because Nano Server supports only a limited set of APIs compared to a full version of Windows Server, DSC on Nano Server does not have full functional parity with DSC running on full SKUs for the time being.</span></span> <span data-ttu-id="eff05-111">DSC na Nano Server je v active vývoj a ještě není funkce dokončení.</span><span class="sxs-lookup"><span data-stu-id="eff05-111">DSC on Nano Server is in active development and is not yet feature complete.</span></span>

 <span data-ttu-id="eff05-112">Následující funkce DSC jsou aktuálně k dispozici na Nano Server:</span><span class="sxs-lookup"><span data-stu-id="eff05-112">The following DSC features are currently available on Nano Server:</span></span>


* <span data-ttu-id="eff05-113">Režimech nabízení a vyžadování</span><span class="sxs-lookup"><span data-stu-id="eff05-113">Both push and pull modes</span></span>

* <span data-ttu-id="eff05-114">Všechny rutiny DSC, které existují na plnou verzi Windows serveru, včetně následujících:</span><span class="sxs-lookup"><span data-stu-id="eff05-114">All DSC cmdlets that exist on a full version of Windows Server, including the following:</span></span>
  * [<span data-ttu-id="eff05-115">Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="eff05-115">Get-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/library/dn407378.aspx)
  * [<span data-ttu-id="eff05-116">Set-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="eff05-116">Set-DscLocalConfigurationManager</span></span>](https://technet.microsoft.com/library/dn521621.aspx)
  * [<span data-ttu-id="eff05-117">Enable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="eff05-117">Enable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [<span data-ttu-id="eff05-118">Zakázat DscDebug</span><span class="sxs-lookup"><span data-stu-id="eff05-118">Disable-DscDebug</span></span>](https://technet.microsoft.com/en-us/library/mt517872.aspx)
  * [<span data-ttu-id="eff05-119">Počáteční DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="eff05-119">Start-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [<span data-ttu-id="eff05-120">Stop-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="eff05-120">Stop-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [<span data-ttu-id="eff05-121">Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="eff05-121">Get-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [<span data-ttu-id="eff05-122">Test DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="eff05-122">Test-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407382.aspx)
  * [<span data-ttu-id="eff05-123">Publikování DscConfiguraiton</span><span class="sxs-lookup"><span data-stu-id="eff05-123">Publish-DscConfiguraiton</span></span>](https://technet.microsoft.com/en-us/library/mt517875.aspx)
  * [<span data-ttu-id="eff05-124">Aktualizace DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="eff05-124">Update-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [<span data-ttu-id="eff05-125">Obnovení DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="eff05-125">Restore-DscConfiguration</span></span>](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [<span data-ttu-id="eff05-126">Odebrat DscConfigurationDocument</span><span class="sxs-lookup"><span data-stu-id="eff05-126">Remove-DscConfigurationDocument</span></span>](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [<span data-ttu-id="eff05-127">Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="eff05-127">Get-DscConfigurationStatus</span></span>](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [<span data-ttu-id="eff05-128">Vyvolání DscResource</span><span class="sxs-lookup"><span data-stu-id="eff05-128">Invoke-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [<span data-ttu-id="eff05-129">Najít DscResource</span><span class="sxs-lookup"><span data-stu-id="eff05-129">Find-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [<span data-ttu-id="eff05-130">Get-DscResource</span><span class="sxs-lookup"><span data-stu-id="eff05-130">Get-DscResource</span></span>](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [<span data-ttu-id="eff05-131">New-DscChecksum</span><span class="sxs-lookup"><span data-stu-id="eff05-131">New-DscChecksum</span></span>](https://technet.microsoft.com/en-us/library/dn521622.aspx)

* <span data-ttu-id="eff05-132">Kompilování konfigurace (viz [konfigurace DSC](configurations.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-132">Compiling configurations (see [DSC configurations](configurations.md))</span></span>

  <span data-ttu-id="eff05-133">**Problém:** šifrování hesla (viz [zabezpečení souboru MOF](securemof.md)) během konfigurace kompilace nefunguje.</span><span class="sxs-lookup"><span data-stu-id="eff05-133">**Issue:** Password encryption (see [Securing the MOF File](securemof.md)) during configuration compilation doesn't work.</span></span>

* <span data-ttu-id="eff05-134">Kompilování metaconfigurations (viz [konfigurace správce místní konfigurace](metaConfig.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-134">Compiling metaconfigurations (see [Configuring the Local Configuration Manager](metaConfig.md))</span></span>

* <span data-ttu-id="eff05-135">Systémem prostředků v kontextu uživatele (viz [DSC spuštěná s pověřeními uživatele (Spustit jako)](runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-135">Running a resource under user context (see [Running DSC with user credentials (RunAs)](runAsUser.md))</span></span>

* <span data-ttu-id="eff05-136">Prostředky na základě – třída (najdete v části [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](authoringResourceClass.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-136">Class-based resources (see [Writing a custom DSC resource with PowerShell classes](authoringResourceClass.md))</span></span>

* <span data-ttu-id="eff05-137">Ladění prostředků DSC (viz [prostředky DSC ladění](debugresource.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-137">Debugging of DSC resources (see [Debugging DSC resources](debugresource.md))</span></span>

  <span data-ttu-id="eff05-138">**Problém:** nefunguje, pokud prostředek používá PsDscRunAsCredential (viz [DSC spuštěná s pověřeními uživatele](runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-138">**Issue:** Doesn't work if a resource is using PsDscRunAsCredential (see [Running DSC with user credentials](runAsUser.md))</span></span>

* [<span data-ttu-id="eff05-139">Určení závislostí mezi uzly</span><span class="sxs-lookup"><span data-stu-id="eff05-139">Specifying cross-node dependencies</span></span>](crossNodeDependencies.md)

* [<span data-ttu-id="eff05-140">Správa verzí prostředků</span><span class="sxs-lookup"><span data-stu-id="eff05-140">Resource versioning</span></span>](sxsResource.md)

* <span data-ttu-id="eff05-141">Vyžádání klienta (konfigurace a prostředků) (v tématu [nastavení vyžadování klienta pomocí názvy konfigurace](pullClientConfigNames.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-141">Pull client (configurations & resources) (see [Setting up a pull client using configuration names](pullClientConfigNames.md))</span></span>

* [<span data-ttu-id="eff05-142">Částečné konfigurace (pull a push)</span><span class="sxs-lookup"><span data-stu-id="eff05-142">Partial configurations (pull & push)</span></span>](partialConfigs.md)

* [<span data-ttu-id="eff05-143">Vytváření sestav na server vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="eff05-143">Reporting to pull server</span></span>](reportServer.md)

* <span data-ttu-id="eff05-144">Šifrování MOF</span><span class="sxs-lookup"><span data-stu-id="eff05-144">MOF encryption</span></span>

* <span data-ttu-id="eff05-145">Protokolování událostí</span><span class="sxs-lookup"><span data-stu-id="eff05-145">Event logging</span></span>

* <span data-ttu-id="eff05-146">Generování sestav služby Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="eff05-146">Azure Automation DSC reporting</span></span>

* <span data-ttu-id="eff05-147">Prostředky, které jsou plně funkční</span><span class="sxs-lookup"><span data-stu-id="eff05-147">Resources that are fully functional</span></span>
  * [<span data-ttu-id="eff05-148">Archiv</span><span class="sxs-lookup"><span data-stu-id="eff05-148">Archive</span></span>](archiveResource.md)
  * [<span data-ttu-id="eff05-149">Prostředí</span><span class="sxs-lookup"><span data-stu-id="eff05-149">Environment</span></span>](environmentResource.md)
  * [<span data-ttu-id="eff05-150">Soubor</span><span class="sxs-lookup"><span data-stu-id="eff05-150">File</span></span>](fileResource.md)
  * [<span data-ttu-id="eff05-151">Protokolu</span><span class="sxs-lookup"><span data-stu-id="eff05-151">Log</span></span>](logResource.md)
  * <span data-ttu-id="eff05-152">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="eff05-152">ProcessSet</span></span>
  * [<span data-ttu-id="eff05-153">Registru</span><span class="sxs-lookup"><span data-stu-id="eff05-153">Registry</span></span>](registryResource.md)
  * [<span data-ttu-id="eff05-154">Skript</span><span class="sxs-lookup"><span data-stu-id="eff05-154">Script</span></span>](scriptResource.md)
  * <span data-ttu-id="eff05-155">WindowsPackageCab</span><span class="sxs-lookup"><span data-stu-id="eff05-155">WindowsPackageCab</span></span>
  * [<span data-ttu-id="eff05-156">WindowsProcess</span><span class="sxs-lookup"><span data-stu-id="eff05-156">WindowsProcess</span></span>](windowsProcessResource.md)
  * <span data-ttu-id="eff05-157">WaitForAll (viz [určení závislostí mezi uzly](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-157">WaitForAll (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="eff05-158">WaitForAny (viz [určení závislostí mezi uzly](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-158">WaitForAny (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>
  * <span data-ttu-id="eff05-159">WaitForSome (viz [určení závislostí mezi uzly](crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="eff05-159">WaitForSome (see [Specifying cross-node dependencies](crossNodeDependencies.md))</span></span>

* <span data-ttu-id="eff05-160">Prostředky, které jsou částečně funkční</span><span class="sxs-lookup"><span data-stu-id="eff05-160">Resources that are partially functional</span></span>
  * [<span data-ttu-id="eff05-161">Skupina</span><span class="sxs-lookup"><span data-stu-id="eff05-161">Group</span></span>](groupResource.md)
  * <span data-ttu-id="eff05-162">GroupSet</span><span class="sxs-lookup"><span data-stu-id="eff05-162">GroupSet</span></span>

  <span data-ttu-id="eff05-163">**Problém:** výše prostředků nezdaří, pokud je konkrétní instanci volala dvakrát (spouštění dvakrát stejnou konfiguraci)</span><span class="sxs-lookup"><span data-stu-id="eff05-163">**Issue:** Above resources fail if specific instance is called twice (running the same configuration twice)</span></span>

  * [<span data-ttu-id="eff05-164">Služby</span><span class="sxs-lookup"><span data-stu-id="eff05-164">Service</span></span>](serviceResource.md)
  * <span data-ttu-id="eff05-165">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="eff05-165">ServiceSet</span></span>

  <span data-ttu-id="eff05-166">**Problém:** funguje jenom pro spuštění nebo zastavení služby (stav).</span><span class="sxs-lookup"><span data-stu-id="eff05-166">**Issue:** Only works for starting/stopping (status) service.</span></span> <span data-ttu-id="eff05-167">Selže, pokud se jeden pokusí změnit další atributy služby jako startuptype, přihlašovací údaje, popis atd...</span><span class="sxs-lookup"><span data-stu-id="eff05-167">Fails, if one tries to change other service attributes like startuptype, credentials, description etc..</span></span> <span data-ttu-id="eff05-168">Vyvolána chyba je podobná:</span><span class="sxs-lookup"><span data-stu-id="eff05-168">The error thrown is similar to:</span></span>

  <span data-ttu-id="eff05-169">*Nelze najít typ [management.managementobject]: Ověřte, že je načteno sestavení obsahující tohoto typu.*</span><span class="sxs-lookup"><span data-stu-id="eff05-169">*Cannot find type [management.managementobject]: verify that the assembly containing this type is loaded.*</span></span>

* <span data-ttu-id="eff05-170">Prostředky, které nejsou funkční</span><span class="sxs-lookup"><span data-stu-id="eff05-170">Resources that are not functional</span></span>
  * [<span data-ttu-id="eff05-171">Uživatel</span><span class="sxs-lookup"><span data-stu-id="eff05-171">User</span></span>](userResource.md)


## <a name="dsc-features-not-available-on-nano-server"></a><span data-ttu-id="eff05-172">DSC funkce není k dispozici v Nano Server</span><span class="sxs-lookup"><span data-stu-id="eff05-172">DSC features not available on Nano Server</span></span>

<span data-ttu-id="eff05-173">Následující funkce DSC nejsou momentálně k dispozici na Nano Server:</span><span class="sxs-lookup"><span data-stu-id="eff05-173">The following DSC features are not currently available on Nano Server:</span></span>

* <span data-ttu-id="eff05-174">Dešifrování MOF dokument s šifrované Změna hesla</span><span class="sxs-lookup"><span data-stu-id="eff05-174">Decrypting MOF document with encrypted password(s)</span></span>
* <span data-ttu-id="eff05-175">Vyžádání obsahu Server--nemůžete nastavit aktuálně na server vyžádané replikace v Nano Server</span><span class="sxs-lookup"><span data-stu-id="eff05-175">Pull Server--you cannot currently set up a pull server on Nano Server</span></span>
* <span data-ttu-id="eff05-176">Všechno, co se nenachází v seznamu funkce funguje</span><span class="sxs-lookup"><span data-stu-id="eff05-176">Anything that is not in the list of feature works</span></span>

## <a name="using-custom-dsc-resources-on-nano-server"></a><span data-ttu-id="eff05-177">Pomocí vlastní prostředky DSC v Nano Server</span><span class="sxs-lookup"><span data-stu-id="eff05-177">Using custom DSC resources on Nano Server</span></span>

<span data-ttu-id="eff05-178">Z důvodu omezenou sadu rozhraní API systému Windows a CLR knihovny k dispozici na serveru Nano prostředků DSC, které fungují na plnou verzi Windows CLR nemusí pracovat na Nano Server.</span><span class="sxs-lookup"><span data-stu-id="eff05-178">Due to a limited sets of Windows APIs and CLR libraries available on Nano Server, DSC resources that work on the full CLR version of Windows do not necessarily work on Nano Server.</span></span>
<span data-ttu-id="eff05-179">Dokončení začátku do konce testování před nasazením jakékoli vlastní prostředky DSC v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="eff05-179">Complete end-to-end testing before deploying any DSC custom resources to a production environment.</span></span>

## <a name="see-also"></a><span data-ttu-id="eff05-180">Viz také</span><span class="sxs-lookup"><span data-stu-id="eff05-180">See Also</span></span>
- [<span data-ttu-id="eff05-181">Začínáme s Nano Server</span><span class="sxs-lookup"><span data-stu-id="eff05-181">Getting Started with Nano Server</span></span>](https://technet.microsoft.com/library/mt126167.aspx)
---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Použití platformy DSC na Nano Serveru
ms.openlocfilehash: fd81fe56d16100f45d9ee2dfd8fdc303c2a6c17a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403727"
---
# <a name="using-dsc-on-nano-server"></a><span data-ttu-id="0ef7c-103">Použití platformy DSC na Nano Serveru</span><span class="sxs-lookup"><span data-stu-id="0ef7c-103">Using DSC on Nano Server</span></span>

> <span data-ttu-id="0ef7c-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0ef7c-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="0ef7c-105">**DSC na Nano serveru** je volitelný balíček v `NanoServer\Packages` složky média systému Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-105">**DSC on Nano Server** is an optional package in the `NanoServer\Packages` folder of the Windows Server 2016 media.</span></span> <span data-ttu-id="0ef7c-106">Balíček lze nainstalovat při vytváření virtuálního pevného disku pro Nano Server tak, že zadáte **Microsoft-NanoServer-DSC-Package** jako hodnotu **balíčky** parametr **rutiny New-NanoServerImage**  funkce.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-106">The package can be installed when you create a VHD for a Nano Server by specifying **Microsoft-NanoServer-DSC-Package** as the value of the **Packages** parameter of the **New-NanoServerImage** function.</span></span> <span data-ttu-id="0ef7c-107">Například při vytváření virtuálního pevného disku pro virtuální počítač, tento příkaz může vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="0ef7c-107">For example, if you are creating a VHD for a virtual machine, the command would look like the following:</span></span>

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

<span data-ttu-id="0ef7c-108">Informace o instalaci a použití Nano serveru, jakož i jak spravovat Nano serveru pomocí vzdálené komunikace Powershellu najdete v tématu [Začínáme s Nano serverem](/windows-server/get-started/getting-started-with-nano-server).</span><span class="sxs-lookup"><span data-stu-id="0ef7c-108">For information about installing and using Nano Server, as well as how to manage Nano Server with PowerShell Remoting, see [Getting Started with Nano Server](/windows-server/get-started/getting-started-with-nano-server).</span></span>

## <a name="dsc-features-available-on-nano-server"></a><span data-ttu-id="0ef7c-109">Funkce DSC na Nano serveru k dispozici</span><span class="sxs-lookup"><span data-stu-id="0ef7c-109">DSC features available on Nano Server</span></span>

<span data-ttu-id="0ef7c-110">Protože Nano Server podporuje pouze omezená sada rozhraní API ve srovnání s plnou verzí Windows serveru, DSC na Nano serveru s DSC běžící na úplné SKU prozatím úplnou paritu nemá.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-110">Because Nano Server supports only a limited set of APIs compared to a full version of Windows Server, DSC on Nano Server does not have full functional parity with DSC running on full SKUs for the time being.</span></span> <span data-ttu-id="0ef7c-111">DSC na Nano serveru je v aktivním vývoji a ještě není kompletní funkce.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-111">DSC on Nano Server is in active development and is not yet feature complete.</span></span>

<span data-ttu-id="0ef7c-112">Následující funkce DSC jsou nyní dostupné na Nano serveru:</span><span class="sxs-lookup"><span data-stu-id="0ef7c-112">The following DSC features are currently available on Nano Server:</span></span>

<span data-ttu-id="0ef7c-113">Režimech nabízení a vyžadování</span><span class="sxs-lookup"><span data-stu-id="0ef7c-113">Both push and pull modes</span></span>

- <span data-ttu-id="0ef7c-114">Všechny rutiny DSC, které existují na plnou verzi Windows serveru, včetně následujících:</span><span class="sxs-lookup"><span data-stu-id="0ef7c-114">All DSC cmdlets that exist on a full version of Windows Server, including the following:</span></span>
- [<span data-ttu-id="0ef7c-115">Get-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="0ef7c-115">Get-DscLocalConfigurationManager</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager)
- [<span data-ttu-id="0ef7c-116">Set-DscLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="0ef7c-116">Set-DscLocalConfigurationManager</span></span>](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager)
- [<span data-ttu-id="0ef7c-117">Enable-DscDebug</span><span class="sxs-lookup"><span data-stu-id="0ef7c-117">Enable-DscDebug</span></span>](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug)
- [<span data-ttu-id="0ef7c-118">Zakázat DscDebug</span><span class="sxs-lookup"><span data-stu-id="0ef7c-118">Disable-DscDebug</span></span>](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug)
- [<span data-ttu-id="0ef7c-119">Start-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="0ef7c-119">Start-DscConfiguration</span></span>](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration)
- [<span data-ttu-id="0ef7c-120">Stop-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="0ef7c-120">Stop-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration)
- [<span data-ttu-id="0ef7c-121">Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="0ef7c-121">Get-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration)
- [<span data-ttu-id="0ef7c-122">Test-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="0ef7c-122">Test-DscConfiguration</span></span>](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)
- [<span data-ttu-id="0ef7c-123">Publikování DscConfiguraiton</span><span class="sxs-lookup"><span data-stu-id="0ef7c-123">Publish-DscConfiguraiton</span></span>](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration)
- [<span data-ttu-id="0ef7c-124">Update-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="0ef7c-124">Update-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration)
- [<span data-ttu-id="0ef7c-125">Restore-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="0ef7c-125">Restore-DscConfiguration</span></span>](/powershell/module/PSDesiredStateConfiguration/Restore-DscConfiguration)
- [<span data-ttu-id="0ef7c-126">Odebrat DscConfigurationDocument</span><span class="sxs-lookup"><span data-stu-id="0ef7c-126">Remove-DscConfigurationDocument</span></span>](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument)
- [<span data-ttu-id="0ef7c-127">Get-DscConfigurationStatus</span><span class="sxs-lookup"><span data-stu-id="0ef7c-127">Get-DscConfigurationStatus</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus)
- [<span data-ttu-id="0ef7c-128">Invoke-DscResource</span><span class="sxs-lookup"><span data-stu-id="0ef7c-128">Invoke-DscResource</span></span>](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource)
- [<span data-ttu-id="0ef7c-129">Find-DscResource</span><span class="sxs-lookup"><span data-stu-id="0ef7c-129">Find-DscResource</span></span>](https://technet.microsoft.com/en-us/library/mt517874.aspx)
- [<span data-ttu-id="0ef7c-130">Get-DscResource</span><span class="sxs-lookup"><span data-stu-id="0ef7c-130">Get-DscResource</span></span>](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)
- [<span data-ttu-id="0ef7c-131">New-DscChecksum</span><span class="sxs-lookup"><span data-stu-id="0ef7c-131">New-DscChecksum</span></span>](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum)

- <span data-ttu-id="0ef7c-132">Kompilace konfigurací (viz [konfigurací DSC](../configurations/configurations.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-132">Compiling configurations (see [DSC configurations](../configurations/configurations.md))</span></span>

  <span data-ttu-id="0ef7c-133">**Problém:** Heslo šifrování (viz [zabezpečení souboru MOF](../pull-server/secureMOF.md)) během konfigurace kompilace nefunguje.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-133">**Issue:** Password encryption (see [Securing the MOF File](../pull-server/secureMOF.md)) during configuration compilation doesn't work.</span></span>

- <span data-ttu-id="0ef7c-134">Kompilování metaconfigurations (viz [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-134">Compiling metaconfigurations (see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md))</span></span>

- <span data-ttu-id="0ef7c-135">S prostředkem v kontextu uživatele (viz [DSC spuštěná s pověřeními uživatele (Spustit jako)](../configurations/runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-135">Running a resource under user context (see [Running DSC with user credentials (RunAs)](../configurations/runAsUser.md))</span></span>

- <span data-ttu-id="0ef7c-136">Prostředky založené na třídě (viz [psaní vlastního prostředku DSC pomocí tříd Powershellu](../resources/authoringResourceClass.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-136">Class-based resources (see [Writing a custom DSC resource with PowerShell classes](../resources/authoringResourceClass.md))</span></span>

- <span data-ttu-id="0ef7c-137">Ladění prostředků DSC (viz [prostředky DSC ladění](../troubleshooting/debugResource.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-137">Debugging of DSC resources (see [Debugging DSC resources](../troubleshooting/debugResource.md))</span></span>

  <span data-ttu-id="0ef7c-138">**Problém:** Nefunguje, pokud prostředek používá PsDscRunAsCredential (naleznete v tématu [DSC spuštěná s pověřeními uživatele](../configurations/runAsUser.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-138">**Issue:** Doesn't work if a resource is using PsDscRunAsCredential (see [Running DSC with user credentials](../configurations/runAsUser.md))</span></span>

- [<span data-ttu-id="0ef7c-139">Určení závislostí mezi uzly</span><span class="sxs-lookup"><span data-stu-id="0ef7c-139">Specifying cross-node dependencies</span></span>](../configurations/crossNodeDependencies.md)

- [<span data-ttu-id="0ef7c-140">Správa verzí prostředků</span><span class="sxs-lookup"><span data-stu-id="0ef7c-140">Resource versioning</span></span>](../configurations/sxsResource.md)

- <span data-ttu-id="0ef7c-141">Načítacího klienta (konfigurace a prostředky) (viz [nastavení načítacího klienta použití konfiguračních názvů](../pull-server/pullClientConfigNames.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-141">Pull client (configurations & resources) (see [Setting up a pull client using configuration names](../pull-server/pullClientConfigNames.md))</span></span>

- [<span data-ttu-id="0ef7c-142">Částečné konfigurace (pull a push)</span><span class="sxs-lookup"><span data-stu-id="0ef7c-142">Partial configurations (pull & push)</span></span>](../pull-server/partialConfigs.md)

- [<span data-ttu-id="0ef7c-143">Generování sestav na serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="0ef7c-143">Reporting to pull server</span></span>](../pull-server/reportServer.md)

- <span data-ttu-id="0ef7c-144">Šifrování MOF</span><span class="sxs-lookup"><span data-stu-id="0ef7c-144">MOF encryption</span></span>

- <span data-ttu-id="0ef7c-145">Protokolování událostí</span><span class="sxs-lookup"><span data-stu-id="0ef7c-145">Event logging</span></span>

- <span data-ttu-id="0ef7c-146">Generování sestav v Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="0ef7c-146">Azure Automation DSC reporting</span></span>

- <span data-ttu-id="0ef7c-147">Prostředky, které jsou plně funkční</span><span class="sxs-lookup"><span data-stu-id="0ef7c-147">Resources that are fully functional</span></span>

- <span data-ttu-id="0ef7c-148">**Archiv**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-148">**Archive**</span></span>
- <span data-ttu-id="0ef7c-149">**Prostředí**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-149">**Environment**</span></span>
- <span data-ttu-id="0ef7c-150">**Soubor**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-150">**File**</span></span>
- <span data-ttu-id="0ef7c-151">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-151">**Log**</span></span>
- <span data-ttu-id="0ef7c-152">**ProcessSet**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-152">**ProcessSet**</span></span>
- <span data-ttu-id="0ef7c-153">**registru**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-153">**Registry**</span></span>
- <span data-ttu-id="0ef7c-154">**Skript**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-154">**Script**</span></span>
- <span data-ttu-id="0ef7c-155">**WindowsPackageCab**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-155">**WindowsPackageCab**</span></span>
- <span data-ttu-id="0ef7c-156">**WindowsProcess**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-156">**WindowsProcess**</span></span>
- <span data-ttu-id="0ef7c-157">**WaitForAll** (viz [určení závislostí mezi uzly](../configurations/crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-157">**WaitForAll** (see [Specifying cross-node dependencies](../configurations/crossNodeDependencies.md))</span></span>
- <span data-ttu-id="0ef7c-158">**WaitForAny** (viz [určení závislostí mezi uzly](../configurations/crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-158">**WaitForAny** (see [Specifying cross-node dependencies](../configurations/crossNodeDependencies.md))</span></span>
- <span data-ttu-id="0ef7c-159">**WaitForSome** (viz [určení závislostí mezi uzly](../configurations/crossNodeDependencies.md))</span><span class="sxs-lookup"><span data-stu-id="0ef7c-159">**WaitForSome** (see [Specifying cross-node dependencies](../configurations/crossNodeDependencies.md))</span></span>

- <span data-ttu-id="0ef7c-160">Prostředky, které jsou částečně funkční</span><span class="sxs-lookup"><span data-stu-id="0ef7c-160">Resources that are partially functional</span></span>
- <span data-ttu-id="0ef7c-161">**Skupina**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-161">**Group**</span></span>
- <span data-ttu-id="0ef7c-162">**GroupSet**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-162">**GroupSet**</span></span>

  <span data-ttu-id="0ef7c-163">**Problém:** Nad prostředky selhat, pokud je konkrétní instanci volána dvakrát (spuštění dvakrát se stejnou konfigurací)</span><span class="sxs-lookup"><span data-stu-id="0ef7c-163">**Issue:** Above resources fail if specific instance is called twice (running the same configuration twice)</span></span>

- <span data-ttu-id="0ef7c-164">**Služba**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-164">**Service**</span></span>
- <span data-ttu-id="0ef7c-165">**ServiceSet**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-165">**ServiceSet**</span></span>

  <span data-ttu-id="0ef7c-166">**Problém:** Funguje jenom pro spuštění/zastavení služby (stav).</span><span class="sxs-lookup"><span data-stu-id="0ef7c-166">**Issue:** Only works for starting/stopping (status) service.</span></span> <span data-ttu-id="0ef7c-167">Selže, pokud se jeden pokusí změnit další atributy služby jako typ spuštění, přihlašovací údaje, popis atd.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-167">Fails, if one tries to change other service attributes like startuptype, credentials, description etc..</span></span> <span data-ttu-id="0ef7c-168">Je podobný vyvolána chyba:</span><span class="sxs-lookup"><span data-stu-id="0ef7c-168">The error thrown is similar to:</span></span>

  <span data-ttu-id="0ef7c-169">*Nepovedlo se najít typ [management.managementobject]: Ověřte, že je načteno sestavení obsahující tohoto typu.*</span><span class="sxs-lookup"><span data-stu-id="0ef7c-169">*Cannot find type [management.managementobject]: verify that the assembly containing this type is loaded.*</span></span>

- <span data-ttu-id="0ef7c-170">Prostředky, které nejsou funkční</span><span class="sxs-lookup"><span data-stu-id="0ef7c-170">Resources that are not functional</span></span>
- <span data-ttu-id="0ef7c-171">**Uživatel**</span><span class="sxs-lookup"><span data-stu-id="0ef7c-171">**User**</span></span>

## <a name="dsc-features-not-available-on-nano-server"></a><span data-ttu-id="0ef7c-172">Funkce DSC na Nano serveru není k dispozici</span><span class="sxs-lookup"><span data-stu-id="0ef7c-172">DSC features not available on Nano Server</span></span>

<span data-ttu-id="0ef7c-173">Následující funkce DSC nejsou aktuálně dostupné na Nano serveru:</span><span class="sxs-lookup"><span data-stu-id="0ef7c-173">The following DSC features are not currently available on Nano Server:</span></span>

- <span data-ttu-id="0ef7c-174">Dešifrování dokument MOF se změna šifrovaná hesla</span><span class="sxs-lookup"><span data-stu-id="0ef7c-174">Decrypting MOF document with encrypted password(s)</span></span>
- <span data-ttu-id="0ef7c-175">Server o přijetí změn – nelze nastavit aktuálně serveru vyžádané replikace na Nano serveru</span><span class="sxs-lookup"><span data-stu-id="0ef7c-175">Pull Server--you cannot currently set up a pull server on Nano Server</span></span>
- <span data-ttu-id="0ef7c-176">Cokoli, co není v seznamu funkcí funguje</span><span class="sxs-lookup"><span data-stu-id="0ef7c-176">Anything that is not in the list of feature works</span></span>

## <a name="using-custom-dsc-resources-on-nano-server"></a><span data-ttu-id="0ef7c-177">Použití vlastní prostředky DSC na Nano serveru</span><span class="sxs-lookup"><span data-stu-id="0ef7c-177">Using custom DSC resources on Nano Server</span></span>

<span data-ttu-id="0ef7c-178">Kvůli omezené sady rozhraní API pro Windows a knihovny CLR na Nano serveru k dispozici prostředky DSC, pracující na plnou verzi CLR Windows nemusí pracovat na Nano serveru.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-178">Due to a limited sets of Windows APIs and CLR libraries available on Nano Server, DSC resources that work on the full CLR version of Windows do not necessarily work on Nano Server.</span></span>
<span data-ttu-id="0ef7c-179">Dokončení začátku do konce testování před nasazením jakékoli vlastní prostředky DSC do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="0ef7c-179">Complete end-to-end testing before deploying any DSC custom resources to a production environment.</span></span>

## <a name="see-also"></a><span data-ttu-id="0ef7c-180">Viz také</span><span class="sxs-lookup"><span data-stu-id="0ef7c-180">See Also</span></span>

- [<span data-ttu-id="0ef7c-181">Začínáme s Nano serverem</span><span class="sxs-lookup"><span data-stu-id="0ef7c-181">Getting Started with Nano Server</span></span>](/windows-server/get-started/getting-started-with-nano-server)

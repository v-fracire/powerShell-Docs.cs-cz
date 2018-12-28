---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace virtuálních počítačů při prvním spuštění – s využitím DSC
ms.openlocfilehash: 7b9ebc6c818aa39365759945667426c8976997e5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403832"
---
# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a><span data-ttu-id="0ada1-103">Konfigurace virtuálních počítačů při prvním spuštění – s využitím DSC</span><span class="sxs-lookup"><span data-stu-id="0ada1-103">Configure a virtual machines at initial boot-up by using DSC</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ada1-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0ada1-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="requirements"></a><span data-ttu-id="0ada1-105">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0ada1-105">Requirements</span></span>

> [!NOTE]
> <span data-ttu-id="0ada1-106">**DSCAutomationHostEnabled** klíče registru popsané v tomto tématu není k dispozici v Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="0ada1-106">The **DSCAutomationHostEnabled** registry key described in this topic is not available in PowerShell 4.0.</span></span>
> <span data-ttu-id="0ada1-107">Informace o tom, jak nakonfigurovat nové virtuální počítače při prvním spuštění – v Powershellu 4.0 najdete v tématu [Chcete automaticky nakonfigurovat svůj počítače pomocí DSC při spuštění počáteční?] > ()https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span><span class="sxs-lookup"><span data-stu-id="0ada1-107">For information on how to configure new virtual machines at initial boot-up in PowerShell 4.0, see [Want to Automatically Configure Your Machines Using DSC at Initial Boot-up?]> (https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span></span>

<span data-ttu-id="0ada1-108">Pokud chcete spustit tyto příklady, budete potřebovat:</span><span class="sxs-lookup"><span data-stu-id="0ada1-108">To run these examples, you will need:</span></span>

- <span data-ttu-id="0ada1-109">Spouštěcí virtuální pevný disk pro práci s.</span><span class="sxs-lookup"><span data-stu-id="0ada1-109">A bootable VHD to work with.</span></span> <span data-ttu-id="0ada1-110">Můžete si stáhnout soubor ISO s zkušební kopii Windows serveru 2016 na [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="0ada1-110">You can download an ISO with an evaluation copy of Windows Server 2016 at [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span> <span data-ttu-id="0ada1-111">Můžete najít pokyny o tom, jak vytvořit virtuální pevný disk z image ISO v [vytváření spouštěcích virtuálních pevných disků](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).</span><span class="sxs-lookup"><span data-stu-id="0ada1-111">You can find instructions on how to create a VHD from an ISO image at [Creating Bootable Virtual Hard Disks](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).</span></span>
- <span data-ttu-id="0ada1-112">Hostitelský počítač, který má technologie Hyper-V povolena.</span><span class="sxs-lookup"><span data-stu-id="0ada1-112">A host computer that has Hyper-V enabled.</span></span> <span data-ttu-id="0ada1-113">Informace najdete v tématu [Přehled technologie Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).</span><span class="sxs-lookup"><span data-stu-id="0ada1-113">For information, see [Hyper-V overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).</span></span>

  <span data-ttu-id="0ada1-114">S využitím DSC, můžete automatizovat instalaci softwaru a konfigurace pro počítač při prvním spuštění.</span><span class="sxs-lookup"><span data-stu-id="0ada1-114">By using DSC, you can automate software installation and configuration for a computer at initial boot-up.</span></span>
  <span data-ttu-id="0ada1-115">Můžete to provést buď vkládání dokument MOF konfigurací nebo metaconfiguration do spouštěcího média (například virtuální pevný disk) tak, že jsou spouštěny během procesu počáteční spouštěcího.</span><span class="sxs-lookup"><span data-stu-id="0ada1-115">You do this by either injecting a configuration MOF document or a metaconfiguration into bootable media (such as a VHD) so that they are run during the initial boot-up process.</span></span>
  <span data-ttu-id="0ada1-116">Toto chování je určená [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíče registru pod `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies`.</span><span class="sxs-lookup"><span data-stu-id="0ada1-116">This behavior is specified by the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies`.</span></span>
  <span data-ttu-id="0ada1-117">Hodnota tohoto klíče je ve výchozím nastavení, 2, který umožňuje DSC na spuštění při spuštění.</span><span class="sxs-lookup"><span data-stu-id="0ada1-117">By default, the value of this key is 2, which allows DSC to run at boot time.</span></span>

  <span data-ttu-id="0ada1-118">Pokud nechcete, aby DSC na spuštění při spuštění, nastavte hodnotu [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíče registru na hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="0ada1-118">If you do not want DSC to run at boot time, set the value of the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key to 0.</span></span>

- <span data-ttu-id="0ada1-119">Vložit dokument MOF konfigurace do virtuálního pevného disku</span><span class="sxs-lookup"><span data-stu-id="0ada1-119">Inject a configuration MOF document into a VHD</span></span>
- <span data-ttu-id="0ada1-120">Vložit DSC metaconfiguration do virtuálního pevného disku</span><span class="sxs-lookup"><span data-stu-id="0ada1-120">Inject a DSC metaconfiguration into a VHD</span></span>
- <span data-ttu-id="0ada1-121">Zakázat DSC v době spuštění</span><span class="sxs-lookup"><span data-stu-id="0ada1-121">Disable DSC at boot time</span></span>

> [!NOTE]
> <span data-ttu-id="0ada1-122">Můžete vložit obě `Pending.mof` a `MetaConfig.mof` do počítače ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="0ada1-122">You can inject both `Pending.mof` and `MetaConfig.mof` into a computer at the same time.</span></span>
> <span data-ttu-id="0ada1-123">Pokud je oba soubory, nastavení zadané v `MetaConfig.mof` přednost.</span><span class="sxs-lookup"><span data-stu-id="0ada1-123">If both files are present, the settings specified in `MetaConfig.mof` take precedence.</span></span>

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a><span data-ttu-id="0ada1-124">Vložit dokument MOF konfigurace do virtuálního pevného disku</span><span class="sxs-lookup"><span data-stu-id="0ada1-124">Inject a configuration MOF document into a VHD</span></span>

<span data-ttu-id="0ada1-125">Přijmout při prvním spuštění – konfigurace, můžete vložit dokument MOF zkompilovanou konfiguraci do virtuálního pevného disku jako jeho `Pending.mof` souboru.</span><span class="sxs-lookup"><span data-stu-id="0ada1-125">To enact a configuration at initial boot-up, you can inject a compiled configuration MOF document into the VHD as its `Pending.mof` file.</span></span>
<span data-ttu-id="0ada1-126">Pokud **DSCAutomationHostEnabled** nastavení klíče registru na 2 (výchozí hodnota), DSC, budou platit konfigurace určené `Pending.mof` při spuštění počítače pro první.</span><span class="sxs-lookup"><span data-stu-id="0ada1-126">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value), DSC will apply the configuration defined by `Pending.mof` when the computer boots up for the first time.</span></span>

<span data-ttu-id="0ada1-127">V tomto příkladu budeme používat následující konfigurace, které nainstaluje službu IIS v novém počítači:</span><span class="sxs-lookup"><span data-stu-id="0ada1-127">For this example, we will use the following configuration, which will install IIS on the new computer:</span></span>

```powershell
Configuration SampleIISInstall
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    node ('localhost')
    {
        WindowsFeature IIS
        {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
    }
}
```

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a><span data-ttu-id="0ada1-128">Chcete-li vložit dokument MOF konfigurace na virtuální pevný disk</span><span class="sxs-lookup"><span data-stu-id="0ada1-128">To inject the configuration MOF document on the VHD</span></span>

1. <span data-ttu-id="0ada1-129">Připojit virtuální pevný disk, do které chcete vložit konfiguraci voláním [připojit virtuální pevný disk](/powershell/module/hyper-v/mount-vhd) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-129">Mount the VHD into which you want to inject the configuration by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="0ada1-130">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0ada1-130">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="0ada1-131">V počítači se systémem PowerShell 5.0 nebo novější, uložte konfiguraci uvedené výš (**SampleIISInstall**) jako soubor skriptu (.ps1) prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ada1-131">On a computer running PowerShell 5.0 or later, save the above configuration (**SampleIISInstall**) as a PowerShell script (.ps1) file.</span></span>

3. <span data-ttu-id="0ada1-132">V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.</span><span class="sxs-lookup"><span data-stu-id="0ada1-132">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

4. <span data-ttu-id="0ada1-133">Spusťte následující příkazy prostředí PowerShell pro kompilaci dokument MOF (informace o kompilaci konfigurace DSC najdete v tématu [konfigurací DSC](../configurations/configurations.md):</span><span class="sxs-lookup"><span data-stu-id="0ada1-133">Run the following PowerShell commands to compile the MOF document (for information about compiling DSC configurations, see [DSC Configurations](../configurations/configurations.md):</span></span>

   ```powershell
   . .\SampleIISInstall.ps1
   SampleIISInstall
   ```

5. <span data-ttu-id="0ada1-134">Tím se vytvoří `localhost.mof` souboru do nové složky s názvem `SampleIISInstall`.</span><span class="sxs-lookup"><span data-stu-id="0ada1-134">This will create a `localhost.mof` file in a new folder named `SampleIISInstall`.</span></span>
   <span data-ttu-id="0ada1-135">Přejmenování a přesunutí tohoto souboru do správného umístění na virtuálním pevném disku jako `Pending.mof` pomocí [přesunout položku](/powershell/module/microsoft.powershell.management/move-item) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-135">Rename and move that file into the proper location on the VHD as `Pending.mof` by using the [Move-Item](/powershell/module/microsoft.powershell.management/move-item) cmdlet.</span></span> <span data-ttu-id="0ada1-136">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0ada1-136">For example:</span></span>

   ```powershell
       Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
   ```

6. <span data-ttu-id="0ada1-137">Odpojte virtuální pevný disk pomocí volání [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-137">Dismount the VHD by calling the [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) cmdlet.</span></span> <span data-ttu-id="0ada1-138">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0ada1-138">For example:</span></span>

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

7. <span data-ttu-id="0ada1-139">Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali dokument DSC MOF.</span><span class="sxs-lookup"><span data-stu-id="0ada1-139">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>

<span data-ttu-id="0ada1-140">Po počáteční spouštěcí nahoru a instalace operačního systému se nainstaluje službu IIS.</span><span class="sxs-lookup"><span data-stu-id="0ada1-140">After intial boot-up and operating system installation, IIS will be installed.</span></span>
<span data-ttu-id="0ada1-141">Můžete to ověřit pomocí volání [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-141">You can verify this by calling the [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) cmdlet.</span></span>

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a><span data-ttu-id="0ada1-142">Vložit DSC metaconfiguration do virtuálního pevného disku</span><span class="sxs-lookup"><span data-stu-id="0ada1-142">Inject a DSC metaconfiguration into a VHD</span></span>

<span data-ttu-id="0ada1-143">Můžete také nakonfigurovat počítač k o přijetí změn konfigurace při počáteční spuštění-vložením metaconfiguration (viz [konfigurace místní Configuration Manageru (LCM)](../managing-nodes/metaConfig.md)) do virtuálního pevného disku jako jeho `MetaConfig.mof` souboru.</span><span class="sxs-lookup"><span data-stu-id="0ada1-143">You can also configure a computer to pull a configuration at intial boot-up by injecting a metaconfiguration (see [Configuring the Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md)) into the VHD as its `MetaConfig.mof` file.</span></span>
<span data-ttu-id="0ada1-144">Pokud **DSCAutomationHostEnabled** nastavení klíče registru na 2 (výchozí hodnota), DSC, má platit metaconfiguration určené `MetaConfig.mof` k LCM, když se počítač spustí do první.</span><span class="sxs-lookup"><span data-stu-id="0ada1-144">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value),  DSC will apply the metaconfiguration defined by `MetaConfig.mof` to the LCM when the computer boots up for the first time.</span></span>
<span data-ttu-id="0ada1-145">Pokud metaconfiguration určuje LCM by měla o přijetí změn konfigurace ze serveru vyžádané replikace, počítač se pokusí o přijetí změn konfigurace z tohoto serveru vyžádané replikace při prvním spuštění.</span><span class="sxs-lookup"><span data-stu-id="0ada1-145">If the metaconfiguration specifies that the LCM should pull configurations from a pull server, the computer will attempt to pull a configuration from that pull server at inital boot-up.</span></span>
<span data-ttu-id="0ada1-146">Informace o nastavení serveru vyžádané replikace DSC najdete v tématu [nastavení webového serveru vyžádané replikace DSC](../pull-server/pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="0ada1-146">For information about setting up a DSC pull server, see [Setting up a DSC web pull server](../pull-server/pullServer.md).</span></span>

<span data-ttu-id="0ada1-147">V tomto příkladu použijeme konfiguraci popsané v předchozí části (**SampleIISInstall**) a následující metaconfiguration:</span><span class="sxs-lookup"><span data-stu-id="0ada1-147">For this example, we will use both the configuration described in the previous section (**SampleIISInstall**), and the following metaconfiguration:</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientBootstrap
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('SampleIISInstall')
        }
    }
}
```

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a><span data-ttu-id="0ada1-148">Chcete-li vložit dokument MOF metaconfiguration virtuální pevný disk</span><span class="sxs-lookup"><span data-stu-id="0ada1-148">To inject the metaconfiguration MOF document on the VHD</span></span>

1. <span data-ttu-id="0ada1-149">Připojit virtuální pevný disk, do které chcete vložit metaconfiguration voláním [připojit virtuální pevný disk](/powershell/module/hyper-v/mount-vhd) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-149">Mount the VHD into which you want to inject the metaconfiguration by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="0ada1-150">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0ada1-150">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="0ada1-151">[Nastavení webového serveru vyžádané replikace DSC](../pull-server/pullServer.md)a uložit **SampleIISInistall** konfigurace do příslušné složky.</span><span class="sxs-lookup"><span data-stu-id="0ada1-151">[Set up a DSC web pull server](../pull-server/pullServer.md), and save the **SampleIISInistall** configuration to the appropriate folder.</span></span>

3. <span data-ttu-id="0ada1-152">V počítači se systémem PowerShell 5.0 nebo novější, uložit výše metaconfiguration (**PullClientBootstrap**) jako soubor skriptu (.ps1) prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ada1-152">On a computer running PowerShell 5.0 or later, save the above metaconfiguration (**PullClientBootstrap**) as a PowerShell script (.ps1) file.</span></span>

4. <span data-ttu-id="0ada1-153">V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.</span><span class="sxs-lookup"><span data-stu-id="0ada1-153">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

5. <span data-ttu-id="0ada1-154">Spusťte následující příkazy prostředí PowerShell pro kompilaci dokument MOF metaconfiguration (informace o kompilaci konfigurace DSC najdete v tématu [konfigurací DSC](../configurations/configurations.md):</span><span class="sxs-lookup"><span data-stu-id="0ada1-154">Run the following PowerShell commands to compile the  metaconfiguration MOF document (for information about compiling DSC configurations, see [DSC Configurations](../configurations/configurations.md):</span></span>

   ```powershell
   . .\PullClientBootstrap.ps1
   PullClientBootstrap
   ```

6. <span data-ttu-id="0ada1-155">Tím se vytvoří `localhost.meta.mof` souboru do nové složky s názvem `PullClientBootstrap`.</span><span class="sxs-lookup"><span data-stu-id="0ada1-155">This will create a `localhost.meta.mof` file in a new folder named `PullClientBootstrap`.</span></span>
   <span data-ttu-id="0ada1-156">Přejmenování a přesunutí tohoto souboru do správného umístění na virtuálním pevném disku jako `MetaConfig.mof` pomocí [přesunout položku](/powershell/module/microsoft.powershell.management/move-item) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-156">Rename and move that file into the proper location on the VHD as `MetaConfig.mof` by using the [Move-Item](/powershell/module/microsoft.powershell.management/move-item) cmdlet.</span></span>

   ```powershell
   Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\System32\Configuration\MetaConfig.mof
   ```

7. <span data-ttu-id="0ada1-157">Odpojte virtuální pevný disk pomocí volání [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-157">Dismount the VHD by calling the [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) cmdlet.</span></span> <span data-ttu-id="0ada1-158">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0ada1-158">For example:</span></span>

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

8. <span data-ttu-id="0ada1-159">Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali dokument DSC MOF.</span><span class="sxs-lookup"><span data-stu-id="0ada1-159">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>

<span data-ttu-id="0ada1-160">Po počáteční spouštěcí nahoru a instalace operačního systému DSC bude o přijetí změn konfigurace ze serveru vyžádané replikace a nainstaluje službu IIS.</span><span class="sxs-lookup"><span data-stu-id="0ada1-160">After intial boot-up and operating system installation, DSC will pull the configuration from the pull server, and IIS will be installed.</span></span>
<span data-ttu-id="0ada1-161">Můžete to ověřit pomocí volání [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-161">You can verify this by calling the [Get-WindowsFeature](/powershell/module/servermanager/get-windowsfeature) cmdlet.</span></span>

## <a name="disable-dsc-at-boot-time"></a><span data-ttu-id="0ada1-162">Zakázat DSC v době spuštění</span><span class="sxs-lookup"><span data-stu-id="0ada1-162">Disable DSC at boot time</span></span>

<span data-ttu-id="0ada1-163">Ve výchozím nastavení mají hodnotu `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled` klíč nastavený na 2, který umožňuje konfiguraci DSC ke spouštění, pokud je počítač ve stavu čekající na vyřízení nebo aktuální.</span><span class="sxs-lookup"><span data-stu-id="0ada1-163">By default, the value of the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled` key is set to 2, which allows a DSC configuration to run if the computer is in pending or current state.</span></span> <span data-ttu-id="0ada1-164">Pokud nechcete, aby konfiguraci, kterou chcete spustit při prvním spuštění-, třeba proto nastavíte hodnotu tohoto klíče na hodnotu 0:</span><span class="sxs-lookup"><span data-stu-id="0ada1-164">If you do not want a configuration to run at initial boot-up, you need so set the value of this key to 0:</span></span>

1. <span data-ttu-id="0ada1-165">Připojit virtuální pevný disk pomocí volání [připojit virtuální pevný disk](/powershell/module/hyper-v/mount-vhd) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0ada1-165">Mount the VHD by calling the [Mount-VHD](/powershell/module/hyper-v/mount-vhd) cmdlet.</span></span> <span data-ttu-id="0ada1-166">Příklad:</span><span class="sxs-lookup"><span data-stu-id="0ada1-166">For example:</span></span>

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. <span data-ttu-id="0ada1-167">Načtení registru `HKLM\Software` podklíče z virtuálního pevného disku voláním `reg load`.</span><span class="sxs-lookup"><span data-stu-id="0ada1-167">Load the registry `HKLM\Software` subkey from the VHD by calling `reg load`.</span></span>

   ```powershell
   reg load HKLM\Vhd E:\Windows\System32\Config\Software`
   ```

3. <span data-ttu-id="0ada1-168">Přejděte `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*` pomocí poskytovatele prostředí PowerShell registru.</span><span class="sxs-lookup"><span data-stu-id="0ada1-168">Navigate to the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*` by using the PowerShell Registry provider.</span></span>

   ```powershell
   Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
   ```

4. <span data-ttu-id="0ada1-169">Změňte hodnotu vlastnosti `DSCAutomationHostEnabled` na hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="0ada1-169">Change the value of `DSCAutomationHostEnabled` to 0.</span></span>

   ```powershell
   Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
   ```

5. <span data-ttu-id="0ada1-170">Uvolněte registru spuštěním následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="0ada1-170">Unload the registry by running the following commands:</span></span>

   ```powershell
   [gc]::Collect()
   reg unload HKLM\Vhd
   ```

## <a name="see-also"></a><span data-ttu-id="0ada1-171">Viz také</span><span class="sxs-lookup"><span data-stu-id="0ada1-171">See Also</span></span>

[<span data-ttu-id="0ada1-172">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="0ada1-172">DSC Configurations</span></span>](../configurations/configurations.md)

[<span data-ttu-id="0ada1-173">Klíč registru DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="0ada1-173">DSCAutomationHostEnabled registry key</span></span>](DSCAutomationHostEnabled.md)

[<span data-ttu-id="0ada1-174">Konfigurace Local Configuration Manageru (LCM)</span><span class="sxs-lookup"><span data-stu-id="0ada1-174">Configuring the Local Configuration Manager (LCM)</span></span>](../managing-nodes/metaConfig.md)

[<span data-ttu-id="0ada1-175">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="0ada1-175">Setting up a DSC web pull server</span></span>](../pull-server/pullServer.md)

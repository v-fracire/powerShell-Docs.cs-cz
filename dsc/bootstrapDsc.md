---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC"
ms.openlocfilehash: 76c990ee7c98ea47d1fc3d7bd955ce6a993e28a6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
><span data-ttu-id="17081-103">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="17081-103">Applies To: Windows PowerShell 5.0</span></span>

><span data-ttu-id="17081-104">**Poznámka:** **DSCAutomationHostEnabled** klíče registru popsané v tomto tématu není k dispozici v prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="17081-104">**Note:** The **DSCAutomationHostEnabled** registry key described in this topic is not available in PowerShell 4.0.</span></span>
<span data-ttu-id="17081-105">Informace o tom, jak konfigurovat nové virtuální počítače na počáteční telefonického spouštění v prostředí PowerShell 4.0 najdete v tématu [chcete automaticky nakonfigurovat vaše počítače pomocí DSC v počáteční spouštěcí up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span><span class="sxs-lookup"><span data-stu-id="17081-105">For information on how to configure new virtual machines at initial boot-up in PowerShell 4.0, see [Want to Automatically Configure Your Machines Using DSC at Initial Boot-up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)</span></span>

# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a><span data-ttu-id="17081-106">Konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC</span><span class="sxs-lookup"><span data-stu-id="17081-106">Configure a virtual machines at initial boot-up by using DSC</span></span>

## <a name="requirements"></a><span data-ttu-id="17081-107">Požadavky</span><span class="sxs-lookup"><span data-stu-id="17081-107">Requirements</span></span>

<span data-ttu-id="17081-108">Pokud chcete spustit tyto příklady, budete potřebovat:</span><span class="sxs-lookup"><span data-stu-id="17081-108">To run these examples, you will need:</span></span>

- <span data-ttu-id="17081-109">Spouštěcí virtuální pevný disk pro práci s.</span><span class="sxs-lookup"><span data-stu-id="17081-109">A bootable VHD to work with.</span></span> <span data-ttu-id="17081-110">Můžete si stáhnout soubor ISO s zkušební kopie systému Windows Server 2016 na [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span><span class="sxs-lookup"><span data-stu-id="17081-110">You can download an ISO with an evaluation copy of Windows Server 2016 at [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span> <span data-ttu-id="17081-111">Pokyny naleznete v tom, jak vytvořit virtuální pevný disk z bitové kopie ISO na [vytváření spouštěcího virtuální pevné disky](https://technet.microsoft.com/en-us/library/gg318049.aspx).</span><span class="sxs-lookup"><span data-stu-id="17081-111">You can find instructions on how to create a VHD from an ISO image at [Creating Bootable Virtual Hard Disks](https://technet.microsoft.com/en-us/library/gg318049.aspx).</span></span>
- <span data-ttu-id="17081-112">Hostitelský počítač, který má technologie Hyper-V povolena.</span><span class="sxs-lookup"><span data-stu-id="17081-112">A host computer that has Hyper-V enabled.</span></span> <span data-ttu-id="17081-113">Informace najdete v tématu [Přehled technologie Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).</span><span class="sxs-lookup"><span data-stu-id="17081-113">For information, see [Hyper-V overview](https://technet.microsoft.com/library/hh831531.aspx).</span></span>

<span data-ttu-id="17081-114">Pomocí DSC můžete automatizovat instalaci softwaru a konfigurace pro počítač v počáteční spouštěcí up.</span><span class="sxs-lookup"><span data-stu-id="17081-114">By using DSC, you can automate software installation and configuration for a computer at initial boot-up.</span></span>
<span data-ttu-id="17081-115">To provedete vložením buď MOF dokumentu konfigurace nebo metakonfiguraci do spouštěcí médium (například virtuální pevný disk) tak, aby se při prvním procesu spouštění up spouštět.</span><span class="sxs-lookup"><span data-stu-id="17081-115">You do this by either injecting a configuration MOF document or a metaconfiguration into bootable media (such as a VHD) so that they are run during the initial boot-up process.</span></span>
<span data-ttu-id="17081-116">Toto chování je zadána [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíč registru v **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.</span><span class="sxs-lookup"><span data-stu-id="17081-116">This behavior is specified by the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.</span></span>
<span data-ttu-id="17081-117">Hodnota tohoto klíče je ve výchozím nastavení, 2, který umožňuje DSC na spuštění při spuštění.</span><span class="sxs-lookup"><span data-stu-id="17081-117">By default, the value of this key is 2, which allows DSC to run at boot time.</span></span>

<span data-ttu-id="17081-118">Pokud nechcete, aby DSC na spuštění při spuštění, nastavte hodnotu [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíč registru na hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="17081-118">If you do not want DSC to run at boot time, set the value of the [DSCAutomationHostEnabled registry key](DSCAutomationHostEnabled.md) registry key to 0.</span></span>

- <span data-ttu-id="17081-119">Vložit dokument MOF konfigurace do virtuální pevný disk</span><span class="sxs-lookup"><span data-stu-id="17081-119">Inject a configuration MOF document into a VHD</span></span>
- <span data-ttu-id="17081-120">Vložit metakonfiguraci DSC do virtuálního pevného disku</span><span class="sxs-lookup"><span data-stu-id="17081-120">Inject a DSC metaconfiguration into a VHD</span></span>
- <span data-ttu-id="17081-121">Zakázat DSC při spuštění</span><span class="sxs-lookup"><span data-stu-id="17081-121">Disable DSC at boot time</span></span>

><span data-ttu-id="17081-122">**Poznámka:** můžete vložit obě `Pending.mof` a `MetaConfig.mof` do počítače ve stejnou dobu.</span><span class="sxs-lookup"><span data-stu-id="17081-122">**Note:** You can inject both `Pending.mof` and `MetaConfig.mof` into a computer at the same time.</span></span>
<span data-ttu-id="17081-123">Pokud nejsou oba soubory, nastavení zadané v `MetaConfig.mof` přednost.</span><span class="sxs-lookup"><span data-stu-id="17081-123">If both files are present, the settings specified in `MetaConfig.mof` take precedence.</span></span>

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a><span data-ttu-id="17081-124">Vložit dokument MOF konfigurace do virtuální pevný disk</span><span class="sxs-lookup"><span data-stu-id="17081-124">Inject a configuration MOF document into a VHD</span></span>

<span data-ttu-id="17081-125">K uplatní konfigurace na počáteční spouštěcí up, můžete vložit dokument MOF kompilované konfigurace do virtuálního pevného disku jako jeho `Pending.mof` souboru.</span><span class="sxs-lookup"><span data-stu-id="17081-125">To enact a configuration at initial boot-up, you can inject a compiled configuration MOF document into the VHD as its `Pending.mof` file.</span></span>
<span data-ttu-id="17081-126">Pokud **DSCAutomationHostEnabled** klíč registru je nastavena na 2 (výchozí hodnota), DSC se použijí konfigurace definované `Pending.mof` když se počítač spustí službu poprvé.</span><span class="sxs-lookup"><span data-stu-id="17081-126">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value), DSC will apply the configuration defined by `Pending.mof` when the computer boots up for the first time.</span></span>

<span data-ttu-id="17081-127">V tomto příkladu použijeme následující konfiguraci, která nainstaluje službu IIS na novém počítači:</span><span class="sxs-lookup"><span data-stu-id="17081-127">For this example, we will use the following configuration, which will install IIS on the new computer:</span></span>

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

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a><span data-ttu-id="17081-128">Vložení dokumentu MOF konfigurace na virtuální pevný disk</span><span class="sxs-lookup"><span data-stu-id="17081-128">To inject the configuration MOF document on the VHD</span></span>

1. <span data-ttu-id="17081-129">Připojit virtuální pevný disk, do kterého chcete vložit konfigurace voláním [připojit virtuální pevný disk](https://technet.microsoft.com/library/hh848551.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-129">Mount the VHD into which you want to inject the configuration by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="17081-130">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17081-130">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```
2. <span data-ttu-id="17081-131">V počítači se systémem PowerShell 5.0 nebo novější, uložte výše konfiguraci (**SampleIISInstall**) jako soubor skriptu (.ps1) v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17081-131">On a computer running PowerShell 5.0 or later, save the above configuration (**SampleIISInstall**) as a PowerShell script (.ps1) file.</span></span>

3. <span data-ttu-id="17081-132">V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.</span><span class="sxs-lookup"><span data-stu-id="17081-132">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

4. <span data-ttu-id="17081-133">Spusťte následující příkazy prostředí PowerShell zkompilovat soubor MOF dokumentu (informace o kompilaci konfigurace DSC najdete v tématu [konfigurace DSC](configurations.md):</span><span class="sxs-lookup"><span data-stu-id="17081-133">Run the following PowerShell commands to compile the MOF document (for information about compiling DSC configurations, see [DSC Configurations](configurations.md):</span></span>

    ```powershell
    . .\SampleIISInstall.ps1
    SampleIISInstall
    ```

5. <span data-ttu-id="17081-134">Tím se vytvoří `localhost.mof` souboru do nové složky s názvem `SampleIISInstall`.</span><span class="sxs-lookup"><span data-stu-id="17081-134">This will create a `localhost.mof` file in a new folder named `SampleIISInstall`.</span></span>
<span data-ttu-id="17081-135">Přejmenování a přesunutí tento soubor do příslušného umístění na virtuální pevný disk jako `Pending.mof` pomocí [přesunout položku](https://technet.microsoft.comlibrary/hh849852.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-135">Rename and move that file into the proper location on the VHD as `Pending.mof` by using the [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx) cmdlet.</span></span> <span data-ttu-id="17081-136">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17081-136">For example:</span></span>

    ```powershell
        Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
    ```
6. <span data-ttu-id="17081-137">Odpojte virtuální pevný disk pomocí volání [odpojení virtuálního pevného disku](https://technet.microsoft.com/library/hh848562.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-137">Dismount the VHD by calling the [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) cmdlet.</span></span> <span data-ttu-id="17081-138">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17081-138">For example:</span></span>

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

7. <span data-ttu-id="17081-139">Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali DSC MOF dokumentu.</span><span class="sxs-lookup"><span data-stu-id="17081-139">Create a VM by using the VHD where you installed the DSC MOF document.</span></span> <span data-ttu-id="17081-140">Po instalaci operačního systému a vyhledá spouštěcí up bude nainstalována služba IIS.</span><span class="sxs-lookup"><span data-stu-id="17081-140">After intial boot-up and operating system installation, IIS will be installed.</span></span>
<span data-ttu-id="17081-141">Můžete to ověřit pomocí volání [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-141">You can verify this by calling the [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) cmdlet.</span></span>

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a><span data-ttu-id="17081-142">Vložit metakonfiguraci DSC do virtuálního pevného disku</span><span class="sxs-lookup"><span data-stu-id="17081-142">Inject a DSC metaconfiguration into a VHD</span></span>

<span data-ttu-id="17081-143">Můžete také nakonfigurovat počítač načítat konfigurace v vyhledá spouštěcí up vložením metakonfiguraci (najdete v části [konfigurace místní Configuration Manager (LCM)](metaConfig.md)) do virtuálního pevného disku jako jeho `MetaConfig.mof` souboru.</span><span class="sxs-lookup"><span data-stu-id="17081-143">You can also configure a computer to pull a configuration at intial boot-up by injecting a metaconfiguration (see [Configuring the Local Configuration Manager (LCM)](metaConfig.md)) into the VHD as its `MetaConfig.mof` file.</span></span>
<span data-ttu-id="17081-144">Pokud **DSCAutomationHostEnabled** klíč registru je nastavena na 2 (výchozí hodnota), DSC se použijí metakonfiguraci definované `MetaConfig.mof` k LCM, když se počítač spustí službu poprvé.</span><span class="sxs-lookup"><span data-stu-id="17081-144">If the **DSCAutomationHostEnabled** registry key is set to 2 (the default value),  DSC will apply the metaconfiguration defined by `MetaConfig.mof` to the LCM when the computer boots up for the first time.</span></span>
<span data-ttu-id="17081-145">Pokud metakonfiguraci Určuje, že by měl LCM přijetí změn konfigurace z načítacího serveru, počítač se pokusí o konfiguraci z tohoto serveru vyžádané replikace pro vyžádání obsahu na počáteční spouštěcí up.</span><span class="sxs-lookup"><span data-stu-id="17081-145">If the metaconfiguration specifies that the LCM should pull configurations from a pull server, the computer will attempt to pull a configuration from that pull server at inital boot-up.</span></span>
<span data-ttu-id="17081-146">Informace o nastavení server DSC za najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="17081-146">For information about setting up a DSC pull server, see [Setting up a DSC web pull server](pullServer.md).</span></span>

<span data-ttu-id="17081-147">V tomto příkladu použijeme konfiguraci popsané v předchozí části (**SampleIISInstall**) a následující metakonfiguraci:</span><span class="sxs-lookup"><span data-stu-id="17081-147">For this example, we will use both the configuration described in the previous section (**SampleIISInstall**), and the following metaconfiguration:</span></span>

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

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a><span data-ttu-id="17081-148">Chcete-li vložit dokument MOF metakonfiguraci na virtuální pevný disk</span><span class="sxs-lookup"><span data-stu-id="17081-148">To inject the metaconfiguration MOF document on the VHD</span></span>

1. <span data-ttu-id="17081-149">Připojit virtuální pevný disk, do kterého chcete vložit metakonfiguraci voláním [připojit virtuální pevný disk](https://technet.microsoft.com/library/hh848551.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-149">Mount the VHD into which you want to inject the metaconfiguration by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="17081-150">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17081-150">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. <span data-ttu-id="17081-151">[Nastavení webového serveru vyžádané replikace DSC](pullServer.md)a uložte **SampleIISInistall** konfigurace do příslušné složky.</span><span class="sxs-lookup"><span data-stu-id="17081-151">[Set up a DSC web pull server](pullServer.md), and save the **SampleIISInistall** configuration to the appropriate folder.</span></span>

3. <span data-ttu-id="17081-152">V počítači se systémem PowerShell 5.0 nebo novější, uložit výše metakonfiguraci (**PullClientBootstrap**) jako soubor skriptu (.ps1) v prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17081-152">On a computer running PowerShell 5.0 or later, save the above metaconfiguration (**PullClientBootstrap**) as a PowerShell script (.ps1) file.</span></span>

4. <span data-ttu-id="17081-153">V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.</span><span class="sxs-lookup"><span data-stu-id="17081-153">In a PowerShell console, navigate to the folder where you saved the .ps1 file.</span></span>

5. <span data-ttu-id="17081-154">Spusťte následující příkazy prostředí PowerShell zkompilovat soubor MOF dokumentu metakonfiguraci (informace o kompilaci konfigurace DSC najdete v tématu [konfigurace DSC](configurations.md):</span><span class="sxs-lookup"><span data-stu-id="17081-154">Run the following PowerShell commands to compile the  metaconfiguration MOF document (for information about compiling DSC configurations, see [DSC Configurations](configurations.md):</span></span>

    ```powershell
    . .\PullClientBootstrap.ps1
    PullClientBootstrap
    ```

6. <span data-ttu-id="17081-155">Tím se vytvoří `localhost.meta.mof` souboru do nové složky s názvem `PullClientBootstrap`.</span><span class="sxs-lookup"><span data-stu-id="17081-155">This will create a `localhost.meta.mof` file in a new folder named `PullClientBootstrap`.</span></span>
<span data-ttu-id="17081-156">Přejmenování a přesunutí tento soubor do příslušného umístění na virtuální pevný disk jako `MetaConfig.mof` pomocí [přesunout položku](https://technet.microsoft.comlibrary/hh849852.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-156">Rename and move that file into the proper location on the VHD as `MetaConfig.mof` by using the [Move-Item](https://technet.microsoft.comlibrary/hh849852.aspx) cmdlet.</span></span>

    ```powershell
    Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\Sytem32\Configuration\MetaConfig.mof
    ```

7. <span data-ttu-id="17081-157">Odpojte virtuální pevný disk pomocí volání [odpojení virtuálního pevného disku](https://technet.microsoft.com/library/hh848562.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-157">Dismount the VHD by calling the [Dismount-VHD](https://technet.microsoft.com/library/hh848562.aspx) cmdlet.</span></span> <span data-ttu-id="17081-158">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17081-158">For example:</span></span>

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

8. <span data-ttu-id="17081-159">Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali DSC MOF dokumentu.</span><span class="sxs-lookup"><span data-stu-id="17081-159">Create a VM by using the VHD where you installed the DSC MOF document.</span></span>
<span data-ttu-id="17081-160">Po instalaci operačního systému a vyhledá spouštěcí up DSC načte konfiguraci z načítacího serveru a služby IIS se nainstalují.</span><span class="sxs-lookup"><span data-stu-id="17081-160">After intial boot-up and operating system installation, DSC will pull the configuration from the pull server, and IIS will be installed.</span></span>
<span data-ttu-id="17081-161">Můžete to ověřit pomocí volání [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-161">You can verify this by calling the [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) cmdlet.</span></span>

## <a name="disable-dsc-at-boot-time"></a><span data-ttu-id="17081-162">Zakázat DSC při spuštění</span><span class="sxs-lookup"><span data-stu-id="17081-162">Disable DSC at boot time</span></span>

<span data-ttu-id="17081-163">Výchozí hodnota **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** klíč je nastavena na 2, což umožňuje konfiguraci DSC ke spuštění, pokud je počítač v aktuální nebo čekající na vyřízení stav.</span><span class="sxs-lookup"><span data-stu-id="17081-163">By default, the value of the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** key is set to 2, which allows a DSC configuration to run if the computer is in pending or current state.</span></span> <span data-ttu-id="17081-164">Pokud nechcete, aby konfiguraci, kterou chcete spustit počáteční spouštěcí up, třeba, nastavte hodnotu tohoto klíče na hodnotu 0:</span><span class="sxs-lookup"><span data-stu-id="17081-164">If you do not want a configuration to run at initial boot-up, you need so set the value of this key to 0:</span></span>

1. <span data-ttu-id="17081-165">Připojit virtuální pevný disk pomocí volání [připojit virtuální pevný disk](https://technet.microsoft.com/library/hh848551.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="17081-165">Mount the VHD by calling the [Mount-VHD](https://technet.microsoft.com/library/hh848551.aspx) cmdlet.</span></span> <span data-ttu-id="17081-166">Příklad:</span><span class="sxs-lookup"><span data-stu-id="17081-166">For example:</span></span>

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. <span data-ttu-id="17081-167">Načíst registr **klíče HKLM\Software** podklíčů z virtuálního pevného disku voláním `reg load`.</span><span class="sxs-lookup"><span data-stu-id="17081-167">Load the registry **HKLM\Software** subkey from the VHD by calling `reg load`.</span></span>

    ```
    reg load HKLM\Vhd E:\Windows\System32\Config\Software`
    ```

3. <span data-ttu-id="17081-168">Přejděte na **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\\***  pomocí poskytovatele prostředí PowerShell registru.</span><span class="sxs-lookup"><span data-stu-id="17081-168">Navigate to the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\\*** by using the PowerShell Registry provider.</span></span>

    ```powershell
    Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
    ```

4. <span data-ttu-id="17081-169">Změňte hodnotu `DSCAutomationHostEnabled` na hodnotu 0.</span><span class="sxs-lookup"><span data-stu-id="17081-169">Change the value of `DSCAutomationHostEnabled` to 0.</span></span>

    ```powershell
    Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
    ```

5. <span data-ttu-id="17081-170">Uvolnění registru tak, že spustíte následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="17081-170">Unload the registry by running the following commands:</span></span>

    ```powershell
    [gc]::Collect()
    reg unload HKLM\Vhd
    ```

## <a name="see-also"></a><span data-ttu-id="17081-171">Viz také</span><span class="sxs-lookup"><span data-stu-id="17081-171">See Also</span></span>

- [<span data-ttu-id="17081-172">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="17081-172">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="17081-173">Klíč registru DSCAutomationHostEnabled</span><span class="sxs-lookup"><span data-stu-id="17081-173">DSCAutomationHostEnabled registry key</span></span>](DSCAutomationHostEnabled.md)
- [<span data-ttu-id="17081-174">Konfigurace Local Configuration Manageru (LCM)</span><span class="sxs-lookup"><span data-stu-id="17081-174">Configuring the Local Configuration Manager (LCM)</span></span>](metaConfig.md)
- [<span data-ttu-id="17081-175">Nastavení webového serveru vyžádané replikace DSC</span><span class="sxs-lookup"><span data-stu-id="17081-175">Setting up a DSC web pull server</span></span>](pullServer.md)


---
title: Instalace PowerShellu Core ve Windows
description: Informace o instalaci Powershellu Core ve Windows
ms.date: 08/06/2018
ms.openlocfilehash: 7c109c7e1848af2349092c1e70fe4a7a25be54b8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403808"
---
# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="3b253-103">Instalace PowerShellu Core ve Windows</span><span class="sxs-lookup"><span data-stu-id="3b253-103">Installing PowerShell Core on Windows</span></span>

## <a name="msi"></a><span data-ttu-id="3b253-104">INSTALAČNÍ SLUŽBY MSI</span><span class="sxs-lookup"><span data-stu-id="3b253-104">MSI</span></span>

<span data-ttu-id="3b253-105">K instalaci prostředí PowerShell na Windows serveru nebo klienta Windows (funguje ve Windows 7 SP1, Server 2008 R2 a novější), stahování balíčku MSI náš GitHub [vydané verze][] stránky.</span><span class="sxs-lookup"><span data-stu-id="3b253-105">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from our GitHub [releases][] page.</span></span>

<span data-ttu-id="3b253-106">Souboru MSI, který vypadá takto – `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span><span class="sxs-lookup"><span data-stu-id="3b253-106">The MSI file looks like this - `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span></span>

<span data-ttu-id="3b253-107">Po stažení poklikejte na instalační program a postupujte podle zobrazených výzev.</span><span class="sxs-lookup"><span data-stu-id="3b253-107">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="3b253-108">Je zástupce v nabídce Start po instalaci.</span><span class="sxs-lookup"><span data-stu-id="3b253-108">There is a shortcut placed in the Start Menu upon installation.</span></span>

- <span data-ttu-id="3b253-109">Ve výchozím nastavení je balíček nainstalován do `$env:ProgramFiles\PowerShell\<version>`</span><span class="sxs-lookup"><span data-stu-id="3b253-109">By default the package is installed to `$env:ProgramFiles\PowerShell\<version>`</span></span>
- <span data-ttu-id="3b253-110">Můžete spustit prostředí PowerShell pomocí nabídky Start nebo `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span><span class="sxs-lookup"><span data-stu-id="3b253-110">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3b253-111">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="3b253-111">Prerequisites</span></span>

<span data-ttu-id="3b253-112">Pokud chcete povolit vzdálenou komunikaci prostředí PowerShell přes WSMan, nutné splnit následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="3b253-112">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

- <span data-ttu-id="3b253-113">Nainstalujte [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) na verze Windows starší než Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3b253-113">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span>
  <span data-ttu-id="3b253-114">Je dostupná prostřednictvím přímé stažení nebo aktualizace Windows.</span><span class="sxs-lookup"><span data-stu-id="3b253-114">It is available via direct download or Windows Update.</span></span>
  <span data-ttu-id="3b253-115">Opravit plně (včetně nepovinné balíčky), podporované systémy se již databázi máte nainstalované.</span><span class="sxs-lookup"><span data-stu-id="3b253-115">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
- <span data-ttu-id="3b253-116">Nainstalujte Windows 7 a Windows Server 2008 R2 Windows Management Frameworku (WMF) 4.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="3b253-116">Install the Windows Management Framework (WMF) 4.0 or newer on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="zip"></a><span data-ttu-id="3b253-117">PSČ</span><span class="sxs-lookup"><span data-stu-id="3b253-117">ZIP</span></span>

<span data-ttu-id="3b253-118">Chcete-li povolit pokročilé scénáře nasazení jsou k dispozici binární archivy ZIP prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b253-118">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span>
<span data-ttu-id="3b253-119">Třeba poznamenat, že při použití archivu ZIP, nezískáte kontroly požadavků jako balíček Instalační služby MSI.</span><span class="sxs-lookup"><span data-stu-id="3b253-119">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span>
<span data-ttu-id="3b253-120">Takže v pořadí pro vzdálenou komunikaci přes WSMan fungovala správně na verze Windows starší než Windows 10, je třeba Ujistěte se, že [požadavky](#prerequisites) jsou splněny.</span><span class="sxs-lookup"><span data-stu-id="3b253-120">So in order for remoting over WSMan to work properly on Windows versions prior to Windows 10, you need to make sure the [prerequisites](#prerequisites) are met.</span></span>

## <a name="deploying-on-windows-iot"></a><span data-ttu-id="3b253-121">Nasazení s využitím Windows IoT</span><span class="sxs-lookup"><span data-stu-id="3b253-121">Deploying on Windows IoT</span></span>

<span data-ttu-id="3b253-122">Windows IoT již obsahuje prostředí Windows PowerShell, který budeme používat k nasazení prostředí PowerShell Core 6.</span><span class="sxs-lookup"><span data-stu-id="3b253-122">Windows IoT already comes with Windows PowerShell which we will use to deploy PowerShell Core 6.</span></span>

1. <span data-ttu-id="3b253-123">Vytvoření `PSSession` cílové zařízení</span><span class="sxs-lookup"><span data-stu-id="3b253-123">Create `PSSession` to target device</span></span>

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. <span data-ttu-id="3b253-124">Zkopírujte balíček ZIP do zařízení</span><span class="sxs-lookup"><span data-stu-id="3b253-124">Copy the ZIP package to the device</span></span>

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-6.1.0-win-arm32.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. <span data-ttu-id="3b253-125">Připojte se k zařízení a rozbalte archiv</span><span class="sxs-lookup"><span data-stu-id="3b253-125">Connect to the device and expand the archive</span></span>

   ```powershell
   Enter-PSSession $s
   Set-Location u:\users\administrator\downloads
   Expand-Archive .\PowerShell-6.1.0-win-arm32.zip
   ```

4. <span data-ttu-id="3b253-126">Instalační program vzdálené komunikace prostředí PowerShell Core 6</span><span class="sxs-lookup"><span data-stu-id="3b253-126">Setup remoting to PowerShell Core 6</span></span>

   ```powershell
   Set-Location .\PowerShell-6.1.0-win-arm32
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. <span data-ttu-id="3b253-127">Připojení ke koncovému bodu PowerShell Core 6 na zařízení</span><span class="sxs-lookup"><span data-stu-id="3b253-127">Connect to PowerShell Core 6 endpoint on device</span></span>

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.6.1.0
   ```

## <a name="deploying-on-nano-server"></a><span data-ttu-id="3b253-128">Nasazení na Nano serveru</span><span class="sxs-lookup"><span data-stu-id="3b253-128">Deploying on Nano Server</span></span>

<span data-ttu-id="3b253-129">Tyto pokyny předpokládají, že verze Powershellu je již spuštěna na image Nano serveru a, je generováno pomocí [Image Builder pro Nano Server](/windows-server/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="3b253-129">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="3b253-130">Nano Server je "bezobslužný" operační systém.</span><span class="sxs-lookup"><span data-stu-id="3b253-130">Nano Server is a "headless" OS.</span></span> <span data-ttu-id="3b253-131">Binární soubory jádra můžete nasadit pomocí dvěma způsoby.</span><span class="sxs-lookup"><span data-stu-id="3b253-131">Core binaries can be deploy using two different methods.</span></span>

1. <span data-ttu-id="3b253-132">Offline – připojení disku VHD Nano serveru a rozbalte obsah souboru zip do zvoleného umístění v rámci připojené image.</span><span class="sxs-lookup"><span data-stu-id="3b253-132">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
2. <span data-ttu-id="3b253-133">Online – přeneste soubor zip po relaci Powershellu a rozbalte ho do zvoleného umístění.</span><span class="sxs-lookup"><span data-stu-id="3b253-133">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="3b253-134">V obou případech je nutné na verzi Windows 10 x64 ZIP balíčku a bude nutné ke spuštění příkazů v rámci instance prostředí PowerShell "Administrator".</span><span class="sxs-lookup"><span data-stu-id="3b253-134">In both cases, you will need the Windows 10 x64 ZIP release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="3b253-135">Offline nasazení Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="3b253-135">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="3b253-136">Použijte váš nástroj pro zipování Oblíbené dekomprimovat balíček do adresáře v rámci připojené image Nano serveru.</span><span class="sxs-lookup"><span data-stu-id="3b253-136">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
2. <span data-ttu-id="3b253-137">Odpojte image a spustit ho.</span><span class="sxs-lookup"><span data-stu-id="3b253-137">Unmount the image and boot it.</span></span>
3. <span data-ttu-id="3b253-138">Připojte se k instanci doručených zpráv Windows powershellu.</span><span class="sxs-lookup"><span data-stu-id="3b253-138">Connect to the inbox instance of Windows PowerShell.</span></span>
4. <span data-ttu-id="3b253-139">Postupujte podle pokynů a vytvořte koncový bod pomocí vzdálené komunikace ["Další instance technikou"](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="3b253-139">Follow the instructions to create a remoting endpoint using the ["another instance technique"](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="3b253-140">Online nasazení Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="3b253-140">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="3b253-141">Následující kroky vás provedou nasazení Powershellu Core ke spuštěné instanci Nano serveru a konfigurace jeho vzdálený koncový bod.</span><span class="sxs-lookup"><span data-stu-id="3b253-141">The following steps guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

- <span data-ttu-id="3b253-142">Připojte se k instanci doručených zpráv Windows powershellu</span><span class="sxs-lookup"><span data-stu-id="3b253-142">Connect to the inbox instance of Windows PowerShell</span></span>

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- <span data-ttu-id="3b253-143">Zkopírujte soubor na instanci Nano serveru</span><span class="sxs-lookup"><span data-stu-id="3b253-143">Copy the file to the Nano Server instance</span></span>

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- <span data-ttu-id="3b253-144">Do relace PSSession</span><span class="sxs-lookup"><span data-stu-id="3b253-144">Enter the session</span></span>

  ```powershell
  Enter-PSSession $session
  ```

- <span data-ttu-id="3b253-145">Extrahování souboru ZIP</span><span class="sxs-lookup"><span data-stu-id="3b253-145">Extract the ZIP file</span></span>

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- <span data-ttu-id="3b253-146">Pokud chcete vzdálené komunikace založená na službě WSMan, postupujte podle pokynů a vytvořte koncový bod vzdálené komunikace pomocí ["Další instance technikou"](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="3b253-146">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the ["another instance technique"](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="3b253-147">Pokyny k vytvoření koncového bodu vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="3b253-147">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="3b253-148">PowerShell Core podporuje protokol vzdálené komunikace prostředí PowerShell (PSRP) prostřednictvím služby WSMan a SSH.</span><span class="sxs-lookup"><span data-stu-id="3b253-148">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span>
<span data-ttu-id="3b253-149">Další informace viz:</span><span class="sxs-lookup"><span data-stu-id="3b253-149">For more information, see:</span></span>

- <span data-ttu-id="3b253-150">[SSH vzdálené komunikace v Powershellu Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="3b253-150">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="3b253-151">[Vzdálená komunikace WSMan v Powershellu Core][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="3b253-151">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="artifact-installation-instructions"></a><span data-ttu-id="3b253-152">Pokyny k instalaci artefaktu</span><span class="sxs-lookup"><span data-stu-id="3b253-152">Artifact Installation Instructions</span></span>

<span data-ttu-id="3b253-153">Publikujeme archiv s bity CoreCLR při každém sestavení CI s [AppVeyor][].</span><span class="sxs-lookup"><span data-stu-id="3b253-153">We publish an archive with CoreCLR bits on every CI build with [AppVeyor][].</span></span>

<span data-ttu-id="3b253-154">Instalace Powershellu Core v CoreCLR artefaktu:</span><span class="sxs-lookup"><span data-stu-id="3b253-154">To install PowerShell Core from the CoreCLR Artifact:</span></span>

1. <span data-ttu-id="3b253-155">Stáhněte si balíček ZIP z **artefakty** kartu konkrétním sestavení.</span><span class="sxs-lookup"><span data-stu-id="3b253-155">Download ZIP package from **artifacts** tab of the particular build.</span></span>
2. <span data-ttu-id="3b253-156">Soubor ZIP odblokovat: klikněte pravým tlačítkem v Průzkumníku souborů -> Vlastnosti -> Zkontrolujte použití pole -> odblokovat</span><span class="sxs-lookup"><span data-stu-id="3b253-156">Unblock ZIP file: right-click in File Explorer -> Properties -> check 'Unblock' box -> apply</span></span>
3. <span data-ttu-id="3b253-157">Extrahujte soubor zip do `bin` adresáře</span><span class="sxs-lookup"><span data-stu-id="3b253-157">Extract zip file to `bin` directory</span></span>
4. `./bin/pwsh.exe`

<!-- [download-center]: TODO -->

[vydané verze]: https://github.com/PowerShell/PowerShell/releases
[releases]: https://github.com/PowerShell/PowerShell/releases
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell

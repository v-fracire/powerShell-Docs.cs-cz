# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="8b0cd-101">Instalace PowerShellu Core ve Windows</span><span class="sxs-lookup"><span data-stu-id="8b0cd-101">Installing PowerShell Core on Windows</span></span>

## <a name="msi"></a><span data-ttu-id="8b0cd-102">INSTALAČNÍ SLUŽBY MSI</span><span class="sxs-lookup"><span data-stu-id="8b0cd-102">MSI</span></span>

<span data-ttu-id="8b0cd-103">K instalaci prostředí PowerShell na Windows serveru nebo klienta Windows (funguje ve Windows 7 SP1, Server 2008 R2 a novější), stahování balíčku MSI náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-103">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from our GitHub [releases][] page.</span></span>

<span data-ttu-id="8b0cd-104">Souboru MSI, který vypadá takto – `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span><span class="sxs-lookup"><span data-stu-id="8b0cd-104">The MSI file looks like this - `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span></span>

<span data-ttu-id="8b0cd-105">Po stažení poklikejte na instalační program a postupujte podle zobrazených výzev.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-105">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="8b0cd-106">Je zástupce v nabídce Start po instalaci.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-106">There is a shortcut placed in the Start Menu upon installation.</span></span>

- <span data-ttu-id="8b0cd-107">Ve výchozím nastavení je balíček nainstalován do `$env:ProgramFiles\PowerShell\<version>`</span><span class="sxs-lookup"><span data-stu-id="8b0cd-107">By default the package is installed to `$env:ProgramFiles\PowerShell\<version>`</span></span>
- <span data-ttu-id="8b0cd-108">Můžete spustit prostředí PowerShell pomocí nabídky Start nebo `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span><span class="sxs-lookup"><span data-stu-id="8b0cd-108">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8b0cd-109">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="8b0cd-109">Prerequisites</span></span>

<span data-ttu-id="8b0cd-110">Pokud chcete povolit vzdálenou komunikaci prostředí PowerShell přes WSMan, nutné splnit následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="8b0cd-110">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

- <span data-ttu-id="8b0cd-111">Nainstalujte [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) na verze Windows starší než Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-111">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span>
  <span data-ttu-id="8b0cd-112">Je dostupná prostřednictvím přímé stažení nebo aktualizace Windows.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-112">It is available via direct download or Windows Update.</span></span>
  <span data-ttu-id="8b0cd-113">Opravit plně (včetně nepovinné balíčky), podporované systémy se již databázi máte nainstalované.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-113">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
- <span data-ttu-id="8b0cd-114">Nainstalujte Windows 7 a Windows Server 2008 R2 Windows Management Frameworku (WMF) 4.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-114">Install the Windows Management Framework (WMF) 4.0 or newer on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="zip"></a><span data-ttu-id="8b0cd-115">PSČ</span><span class="sxs-lookup"><span data-stu-id="8b0cd-115">ZIP</span></span>

<span data-ttu-id="8b0cd-116">Chcete-li povolit pokročilé scénáře nasazení jsou k dispozici binární archivy ZIP prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-116">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span>
<span data-ttu-id="8b0cd-117">Třeba poznamenat, že při použití archivu ZIP, nezískáte kontroly požadavků jako balíček Instalační služby MSI.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-117">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span>
<span data-ttu-id="8b0cd-118">Takže v pořadí pro vzdálenou komunikaci přes WSMan fungovala správně na verze Windows starší než Windows 10, je třeba Ujistěte se, že [požadavky](#prerequisites) jsou splněny.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-118">So in order for remoting over WSMan to work properly on Windows versions prior to Windows 10, you need to make sure the [prerequisites](#prerequisites) are met.</span></span>

## <a name="deploying-on-windows-iot"></a><span data-ttu-id="8b0cd-119">Nasazení s využitím Windows IoT</span><span class="sxs-lookup"><span data-stu-id="8b0cd-119">Deploying on Windows IoT</span></span>

<span data-ttu-id="8b0cd-120">Windows IoT již obsahuje prostředí Windows PowerShell, který budeme používat k nasazení prostředí PowerShell Core 6.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-120">Windows IoT already comes with Windows PowerShell which we will use to deploy PowerShell Core 6.</span></span>

1. <span data-ttu-id="8b0cd-121">Vytvoření `PSSession` cílové zařízení</span><span class="sxs-lookup"><span data-stu-id="8b0cd-121">Create `PSSession` to target device</span></span>

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. <span data-ttu-id="8b0cd-122">Zkopírujte balíček ZIP do zařízení</span><span class="sxs-lookup"><span data-stu-id="8b0cd-122">Copy the ZIP package to the device</span></span>

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-6.0.2-win-arm32.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. <span data-ttu-id="8b0cd-123">Připojte se k zařízení a rozbalte archiv</span><span class="sxs-lookup"><span data-stu-id="8b0cd-123">Connect to the device and expand the archive</span></span>

   ```powershell
   Enter-PSSession $s
   cd u:\users\administrator\downloads
   Expand-Archive .\PowerShell-6.0.2-win-arm32.zip
   ```

4. <span data-ttu-id="8b0cd-124">Instalační program vzdálené komunikace prostředí PowerShell Core 6</span><span class="sxs-lookup"><span data-stu-id="8b0cd-124">Setup remoting to PowerShell Core 6</span></span>

   ```powershell
   cd .\PowerShell-6.0.2-win-arm32
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. <span data-ttu-id="8b0cd-125">Připojení ke koncovému bodu PowerShell Core 6 na zařízení</span><span class="sxs-lookup"><span data-stu-id="8b0cd-125">Connect to PowerShell Core 6 endpoint on device</span></span>

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.6.0.2
   ```

## <a name="deploying-on-nano-server"></a><span data-ttu-id="8b0cd-126">Nasazení na Nano serveru</span><span class="sxs-lookup"><span data-stu-id="8b0cd-126">Deploying on Nano Server</span></span>

<span data-ttu-id="8b0cd-127">Tyto pokyny předpokládají, že verze Powershellu je již spuštěna na image Nano serveru a, je generováno pomocí [Image Builder pro Nano Server](/windows-server/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="8b0cd-127">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="8b0cd-128">Nano Server je "bezobslužný" operační systém.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-128">Nano Server is a "headless" OS.</span></span> <span data-ttu-id="8b0cd-129">Binární soubory jádra můžete nasadit pomocí dvěma způsoby.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-129">Core binaries can be deploy using two different methods.</span></span>

1. <span data-ttu-id="8b0cd-130">Offline – připojení disku VHD Nano serveru a rozbalte obsah souboru zip do zvoleného umístění v rámci připojené image.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-130">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
2. <span data-ttu-id="8b0cd-131">Online – přeneste soubor zip po relaci Powershellu a rozbalte ho do zvoleného umístění.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-131">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="8b0cd-132">V obou případech je nutné na verzi Windows 10 x64 ZIP balíčku a bude nutné ke spuštění příkazů v rámci instance prostředí PowerShell "Administrator".</span><span class="sxs-lookup"><span data-stu-id="8b0cd-132">In both cases, you will need the Windows 10 x64 ZIP release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="8b0cd-133">Offline nasazení Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="8b0cd-133">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="8b0cd-134">Použijte váš nástroj pro zipování Oblíbené dekomprimovat balíček do adresáře v rámci připojené image Nano serveru.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-134">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
2. <span data-ttu-id="8b0cd-135">Odpojte image a spustit ho.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-135">Unmount the image and boot it.</span></span>
3. <span data-ttu-id="8b0cd-136">Připojte se k instanci doručených zpráv Windows powershellu.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-136">Connect to the inbox instance of Windows PowerShell.</span></span>
4. <span data-ttu-id="8b0cd-137">Postupujte podle pokynů a vytvořte koncový bod pomocí vzdálené komunikace ["Další instance technikou"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="8b0cd-137">Follow the instructions to create a remoting endpoint using the ["another instance technique"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="8b0cd-138">Online nasazení Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="8b0cd-138">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="8b0cd-139">Následující kroky vás provedou nasazení Powershellu Core ke spuštěné instanci Nano serveru a konfigurace jeho vzdálený koncový bod.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-139">The following steps guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

- <span data-ttu-id="8b0cd-140">Připojte se k instanci doručených zpráv Windows powershellu</span><span class="sxs-lookup"><span data-stu-id="8b0cd-140">Connect to the inbox instance of Windows PowerShell</span></span>

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- <span data-ttu-id="8b0cd-141">Zkopírujte soubor na instanci Nano serveru</span><span class="sxs-lookup"><span data-stu-id="8b0cd-141">Copy the file to the Nano Server instance</span></span>

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- <span data-ttu-id="8b0cd-142">Do relace PSSession</span><span class="sxs-lookup"><span data-stu-id="8b0cd-142">Enter the session</span></span>

  ```powershell
  Enter-PSSession $session
  ```

- <span data-ttu-id="8b0cd-143">Extrahování souboru ZIP</span><span class="sxs-lookup"><span data-stu-id="8b0cd-143">Extract the ZIP file</span></span>

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- <span data-ttu-id="8b0cd-144">Pokud chcete vzdálené komunikace založená na službě WSMan, postupujte podle pokynů a vytvořte koncový bod vzdálené komunikace pomocí ["Další instance technikou"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="8b0cd-144">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the ["another instance technique"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="8b0cd-145">Pokyny k vytvoření koncového bodu vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="8b0cd-145">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="8b0cd-146">PowerShell Core podporuje protokol vzdálené komunikace prostředí PowerShell (PSRP) prostřednictvím služby WSMan a SSH.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-146">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span>
<span data-ttu-id="8b0cd-147">Další informace viz:</span><span class="sxs-lookup"><span data-stu-id="8b0cd-147">For more information, see:</span></span>

- <span data-ttu-id="8b0cd-148">[SSH vzdálené komunikace v Powershellu Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="8b0cd-148">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="8b0cd-149">[Vzdálená komunikace WSMan v Powershellu Core][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="8b0cd-149">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="artifact-installation-instructions"></a><span data-ttu-id="8b0cd-150">Pokyny k instalaci artefaktu</span><span class="sxs-lookup"><span data-stu-id="8b0cd-150">Artifact Installation Instructions</span></span>

<span data-ttu-id="8b0cd-151">Publikujeme archiv s bity CoreCLR při každém sestavení CI s [AppVeyor][].</span><span class="sxs-lookup"><span data-stu-id="8b0cd-151">We publish an archive with CoreCLR bits on every CI build with [AppVeyor][].</span></span>

<span data-ttu-id="8b0cd-152">Instalace Powershellu Core v CoreCLR artefaktu:</span><span class="sxs-lookup"><span data-stu-id="8b0cd-152">To install PowerShell Core from the CoreCLR Artifact:</span></span>

1. <span data-ttu-id="8b0cd-153">Stáhněte si balíček ZIP z **artefakty** kartu konkrétním sestavení.</span><span class="sxs-lookup"><span data-stu-id="8b0cd-153">Download ZIP package from **artifacts** tab of the particular build.</span></span>
2. <span data-ttu-id="8b0cd-154">Soubor ZIP odblokovat: klikněte pravým tlačítkem v Průzkumníku souborů -> Vlastnosti -> Zkontrolujte použití pole -> odblokovat</span><span class="sxs-lookup"><span data-stu-id="8b0cd-154">Unblock ZIP file: right-click in File Explorer -> Properties -> check 'Unblock' box -> apply</span></span>
3. <span data-ttu-id="8b0cd-155">Extrahujte soubor zip do `bin` adresáře</span><span class="sxs-lookup"><span data-stu-id="8b0cd-155">Extract zip file to `bin` directory</span></span>
4. `./bin/pwsh.exe`

<!-- [download-center]: TODO -->

[uvolní]: https://github.com/PowerShell/PowerShell/releases
[releases]: https://github.com/PowerShell/PowerShell/releases
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell

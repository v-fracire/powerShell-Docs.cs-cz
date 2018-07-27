
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="36842-101">Vzdálená komunikace PowerShellu přes SSH</span><span class="sxs-lookup"><span data-stu-id="36842-101">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="36842-102">Přehled</span><span class="sxs-lookup"><span data-stu-id="36842-102">Overview</span></span>

<span data-ttu-id="36842-103">Vzdálenou komunikaci prostředí PowerShell pro vyjednávání připojení a přenos dat obvykle používá WinRM.</span><span class="sxs-lookup"><span data-stu-id="36842-103">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span> <span data-ttu-id="36842-104">SSH byla vybrána pro tuto implementaci vzdálenou komunikaci, protože je teď dostupná pro platformy Linux i Windows a umožňuje true multiplatformní vzdálenou komunikaci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36842-104">SSH was chosen for this remoting implementation since it is now available for both Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span> <span data-ttu-id="36842-105">Služba WinRM však také poskytuje robustní model hostingu pro vzdálené relace prostředí PowerShell, které tato implementace zatím nenabízí.</span><span class="sxs-lookup"><span data-stu-id="36842-105">However, WinRM also provides a robust hosting model for PowerShell remote sessions which this implementation does not yet do.</span></span> <span data-ttu-id="36842-106">A to znamená, že vzdálený koncový bod konfigurace prostředí PowerShell a JEA (Just Enough Administration) se ještě nepodporuje v této implementaci.</span><span class="sxs-lookup"><span data-stu-id="36842-106">And this means that PowerShell remote endpoint configuration and JEA (Just Enough Administration) is not yet supported in this implementation.</span></span>

<span data-ttu-id="36842-107">PowerShell SSH remoting umožňuje provádět základní vzdálené komunikace Powershellu relace mezi počítače s Windows a Linuxem.</span><span class="sxs-lookup"><span data-stu-id="36842-107">PowerShell SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span> <span data-ttu-id="36842-108">To se provádí tak, že vytvoříte Powershellu hostující proces na cílovém počítači jako podsystému SSH.</span><span class="sxs-lookup"><span data-stu-id="36842-108">This is done by creating a PowerShell hosting process on the target machine as an SSH subsystem.</span></span> <span data-ttu-id="36842-109">Nakonec to bude změněno na obecnější hostování model podobný Princip WinRM, aby bylo možné podporovat konfiguraci koncového bodu a JEA.</span><span class="sxs-lookup"><span data-stu-id="36842-109">Eventually this will be changed to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="36842-110">`New-PSSession`, `Enter-PSSession` a `Invoke-Command` tyto rutiny teď mají nový parametr nastavte pro usnadnění tohoto nového připojení vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="36842-110">The `New-PSSession`, `Enter-PSSession` and `Invoke-Command` cmdlets now have a new parameter set to facilitate this new remoting connection</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="36842-111">Tato nová sada parametrů se pravděpodobně změní, ale teď umožňuje vytvářet SSH PSSessions, že budete pracovat z příkazového řádku nebo vyvolat příkazy a skripty na.</span><span class="sxs-lookup"><span data-stu-id="36842-111">This new parameter set will likely change but for now allows you to create SSH PSSessions that you can interact with from the command line or invoke commands and scripts on.</span></span> <span data-ttu-id="36842-112">Zadejte cílový počítač s parametrem názvu hostitele a zadejte uživatelské jméno s uživatelským jménem.</span><span class="sxs-lookup"><span data-stu-id="36842-112">You specify the target machine with the HostName parameter and provide the user name with UserName.</span></span> <span data-ttu-id="36842-113">Při interaktivním spuštění rutiny příkazového řádku Powershellu se výzva k zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="36842-113">When running the cmdlets interactively at the PowerShell command line you will be prompted for a password.</span></span> <span data-ttu-id="36842-114">Ale máte také možnost použít ověřování pomocí klíče SSH a zadejte cestu souboru s privátním klíčem s parametrem KeyFilePath.</span><span class="sxs-lookup"><span data-stu-id="36842-114">But you also have the option to use SSH key authentication and provide a private key file path with the KeyFilePath parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="36842-115">Informace o obecných nastavení</span><span class="sxs-lookup"><span data-stu-id="36842-115">General setup information</span></span>

<span data-ttu-id="36842-116">SSH je musí být nainstalovaný na všech počítačích.</span><span class="sxs-lookup"><span data-stu-id="36842-116">SSH is required to be installed on all machines.</span></span> <span data-ttu-id="36842-117">Měli byste nainstalovat klientské (`ssh.exe`) a serveru (`sshd.exe`) tak, že můžete experimentovat s vzdálené komunikace do a z počítače.</span><span class="sxs-lookup"><span data-stu-id="36842-117">You should install both client (`ssh.exe`) and server (`sshd.exe`) so that you can experiment with remoting to and from the machines.</span></span> <span data-ttu-id="36842-118">Pro Windows je potřeba nainstalovat [Win32 OpenSSH z Githubu](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="36842-118">For Windows you will need to install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="36842-119">Pro Linux je potřeba nainstalovat SSH (včetně server sshd) pro vaši platformu.</span><span class="sxs-lookup"><span data-stu-id="36842-119">For Linux you will need to install SSH (including sshd server) appropriate to your platform.</span></span> <span data-ttu-id="36842-120">Budete také potřebovat poslední sestavení prostředí PowerShell nebo balíček z Githubu s funkcí vzdálenou komunikaci SSH.</span><span class="sxs-lookup"><span data-stu-id="36842-120">You will also need a recent PowerShell build or package from GitHub having the SSH remoting feature.</span></span>
<span data-ttu-id="36842-121">Subsystémy SSH se používá k navázání Powershellu procesu ve vzdáleném počítači a SSH server bude potřeba nakonfigurovat pro daný.</span><span class="sxs-lookup"><span data-stu-id="36842-121">SSH subsystems is used to establish a PowerShell process on the remote machine and the SSH server will need to be configured for that.</span></span> <span data-ttu-id="36842-122">Kromě toho je potřeba povolit ověřování pomocí hesla a volitelně klíče ověřování.</span><span class="sxs-lookup"><span data-stu-id="36842-122">In addition you will need to enable password authentication and optionally key based authentication.</span></span>

## <a name="setup-on-windows-machine"></a><span data-ttu-id="36842-123">Instalační program na počítači s Windows</span><span class="sxs-lookup"><span data-stu-id="36842-123">Setup on Windows Machine</span></span>

1. <span data-ttu-id="36842-124">Nainstalujte nejnovější verzi [PowerShell Core pro Windows]</span><span class="sxs-lookup"><span data-stu-id="36842-124">Install the latest version of [PowerShell Core for Windows]</span></span>

   - <span data-ttu-id="36842-125">Poznáte, že jestli bylo Podpora vzdálené komunikace SSH zobrazením parametr nastaví pro `New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="36842-125">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="36842-126">Nainstalujte nejnovější sestavení [Win32 OpenSSH] z Githubu pomocí instrukcí [instalace]</span><span class="sxs-lookup"><span data-stu-id="36842-126">Install the latest [Win32 OpenSSH] build from GitHub using the [installation] instructions</span></span>
3. <span data-ttu-id="36842-127">Úprava souboru sshd_config v umístění, kam jste nainstalovali Win32 OpenSSH</span><span class="sxs-lookup"><span data-stu-id="36842-127">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>

   - <span data-ttu-id="36842-128">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="36842-128">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > <span data-ttu-id="36842-129">OpenSSH pro Windows, který brání práce v cestách spustitelný subsystému prostorů je chyba.</span><span class="sxs-lookup"><span data-stu-id="36842-129">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span>
     > <span data-ttu-id="36842-130">Zobrazit [tento problém na Githubu pro další informace o](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="36842-130">See [this issue on GitHub for more information](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

     <span data-ttu-id="36842-131">Jedním z řešení je vytvořte symlink do instalačního adresáře prostředí Powershell, který neobsahuje mezery:</span><span class="sxs-lookup"><span data-stu-id="36842-131">One solution is to create a symlink to the Powershell installation directory that does not contain spaces:</span></span>

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
     ```

     <span data-ttu-id="36842-132">a zadejte ho v subsystému:</span><span class="sxs-lookup"><span data-stu-id="36842-132">and then enter it in the subsystem:</span></span>

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="36842-133">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="36842-133">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

4. <span data-ttu-id="36842-134">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="36842-134">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="36842-135">Přidat cestu, kde je nainstalován OpenSSH na vaše proměnné Env cesta</span><span class="sxs-lookup"><span data-stu-id="36842-135">Add the path where OpenSSH is installed to your Path Env Variable</span></span>

   - <span data-ttu-id="36842-136">To by měla být podle `C:\Program Files\OpenSSH\`</span><span class="sxs-lookup"><span data-stu-id="36842-136">This should be along the lines of `C:\Program Files\OpenSSH\`</span></span>
   - <span data-ttu-id="36842-137">To umožňuje ssh.exe nalezen</span><span class="sxs-lookup"><span data-stu-id="36842-137">This allows for the ssh.exe to be found</span></span>

## <a name="setup-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="36842-138">Instalační program na počítači s Linuxem (Ubuntu 14.04)</span><span class="sxs-lookup"><span data-stu-id="36842-138">Setup on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="36842-139">Nainstalujte nejnovější sestavení [PowerShell Core pro Linux] z Githubu</span><span class="sxs-lookup"><span data-stu-id="36842-139">Install the latest [PowerShell Core for Linux] build from GitHub</span></span>
2. <span data-ttu-id="36842-140">Instalace [Ubuntu SSH] podle potřeby</span><span class="sxs-lookup"><span data-stu-id="36842-140">Install [Ubuntu SSH] as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="36842-141">Úprava souboru sshd_config na umístění /etc/ssh</span><span class="sxs-lookup"><span data-stu-id="36842-141">Edit the sshd_config file at location /etc/ssh</span></span>

   - <span data-ttu-id="36842-142">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="36842-142">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="36842-143">Přidejte položku subsystém PowerShell</span><span class="sxs-lookup"><span data-stu-id="36842-143">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="36842-144">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="36842-144">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="36842-145">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="36842-145">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="setup-on-macos-machine"></a><span data-ttu-id="36842-146">Instalace na počítači s MacOS</span><span class="sxs-lookup"><span data-stu-id="36842-146">Setup on MacOS Machine</span></span>

1. <span data-ttu-id="36842-147">Nainstalujte nejnovější sestavení [PowerShell Core pro MacOS]</span><span class="sxs-lookup"><span data-stu-id="36842-147">Install the latest [PowerShell Core for MacOS] build</span></span>

   - <span data-ttu-id="36842-148">Ujistěte se, že je povolená Vzdálená SSH pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="36842-148">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="36842-149">Otevřít `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="36842-149">Open `System Preferences`</span></span>
     - <span data-ttu-id="36842-150">Klikněte na `Sharing`</span><span class="sxs-lookup"><span data-stu-id="36842-150">Click on `Sharing`</span></span>
     - <span data-ttu-id="36842-151">Zkontrolujte `Remote Login` – by mělo být uvedeno `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="36842-151">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="36842-152">Povolit přístup k příslušným uživatelům</span><span class="sxs-lookup"><span data-stu-id="36842-152">Allow access to appropriate users</span></span>

2. <span data-ttu-id="36842-153">Upravit `sshd_config` soubor na místě `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="36842-153">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>

   - <span data-ttu-id="36842-154">Pomocí oblíbeného editoru nebo</span><span class="sxs-lookup"><span data-stu-id="36842-154">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="36842-155">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="36842-155">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="36842-156">Přidejte položku subsystém PowerShell</span><span class="sxs-lookup"><span data-stu-id="36842-156">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="36842-157">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="36842-157">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="36842-158">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="36842-158">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="powershell-remoting-example"></a><span data-ttu-id="36842-159">Příklad vzdálené komunikace Powershellu</span><span class="sxs-lookup"><span data-stu-id="36842-159">PowerShell Remoting Example</span></span>

<span data-ttu-id="36842-160">Nejjednodušší způsob otestování vzdálené komunikace je prostě to zkuste na jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="36842-160">The easiest way to test remoting is to just try it on a single machine.</span></span> <span data-ttu-id="36842-161">Tady můžu se vytvořit relaci vzdálené zpět do stejného počítače v systému Linux box.</span><span class="sxs-lookup"><span data-stu-id="36842-161">Here I will create a remote session back to the same machine on a Linux box.</span></span> <span data-ttu-id="36842-162">Všimněte si, že používám rutin Powershellu z příkazového řádku, proto jsme zobrazovat výzvy z SSH s výzvou k ověření hostitelského počítače, stejně jako zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="36842-162">Notice that I am using PowerShell cmdlets from a command prompt so we see prompts from SSH asking to verify the host computer as well as password prompts.</span></span> <span data-ttu-id="36842-163">Můžete provést totéž v počítači Windows k zajištění, že existuje funguje vzdálené komunikace a pak vzdálené mezi počítači jednoduchou změnou názvu hostitele.</span><span class="sxs-lookup"><span data-stu-id="36842-163">You can do the same thing on a Windows machine to ensure remoting is working there and then remote between machines by simply changing the host name.</span></span>

```powershell
#
# Linux to Linux
#
$session = New-PSSession -HostName UbuntuVM1 -UserName TestUser
```

```output
The authenticity of host 'UbuntuVM1 (9.129.17.107)' cannot be established.
ECDSA key fingerprint is SHA256:2kCbnhT2dUE6WCGgVJ8Hyfu1z2wE4lifaJXLO7QJy0Y.
Are you sure you want to continue connecting (yes/no)?
TestUser@UbuntuVM1s password:
```

```powershell
$session
```

```output
 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            UbuntuVM1       RemoteMachine   Opened        DefaultShell             Available
```

```powershell
Enter-PSSession $session
```

```output
[UbuntuVM1]: PS /home/TestUser> uname -a
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~14.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

[UbuntuVM1]: PS /home/TestUser> Exit-PSSession
```

```powershell
Invoke-Command $session -ScriptBlock { Get-Process powershell }
```

```output
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName                    PSComputerName
-------  ------    -----      -----     ------     --  -- -----------                    --------------
      0       0        0         19       3.23  10635 635 powershell                     UbuntuVM1
      0       0        0         21       4.92  11033 017 powershell                     UbuntuVM1
      0       0        0         20       3.07  11076 076 powershell                     UbuntuVM1
```

```powershell
#
# Linux to Windows
#
Enter-PSSession -HostName WinVM1 -UserName PTestName
```

```output
PTestName@WinVM1s password:
```

```powershell
[WinVM1]: PS C:\Users\PTestName\Documents> cmd /c ver
```

```output
Microsoft Windows [Version 10.0.10586]
```

```powershell
#
# Windows to Windows
#
C:\Users\PSUser\Documents>pwsh.exe
```

```output
PowerShell
Copyright (c) Microsoft Corporation. All rights reserved.
```

```powershell
$session = New-PSSession -HostName WinVM2 -UserName PSRemoteUser
```

```output
The authenticity of host 'WinVM2 (10.13.37.3)' can't be established.
ECDSA key fingerprint is SHA256:kSU6slAROyQVMEynVIXAdxSiZpwDBigpAF/TXjjWjmw.
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'WinVM2,10.13.37.3' (ECDSA) to the list of known hosts.
PSRemoteUser@WinVM2's password:
```

```powershell
$session
```

```output
 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            WinVM2          RemoteMachine   Opened        DefaultShell             Available
```

```powershell
Enter-PSSession -Session $session
```

```output
[WinVM2]: PS C:\Users\PSRemoteUser\Documents> $PSVersionTable

Name                           Value
----                           -----
PSEdition                      Core
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
SerializationVersion           1.1.0.1
BuildVersion                   3.0.0.0
CLRVersion
PSVersion                      6.0.0-alpha
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
GitCommitId                    v6.0.0-alpha.17


[WinVM2]: PS C:\Users\PSRemoteUser\Documents>
```

### <a name="known-issues"></a><span data-ttu-id="36842-164">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="36842-164">Known Issues</span></span>

<span data-ttu-id="36842-165">Příkaz sudo nefunguje v relaci vzdálené k počítači s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="36842-165">The sudo command does not work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="36842-166">Viz také</span><span class="sxs-lookup"><span data-stu-id="36842-166">See Also</span></span>

[<span data-ttu-id="36842-167">PowerShell Core pro Windows</span><span class="sxs-lookup"><span data-stu-id="36842-167">PowerShell Core for Windows</span></span>](../setup/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="36842-168">PowerShell Core pro Linux</span><span class="sxs-lookup"><span data-stu-id="36842-168">PowerShell Core for Linux</span></span>](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="36842-169">PowerShell Core pro MacOS</span><span class="sxs-lookup"><span data-stu-id="36842-169">PowerShell Core for MacOS</span></span>](../setup/installing-powershell-core-on-macos.md)

[<span data-ttu-id="36842-170">Win32 OpenSSH</span><span class="sxs-lookup"><span data-stu-id="36842-170">Win32 OpenSSH</span></span>](https://github.com/PowerShell/Win32-OpenSSH/releases)

[<span data-ttu-id="36842-171">instalace</span><span class="sxs-lookup"><span data-stu-id="36842-171">installation</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[<span data-ttu-id="36842-172">SSH se systémem Ubuntu</span><span class="sxs-lookup"><span data-stu-id="36842-172">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
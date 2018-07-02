# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="62a19-101">Vzdálená komunikace PowerShellu přes SSH</span><span class="sxs-lookup"><span data-stu-id="62a19-101">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="62a19-102">Přehled</span><span class="sxs-lookup"><span data-stu-id="62a19-102">Overview</span></span>

<span data-ttu-id="62a19-103">Vzdálená komunikace prostředí PowerShell normálně používá WinRM pro vyjednávání připojení a přenosu dat.</span><span class="sxs-lookup"><span data-stu-id="62a19-103">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span>
<span data-ttu-id="62a19-104">SSH jste vybrali pro tuto implementaci vzdálenou komunikaci, protože je teď dostupná pro platformy Linux a Windows a umožňuje true vzdálenou komunikaci prostředí PowerShell s více platformami.</span><span class="sxs-lookup"><span data-stu-id="62a19-104">SSH was chosen for this remoting implementation since it is now available for both Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>
<span data-ttu-id="62a19-105">WinRM však také poskytuje robustní hostování model pro vzdálené relace prostředí PowerShell, které tato implementace ještě neprovádí.</span><span class="sxs-lookup"><span data-stu-id="62a19-105">However, WinRM also provides a robust hosting model for PowerShell remote sessions which this implementation does not yet do.</span></span>
<span data-ttu-id="62a19-106">A to znamená, že JEA (právě dostatečně správy) a konfigurace prostředí PowerShell vzdálený koncový bod není dosud podporováno v této implementaci.</span><span class="sxs-lookup"><span data-stu-id="62a19-106">And this means that PowerShell remote endpoint configuration and JEA (Just Enough Administration) is not yet supported in this implementation.</span></span>

<span data-ttu-id="62a19-107">Remoting SSH prostředí PowerShell vám umožňuje provést základní vzdálenou komunikaci prostředí PowerShell relací mezi počítači Windows a Linux.</span><span class="sxs-lookup"><span data-stu-id="62a19-107">PowerShell SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span>
<span data-ttu-id="62a19-108">Děje se tak, že vytvoříte proces v cílovém počítači jako podsystému SSH hostování prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62a19-108">This is done by creating a PowerShell hosting process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="62a19-109">Nakonec to bude změněno na další obecné podobný Princip WinRM za účelem podpory konfigurace koncového bodu a JEA hostování modelu.</span><span class="sxs-lookup"><span data-stu-id="62a19-109">Eventually this will be changed to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="62a19-110">Rutiny New-PSSession, Enter-PSSession a Invoke-Command Teď máte nový parametr nastavit pro usnadnění tohoto nového připojení vzdálené komunikace</span><span class="sxs-lookup"><span data-stu-id="62a19-110">The New-PSSession, Enter-PSSession and Invoke-Command cmdlets now have a new parameter set to facilitate this new remoting connection</span></span>

```powershell
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="62a19-111">Tuto novou sadu parametrů pravděpodobně se změní, ale teď umožňuje vytvářet SSH PSSessions můžete pracovat s z příkazového řádku nebo vyvolání na příkazy a skripty.</span><span class="sxs-lookup"><span data-stu-id="62a19-111">This new parameter set will likely change but for now allows you to create SSH PSSessions that you can interact with from the command line or invoke commands and scripts on.</span></span>
<span data-ttu-id="62a19-112">Zadejte cílový počítač s parametrem název hostitele a zadejte uživatelské jméno s uživatelským jménem.</span><span class="sxs-lookup"><span data-stu-id="62a19-112">You specify the target machine with the HostName parameter and provide the user name with UserName.</span></span>
<span data-ttu-id="62a19-113">Při interaktivním spuštění rutiny na příkazovém řádku prostředí PowerShell vás vyzve k zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="62a19-113">When running the cmdlets interactively at the PowerShell command line you will be prompted for a password.</span></span>
<span data-ttu-id="62a19-114">Ale máte také možnost použít ověření pomocí klíče SSH a zadejte cestu soubor privátního klíče s parametrem KeyFilePath.</span><span class="sxs-lookup"><span data-stu-id="62a19-114">But you also have the option to use SSH key authentication and provide a private key file path with the KeyFilePath parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="62a19-115">Informace o obecné nastavení</span><span class="sxs-lookup"><span data-stu-id="62a19-115">General setup information</span></span>

<span data-ttu-id="62a19-116">SSH je musí být nainstalovaný na všech počítačích.</span><span class="sxs-lookup"><span data-stu-id="62a19-116">SSH is required to be installed on all machines.</span></span>
<span data-ttu-id="62a19-117">Musíte nainstalovat klienta (ssh.exe) a serveru (sshd.exe) tak, aby můžete experimentovat s vzdálené komunikace do a z počítačů.</span><span class="sxs-lookup"><span data-stu-id="62a19-117">You should install both client (ssh.exe) and server (sshd.exe) so that you can experiment with remoting to and from the machines.</span></span>
<span data-ttu-id="62a19-118">Pro systém Windows je potřeba nainstalovat [OpenSSH Win32 z Githubu](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="62a19-118">For Windows you will need to install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="62a19-119">Pro Linux, musíte nainstalovat SSH (včetně sshd server) vhodné pro vaši platformu.</span><span class="sxs-lookup"><span data-stu-id="62a19-119">For Linux you will need to install SSH (including sshd server) appropriate to your platform.</span></span>
<span data-ttu-id="62a19-120">Budete také potřebovat poslední sestavení prostředí PowerShell nebo balíček z Githubu s funkci Vzdálená komunikace SSH.</span><span class="sxs-lookup"><span data-stu-id="62a19-120">You will also need a recent PowerShell build or package from GitHub having the SSH remoting feature.</span></span>
<span data-ttu-id="62a19-121">Subsystémy SSH se používá k zahájení procesu prostředí PowerShell ve vzdáleném počítači a serverem SSH bude nutné je nakonfigurovat pro tento.</span><span class="sxs-lookup"><span data-stu-id="62a19-121">SSH subsystems is used to establish a PowerShell process on the remote machine and the SSH server will need to be configured for that.</span></span>
<span data-ttu-id="62a19-122">Kromě toho musíte povolit ověřování hesla a volitelně klíče ověřování založené na.</span><span class="sxs-lookup"><span data-stu-id="62a19-122">In addition you will need to enable password authentication and optionally key based authentication.</span></span>

## <a name="setup-on-windows-machine"></a><span data-ttu-id="62a19-123">Instalace na počítač s Windows</span><span class="sxs-lookup"><span data-stu-id="62a19-123">Setup on Windows Machine</span></span>

1. <span data-ttu-id="62a19-124">Nainstalujte nejnovější verzi [jádra prostředí PowerShell pro systém Windows]</span><span class="sxs-lookup"><span data-stu-id="62a19-124">Install the latest version of [PowerShell Core for Windows]</span></span>
    - <span data-ttu-id="62a19-125">Můžete zadat, že pokud má dokonalejší podpora SSH prohlížením Nastaví parametr pro New-PSSession</span><span class="sxs-lookup"><span data-stu-id="62a19-125">You can tell if it has the SSH remoting support by looking at the parameter sets for New-PSSession</span></span>

    ```powershell
    PS> Get-Command New-PSSession -syntax
    New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
    ```

1. <span data-ttu-id="62a19-126">Nainstalujte si nejnovější verzi [Win32 OpenSSH] sestavení z Githubu pomocí [instalace] pokyny</span><span class="sxs-lookup"><span data-stu-id="62a19-126">Install the latest [Win32 OpenSSH] build from GitHub using the [installation] instructions</span></span>
1. <span data-ttu-id="62a19-127">Upravte soubor sshd_config v umístění, kam jste nainstalovali Win32 OpenSSH</span><span class="sxs-lookup"><span data-stu-id="62a19-127">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>
    - <span data-ttu-id="62a19-128">Ujistěte se, že je povolené ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="62a19-128">Make sure password authentication is enabled</span></span>

    ```
    PasswordAuthentication yes
    ```

    - <span data-ttu-id="62a19-129">Přidat položku subsystém prostředí PowerShell, nahraďte `c:/program files/powershell/6.0.0/pwsh.exe` správná cesta na verzi, kterou chcete použít</span><span class="sxs-lookup"><span data-stu-id="62a19-129">Add a PowerShell subsystem entry, replace `c:/program files/powershell/6.0.0/pwsh.exe` with the correct path to the version you want to use</span></span>

    ```
    Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
    ```
    
    > [!NOTE]
    <span data-ttu-id="62a19-130">V OpenSSH pro Windows, který brání prostory v práci v subsystému spustitelné cesty je chyba.</span><span class="sxs-lookup"><span data-stu-id="62a19-130">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span>
    <span data-ttu-id="62a19-131">V tématu [potíže na Githubu informace](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="62a19-131">See [this issue on GitHub for more information](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>
    
    <span data-ttu-id="62a19-132">Jedno řešení je vytvořit symlink do instalačního adresáře nástroje Powershell, který neobsahuje mezery:</span><span class="sxs-lookup"><span data-stu-id="62a19-132">One solution is to create a symlink to the Powershell installation directory that does not contain spaces:</span></span>
    
    ```powershell
    mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
    ```

    <span data-ttu-id="62a19-133">a zadejte ho v subsystému:</span><span class="sxs-lookup"><span data-stu-id="62a19-133">and then enter it in the subsystem:</span></span>
 
    ```
    Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
    ```

    - <span data-ttu-id="62a19-134">Volitelně můžete povolit ověření pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="62a19-134">Optionally enable key authentication</span></span>

    ```
    PubkeyAuthentication yes
    ```

1. <span data-ttu-id="62a19-135">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="62a19-135">Restart the sshd service</span></span>

    ```powershell
    Restart-Service sshd
    ```

1. <span data-ttu-id="62a19-136">Přidat cestu, kde je nainstalován OpenSSH pro vaši cestu Env proměnné</span><span class="sxs-lookup"><span data-stu-id="62a19-136">Add the path where OpenSSH is installed to your Path Env Variable</span></span>
    - <span data-ttu-id="62a19-137">Měl by být spolu čar `C:\Program Files\OpenSSH\`</span><span class="sxs-lookup"><span data-stu-id="62a19-137">This should be along the lines of `C:\Program Files\OpenSSH\`</span></span>
    - <span data-ttu-id="62a19-138">To umožňuje, aby ssh.exe chcete vyhledat</span><span class="sxs-lookup"><span data-stu-id="62a19-138">This allows for the ssh.exe to be found</span></span>

## <a name="setup-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="62a19-139">Instalační program na počítači Linux (Ubuntu 14.04)</span><span class="sxs-lookup"><span data-stu-id="62a19-139">Setup on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="62a19-140">Nainstalujte si nejnovější verzi [základní prostředí PowerShell pro Linux] sestavení z Githubu</span><span class="sxs-lookup"><span data-stu-id="62a19-140">Install the latest [PowerShell Core for Linux] build from GitHub</span></span>
1. <span data-ttu-id="62a19-141">Nainstalujte [Ubuntu SSH] podle potřeby</span><span class="sxs-lookup"><span data-stu-id="62a19-141">Install [Ubuntu SSH] as needed</span></span>

    ```bash
    sudo apt install openssh-client
    sudo apt install openssh-server
    ```

1. <span data-ttu-id="62a19-142">Upravte soubor sshd_config v umístění /etc/ssh</span><span class="sxs-lookup"><span data-stu-id="62a19-142">Edit the sshd_config file at location /etc/ssh</span></span>
    - <span data-ttu-id="62a19-143">Ujistěte se, že je povolené ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="62a19-143">Make sure password authentication is enabled</span></span>

    ```
    PasswordAuthentication yes
    ```

    - <span data-ttu-id="62a19-144">Přidat položku subsystém prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="62a19-144">Add a PowerShell subsystem entry</span></span>

    ```
    Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
    ```

    - <span data-ttu-id="62a19-145">Volitelně můžete povolit ověření pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="62a19-145">Optionally enable key authentication</span></span>

    ```
    PubkeyAuthentication yes
    ```

1. <span data-ttu-id="62a19-146">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="62a19-146">Restart the sshd service</span></span>

    ```bash
    sudo service sshd restart
    ```

## <a name="setup-on-macos-machine"></a><span data-ttu-id="62a19-147">Instalační program na počítači systému MacOS</span><span class="sxs-lookup"><span data-stu-id="62a19-147">Setup on MacOS Machine</span></span>

1. <span data-ttu-id="62a19-148">Nainstalujte si nejnovější verzi [jádro prostředí PowerShell pro systému MacOS] sestavení</span><span class="sxs-lookup"><span data-stu-id="62a19-148">Install the latest [PowerShell Core for MacOS] build</span></span>
    - <span data-ttu-id="62a19-149">Zkontrolujte, zda že je povolena vzdálená SSH komunikace pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="62a19-149">Make sure SSH Remoting is enabled by following these steps:</span></span>
      - <span data-ttu-id="62a19-150">Otevřete `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="62a19-150">Open `System Preferences`</span></span>
      - <span data-ttu-id="62a19-151">Klikněte na `Sharing`</span><span class="sxs-lookup"><span data-stu-id="62a19-151">Click on `Sharing`</span></span>
      - <span data-ttu-id="62a19-152">Zkontrolujte `Remote Login` – by mělo být uvedeno `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="62a19-152">Check `Remote Login` - Should say `Remote Login: On`</span></span>
      - <span data-ttu-id="62a19-153">Povolit přístup k příslušné uživatele</span><span class="sxs-lookup"><span data-stu-id="62a19-153">Allow access to appropriate users</span></span>
1. <span data-ttu-id="62a19-154">Upravit `sshd_config` soubor v umístění `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="62a19-154">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>
    - <span data-ttu-id="62a19-155">Pomocí oblíbeného editoru nebo</span><span class="sxs-lookup"><span data-stu-id="62a19-155">Use your favorite editor or</span></span>

    ```bash
    sudo nano /private/etc/ssh/sshd_config
    ```

    - <span data-ttu-id="62a19-156">Ujistěte se, že je povolené ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="62a19-156">Make sure password authentication is enabled</span></span>

    ```
    PasswordAuthentication yes
    ```

    - <span data-ttu-id="62a19-157">Přidat položku subsystém prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="62a19-157">Add a PowerShell subsystem entry</span></span>

    ```
    Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
    ```

    - <span data-ttu-id="62a19-158">Volitelně můžete povolit ověření pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="62a19-158">Optionally enable key authentication</span></span>

    ```
    PubkeyAuthentication yes
    ```

1. <span data-ttu-id="62a19-159">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="62a19-159">Restart the sshd service</span></span>

    ```bash
    sudo launchctl stop com.openssh.sshd
    sudo launchctl start com.openssh.sshd
    ```

## <a name="powershell-remoting-example"></a><span data-ttu-id="62a19-160">Příklad vzdálenou komunikaci prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="62a19-160">PowerShell Remoting Example</span></span>

<span data-ttu-id="62a19-161">Nejjednodušší způsob, jak otestovat vzdálené komunikace je právě vyzkoušejte si to na jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="62a19-161">The easiest way to test remoting is to just try it on a single machine.</span></span>
<span data-ttu-id="62a19-162">Tady na pole Linux vytvořím vzdálenou relaci zpátky do stejného počítače.</span><span class="sxs-lookup"><span data-stu-id="62a19-162">Here I will create a remote session back to the same machine on a Linux box.</span></span>
<span data-ttu-id="62a19-163">Všimněte si, že je používána rutiny prostředí PowerShell z příkazového řádku, vidíme výzvy ze SSH s dotazem, chcete-li ověřit na hostitelském počítači a také na zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="62a19-163">Notice that I am using PowerShell cmdlets from a command prompt so we see prompts from SSH asking to verify the host computer as well as password prompts.</span></span>
<span data-ttu-id="62a19-164">Můžete to samé na počítač Windows k zajištění, že vzdálenou komunikaci pracuje existuje a pak vzdálené mezi počítači jednoduše změnou názvu hostitele.</span><span class="sxs-lookup"><span data-stu-id="62a19-164">You can do the same thing on a Windows machine to ensure remoting is working there and then remote between machines by simply changing the host name.</span></span>

```powershell
#
# Linux to Linux
#
PS /home/TestUser> $session = New-PSSession -HostName UbuntuVM1 -UserName TestUser
The authenticity of host 'UbuntuVM1 (9.129.17.107)' cannot be established.
ECDSA key fingerprint is SHA256:2kCbnhT2dUE6WCGgVJ8Hyfu1z2wE4lifaJXLO7QJy0Y.
Are you sure you want to continue connecting (yes/no)?
TestUser@UbuntuVM1s password:

PS /home/TestUser> $session

 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            UbuntuVM1       RemoteMachine   Opened        DefaultShell             Available

PS /home/TestUser> Enter-PSSession $session

[UbuntuVM1]: PS /home/TestUser> uname -a
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~14.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

[UbuntuVM1]: PS /home/TestUser> Exit-PSSession

PS /home/TestUser> Invoke-Command $session -ScriptBlock { Get-Process powershell }

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName                    PSComputerName
-------  ------    -----      -----     ------     --  -- -----------                    --------------
      0       0        0         19       3.23  10635 635 powershell                     UbuntuVM1
      0       0        0         21       4.92  11033 017 powershell                     UbuntuVM1
      0       0        0         20       3.07  11076 076 powershell                     UbuntuVM1


#
# Linux to Windows
#
PS /home/TestUser> Enter-PSSession -HostName WinVM1 -UserName PTestName
PTestName@WinVM1s password:

[WinVM1]: PS C:\Users\PTestName\Documents> cmd /c ver

Microsoft Windows [Version 10.0.10586]

[WinVM1]: PS C:\Users\PTestName\Documents>

#
# Windows to Windows
#
C:\Users\PSUser\Documents>pwsh.exe
PowerShell
Copyright (c) Microsoft Corporation. All rights reserved.

PS C:\Users\PSUser\Documents> $session = New-PSSession -HostName WinVM2 -UserName PSRemoteUser
The authenticity of host 'WinVM2 (10.13.37.3)' can't be established.
ECDSA key fingerprint is SHA256:kSU6slAROyQVMEynVIXAdxSiZpwDBigpAF/TXjjWjmw.
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'WinVM2,10.13.37.3' (ECDSA) to the list of known hosts.
PSRemoteUser@WinVM2's password:
PS C:\Users\PSUser\Documents> $session

 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            WinVM2          RemoteMachine   Opened        DefaultShell             Available


PS C:\Users\PSUser\Documents> Enter-PSSession -Session $session
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

### <a name="known-issues"></a><span data-ttu-id="62a19-165">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="62a19-165">Known Issues</span></span>

1. <span data-ttu-id="62a19-166">příkaz sudo v vzdálené relace k počítači Linux nefunguje.</span><span class="sxs-lookup"><span data-stu-id="62a19-166">sudo command does not work in remote session to Linux machine.</span></span>

[jádra prostředí PowerShell pro systém Windows]: ../setup/installing-powershell-core-on-windows.md#msi
[PowerShell Core for Windows]: ../setup/installing-powershell-core-on-windows.md#msi
[Základní prostředí PowerShell pro Linux]: ../setup/installing-powershell-core-on-linux.md#ubuntu-1404
[PowerShell Core for Linux]: ../setup/installing-powershell-core-on-linux.md#ubuntu-1404
[Jádro prostředí PowerShell pro systému MacOS]: ../setup/installing-powershell-core-on-macos.md
[PowerShell Core for MacOS]: ../setup/installing-powershell-core-on-macos.md
[Win32 OpenSSH]: https://github.com/PowerShell/Win32-OpenSSH/releases
[Instalace]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
[installation]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
[Ubuntu SSH]: https://help.ubuntu.com/lts/serverguide/openssh-server.html

---
title: Vzdálená komunikace PowerShellu přes SSH
description: Vzdálená komunikace v prostředí PowerShell Core pomocí protokolu SSH
ms.date: 08/14/2018
ms.openlocfilehash: 84c3896fe28847beb03e930f933bb4a9dfad397f
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851233"
---
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="3a094-103">Vzdálená komunikace PowerShellu přes SSH</span><span class="sxs-lookup"><span data-stu-id="3a094-103">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="3a094-104">Přehled</span><span class="sxs-lookup"><span data-stu-id="3a094-104">Overview</span></span>

<span data-ttu-id="3a094-105">Vzdálenou komunikaci prostředí PowerShell pro vyjednávání připojení a přenos dat obvykle používá WinRM.</span><span class="sxs-lookup"><span data-stu-id="3a094-105">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span> <span data-ttu-id="3a094-106">SSH je teď dostupná pro platformy operačních systémů Linux a Windows a umožňuje true multiplatformní vzdálenou komunikaci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a094-106">SSH is now available for Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>

<span data-ttu-id="3a094-107">Služba WinRM poskytuje robustní model hostingu pro vzdálené relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a094-107">WinRM provides a robust hosting model for PowerShell remote sessions.</span></span> <span data-ttu-id="3a094-108">které tato implementace založeného na protokolu SSH remoting není aktuálně podporují konfigurace vzdáleného koncového bodu a JEA (Just Enough Administration).</span><span class="sxs-lookup"><span data-stu-id="3a094-108">which this implementation SSH-based remoting doesn't currently support remote endpoint configuration and JEA (Just Enough Administration).</span></span>

<span data-ttu-id="3a094-109">Vzdálenou komunikaci SSH umožňuje provádět základní vzdálené komunikace Powershellu relace mezi počítače s Windows a Linuxem.</span><span class="sxs-lookup"><span data-stu-id="3a094-109">SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span> <span data-ttu-id="3a094-110">Vzdálenou komunikaci SSH vytvoří proces hostitele prostředí PowerShell na cílovém počítači jako podsystému SSH.</span><span class="sxs-lookup"><span data-stu-id="3a094-110">SSH Remoting creates a PowerShell host process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="3a094-111">Nakonec jsme budete implementovat obecný hostování model, podobně jako WinRM pro podporu konfigurace koncového bodu a JEA.</span><span class="sxs-lookup"><span data-stu-id="3a094-111">Eventually we'll implement a general hosting model, similar to WinRM, to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="3a094-112">`New-PSSession`, `Enter-PSSession`, A `Invoke-Command` tyto rutiny teď mají nový parametr nastavte pro podporu této nové připojení vzdálené komunikace.</span><span class="sxs-lookup"><span data-stu-id="3a094-112">The `New-PSSession`, `Enter-PSSession`, and `Invoke-Command` cmdlets now have a new parameter set to support this new remoting connection.</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="3a094-113">Chcete-li vytvořit vzdálené relace, zadejte cílový počítač s `HostName` parametr a zadejte uživatelské jméno s `UserName`.</span><span class="sxs-lookup"><span data-stu-id="3a094-113">To create a remote session, you specify the target machine with the `HostName` parameter and provide the user name with `UserName`.</span></span> <span data-ttu-id="3a094-114">Při interaktivním spuštění rutiny se zobrazí výzva k zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="3a094-114">When running the cmdlets interactively, you're prompted for a password.</span></span> <span data-ttu-id="3a094-115">Můžete také, použijte soubor privátního klíče s použitím ověřování pomocí klíče SSH `KeyFilePath` parametru.</span><span class="sxs-lookup"><span data-stu-id="3a094-115">You can also, use SSH key authentication using a private key file with the `KeyFilePath` parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="3a094-116">Informace o obecných nastavení</span><span class="sxs-lookup"><span data-stu-id="3a094-116">General setup information</span></span>

<span data-ttu-id="3a094-117">SSH musí být nainstalován ve všech počítačích.</span><span class="sxs-lookup"><span data-stu-id="3a094-117">SSH must be installed on all machines.</span></span> <span data-ttu-id="3a094-118">Instalace klienta SSH (`ssh.exe`) a serveru (`sshd.exe`), který umožňuje vzdálený do a z počítače.</span><span class="sxs-lookup"><span data-stu-id="3a094-118">Install both the SSH client (`ssh.exe`) and server (`sshd.exe`) so that you can remote to and from the machines.</span></span> <span data-ttu-id="3a094-119">Pro Windows, nainstalujte [Win32 OpenSSH z Githubu](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="3a094-119">For Windows, install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="3a094-120">Pro Linux instalace SSH (včetně server sshd) pro vaši platformu.</span><span class="sxs-lookup"><span data-stu-id="3a094-120">For Linux, install SSH (including sshd server) appropriate to your platform.</span></span> <span data-ttu-id="3a094-121">Také musíte nainstalovat PowerShell Core z Githubu, které chcete tuto funkci vzdálenou komunikaci SSH.</span><span class="sxs-lookup"><span data-stu-id="3a094-121">You also need to install PowerShell Core from GitHub to get the SSH remoting feature.</span></span> <span data-ttu-id="3a094-122">SSH server musí nakonfigurovat, aby vytvořila podsystému SSH k hostování prostředí PowerShell procesu ve vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="3a094-122">The SSH server must be configured to create an SSH subsystem to host a PowerShell process on the remote machine.</span></span> <span data-ttu-id="3a094-123">Musíte také povolit heslo nebo nastavit ověřování na základě klíče.</span><span class="sxs-lookup"><span data-stu-id="3a094-123">You also must configure enable password or key-based authentication.</span></span>

## <a name="set-up-on-windows-machine"></a><span data-ttu-id="3a094-124">Nastavení na počítači s Windows</span><span class="sxs-lookup"><span data-stu-id="3a094-124">Set up on Windows Machine</span></span>

1. <span data-ttu-id="3a094-125">Nainstalujte nejnovější verzi [PowerShell Core pro Windows](../setup/installing-powershell-core-on-windows.md#msi)</span><span class="sxs-lookup"><span data-stu-id="3a094-125">Install the latest version of [PowerShell Core for Windows](../setup/installing-powershell-core-on-windows.md#msi)</span></span>

   - <span data-ttu-id="3a094-126">Poznáte, že jestli bylo Podpora vzdálené komunikace SSH zobrazením parametr nastaví pro `New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="3a094-126">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="3a094-127">Nainstalujte nejnovější [Win32 OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases) sestavení z Githubu pomocí [instalace](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH) pokyny</span><span class="sxs-lookup"><span data-stu-id="3a094-127">Install the latest [Win32 OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases) build from GitHub using the [installation](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH) instructions</span></span>
3. <span data-ttu-id="3a094-128">Úprava souboru sshd_config v umístění, kam jste nainstalovali Win32 OpenSSH</span><span class="sxs-lookup"><span data-stu-id="3a094-128">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>

   - <span data-ttu-id="3a094-129">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="3a094-129">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.4/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > <span data-ttu-id="3a094-130">OpenSSH pro Windows, který brání práce v cestách spustitelný subsystému prostorů je chyba.</span><span class="sxs-lookup"><span data-stu-id="3a094-130">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span> <span data-ttu-id="3a094-131">Další informace najdete v tématu [tento problém Githubu](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="3a094-131">For more information, see [this GitHub issue](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

     <span data-ttu-id="3a094-132">Jedním z řešení je vytvořte symlink do instalačního adresáře prostředí Powershell, který neobsahuje mezery:</span><span class="sxs-lookup"><span data-stu-id="3a094-132">One solution is to create a symlink to the Powershell installation directory that doesn't have spaces:</span></span>

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.4"
     ```

     <span data-ttu-id="3a094-133">a zadejte ho v subsystému:</span><span class="sxs-lookup"><span data-stu-id="3a094-133">and then enter it in the subsystem:</span></span>

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="3a094-134">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="3a094-134">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

4. <span data-ttu-id="3a094-135">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="3a094-135">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="3a094-136">Přidáte cestu, kde je nainstalován OpenSSH do proměnné prostředí Path.</span><span class="sxs-lookup"><span data-stu-id="3a094-136">Add the path where OpenSSH is installed to your Path environment variable.</span></span> <span data-ttu-id="3a094-137">Například `C:\Program Files\OpenSSH\`.</span><span class="sxs-lookup"><span data-stu-id="3a094-137">For example, `C:\Program Files\OpenSSH\`.</span></span> <span data-ttu-id="3a094-138">Tato položka umožňuje ssh.exe nalezen.</span><span class="sxs-lookup"><span data-stu-id="3a094-138">This entry allows for the ssh.exe to be found.</span></span>

## <a name="set-up-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="3a094-139">Nastavte na počítači s Linuxem (Ubuntu 14.04)</span><span class="sxs-lookup"><span data-stu-id="3a094-139">Set up on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="3a094-140">Nainstalujte nejnovější [PowerShell Core pro Linux](../setup/installing-powershell-core-on-linux.md#ubuntu-1404) sestavení z Githubu</span><span class="sxs-lookup"><span data-stu-id="3a094-140">Install the latest [PowerShell Core for Linux](../setup/installing-powershell-core-on-linux.md#ubuntu-1404) build from GitHub</span></span>
2. <span data-ttu-id="3a094-141">Nainstalujte [SSH se systémem Ubuntu](https://help.ubuntu.com/lts/serverguide/openssh-server.html) podle potřeby</span><span class="sxs-lookup"><span data-stu-id="3a094-141">Install [Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="3a094-142">Úprava souboru sshd_config na umístění /etc/ssh</span><span class="sxs-lookup"><span data-stu-id="3a094-142">Edit the sshd_config file at location /etc/ssh</span></span>

   - <span data-ttu-id="3a094-143">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="3a094-143">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="3a094-144">Přidejte položku subsystém PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a094-144">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="3a094-145">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="3a094-145">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="3a094-146">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="3a094-146">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a><span data-ttu-id="3a094-147">Na počítači s MacOS</span><span class="sxs-lookup"><span data-stu-id="3a094-147">Set up on MacOS Machine</span></span>

1. <span data-ttu-id="3a094-148">Nainstalujte nejnovější [PowerShell Core pro MacOS](../setup/installing-powershell-core-on-macos.md) sestavení</span><span class="sxs-lookup"><span data-stu-id="3a094-148">Install the latest [PowerShell Core for MacOS](../setup/installing-powershell-core-on-macos.md) build</span></span>

   - <span data-ttu-id="3a094-149">Ujistěte se, že je povolená Vzdálená SSH pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="3a094-149">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="3a094-150">Otevřít `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="3a094-150">Open `System Preferences`</span></span>
     - <span data-ttu-id="3a094-151">Klikněte na `Sharing`</span><span class="sxs-lookup"><span data-stu-id="3a094-151">Click on `Sharing`</span></span>
     - <span data-ttu-id="3a094-152">Zkontrolujte `Remote Login` – by mělo být uvedeno `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="3a094-152">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="3a094-153">Povolit přístup k příslušným uživatelům</span><span class="sxs-lookup"><span data-stu-id="3a094-153">Allow access to appropriate users</span></span>

2. <span data-ttu-id="3a094-154">Upravit `sshd_config` soubor na místě `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="3a094-154">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>

   - <span data-ttu-id="3a094-155">Pomocí oblíbeného editoru nebo</span><span class="sxs-lookup"><span data-stu-id="3a094-155">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="3a094-156">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="3a094-156">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="3a094-157">Přidejte položku subsystém PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a094-157">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="3a094-158">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="3a094-158">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="3a094-159">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="3a094-159">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a><span data-ttu-id="3a094-160">Ověřování</span><span class="sxs-lookup"><span data-stu-id="3a094-160">Authentication</span></span>

<span data-ttu-id="3a094-161">Vzdálená komunikace Powershellu přes SSH využívá exchange ověřování mezi klientem SSH a službu SSH a neimplementuje žádné ověřovací schémata samotný.</span><span class="sxs-lookup"><span data-stu-id="3a094-161">PowerShell remoting over SSH relies on the authentication exchange between the SSH client and SSH service and does not implement any authentication schemes itself.</span></span>
<span data-ttu-id="3a094-162">To znamená, že všechny schémat nakonfigurované ověřování, včetně ověřování službou Multi-Factor Authentication zařizuje služba SSH a bez ohledu na prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a094-162">This means that any configured authentication schemes including multi-factor authentication is handled by SSH and independent of PowerShell.</span></span>
<span data-ttu-id="3a094-163">Můžete například nakonfigurovat službu SSH tak, aby vyžadovala ověření veřejného klíče, jakož i jednorázové heslo pro zvýšení zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="3a094-163">For example, you can configure the SSH service to require public key authentication as well as a one-time password for added security.</span></span>
<span data-ttu-id="3a094-164">Konfigurace ověřování službou Multi-Factor Authentication je mimo rozsah této dokumentace.</span><span class="sxs-lookup"><span data-stu-id="3a094-164">Configuration of multi-factor authentication is outside the scope of this documentation.</span></span>
<span data-ttu-id="3a094-165">V dokumentaci pro SSH o tom, jak správně nakonfigurovat ověřování Multi-Factor Authentication a ověřit před pokusem o pomocí vzdálené komunikace Powershellu funguje mimo prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a094-165">Refer to documentation for SSH on how to correctly configure multi-factor authentication and validate it works outside of PowerShell before attempting to use it with PowerShell remoting.</span></span>

## <a name="powershell-remoting-example"></a><span data-ttu-id="3a094-166">Příklad vzdálené komunikace Powershellu</span><span class="sxs-lookup"><span data-stu-id="3a094-166">PowerShell Remoting Example</span></span>

<span data-ttu-id="3a094-167">Nejjednodušší způsob otestování vzdálené komunikace je vyzkoušejte na jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="3a094-167">The easiest way to test remoting is to try it on a single machine.</span></span> <span data-ttu-id="3a094-168">V tomto příkladu vytvoříme relaci vzdálené zpět na stejný počítač s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="3a094-168">In this example, we create a remote session back to the same Linux machine.</span></span> <span data-ttu-id="3a094-169">Používáme Powershellu rutiny interaktivně, takže uvidíme výzev SSH s výzvou k ověření hostitelského počítače a s výzvou k zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="3a094-169">We are using PowerShell cmdlets interactively so we see prompts from SSH asking to verify the host computer and prompting for a password.</span></span> <span data-ttu-id="3a094-170">Můžete to samé udělá na počítači s Windows k zajištění, že funguje vzdálené komunikace.</span><span class="sxs-lookup"><span data-stu-id="3a094-170">You can do the same thing on a Windows machine to ensure remoting is working.</span></span> <span data-ttu-id="3a094-171">Pak pro něj mezi počítači tak, že změníte název hostitele.</span><span class="sxs-lookup"><span data-stu-id="3a094-171">Then remote between machines by changing the host name.</span></span>

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
 Id Name   ComputerName    ComputerType    State    ConfigurationName     Availability
 -- ----   ------------    ------------    -----    -----------------     ------------
  1 SSH1   UbuntuVM1       RemoteMachine   Opened   DefaultShell             Available
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

### <a name="known-issues"></a><span data-ttu-id="3a094-172">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="3a094-172">Known Issues</span></span>

<span data-ttu-id="3a094-173">Příkaz sudo nefunguje v relaci vzdálené k počítači s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="3a094-173">The sudo command doesn't work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="3a094-174">Viz také</span><span class="sxs-lookup"><span data-stu-id="3a094-174">See Also</span></span>

[<span data-ttu-id="3a094-175">PowerShell Core pro Windows</span><span class="sxs-lookup"><span data-stu-id="3a094-175">PowerShell Core for Windows</span></span>](../setup/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="3a094-176">PowerShell Core pro Linux</span><span class="sxs-lookup"><span data-stu-id="3a094-176">PowerShell Core for Linux</span></span>](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="3a094-177">PowerShell Core pro MacOS</span><span class="sxs-lookup"><span data-stu-id="3a094-177">PowerShell Core for MacOS</span></span>](../setup/installing-powershell-core-on-macos.md)

[<span data-ttu-id="3a094-178">Win32 OpenSSH</span><span class="sxs-lookup"><span data-stu-id="3a094-178">Win32 OpenSSH</span></span>](https://github.com/PowerShell/Win32-OpenSSH/releases)

[<span data-ttu-id="3a094-179">SSH se systémem Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3a094-179">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
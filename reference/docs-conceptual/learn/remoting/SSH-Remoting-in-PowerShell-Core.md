---
title: Vzdálená komunikace PowerShellu přes SSH
description: Vzdálená komunikace v prostředí PowerShell Core pomocí protokolu SSH
ms.date: 08/14/2018
ms.openlocfilehash: b5c6bd70841e270c2c128601612c07af9d9aa6e4
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655289"
---
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="da72f-103">Vzdálená komunikace PowerShellu přes SSH</span><span class="sxs-lookup"><span data-stu-id="da72f-103">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="da72f-104">Přehled</span><span class="sxs-lookup"><span data-stu-id="da72f-104">Overview</span></span>

<span data-ttu-id="da72f-105">Vzdálenou komunikaci prostředí PowerShell pro vyjednávání připojení a přenos dat obvykle používá WinRM.</span><span class="sxs-lookup"><span data-stu-id="da72f-105">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span> <span data-ttu-id="da72f-106">SSH je teď dostupná pro platformy operačních systémů Linux a Windows a umožňuje true multiplatformní vzdálenou komunikaci prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da72f-106">SSH is now available for Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>

<span data-ttu-id="da72f-107">Služba WinRM poskytuje robustní model hostingu pro vzdálené relace prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da72f-107">WinRM provides a robust hosting model for PowerShell remote sessions.</span></span> <span data-ttu-id="da72f-108">Vzdálená komunikace založeného na protokolu SSH aktuálně nepodporuje konfiguraci vzdáleného koncového bodu a JEA (Just Enough Administration).</span><span class="sxs-lookup"><span data-stu-id="da72f-108">SSH-based remoting doesn't currently support remote endpoint configuration and JEA (Just Enough Administration).</span></span>

<span data-ttu-id="da72f-109">Vzdálenou komunikaci SSH umožňuje provádět základní vzdálené komunikace Powershellu relace mezi počítače s Windows a Linuxem.</span><span class="sxs-lookup"><span data-stu-id="da72f-109">SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span> <span data-ttu-id="da72f-110">Vzdálenou komunikaci SSH vytvoří proces hostitele prostředí PowerShell na cílovém počítači jako podsystému SSH.</span><span class="sxs-lookup"><span data-stu-id="da72f-110">SSH Remoting creates a PowerShell host process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="da72f-111">Nakonec jsme budete implementovat obecný hostování model, podobně jako WinRM pro podporu konfigurace koncového bodu a JEA.</span><span class="sxs-lookup"><span data-stu-id="da72f-111">Eventually we'll implement a general hosting model, similar to WinRM, to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="da72f-112">`New-PSSession`, `Enter-PSSession`, A `Invoke-Command` tyto rutiny teď mají nový parametr nastavte pro podporu této nové připojení vzdálené komunikace.</span><span class="sxs-lookup"><span data-stu-id="da72f-112">The `New-PSSession`, `Enter-PSSession`, and `Invoke-Command` cmdlets now have a new parameter set to support this new remoting connection.</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="da72f-113">Chcete-li vytvořit vzdálené relace, zadejte cílový počítač s `HostName` parametr a zadejte uživatelské jméno s `UserName`.</span><span class="sxs-lookup"><span data-stu-id="da72f-113">To create a remote session, you specify the target machine with the `HostName` parameter and provide the user name with `UserName`.</span></span> <span data-ttu-id="da72f-114">Při interaktivním spuštění rutiny se zobrazí výzva k zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="da72f-114">When running the cmdlets interactively, you're prompted for a password.</span></span> <span data-ttu-id="da72f-115">Můžete také, použijte soubor privátního klíče s použitím ověřování pomocí klíče SSH `KeyFilePath` parametru.</span><span class="sxs-lookup"><span data-stu-id="da72f-115">You can also, use SSH key authentication using a private key file with the `KeyFilePath` parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="da72f-116">Informace o obecných nastavení</span><span class="sxs-lookup"><span data-stu-id="da72f-116">General setup information</span></span>

<span data-ttu-id="da72f-117">SSH musí být nainstalován ve všech počítačích.</span><span class="sxs-lookup"><span data-stu-id="da72f-117">SSH must be installed on all machines.</span></span> <span data-ttu-id="da72f-118">Instalace klienta SSH (`ssh.exe`) a serveru (`sshd.exe`), který umožňuje vzdálený do a z počítače.</span><span class="sxs-lookup"><span data-stu-id="da72f-118">Install both the SSH client (`ssh.exe`) and server (`sshd.exe`) so that you can remote to and from the machines.</span></span> <span data-ttu-id="da72f-119">OpenSSH pro Windows je teď ve Windows 10 sestavení 1809 a Windows Server 2019.</span><span class="sxs-lookup"><span data-stu-id="da72f-119">OpenSSH for Windows is now availabe in Windows 10 build 1809 and Windows Server 2019.</span></span> <span data-ttu-id="da72f-120">Další informace najdete v tématu [OpenSSH pro Windows](/windows-server/administration/openssh/openssh_overview).</span><span class="sxs-lookup"><span data-stu-id="da72f-120">For more information, see [OpenSSH for Windows](/windows-server/administration/openssh/openssh_overview).</span></span> <span data-ttu-id="da72f-121">Pro Linux instalace SSH (včetně server sshd) pro vaši platformu.</span><span class="sxs-lookup"><span data-stu-id="da72f-121">For Linux, install SSH (including sshd server) appropriate to your platform.</span></span> <span data-ttu-id="da72f-122">Také musíte nainstalovat PowerShell Core z Githubu, které chcete tuto funkci vzdálenou komunikaci SSH.</span><span class="sxs-lookup"><span data-stu-id="da72f-122">You also need to install PowerShell Core from GitHub to get the SSH remoting feature.</span></span> <span data-ttu-id="da72f-123">SSH server musí nakonfigurovat, aby vytvořila podsystému SSH k hostování prostředí PowerShell procesu ve vzdáleném počítači.</span><span class="sxs-lookup"><span data-stu-id="da72f-123">The SSH server must be configured to create an SSH subsystem to host a PowerShell process on the remote machine.</span></span> <span data-ttu-id="da72f-124">Musíte také povolit heslo nebo nastavit ověřování na základě klíče.</span><span class="sxs-lookup"><span data-stu-id="da72f-124">You also must configure enable password or key-based authentication.</span></span>

## <a name="set-up-on-windows-machine"></a><span data-ttu-id="da72f-125">Nastavení na počítači s Windows</span><span class="sxs-lookup"><span data-stu-id="da72f-125">Set up on Windows Machine</span></span>

1. <span data-ttu-id="da72f-126">Nainstalujte nejnovější verzi [PowerShell Core pro Windows](../../install/installing-powershell-core-on-windows.md#msi)</span><span class="sxs-lookup"><span data-stu-id="da72f-126">Install the latest version of [PowerShell Core for Windows](../../install/installing-powershell-core-on-windows.md#msi)</span></span>

   - <span data-ttu-id="da72f-127">Poznáte, že jestli bylo Podpora vzdálené komunikace SSH zobrazením parametr nastaví pro `New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="da72f-127">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="da72f-128">Nainstalujte nejnovější Win32 OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="da72f-128">Install the latest Win32 OpenSSH.</span></span> <span data-ttu-id="da72f-129">Pokyny k instalaci, naleznete v tématu [instalace OpenSSH](/windows-server/administration/openssh/openssh_install_firstuse).</span><span class="sxs-lookup"><span data-stu-id="da72f-129">For installation instructions, see [Installation of OpenSSH](/windows-server/administration/openssh/openssh_install_firstuse).</span></span>
3. <span data-ttu-id="da72f-130">Upravit `sshd_config` se nachází v `%ProgramData%\ssh`.</span><span class="sxs-lookup"><span data-stu-id="da72f-130">Edit the `sshd_config` file located at `%ProgramData%\ssh`.</span></span>

   - <span data-ttu-id="da72f-131">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="da72f-131">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > <span data-ttu-id="da72f-132">OpenSSH pro Windows, který brání práce v cestách spustitelný subsystému prostorů je chyba.</span><span class="sxs-lookup"><span data-stu-id="da72f-132">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span> <span data-ttu-id="da72f-133">Další informace najdete v tématu [tento problém Githubu](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="da72f-133">For more information, see [this GitHub issue](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

     <span data-ttu-id="da72f-134">Jedním z řešení je vytvořte symlink do instalačního adresáře prostředí Powershell, který neobsahuje mezery:</span><span class="sxs-lookup"><span data-stu-id="da72f-134">One solution is to create a symlink to the Powershell installation directory that doesn't have spaces:</span></span>

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6"
     ```

     <span data-ttu-id="da72f-135">a zadejte ho v subsystému:</span><span class="sxs-lookup"><span data-stu-id="da72f-135">and then enter it in the subsystem:</span></span>

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="da72f-136">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="da72f-136">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

4. <span data-ttu-id="da72f-137">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="da72f-137">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="da72f-138">Přidáte cestu, kde je nainstalován OpenSSH do proměnné prostředí Path.</span><span class="sxs-lookup"><span data-stu-id="da72f-138">Add the path where OpenSSH is installed to your Path environment variable.</span></span> <span data-ttu-id="da72f-139">Například `C:\Program Files\OpenSSH\`.</span><span class="sxs-lookup"><span data-stu-id="da72f-139">For example, `C:\Program Files\OpenSSH\`.</span></span> <span data-ttu-id="da72f-140">Tato položka umožňuje ssh.exe nalezen.</span><span class="sxs-lookup"><span data-stu-id="da72f-140">This entry allows for the ssh.exe to be found.</span></span>

## <a name="set-up-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="da72f-141">Nastavte na počítači s Linuxem (Ubuntu 14.04)</span><span class="sxs-lookup"><span data-stu-id="da72f-141">Set up on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="da72f-142">Nainstalujte nejnovější [PowerShell Core pro Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1404) sestavení z Githubu</span><span class="sxs-lookup"><span data-stu-id="da72f-142">Install the latest [PowerShell Core for Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1404) build from GitHub</span></span>
2. <span data-ttu-id="da72f-143">Nainstalujte [SSH se systémem Ubuntu](https://help.ubuntu.com/lts/serverguide/openssh-server.html) podle potřeby</span><span class="sxs-lookup"><span data-stu-id="da72f-143">Install [Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="da72f-144">Úprava souboru sshd_config na umístění /etc/ssh</span><span class="sxs-lookup"><span data-stu-id="da72f-144">Edit the sshd_config file at location /etc/ssh</span></span>

   - <span data-ttu-id="da72f-145">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="da72f-145">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="da72f-146">Přidejte položku subsystém PowerShell</span><span class="sxs-lookup"><span data-stu-id="da72f-146">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="da72f-147">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="da72f-147">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="da72f-148">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="da72f-148">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a><span data-ttu-id="da72f-149">Na počítači s MacOS</span><span class="sxs-lookup"><span data-stu-id="da72f-149">Set up on MacOS Machine</span></span>

1. <span data-ttu-id="da72f-150">Nainstalujte nejnovější [PowerShell Core pro MacOS](../../install/installing-powershell-core-on-macos.md) sestavení</span><span class="sxs-lookup"><span data-stu-id="da72f-150">Install the latest [PowerShell Core for MacOS](../../install/installing-powershell-core-on-macos.md) build</span></span>

   - <span data-ttu-id="da72f-151">Ujistěte se, že je povolená Vzdálená SSH pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="da72f-151">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="da72f-152">Otevřít `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="da72f-152">Open `System Preferences`</span></span>
     - <span data-ttu-id="da72f-153">Klikněte na `Sharing`</span><span class="sxs-lookup"><span data-stu-id="da72f-153">Click on `Sharing`</span></span>
     - <span data-ttu-id="da72f-154">Zkontrolujte `Remote Login` – by mělo být uvedeno `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="da72f-154">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="da72f-155">Povolit přístup k příslušným uživatelům</span><span class="sxs-lookup"><span data-stu-id="da72f-155">Allow access to appropriate users</span></span>

2. <span data-ttu-id="da72f-156">Upravit `sshd_config` soubor na místě `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="da72f-156">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>

   - <span data-ttu-id="da72f-157">Pomocí oblíbeného editoru nebo</span><span class="sxs-lookup"><span data-stu-id="da72f-157">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="da72f-158">Ujistěte se, že je povoleno ověřování hesla</span><span class="sxs-lookup"><span data-stu-id="da72f-158">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="da72f-159">Přidejte položku subsystém PowerShell</span><span class="sxs-lookup"><span data-stu-id="da72f-159">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="da72f-160">Volitelně můžete povolit ověřování pomocí klíče</span><span class="sxs-lookup"><span data-stu-id="da72f-160">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="da72f-161">Restartujte službu sshd</span><span class="sxs-lookup"><span data-stu-id="da72f-161">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a><span data-ttu-id="da72f-162">Ověřování</span><span class="sxs-lookup"><span data-stu-id="da72f-162">Authentication</span></span>

<span data-ttu-id="da72f-163">Vzdálená komunikace Powershellu přes SSH využívá exchange ověřování mezi klientem SSH a službu SSH a neimplementuje žádné ověřovací schémata samotný.</span><span class="sxs-lookup"><span data-stu-id="da72f-163">PowerShell remoting over SSH relies on the authentication exchange between the SSH client and SSH service and does not implement any authentication schemes itself.</span></span>
<span data-ttu-id="da72f-164">To znamená, že všechny schémat nakonfigurované ověřování, včetně ověřování službou Multi-Factor Authentication zařizuje služba SSH a bez ohledu na prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da72f-164">This means that any configured authentication schemes including multi-factor authentication is handled by SSH and independent of PowerShell.</span></span>
<span data-ttu-id="da72f-165">Můžete například nakonfigurovat službu SSH tak, aby vyžadovala ověření veřejného klíče, jakož i jednorázové heslo pro zvýšení zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="da72f-165">For example, you can configure the SSH service to require public key authentication as well as a one-time password for added security.</span></span>
<span data-ttu-id="da72f-166">Konfigurace ověřování službou Multi-Factor Authentication je mimo rozsah této dokumentace.</span><span class="sxs-lookup"><span data-stu-id="da72f-166">Configuration of multi-factor authentication is outside the scope of this documentation.</span></span>
<span data-ttu-id="da72f-167">V dokumentaci pro SSH o tom, jak správně nakonfigurovat ověřování Multi-Factor Authentication a ověřit před pokusem o pomocí vzdálené komunikace Powershellu funguje mimo prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da72f-167">Refer to documentation for SSH on how to correctly configure multi-factor authentication and validate it works outside of PowerShell before attempting to use it with PowerShell remoting.</span></span>

## <a name="powershell-remoting-example"></a><span data-ttu-id="da72f-168">Příklad vzdálené komunikace Powershellu</span><span class="sxs-lookup"><span data-stu-id="da72f-168">PowerShell Remoting Example</span></span>

<span data-ttu-id="da72f-169">Nejjednodušší způsob otestování vzdálené komunikace je vyzkoušejte na jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="da72f-169">The easiest way to test remoting is to try it on a single machine.</span></span> <span data-ttu-id="da72f-170">V tomto příkladu vytvoříme relaci vzdálené zpět na stejný počítač s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="da72f-170">In this example, we create a remote session back to the same Linux machine.</span></span> <span data-ttu-id="da72f-171">Používáme Powershellu rutiny interaktivně, takže uvidíme výzev SSH s výzvou k ověření hostitelského počítače a s výzvou k zadání hesla.</span><span class="sxs-lookup"><span data-stu-id="da72f-171">We are using PowerShell cmdlets interactively so we see prompts from SSH asking to verify the host computer and prompting for a password.</span></span> <span data-ttu-id="da72f-172">Můžete to samé udělá na počítači s Windows k zajištění, že funguje vzdálené komunikace.</span><span class="sxs-lookup"><span data-stu-id="da72f-172">You can do the same thing on a Windows machine to ensure remoting is working.</span></span> <span data-ttu-id="da72f-173">Pak pro něj mezi počítači tak, že změníte název hostitele.</span><span class="sxs-lookup"><span data-stu-id="da72f-173">Then remote between machines by changing the host name.</span></span>

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

### <a name="known-issues"></a><span data-ttu-id="da72f-174">Známé problémy</span><span class="sxs-lookup"><span data-stu-id="da72f-174">Known Issues</span></span>

<span data-ttu-id="da72f-175">Příkaz sudo nefunguje v relaci vzdálené k počítači s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="da72f-175">The sudo command doesn't work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="da72f-176">Viz také</span><span class="sxs-lookup"><span data-stu-id="da72f-176">See Also</span></span>

[<span data-ttu-id="da72f-177">PowerShell Core pro Windows</span><span class="sxs-lookup"><span data-stu-id="da72f-177">PowerShell Core for Windows</span></span>](../../install/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="da72f-178">PowerShell Core pro Linux</span><span class="sxs-lookup"><span data-stu-id="da72f-178">PowerShell Core for Linux</span></span>](../../install/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="da72f-179">PowerShell Core pro MacOS</span><span class="sxs-lookup"><span data-stu-id="da72f-179">PowerShell Core for MacOS</span></span>](../../install/installing-powershell-core-on-macos.md)

[<span data-ttu-id="da72f-180">OpenSSH pro Windows</span><span class="sxs-lookup"><span data-stu-id="da72f-180">OpenSSH for Windows</span></span>](/windows-server/administration/openssh/openssh_overview)

[<span data-ttu-id="da72f-181">SSH se systémem Ubuntu</span><span class="sxs-lookup"><span data-stu-id="da72f-181">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)

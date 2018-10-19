---
title: Vzdálená komunikace PowerShellu přes SSH
description: Vzdálená komunikace v prostředí PowerShell Core pomocí protokolu SSH
ms.date: 08/14/2018
ms.openlocfilehash: 842e67e96661bca8be54aab33cbc11aa23dbd1c0
ms.sourcegitcommit: 47becf2823ece251a7264db2387bb503cf3abaa9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/19/2018
ms.locfileid: "49451061"
---
# <a name="powershell-remoting-over-ssh"></a>Vzdálená komunikace PowerShellu přes SSH

## <a name="overview"></a>Přehled

Vzdálenou komunikaci prostředí PowerShell pro vyjednávání připojení a přenos dat obvykle používá WinRM. SSH je teď dostupná pro platformy operačních systémů Linux a Windows a umožňuje true multiplatformní vzdálenou komunikaci prostředí PowerShell.

Služba WinRM poskytuje robustní model hostingu pro vzdálené relace prostředí PowerShell. Vzdálená komunikace založeného na protokolu SSH aktuálně nepodporuje konfiguraci vzdáleného koncového bodu a JEA (Just Enough Administration).

Vzdálenou komunikaci SSH umožňuje provádět základní vzdálené komunikace Powershellu relace mezi počítače s Windows a Linuxem. Vzdálenou komunikaci SSH vytvoří proces hostitele prostředí PowerShell na cílovém počítači jako podsystému SSH.
Nakonec jsme budete implementovat obecný hostování model, podobně jako WinRM pro podporu konfigurace koncového bodu a JEA.

`New-PSSession`, `Enter-PSSession`, A `Invoke-Command` tyto rutiny teď mají nový parametr nastavte pro podporu této nové připojení vzdálené komunikace.

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Chcete-li vytvořit vzdálené relace, zadejte cílový počítač s `HostName` parametr a zadejte uživatelské jméno s `UserName`. Při interaktivním spuštění rutiny se zobrazí výzva k zadání hesla. Můžete také, použijte soubor privátního klíče s použitím ověřování pomocí klíče SSH `KeyFilePath` parametru.

## <a name="general-setup-information"></a>Informace o obecných nastavení

SSH musí být nainstalován ve všech počítačích. Instalace klienta SSH (`ssh.exe`) a serveru (`sshd.exe`), který umožňuje vzdálený do a z počítače. Pro Windows, nainstalujte [Win32 OpenSSH z Githubu](https://github.com/PowerShell/Win32-OpenSSH/releases).
Pro Linux instalace SSH (včetně server sshd) pro vaši platformu. Také musíte nainstalovat PowerShell Core z Githubu, které chcete tuto funkci vzdálenou komunikaci SSH. SSH server musí nakonfigurovat, aby vytvořila podsystému SSH k hostování prostředí PowerShell procesu ve vzdáleném počítači. Musíte také povolit heslo nebo nastavit ověřování na základě klíče.

## <a name="set-up-on-windows-machine"></a>Nastavení na počítači s Windows

1. Nainstalujte nejnovější verzi [PowerShell Core pro Windows](../setup/installing-powershell-core-on-windows.md#msi)

   - Poznáte, že jestli bylo Podpora vzdálené komunikace SSH zobrazením parametr nastaví pro `New-PSSession`

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. Nainstalujte nejnovější [Win32 OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases) sestavení z Githubu pomocí [instalace](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH) pokyny
3. Upravit umístění souboru sshd_config `%ProgramData%\ssh`.

   - Ujistěte se, že je povoleno ověřování hesla

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > OpenSSH pro Windows, který brání práce v cestách spustitelný subsystému prostorů je chyba. Další informace najdete v tématu [tento problém Githubu](https://github.com/PowerShell/Win32-OpenSSH/issues/784).

     Jedním z řešení je vytvořte symlink do instalačního adresáře prostředí Powershell, který neobsahuje mezery:

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6"
     ```

     a zadejte ho v subsystému:

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - Volitelně můžete povolit ověřování pomocí klíče

     ```
     PubkeyAuthentication yes
     ```

4. Restartujte službu sshd

   ```powershell
   Restart-Service sshd
   ```

5. Přidáte cestu, kde je nainstalován OpenSSH do proměnné prostředí Path. Například `C:\Program Files\OpenSSH\`. Tato položka umožňuje ssh.exe nalezen.

## <a name="set-up-on-linux-ubuntu-1404-machine"></a>Nastavte na počítači s Linuxem (Ubuntu 14.04)

1. Nainstalujte nejnovější [PowerShell Core pro Linux](../setup/installing-powershell-core-on-linux.md#ubuntu-1404) sestavení z Githubu
2. Nainstalujte [SSH se systémem Ubuntu](https://help.ubuntu.com/lts/serverguide/openssh-server.html) podle potřeby

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. Úprava souboru sshd_config na umístění /etc/ssh

   - Ujistěte se, že je povoleno ověřování hesla

   ```
   PasswordAuthentication yes
   ```

   - Přidejte položku subsystém PowerShell

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - Volitelně můžete povolit ověřování pomocí klíče

   ```
   PubkeyAuthentication yes
   ```

4. Restartujte službu sshd

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a>Na počítači s MacOS

1. Nainstalujte nejnovější [PowerShell Core pro MacOS](../setup/installing-powershell-core-on-macos.md) sestavení

   - Ujistěte se, že je povolená Vzdálená SSH pomocí následujících kroků:
     - Otevřít `System Preferences`
     - Klikněte na `Sharing`
     - Zkontrolujte `Remote Login` – by mělo být uvedeno `Remote Login: On`
     - Povolit přístup k příslušným uživatelům

2. Upravit `sshd_config` soubor na místě `/private/etc/ssh/sshd_config`

   - Pomocí oblíbeného editoru nebo

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - Ujistěte se, že je povoleno ověřování hesla

     ```
     PasswordAuthentication yes
     ```

   - Přidejte položku subsystém PowerShell

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - Volitelně můžete povolit ověřování pomocí klíče

     ```
     PubkeyAuthentication yes
     ```

3. Restartujte službu sshd

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a>Ověřování

Vzdálená komunikace Powershellu přes SSH využívá exchange ověřování mezi klientem SSH a službu SSH a neimplementuje žádné ověřovací schémata samotný.
To znamená, že všechny schémat nakonfigurované ověřování, včetně ověřování službou Multi-Factor Authentication zařizuje služba SSH a bez ohledu na prostředí PowerShell.
Můžete například nakonfigurovat službu SSH tak, aby vyžadovala ověření veřejného klíče, jakož i jednorázové heslo pro zvýšení zabezpečení.
Konfigurace ověřování službou Multi-Factor Authentication je mimo rozsah této dokumentace.
V dokumentaci pro SSH o tom, jak správně nakonfigurovat ověřování Multi-Factor Authentication a ověřit před pokusem o pomocí vzdálené komunikace Powershellu funguje mimo prostředí PowerShell.

## <a name="powershell-remoting-example"></a>Příklad vzdálené komunikace Powershellu

Nejjednodušší způsob otestování vzdálené komunikace je vyzkoušejte na jednom počítači. V tomto příkladu vytvoříme relaci vzdálené zpět na stejný počítač s Linuxem. Používáme Powershellu rutiny interaktivně, takže uvidíme výzev SSH s výzvou k ověření hostitelského počítače a s výzvou k zadání hesla. Můžete to samé udělá na počítači s Windows k zajištění, že funguje vzdálené komunikace. Pak pro něj mezi počítači tak, že změníte název hostitele.

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

### <a name="known-issues"></a>Známé problémy

Příkaz sudo nefunguje v relaci vzdálené k počítači s Linuxem.

## <a name="see-also"></a>Viz také

[PowerShell Core pro Windows](../setup/installing-powershell-core-on-windows.md#msi)

[PowerShell Core pro Linux](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[PowerShell Core pro MacOS](../setup/installing-powershell-core-on-macos.md)

[Win32 OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases)

[SSH se systémem Ubuntu](https://help.ubuntu.com/lts/serverguide/openssh-server.html)

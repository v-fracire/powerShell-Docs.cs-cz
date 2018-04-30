# <a name="powershell-remoting-over-ssh"></a>Vzdálená komunikace PowerShellu přes SSH

## <a name="overview"></a>Přehled

Vzdálená komunikace prostředí PowerShell normálně používá WinRM pro vyjednávání připojení a přenosu dat.
SSH jste vybrali pro tuto implementaci vzdálenou komunikaci, protože je teď dostupná pro platformy Linux a Windows a umožňuje true vzdálenou komunikaci prostředí PowerShell s více platformami.
WinRM však také poskytuje robustní hostování model pro vzdálené relace prostředí PowerShell, které tato implementace ještě neprovádí.
A to znamená, že JEA (právě dostatečně správy) a konfigurace prostředí PowerShell vzdálený koncový bod není dosud podporováno v této implementaci.

Remoting SSH prostředí PowerShell vám umožňuje provést základní vzdálenou komunikaci prostředí PowerShell relací mezi počítači Windows a Linux.
Děje se tak, že vytvoříte proces v cílovém počítači jako podsystému SSH hostování prostředí PowerShell.
Nakonec to bude změněno na další obecné podobný Princip WinRM za účelem podpory konfigurace koncového bodu a JEA hostování modelu.

Rutiny New-PSSession, Enter-PSSession a Invoke-Command Teď máte nový parametr nastavit pro usnadnění tohoto nového připojení vzdálené komunikace

```powershell
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Tuto novou sadu parametrů pravděpodobně se změní, ale teď umožňuje vytvářet SSH PSSessions můžete pracovat s z příkazového řádku nebo vyvolání na příkazy a skripty.
Zadejte cílový počítač s parametrem název hostitele a zadejte uživatelské jméno s uživatelským jménem.
Při interaktivním spuštění rutiny na příkazovém řádku prostředí PowerShell vás vyzve k zadání hesla.
Ale máte také možnost použít ověření pomocí klíče SSH a zadejte cestu soubor privátního klíče s parametrem KeyFilePath.

## <a name="general-setup-information"></a>Informace o obecné nastavení

SSH je musí být nainstalovaný na všech počítačích.
Musíte nainstalovat klienta (ssh.exe) a serveru (sshd.exe) tak, aby můžete experimentovat s vzdálené komunikace do a z počítačů.
Pro systém Windows je potřeba nainstalovat [OpenSSH Win32 z Githubu](https://github.com/PowerShell/Win32-OpenSSH/releases).
Pro Linux, musíte nainstalovat SSH (včetně sshd server) vhodné pro vaši platformu.
Budete také potřebovat poslední sestavení prostředí PowerShell nebo balíček z Githubu s funkci Vzdálená komunikace SSH.
Subsystémy SSH se používá k zahájení procesu prostředí PowerShell ve vzdáleném počítači a serverem SSH bude nutné je nakonfigurovat pro tento.
Kromě toho musíte povolit ověřování hesla a volitelně klíče ověřování založené na.

## <a name="setup-on-windows-machine"></a>Instalace na počítač s Windows

1. Nainstalujte nejnovější verzi [jádra prostředí PowerShell pro systém Windows]
    - Můžete zadat, že pokud má dokonalejší podpora SSH prohlížením Nastaví parametr pro New-PSSession

    ```powershell
    PS> Get-Command New-PSSession -syntax
    New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
    ```

1. Nainstalujte si nejnovější verzi [Win32 OpenSSH] sestavení z Githubu pomocí [instalace] pokyny
1. Upravte soubor sshd_config v umístění, kam jste nainstalovali Win32 OpenSSH
    - Ujistěte se, že je povolené ověřování hesla

    ```
    PasswordAuthentication yes
    ```

    - Přidat položku subsystém prostředí PowerShell, nahraďte `c:/program files/powershell/6.0.0/pwsh.exe` správná cesta na verzi, kterou chcete použít

    ```
    Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
    ```

    - Volitelně můžete povolit ověření pomocí klíče

    ```
    PubkeyAuthentication yes
    ```

1. Restartujte službu sshd

    ```powershell
    Restart-Service sshd
    ```

1. Přidat cestu, kde je nainstalován OpenSSH pro vaši cestu Env proměnné
    - Měl by být spolu čar `C:\Program Files\OpenSSH\`
    - To umožňuje, aby ssh.exe chcete vyhledat

## <a name="setup-on-linux-ubuntu-1404-machine"></a>Instalační program na počítači Linux (Ubuntu 14.04)

1. Nainstalujte si nejnovější verzi [prostředí PowerShell pro Linux] sestavení z Githubu
1. Nainstalujte [Ubuntu SSH] podle potřeby

    ```bash
    sudo apt install openssh-client
    sudo apt install openssh-server
    ```

1. Upravte soubor sshd_config v umístění /etc/ssh
    - Ujistěte se, že je povolené ověřování hesla

    ```
    PasswordAuthentication yes
    ```

    - Přidat položku subsystém prostředí PowerShell

    ```
    Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
    ```

    - Volitelně můžete povolit ověření pomocí klíče

    ```
    PubkeyAuthentication yes
    ```

1. Restartujte službu sshd

    ```bash
    sudo service sshd restart
    ```

## <a name="setup-on-macos-machine"></a>Instalační program na počítači systému MacOS

1. Nainstalujte si nejnovější verzi [prostředí PowerShell pro systému MacOS] sestavení
    - Zkontrolujte, zda že je povolena vzdálená SSH komunikace pomocí následujících kroků:
      - Otevřete `System Preferences`
      - Klikněte na `Sharing`
      - Zkontrolujte `Remote Login` – by mělo být uvedeno `Remote Login: On`
      - Povolit přístup k příslušné uživatele
1. Upravit `sshd_config` soubor v umístění `/private/etc/ssh/sshd_config`
    - Pomocí oblíbeného editoru nebo

    ```bash
    sudo nano /private/etc/ssh/sshd_config
    ```

    - Ujistěte se, že je povolené ověřování hesla

    ```
    PasswordAuthentication yes
    ```

    - Přidat položku subsystém prostředí PowerShell

    ```
    Subsystem powershell /usr/local/bin/powershell -sshs -NoLogo -NoProfile
    ```

    - Volitelně můžete povolit ověření pomocí klíče

    ```
    PubkeyAuthentication yes
    ```

1. Restartujte službu sshd

    ```bash
    sudo launchctl stop com.openssh.sshd
    sudo launchctl start com.openssh.sshd
    ```

## <a name="powershell-remoting-example"></a>Příklad vzdálenou komunikaci prostředí PowerShell

Nejjednodušší způsob, jak otestovat vzdálené komunikace je právě vyzkoušejte si to na jednom počítači.
Tady na pole Linux vytvořím vzdálenou relaci zpátky do stejného počítače.
Všimněte si, že je používána rutiny prostředí PowerShell z příkazového řádku, vidíme výzvy ze SSH s dotazem, chcete-li ověřit na hostitelském počítači a také na zadání hesla.
Můžete to samé na počítač Windows k zajištění, že vzdálenou komunikaci pracuje existuje a pak vzdálené mezi počítači jednoduše změnou názvu hostitele.

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

### <a name="known-issues"></a>Známé problémy

1. příkaz sudo v vzdálené relace k počítači Linux nefunguje.

[jádra prostředí PowerShell pro systém Windows]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/windows.md#msi
[Win32 OpenSSH]: https://github.com/PowerShell/Win32-OpenSSH/releases
[instalace]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
[prostředí PowerShell pro Linux]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#ubuntu-1404
[Ubuntu SSH]: https://help.ubuntu.com/lts/serverguide/openssh-server.html
[prostředí PowerShell pro systému MacOS]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/macos.md#macos-1012

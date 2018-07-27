
# <a name="powershell-remoting-over-ssh"></a>Vzdálená komunikace PowerShellu přes SSH

## <a name="overview"></a>Přehled

Vzdálenou komunikaci prostředí PowerShell pro vyjednávání připojení a přenos dat obvykle používá WinRM. SSH byla vybrána pro tuto implementaci vzdálenou komunikaci, protože je teď dostupná pro platformy Linux i Windows a umožňuje true multiplatformní vzdálenou komunikaci prostředí PowerShell. Služba WinRM však také poskytuje robustní model hostingu pro vzdálené relace prostředí PowerShell, které tato implementace zatím nenabízí. A to znamená, že vzdálený koncový bod konfigurace prostředí PowerShell a JEA (Just Enough Administration) se ještě nepodporuje v této implementaci.

PowerShell SSH remoting umožňuje provádět základní vzdálené komunikace Powershellu relace mezi počítače s Windows a Linuxem. To se provádí tak, že vytvoříte Powershellu hostující proces na cílovém počítači jako podsystému SSH. Nakonec to bude změněno na obecnější hostování model podobný Princip WinRM, aby bylo možné podporovat konfiguraci koncového bodu a JEA.

`New-PSSession`, `Enter-PSSession` a `Invoke-Command` tyto rutiny teď mají nový parametr nastavte pro usnadnění tohoto nového připojení vzdálené komunikace

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Tato nová sada parametrů se pravděpodobně změní, ale teď umožňuje vytvářet SSH PSSessions, že budete pracovat z příkazového řádku nebo vyvolat příkazy a skripty na. Zadejte cílový počítač s parametrem názvu hostitele a zadejte uživatelské jméno s uživatelským jménem. Při interaktivním spuštění rutiny příkazového řádku Powershellu se výzva k zadání hesla. Ale máte také možnost použít ověřování pomocí klíče SSH a zadejte cestu souboru s privátním klíčem s parametrem KeyFilePath.

## <a name="general-setup-information"></a>Informace o obecných nastavení

SSH je musí být nainstalovaný na všech počítačích. Měli byste nainstalovat klientské (`ssh.exe`) a serveru (`sshd.exe`) tak, že můžete experimentovat s vzdálené komunikace do a z počítače. Pro Windows je potřeba nainstalovat [Win32 OpenSSH z Githubu](https://github.com/PowerShell/Win32-OpenSSH/releases).
Pro Linux je potřeba nainstalovat SSH (včetně server sshd) pro vaši platformu. Budete také potřebovat poslední sestavení prostředí PowerShell nebo balíček z Githubu s funkcí vzdálenou komunikaci SSH.
Subsystémy SSH se používá k navázání Powershellu procesu ve vzdáleném počítači a SSH server bude potřeba nakonfigurovat pro daný. Kromě toho je potřeba povolit ověřování pomocí hesla a volitelně klíče ověřování.

## <a name="setup-on-windows-machine"></a>Instalační program na počítači s Windows

1. Nainstalujte nejnovější verzi [PowerShell Core pro Windows]

   - Poznáte, že jestli bylo Podpora vzdálené komunikace SSH zobrazením parametr nastaví pro `New-PSSession`

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. Nainstalujte nejnovější sestavení [Win32 OpenSSH] z Githubu pomocí instrukcí [instalace]
3. Úprava souboru sshd_config v umístění, kam jste nainstalovali Win32 OpenSSH

   - Ujistěte se, že je povoleno ověřování hesla

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > OpenSSH pro Windows, který brání práce v cestách spustitelný subsystému prostorů je chyba.
     > Zobrazit [tento problém na Githubu pro další informace o](https://github.com/PowerShell/Win32-OpenSSH/issues/784).

     Jedním z řešení je vytvořte symlink do instalačního adresáře prostředí Powershell, který neobsahuje mezery:

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
     ```

     a zadejte ho v subsystému:

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - Volitelně můžete povolit ověřování pomocí klíče

     ```
     PubkeyAuthentication yes
     ```

4. Restartujte službu sshd

   ```powershell
   Restart-Service sshd
   ```

5. Přidat cestu, kde je nainstalován OpenSSH na vaše proměnné Env cesta

   - To by měla být podle `C:\Program Files\OpenSSH\`
   - To umožňuje ssh.exe nalezen

## <a name="setup-on-linux-ubuntu-1404-machine"></a>Instalační program na počítači s Linuxem (Ubuntu 14.04)

1. Nainstalujte nejnovější sestavení [PowerShell Core pro Linux] z Githubu
2. Instalace [Ubuntu SSH] podle potřeby

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

## <a name="setup-on-macos-machine"></a>Instalace na počítači s MacOS

1. Nainstalujte nejnovější sestavení [PowerShell Core pro MacOS]

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

## <a name="powershell-remoting-example"></a>Příklad vzdálené komunikace Powershellu

Nejjednodušší způsob otestování vzdálené komunikace je prostě to zkuste na jednom počítači. Tady můžu se vytvořit relaci vzdálené zpět do stejného počítače v systému Linux box. Všimněte si, že používám rutin Powershellu z příkazového řádku, proto jsme zobrazovat výzvy z SSH s výzvou k ověření hostitelského počítače, stejně jako zadání hesla. Můžete provést totéž v počítači Windows k zajištění, že existuje funguje vzdálené komunikace a pak vzdálené mezi počítači jednoduchou změnou názvu hostitele.

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

### <a name="known-issues"></a>Známé problémy

Příkaz sudo nefunguje v relaci vzdálené k počítači s Linuxem.

## <a name="see-also"></a>Viz také

[PowerShell Core pro Windows](../setup/installing-powershell-core-on-windows.md#msi)

[PowerShell Core pro Linux](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[PowerShell Core pro MacOS](../setup/installing-powershell-core-on-macos.md)

[Win32 OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases)

[instalace](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[SSH se systémem Ubuntu](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
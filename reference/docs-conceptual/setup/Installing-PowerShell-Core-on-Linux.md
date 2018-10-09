---
title: Instalace PowerShellu Core v Linuxu
description: Informace o instalaci Powershellu Core v různých distribucích systému Linux
ms.date: 08/06/2018
ms.openlocfilehash: d60e1d5a89b6907b67c19b8cfcde969be156bd60
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851285"
---
# <a name="installing-powershell-core-on-linux"></a>Instalace PowerShellu Core v Linuxu

Podporuje [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.10] [ u18], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27 ] [ fedora], [Fedora 28][fedora], a [Arch Linux][arch].

Pro distribuce Linuxu, které nejsou oficiálně podporované, můžete zkusit použít [balíčků v Powershellu Přichytit][snap].
Nasazení prostředí PowerShell binární soubory přímo s Linuxem můžete také zkusit [ `tar.gz` archivu][tar], ale je potřeba nastavit potřebné závislosti podle operačního systému v samostatné kroky.

Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.
Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u18]: #ubuntu-1810
[u18]: #ubuntu-1804
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-423
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a>Instalace Preview verzí

Při instalaci verze Preview prostředí PowerShell Core pro Linux přes úložiště balíčků, názvu balíčku se změní z `powershell` k `powershell-preview`.

Instalace přes přímé stažení nezmění, než je název souboru.

Tady je tabulka znázorňující příkazy, abyste nainstalovali stabilní verze a preview balíčků pomocí různých správců balíčků:

|Distribution(s)|Stabilní příkaz | Příkaz ve verzi Preview |
|---------------|---------------|-----------------|
| Ubuntu, Debian |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| CentOS, Red Hat |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| OpenSUSE |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| Fedora   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a>Ubuntu 14.04

### <a name="installation-via-package-repository---ubuntu-1404"></a>Instalace přes úložiště balíčků – Ubuntu 14.04

PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).
Toto je upřednostňovaná metoda.

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Jako superuživatele zaregistrujte úložiště společnosti Microsoft.
Od té chvíle stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.

### <a name="installation-via-direct-download---ubuntu-1404"></a>Instalace přes přímé stažení – Ubuntu 14.04

Stáhněte si balíček Debian `powershell_6.1.0-1.ubuntu.14.04_amd64.deb`
z [uvolní][] stránky do počítače se systémem Ubuntu.

Potom v terminálu spusťte následující:

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` Příkaz selže s dosud nevyřešených závislosti.
> Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.

### <a name="uninstallation---ubuntu-1404"></a>Odinstalace – Ubuntu 14.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a>Ubuntu 16.04

### <a name="installation-via-package-repository---ubuntu-1604"></a>Instalace přes úložiště balíčků – Ubuntu 16.04

PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).
Toto je upřednostňovaná metoda.

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.

### <a name="installation-via-direct-download---ubuntu-1604"></a>Instalace přes přímé stažení – Ubuntu 16.04

Stáhněte si balíček Debian `powershell_6.1.0-1.ubuntu.16.04_amd64.deb`
z [uvolní][] stránky do počítače se systémem Ubuntu.

Potom v terminálu spusťte následující:

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` Příkaz selže s dosud nevyřešených závislosti.
> Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.

### <a name="uninstallation---ubuntu-1604"></a>Odinstalace – Ubuntu 16.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a>Ubuntu 18.04

> [!NOTE]
> Přidali jsme podporu pro Ubuntu 18.04 po `6.1.0-preview.2`

### <a name="installation-via-package-repository---ubuntu-1804"></a>Instalace přes úložiště balíčků – Ubuntu 18.04

PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).
Toto je upřednostňovaná metoda.

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.

### <a name="installation-via-direct-download---ubuntu-1804"></a>Instalace přes přímé stažení – Ubuntu 18.04

Stáhněte si balíček Debian `powershell_6.1.0-1.ubuntu.18.04_amd64.deb`
z [uvolní][] stránky do počítače se systémem Ubuntu.

Potom v terminálu spusťte následující:

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` Příkaz selže s dosud nevyřešených závislosti.
> Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.

### <a name="uninstallation---ubuntu-1804"></a>Odinstalace – Ubuntu 18.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a>Ubuntu 18.10

> [!NOTE]
> Přidali jsme podporu pro Ubuntu 18.10 po `6.1.0-preview.3`.
> Je 18.10 každodenními buildy, je podporovaná pouze komunitou.

Instalace na 18.10 je podporované prostřednictvím `snapd`. Zobrazit [Přichytit balíček] [ snap] úplné pokyny;

## <a name="debian-8"></a>Debian 8

### <a name="installation-via-package-repository---debian-8"></a>Instalace přes úložiště balíčků – Debian 8

PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).
Toto je upřednostňovaná metoda.

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.

### <a name="installation-via-direct-download---debian-8"></a>Instalace přes přímé stažení – Debian 8

Stáhněte si balíček Debian `powershell_6.1.0-1.debian.8_amd64.deb`
z [uvolní][] stránky do počítače, Debian.

Potom v terminálu spusťte následující:

```sh
sudo dpkg -i powershell_6.1.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> `dpkg -i` Příkaz selže s dosud nevyřešených závislosti.
> Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.

### <a name="uninstallation---debian-8"></a>Odinstalace – Debian 8

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a>Debian 9

### <a name="installation-via-package-repository---debian-9"></a>Instalace přes úložiště balíčků – Debian 9

PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).
Toto je upřednostňovaná metoda.

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl gnupg apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.

### <a name="installation-via-direct-download---debian-9"></a>Instalace přes přímé stažení – Debian 9

Stáhněte si balíček Debian `powershell_6.1.0-1.debian.9_amd64.deb`
z [uvolní][] stránky do počítače, Debian.

Potom v terminálu spusťte následující:

```sh
sudo dpkg -i powershell_6.1.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a>Odinstalace – Debian 9

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a>CentOS 7

> [!NOTE]
> Tento balíček funguje taky na Oracle Linux 7.

### <a name="installation-via-package-repository-preferred---centos-7"></a>Instalace přes úložiště balíčků (upřednostňováno) - CentOS 7

PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.

### <a name="installation-via-direct-download---centos-7"></a>Instalace přes přímé stažení - CentOS 7

Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.1.0-1.rhel.7.x86_64.rpm`
z [uvolní][] stránky do počítače CentOS.

Potom v terminálu spusťte následující:

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

Můžete také nainstalovat RPM bez přechodný krok stahování ho:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a>Odinstalace - CentOS 7

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a>Red Hat Enterprise Linux (RHEL) 7

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a>Instalace přes úložiště balíčků (upřednostňováno) – Red Hat Enterprise Linux (RHEL) 7

PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a>Instalace přes přímé stažení – Red Hat Enterprise Linux (RHEL) 7

Stáhněte si balíček RPM `powershell-6.1.0-1.rhel.7.x86_64.rpm`
z [uvolní][] stránky do počítače, Red Hat Enterprise Linux.

Potom v terminálu spusťte následující:

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

Můžete také nainstalovat RPM bez přechodný krok stahování ho:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a>Odinstalace – Red Hat Enterprise Linux (RHEL) 7

```sh
sudo yum remove powershell
```

## <a name="opensuse-423"></a>OpenSUSE 42.3

Když instalace Powershellu Core `zypper` může nahlaste mu následující chybu:

```Output
Problem: nothing provides libcurl needed by powershell-6.1.0-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.1.0-1.rhel.7.x86_64
 Solution 2: break powershell-6.1.0-1.rhel.7.x86_64 by ignoring some of its dependencies
```

V takovém případě ověřte, že kompatibilní `libcurl` knihovna je k dispozici tak, že zkontrolujete, že následující příkaz ukazuje `libcurl4` zabalit jako nainstalovaní:

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

Klikněte na tlačítko `break powershell-6.1.0-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci balíčků prostředí PowerShell.

### <a name="installation-via-package-repository-preferred---opensuse-423"></a>Instalace přes úložiště balíčků (upřednostňováno) - OpenSUSE 42.3

PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Repository
zypper ar https://packages.microsoft.com/rhel/7/prod/

# Update the list of products
sudo zypper update

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-423"></a>Instalace přes přímé stažení - OpenSUSE 42.3

Stáhněte si balíček RPM `powershell-6.1.0-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače OpenSUSE.

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

Můžete také nainstalovat RPM bez přechodný krok stahování ho:

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-423"></a>Odinstalace - OpenSUSE 42.3

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a>Fedora

> [!NOTE]
> Fedora 28 je podporována pouze v prostředí PowerShell Core 6.1 a novější.

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a>Instalace přes úložiště balíčků (upřednostňováno) - Fedora 27 Fedora 28

PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install a system component
sudo dnf install compat-openssl10

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a>Instalace přes přímé stažení - Fedora 27, Fedora 28

Stáhněte si balíček RPM `powershell-6.1.0-1.rhel.7.x86_64.rpm`
z [uvolní][] stránky do počítače, Fedora.

Potom v terminálu spusťte následující:

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

Můžete také nainstalovat RPM bez přechodný krok stahování ho:

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a>Odinstalace - Fedora 27, Fedora 28

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a>Arch Linux

> [!NOTE]
> Podpora architektury je experimentální.

PowerShell je k dispozici [Arch Linux][] úložišti uživatele (AUR).

* Může být zkompilován s [označené nejnovější verzi][arch-release]
* Mohou být zkompilovány z [nejnovější potvrzení změn do hlavní větve][arch-git]
* Nainstalujete ho pomocí [nejnovější verze binárního souboru][arch-bin]

Balíčky AUR jsou komunity udržuje – neexistuje žádná oficiální podpora.

Další informace o instalaci balíčků z AUR najdete v tématu [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunitou [soubor DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a>Přichytit balíčku

### <a name="getting-snapd"></a>Získávání snapd

`snapd` je požadován pro spuštění při kolika rozehrávkách byli.
Použití [tyto pokyny](https://docs.snapcraft.io/core/install) abyste měli jistotu, že máte `snapd` nainstalované.

### <a name="installation-via-snap"></a>Instalace přes modul Snap

PowerShell Core pro Linux, je publikovaná [Snap úložiště](https://snapcraft.io/store) Snadná instalace (a aktualizace).
Toto je upřednostňovaná metoda.

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

Po instalaci modulu Snap budou automaticky upgradovat, ale můžete aktivovat upgradu pomocí `sudo snap refresh powershell-preview`.

### <a name="uninstallation"></a>Odinstalace

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a>Kali

### <a name="installation"></a>Instalace

```sh
# Download & Install prerequisites
wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu57_57.1-9_amd64.deb
dpkg -i libicu57_57.1-9_amd64.deb
apt-get update && apt-get install -y curl gnupg apt-transport-https

# Add Microsoft public repository key to APT
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

# Add Microsoft package repository to the source list
echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" | tee /etc/apt/sources.list.d/powershell.list

# Install PowerShell package
apt-get update && apt-get install -y powershell

# Start PowerShell
pwsh
```

### <a name="uninstallation---kali"></a>Odinstalace - Kali

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a>Raspbian

> [!NOTE]
> Podpora Raspbian je experimentální.

Prostředí PowerShell je v současné době podporována pouze na Raspbian Stretch.

Také CoreCLR (a tedy PowerShell Core) bude fungovat jenom na zařízeních Pi 2 a Pi 3 jako jiná zařízení, jako je třeba [Pi nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesor.

Stáhněte si [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) zobrazíte na vaše číslo pí.

### <a name="installation"></a>Instalace

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.1.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty ke "pwsh" binární

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a>Odinstalace - Raspbian

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a>Binární archivy

Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformy Linux umožňuje pokročilé scénáře nasazení.

### <a name="dependencies"></a>Závislosti

Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce Linuxu.
Ale modulu runtime .NET Core vyžaduje různých závislostí v různých distribucích a proto Powershellu dělá to samé.

Následující graf ukazuje závislosti rozhraní .NET Core 2.0, oficiálně podporované v různých distribucích systému Linux.

| Operační systém                 | Závislosti |
| ------------------ | ------------ |
| Ubuntu 14.04       | libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6 <br> libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Ubuntu 16.04       | libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6 <br> libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55 |
| Ubuntu 17.10       | libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6 <br> libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57 |
| Ubuntu 18.04       | libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6 <br> libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60 |
| Debian 8 (Jessie)  | libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6 <br> libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Debian 9 (roztáhnout) | libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6 <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57 |
| CentOS 7 <br> Oracle Linux 7 <br> RHEL 7 <br> OpenSUSE OpenSUSE 42.3 | libunwind libcurl, knihovny openssl, libicu |
| Fedora 27 <br> Fedora 28 | libunwind libcurl, knihovny openssl, libicu, compat openssl10 |

K nasazení binárních souborů prostředí PowerShell v Linuxových distribucích, které nejsou oficiálně podporované, budete muset nainstalovat potřebné závislosti pro cílový operační systém v samostatných krocích.
Například náš [soubor dockerfile Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a poté rozbalí Linuxový `tar.gz` archivu.

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a>Instalace - binární archivy

#### <a name="linux"></a>Linux

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.1.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.1.0

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.1.0/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a>Probíhá odinstalace binárního archivy

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a>Cesty

* `$PSHOME` je `/opt/microsoft/powershell/6.1.0/`
* Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`
* Výchozí profily se budou číst z `$PSHOME/profile.ps1`
* Moduly uživatele bude číst z `~/.local/share/powershell/Modules`
* Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`
* Výchozí moduly se budou číst z `$PSHOME/Modules`
* Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

Profily respektovat konfigurace Powershellu na hostitele, takže výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.

Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v Linuxu.

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

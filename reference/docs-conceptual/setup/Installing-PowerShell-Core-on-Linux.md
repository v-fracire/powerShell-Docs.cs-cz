# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="c42a0-101">Instalace PowerShellu Core v Linuxu</span><span class="sxs-lookup"><span data-stu-id="c42a0-101">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="c42a0-102">Podporuje [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27 ] [ fedora], [Fedora 28][fedora], a [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="c42a0-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="c42a0-103">Pro distribuce Linuxu, které nejsou oficiálně podporované, můžete zkusit použít [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="c42a0-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="c42a0-104">Nasazení prostředí PowerShell binární soubory přímo s Linuxem můžete také zkusit [ `tar.gz` archivu][tar], ale je potřeba nastavit potřebné závislosti podle operačního systému v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="c42a0-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="c42a0-105">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="c42a0-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="c42a0-106">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1710
[u18]: #ubuntu-1804
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-423
[fedora]: #fedora
[arch]: #arch-linux
[lai]: #linux-appimage
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="c42a0-107">Instalace Preview verzí</span><span class="sxs-lookup"><span data-stu-id="c42a0-107">Installing Preview Releases</span></span>

<span data-ttu-id="c42a0-108">Při instalaci verze Preview prostředí PowerShell Core pro Linux přes úložiště balíčků, názvu balíčku se změní z `powershell` k `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="c42a0-108">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="c42a0-109">Instalace přes přímé stažení nezmění, než je název souboru.</span><span class="sxs-lookup"><span data-stu-id="c42a0-109">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="c42a0-110">Tady je tabulka znázorňující příkazy, abyste nainstalovali stabilní verze a preview balíčků pomocí různých správců balíčků:</span><span class="sxs-lookup"><span data-stu-id="c42a0-110">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="c42a0-111">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="c42a0-111">Distribution(s)</span></span>|<span data-ttu-id="c42a0-112">Stabilní příkaz</span><span class="sxs-lookup"><span data-stu-id="c42a0-112">Stable Command</span></span> | <span data-ttu-id="c42a0-113">Příkaz ve verzi Preview</span><span class="sxs-lookup"><span data-stu-id="c42a0-113">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="c42a0-114">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="c42a0-114">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="c42a0-115">CentOS, Red Hat</span><span class="sxs-lookup"><span data-stu-id="c42a0-115">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="c42a0-116">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="c42a0-116">OpenSUSE</span></span> |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| <span data-ttu-id="c42a0-117">Fedora</span><span class="sxs-lookup"><span data-stu-id="c42a0-117">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="c42a0-118">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-118">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="c42a0-119">Instalace přes úložiště balíčků – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-119">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="c42a0-120">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c42a0-121">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c42a0-121">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c42a0-122">Jako superuživatele zaregistrujte úložiště společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c42a0-122">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="c42a0-123">Od té chvíle stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.</span><span class="sxs-lookup"><span data-stu-id="c42a0-123">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="c42a0-124">Instalace přes přímé stažení – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-124">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="c42a0-125">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-125">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c42a0-126">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-126">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c42a0-127">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c42a0-127">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c42a0-128">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-128">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="c42a0-129">Odinstalace – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-129">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="c42a0-130">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-130">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="c42a0-131">Instalace přes úložiště balíčků – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-131">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="c42a0-132">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-132">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c42a0-133">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c42a0-133">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/16.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c42a0-134">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c42a0-134">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="c42a0-135">Instalace přes přímé stažení – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-135">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="c42a0-136">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-136">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c42a0-137">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-137">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c42a0-138">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c42a0-138">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c42a0-139">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-139">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="c42a0-140">Odinstalace – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-140">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1710"></a><span data-ttu-id="c42a0-141">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="c42a0-141">Ubuntu 17.10</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-142">Přidali jsme podporu pro Ubuntu č. 17.04 po `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="c42a0-142">Support for Ubuntu 17.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1710"></a><span data-ttu-id="c42a0-143">Instalace přes úložiště balíčků – Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="c42a0-143">Installation via Package Repository - Ubuntu 17.10</span></span>

<span data-ttu-id="c42a0-144">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-144">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c42a0-145">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c42a0-145">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/17.10/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c42a0-146">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c42a0-146">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1710"></a><span data-ttu-id="c42a0-147">Instalace přes přímé stažení – Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="c42a0-147">Installation via Direct Download - Ubuntu 17.10</span></span>

<span data-ttu-id="c42a0-148">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-148">Download the Debian package `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c42a0-149">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-149">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.10_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c42a0-150">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c42a0-150">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c42a0-151">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-151">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1710"></a><span data-ttu-id="c42a0-152">Odinstalace – Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="c42a0-152">Uninstallation - Ubuntu 17.10</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="c42a0-153">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-153">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-154">Přidali jsme podporu pro Ubuntu 18.04 po `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="c42a0-154">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="c42a0-155">Instalace přes úložiště balíčků – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-155">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="c42a0-156">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-156">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c42a0-157">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c42a0-157">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell-preview

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="c42a0-158">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c42a0-158">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="c42a0-159">Instalace přes přímé stažení – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-159">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="c42a0-160">Stáhněte si balíček Debian `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-160">Download the Debian package `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c42a0-161">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-161">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c42a0-162">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c42a0-162">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c42a0-163">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-163">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="c42a0-164">Odinstalace – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-164">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="c42a0-165">Debian 8</span><span class="sxs-lookup"><span data-stu-id="c42a0-165">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="c42a0-166">Instalace přes úložiště balíčků – Debian 8</span><span class="sxs-lookup"><span data-stu-id="c42a0-166">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="c42a0-167">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-167">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c42a0-168">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c42a0-168">This is the preferred method.</span></span>

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

<span data-ttu-id="c42a0-169">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c42a0-169">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="c42a0-170">Instalace přes přímé stažení – Debian 8</span><span class="sxs-lookup"><span data-stu-id="c42a0-170">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="c42a0-171">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.8_amd64.deb` z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="c42a0-171">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="c42a0-172">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-172">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c42a0-173">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c42a0-173">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c42a0-174">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-174">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="c42a0-175">Odinstalace – Debian 8</span><span class="sxs-lookup"><span data-stu-id="c42a0-175">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="c42a0-176">Debian 9</span><span class="sxs-lookup"><span data-stu-id="c42a0-176">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="c42a0-177">Instalace přes úložiště balíčků – Debian 9</span><span class="sxs-lookup"><span data-stu-id="c42a0-177">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="c42a0-178">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-178">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c42a0-179">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c42a0-179">This is the preferred method.</span></span>

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

<span data-ttu-id="c42a0-180">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c42a0-180">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="c42a0-181">Instalace přes přímé stažení – Debian 9</span><span class="sxs-lookup"><span data-stu-id="c42a0-181">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="c42a0-182">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.9_amd64.deb` z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="c42a0-182">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="c42a0-183">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-183">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="c42a0-184">Odinstalace – Debian 9</span><span class="sxs-lookup"><span data-stu-id="c42a0-184">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="c42a0-185">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-185">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-186">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="c42a0-186">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="c42a0-187">Instalace přes úložiště balíčků (upřednostňováno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-187">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="c42a0-188">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-188">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c42a0-189">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-189">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="c42a0-190">Instalace přes přímé stažení - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-190">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="c42a0-191">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače CentOS.</span><span class="sxs-lookup"><span data-stu-id="c42a0-191">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="c42a0-192">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-192">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c42a0-193">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c42a0-193">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="c42a0-194">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-194">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c42a0-196">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-196">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c42a0-197">Instalace přes úložiště balíčků (upřednostňováno) – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-197">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="c42a0-198">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-198">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c42a0-199">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-199">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c42a0-200">Instalace přes přímé stažení – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-200">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="c42a0-201">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače, Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="c42a0-201">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="c42a0-202">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-202">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c42a0-203">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c42a0-203">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c42a0-204">Odinstalace – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-204">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-423"></a><span data-ttu-id="c42a0-205">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c42a0-205">OpenSUSE 42.3</span></span>

<span data-ttu-id="c42a0-206">Když instalace Powershellu Core `zypper` může nahlaste mu následující chybu:</span><span class="sxs-lookup"><span data-stu-id="c42a0-206">When installing PowerShell Core, `zypper` may report the following error:</span></span>

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

<span data-ttu-id="c42a0-207">V takovém případě ověřte, že kompatibilní `libcurl` knihovna je k dispozici tak, že zkontrolujete, že následující příkaz ukazuje `libcurl4` zabalit jako nainstalovaní:</span><span class="sxs-lookup"><span data-stu-id="c42a0-207">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

<span data-ttu-id="c42a0-208">Klikněte na tlačítko `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci balíčků prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c42a0-208">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-423"></a><span data-ttu-id="c42a0-209">Instalace přes úložiště balíčků (upřednostňováno) - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c42a0-209">Installation via Package Repository (preferred) - OpenSUSE 42.3</span></span>

<span data-ttu-id="c42a0-210">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-210">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-423"></a><span data-ttu-id="c42a0-211">Instalace přes přímé stažení - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c42a0-211">Installation via Direct Download - OpenSUSE 42.3</span></span>

<span data-ttu-id="c42a0-212">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="c42a0-212">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c42a0-213">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c42a0-213">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-423"></a><span data-ttu-id="c42a0-214">Odinstalace - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c42a0-214">Uninstallation - OpenSUSE 42.3</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="c42a0-215">Fedora</span><span class="sxs-lookup"><span data-stu-id="c42a0-215">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-216">Fedora 28 je podporována pouze v prostředí PowerShell Core 6.1 a novější.</span><span class="sxs-lookup"><span data-stu-id="c42a0-216">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="c42a0-217">Instalace přes úložiště balíčků (upřednostňováno) - Fedora 27 Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c42a0-217">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="c42a0-218">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c42a0-218">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="c42a0-219">Instalace přes přímé stažení - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c42a0-219">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="c42a0-220">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače, Fedora.</span><span class="sxs-lookup"><span data-stu-id="c42a0-220">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="c42a0-221">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-221">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c42a0-222">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c42a0-222">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="c42a0-223">Odinstalace - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c42a0-223">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="c42a0-224">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="c42a0-224">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-225">Podpora architektury je experimentální.</span><span class="sxs-lookup"><span data-stu-id="c42a0-225">Arch support is experimental.</span></span>

<span data-ttu-id="c42a0-226">PowerShell je k dispozici [Arch Linux][] úložišti uživatele (AUR).</span><span class="sxs-lookup"><span data-stu-id="c42a0-226">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="c42a0-227">Může být zkompilován s [označené nejnovější verzi][arch-release]</span><span class="sxs-lookup"><span data-stu-id="c42a0-227">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="c42a0-228">Mohou být zkompilovány z [nejnovější potvrzení změn do hlavní větve][arch-git]</span><span class="sxs-lookup"><span data-stu-id="c42a0-228">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="c42a0-229">Nainstalujete ho pomocí [nejnovější verze binárního souboru][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="c42a0-229">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="c42a0-230">Balíčky AUR jsou komunity udržuje – neexistuje žádná oficiální podpora.</span><span class="sxs-lookup"><span data-stu-id="c42a0-230">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="c42a0-231">Další informace o instalaci balíčků z AUR najdete v tématu [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunitou [soubor DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="c42a0-231">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="c42a0-233">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="c42a0-233">Linux AppImage</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-234">Podpora AppImage je experimentální</span><span class="sxs-lookup"><span data-stu-id="c42a0-234">AppImage support is experimental</span></span>

<span data-ttu-id="c42a0-235">Pomocí nejnovější distribuce Linuxu, stáhněte si AppImage `powershell-6.0.1-x86_64.AppImage` z [uvolní][] stránky na počítači s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="c42a0-235">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="c42a0-236">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c42a0-236">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="c42a0-237">[AppImage][] umožňuje spustit prostředí PowerShell bez nutnosti jeho instalace.</span><span class="sxs-lookup"><span data-stu-id="c42a0-237">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="c42a0-238">Je přenosné aplikace, která obsahuje ureitou prostředí PowerShell a jeho závislosti (včetně .NET Core závislosti systému) do jednoho získá na ucelenosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="c42a0-238">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="c42a0-239">Tento balíček je jeden binární soubor, který funguje nezávisle na Linuxové distribuci daného uživatele.</span><span class="sxs-lookup"><span data-stu-id="c42a0-239">This package is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="c42a0-241">Kali</span><span class="sxs-lookup"><span data-stu-id="c42a0-241">Kali</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-242">Podpora Kali je experimentální.</span><span class="sxs-lookup"><span data-stu-id="c42a0-242">Kali support is experimental.</span></span>

### <a name="installation"></a><span data-ttu-id="c42a0-243">Instalace</span><span class="sxs-lookup"><span data-stu-id="c42a0-243">Installation</span></span>

```sh
# Download & Install prerequisites
sudo apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Install PowerShell
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="c42a0-244">Spusťte prostředí PowerShell v nejnovější Kali (Kali GNU/Linux se zajištěním provozu) bez nutnosti jeho instalace</span><span class="sxs-lookup"><span data-stu-id="c42a0-244">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="c42a0-245">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="c42a0-245">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="c42a0-246">Raspbian</span><span class="sxs-lookup"><span data-stu-id="c42a0-246">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="c42a0-247">Podpora Raspbian je experimentální.</span><span class="sxs-lookup"><span data-stu-id="c42a0-247">Raspbian support is experimental.</span></span>

<span data-ttu-id="c42a0-248">Prostředí PowerShell je v současné době podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="c42a0-248">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="c42a0-249">Také CoreCLR (a tedy PowerShell Core) bude fungovat jenom na zařízeních Pi 2 a Pi 3 jako jiná zařízení, jako je třeba [Pi nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesor.</span><span class="sxs-lookup"><span data-stu-id="c42a0-249">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="c42a0-250">Stáhněte si [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) zobrazíte na vaše číslo pí.</span><span class="sxs-lookup"><span data-stu-id="c42a0-250">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="c42a0-251">Instalace</span><span class="sxs-lookup"><span data-stu-id="c42a0-251">Installation</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.2-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

<span data-ttu-id="c42a0-252">Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty ke "pwsh" binární</span><span class="sxs-lookup"><span data-stu-id="c42a0-252">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="c42a0-253">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="c42a0-253">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="c42a0-254">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="c42a0-254">Binary Archives</span></span>

<span data-ttu-id="c42a0-255">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformy Linux umožňuje pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="c42a0-255">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="c42a0-256">Závislosti</span><span class="sxs-lookup"><span data-stu-id="c42a0-256">Dependencies</span></span>

<span data-ttu-id="c42a0-257">Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce Linuxu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-257">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="c42a0-258">Ale modulu runtime .NET Core vyžaduje různých závislostí v různých distribucích a proto Powershellu dělá to samé.</span><span class="sxs-lookup"><span data-stu-id="c42a0-258">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="c42a0-259">Následující graf ukazuje závislosti rozhraní .NET Core 2.0, oficiálně podporované v různých distribucích systému Linux.</span><span class="sxs-lookup"><span data-stu-id="c42a0-259">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="c42a0-260">Operační systém</span><span class="sxs-lookup"><span data-stu-id="c42a0-260">OS</span></span>                 | <span data-ttu-id="c42a0-261">Závislosti</span><span class="sxs-lookup"><span data-stu-id="c42a0-261">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="c42a0-262">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-262">Ubuntu 14.04</span></span>       | <span data-ttu-id="c42a0-263">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c42a0-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c42a0-264">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="c42a0-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="c42a0-265">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-265">Ubuntu 16.04</span></span>       | <span data-ttu-id="c42a0-266">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c42a0-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c42a0-267">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="c42a0-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="c42a0-268">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="c42a0-268">Ubuntu 17.10</span></span>       | <span data-ttu-id="c42a0-269">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c42a0-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c42a0-270">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="c42a0-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="c42a0-271">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c42a0-271">Ubuntu 18.04</span></span>       | <span data-ttu-id="c42a0-272">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c42a0-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c42a0-273">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="c42a0-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="c42a0-274">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="c42a0-274">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="c42a0-275">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c42a0-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c42a0-276">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="c42a0-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="c42a0-277">Debian 9 (roztáhnout)</span><span class="sxs-lookup"><span data-stu-id="c42a0-277">Debian 9 (Stretch)</span></span> | <span data-ttu-id="c42a0-278">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c42a0-278">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c42a0-279">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="c42a0-279">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="c42a0-280">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-280">CentOS 7</span></span> <br> <span data-ttu-id="c42a0-281">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-281">Oracle Linux 7</span></span> <br> <span data-ttu-id="c42a0-282">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="c42a0-282">RHEL 7</span></span> <br> <span data-ttu-id="c42a0-283">OpenSUSE OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c42a0-283">OpenSUSE OpenSUSE 42.3</span></span> | <span data-ttu-id="c42a0-284">libunwind libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="c42a0-284">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="c42a0-285">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="c42a0-285">Fedora 27</span></span> <br> <span data-ttu-id="c42a0-286">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c42a0-286">Fedora 28</span></span> | <span data-ttu-id="c42a0-287">libunwind libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="c42a0-287">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="c42a0-288">K nasazení binárních souborů prostředí PowerShell v Linuxových distribucích, které nejsou oficiálně podporované, budete muset nainstalovat potřebné závislosti pro cílový operační systém v samostatných krocích.</span><span class="sxs-lookup"><span data-stu-id="c42a0-288">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="c42a0-289">Například náš [soubor dockerfile Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a poté rozbalí Linuxový `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-289">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="c42a0-290">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="c42a0-290">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="c42a0-291">Linux</span><span class="sxs-lookup"><span data-stu-id="c42a0-291">Linux</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.0.2

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.0.2

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/6.0.2/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.0.2/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="c42a0-292">Probíhá odinstalace binárního archivy</span><span class="sxs-lookup"><span data-stu-id="c42a0-292">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="c42a0-293">Cesty</span><span class="sxs-lookup"><span data-stu-id="c42a0-293">Paths</span></span>

* <span data-ttu-id="c42a0-294">`$PSHOME` je `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="c42a0-294">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="c42a0-295">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="c42a0-295">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="c42a0-296">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="c42a0-296">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="c42a0-297">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="c42a0-297">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="c42a0-298">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="c42a0-298">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="c42a0-299">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="c42a0-299">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="c42a0-300">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="c42a0-300">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="c42a0-301">Profily respektovat konfigurace Powershellu na hostitele, takže výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="c42a0-301">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="c42a0-302">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v Linuxu.</span><span class="sxs-lookup"><span data-stu-id="c42a0-302">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

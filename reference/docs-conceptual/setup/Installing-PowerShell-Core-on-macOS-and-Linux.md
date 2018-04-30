# <a name="installing-powershell-core-on-macos-and-linux"></a><span data-ttu-id="6171c-101">Instalace PowerShellu Core v macOS a Linuxu</span><span class="sxs-lookup"><span data-stu-id="6171c-101">Installing PowerShell Core on macOS and Linux</span></span>

<span data-ttu-id="6171c-102">Podporuje [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu č. 17.04] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25 ] [ fed25], [Fedora 26][fed26], [Arch Linux][arch]a [systému macOS 10.12][mac].</span><span class="sxs-lookup"><span data-stu-id="6171c-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], [Arch Linux][arch], and [macOS 10.12][mac].</span></span>

<span data-ttu-id="6171c-103">Pro Linux distribuce, které nejsou oficiálně podporované, můžete se pokusit [prostředí PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="6171c-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span> <span data-ttu-id="6171c-104">Můžete také zkusit nasazení binárních souborů prostředí PowerShell přímo pomocí sady Linux [ `tar.gz` archivu][tar], ale je potřeba nastavit podle operačního systému v samostatné kroky potřebné závislosti.</span><span class="sxs-lookup"><span data-stu-id="6171c-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="6171c-105">Všechny balíčky jsou k dispozici na našem Githubu [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="6171c-105">All packages are available on our GitHub [releases][] page.</span></span> <span data-ttu-id="6171c-106">Spustit po instalaci balíčku `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="6171c-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1704
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fed25]: #fedora-25
[fed26]: #fedora-26
[arch]: #arch-linux
[lai]: #linux-appimage
[mac]: #macos-1012
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="6171c-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6171c-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="6171c-108">Instalaci přes úložiště balíčků - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6171c-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="6171c-109">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span> <span data-ttu-id="6171c-110">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="6171c-110">This is the preferred method.</span></span>

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

<span data-ttu-id="6171c-111">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="6171c-111">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="6171c-112">Instalace prostřednictvím přímé stahování - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6171c-112">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="6171c-113">Stáhněte si balíček Debian `powershell_6.0.0-1.ubuntu.14.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6171c-113">Download the Debian package `powershell_6.0.0-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.14.04_amd64.deb
```

<span data-ttu-id="6171c-114">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-114">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6171c-115">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6171c-115">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="6171c-116">Odinstalace - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6171c-116">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="6171c-117">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6171c-117">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="6171c-118">Instalaci přes úložiště balíčků - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6171c-118">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="6171c-119">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-119">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6171c-120">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="6171c-120">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6171c-121">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="6171c-121">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="6171c-122">Instalace prostřednictvím přímé stahování - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6171c-122">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="6171c-123">Stáhněte si balíček Debian `powershell_6.0.0-1.ubuntu.16.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="6171c-123">Download the Debian package `powershell_6.0.0-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
```

<span data-ttu-id="6171c-124">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-124">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6171c-125">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6171c-125">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="6171c-126">Odinstalace - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6171c-126">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="6171c-127">Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="6171c-127">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="6171c-128">Instalaci přes úložiště balíčků - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="6171c-128">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="6171c-129">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-129">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6171c-130">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="6171c-130">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/17.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6171c-131">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="6171c-131">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="6171c-132">Instalace prostřednictvím přímé stahování - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="6171c-132">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="6171c-133">Stáhněte si balíček Debian `powershell_6.0.0-1.ubuntu.17.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu:</span><span class="sxs-lookup"><span data-stu-id="6171c-133">Download the Debian package `powershell_6.0.0-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.17.04_amd64.deb
```

<span data-ttu-id="6171c-134">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-134">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6171c-135">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6171c-135">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="6171c-136">Odinstalace - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="6171c-136">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="6171c-137">Debian 8</span><span class="sxs-lookup"><span data-stu-id="6171c-137">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="6171c-138">Instalaci přes úložiště balíčků - Debian 8</span><span class="sxs-lookup"><span data-stu-id="6171c-138">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="6171c-139">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-139">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6171c-140">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="6171c-140">This is the preferred method.</span></span>

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

<span data-ttu-id="6171c-141">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="6171c-141">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="6171c-142">Instalace prostřednictvím přímé stahování - Debian 8</span><span class="sxs-lookup"><span data-stu-id="6171c-142">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="6171c-143">Stáhněte si balíček Debian `powershell_6.0.0-1.debian.8_amd64.deb` z [uvolní][] stránky do Debian počítače:</span><span class="sxs-lookup"><span data-stu-id="6171c-143">Download the Debian package `powershell_6.0.0-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.8_amd64.deb
```

<span data-ttu-id="6171c-144">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-144">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6171c-145">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6171c-145">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="6171c-146">Odinstalace - Debian 8</span><span class="sxs-lookup"><span data-stu-id="6171c-146">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="6171c-147">Debian 9</span><span class="sxs-lookup"><span data-stu-id="6171c-147">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="6171c-148">Instalaci přes úložiště balíčků - Debian 9</span><span class="sxs-lookup"><span data-stu-id="6171c-148">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="6171c-149">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-149">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6171c-150">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="6171c-150">This is the preferred method.</span></span>

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

<span data-ttu-id="6171c-151">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="6171c-151">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="6171c-152">Instalace prostřednictvím přímé stahování - Debian 9</span><span class="sxs-lookup"><span data-stu-id="6171c-152">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="6171c-153">Stáhněte si balíček Debian `powershell_6.0.0-1.debian.9_amd64.deb` z [uvolní][] stránky do Debian počítače:</span><span class="sxs-lookup"><span data-stu-id="6171c-153">Download the Debian package `powershell_6.0.0-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

<span data-ttu-id="6171c-154">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-154">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6171c-155">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6171c-155">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="6171c-156">Odinstalace - Debian 9</span><span class="sxs-lookup"><span data-stu-id="6171c-156">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="6171c-157">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6171c-157">CentOS 7</span></span>

> <span data-ttu-id="6171c-158">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="6171c-158">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="6171c-159">Instalaci přes úložiště balíčků (doporučeno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6171c-159">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="6171c-160">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-160">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6171c-161">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6171c-161">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="6171c-162">Instalace prostřednictvím přímé stahování - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6171c-162">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="6171c-163">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače CentOS:</span><span class="sxs-lookup"><span data-stu-id="6171c-163">Using [CentOS 7][], download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-164">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-164">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-165">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="6171c-165">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="6171c-166">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6171c-166">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6171c-168">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6171c-168">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6171c-169">Instalaci přes úložiště balíčků (doporučeno) - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6171c-169">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="6171c-170">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-170">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6171c-171">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6171c-171">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6171c-172">Instalace prostřednictvím přímé stahování - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6171c-172">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="6171c-173">Stáhněte si balíček RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Red Hat Enterprise Linux:</span><span class="sxs-lookup"><span data-stu-id="6171c-173">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

<span data-ttu-id="6171c-174">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-174">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-175">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="6171c-175">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6171c-176">Odinstalace - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6171c-176">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="6171c-177">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6171c-177">OpenSUSE 42.2</span></span>

> <span data-ttu-id="6171c-178">**Poznámka:** při instalaci prostředí PowerShell základní `zypper` může nahlaste mu následující chybu:</span><span class="sxs-lookup"><span data-stu-id="6171c-178">**Note:** When installing PowerShell Core, `zypper` may report the following error:</span></span>
>
> ```text
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> <span data-ttu-id="6171c-179">V takovém případě ověřte, že kompatibilní `libcurl` knihovny nachází kontrolou, že následující příkaz ukazuje `libcurl4` balíčku se po instalaci:</span><span class="sxs-lookup"><span data-stu-id="6171c-179">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> <span data-ttu-id="6171c-180">Zvolte `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci `powershell` balíčku.</span><span class="sxs-lookup"><span data-stu-id="6171c-180">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the `powershell` package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="6171c-181">Instalaci přes úložiště balíčků (doporučeno) - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6171c-181">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="6171c-182">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-182">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Product feed
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/zypp/repos.d/microsoft.repo

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="6171c-183">Instalace prostřednictvím přímé stahování - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6171c-183">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="6171c-184">Stáhněte si balíček RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače OpenSUSE:</span><span class="sxs-lookup"><span data-stu-id="6171c-184">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-185">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="6171c-185">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="6171c-186">Odinstalace - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6171c-186">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora-25"></a><span data-ttu-id="6171c-187">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6171c-187">Fedora 25</span></span>

### <a name="installation-via-package-repository-preferred---fedora-25"></a><span data-ttu-id="6171c-188">Instalaci přes úložiště balíčků (doporučeno) - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6171c-188">Installation via Package Repository (preferred) - Fedora 25</span></span>

<span data-ttu-id="6171c-189">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-189">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-25"></a><span data-ttu-id="6171c-190">Instalace prostřednictvím přímé stahování - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6171c-190">Installation via Direct Download - Fedora 25</span></span>

<span data-ttu-id="6171c-191">Stáhněte si balíček RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Fedora:</span><span class="sxs-lookup"><span data-stu-id="6171c-191">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-192">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-192">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-193">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="6171c-193">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-25"></a><span data-ttu-id="6171c-194">Odinstalace - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6171c-194">Uninstallation - Fedora 25</span></span>

```sh
sudo dnf remove powershell
```

## <a name="fedora-26"></a><span data-ttu-id="6171c-195">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6171c-195">Fedora 26</span></span>

### <a name="installation-via-package-repository-preferred---fedora-26"></a><span data-ttu-id="6171c-196">Instalaci přes úložiště balíčků (doporučeno) - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6171c-196">Installation via Package Repository (preferred) - Fedora 26</span></span>

<span data-ttu-id="6171c-197">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="6171c-197">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-26"></a><span data-ttu-id="6171c-198">Instalace prostřednictvím přímé stahování - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6171c-198">Installation via Direct Download - Fedora 26</span></span>

<span data-ttu-id="6171c-199">Stáhněte si balíček RPM `powershell-6.0.0-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Fedora:</span><span class="sxs-lookup"><span data-stu-id="6171c-199">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-200">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-200">Then execute the following in the terminal:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6171c-201">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="6171c-201">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-26"></a><span data-ttu-id="6171c-202">Odinstalace - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6171c-202">Uninstallation - Fedora 26</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="6171c-203">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="6171c-203">Arch Linux</span></span>

<span data-ttu-id="6171c-204">PowerShell je k dispozici [architektura Linux][] uživatele úložiště (AUR).</span><span class="sxs-lookup"><span data-stu-id="6171c-204">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="6171c-205">Může být zkompilován s [označené nejnovější verze][arch-release]</span><span class="sxs-lookup"><span data-stu-id="6171c-205">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="6171c-206">Mohou být zkompilovány z [nejnovější potvrzení změn na hlavní server][arch-git]</span><span class="sxs-lookup"><span data-stu-id="6171c-206">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="6171c-207">Můžete nainstalovat, pomocí [nejnovější verzi binární][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="6171c-207">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="6171c-208">Balíčky v AUR jsou udržuje komunitní – neexistuje žádná podpora oficiální.</span><span class="sxs-lookup"><span data-stu-id="6171c-208">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="6171c-209">Další informace o instalaci balíčků z AUR najdete v tématu [architektura Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunity [soubor Docker](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="6171c-209">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[architektura Linux]: https://www.archlinux.org/download/
[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="6171c-211">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="6171c-211">Linux AppImage</span></span>

<span data-ttu-id="6171c-212">Pomocí poslední distribuci systému Linux, stáhněte si AppImage `powershell-6.0.0-x86_64.AppImage` z [uvolní][] stránky do počítače Linux.</span><span class="sxs-lookup"><span data-stu-id="6171c-212">Using a recent Linux distribution, download the AppImage `powershell-6.0.0-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="6171c-213">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-213">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.0-x86_64.AppImage
./powershell-6.0.0-x86_64.AppImage
```

<span data-ttu-id="6171c-214">[AppImage][] vám umožní spustit prostředí PowerShell bez jeho instalaci.</span><span class="sxs-lookup"><span data-stu-id="6171c-214">The [AppImage][] lets you run PowerShell without installing it.</span></span> <span data-ttu-id="6171c-215">Je přenosné aplikace, která obsahuje ureitou prostředí PowerShell a jeho závislosti (včetně závislostí systému .NET Core) do jednoho získá na ucelenosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="6171c-215">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span> <span data-ttu-id="6171c-216">Tento balíček funguje nezávisle na distribuční Linux uživatele a je jediné binární.</span><span class="sxs-lookup"><span data-stu-id="6171c-216">This package works independently of the user's Linux distribution, and is a single binary.</span></span>

[appimage]: http://appimage.org/

## <a name="macos-1012"></a><span data-ttu-id="6171c-218">systému macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="6171c-218">macOS 10.12</span></span>

### <a name="installation-via-homebrew-preferred---macos-1012"></a><span data-ttu-id="6171c-219">Instalaci přes Homebrew (doporučeno) - systému macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="6171c-219">Installation via Homebrew (preferred) - macOS 10.12</span></span>

<span data-ttu-id="6171c-220">[Homebrew] [ brew] je chybějící Správce balíčků pro systému macOS.</span><span class="sxs-lookup"><span data-stu-id="6171c-220">[Homebrew][brew] is the missing package manager for macOS.</span></span> <span data-ttu-id="6171c-221">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="6171c-221">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="6171c-222">Jakmile jste nainstalovali Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="6171c-222">Once you've installed Homebrew, installing PowerShell is easy.</span></span> <span data-ttu-id="6171c-223">Nejdřív nainstalujte [obalového Homebrew souboru][cask], takže můžete nainstalovat další balíčky:</span><span class="sxs-lookup"><span data-stu-id="6171c-223">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="6171c-224">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6171c-224">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="6171c-225">Když jsou vydávány nové verze prostředí PowerShell, jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6171c-225">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> <span data-ttu-id="6171c-226">Poznámka: Výše uvedené příkazy lze volat z v rámci hostitele prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a dokončete upgrade a aktualizujte hodnoty zobrazené v $PSVersionTable opětovný vstup.</span><span class="sxs-lookup"><span data-stu-id="6171c-226">Note: The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and re-entered to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download---macos-1012"></a><span data-ttu-id="6171c-227">Instalace prostřednictvím přímé stáhnout - systému macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="6171c-227">Installation via Direct Download - macOS 10.12</span></span>

<span data-ttu-id="6171c-228">Pomocí systému macOS 10.12, stáhněte si balíček PKG `powershell-6.0.0-osx.10.12-x64.pkg` z [uvolní][] stránky do systému macOS počítače.</span><span class="sxs-lookup"><span data-stu-id="6171c-228">Using macOS 10.12, download the PKG package `powershell-6.0.0-osx.10.12-x64.pkg` from the [releases][] page onto the macOS machine.</span></span>

<span data-ttu-id="6171c-229">Buď poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="6171c-229">Either double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.0-osx.10.12-x64.pkg -target /
```

### <a name="uninstallation---macos-1012"></a><span data-ttu-id="6171c-230">Odinstalace - systému macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="6171c-230">Uninstallation - macOS 10.12</span></span>

<span data-ttu-id="6171c-231">Pokud jste nainstalovali prostředí PowerShell s Homebrew, je snadné odinstalace:</span><span class="sxs-lookup"><span data-stu-id="6171c-231">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="6171c-232">Pokud jste nainstalovali PowerShell prostřednictvím přímé stahování, musíte ručně odstranit prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6171c-232">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="6171c-233">Chcete-li odinstalovat další cesty prostředí PowerShell (například cesta k profilu uživatele) najdete v tématu [cesty] [ paths] části níže v tomto dokumentu a odeberte požadovanou cesty s `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="6171c-233">To uninstall the additional PowerShell paths (such as the user profile path) please see the [paths][paths] section below in this document and remove the desired the paths with `sudo rm`.</span></span> <span data-ttu-id="6171c-234">(Poznámka: Toto není nutné v případě, že jste nainstalovali s Homebrew.)</span><span class="sxs-lookup"><span data-stu-id="6171c-234">(Note: this is not necessary if you installed with Homebrew.)</span></span>

[paths]:#paths

## <a name="kali"></a><span data-ttu-id="6171c-235">Kali</span><span class="sxs-lookup"><span data-stu-id="6171c-235">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="6171c-236">Instalace</span><span class="sxs-lookup"><span data-stu-id="6171c-236">Installation</span></span>

```sh
# Download & Install prerequisites
sudo apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Download & Install PowerShell
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="6171c-237">Spusťte prostředí PowerShell bez instalace se v nejnovější Kali (vrácení Kali GNU/Linux)</span><span class="sxs-lookup"><span data-stu-id="6171c-237">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.0-x86_64.AppImage

# Start PowerShell
./powershell-6.0.0-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="6171c-238">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="6171c-238">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell-6.0.0-x86_64.AppImage
```

## <a name="raspbian"></a><span data-ttu-id="6171c-239">Raspbian</span><span class="sxs-lookup"><span data-stu-id="6171c-239">Raspbian</span></span>

<span data-ttu-id="6171c-240">V současné době prostředí PowerShell je podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="6171c-240">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

### <a name="installation"></a><span data-ttu-id="6171c-241">Instalace</span><span class="sxs-lookup"><span data-stu-id="6171c-241">Installation</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="6171c-242">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="6171c-242">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="6171c-243">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="6171c-243">Binary Archives</span></span>

<span data-ttu-id="6171c-244">Prostředí PowerShell binární `tar.gz` archivy jsou k dispozici pro systému macOS a platformy Linux k povolení pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="6171c-244">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="6171c-245">Závislosti</span><span class="sxs-lookup"><span data-stu-id="6171c-245">Dependencies</span></span>

<span data-ttu-id="6171c-246">Pro systémy Linux prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce systému Linux.</span><span class="sxs-lookup"><span data-stu-id="6171c-246">For Linux, PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="6171c-247">Ale .NET Core runtime vyžaduje jiný závislosti na různých distribucí, a proto prostředí PowerShell dělá to stejné.</span><span class="sxs-lookup"><span data-stu-id="6171c-247">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="6171c-248">Následující graf zobrazuje rozhraní .NET 2.0 základní závislosti na různých distribucí Linux, které jsou oficiálně podporované.</span><span class="sxs-lookup"><span data-stu-id="6171c-248">The following chart shows the .NET Core 2.0 dependencies on different Linux distributions that are officially supported.</span></span>

| <span data-ttu-id="6171c-249">Operační systém</span><span class="sxs-lookup"><span data-stu-id="6171c-249">OS</span></span>                 | <span data-ttu-id="6171c-250">Závislosti</span><span class="sxs-lookup"><span data-stu-id="6171c-250">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="6171c-251">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6171c-251">Ubuntu 14.04</span></span>       | <span data-ttu-id="6171c-252">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="6171c-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6171c-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="6171c-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="6171c-254">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6171c-254">Ubuntu 16.04</span></span>       | <span data-ttu-id="6171c-255">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="6171c-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6171c-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="6171c-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="6171c-257">Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="6171c-257">Ubuntu 17.04</span></span>       | <span data-ttu-id="6171c-258">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="6171c-258">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6171c-259">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="6171c-259">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="6171c-260">Debian 8 (Klára)</span><span class="sxs-lookup"><span data-stu-id="6171c-260">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="6171c-261">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="6171c-261">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6171c-262">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="6171c-262">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="6171c-263">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="6171c-263">Debian 9 (Stretch)</span></span> | <span data-ttu-id="6171c-264">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="6171c-264">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6171c-265">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="6171c-265">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="6171c-266">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6171c-266">CentOS 7</span></span> <br> <span data-ttu-id="6171c-267">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="6171c-267">Oracle Linux 7</span></span> <br> <span data-ttu-id="6171c-268">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="6171c-268">RHEL 7</span></span> <br> <span data-ttu-id="6171c-269">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6171c-269">OpenSUSE 42.2</span></span> <br> <span data-ttu-id="6171c-270">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6171c-270">Fedora 25</span></span> | <span data-ttu-id="6171c-271">libunwind, libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="6171c-271">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="6171c-272">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6171c-272">Fedora 26</span></span>          | <span data-ttu-id="6171c-273">libunwind, libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="6171c-273">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="6171c-274">Abyste mohli nasadit binární soubory prostředí PowerShell na Linuxových distribucích, které nejsou oficiálně podporované, museli byste nainstalujte potřebné závislosti pro cílový operační systém v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="6171c-274">In order to deploy PowerShell binaries on Linux distributions that are not officially supported, you would need to install the necessary dependencies for the target OS in separate steps.</span></span> <span data-ttu-id="6171c-275">Například naše [soubor docker Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a pak extrahuje sady Linux `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="6171c-275">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="6171c-276">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="6171c-276">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="6171c-277">Linux</span><span class="sxs-lookup"><span data-stu-id="6171c-277">Linux</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.0.0/pwsh /usr/bin/pwsh
```

#### <a name="macos"></a><span data-ttu-id="6171c-278">macOS</span><span class="sxs-lookup"><span data-stu-id="6171c-278">macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.0/pwsh /usr/local/bin/pwsh
```

### <a name="uninstallation---binary-archives"></a><span data-ttu-id="6171c-279">Odinstalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="6171c-279">Uninstallation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="6171c-280">Linux</span><span class="sxs-lookup"><span data-stu-id="6171c-280">Linux</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

#### <a name="macos"></a><span data-ttu-id="6171c-281">macOS</span><span class="sxs-lookup"><span data-stu-id="6171c-281">macOS</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="6171c-282">Cesty</span><span class="sxs-lookup"><span data-stu-id="6171c-282">Paths</span></span>

* <span data-ttu-id="6171c-283">`$PSHOME` je `/opt/microsoft/powershell/6.0.0/`</span><span class="sxs-lookup"><span data-stu-id="6171c-283">`$PSHOME` is `/opt/microsoft/powershell/6.0.0/`</span></span>
* <span data-ttu-id="6171c-284">Profily uživatelů, bude číst ze `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="6171c-284">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="6171c-285">Výchozí profily bude číst ze `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="6171c-285">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="6171c-286">Moduly uživatele bude číst ze `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="6171c-286">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="6171c-287">Sdílené moduly, bude číst ze `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="6171c-287">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="6171c-288">Výchozí moduly, bude číst ze `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="6171c-288">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="6171c-289">Historie PSReadline budou zaznamenány do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="6171c-289">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="6171c-290">Profily respektují konfigurace Powershellu na hostitele, takže výchozí konkrétního hostitele profily existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="6171c-290">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="6171c-291">Na Linuxu a systému macOS [XDG základní Directory specifikace] [ xdg-bds] je dodržena.</span><span class="sxs-lookup"><span data-stu-id="6171c-291">On Linux and macOS, the [XDG Base Directory Specification][xdg-bds] is respected.</span></span>

<span data-ttu-id="6171c-292">Všimněte si, že vzhledem k tomu, že systému macOS je odvozený od BSD, místo `/opt`, je Předpona použitá `/usr/local`.</span><span class="sxs-lookup"><span data-stu-id="6171c-292">Note that because macOS is a derivation of BSD, instead of `/opt`, the prefix used is `/usr/local`.</span></span> <span data-ttu-id="6171c-293">Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.0.0/`, a symlink je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="6171c-293">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

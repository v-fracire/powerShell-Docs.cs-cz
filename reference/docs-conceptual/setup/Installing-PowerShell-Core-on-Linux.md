# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="691c1-101">Instalace jádra prostředí PowerShell v systému Linux</span><span class="sxs-lookup"><span data-stu-id="691c1-101">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="691c1-102">Podporuje [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu č. 17.04] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25 ] [ fed25], [Fedora 26][fed26], a [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="691c1-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], and [Arch Linux][arch].</span></span>

<span data-ttu-id="691c1-103">Pro Linux distribuce, které nejsou oficiálně podporované, můžete se pokusit [prostředí PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="691c1-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="691c1-104">Můžete také zkusit nasazení binárních souborů prostředí PowerShell přímo pomocí sady Linux [ `tar.gz` archivu][tar], ale je potřeba nastavit podle operačního systému v samostatné kroky potřebné závislosti.</span><span class="sxs-lookup"><span data-stu-id="691c1-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="691c1-105">Všechny balíčky jsou k dispozici na našem Githubu [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="691c1-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="691c1-106">Spustit po instalaci balíčku `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="691c1-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

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
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="691c1-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="691c1-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="691c1-108">Instalaci přes úložiště balíčků - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="691c1-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="691c1-109">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="691c1-110">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="691c1-110">This is the preferred method.</span></span>

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

<span data-ttu-id="691c1-111">Jako superuživatele zaregistrujte úložiště společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="691c1-111">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="691c1-112">Od toho stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.</span><span class="sxs-lookup"><span data-stu-id="691c1-112">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="691c1-113">Instalace prostřednictvím přímé stahování - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="691c1-113">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="691c1-114">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="691c1-114">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="691c1-115">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-115">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="691c1-116">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-116">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="691c1-117">Odinstalace - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="691c1-117">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="691c1-118">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="691c1-118">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="691c1-119">Instalaci přes úložiště balíčků - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="691c1-119">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="691c1-120">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="691c1-121">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="691c1-121">This is the preferred method.</span></span>

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

<span data-ttu-id="691c1-122">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="691c1-122">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="691c1-123">Instalace prostřednictvím přímé stahování - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="691c1-123">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="691c1-124">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="691c1-124">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="691c1-125">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-125">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="691c1-126">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-126">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="691c1-127">Odinstalace - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="691c1-127">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="691c1-128">Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="691c1-128">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="691c1-129">Instalaci přes úložiště balíčků - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="691c1-129">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="691c1-130">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-130">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="691c1-131">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="691c1-131">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/17.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="691c1-132">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="691c1-132">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="691c1-133">Instalace prostřednictvím přímé stahování - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="691c1-133">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="691c1-134">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="691c1-134">Download the Debian package `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="691c1-135">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-135">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="691c1-136">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-136">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="691c1-137">Odinstalace - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="691c1-137">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="691c1-138">Debian 8</span><span class="sxs-lookup"><span data-stu-id="691c1-138">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="691c1-139">Instalaci přes úložiště balíčků - Debian 8</span><span class="sxs-lookup"><span data-stu-id="691c1-139">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="691c1-140">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-140">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="691c1-141">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="691c1-141">This is the preferred method.</span></span>

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

<span data-ttu-id="691c1-142">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="691c1-142">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="691c1-143">Instalace prostřednictvím přímé stahování - Debian 8</span><span class="sxs-lookup"><span data-stu-id="691c1-143">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="691c1-144">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.8_amd64.deb` z [uvolní][] stránky do Debian počítače.</span><span class="sxs-lookup"><span data-stu-id="691c1-144">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="691c1-145">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-145">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="691c1-146">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti.</span><span class="sxs-lookup"><span data-stu-id="691c1-146">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="691c1-147">Další příkaz `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-147">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="691c1-148">Odinstalace - Debian 8</span><span class="sxs-lookup"><span data-stu-id="691c1-148">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="691c1-149">Debian 9</span><span class="sxs-lookup"><span data-stu-id="691c1-149">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="691c1-150">Instalaci přes úložiště balíčků - Debian 9</span><span class="sxs-lookup"><span data-stu-id="691c1-150">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="691c1-151">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-151">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="691c1-152">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="691c1-152">This is the preferred method.</span></span>

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

<span data-ttu-id="691c1-153">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="691c1-153">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="691c1-154">Instalace prostřednictvím přímé stahování - Debian 9</span><span class="sxs-lookup"><span data-stu-id="691c1-154">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="691c1-155">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.9_amd64.deb` z [uvolní][] stránky do Debian počítače.</span><span class="sxs-lookup"><span data-stu-id="691c1-155">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="691c1-156">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-156">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="691c1-157">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti.</span><span class="sxs-lookup"><span data-stu-id="691c1-157">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="691c1-158">Další příkaz `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-158">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="691c1-159">Odinstalace - Debian 9</span><span class="sxs-lookup"><span data-stu-id="691c1-159">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="691c1-160">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="691c1-160">CentOS 7</span></span>

> <span data-ttu-id="691c1-161">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="691c1-161">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="691c1-162">Instalaci přes úložiště balíčků (doporučeno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="691c1-162">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="691c1-163">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-163">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="691c1-164">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-164">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="691c1-165">Instalace prostřednictvím přímé stahování - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="691c1-165">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="691c1-166">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače CentOS.</span><span class="sxs-lookup"><span data-stu-id="691c1-166">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="691c1-167">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-167">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="691c1-168">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="691c1-168">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="691c1-169">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="691c1-169">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="691c1-171">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="691c1-171">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="691c1-172">Instalaci přes úložiště balíčků (doporučeno) - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="691c1-172">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="691c1-173">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-173">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="691c1-174">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-174">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="691c1-175">Instalace prostřednictvím přímé stahování - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="691c1-175">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="691c1-176">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="691c1-176">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="691c1-177">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-177">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="691c1-178">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="691c1-178">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="691c1-179">Odinstalace - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="691c1-179">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="691c1-180">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="691c1-180">OpenSUSE 42.2</span></span>

> [!NOTE]
> <span data-ttu-id="691c1-181">Při instalaci prostředí PowerShell základní `zypper` může nahlaste mu následující chybu:</span><span class="sxs-lookup"><span data-stu-id="691c1-181">When installing PowerShell Core, `zypper` may report the following error:</span></span>
>
> ```Output
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> <span data-ttu-id="691c1-182">V takovém případě ověřte, že kompatibilní `libcurl` knihovny nachází kontrolou, že následující příkaz ukazuje `libcurl4` balíčku se po instalaci:</span><span class="sxs-lookup"><span data-stu-id="691c1-182">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> <span data-ttu-id="691c1-183">Zvolte `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="691c1-183">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="691c1-184">Instalaci přes úložiště balíčků (doporučeno) - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="691c1-184">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="691c1-185">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-185">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Product feed
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/zypp/repos.d/microsoft.repo

# Update the list of products
sudo zypper update

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="691c1-186">Instalace prostřednictvím přímé stahování - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="691c1-186">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="691c1-187">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="691c1-187">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="691c1-188">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="691c1-188">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="691c1-189">Odinstalace - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="691c1-189">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora-25"></a><span data-ttu-id="691c1-190">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="691c1-190">Fedora 25</span></span>

### <a name="installation-via-package-repository-preferred---fedora-25"></a><span data-ttu-id="691c1-191">Instalaci přes úložiště balíčků (doporučeno) - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="691c1-191">Installation via Package Repository (preferred) - Fedora 25</span></span>

<span data-ttu-id="691c1-192">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-192">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-25"></a><span data-ttu-id="691c1-193">Instalace prostřednictvím přímé stahování - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="691c1-193">Installation via Direct Download - Fedora 25</span></span>

<span data-ttu-id="691c1-194">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Fedora.</span><span class="sxs-lookup"><span data-stu-id="691c1-194">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="691c1-195">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-195">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="691c1-196">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="691c1-196">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-25"></a><span data-ttu-id="691c1-197">Odinstalace - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="691c1-197">Uninstallation - Fedora 25</span></span>

```sh
sudo dnf remove powershell
```

## <a name="fedora-26"></a><span data-ttu-id="691c1-198">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="691c1-198">Fedora 26</span></span>

### <a name="installation-via-package-repository-preferred---fedora-26"></a><span data-ttu-id="691c1-199">Instalaci přes úložiště balíčků (doporučeno) - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="691c1-199">Installation via Package Repository (preferred) - Fedora 26</span></span>

<span data-ttu-id="691c1-200">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="691c1-200">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-26"></a><span data-ttu-id="691c1-201">Instalace prostřednictvím přímé stahování - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="691c1-201">Installation via Direct Download - Fedora 26</span></span>

<span data-ttu-id="691c1-202">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Fedora.</span><span class="sxs-lookup"><span data-stu-id="691c1-202">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="691c1-203">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-203">Then execute the following in the terminal:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="691c1-204">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="691c1-204">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-26"></a><span data-ttu-id="691c1-205">Odinstalace - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="691c1-205">Uninstallation - Fedora 26</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="691c1-206">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="691c1-206">Arch Linux</span></span>

<span data-ttu-id="691c1-207">PowerShell je k dispozici [architektura Linux][] uživatele úložiště (AUR).</span><span class="sxs-lookup"><span data-stu-id="691c1-207">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="691c1-208">Může být zkompilován s [označené nejnovější verze][arch-release]</span><span class="sxs-lookup"><span data-stu-id="691c1-208">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="691c1-209">Mohou být zkompilovány z [nejnovější potvrzení změn na hlavní server][arch-git]</span><span class="sxs-lookup"><span data-stu-id="691c1-209">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="691c1-210">Můžete nainstalovat, pomocí [nejnovější verzi binární][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="691c1-210">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="691c1-211">Balíčky v AUR jsou udržuje komunitní – neexistuje žádná podpora oficiální.</span><span class="sxs-lookup"><span data-stu-id="691c1-211">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="691c1-212">Další informace o instalaci balíčků z AUR najdete v tématu [architektura Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunity [soubor Docker](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="691c1-212">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[architektura Linux]: https://www.archlinux.org/download/
[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="691c1-214">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="691c1-214">Linux AppImage</span></span>

<span data-ttu-id="691c1-215">Pomocí poslední distribuci systému Linux, stáhněte si AppImage `powershell-6.0.1-x86_64.AppImage` z [uvolní][] stránky do počítače Linux.</span><span class="sxs-lookup"><span data-stu-id="691c1-215">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="691c1-216">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="691c1-216">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="691c1-217">[AppImage][] vám umožní spustit prostředí PowerShell bez jeho instalaci.</span><span class="sxs-lookup"><span data-stu-id="691c1-217">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="691c1-218">Je přenosné aplikace, která obsahuje ureitou prostředí PowerShell a jeho závislosti (včetně závislostí systému .NET Core) do jednoho získá na ucelenosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="691c1-218">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="691c1-219">Tento balíček je jednoho binárního souboru, který funguje nezávisle na distribuční Linux uživatele.</span><span class="sxs-lookup"><span data-stu-id="691c1-219">This package  is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="691c1-221">Kali</span><span class="sxs-lookup"><span data-stu-id="691c1-221">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="691c1-222">Instalace</span><span class="sxs-lookup"><span data-stu-id="691c1-222">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="691c1-223">Spusťte prostředí PowerShell bez instalace se v nejnovější Kali (vrácení Kali GNU/Linux)</span><span class="sxs-lookup"><span data-stu-id="691c1-223">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="691c1-224">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="691c1-224">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="691c1-225">Raspbian</span><span class="sxs-lookup"><span data-stu-id="691c1-225">Raspbian</span></span>

<span data-ttu-id="691c1-226">V současné době prostředí PowerShell je podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="691c1-226">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="691c1-227">Také CoreCLR (a tedy základní prostředí PowerShell) budou fungovat jenom na zařízení pí 2 a 3 platformy jako další zařízení, jako je třeba [pí nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesoru.</span><span class="sxs-lookup"><span data-stu-id="691c1-227">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="691c1-228">Stáhnout [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) pro přístup na váš pí.</span><span class="sxs-lookup"><span data-stu-id="691c1-228">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="691c1-229">Instalace</span><span class="sxs-lookup"><span data-stu-id="691c1-229">Installation</span></span>

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

<span data-ttu-id="691c1-230">Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty k "pwsh" binární</span><span class="sxs-lookup"><span data-stu-id="691c1-230">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="691c1-231">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="691c1-231">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="691c1-232">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="691c1-232">Binary Archives</span></span>

<span data-ttu-id="691c1-233">Prostředí PowerShell binární `tar.gz` archivy jsou k dispozici pro Linux platformy a povolíte pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="691c1-233">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="691c1-234">Závislosti</span><span class="sxs-lookup"><span data-stu-id="691c1-234">Dependencies</span></span>

<span data-ttu-id="691c1-235">Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce systému Linux.</span><span class="sxs-lookup"><span data-stu-id="691c1-235">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="691c1-236">Ale .NET Core runtime vyžaduje jiný závislosti na různých distribucí, a proto prostředí PowerShell dělá to stejné.</span><span class="sxs-lookup"><span data-stu-id="691c1-236">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="691c1-237">Následující graf zobrazuje závislosti rozhraní .NET 2.0 jádra, které jsou oficiálně podporované v různých distribucí Linux.</span><span class="sxs-lookup"><span data-stu-id="691c1-237">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="691c1-238">Operační systém</span><span class="sxs-lookup"><span data-stu-id="691c1-238">OS</span></span>                 | <span data-ttu-id="691c1-239">Závislosti</span><span class="sxs-lookup"><span data-stu-id="691c1-239">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="691c1-240">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="691c1-240">Ubuntu 14.04</span></span>       | <span data-ttu-id="691c1-241">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="691c1-241">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="691c1-242">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="691c1-242">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="691c1-243">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="691c1-243">Ubuntu 16.04</span></span>       | <span data-ttu-id="691c1-244">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="691c1-244">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="691c1-245">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="691c1-245">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="691c1-246">Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="691c1-246">Ubuntu 17.04</span></span>       | <span data-ttu-id="691c1-247">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="691c1-247">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="691c1-248">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="691c1-248">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="691c1-249">Debian 8 (Klára)</span><span class="sxs-lookup"><span data-stu-id="691c1-249">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="691c1-250">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="691c1-250">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="691c1-251">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="691c1-251">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="691c1-252">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="691c1-252">Debian 9 (Stretch)</span></span> | <span data-ttu-id="691c1-253">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="691c1-253">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="691c1-254">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="691c1-254">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="691c1-255">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="691c1-255">CentOS 7</span></span> <br> <span data-ttu-id="691c1-256">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="691c1-256">Oracle Linux 7</span></span> <br> <span data-ttu-id="691c1-257">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="691c1-257">RHEL 7</span></span> <br> <span data-ttu-id="691c1-258">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="691c1-258">OpenSUSE 42.2</span></span> <br> <span data-ttu-id="691c1-259">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="691c1-259">Fedora 25</span></span> | <span data-ttu-id="691c1-260">libunwind, libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="691c1-260">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="691c1-261">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="691c1-261">Fedora 26</span></span>          | <span data-ttu-id="691c1-262">libunwind, libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="691c1-262">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="691c1-263">Pokud chcete nasadit binární soubory prostředí PowerShell na Linuxových distribucích, které nejsou oficiálně podporované, musíte nainstalovat potřebné závislosti pro cílový operační systém v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="691c1-263">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="691c1-264">Například naše [soubor docker Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a pak extrahuje sady Linux `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="691c1-264">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="691c1-265">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="691c1-265">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="691c1-266">Linux</span><span class="sxs-lookup"><span data-stu-id="691c1-266">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="691c1-267">Odinstalaci binární archivy</span><span class="sxs-lookup"><span data-stu-id="691c1-267">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="691c1-268">Cesty</span><span class="sxs-lookup"><span data-stu-id="691c1-268">Paths</span></span>

* <span data-ttu-id="691c1-269">`$PSHOME` je `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="691c1-269">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="691c1-270">Profily uživatelů, bude číst ze `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="691c1-270">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="691c1-271">Výchozí profily bude číst ze `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="691c1-271">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="691c1-272">Moduly uživatele bude číst ze `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="691c1-272">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="691c1-273">Sdílené moduly, bude číst ze `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="691c1-273">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="691c1-274">Výchozí moduly, bude číst ze `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="691c1-274">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="691c1-275">Historie PSReadline budou zaznamenány do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="691c1-275">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="691c1-276">Profily respektují konfigurace Powershellu na hostitele, takže výchozí konkrétního hostitele profily existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="691c1-276">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="691c1-277">Prostředí PowerShell respektuje [XDG základní Directory specifikace] [ xdg-bds] v systému Linux.</span><span class="sxs-lookup"><span data-stu-id="691c1-277">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="603ce-101">Instalace PowerShellu Core v Linuxu</span><span class="sxs-lookup"><span data-stu-id="603ce-101">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="603ce-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="603ce-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="603ce-103">Pro Linux distribuce, které nejsou oficiálně podporované, můžete se pokusit [prostředí PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="603ce-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="603ce-104">Můžete také zkusit nasazení binárních souborů prostředí PowerShell přímo pomocí sady Linux [ `tar.gz` archivu][tar], ale je potřeba nastavit podle operačního systému v samostatné kroky potřebné závislosti.</span><span class="sxs-lookup"><span data-stu-id="603ce-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="603ce-105">Všechny balíčky jsou k dispozici na našem Githubu [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="603ce-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="603ce-106">Spustit po instalaci balíčku `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="603ce-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1710
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fedora]: #fedora
[arch]: #arch-linux
[lai]: #linux-appimage
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="603ce-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="603ce-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="603ce-108">Instalaci přes úložiště balíčků - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="603ce-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="603ce-109">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="603ce-110">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="603ce-110">This is the preferred method.</span></span>

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

<span data-ttu-id="603ce-111">Jako superuživatele zaregistrujte úložiště společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="603ce-111">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="603ce-112">Od toho stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.</span><span class="sxs-lookup"><span data-stu-id="603ce-112">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="603ce-113">Instalace prostřednictvím přímé stahování - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="603ce-113">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="603ce-114">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="603ce-114">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="603ce-115">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-115">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="603ce-116">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-116">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="603ce-117">Odinstalace - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="603ce-117">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="603ce-118">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="603ce-118">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="603ce-119">Instalaci přes úložiště balíčků - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="603ce-119">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="603ce-120">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="603ce-121">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="603ce-121">This is the preferred method.</span></span>

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

<span data-ttu-id="603ce-122">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="603ce-122">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="603ce-123">Instalace prostřednictvím přímé stahování - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="603ce-123">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="603ce-124">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="603ce-124">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="603ce-125">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-125">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="603ce-126">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-126">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="603ce-127">Odinstalace - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="603ce-127">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1710"></a><span data-ttu-id="603ce-128">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="603ce-128">Ubuntu 17.10</span></span>

> <span data-ttu-id="603ce-129">Poznámka: Po byla přidána podpora pro Ubuntu 18.04 `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="603ce-129">Note: Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1710"></a><span data-ttu-id="603ce-130">Instalaci přes úložiště balíčků - Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="603ce-130">Installation via Package Repository - Ubuntu 17.10</span></span>

<span data-ttu-id="603ce-131">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-131">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="603ce-132">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="603ce-132">This is the preferred method.</span></span>

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

<span data-ttu-id="603ce-133">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="603ce-133">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1710"></a><span data-ttu-id="603ce-134">Instalace prostřednictvím přímé stahování - Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="603ce-134">Installation via Direct Download - Ubuntu 17.10</span></span>

<span data-ttu-id="603ce-135">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="603ce-135">Download the Debian package `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="603ce-136">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-136">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.10_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="603ce-137">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-137">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1710"></a><span data-ttu-id="603ce-138">Odinstalace - Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="603ce-138">Uninstallation - Ubuntu 17.10</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="603ce-139">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="603ce-139">Ubuntu 18.04</span></span>

> <span data-ttu-id="603ce-140">Poznámka: Po byla přidána podpora pro Ubuntu 18.04 `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="603ce-140">Note: Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="603ce-141">Instalaci přes úložiště balíčků - Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="603ce-141">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="603ce-142">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-142">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="603ce-143">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="603ce-143">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="603ce-144">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="603ce-144">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="603ce-145">Instalace prostřednictvím přímé stahování - Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="603ce-145">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="603ce-146">Stáhněte si balíček Debian `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` z [uvolní][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="603ce-146">Download the Debian package `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="603ce-147">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-147">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="603ce-148">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-148">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1710"></a><span data-ttu-id="603ce-149">Odinstalace - Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="603ce-149">Uninstallation - Ubuntu 17.10</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="603ce-150">Debian 8</span><span class="sxs-lookup"><span data-stu-id="603ce-150">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="603ce-151">Instalaci přes úložiště balíčků - Debian 8</span><span class="sxs-lookup"><span data-stu-id="603ce-151">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="603ce-152">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-152">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="603ce-153">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="603ce-153">This is the preferred method.</span></span>

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

<span data-ttu-id="603ce-154">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="603ce-154">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="603ce-155">Instalace prostřednictvím přímé stahování - Debian 8</span><span class="sxs-lookup"><span data-stu-id="603ce-155">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="603ce-156">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.8_amd64.deb` z [uvolní][] stránky do Debian počítače.</span><span class="sxs-lookup"><span data-stu-id="603ce-156">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="603ce-157">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-157">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="603ce-158">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti.</span><span class="sxs-lookup"><span data-stu-id="603ce-158">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="603ce-159">Další příkaz `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-159">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="603ce-160">Odinstalace - Debian 8</span><span class="sxs-lookup"><span data-stu-id="603ce-160">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="603ce-161">Debian 9</span><span class="sxs-lookup"><span data-stu-id="603ce-161">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="603ce-162">Instalaci přes úložiště balíčků - Debian 9</span><span class="sxs-lookup"><span data-stu-id="603ce-162">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="603ce-163">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-163">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="603ce-164">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="603ce-164">This is the preferred method.</span></span>

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

<span data-ttu-id="603ce-165">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="603ce-165">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="603ce-166">Instalace prostřednictvím přímé stahování - Debian 9</span><span class="sxs-lookup"><span data-stu-id="603ce-166">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="603ce-167">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.9_amd64.deb` z [uvolní][] stránky do Debian počítače.</span><span class="sxs-lookup"><span data-stu-id="603ce-167">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="603ce-168">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-168">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="603ce-169">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti.</span><span class="sxs-lookup"><span data-stu-id="603ce-169">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="603ce-170">Další příkaz `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-170">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="603ce-171">Odinstalace - Debian 9</span><span class="sxs-lookup"><span data-stu-id="603ce-171">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="603ce-172">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="603ce-172">CentOS 7</span></span>

> <span data-ttu-id="603ce-173">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="603ce-173">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="603ce-174">Instalaci přes úložiště balíčků (doporučeno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="603ce-174">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="603ce-175">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-175">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="603ce-176">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-176">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="603ce-177">Instalace prostřednictvím přímé stahování - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="603ce-177">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="603ce-178">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače CentOS.</span><span class="sxs-lookup"><span data-stu-id="603ce-178">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="603ce-179">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-179">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="603ce-180">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="603ce-180">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="603ce-181">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="603ce-181">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="603ce-183">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="603ce-183">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="603ce-184">Instalaci přes úložiště balíčků (doporučeno) - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="603ce-184">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="603ce-185">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-185">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="603ce-186">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-186">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="603ce-187">Instalace prostřednictvím přímé stahování - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="603ce-187">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="603ce-188">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="603ce-188">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="603ce-189">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-189">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="603ce-190">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="603ce-190">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="603ce-191">Odinstalace - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="603ce-191">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="603ce-192">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="603ce-192">OpenSUSE 42.2</span></span>

> [!NOTE]
> <span data-ttu-id="603ce-193">Při instalaci prostředí PowerShell základní `zypper` může nahlaste mu následující chybu:</span><span class="sxs-lookup"><span data-stu-id="603ce-193">When installing PowerShell Core, `zypper` may report the following error:</span></span>
>
> ```Output
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> <span data-ttu-id="603ce-194">V takovém případě ověřte, že kompatibilní `libcurl` knihovny nachází kontrolou, že následující příkaz ukazuje `libcurl4` balíčku se po instalaci:</span><span class="sxs-lookup"><span data-stu-id="603ce-194">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> <span data-ttu-id="603ce-195">Zvolte `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="603ce-195">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="603ce-196">Instalaci přes úložiště balíčků (doporučeno) - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="603ce-196">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="603ce-197">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-197">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="603ce-198">Instalace prostřednictvím přímé stahování - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="603ce-198">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="603ce-199">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="603ce-199">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="603ce-200">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="603ce-200">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="603ce-201">Odinstalace - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="603ce-201">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="603ce-202">Fedora</span><span class="sxs-lookup"><span data-stu-id="603ce-202">Fedora</span></span>

> <span data-ttu-id="603ce-203">Poznámka: Fedora 28 je podporována pouze v prostředí PowerShell základní 6.1 a novější.</span><span class="sxs-lookup"><span data-stu-id="603ce-203">Please note, Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="603ce-204">Instalaci přes úložiště balíčků (doporučeno) - Fedora 27 Fedora 28</span><span class="sxs-lookup"><span data-stu-id="603ce-204">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="603ce-205">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="603ce-205">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="603ce-206">Instalace prostřednictvím přímé stahování - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="603ce-206">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="603ce-207">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače Fedora.</span><span class="sxs-lookup"><span data-stu-id="603ce-207">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="603ce-208">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-208">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="603ce-209">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="603ce-209">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="603ce-210">Odinstalace - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="603ce-210">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="603ce-211">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="603ce-211">Arch Linux</span></span>

<span data-ttu-id="603ce-212">PowerShell je k dispozici [Arch Linux][] uživatele úložiště (AUR).</span><span class="sxs-lookup"><span data-stu-id="603ce-212">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="603ce-213">Může být zkompilován s [označené nejnovější verze][arch-release]</span><span class="sxs-lookup"><span data-stu-id="603ce-213">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="603ce-214">Mohou být zkompilovány z [nejnovější potvrzení změn na hlavní server][arch-git]</span><span class="sxs-lookup"><span data-stu-id="603ce-214">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="603ce-215">Můžete nainstalovat, pomocí [nejnovější verzi binární][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="603ce-215">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="603ce-216">Balíčky v AUR jsou udržuje komunitní – neexistuje žádná podpora oficiální.</span><span class="sxs-lookup"><span data-stu-id="603ce-216">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="603ce-217">Další informace o instalaci balíčků z AUR najdete v tématu [architektura Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunity [soubor Docker](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="603ce-217">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="603ce-219">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="603ce-219">Linux AppImage</span></span>

<span data-ttu-id="603ce-220">Pomocí poslední distribuci systému Linux, stáhněte si AppImage `powershell-6.0.1-x86_64.AppImage` z [uvolní][] stránky do počítače Linux.</span><span class="sxs-lookup"><span data-stu-id="603ce-220">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="603ce-221">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="603ce-221">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="603ce-222">[AppImage][] vám umožní spustit prostředí PowerShell bez jeho instalaci.</span><span class="sxs-lookup"><span data-stu-id="603ce-222">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="603ce-223">Je přenosné aplikace, která obsahuje ureitou prostředí PowerShell a jeho závislosti (včetně závislostí systému .NET Core) do jednoho získá na ucelenosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="603ce-223">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="603ce-224">Tento balíček je jednoho binárního souboru, který funguje nezávisle na distribuční Linux uživatele.</span><span class="sxs-lookup"><span data-stu-id="603ce-224">This package  is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="603ce-226">Kali</span><span class="sxs-lookup"><span data-stu-id="603ce-226">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="603ce-227">Instalace</span><span class="sxs-lookup"><span data-stu-id="603ce-227">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="603ce-228">Spusťte prostředí PowerShell bez instalace se v nejnovější Kali (vrácení Kali GNU/Linux)</span><span class="sxs-lookup"><span data-stu-id="603ce-228">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="603ce-229">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="603ce-229">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="603ce-230">Raspbian</span><span class="sxs-lookup"><span data-stu-id="603ce-230">Raspbian</span></span>

<span data-ttu-id="603ce-231">V současné době prostředí PowerShell je podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="603ce-231">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="603ce-232">Také CoreCLR (a tedy základní prostředí PowerShell) budou fungovat jenom na zařízení pí 2 a 3 platformy jako další zařízení, jako je třeba [pí nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesoru.</span><span class="sxs-lookup"><span data-stu-id="603ce-232">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="603ce-233">Stáhnout [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) pro přístup na váš pí.</span><span class="sxs-lookup"><span data-stu-id="603ce-233">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="603ce-234">Instalace</span><span class="sxs-lookup"><span data-stu-id="603ce-234">Installation</span></span>

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

<span data-ttu-id="603ce-235">Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty k "pwsh" binární</span><span class="sxs-lookup"><span data-stu-id="603ce-235">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="603ce-236">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="603ce-236">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="603ce-237">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="603ce-237">Binary Archives</span></span>

<span data-ttu-id="603ce-238">Prostředí PowerShell binární `tar.gz` archivy jsou k dispozici pro Linux platformy a povolíte pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="603ce-238">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="603ce-239">Závislosti</span><span class="sxs-lookup"><span data-stu-id="603ce-239">Dependencies</span></span>

<span data-ttu-id="603ce-240">Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce systému Linux.</span><span class="sxs-lookup"><span data-stu-id="603ce-240">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="603ce-241">Ale .NET Core runtime vyžaduje jiný závislosti na různých distribucí, a proto prostředí PowerShell dělá to stejné.</span><span class="sxs-lookup"><span data-stu-id="603ce-241">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="603ce-242">Následující graf zobrazuje závislosti rozhraní .NET 2.0 jádra, které jsou oficiálně podporované v různých distribucí Linux.</span><span class="sxs-lookup"><span data-stu-id="603ce-242">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="603ce-243">Operační systém</span><span class="sxs-lookup"><span data-stu-id="603ce-243">OS</span></span>                 | <span data-ttu-id="603ce-244">Závislosti</span><span class="sxs-lookup"><span data-stu-id="603ce-244">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="603ce-245">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="603ce-245">Ubuntu 14.04</span></span>       | <span data-ttu-id="603ce-246">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="603ce-246">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="603ce-247">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="603ce-247">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="603ce-248">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="603ce-248">Ubuntu 16.04</span></span>       | <span data-ttu-id="603ce-249">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="603ce-249">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="603ce-250">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="603ce-250">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="603ce-251">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="603ce-251">Ubuntu 17.10</span></span>       | <span data-ttu-id="603ce-252">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="603ce-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="603ce-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="603ce-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="603ce-254">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="603ce-254">Ubuntu 18.04</span></span>       | <span data-ttu-id="603ce-255">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="603ce-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="603ce-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="603ce-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="603ce-257">Debian 8 (Klára)</span><span class="sxs-lookup"><span data-stu-id="603ce-257">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="603ce-258">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="603ce-258">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="603ce-259">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="603ce-259">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="603ce-260">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="603ce-260">Debian 9 (Stretch)</span></span> | <span data-ttu-id="603ce-261">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="603ce-261">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="603ce-262">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="603ce-262">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="603ce-263">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="603ce-263">CentOS 7</span></span> <br> <span data-ttu-id="603ce-264">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="603ce-264">Oracle Linux 7</span></span> <br> <span data-ttu-id="603ce-265">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="603ce-265">RHEL 7</span></span> <br> <span data-ttu-id="603ce-266">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="603ce-266">OpenSUSE 42.2</span></span> | <span data-ttu-id="603ce-267">libunwind, libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="603ce-267">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="603ce-268">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="603ce-268">Fedora 27</span></span> <br> <span data-ttu-id="603ce-269">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="603ce-269">Fedora 28</span></span> | <span data-ttu-id="603ce-270">libunwind, libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="603ce-270">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="603ce-271">Pokud chcete nasadit binární soubory prostředí PowerShell na Linuxových distribucích, které nejsou oficiálně podporované, musíte nainstalovat potřebné závislosti pro cílový operační systém v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="603ce-271">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="603ce-272">Například naše [soubor docker Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a pak extrahuje sady Linux `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="603ce-272">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="603ce-273">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="603ce-273">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="603ce-274">Linux</span><span class="sxs-lookup"><span data-stu-id="603ce-274">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="603ce-275">Odinstalaci binární archivy</span><span class="sxs-lookup"><span data-stu-id="603ce-275">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="603ce-276">Cesty</span><span class="sxs-lookup"><span data-stu-id="603ce-276">Paths</span></span>

* <span data-ttu-id="603ce-277">`$PSHOME` je `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="603ce-277">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="603ce-278">Profily uživatelů, bude číst ze `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="603ce-278">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="603ce-279">Výchozí profily bude číst ze `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="603ce-279">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="603ce-280">Moduly uživatele bude číst ze `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="603ce-280">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="603ce-281">Sdílené moduly, bude číst ze `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="603ce-281">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="603ce-282">Výchozí moduly, bude číst ze `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="603ce-282">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="603ce-283">Historie PSReadline budou zaznamenány do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="603ce-283">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="603ce-284">Profily respektují konfigurace Powershellu na hostitele, takže výchozí konkrétního hostitele profily existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="603ce-284">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="603ce-285">Prostředí PowerShell respektuje [XDG základní Directory specifikace] [ xdg-bds] v systému Linux.</span><span class="sxs-lookup"><span data-stu-id="603ce-285">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

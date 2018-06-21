# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="f954f-101">Instalace PowerShellu Core v Linuxu</span><span class="sxs-lookup"><span data-stu-id="f954f-101">Installing PowerShell Core on Linux</span></span>

Supports <bpt id="p1">[</bpt>Ubuntu 14.04<ept id="p1">]</ept><bpt id="p2">[</bpt><ept id="p2">u14]</ept>, <bpt id="p3">[</bpt>Ubuntu 16.04<ept id="p3">]</ept><bpt id="p4">[</bpt><ept id="p4">u16]</ept>, <bpt id="p5">[</bpt>Ubuntu 17.04<ept id="p5">]</ept><bpt id="p6">[</bpt><ept id="p6">u17]</ept>, <bpt id="p7">[</bpt>Debian 8<ept id="p7">]</ept><bpt id="p8">[</bpt><ept id="p8">deb8]</ept>, <bpt id="p9">[</bpt>Debian 9<ept id="p9">]</ept><bpt id="p10">[</bpt><ept id="p10">deb9]</ept>, <bpt id="p11">[</bpt>CentOS 7<ept id="p11">]</ept><bpt id="p12">[</bpt><ept id="p12">cos]</ept>, <bpt id="p13">[</bpt>Red Hat Enterprise Linux (RHEL) 7<ept id="p13">]</ept><bpt id="p14">[</bpt><ept id="p14">rhel7]</ept>, <bpt id="p15">[</bpt>OpenSUSE 42.2<ept id="p15">]</ept><bpt id="p16">[</bpt><ept id="p16">opensuse]</ept>, <bpt id="p17">[</bpt>Fedora 27<ept id="p17">]</ept><bpt id="p18">[</bpt><ept id="p18">fedora]</ept>, <bpt id="p19">[</bpt>Fedora 28<ept id="p19">]</ept><bpt id="p20">[</bpt><ept id="p20">fedora]</ept>, and <bpt id="p21">[</bpt>Arch Linux<ept id="p21">]</ept><bpt id="p22">[</bpt><ept id="p22">arch]</ept>.

<span data-ttu-id="f954f-103">Pro Linux distribuce, které nejsou oficiálně podporované, můžete se pokusit [prostředí PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="f954f-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="f954f-104">Můžete také zkusit nasazení binárních souborů prostředí PowerShell přímo pomocí sady Linux [ `tar.gz` archivu][tar], ale je potřeba nastavit podle operačního systému v samostatné kroky potřebné závislosti.</span><span class="sxs-lookup"><span data-stu-id="f954f-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="f954f-105">Všechny balíčky jsou k dispozici na našem Githubu [Verze][] stránky.</span><span class="sxs-lookup"><span data-stu-id="f954f-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="f954f-106">Spustit po instalaci balíčku `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="f954f-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1704
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fedora]: #fedora
[arch]: #arch-linux
[lai]: #linux-appimage
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="f954f-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f954f-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="f954f-108">Instalaci přes úložiště balíčků - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f954f-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="f954f-109">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f954f-110">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="f954f-110">This is the preferred method.</span></span>

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

<span data-ttu-id="f954f-111">Jako superuživatele zaregistrujte úložiště společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f954f-111">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="f954f-112">Od toho stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.</span><span class="sxs-lookup"><span data-stu-id="f954f-112">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="f954f-113">Instalace prostřednictvím přímé stahování - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f954f-113">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="f954f-114">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` z [Verze][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f954f-114">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="f954f-115">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-115">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="f954f-116">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-116">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="f954f-117">Odinstalace - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f954f-117">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="f954f-118">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f954f-118">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="f954f-119">Instalaci přes úložiště balíčků - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f954f-119">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="f954f-120">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f954f-121">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="f954f-121">This is the preferred method.</span></span>

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

<span data-ttu-id="f954f-122">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="f954f-122">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="f954f-123">Instalace prostřednictvím přímé stahování - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f954f-123">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="f954f-124">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` z [Verze][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f954f-124">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="f954f-125">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-125">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="f954f-126">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-126">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="f954f-127">Odinstalace - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f954f-127">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="f954f-128">Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="f954f-128">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="f954f-129">Instalaci přes úložiště balíčků - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="f954f-129">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="f954f-130">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-130">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f954f-131">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="f954f-131">This is the preferred method.</span></span>

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

<span data-ttu-id="f954f-132">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="f954f-132">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="f954f-133">Instalace prostřednictvím přímé stahování - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="f954f-133">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="f954f-134">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` z [Verze][] stránky do počítače Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f954f-134">Download the Debian package `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="f954f-135">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-135">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="f954f-136">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti; příkaz Další `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-136">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="f954f-137">Odinstalace - Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="f954f-137">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="f954f-138">Debian 8</span><span class="sxs-lookup"><span data-stu-id="f954f-138">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="f954f-139">Instalaci přes úložiště balíčků - Debian 8</span><span class="sxs-lookup"><span data-stu-id="f954f-139">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="f954f-140">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-140">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f954f-141">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="f954f-141">This is the preferred method.</span></span>

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

<span data-ttu-id="f954f-142">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="f954f-142">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="f954f-143">Instalace prostřednictvím přímé stahování - Debian 8</span><span class="sxs-lookup"><span data-stu-id="f954f-143">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="f954f-144">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.8_amd64.deb` z [Verze][] stránky do Debian počítače.</span><span class="sxs-lookup"><span data-stu-id="f954f-144">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="f954f-145">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-145">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="f954f-146">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti.</span><span class="sxs-lookup"><span data-stu-id="f954f-146">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="f954f-147">Další příkaz `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-147">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="f954f-148">Odinstalace - Debian 8</span><span class="sxs-lookup"><span data-stu-id="f954f-148">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="f954f-149">Debian 9</span><span class="sxs-lookup"><span data-stu-id="f954f-149">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="f954f-150">Instalaci přes úložiště balíčků - Debian 9</span><span class="sxs-lookup"><span data-stu-id="f954f-150">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="f954f-151">Základní prostředí PowerShell pro Linux, je publikovaný na balíček úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-151">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f954f-152">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="f954f-152">This is the preferred method.</span></span>

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

<span data-ttu-id="f954f-153">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, od toho stačí použít `sudo apt-get upgrade powershell` jej aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="f954f-153">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="f954f-154">Instalace prostřednictvím přímé stahování - Debian 9</span><span class="sxs-lookup"><span data-stu-id="f954f-154">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="f954f-155">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.9_amd64.deb` z [Verze][] stránky do Debian počítače.</span><span class="sxs-lookup"><span data-stu-id="f954f-155">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="f954f-156">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-156">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="f954f-157">Pamatujte, že `dpkg -i` se nezdaří s unmet závislosti.</span><span class="sxs-lookup"><span data-stu-id="f954f-157">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="f954f-158">Další příkaz `apt-get install -f` řeší tyto a pak dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-158">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="f954f-159">Odinstalace - Debian 9</span><span class="sxs-lookup"><span data-stu-id="f954f-159">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="f954f-160">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f954f-160">CentOS 7</span></span>

> <span data-ttu-id="f954f-161">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="f954f-161">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="f954f-162">Instalaci přes úložiště balíčků (doporučeno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f954f-162">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="f954f-163">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-163">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="f954f-164">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-164">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="f954f-165">Instalace prostřednictvím přímé stahování - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f954f-165">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="f954f-166">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [Verze][] stránky do počítače CentOS.</span><span class="sxs-lookup"><span data-stu-id="f954f-166">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="f954f-167">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-167">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f954f-168">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="f954f-168">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="f954f-169">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f954f-169">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f954f-171">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="f954f-171">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f954f-172">Instalaci přes úložiště balíčků (doporučeno) - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="f954f-172">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="f954f-173">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-173">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="f954f-174">Po registraci jednou úložiště společnosti Microsoft jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-174">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f954f-175">Instalace prostřednictvím přímé stahování - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="f954f-175">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="f954f-176">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [Verze][] stránky do počítače Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="f954f-176">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="f954f-177">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-177">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f954f-178">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="f954f-178">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f954f-179">Odinstalace - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="f954f-179">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="f954f-180">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="f954f-180">OpenSUSE 42.2</span></span>

> [!NOTE]
> <span data-ttu-id="f954f-181">Při instalaci prostředí PowerShell základní `zypper` může nahlaste mu následující chybu:</span><span class="sxs-lookup"><span data-stu-id="f954f-181">When installing PowerShell Core, `zypper` may report the following error:</span></span>
>
> ```Output
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> <span data-ttu-id="f954f-182">V takovém případě ověřte, že kompatibilní `libcurl` knihovny nachází kontrolou, že následující příkaz ukazuje `libcurl4` balíčku se po instalaci:</span><span class="sxs-lookup"><span data-stu-id="f954f-182">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> <span data-ttu-id="f954f-183">Zvolte `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f954f-183">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="f954f-184">Instalaci přes úložiště balíčků (doporučeno) - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="f954f-184">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="f954f-185">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-185">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="f954f-186">Instalace prostřednictvím přímé stahování - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="f954f-186">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="f954f-187">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [Verze][] stránky do počítače OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="f954f-187">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f954f-188">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="f954f-188">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="f954f-189">Odinstalace - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="f954f-189">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="f954f-190">Fedora</span><span class="sxs-lookup"><span data-stu-id="f954f-190">Fedora</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="f954f-191">Instalaci přes úložiště balíčků (doporučeno) - Fedora 27 Fedora 28</span><span class="sxs-lookup"><span data-stu-id="f954f-191">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="f954f-192">Základní prostředí PowerShell pro Linux je publikovaný na oficiální Microsoft úložiště pro Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="f954f-192">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="f954f-193">Instalace prostřednictvím přímé stahování - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="f954f-193">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="f954f-194">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [Verze][] stránky do počítače Fedora.</span><span class="sxs-lookup"><span data-stu-id="f954f-194">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="f954f-195">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-195">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f954f-196">Můžete taky nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="f954f-196">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="f954f-197">Odinstalace - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="f954f-197">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="f954f-198">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="f954f-198">Arch Linux</span></span>

<span data-ttu-id="f954f-199">PowerShell je k dispozici [Arch Linux][] uživatele úložiště (AUR).</span><span class="sxs-lookup"><span data-stu-id="f954f-199">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="f954f-200">Může být zkompilován s [označené nejnovější verze][arch-release]</span><span class="sxs-lookup"><span data-stu-id="f954f-200">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="f954f-201">Mohou být zkompilovány z [nejnovější potvrzení změn na hlavní server][arch-git]</span><span class="sxs-lookup"><span data-stu-id="f954f-201">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="f954f-202">Můžete nainstalovat, pomocí [nejnovější verzi binární][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="f954f-202">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="f954f-203">Balíčky v AUR jsou udržuje komunitní – neexistuje žádná podpora oficiální.</span><span class="sxs-lookup"><span data-stu-id="f954f-203">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="f954f-204">Další informace o instalaci balíčků z AUR najdete v tématu [architektura Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunity [soubor Docker](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="f954f-204">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="f954f-206">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="f954f-206">Linux AppImage</span></span>

<span data-ttu-id="f954f-207">Pomocí poslední distribuci systému Linux, stáhněte si AppImage `powershell-6.0.1-x86_64.AppImage` z [Verze][] stránky do počítače Linux.</span><span class="sxs-lookup"><span data-stu-id="f954f-207">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="f954f-208">Potom spusťte následující v terminálu:</span><span class="sxs-lookup"><span data-stu-id="f954f-208">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="f954f-209">[AppImage][] vám umožní spustit prostředí PowerShell bez jeho instalaci.</span><span class="sxs-lookup"><span data-stu-id="f954f-209">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="f954f-210">Je přenosné aplikace, která obsahuje ureitou prostředí PowerShell a jeho závislosti (včetně závislostí systému .NET Core) do jednoho získá na ucelenosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="f954f-210">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="f954f-211">Tento balíček je jednoho binárního souboru, který funguje nezávisle na distribuční Linux uživatele.</span><span class="sxs-lookup"><span data-stu-id="f954f-211">This package  is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="f954f-213">Kali</span><span class="sxs-lookup"><span data-stu-id="f954f-213">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="f954f-214">Instalace</span><span class="sxs-lookup"><span data-stu-id="f954f-214">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="f954f-215">Spusťte prostředí PowerShell bez instalace se v nejnovější Kali (vrácení Kali GNU/Linux)</span><span class="sxs-lookup"><span data-stu-id="f954f-215">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="f954f-216">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="f954f-216">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="f954f-217">Raspbian</span><span class="sxs-lookup"><span data-stu-id="f954f-217">Raspbian</span></span>

<span data-ttu-id="f954f-218">V současné době prostředí PowerShell je podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="f954f-218">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="f954f-219">Také CoreCLR (a tedy základní prostředí PowerShell) budou fungovat jenom na zařízení pí 2 a 3 platformy jako další zařízení, jako je třeba [pí nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesoru.</span><span class="sxs-lookup"><span data-stu-id="f954f-219">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="f954f-220">Stáhnout [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) pro přístup na váš pí.</span><span class="sxs-lookup"><span data-stu-id="f954f-220">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="f954f-221">Instalace</span><span class="sxs-lookup"><span data-stu-id="f954f-221">Installation</span></span>

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

<span data-ttu-id="f954f-222">Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty k "pwsh" binární</span><span class="sxs-lookup"><span data-stu-id="f954f-222">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="f954f-223">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="f954f-223">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="f954f-224">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="f954f-224">Binary Archives</span></span>

<span data-ttu-id="f954f-225">Prostředí PowerShell binární `tar.gz` archivy jsou k dispozici pro Linux platformy a povolíte pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="f954f-225">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="f954f-226">Závislosti</span><span class="sxs-lookup"><span data-stu-id="f954f-226">Dependencies</span></span>

<span data-ttu-id="f954f-227">Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce systému Linux.</span><span class="sxs-lookup"><span data-stu-id="f954f-227">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="f954f-228">Ale .NET Core runtime vyžaduje jiný závislosti na různých distribucí, a proto prostředí PowerShell dělá to stejné.</span><span class="sxs-lookup"><span data-stu-id="f954f-228">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="f954f-229">Následující graf zobrazuje závislosti rozhraní .NET 2.0 jádra, které jsou oficiálně podporované v různých distribucí Linux.</span><span class="sxs-lookup"><span data-stu-id="f954f-229">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="f954f-230">Operační systém</span><span class="sxs-lookup"><span data-stu-id="f954f-230">OS</span></span>                 | <span data-ttu-id="f954f-231">Závislosti</span><span class="sxs-lookup"><span data-stu-id="f954f-231">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="f954f-232">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f954f-232">Ubuntu 14.04</span></span>       | <span data-ttu-id="f954f-233">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="f954f-233">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f954f-234">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="f954f-234">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="f954f-235">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f954f-235">Ubuntu 16.04</span></span>       | <span data-ttu-id="f954f-236">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="f954f-236">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f954f-237">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="f954f-237">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="f954f-238">Ubuntu č. 17.04</span><span class="sxs-lookup"><span data-stu-id="f954f-238">Ubuntu 17.04</span></span>       | <span data-ttu-id="f954f-239">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="f954f-239">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f954f-240">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="f954f-240">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="f954f-241">Debian 8 (Klára)</span><span class="sxs-lookup"><span data-stu-id="f954f-241">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="f954f-242">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="f954f-242">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f954f-243">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="f954f-243">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="f954f-244">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="f954f-244">Debian 9 (Stretch)</span></span> | <span data-ttu-id="f954f-245">libc6, ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="f954f-245">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f954f-246">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="f954f-246">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="f954f-247">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f954f-247">CentOS 7</span></span> <br> <span data-ttu-id="f954f-248">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="f954f-248">Oracle Linux 7</span></span> <br> <span data-ttu-id="f954f-249">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="f954f-249">RHEL 7</span></span> <br> <span data-ttu-id="f954f-250">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="f954f-250">OpenSUSE 42.2</span></span> | <span data-ttu-id="f954f-251">libunwind, libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="f954f-251">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="f954f-252">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="f954f-252">Fedora 27</span></span> <br> <span data-ttu-id="f954f-253">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="f954f-253">Fedora 28</span></span> | <span data-ttu-id="f954f-254">libunwind, libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="f954f-254">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="f954f-255">Pokud chcete nasadit binární soubory prostředí PowerShell na Linuxových distribucích, které nejsou oficiálně podporované, musíte nainstalovat potřebné závislosti pro cílový operační systém v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="f954f-255">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="f954f-256">Například naše [soubor docker Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a pak extrahuje sady Linux `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="f954f-256">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="f954f-257">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="f954f-257">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="f954f-258">Linux</span><span class="sxs-lookup"><span data-stu-id="f954f-258">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="f954f-259">Odinstalaci binární archivy</span><span class="sxs-lookup"><span data-stu-id="f954f-259">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="f954f-260">Cesty</span><span class="sxs-lookup"><span data-stu-id="f954f-260">Paths</span></span>

* <span data-ttu-id="f954f-261">`$PSHOME` je `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="f954f-261">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="f954f-262">Profily uživatelů, bude číst ze `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f954f-262">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="f954f-263">Výchozí profily bude číst ze `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f954f-263">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="f954f-264">Moduly uživatele bude číst ze `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f954f-264">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f954f-265">Sdílené moduly, bude číst ze `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f954f-265">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f954f-266">Výchozí moduly, bude číst ze `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="f954f-266">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="f954f-267">Historie PSReadline budou zaznamenány do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="f954f-267">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="f954f-268">Profily respektují konfigurace Powershellu na hostitele, takže výchozí konkrétního hostitele profily existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="f954f-268">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="f954f-269">Prostředí PowerShell respektuje [XDG základní Directory specifikace] [ xdg-bds] v systému Linux.</span><span class="sxs-lookup"><span data-stu-id="f954f-269">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[Verze]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

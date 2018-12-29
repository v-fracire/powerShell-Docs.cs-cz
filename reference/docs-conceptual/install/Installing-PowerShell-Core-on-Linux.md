---
title: Instalace PowerShellu Core v Linuxu
description: Informace o instalaci Powershellu Core v různých distribucích systému Linux
ms.date: 08/06/2018
ms.openlocfilehash: afb11f053517af592fe42754d543f9f4a9966c5b
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403753"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="104f2-103">Instalace PowerShellu Core v Linuxu</span><span class="sxs-lookup"><span data-stu-id="104f2-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="104f2-104">Podporuje [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04] [ u1804], [Ubuntu 18.10][u1810], [Debian 8][deb8], [Debian 9] [ deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE skok 15][opensuse], [Fedora 27][fedora], [ Fedora 28][fedora], a [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="104f2-104">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="104f2-105">Pro distribuce Linuxu, které nejsou oficiálně podporované, můžete zkusit použít [balíčků v Powershellu Přichytit][snap].</span><span class="sxs-lookup"><span data-stu-id="104f2-105">For Linux distributions that are not officially supported, you can try using the [PowerShell Snap Package][snap].</span></span>
<span data-ttu-id="104f2-106">Nasazení prostředí PowerShell binární soubory přímo s Linuxem můžete také zkusit [ `tar.gz` archivu][tar], ale je potřeba nastavit potřebné závislosti podle operačního systému v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="104f2-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="104f2-107">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="104f2-107">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="104f2-108">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="104f2-108">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u1804]: #ubuntu-1804
[u1810]: #ubuntu-1810
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="104f2-109">Instalace Preview verzí</span><span class="sxs-lookup"><span data-stu-id="104f2-109">Installing Preview Releases</span></span>

<span data-ttu-id="104f2-110">Při instalaci verze Preview prostředí PowerShell Core pro Linux přes úložiště balíčků, názvu balíčku se změní z `powershell` k `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="104f2-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="104f2-111">Instalace přes přímé stažení nezmění, než je název souboru.</span><span class="sxs-lookup"><span data-stu-id="104f2-111">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="104f2-112">Tady je tabulka znázorňující příkazy, abyste nainstalovali stabilní verze a preview balíčků pomocí různých správců balíčků:</span><span class="sxs-lookup"><span data-stu-id="104f2-112">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="104f2-113">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="104f2-113">Distribution(s)</span></span>|<span data-ttu-id="104f2-114">Stabilní příkaz</span><span class="sxs-lookup"><span data-stu-id="104f2-114">Stable Command</span></span> | <span data-ttu-id="104f2-115">Příkaz ve verzi Preview</span><span class="sxs-lookup"><span data-stu-id="104f2-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="104f2-116">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="104f2-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="104f2-117">CentOS, Red Hat</span><span class="sxs-lookup"><span data-stu-id="104f2-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="104f2-118">Fedora</span><span class="sxs-lookup"><span data-stu-id="104f2-118">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="104f2-119">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="104f2-119">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="104f2-120">Instalace přes úložiště balíčků – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="104f2-120">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="104f2-121">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-121">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="104f2-122">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="104f2-122">This is the preferred method.</span></span>

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

<span data-ttu-id="104f2-123">Jako superuživatele zaregistrujte úložiště společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="104f2-123">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="104f2-124">Od té chvíle stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.</span><span class="sxs-lookup"><span data-stu-id="104f2-124">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="104f2-125">Instalace přes přímé stažení – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="104f2-125">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="104f2-126">Stáhněte si balíček Debian `powershell_6.1.0-1.ubuntu.14.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="104f2-126">Download the Debian package `powershell_6.1.0-1.ubuntu.14.04_amd64.deb`</span></span>
<span data-ttu-id="104f2-127">z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="104f2-127">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="104f2-128">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-128">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="104f2-129">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="104f2-129">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="104f2-130">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="104f2-130">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="104f2-131">Odinstalace – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="104f2-131">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="104f2-132">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="104f2-132">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="104f2-133">Instalace přes úložiště balíčků – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="104f2-133">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="104f2-134">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-134">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="104f2-135">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="104f2-135">This is the preferred method.</span></span>

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

<span data-ttu-id="104f2-136">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="104f2-136">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="104f2-137">Instalace přes přímé stažení – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="104f2-137">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="104f2-138">Stáhněte si balíček Debian `powershell_6.1.0-1.ubuntu.16.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="104f2-138">Download the Debian package `powershell_6.1.0-1.ubuntu.16.04_amd64.deb`</span></span>
<span data-ttu-id="104f2-139">z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="104f2-139">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="104f2-140">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-140">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="104f2-141">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="104f2-141">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="104f2-142">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="104f2-142">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="104f2-143">Odinstalace – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="104f2-143">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="104f2-144">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="104f2-144">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="104f2-145">Přidali jsme podporu pro Ubuntu 18.04 po `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="104f2-145">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="104f2-146">Instalace přes úložiště balíčků – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="104f2-146">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="104f2-147">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-147">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="104f2-148">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="104f2-148">This is the preferred method.</span></span>

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

<span data-ttu-id="104f2-149">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="104f2-149">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="104f2-150">Instalace přes přímé stažení – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="104f2-150">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="104f2-151">Stáhněte si balíček Debian `powershell_6.1.0-1.ubuntu.18.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="104f2-151">Download the Debian package `powershell_6.1.0-1.ubuntu.18.04_amd64.deb`</span></span>
<span data-ttu-id="104f2-152">z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="104f2-152">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="104f2-153">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-153">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="104f2-154">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="104f2-154">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="104f2-155">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="104f2-155">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="104f2-156">Odinstalace – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="104f2-156">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="104f2-157">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="104f2-157">Ubuntu 18.10</span></span>

> [!NOTE]
> <span data-ttu-id="104f2-158">Přidali jsme podporu pro Ubuntu 18.10 po `6.1.0-preview.3`.</span><span class="sxs-lookup"><span data-stu-id="104f2-158">Support for Ubuntu 18.10 was added after `6.1.0-preview.3`.</span></span>
> <span data-ttu-id="104f2-159">Je 18.10 každodenními buildy, je podporovaná pouze komunitou.</span><span class="sxs-lookup"><span data-stu-id="104f2-159">As 18.10 is a daily build, it is only community supported.</span></span>

<span data-ttu-id="104f2-160">Instalace na 18.10 je podporované prostřednictvím `snapd`.</span><span class="sxs-lookup"><span data-stu-id="104f2-160">Installing on 18.10 is supported via `snapd`.</span></span> <span data-ttu-id="104f2-161">Zobrazit [Přichytit balíček] [ snap] úplné pokyny;</span><span class="sxs-lookup"><span data-stu-id="104f2-161">See [Snap Package][snap] for full instructions;</span></span>

## <a name="debian-8"></a><span data-ttu-id="104f2-162">Debian 8</span><span class="sxs-lookup"><span data-stu-id="104f2-162">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="104f2-163">Instalace přes úložiště balíčků – Debian 8</span><span class="sxs-lookup"><span data-stu-id="104f2-163">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="104f2-164">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-164">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="104f2-165">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="104f2-165">This is the preferred method.</span></span>

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

<span data-ttu-id="104f2-166">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="104f2-166">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="104f2-167">Instalace přes přímé stažení – Debian 8</span><span class="sxs-lookup"><span data-stu-id="104f2-167">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="104f2-168">Stáhněte si balíček Debian `powershell_6.1.0-1.debian.8_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="104f2-168">Download the Debian package `powershell_6.1.0-1.debian.8_amd64.deb`</span></span>
<span data-ttu-id="104f2-169">z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="104f2-169">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="104f2-170">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-170">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="104f2-171">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="104f2-171">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="104f2-172">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="104f2-172">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="104f2-173">Odinstalace – Debian 8</span><span class="sxs-lookup"><span data-stu-id="104f2-173">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="104f2-174">Debian 9</span><span class="sxs-lookup"><span data-stu-id="104f2-174">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="104f2-175">Instalace přes úložiště balíčků – Debian 9</span><span class="sxs-lookup"><span data-stu-id="104f2-175">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="104f2-176">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-176">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="104f2-177">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="104f2-177">This is the preferred method.</span></span>

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

<span data-ttu-id="104f2-178">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="104f2-178">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="104f2-179">Instalace přes přímé stažení – Debian 9</span><span class="sxs-lookup"><span data-stu-id="104f2-179">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="104f2-180">Stáhněte si balíček Debian `powershell_6.1.0-1.debian.9_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="104f2-180">Download the Debian package `powershell_6.1.0-1.debian.9_amd64.deb`</span></span>
<span data-ttu-id="104f2-181">z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="104f2-181">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="104f2-182">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-182">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="104f2-183">Odinstalace – Debian 9</span><span class="sxs-lookup"><span data-stu-id="104f2-183">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="104f2-184">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="104f2-184">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="104f2-185">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="104f2-185">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="104f2-186">Instalace přes úložiště balíčků (upřednostňováno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="104f2-186">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="104f2-187">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-187">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="104f2-188">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="104f2-188">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="104f2-189">Instalace přes přímé stažení - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="104f2-189">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="104f2-190">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="104f2-190">Using [CentOS 7][], download the RPM package `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="104f2-191">z [uvolní][] stránky do počítače CentOS.</span><span class="sxs-lookup"><span data-stu-id="104f2-191">from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="104f2-192">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-192">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="104f2-193">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="104f2-193">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="104f2-194">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="104f2-194">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="104f2-196">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="104f2-196">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="104f2-197">Instalace přes úložiště balíčků (upřednostňováno) – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="104f2-197">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="104f2-198">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-198">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="104f2-199">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="104f2-199">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="104f2-200">Instalace přes přímé stažení – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="104f2-200">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="104f2-201">Stáhněte si balíček RPM `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="104f2-201">Download the RPM package `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="104f2-202">z [uvolní][] stránky do počítače, Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="104f2-202">from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="104f2-203">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-203">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="104f2-204">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="104f2-204">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="104f2-205">Odinstalace – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="104f2-205">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a><span data-ttu-id="104f2-206">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="104f2-206">openSUSE</span></span>

### <a name="installation---opensuse-423"></a><span data-ttu-id="104f2-207">Instalace - openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="104f2-207">Installation - openSUSE 42.3</span></span>

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar libicu52_1

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.1.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.1.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.1.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="installation---opensuse-leap-15"></a><span data-ttu-id="104f2-208">Instalace - openSUSE skok 15</span><span class="sxs-lookup"><span data-stu-id="104f2-208">Installation - openSUSE Leap 15</span></span>

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar gzip libopenssl1_0_0 libicu60_2

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.1.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.1.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.1.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a><span data-ttu-id="104f2-209">Odinstalace - openSUSE 42.3, openSUSE skok 15</span><span class="sxs-lookup"><span data-stu-id="104f2-209">Uninstallation - openSUSE 42.3, openSUSE Leap 15</span></span>

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a><span data-ttu-id="104f2-210">Fedora</span><span class="sxs-lookup"><span data-stu-id="104f2-210">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="104f2-211">Fedora 28 je podporována pouze v prostředí PowerShell Core 6.1 a novější.</span><span class="sxs-lookup"><span data-stu-id="104f2-211">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="104f2-212">Instalace přes úložiště balíčků (upřednostňováno) - Fedora 27 Fedora 28</span><span class="sxs-lookup"><span data-stu-id="104f2-212">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="104f2-213">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-213">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="104f2-214">Instalace přes přímé stažení - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="104f2-214">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="104f2-215">Stáhněte si balíček RPM `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="104f2-215">Download the RPM package `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="104f2-216">z [uvolní][] stránky do počítače, Fedora.</span><span class="sxs-lookup"><span data-stu-id="104f2-216">from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="104f2-217">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="104f2-217">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="104f2-218">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="104f2-218">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="104f2-219">Odinstalace - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="104f2-219">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="104f2-220">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="104f2-220">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="104f2-221">Podpora architektury je experimentální.</span><span class="sxs-lookup"><span data-stu-id="104f2-221">Arch support is experimental.</span></span>

<span data-ttu-id="104f2-222">PowerShell je k dispozici [Arch Linux][] úložišti uživatele (AUR).</span><span class="sxs-lookup"><span data-stu-id="104f2-222">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="104f2-223">Může být zkompilován s [označené nejnovější verzi][arch-release]</span><span class="sxs-lookup"><span data-stu-id="104f2-223">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="104f2-224">Mohou být zkompilovány z [nejnovější potvrzení změn do hlavní větve][arch-git]</span><span class="sxs-lookup"><span data-stu-id="104f2-224">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="104f2-225">Nainstalujete ho pomocí [nejnovější verze binárního souboru][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="104f2-225">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="104f2-226">Balíčky AUR jsou komunity udržuje – neexistuje žádná oficiální podpora.</span><span class="sxs-lookup"><span data-stu-id="104f2-226">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="104f2-227">Další informace o instalaci balíčků z AUR najdete v tématu [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunitou [soubor DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="104f2-227">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="104f2-229">Přichytit balíčku</span><span class="sxs-lookup"><span data-stu-id="104f2-229">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="104f2-230">Získávání snapd</span><span class="sxs-lookup"><span data-stu-id="104f2-230">Getting snapd</span></span>

<span data-ttu-id="104f2-231">`snapd` je požadován pro spuštění při kolika rozehrávkách byli.</span><span class="sxs-lookup"><span data-stu-id="104f2-231">`snapd` is required to run snaps.</span></span>
<span data-ttu-id="104f2-232">Použití [tyto pokyny](https://docs.snapcraft.io/core/install) abyste měli jistotu, že máte `snapd` nainstalované.</span><span class="sxs-lookup"><span data-stu-id="104f2-232">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="104f2-233">Instalace přes modul Snap</span><span class="sxs-lookup"><span data-stu-id="104f2-233">Installation via Snap</span></span>

<span data-ttu-id="104f2-234">PowerShell Core pro Linux, je publikovaná [Snap úložiště](https://snapcraft.io/store) Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="104f2-234">PowerShell Core, for Linux, is published to the [Snap store](https://snapcraft.io/store) for easy installation (and updates).</span></span>
<span data-ttu-id="104f2-235">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="104f2-235">This is the preferred method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

<span data-ttu-id="104f2-236">Pokud chcete nainstalovat verzi preview, použít následující metody.</span><span class="sxs-lookup"><span data-stu-id="104f2-236">If you want to install preview version, use following method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="104f2-237">Po instalaci modulu Snap budou automaticky upgradovat, ale můžete aktivovat upgradu pomocí `sudo snap refresh powershell` nebo `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="104f2-237">After installing Snap will automatically upgrade, but you can trigger an upgrade using `sudo snap refresh powershell` or `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="104f2-238">Odinstalace</span><span class="sxs-lookup"><span data-stu-id="104f2-238">Uninstallation</span></span>

```sh
sudo snap remove powershell
```

<span data-ttu-id="104f2-239">nebo</span><span class="sxs-lookup"><span data-stu-id="104f2-239">or</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a><span data-ttu-id="104f2-240">Kali</span><span class="sxs-lookup"><span data-stu-id="104f2-240">Kali</span></span>

### <a name="installation---kali"></a><span data-ttu-id="104f2-241">Instalace - Kali</span><span class="sxs-lookup"><span data-stu-id="104f2-241">Installation - Kali</span></span>

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

### <a name="uninstallation---kali"></a><span data-ttu-id="104f2-242">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="104f2-242">Uninstallation - Kali</span></span>

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a><span data-ttu-id="104f2-243">Raspbian</span><span class="sxs-lookup"><span data-stu-id="104f2-243">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="104f2-244">Podpora Raspbian je experimentální.</span><span class="sxs-lookup"><span data-stu-id="104f2-244">Raspbian support is experimental.</span></span>

<span data-ttu-id="104f2-245">Prostředí PowerShell je v současné době podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="104f2-245">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="104f2-246">Také CoreCLR (a tedy PowerShell Core) bude fungovat jenom na zařízeních Pi 2 a Pi 3 jako jiná zařízení, jako je třeba [Pi nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesor.</span><span class="sxs-lookup"><span data-stu-id="104f2-246">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="104f2-247">Stáhněte si [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) zobrazíte na vaše číslo pí.</span><span class="sxs-lookup"><span data-stu-id="104f2-247">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation---raspbian"></a><span data-ttu-id="104f2-248">Instalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="104f2-248">Installation - Raspbian</span></span>

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

<span data-ttu-id="104f2-249">Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty ke "pwsh" binární</span><span class="sxs-lookup"><span data-stu-id="104f2-249">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="104f2-250">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="104f2-250">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="104f2-251">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="104f2-251">Binary Archives</span></span>

<span data-ttu-id="104f2-252">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformy Linux umožňuje pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="104f2-252">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="104f2-253">Závislosti</span><span class="sxs-lookup"><span data-stu-id="104f2-253">Dependencies</span></span>

<span data-ttu-id="104f2-254">Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce Linuxu.</span><span class="sxs-lookup"><span data-stu-id="104f2-254">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="104f2-255">Ale modulu runtime .NET Core vyžaduje různých závislostí v různých distribucích a proto Powershellu dělá to samé.</span><span class="sxs-lookup"><span data-stu-id="104f2-255">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="104f2-256">Následující graf ukazuje závislosti rozhraní .NET Core 2.0, oficiálně podporované v různých distribucích systému Linux.</span><span class="sxs-lookup"><span data-stu-id="104f2-256">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="104f2-257">Operační systém</span><span class="sxs-lookup"><span data-stu-id="104f2-257">OS</span></span>                 | <span data-ttu-id="104f2-258">Závislosti</span><span class="sxs-lookup"><span data-stu-id="104f2-258">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="104f2-259">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="104f2-259">Ubuntu 14.04</span></span>       | <span data-ttu-id="104f2-260">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="104f2-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="104f2-261">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="104f2-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="104f2-262">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="104f2-262">Ubuntu 16.04</span></span>       | <span data-ttu-id="104f2-263">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="104f2-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="104f2-264">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="104f2-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="104f2-265">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="104f2-265">Ubuntu 17.10</span></span>       | <span data-ttu-id="104f2-266">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="104f2-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="104f2-267">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="104f2-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="104f2-268">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="104f2-268">Ubuntu 18.04</span></span>       | <span data-ttu-id="104f2-269">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="104f2-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="104f2-270">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="104f2-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="104f2-271">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="104f2-271">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="104f2-272">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="104f2-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="104f2-273">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="104f2-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="104f2-274">Debian 9 (roztáhnout)</span><span class="sxs-lookup"><span data-stu-id="104f2-274">Debian 9 (Stretch)</span></span> | <span data-ttu-id="104f2-275">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="104f2-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="104f2-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="104f2-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="104f2-277">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="104f2-277">CentOS 7</span></span> <br> <span data-ttu-id="104f2-278">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="104f2-278">Oracle Linux 7</span></span> <br> <span data-ttu-id="104f2-279">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="104f2-279">RHEL 7</span></span> | <span data-ttu-id="104f2-280">libunwind libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="104f2-280">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="104f2-281">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="104f2-281">openSUSE 42.3</span></span> | <span data-ttu-id="104f2-282">libcurl4 libopenssl1_0_0, libicu52_1</span><span class="sxs-lookup"><span data-stu-id="104f2-282">libcurl4, libopenssl1_0_0, libicu52_1</span></span> |
| <span data-ttu-id="104f2-283">openSUSE skok 15</span><span class="sxs-lookup"><span data-stu-id="104f2-283">openSUSE Leap 15</span></span> | <span data-ttu-id="104f2-284">libcurl4 libopenssl1_0_0, libicu60_2</span><span class="sxs-lookup"><span data-stu-id="104f2-284">libcurl4, libopenssl1_0_0, libicu60_2</span></span> |
| <span data-ttu-id="104f2-285">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="104f2-285">Fedora 27</span></span> <br> <span data-ttu-id="104f2-286">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="104f2-286">Fedora 28</span></span> | <span data-ttu-id="104f2-287">libunwind libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="104f2-287">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="104f2-288">K nasazení binárních souborů prostředí PowerShell v Linuxových distribucích, které nejsou oficiálně podporované, budete muset nainstalovat potřebné závislosti pro cílový operační systém v samostatných krocích.</span><span class="sxs-lookup"><span data-stu-id="104f2-288">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="104f2-289">Například náš [soubor dockerfile Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a poté rozbalí Linuxový `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="104f2-289">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="104f2-290">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="104f2-290">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="104f2-291">Linux</span><span class="sxs-lookup"><span data-stu-id="104f2-291">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="104f2-292">Probíhá odinstalace binárního archivy</span><span class="sxs-lookup"><span data-stu-id="104f2-292">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="104f2-293">Cesty</span><span class="sxs-lookup"><span data-stu-id="104f2-293">Paths</span></span>

* <span data-ttu-id="104f2-294">`$PSHOME` je `/opt/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="104f2-294">`$PSHOME` is `/opt/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="104f2-295">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="104f2-295">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="104f2-296">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="104f2-296">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="104f2-297">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="104f2-297">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="104f2-298">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="104f2-298">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="104f2-299">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="104f2-299">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="104f2-300">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="104f2-300">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="104f2-301">Profily respektovat konfigurace Powershellu na hostitele, takže výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="104f2-301">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="104f2-302">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v Linuxu.</span><span class="sxs-lookup"><span data-stu-id="104f2-302">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

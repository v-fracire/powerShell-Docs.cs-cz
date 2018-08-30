---
title: Instalace PowerShellu Core v Linuxu
description: Informace o instalaci Powershellu Core v různých distribucích systému Linux
ms.date: 08/06/2018
ms.openlocfilehash: 0a1f30ef75a0feeb97df9a35a08d6b0d3edaeccf
ms.sourcegitcommit: 56b9be8503a5a1342c0b85b36f5ba6f57c281b63
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/21/2018
ms.locfileid: "43133846"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="c7c25-103">Instalace PowerShellu Core v Linuxu</span><span class="sxs-lookup"><span data-stu-id="c7c25-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="c7c25-104">Podporuje [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.10] [ u18], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27 ] [ fedora], [Fedora 28][fedora], a [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="c7c25-104">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.10][u18], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="c7c25-105">Pro distribuce Linuxu, které nejsou oficiálně podporované, můžete zkusit použít [balíčků v Powershellu Přichytit][snap].</span><span class="sxs-lookup"><span data-stu-id="c7c25-105">For Linux distributions that are not officially supported, you can try using the [PowerShell Snap Package][snap].</span></span>
<span data-ttu-id="c7c25-106">Nasazení prostředí PowerShell binární soubory přímo s Linuxem můžete také zkusit [ `tar.gz` archivu][tar], ale je potřeba nastavit potřebné závislosti podle operačního systému v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="c7c25-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="c7c25-107">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="c7c25-107">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="c7c25-108">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="c7c25-108">Once the package is installed, run `pwsh` from a terminal.</span></span>

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

## <a name="installing-preview-releases"></a><span data-ttu-id="c7c25-109">Instalace Preview verzí</span><span class="sxs-lookup"><span data-stu-id="c7c25-109">Installing Preview Releases</span></span>

<span data-ttu-id="c7c25-110">Při instalaci verze Preview prostředí PowerShell Core pro Linux přes úložiště balíčků, názvu balíčku se změní z `powershell` k `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="c7c25-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="c7c25-111">Instalace přes přímé stažení nezmění, než je název souboru.</span><span class="sxs-lookup"><span data-stu-id="c7c25-111">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="c7c25-112">Tady je tabulka znázorňující příkazy, abyste nainstalovali stabilní verze a preview balíčků pomocí různých správců balíčků:</span><span class="sxs-lookup"><span data-stu-id="c7c25-112">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="c7c25-113">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="c7c25-113">Distribution(s)</span></span>|<span data-ttu-id="c7c25-114">Stabilní příkaz</span><span class="sxs-lookup"><span data-stu-id="c7c25-114">Stable Command</span></span> | <span data-ttu-id="c7c25-115">Příkaz ve verzi Preview</span><span class="sxs-lookup"><span data-stu-id="c7c25-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="c7c25-116">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="c7c25-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="c7c25-117">CentOS, Red Hat</span><span class="sxs-lookup"><span data-stu-id="c7c25-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="c7c25-118">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="c7c25-118">OpenSUSE</span></span> |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| <span data-ttu-id="c7c25-119">Fedora</span><span class="sxs-lookup"><span data-stu-id="c7c25-119">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="c7c25-120">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-120">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="c7c25-121">Instalace přes úložiště balíčků – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-121">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="c7c25-122">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-122">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c7c25-123">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c7c25-123">This is the preferred method.</span></span>

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

<span data-ttu-id="c7c25-124">Jako superuživatele zaregistrujte úložiště společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c7c25-124">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="c7c25-125">Od té chvíle stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.</span><span class="sxs-lookup"><span data-stu-id="c7c25-125">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="c7c25-126">Instalace přes přímé stažení – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-126">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="c7c25-127">Stáhněte si balíček Debian `powershell_6.0.3-1.ubuntu.14.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="c7c25-127">Download the Debian package `powershell_6.0.3-1.ubuntu.14.04_amd64.deb`</span></span>
<span data-ttu-id="c7c25-128">z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c7c25-128">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c7c25-129">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-129">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.3-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c7c25-130">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c7c25-130">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c7c25-131">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c25-131">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="c7c25-132">Odinstalace – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-132">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="c7c25-133">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-133">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="c7c25-134">Instalace přes úložiště balíčků – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-134">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="c7c25-135">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-135">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c7c25-136">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c7c25-136">This is the preferred method.</span></span>

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

<span data-ttu-id="c7c25-137">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c7c25-137">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="c7c25-138">Instalace přes přímé stažení – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-138">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="c7c25-139">Stáhněte si balíček Debian `powershell_6.0.3-1.ubuntu.16.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="c7c25-139">Download the Debian package `powershell_6.0.3-1.ubuntu.16.04_amd64.deb`</span></span>
<span data-ttu-id="c7c25-140">z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c7c25-140">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c7c25-141">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-141">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.3-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c7c25-142">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c7c25-142">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c7c25-143">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c25-143">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="c7c25-144">Odinstalace – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-144">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="c7c25-145">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-145">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-146">Přidali jsme podporu pro Ubuntu 18.04 po `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="c7c25-146">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="c7c25-147">Instalace přes úložiště balíčků – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-147">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="c7c25-148">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-148">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c7c25-149">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c7c25-149">This is the preferred method.</span></span>

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

<span data-ttu-id="c7c25-150">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c7c25-150">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="c7c25-151">Instalace přes přímé stažení – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-151">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="c7c25-152">Stáhněte si balíček Debian `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="c7c25-152">Download the Debian package `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb`</span></span>
<span data-ttu-id="c7c25-153">z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c7c25-153">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="c7c25-154">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-154">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c7c25-155">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c7c25-155">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c7c25-156">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c25-156">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="c7c25-157">Odinstalace – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-157">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="c7c25-158">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="c7c25-158">Ubuntu 18.10</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-159">Přidali jsme podporu pro Ubuntu 18.10 po `6.1.0-preview.3`.</span><span class="sxs-lookup"><span data-stu-id="c7c25-159">Support for Ubuntu 18.10 was added after `6.1.0-preview.3`.</span></span>
> <span data-ttu-id="c7c25-160">Je 18.10 každodenními buildy, je podporovaná pouze komunitou.</span><span class="sxs-lookup"><span data-stu-id="c7c25-160">As 18.10 is a daily build, it is only community supported.</span></span>

<span data-ttu-id="c7c25-161">Instalace na 18.10 je podporované prostřednictvím `snapd`.</span><span class="sxs-lookup"><span data-stu-id="c7c25-161">Installing on 18.10 is supported via `snapd`.</span></span> <span data-ttu-id="c7c25-162">Zobrazit [Přichytit balíček] [ snap] úplné pokyny;</span><span class="sxs-lookup"><span data-stu-id="c7c25-162">See [Snap Package][snap] for full instructions;</span></span>

## <a name="debian-8"></a><span data-ttu-id="c7c25-163">Debian 8</span><span class="sxs-lookup"><span data-stu-id="c7c25-163">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="c7c25-164">Instalace přes úložiště balíčků – Debian 8</span><span class="sxs-lookup"><span data-stu-id="c7c25-164">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="c7c25-165">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-165">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c7c25-166">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c7c25-166">This is the preferred method.</span></span>

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

<span data-ttu-id="c7c25-167">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c7c25-167">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="c7c25-168">Instalace přes přímé stažení – Debian 8</span><span class="sxs-lookup"><span data-stu-id="c7c25-168">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="c7c25-169">Stáhněte si balíček Debian `powershell_6.0.3-1.debian.8_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="c7c25-169">Download the Debian package `powershell_6.0.3-1.debian.8_amd64.deb`</span></span>
<span data-ttu-id="c7c25-170">z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="c7c25-170">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="c7c25-171">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-171">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.3-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="c7c25-172">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="c7c25-172">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="c7c25-173">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c25-173">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="c7c25-174">Odinstalace – Debian 8</span><span class="sxs-lookup"><span data-stu-id="c7c25-174">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="c7c25-175">Debian 9</span><span class="sxs-lookup"><span data-stu-id="c7c25-175">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="c7c25-176">Instalace přes úložiště balíčků – Debian 9</span><span class="sxs-lookup"><span data-stu-id="c7c25-176">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="c7c25-177">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-177">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="c7c25-178">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c7c25-178">This is the preferred method.</span></span>

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

<span data-ttu-id="c7c25-179">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="c7c25-179">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="c7c25-180">Instalace přes přímé stažení – Debian 9</span><span class="sxs-lookup"><span data-stu-id="c7c25-180">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="c7c25-181">Stáhněte si balíček Debian `powershell_6.0.3-1.debian.9_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="c7c25-181">Download the Debian package `powershell_6.0.3-1.debian.9_amd64.deb`</span></span>
<span data-ttu-id="c7c25-182">z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="c7c25-182">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="c7c25-183">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-183">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.3-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="c7c25-184">Odinstalace – Debian 9</span><span class="sxs-lookup"><span data-stu-id="c7c25-184">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="c7c25-185">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-185">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-186">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="c7c25-186">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="c7c25-187">Instalace přes úložiště balíčků (upřednostňováno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-187">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="c7c25-188">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-188">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c7c25-189">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c25-189">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="c7c25-190">Instalace přes přímé stažení - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-190">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="c7c25-191">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.0.3-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="c7c25-191">Using [CentOS 7][], download the RPM package `powershell-6.0.3-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="c7c25-192">z [uvolní][] stránky do počítače CentOS.</span><span class="sxs-lookup"><span data-stu-id="c7c25-192">from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="c7c25-193">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-193">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.3-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c7c25-194">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c7c25-194">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.3/powershell-6.0.3-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="c7c25-195">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-195">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c7c25-197">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-197">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c7c25-198">Instalace přes úložiště balíčků (upřednostňováno) – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-198">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="c7c25-199">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-199">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="c7c25-200">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c25-200">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c7c25-201">Instalace přes přímé stažení – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-201">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="c7c25-202">Stáhněte si balíček RPM `powershell-6.0.3-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="c7c25-202">Download the RPM package `powershell-6.0.3-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="c7c25-203">z [uvolní][] stránky do počítače, Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="c7c25-203">from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="c7c25-204">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-204">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.3-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c7c25-205">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c7c25-205">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.3/powershell-6.0.3-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="c7c25-206">Odinstalace – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-206">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-423"></a><span data-ttu-id="c7c25-207">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c7c25-207">OpenSUSE 42.3</span></span>

<span data-ttu-id="c7c25-208">Když instalace Powershellu Core `zypper` může nahlaste mu následující chybu:</span><span class="sxs-lookup"><span data-stu-id="c7c25-208">When installing PowerShell Core, `zypper` may report the following error:</span></span>

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

<span data-ttu-id="c7c25-209">V takovém případě ověřte, že kompatibilní `libcurl` knihovna je k dispozici tak, že zkontrolujete, že následující příkaz ukazuje `libcurl4` zabalit jako nainstalovaní:</span><span class="sxs-lookup"><span data-stu-id="c7c25-209">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

<span data-ttu-id="c7c25-210">Klikněte na tlačítko `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci balíčků prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7c25-210">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-423"></a><span data-ttu-id="c7c25-211">Instalace přes úložiště balíčků (upřednostňováno) - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c7c25-211">Installation via Package Repository (preferred) - OpenSUSE 42.3</span></span>

<span data-ttu-id="c7c25-212">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-212">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-423"></a><span data-ttu-id="c7c25-213">Instalace přes přímé stažení - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c7c25-213">Installation via Direct Download - OpenSUSE 42.3</span></span>

<span data-ttu-id="c7c25-214">Stáhněte si balíček RPM `powershell-6.0.3-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="c7c25-214">Download the RPM package `powershell-6.0.3-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.3-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c7c25-215">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c7c25-215">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.3/powershell-6.0.3-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-423"></a><span data-ttu-id="c7c25-216">Odinstalace - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c7c25-216">Uninstallation - OpenSUSE 42.3</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="c7c25-217">Fedora</span><span class="sxs-lookup"><span data-stu-id="c7c25-217">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-218">Fedora 28 je podporována pouze v prostředí PowerShell Core 6.1 a novější.</span><span class="sxs-lookup"><span data-stu-id="c7c25-218">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="c7c25-219">Instalace přes úložiště balíčků (upřednostňováno) - Fedora 27 Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c7c25-219">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="c7c25-220">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-220">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="c7c25-221">Instalace přes přímé stažení - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c7c25-221">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="c7c25-222">Stáhněte si balíček RPM `powershell-6.0.3-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="c7c25-222">Download the RPM package `powershell-6.0.3-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="c7c25-223">z [uvolní][] stránky do počítače, Fedora.</span><span class="sxs-lookup"><span data-stu-id="c7c25-223">from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="c7c25-224">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-224">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.3-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="c7c25-225">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="c7c25-225">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="c7c25-226">Odinstalace - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c7c25-226">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="c7c25-227">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="c7c25-227">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-228">Podpora architektury je experimentální.</span><span class="sxs-lookup"><span data-stu-id="c7c25-228">Arch support is experimental.</span></span>

<span data-ttu-id="c7c25-229">PowerShell je k dispozici [Arch Linux][] úložišti uživatele (AUR).</span><span class="sxs-lookup"><span data-stu-id="c7c25-229">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="c7c25-230">Může být zkompilován s [označené nejnovější verzi][arch-release]</span><span class="sxs-lookup"><span data-stu-id="c7c25-230">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="c7c25-231">Mohou být zkompilovány z [nejnovější potvrzení změn do hlavní větve][arch-git]</span><span class="sxs-lookup"><span data-stu-id="c7c25-231">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="c7c25-232">Nainstalujete ho pomocí [nejnovější verze binárního souboru][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="c7c25-232">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="c7c25-233">Balíčky AUR jsou komunity udržuje – neexistuje žádná oficiální podpora.</span><span class="sxs-lookup"><span data-stu-id="c7c25-233">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="c7c25-234">Další informace o instalaci balíčků z AUR najdete v tématu [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunitou [soubor DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="c7c25-234">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="c7c25-236">Přichytit balíčku</span><span class="sxs-lookup"><span data-stu-id="c7c25-236">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="c7c25-237">Získávání snapd</span><span class="sxs-lookup"><span data-stu-id="c7c25-237">Getting snapd</span></span>

<span data-ttu-id="c7c25-238">`snapd` je požadován pro spuštění při kolika rozehrávkách byli.</span><span class="sxs-lookup"><span data-stu-id="c7c25-238">`snapd` is required to run snaps.</span></span>  <span data-ttu-id="c7c25-239">Použití [tyto pokyny](https://docs.snapcraft.io/core/install) abyste měli jistotu, že máte `snapd` nainstalované.</span><span class="sxs-lookup"><span data-stu-id="c7c25-239">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="c7c25-240">Instalace přes modul Snap</span><span class="sxs-lookup"><span data-stu-id="c7c25-240">Installation via Snap</span></span>

<span data-ttu-id="c7c25-241">PowerShell Core pro Linux, je publikovaná [Snap úložiště](https://snapcraft.io/store) Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="c7c25-241">PowerShell Core, for Linux, is published to the [Snap store](https://snapcraft.io/store) for easy installation (and updates).</span></span>
<span data-ttu-id="c7c25-242">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="c7c25-242">This is the preferred method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="c7c25-243">Po instalaci modulu Snap budou automaticky upgradovat, ale můžete aktivovat upgradu pomocí `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="c7c25-243">After installing Snap will automatically upgrade, but you can trigger an upgrade using `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="c7c25-244">Odinstalace</span><span class="sxs-lookup"><span data-stu-id="c7c25-244">Uninstallation</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="linux-appimage"></a><span data-ttu-id="c7c25-245">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="c7c25-245">Linux AppImage</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-246">Podpora AppImage je experimentální</span><span class="sxs-lookup"><span data-stu-id="c7c25-246">AppImage support is experimental</span></span>

<span data-ttu-id="c7c25-247">Pomocí nejnovější distribuce Linuxu, stáhněte si AppImage `powershell-6.0.1-x86_64.AppImage` z [uvolní][] stránky na počítači s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="c7c25-247">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="c7c25-248">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="c7c25-248">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="c7c25-249">[AppImage][] umožňuje spustit prostředí PowerShell bez nutnosti jeho instalace.</span><span class="sxs-lookup"><span data-stu-id="c7c25-249">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="c7c25-250">Je přenosné aplikace, která obsahuje ureitou prostředí PowerShell a jeho závislosti (včetně .NET Core závislosti systému) do jednoho získá na ucelenosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="c7c25-250">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="c7c25-251">Tento balíček je jeden binární soubor, který funguje nezávisle na Linuxové distribuci daného uživatele.</span><span class="sxs-lookup"><span data-stu-id="c7c25-251">This package is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="c7c25-253">Kali</span><span class="sxs-lookup"><span data-stu-id="c7c25-253">Kali</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-254">Podpora Kali je experimentální.</span><span class="sxs-lookup"><span data-stu-id="c7c25-254">Kali support is experimental.</span></span>

### <a name="installation"></a><span data-ttu-id="c7c25-255">Instalace</span><span class="sxs-lookup"><span data-stu-id="c7c25-255">Installation</span></span>

```sh
# Download & Install prerequisites
sudo apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Install PowerShell
sudo dpkg -i powershell_6.0.3-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="c7c25-256">Spusťte prostředí PowerShell v nejnovější Kali (Kali GNU/Linux se zajištěním provozu) bez nutnosti jeho instalace</span><span class="sxs-lookup"><span data-stu-id="c7c25-256">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="c7c25-257">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="c7c25-257">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="c7c25-258">Raspbian</span><span class="sxs-lookup"><span data-stu-id="c7c25-258">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="c7c25-259">Podpora Raspbian je experimentální.</span><span class="sxs-lookup"><span data-stu-id="c7c25-259">Raspbian support is experimental.</span></span>

<span data-ttu-id="c7c25-260">Prostředí PowerShell je v současné době podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="c7c25-260">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="c7c25-261">Také CoreCLR (a tedy PowerShell Core) bude fungovat jenom na zařízeních Pi 2 a Pi 3 jako jiná zařízení, jako je třeba [Pi nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesor.</span><span class="sxs-lookup"><span data-stu-id="c7c25-261">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="c7c25-262">Stáhněte si [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) zobrazíte na vaše číslo pí.</span><span class="sxs-lookup"><span data-stu-id="c7c25-262">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="c7c25-263">Instalace</span><span class="sxs-lookup"><span data-stu-id="c7c25-263">Installation</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.3/powershell-6.0.3-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.3-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

<span data-ttu-id="c7c25-264">Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty ke "pwsh" binární</span><span class="sxs-lookup"><span data-stu-id="c7c25-264">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="c7c25-265">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="c7c25-265">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="c7c25-266">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="c7c25-266">Binary Archives</span></span>

<span data-ttu-id="c7c25-267">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformy Linux umožňuje pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="c7c25-267">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="c7c25-268">Závislosti</span><span class="sxs-lookup"><span data-stu-id="c7c25-268">Dependencies</span></span>

<span data-ttu-id="c7c25-269">Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce Linuxu.</span><span class="sxs-lookup"><span data-stu-id="c7c25-269">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="c7c25-270">Ale modulu runtime .NET Core vyžaduje různých závislostí v různých distribucích a proto Powershellu dělá to samé.</span><span class="sxs-lookup"><span data-stu-id="c7c25-270">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="c7c25-271">Následující graf ukazuje závislosti rozhraní .NET Core 2.0, oficiálně podporované v různých distribucích systému Linux.</span><span class="sxs-lookup"><span data-stu-id="c7c25-271">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="c7c25-272">Operační systém</span><span class="sxs-lookup"><span data-stu-id="c7c25-272">OS</span></span>                 | <span data-ttu-id="c7c25-273">Závislosti</span><span class="sxs-lookup"><span data-stu-id="c7c25-273">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="c7c25-274">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-274">Ubuntu 14.04</span></span>       | <span data-ttu-id="c7c25-275">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c7c25-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c7c25-276">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="c7c25-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="c7c25-277">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-277">Ubuntu 16.04</span></span>       | <span data-ttu-id="c7c25-278">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c7c25-278">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c7c25-279">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="c7c25-279">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="c7c25-280">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="c7c25-280">Ubuntu 17.10</span></span>       | <span data-ttu-id="c7c25-281">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c7c25-281">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c7c25-282">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="c7c25-282">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="c7c25-283">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="c7c25-283">Ubuntu 18.04</span></span>       | <span data-ttu-id="c7c25-284">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c7c25-284">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c7c25-285">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="c7c25-285">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="c7c25-286">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="c7c25-286">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="c7c25-287">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c7c25-287">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c7c25-288">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="c7c25-288">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="c7c25-289">Debian 9 (roztáhnout)</span><span class="sxs-lookup"><span data-stu-id="c7c25-289">Debian 9 (Stretch)</span></span> | <span data-ttu-id="c7c25-290">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="c7c25-290">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="c7c25-291">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="c7c25-291">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="c7c25-292">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-292">CentOS 7</span></span> <br> <span data-ttu-id="c7c25-293">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-293">Oracle Linux 7</span></span> <br> <span data-ttu-id="c7c25-294">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="c7c25-294">RHEL 7</span></span> <br> <span data-ttu-id="c7c25-295">OpenSUSE OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="c7c25-295">OpenSUSE OpenSUSE 42.3</span></span> | <span data-ttu-id="c7c25-296">libunwind libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="c7c25-296">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="c7c25-297">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="c7c25-297">Fedora 27</span></span> <br> <span data-ttu-id="c7c25-298">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="c7c25-298">Fedora 28</span></span> | <span data-ttu-id="c7c25-299">libunwind libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="c7c25-299">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="c7c25-300">K nasazení binárních souborů prostředí PowerShell v Linuxových distribucích, které nejsou oficiálně podporované, budete muset nainstalovat potřebné závislosti pro cílový operační systém v samostatných krocích.</span><span class="sxs-lookup"><span data-stu-id="c7c25-300">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="c7c25-301">Například náš [soubor dockerfile Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a poté rozbalí Linuxový `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="c7c25-301">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="c7c25-302">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="c7c25-302">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="c7c25-303">Linux</span><span class="sxs-lookup"><span data-stu-id="c7c25-303">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="c7c25-304">Probíhá odinstalace binárního archivy</span><span class="sxs-lookup"><span data-stu-id="c7c25-304">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="c7c25-305">Cesty</span><span class="sxs-lookup"><span data-stu-id="c7c25-305">Paths</span></span>

* <span data-ttu-id="c7c25-306">`$PSHOME` je `/opt/microsoft/powershell/6.0.3/`</span><span class="sxs-lookup"><span data-stu-id="c7c25-306">`$PSHOME` is `/opt/microsoft/powershell/6.0.3/`</span></span>
* <span data-ttu-id="c7c25-307">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="c7c25-307">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="c7c25-308">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="c7c25-308">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="c7c25-309">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="c7c25-309">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="c7c25-310">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="c7c25-310">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="c7c25-311">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="c7c25-311">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="c7c25-312">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="c7c25-312">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="c7c25-313">Profily respektovat konfigurace Powershellu na hostitele, takže výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="c7c25-313">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="c7c25-314">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v Linuxu.</span><span class="sxs-lookup"><span data-stu-id="c7c25-314">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

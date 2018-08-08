---
title: Instalace PowerShellu Core v Linuxu
description: Informace o instalaci Powershellu Core v různých distribucích systému Linux
ms.date: 08/06/2018
ms.openlocfilehash: a6b0e3003f84ea6dc99cffcc7edf1b5b6963aa21
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587444"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="517bf-103">Instalace PowerShellu Core v Linuxu</span><span class="sxs-lookup"><span data-stu-id="517bf-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="517bf-104">Podporuje [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.10] [ u18], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27 ] [ fedora], [Fedora 28][fedora], a [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="517bf-104">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.10][u18], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="517bf-105">Pro distribuce Linuxu, které nejsou oficiálně podporované, můžete zkusit použít [balíčků v Powershellu Přichytit][snap].</span><span class="sxs-lookup"><span data-stu-id="517bf-105">For Linux distributions that are not officially supported, you can try using the [PowerShell Snap Package][snap].</span></span>
<span data-ttu-id="517bf-106">Nasazení prostředí PowerShell binární soubory přímo s Linuxem můžete také zkusit [ `tar.gz` archivu][tar], ale je potřeba nastavit potřebné závislosti podle operačního systému v samostatné kroky.</span><span class="sxs-lookup"><span data-stu-id="517bf-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="517bf-107">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="517bf-107">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="517bf-108">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="517bf-108">Once the package is installed, run `pwsh` from a terminal.</span></span>

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

## <a name="installing-preview-releases"></a><span data-ttu-id="517bf-109">Instalace Preview verzí</span><span class="sxs-lookup"><span data-stu-id="517bf-109">Installing Preview Releases</span></span>

<span data-ttu-id="517bf-110">Při instalaci verze Preview prostředí PowerShell Core pro Linux přes úložiště balíčků, názvu balíčku se změní z `powershell` k `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="517bf-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="517bf-111">Instalace přes přímé stažení nezmění, než je název souboru.</span><span class="sxs-lookup"><span data-stu-id="517bf-111">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="517bf-112">Tady je tabulka znázorňující příkazy, abyste nainstalovali stabilní verze a preview balíčků pomocí různých správců balíčků:</span><span class="sxs-lookup"><span data-stu-id="517bf-112">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="517bf-113">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="517bf-113">Distribution(s)</span></span>|<span data-ttu-id="517bf-114">Stabilní příkaz</span><span class="sxs-lookup"><span data-stu-id="517bf-114">Stable Command</span></span> | <span data-ttu-id="517bf-115">Příkaz ve verzi Preview</span><span class="sxs-lookup"><span data-stu-id="517bf-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="517bf-116">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="517bf-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="517bf-117">CentOS, Red Hat</span><span class="sxs-lookup"><span data-stu-id="517bf-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="517bf-118">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="517bf-118">OpenSUSE</span></span> |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| <span data-ttu-id="517bf-119">Fedora</span><span class="sxs-lookup"><span data-stu-id="517bf-119">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="517bf-120">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="517bf-120">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="517bf-121">Instalace přes úložiště balíčků – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="517bf-121">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="517bf-122">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-122">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="517bf-123">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="517bf-123">This is the preferred method.</span></span>

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

<span data-ttu-id="517bf-124">Jako superuživatele zaregistrujte úložiště společnosti Microsoft.</span><span class="sxs-lookup"><span data-stu-id="517bf-124">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="517bf-125">Od té chvíle stačí použít `sudo apt-get upgrade powershell` k aktualizaci instalace.</span><span class="sxs-lookup"><span data-stu-id="517bf-125">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="517bf-126">Instalace přes přímé stažení – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="517bf-126">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="517bf-127">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="517bf-127">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="517bf-128">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-128">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="517bf-129">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="517bf-129">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="517bf-130">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="517bf-130">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="517bf-131">Odinstalace – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="517bf-131">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="517bf-132">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="517bf-132">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="517bf-133">Instalace přes úložiště balíčků – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="517bf-133">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="517bf-134">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-134">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="517bf-135">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="517bf-135">This is the preferred method.</span></span>

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

<span data-ttu-id="517bf-136">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="517bf-136">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="517bf-137">Instalace přes přímé stažení – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="517bf-137">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="517bf-138">Stáhněte si balíček Debian `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="517bf-138">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="517bf-139">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-139">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="517bf-140">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="517bf-140">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="517bf-141">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="517bf-141">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="517bf-142">Odinstalace – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="517bf-142">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="517bf-143">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="517bf-143">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-144">Přidali jsme podporu pro Ubuntu 18.04 po `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="517bf-144">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="517bf-145">Instalace přes úložiště balíčků – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="517bf-145">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="517bf-146">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-146">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="517bf-147">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="517bf-147">This is the preferred method.</span></span>

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

<span data-ttu-id="517bf-148">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="517bf-148">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="517bf-149">Instalace přes přímé stažení – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="517bf-149">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="517bf-150">Stáhněte si balíček Debian `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` z [uvolní][] stránky do počítače se systémem Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="517bf-150">Download the Debian package `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="517bf-151">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-151">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="517bf-152">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="517bf-152">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="517bf-153">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="517bf-153">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="517bf-154">Odinstalace – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="517bf-154">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="517bf-155">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="517bf-155">Ubuntu 18.10</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-156">Přidali jsme podporu pro Ubuntu 18.10 po `6.1.0-preview.3`.</span><span class="sxs-lookup"><span data-stu-id="517bf-156">Support for Ubuntu 18.10 was added after `6.1.0-preview.3`.</span></span>
> <span data-ttu-id="517bf-157">Je 18.10 každodenními buildy, je podporovaná pouze komunitou.</span><span class="sxs-lookup"><span data-stu-id="517bf-157">As 18.10 is a daily build, it is only community supported.</span></span>

<span data-ttu-id="517bf-158">Instalace na 18.10 je podporované prostřednictvím `snapd`.</span><span class="sxs-lookup"><span data-stu-id="517bf-158">Installing on 18.10 is supported via `snapd`.</span></span> <span data-ttu-id="517bf-159">Zobrazit [Přichytit balíček] [ snap] úplné pokyny;</span><span class="sxs-lookup"><span data-stu-id="517bf-159">See [Snap Package][snap] for full instructions;</span></span>

## <a name="debian-8"></a><span data-ttu-id="517bf-160">Debian 8</span><span class="sxs-lookup"><span data-stu-id="517bf-160">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="517bf-161">Instalace přes úložiště balíčků – Debian 8</span><span class="sxs-lookup"><span data-stu-id="517bf-161">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="517bf-162">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-162">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="517bf-163">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="517bf-163">This is the preferred method.</span></span>

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

<span data-ttu-id="517bf-164">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="517bf-164">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="517bf-165">Instalace přes přímé stažení – Debian 8</span><span class="sxs-lookup"><span data-stu-id="517bf-165">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="517bf-166">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.8_amd64.deb` z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="517bf-166">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="517bf-167">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-167">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="517bf-168">`dpkg -i` Příkaz selže s dosud nevyřešených závislosti.</span><span class="sxs-lookup"><span data-stu-id="517bf-168">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="517bf-169">Další příkaz `apt-get install -f` řeší tyto problémy po dokončení konfigurace balíčku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="517bf-169">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="517bf-170">Odinstalace – Debian 8</span><span class="sxs-lookup"><span data-stu-id="517bf-170">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="517bf-171">Debian 9</span><span class="sxs-lookup"><span data-stu-id="517bf-171">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="517bf-172">Instalace přes úložiště balíčků – Debian 9</span><span class="sxs-lookup"><span data-stu-id="517bf-172">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="517bf-173">PowerShell Core pro Linux, se publikují do úložišť balíčků pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-173">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="517bf-174">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="517bf-174">This is the preferred method.</span></span>

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

<span data-ttu-id="517bf-175">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, od té chvíle stačí použít `sudo apt-get upgrade powershell` ji aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="517bf-175">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="517bf-176">Instalace přes přímé stažení – Debian 9</span><span class="sxs-lookup"><span data-stu-id="517bf-176">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="517bf-177">Stáhněte si balíček Debian `powershell_6.0.2-1.debian.9_amd64.deb` z [uvolní][] stránky do počítače, Debian.</span><span class="sxs-lookup"><span data-stu-id="517bf-177">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="517bf-178">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-178">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="517bf-179">Odinstalace – Debian 9</span><span class="sxs-lookup"><span data-stu-id="517bf-179">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="517bf-180">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="517bf-180">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-181">Tento balíček funguje taky na Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="517bf-181">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="517bf-182">Instalace přes úložiště balíčků (upřednostňováno) - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="517bf-182">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="517bf-183">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-183">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="517bf-184">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="517bf-184">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="517bf-185">Instalace přes přímé stažení - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="517bf-185">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="517bf-186">Pomocí [CentOS 7][], stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače CentOS.</span><span class="sxs-lookup"><span data-stu-id="517bf-186">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="517bf-187">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-187">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="517bf-188">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="517bf-188">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="517bf-189">Odinstalace - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="517bf-189">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="517bf-191">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="517bf-191">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="517bf-192">Instalace přes úložiště balíčků (upřednostňováno) – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="517bf-192">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="517bf-193">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-193">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="517bf-194">Po registraci úložiště společnosti Microsoft jednou jako superuživatele, stačí použít `sudo yum update powershell` aktualizovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="517bf-194">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="517bf-195">Instalace přes přímé stažení – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="517bf-195">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="517bf-196">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače, Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="517bf-196">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="517bf-197">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-197">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="517bf-198">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="517bf-198">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="517bf-199">Odinstalace – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="517bf-199">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-423"></a><span data-ttu-id="517bf-200">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="517bf-200">OpenSUSE 42.3</span></span>

<span data-ttu-id="517bf-201">Když instalace Powershellu Core `zypper` může nahlaste mu následující chybu:</span><span class="sxs-lookup"><span data-stu-id="517bf-201">When installing PowerShell Core, `zypper` may report the following error:</span></span>

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

<span data-ttu-id="517bf-202">V takovém případě ověřte, že kompatibilní `libcurl` knihovna je k dispozici tak, že zkontrolujete, že následující příkaz ukazuje `libcurl4` zabalit jako nainstalovaní:</span><span class="sxs-lookup"><span data-stu-id="517bf-202">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

<span data-ttu-id="517bf-203">Klikněte na tlačítko `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` řešení při instalaci balíčků prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="517bf-203">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-423"></a><span data-ttu-id="517bf-204">Instalace přes úložiště balíčků (upřednostňováno) - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="517bf-204">Installation via Package Repository (preferred) - OpenSUSE 42.3</span></span>

<span data-ttu-id="517bf-205">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-205">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-423"></a><span data-ttu-id="517bf-206">Instalace přes přímé stažení - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="517bf-206">Installation via Direct Download - OpenSUSE 42.3</span></span>

<span data-ttu-id="517bf-207">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="517bf-207">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="517bf-208">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="517bf-208">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-423"></a><span data-ttu-id="517bf-209">Odinstalace - OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="517bf-209">Uninstallation - OpenSUSE 42.3</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="517bf-210">Fedora</span><span class="sxs-lookup"><span data-stu-id="517bf-210">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-211">Fedora 28 je podporována pouze v prostředí PowerShell Core 6.1 a novější.</span><span class="sxs-lookup"><span data-stu-id="517bf-211">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="517bf-212">Instalace přes úložiště balíčků (upřednostňováno) - Fedora 27 Fedora 28</span><span class="sxs-lookup"><span data-stu-id="517bf-212">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="517bf-213">PowerShell Core pro Linux je publikovaný na oficiální úložišť Microsoft pro snadnou instalaci (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-213">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="517bf-214">Instalace přes přímé stažení - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="517bf-214">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="517bf-215">Stáhněte si balíček RPM `powershell-6.0.2-1.rhel.7.x86_64.rpm` z [uvolní][] stránky do počítače, Fedora.</span><span class="sxs-lookup"><span data-stu-id="517bf-215">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="517bf-216">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-216">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="517bf-217">Můžete také nainstalovat RPM bez přechodný krok stahování ho:</span><span class="sxs-lookup"><span data-stu-id="517bf-217">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="517bf-218">Odinstalace - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="517bf-218">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="517bf-219">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="517bf-219">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-220">Podpora architektury je experimentální.</span><span class="sxs-lookup"><span data-stu-id="517bf-220">Arch support is experimental.</span></span>

<span data-ttu-id="517bf-221">PowerShell je k dispozici [Arch Linux][] úložišti uživatele (AUR).</span><span class="sxs-lookup"><span data-stu-id="517bf-221">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="517bf-222">Může být zkompilován s [označené nejnovější verzi][arch-release]</span><span class="sxs-lookup"><span data-stu-id="517bf-222">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="517bf-223">Mohou být zkompilovány z [nejnovější potvrzení změn do hlavní větve][arch-git]</span><span class="sxs-lookup"><span data-stu-id="517bf-223">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="517bf-224">Nainstalujete ho pomocí [nejnovější verze binárního souboru][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="517bf-224">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="517bf-225">Balíčky AUR jsou komunity udržuje – neexistuje žádná oficiální podpora.</span><span class="sxs-lookup"><span data-stu-id="517bf-225">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="517bf-226">Další informace o instalaci balíčků z AUR najdete v tématu [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) nebo komunitou [soubor DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="517bf-226">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="517bf-228">Přichytit balíčku</span><span class="sxs-lookup"><span data-stu-id="517bf-228">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="517bf-229">Získávání snapd</span><span class="sxs-lookup"><span data-stu-id="517bf-229">Getting snapd</span></span>

<span data-ttu-id="517bf-230">`snapd` je požadován pro spuštění při kolika rozehrávkách byli.</span><span class="sxs-lookup"><span data-stu-id="517bf-230">`snapd` is required to run snaps.</span></span>  <span data-ttu-id="517bf-231">Použití [tyto pokyny](https://docs.snapcraft.io/core/install) abyste měli jistotu, že máte `snapd` nainstalované.</span><span class="sxs-lookup"><span data-stu-id="517bf-231">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="517bf-232">Instalace přes modul Snap</span><span class="sxs-lookup"><span data-stu-id="517bf-232">Installation via Snap</span></span>

<span data-ttu-id="517bf-233">PowerShell Core pro Linux, je publikovaná [Snap úložiště](https://snapcraft.io/store) Snadná instalace (a aktualizace).</span><span class="sxs-lookup"><span data-stu-id="517bf-233">PowerShell Core, for Linux, is published to the [Snap store](https://snapcraft.io/store) for easy installation (and updates).</span></span>
<span data-ttu-id="517bf-234">Toto je upřednostňovaná metoda.</span><span class="sxs-lookup"><span data-stu-id="517bf-234">This is the preferred method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="517bf-235">Po instalaci modulu Snap budou automaticky upgradovat, ale můžete aktivovat upgradu pomocí `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="517bf-235">After installing Snap will automatically upgrade, but you can trigger an upgrade using `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="517bf-236">Odinstalace</span><span class="sxs-lookup"><span data-stu-id="517bf-236">Uninstallation</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="linux-appimage"></a><span data-ttu-id="517bf-237">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="517bf-237">Linux AppImage</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-238">Podpora AppImage je experimentální</span><span class="sxs-lookup"><span data-stu-id="517bf-238">AppImage support is experimental</span></span>

<span data-ttu-id="517bf-239">Pomocí nejnovější distribuce Linuxu, stáhněte si AppImage `powershell-6.0.1-x86_64.AppImage` z [uvolní][] stránky na počítači s Linuxem.</span><span class="sxs-lookup"><span data-stu-id="517bf-239">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="517bf-240">Potom v terminálu spusťte následující:</span><span class="sxs-lookup"><span data-stu-id="517bf-240">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="517bf-241">[AppImage][] umožňuje spustit prostředí PowerShell bez nutnosti jeho instalace.</span><span class="sxs-lookup"><span data-stu-id="517bf-241">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="517bf-242">Je přenosné aplikace, která obsahuje ureitou prostředí PowerShell a jeho závislosti (včetně .NET Core závislosti systému) do jednoho získá na ucelenosti balíčku.</span><span class="sxs-lookup"><span data-stu-id="517bf-242">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="517bf-243">Tento balíček je jeden binární soubor, který funguje nezávisle na Linuxové distribuci daného uživatele.</span><span class="sxs-lookup"><span data-stu-id="517bf-243">This package is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="517bf-245">Kali</span><span class="sxs-lookup"><span data-stu-id="517bf-245">Kali</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-246">Podpora Kali je experimentální.</span><span class="sxs-lookup"><span data-stu-id="517bf-246">Kali support is experimental.</span></span>

### <a name="installation"></a><span data-ttu-id="517bf-247">Instalace</span><span class="sxs-lookup"><span data-stu-id="517bf-247">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="517bf-248">Spusťte prostředí PowerShell v nejnovější Kali (Kali GNU/Linux se zajištěním provozu) bez nutnosti jeho instalace</span><span class="sxs-lookup"><span data-stu-id="517bf-248">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="517bf-249">Odinstalace - Kali</span><span class="sxs-lookup"><span data-stu-id="517bf-249">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="517bf-250">Raspbian</span><span class="sxs-lookup"><span data-stu-id="517bf-250">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="517bf-251">Podpora Raspbian je experimentální.</span><span class="sxs-lookup"><span data-stu-id="517bf-251">Raspbian support is experimental.</span></span>

<span data-ttu-id="517bf-252">Prostředí PowerShell je v současné době podporována pouze na Raspbian Stretch.</span><span class="sxs-lookup"><span data-stu-id="517bf-252">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="517bf-253">Také CoreCLR (a tedy PowerShell Core) bude fungovat jenom na zařízeních Pi 2 a Pi 3 jako jiná zařízení, jako je třeba [Pi nula](https://github.com/dotnet/coreclr/issues/10605), mají nepodporovaný procesor.</span><span class="sxs-lookup"><span data-stu-id="517bf-253">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="517bf-254">Stáhněte si [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) a postupujte podle pokynů [pokyny k instalaci](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) zobrazíte na vaše číslo pí.</span><span class="sxs-lookup"><span data-stu-id="517bf-254">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="517bf-255">Instalace</span><span class="sxs-lookup"><span data-stu-id="517bf-255">Installation</span></span>

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

<span data-ttu-id="517bf-256">Volitelně můžete vytvořit symbolický odkaz, abyste mohli spustit prostředí PowerShell bez zadání cesty ke "pwsh" binární</span><span class="sxs-lookup"><span data-stu-id="517bf-256">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="517bf-257">Odinstalace - Raspbian</span><span class="sxs-lookup"><span data-stu-id="517bf-257">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="517bf-258">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="517bf-258">Binary Archives</span></span>

<span data-ttu-id="517bf-259">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformy Linux umožňuje pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="517bf-259">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="517bf-260">Závislosti</span><span class="sxs-lookup"><span data-stu-id="517bf-260">Dependencies</span></span>

<span data-ttu-id="517bf-261">Prostředí PowerShell vytvoří přenosné binární soubory pro všechny distribuce Linuxu.</span><span class="sxs-lookup"><span data-stu-id="517bf-261">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="517bf-262">Ale modulu runtime .NET Core vyžaduje různých závislostí v různých distribucích a proto Powershellu dělá to samé.</span><span class="sxs-lookup"><span data-stu-id="517bf-262">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="517bf-263">Následující graf ukazuje závislosti rozhraní .NET Core 2.0, oficiálně podporované v různých distribucích systému Linux.</span><span class="sxs-lookup"><span data-stu-id="517bf-263">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="517bf-264">Operační systém</span><span class="sxs-lookup"><span data-stu-id="517bf-264">OS</span></span>                 | <span data-ttu-id="517bf-265">Závislosti</span><span class="sxs-lookup"><span data-stu-id="517bf-265">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="517bf-266">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="517bf-266">Ubuntu 14.04</span></span>       | <span data-ttu-id="517bf-267">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="517bf-267">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="517bf-268">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="517bf-268">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="517bf-269">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="517bf-269">Ubuntu 16.04</span></span>       | <span data-ttu-id="517bf-270">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="517bf-270">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="517bf-271">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="517bf-271">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="517bf-272">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="517bf-272">Ubuntu 17.10</span></span>       | <span data-ttu-id="517bf-273">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="517bf-273">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="517bf-274">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="517bf-274">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="517bf-275">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="517bf-275">Ubuntu 18.04</span></span>       | <span data-ttu-id="517bf-276">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="517bf-276">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="517bf-277">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="517bf-277">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="517bf-278">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="517bf-278">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="517bf-279">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="517bf-279">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="517bf-280">libcurl3 libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="517bf-280">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="517bf-281">Debian 9 (roztáhnout)</span><span class="sxs-lookup"><span data-stu-id="517bf-281">Debian 9 (Stretch)</span></span> | <span data-ttu-id="517bf-282">libc6 ust0-libgcc1, libgssapi-krb5-2, liblttng, libstdc ++ 6</span><span class="sxs-lookup"><span data-stu-id="517bf-282">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="517bf-283">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="517bf-283">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="517bf-284">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="517bf-284">CentOS 7</span></span> <br> <span data-ttu-id="517bf-285">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="517bf-285">Oracle Linux 7</span></span> <br> <span data-ttu-id="517bf-286">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="517bf-286">RHEL 7</span></span> <br> <span data-ttu-id="517bf-287">OpenSUSE OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="517bf-287">OpenSUSE OpenSUSE 42.3</span></span> | <span data-ttu-id="517bf-288">libunwind libcurl, knihovny openssl, libicu</span><span class="sxs-lookup"><span data-stu-id="517bf-288">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="517bf-289">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="517bf-289">Fedora 27</span></span> <br> <span data-ttu-id="517bf-290">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="517bf-290">Fedora 28</span></span> | <span data-ttu-id="517bf-291">libunwind libcurl, knihovny openssl, libicu, compat openssl10</span><span class="sxs-lookup"><span data-stu-id="517bf-291">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="517bf-292">K nasazení binárních souborů prostředí PowerShell v Linuxových distribucích, které nejsou oficiálně podporované, budete muset nainstalovat potřebné závislosti pro cílový operační systém v samostatných krocích.</span><span class="sxs-lookup"><span data-stu-id="517bf-292">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="517bf-293">Například náš [soubor dockerfile Amazon Linux] [ amazon-dockerfile] nejdřív nainstaluje závislosti a poté rozbalí Linuxový `tar.gz` archivu.</span><span class="sxs-lookup"><span data-stu-id="517bf-293">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="517bf-294">Instalace - binární archivy</span><span class="sxs-lookup"><span data-stu-id="517bf-294">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="517bf-295">Linux</span><span class="sxs-lookup"><span data-stu-id="517bf-295">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="517bf-296">Probíhá odinstalace binárního archivy</span><span class="sxs-lookup"><span data-stu-id="517bf-296">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="517bf-297">Cesty</span><span class="sxs-lookup"><span data-stu-id="517bf-297">Paths</span></span>

* <span data-ttu-id="517bf-298">`$PSHOME` je `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="517bf-298">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="517bf-299">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="517bf-299">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="517bf-300">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="517bf-300">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="517bf-301">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="517bf-301">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="517bf-302">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="517bf-302">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="517bf-303">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="517bf-303">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="517bf-304">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="517bf-304">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="517bf-305">Profily respektovat konfigurace Powershellu na hostitele, takže výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="517bf-305">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="517bf-306">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v Linuxu.</span><span class="sxs-lookup"><span data-stu-id="517bf-306">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

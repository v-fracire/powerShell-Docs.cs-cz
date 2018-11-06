---
title: Instalace PowerShellu Core v macOS
description: Informace o instalaci Powershellu Core v macOS
ms.date: 11/02/2018
ms.openlocfilehash: 162e841bf71d708e9db84ea1bb2dbef13924783b
ms.sourcegitcommit: f4247d3f91d06ec392c4cd66921ce7d0456a2bd9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2018
ms.locfileid: "50998499"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="dd376-103">Instalace PowerShellu Core v macOS</span><span class="sxs-lookup"><span data-stu-id="dd376-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="dd376-104">PowerShell Core podporuje macOS 10.12 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="dd376-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="dd376-105">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="dd376-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="dd376-106">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="dd376-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="about-brew"></a><span data-ttu-id="dd376-107">O Brew</span><span class="sxs-lookup"><span data-stu-id="dd376-107">About Brew</span></span>

<span data-ttu-id="dd376-108">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="dd376-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="dd376-109">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="dd376-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="dd376-110">Instalace nejnovější stabilní verze pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="dd376-110">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="dd376-111">Zobrazit [o Brew](#about-brew) informace o Brew.</span><span class="sxs-lookup"><span data-stu-id="dd376-111">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="dd376-112">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd376-112">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="dd376-113">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="dd376-113">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="dd376-114">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd376-114">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="dd376-115">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="dd376-115">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="dd376-116">Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="dd376-116">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="dd376-117">Zobrazit [o Brew](#about-brew) informace o Brew.</span><span class="sxs-lookup"><span data-stu-id="dd376-117">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="dd376-118">Po instalaci Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="dd376-118">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="dd376-119">Nejdřív nainstalujte [Cask verze] [ cask-versions] který umožňuje nainstalovat alternativní verze cask balíčků:</span><span class="sxs-lookup"><span data-stu-id="dd376-119">First, install [Cask-Versions][cask-versions] which lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="dd376-120">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd376-120">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="dd376-121">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="dd376-121">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="dd376-122">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd376-122">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="dd376-123">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.</span><span class="sxs-lookup"><span data-stu-id="dd376-123">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="dd376-124">a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="dd376-124">and refresh the values shown in $PSVersionTable.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="dd376-125">Instalace přes přímé stažení</span><span class="sxs-lookup"><span data-stu-id="dd376-125">Installation via Direct Download</span></span>

<span data-ttu-id="dd376-126">Stáhněte si balíček PKG `powershell-6.1.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="dd376-126">Download the PKG package `powershell-6.1.0-osx-x64.pkg`</span></span>
<span data-ttu-id="dd376-127">z [uvolní][] stránky na svém počítači s macOS.</span><span class="sxs-lookup"><span data-stu-id="dd376-127">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="dd376-128">Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="dd376-128">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

<span data-ttu-id="dd376-129">Nainstalujte [OpenSSL](#install-openssl) jako to je potřeba pro vzdálenou komunikaci prostředí PowerShell a operace CIM.</span><span class="sxs-lookup"><span data-stu-id="dd376-129">Install [OpenSSL](#install-openssl) as this is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="binary-archives"></a><span data-ttu-id="dd376-130">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="dd376-130">Binary Archives</span></span>

<span data-ttu-id="dd376-131">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformu macOS umožňující pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="dd376-131">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="dd376-132">Instalace binárních archivy v systému macOS</span><span class="sxs-lookup"><span data-stu-id="dd376-132">Installing binary archives on macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.1.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.1.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.1.0/pwsh /usr/local/bin/pwsh
```

<span data-ttu-id="dd376-133">Nainstalujte [OpenSSL](#install-openssl) jako to je potřeba pro vzdálenou komunikaci prostředí PowerShell a operace CIM.</span><span class="sxs-lookup"><span data-stu-id="dd376-133">Install [OpenSSL](#install-openssl) as this is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="installing-dependencies"></a><span data-ttu-id="dd376-134">Instalování závislostí</span><span class="sxs-lookup"><span data-stu-id="dd376-134">Installing dependencies</span></span>

### <a name="install-xcode-command-line-tools"></a><span data-ttu-id="dd376-135">Instalace nástrojů příkazového řádku pro XCode</span><span class="sxs-lookup"><span data-stu-id="dd376-135">Install XCode command line tools</span></span>

```shell
xcode-select -install
```

### <a name="install-openssl"></a><span data-ttu-id="dd376-136">Nainstalujte OpenSSL</span><span class="sxs-lookup"><span data-stu-id="dd376-136">Install OpenSSL</span></span>

<span data-ttu-id="dd376-137">Pro operace CIM a vzdálené komunikace Powershellu je požadován OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="dd376-137">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>  <span data-ttu-id="dd376-138">Můžete nainstalovat prostřednictvím MacPorts nebo Brew.</span><span class="sxs-lookup"><span data-stu-id="dd376-138">You can install via MacPorts or Brew.</span></span>

#### <a name="install-openssl-via-brew"></a><span data-ttu-id="dd376-139">Nainstalujte OpenSSL prostřednictvím Brew</span><span class="sxs-lookup"><span data-stu-id="dd376-139">Install OpenSSL via Brew</span></span>

<span data-ttu-id="dd376-140">Zobrazit [o Brew](#about-brew) informace o Brew.</span><span class="sxs-lookup"><span data-stu-id="dd376-140">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="dd376-141">Spustit `brew install openssl` nainstalovat OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="dd376-141">Run `brew install openssl` to install OpenSSL.</span></span>

#### <a name="install-openssl-via-macports"></a><span data-ttu-id="dd376-142">Nainstalujte OpenSSL prostřednictvím MacPorts</span><span class="sxs-lookup"><span data-stu-id="dd376-142">Install OpenSSL via MacPorts</span></span>

1. <span data-ttu-id="dd376-143">Instalovat [příkazového řádku nástroje XCode](#install-xcode-command-line-tools)</span><span class="sxs-lookup"><span data-stu-id="dd376-143">Instal the [XCode command line tools](#install-xcode-command-line-tools)</span></span>
1. <span data-ttu-id="dd376-144">Nainstalujte MacPorts.</span><span class="sxs-lookup"><span data-stu-id="dd376-144">Install MacPorts.</span></span>
   <span data-ttu-id="dd376-145">Zobrazit [Průvodce instalací](https://guide.macports.org/chunked/installing.macports.html) Pokud potřebujete pokyny.</span><span class="sxs-lookup"><span data-stu-id="dd376-145">See the [installation guide](https://guide.macports.org/chunked/installing.macports.html) if you need instructions.</span></span>
1. <span data-ttu-id="dd376-146">Aktualizovat MacPorts spuštěním `sudo port selfupdate`</span><span class="sxs-lookup"><span data-stu-id="dd376-146">Update MacPorts by running `sudo port selfupdate`</span></span>
1. <span data-ttu-id="dd376-147">Balíčky s upgradem MacPorts spuštěním `sudo port upgrade outdated`</span><span class="sxs-lookup"><span data-stu-id="dd376-147">Upgrade MacPorts packages by running `sudo port upgrade outdated`</span></span>
1. <span data-ttu-id="dd376-148">Nainstalujte OpenSSL spuštěním spuštěním `sudo port instal openssl`</span><span class="sxs-lookup"><span data-stu-id="dd376-148">Install OpenSSL by running by running `sudo port instal openssl`</span></span>
1. <span data-ttu-id="dd376-149">Odkaz na knihovny tak, aby ho může použít PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd376-149">Link the libraries so that PowerShell can use it.</span></span>

```shell
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="dd376-150">Odinstalace Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="dd376-150">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="dd376-151">Pokud jste nainstalovali Powershellu pomocí Homebrew, je snadné odinstalace:</span><span class="sxs-lookup"><span data-stu-id="dd376-151">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="dd376-152">Pokud jste instalovali prostřednictvím přímé stažení prostředí PowerShell, musí ručně odebrat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dd376-152">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="dd376-153">Odebrání dalších cest prostředí PowerShell, najdete [cesty](#paths) části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="dd376-153">To remove the additional PowerShell paths, please see the [paths](#paths) section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="dd376-154">Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.</span><span class="sxs-lookup"><span data-stu-id="dd376-154">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="dd376-155">Cesty</span><span class="sxs-lookup"><span data-stu-id="dd376-155">Paths</span></span>

* <span data-ttu-id="dd376-156">`$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="dd376-156">`$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="dd376-157">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="dd376-157">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="dd376-158">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="dd376-158">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="dd376-159">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="dd376-159">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="dd376-160">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="dd376-160">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="dd376-161">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="dd376-161">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="dd376-162">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="dd376-162">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="dd376-163">Profily respektovat konfigurace Powershellu na hostitele.</span><span class="sxs-lookup"><span data-stu-id="dd376-163">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="dd376-164">Proto výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="dd376-164">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="dd376-165">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="dd376-165">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="dd376-166">Protože je odvozený od BSD, předpona macOS `/usr/local` se použije namísto `/opt`.</span><span class="sxs-lookup"><span data-stu-id="dd376-166">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="dd376-167">Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`, a symbolický odkaz je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="dd376-167">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`, and the symbolic link is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd376-168">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="dd376-168">Additional Resources</span></span>

* <span data-ttu-id="dd376-169">[Homebrew Web][brew]</span><span class="sxs-lookup"><span data-stu-id="dd376-169">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="dd376-170">[Úložiště Github Homebrew][GitHub]</span><span class="sxs-lookup"><span data-stu-id="dd376-170">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="dd376-171">[Homebrew Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="dd376-171">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

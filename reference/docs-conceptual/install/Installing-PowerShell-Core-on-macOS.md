---
title: Instalace PowerShellu Core v macOS
description: Informace o instalaci Powershellu Core v macOS
ms.date: 12/12/2018
ms.openlocfilehash: 91e64cace7d4ed988da56109dde9bf2a80528eb4
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403726"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="84c25-103">Instalace PowerShellu Core v macOS</span><span class="sxs-lookup"><span data-stu-id="84c25-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="84c25-104">PowerShell Core podporuje macOS 10.12 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="84c25-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="84c25-105">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="84c25-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="84c25-106">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="84c25-106">After the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="about-brew"></a><span data-ttu-id="84c25-107">O Brew</span><span class="sxs-lookup"><span data-stu-id="84c25-107">About Brew</span></span>

<span data-ttu-id="84c25-108">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="84c25-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="84c25-109">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="84c25-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="84c25-110">Instalace nejnovější stabilní verze pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="84c25-110">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="84c25-111">Zobrazit [o Brew](#about-brew) informace o Brew.</span><span class="sxs-lookup"><span data-stu-id="84c25-111">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="84c25-112">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84c25-112">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="84c25-113">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="84c25-113">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="84c25-114">Po vydání nové verze powershellu jsou aktualizace na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84c25-114">When new versions of PowerShell are released, update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="84c25-115">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="84c25-115">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in `$PSVersionTable`.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="84c25-116">Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="84c25-116">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="84c25-117">Zobrazit [o Brew](#about-brew) informace o Brew.</span><span class="sxs-lookup"><span data-stu-id="84c25-117">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="84c25-118">Po instalaci Homebrew, můžete nainstalovat prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84c25-118">After you've installed Homebrew, you can install PowerShell.</span></span>
<span data-ttu-id="84c25-119">Nejdřív nainstalujte [Cask verze] [ cask-versions] balíček, který umožňuje nainstalovat alternativní verze cask balíčků:</span><span class="sxs-lookup"><span data-stu-id="84c25-119">First, install the [Cask-Versions][cask-versions] package that lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="84c25-120">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84c25-120">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="84c25-121">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="84c25-121">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="84c25-122">Po vydání nové verze powershellu jsou aktualizace na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84c25-122">When new versions of PowerShell are released, update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="84c25-123">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.</span><span class="sxs-lookup"><span data-stu-id="84c25-123">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="84c25-124">a aktualizujte hodnoty zobrazené v `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="84c25-124">and refresh the values shown in `$PSVersionTable`.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="84c25-125">Instalace přes přímé stažení</span><span class="sxs-lookup"><span data-stu-id="84c25-125">Installation via Direct Download</span></span>

<span data-ttu-id="84c25-126">Stáhněte si balíček PKG `powershell-6.1.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="84c25-126">Download the PKG package `powershell-6.1.0-osx-x64.pkg`</span></span>
<span data-ttu-id="84c25-127">z [uvolní][] stránky na svém počítači s macOS.</span><span class="sxs-lookup"><span data-stu-id="84c25-127">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="84c25-128">Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="84c25-128">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

<span data-ttu-id="84c25-129">Nainstalujte [OpenSSL](#install-openssl).</span><span class="sxs-lookup"><span data-stu-id="84c25-129">Install [OpenSSL](#install-openssl).</span></span> <span data-ttu-id="84c25-130">Pro operace CIM a vzdálené komunikace Powershellu je požadován OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="84c25-130">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="binary-archives"></a><span data-ttu-id="84c25-131">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="84c25-131">Binary Archives</span></span>

<span data-ttu-id="84c25-132">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformu macOS umožňující pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="84c25-132">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="84c25-133">Instalace binárních archivy v systému macOS</span><span class="sxs-lookup"><span data-stu-id="84c25-133">Installing binary archives on macOS</span></span>

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

<span data-ttu-id="84c25-134">Nainstalujte [OpenSSL](#install-openssl).</span><span class="sxs-lookup"><span data-stu-id="84c25-134">Install [OpenSSL](#install-openssl).</span></span> <span data-ttu-id="84c25-135">Pro operace CIM a vzdálené komunikace Powershellu je požadován OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="84c25-135">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="installing-dependencies"></a><span data-ttu-id="84c25-136">Instalování závislostí</span><span class="sxs-lookup"><span data-stu-id="84c25-136">Installing dependencies</span></span>

### <a name="install-xcode-command-line-tools"></a><span data-ttu-id="84c25-137">Instalace nástrojů příkazového řádku pro XCode</span><span class="sxs-lookup"><span data-stu-id="84c25-137">Install XCode command-line tools</span></span>

```sh
xcode-select --install
```

### <a name="install-openssl"></a><span data-ttu-id="84c25-138">Nainstalujte OpenSSL</span><span class="sxs-lookup"><span data-stu-id="84c25-138">Install OpenSSL</span></span>

<span data-ttu-id="84c25-139">Pro operace CIM a vzdálené komunikace Powershellu je požadován OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="84c25-139">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span> <span data-ttu-id="84c25-140">Můžete nainstalovat prostřednictvím MacPorts nebo Brew.</span><span class="sxs-lookup"><span data-stu-id="84c25-140">You can install via MacPorts or Brew.</span></span>

#### <a name="install-openssl-via-brew"></a><span data-ttu-id="84c25-141">Nainstalujte OpenSSL prostřednictvím Brew</span><span class="sxs-lookup"><span data-stu-id="84c25-141">Install OpenSSL via Brew</span></span>

<span data-ttu-id="84c25-142">Zobrazit [o Brew](#about-brew) informace o Brew.</span><span class="sxs-lookup"><span data-stu-id="84c25-142">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="84c25-143">Chcete-li nainstalovat OpenSSL, spusťte `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="84c25-143">To install OpenSSL, run `brew install openssl`.</span></span>

#### <a name="install-openssl-via-macports"></a><span data-ttu-id="84c25-144">Nainstalujte OpenSSL prostřednictvím MacPorts</span><span class="sxs-lookup"><span data-stu-id="84c25-144">Install OpenSSL via MacPorts</span></span>

1. <span data-ttu-id="84c25-145">Nainstalujte [příkazového řádku nástroje XCode](#install-xcode-command-line-tools).</span><span class="sxs-lookup"><span data-stu-id="84c25-145">Install the [XCode command line tools](#install-xcode-command-line-tools).</span></span>
1. <span data-ttu-id="84c25-146">Nainstalujte MacPorts.</span><span class="sxs-lookup"><span data-stu-id="84c25-146">Install MacPorts.</span></span>
   <span data-ttu-id="84c25-147">Pokud potřebujete získat pokyny, přečtěte si [Průvodce instalací](https://guide.macports.org/chunked/installing.macports.html).</span><span class="sxs-lookup"><span data-stu-id="84c25-147">If you need instructions, refer to the [installation guide](https://guide.macports.org/chunked/installing.macports.html).</span></span>
1. <span data-ttu-id="84c25-148">Aktualizovat MacPorts spuštěním `sudo port selfupdate`.</span><span class="sxs-lookup"><span data-stu-id="84c25-148">Update MacPorts by running `sudo port selfupdate`.</span></span>
1. <span data-ttu-id="84c25-149">MacPorts balíčky s upgradem spuštěním `sudo port upgrade outdated`.</span><span class="sxs-lookup"><span data-stu-id="84c25-149">Upgrade MacPorts packages by running `sudo port upgrade outdated`.</span></span>
1. <span data-ttu-id="84c25-150">Nainstalujte OpenSSL spuštěním `sudo port install openssl`.</span><span class="sxs-lookup"><span data-stu-id="84c25-150">Install OpenSSL by running `sudo port install openssl`.</span></span>
1. <span data-ttu-id="84c25-151">Odkaz knihovny, aby byly k dispozici pro prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84c25-151">Link the libraries to make them available to PowerShell:</span></span>

```sh
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="84c25-152">Odinstalace Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="84c25-152">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="84c25-153">Pokud jste nainstalovali Powershellu pomocí Homebrew, použijte následující příkaz pro odinstalaci:</span><span class="sxs-lookup"><span data-stu-id="84c25-153">If you installed PowerShell with Homebrew, use the following command to uninstall:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="84c25-154">Pokud jste instalovali prostřednictvím přímé stažení prostředí PowerShell, musí ručně odebrat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="84c25-154">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="84c25-155">Odebrání dalších cest prostředí PowerShell, najdete [cesty](#paths) části v tomto dokumentu a odebrání cesty pomocí `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="84c25-155">To remove the additional PowerShell paths, refer to the [paths](#paths) section in this document and remove the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="84c25-156">Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.</span><span class="sxs-lookup"><span data-stu-id="84c25-156">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="84c25-157">Cesty</span><span class="sxs-lookup"><span data-stu-id="84c25-157">Paths</span></span>

* <span data-ttu-id="84c25-158">`$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="84c25-158">`$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="84c25-159">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="84c25-159">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="84c25-160">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="84c25-160">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="84c25-161">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="84c25-161">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="84c25-162">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="84c25-162">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="84c25-163">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="84c25-163">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="84c25-164">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="84c25-164">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="84c25-165">Profily respektovat konfigurace Powershellu na hostitele.</span><span class="sxs-lookup"><span data-stu-id="84c25-165">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="84c25-166">Proto výchozí profil hostitele konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="84c25-166">So the default host-specific profile exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="84c25-167">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="84c25-167">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="84c25-168">Protože je odvozený od BSD, předpona macOS `/usr/local` se použije namísto `/opt`.</span><span class="sxs-lookup"><span data-stu-id="84c25-168">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="84c25-169">Ano `$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`, a symbolický odkaz je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="84c25-169">So, `$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`, and the symbolic link is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="84c25-170">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="84c25-170">Additional Resources</span></span>

* <span data-ttu-id="84c25-171">[Homebrew Web][brew]</span><span class="sxs-lookup"><span data-stu-id="84c25-171">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="84c25-172">[Úložiště Github Homebrew][GitHub]</span><span class="sxs-lookup"><span data-stu-id="84c25-172">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="84c25-173">[Homebrew Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="84c25-173">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

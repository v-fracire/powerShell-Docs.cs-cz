---
title: Instalace PowerShellu Core v macOS
description: Informace o instalaci Powershellu Core v macOS
ms.date: 08/06/2018
ms.openlocfilehash: e226cd64f8788ae74dc72fdc0cd219923b7a2cd6
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002355"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="8203c-103">Instalace PowerShellu Core v macOS</span><span class="sxs-lookup"><span data-stu-id="8203c-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="8203c-104">PowerShell Core podporuje macOS 10.12 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="8203c-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="8203c-105">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="8203c-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="8203c-106">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="8203c-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="8203c-107">Instalace nejnovější stabilní verze pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="8203c-107">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="8203c-108">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="8203c-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="8203c-109">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="8203c-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="8203c-110">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8203c-110">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="8203c-111">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="8203c-111">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="8203c-112">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8203c-112">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="8203c-113">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="8203c-113">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="8203c-114">Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="8203c-114">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="8203c-115">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="8203c-115">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="8203c-116">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="8203c-116">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="8203c-117">Po instalaci Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="8203c-117">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="8203c-118">Nejdřív nainstalujte [Cask verze] [ cask-versions] který umožňuje nainstalovat alternativní verze cask balíčků:</span><span class="sxs-lookup"><span data-stu-id="8203c-118">First, install [Cask-Versions][cask-versions] which lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="8203c-119">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8203c-119">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="8203c-120">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="8203c-120">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="8203c-121">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8203c-121">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="8203c-122">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.</span><span class="sxs-lookup"><span data-stu-id="8203c-122">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="8203c-123">a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="8203c-123">and refresh the values shown in $PSVersionTable.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="8203c-124">Instalace přes přímé stažení</span><span class="sxs-lookup"><span data-stu-id="8203c-124">Installation via Direct Download</span></span>

<span data-ttu-id="8203c-125">Stáhněte si balíček PKG `powershell-6.1.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="8203c-125">Download the PKG package `powershell-6.1.0-osx-x64.pkg`</span></span>
<span data-ttu-id="8203c-126">z [uvolní][] stránky na svém počítači s macOS.</span><span class="sxs-lookup"><span data-stu-id="8203c-126">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="8203c-127">Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="8203c-127">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="8203c-128">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="8203c-128">Binary Archives</span></span>

<span data-ttu-id="8203c-129">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformu macOS umožňující pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="8203c-129">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="8203c-130">Instalace binárních archivy v systému macOS</span><span class="sxs-lookup"><span data-stu-id="8203c-130">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="8203c-131">Odinstalace Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="8203c-131">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="8203c-132">Pokud jste nainstalovali Powershellu pomocí Homebrew, je snadné odinstalace:</span><span class="sxs-lookup"><span data-stu-id="8203c-132">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="8203c-133">Pokud jste instalovali prostřednictvím přímé stažení prostředí PowerShell, musí ručně odebrat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8203c-133">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="8203c-134">Odebrání dalších cest prostředí PowerShell, najdete [cesty](#paths) části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="8203c-134">To remove the additional PowerShell paths, please see the [paths](#paths) section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="8203c-135">Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.</span><span class="sxs-lookup"><span data-stu-id="8203c-135">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="8203c-136">Cesty</span><span class="sxs-lookup"><span data-stu-id="8203c-136">Paths</span></span>

* <span data-ttu-id="8203c-137">`$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="8203c-137">`$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="8203c-138">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="8203c-138">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="8203c-139">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="8203c-139">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="8203c-140">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="8203c-140">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="8203c-141">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="8203c-141">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="8203c-142">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="8203c-142">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="8203c-143">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="8203c-143">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="8203c-144">Profily respektovat konfigurace Powershellu na hostitele.</span><span class="sxs-lookup"><span data-stu-id="8203c-144">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="8203c-145">Proto výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="8203c-145">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="8203c-146">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="8203c-146">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="8203c-147">Protože je odvozený od BSD, předpona macOS `/usr/local` se použije namísto `/opt`.</span><span class="sxs-lookup"><span data-stu-id="8203c-147">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="8203c-148">Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`, a symlink je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="8203c-148">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8203c-149">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="8203c-149">Additional Resources</span></span>

* <span data-ttu-id="8203c-150">[Homebrew Web][brew]</span><span class="sxs-lookup"><span data-stu-id="8203c-150">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="8203c-151">[Úložiště Github Homebrew][GitHub]</span><span class="sxs-lookup"><span data-stu-id="8203c-151">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="8203c-152">[Homebrew Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="8203c-152">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

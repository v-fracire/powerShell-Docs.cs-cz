---
title: Instalace PowerShellu Core v macOS
description: Informace o instalaci Powershellu Core v macOS
ms.date: 08/06/2018
ms.openlocfilehash: 50b8dbbf26f02580e4be45978c926d5337da6b63
ms.sourcegitcommit: b235c58b34d23317076540631f5cf83f1f309c0d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45557156"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="9b71a-103">Instalace PowerShellu Core v macOS</span><span class="sxs-lookup"><span data-stu-id="9b71a-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="9b71a-104">PowerShell Core podporuje macOS 10.12 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="9b71a-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="9b71a-105">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="9b71a-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="9b71a-106">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="9b71a-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="9b71a-107">Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="9b71a-107">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="9b71a-108">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="9b71a-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="9b71a-109">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="9b71a-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="9b71a-110">Po instalaci Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="9b71a-110">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="9b71a-111">Nejdřív nainstalujte [Homebrew Cask][cask], takže můžete nainstalovat další balíčky a instalace [Cask-verze] [cask verze], která vám umožní nainstalovat alternativní verze balíčků:</span><span class="sxs-lookup"><span data-stu-id="9b71a-111">First, install [Homebrew-Cask][cask], so you can install more packages and install [Cask-Versions][cask-version] which lets you install alternative versions of packages:</span></span>

```sh
brew tap caskroom/cask
brew tap caskroom/versions
```

<span data-ttu-id="9b71a-112">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b71a-112">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="9b71a-113">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="9b71a-113">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="9b71a-114">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b71a-114">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="9b71a-115">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.</span><span class="sxs-lookup"><span data-stu-id="9b71a-115">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="9b71a-116">a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="9b71a-116">and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions

### <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="9b71a-117">Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší</span><span class="sxs-lookup"><span data-stu-id="9b71a-117">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="9b71a-118">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="9b71a-118">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="9b71a-119">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="9b71a-119">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="9b71a-120">Po instalaci Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="9b71a-120">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="9b71a-121">Nejdřív nainstalujte [Homebrew Cask][cask], takže můžete nainstalovat další balíčky a instalace [Cask-verze] [cask verze], která vám umožní nainstalovat alternativní verze balíčků:</span><span class="sxs-lookup"><span data-stu-id="9b71a-121">First, install [Homebrew-Cask][cask], so you can install more packages and install [Cask-Versions][cask-version] which lets you install alternative versions of packages:</span></span>

```sh
brew tap caskroom/cask
brew tap caskroom/versions
```

<span data-ttu-id="9b71a-122">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b71a-122">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="9b71a-123">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="9b71a-123">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="9b71a-124">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b71a-124">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="9b71a-125">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.</span><span class="sxs-lookup"><span data-stu-id="9b71a-125">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="9b71a-126">a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="9b71a-126">and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions

### <a name="installation-via-direct-download"></a><span data-ttu-id="9b71a-127">Instalace přes přímé stažení</span><span class="sxs-lookup"><span data-stu-id="9b71a-127">Installation via Direct Download</span></span>

<span data-ttu-id="9b71a-128">Stáhněte si balíček PKG `powershell-6.1.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="9b71a-128">Download the PKG package `powershell-6.1.0-osx-x64.pkg`</span></span>
<span data-ttu-id="9b71a-129">z [uvolní][] stránky na svém počítači s macOS.</span><span class="sxs-lookup"><span data-stu-id="9b71a-129">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="9b71a-130">Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="9b71a-130">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="9b71a-131">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="9b71a-131">Binary Archives</span></span>

<span data-ttu-id="9b71a-132">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro macOS a Linux platformy a povolíte pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="9b71a-132">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="9b71a-133">Instalace binárních archivy v systému macOS</span><span class="sxs-lookup"><span data-stu-id="9b71a-133">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="9b71a-134">Odinstalace Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="9b71a-134">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="9b71a-135">Pokud jste nainstalovali Powershellu pomocí Homebrew, je snadné odinstalace:</span><span class="sxs-lookup"><span data-stu-id="9b71a-135">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="9b71a-136">Pokud jste instalovali prostřednictvím přímé stažení prostředí PowerShell, musí ručně odebrat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b71a-136">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="9b71a-137">Odebrání dalších cest prostředí PowerShell, najdete [cesty][] části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="9b71a-137">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="9b71a-138">Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.</span><span class="sxs-lookup"><span data-stu-id="9b71a-138">This is not necessary if you installed with Homebrew.</span></span>

[Cesty]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="9b71a-140">Cesty</span><span class="sxs-lookup"><span data-stu-id="9b71a-140">Paths</span></span>

* <span data-ttu-id="9b71a-141">`$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="9b71a-141">`$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="9b71a-142">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="9b71a-142">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="9b71a-143">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="9b71a-143">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="9b71a-144">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="9b71a-144">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="9b71a-145">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="9b71a-145">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="9b71a-146">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="9b71a-146">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="9b71a-147">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="9b71a-147">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="9b71a-148">Profily respektovat konfigurace Powershellu na hostitele.</span><span class="sxs-lookup"><span data-stu-id="9b71a-148">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="9b71a-149">Proto výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="9b71a-149">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="9b71a-150">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="9b71a-150">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="9b71a-151">Protože je odvozený od BSD, předpona macOS `/usr/local` se použije namísto `/opt`.</span><span class="sxs-lookup"><span data-stu-id="9b71a-151">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="9b71a-152">Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`, a symlink je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="9b71a-152">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9b71a-153">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="9b71a-153">Additional Resources</span></span>

* <span data-ttu-id="9b71a-154">[Homebrew Web][brew]</span><span class="sxs-lookup"><span data-stu-id="9b71a-154">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="9b71a-155">[Úložiště Github Homebrew][GitHub]</span><span class="sxs-lookup"><span data-stu-id="9b71a-155">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="9b71a-156">[Homebrew Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="9b71a-156">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

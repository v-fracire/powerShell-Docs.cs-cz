---
title: Instalace PowerShellu Core v macOS
description: Informace o instalaci Powershellu Core v macOS
ms.date: 08/06/2018
ms.openlocfilehash: ff1814d95b3ca3fa8497069dff249fd2ad5576ef
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587461"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="3da50-103">Instalace PowerShellu Core v macOS</span><span class="sxs-lookup"><span data-stu-id="3da50-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="3da50-104">PowerShell Core podporuje macOS 10.12 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="3da50-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="3da50-105">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="3da50-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="3da50-106">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="3da50-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="3da50-107">Instalace pomocí Homebrew v systému macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="3da50-107">Installation via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="3da50-108">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="3da50-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="3da50-109">V okně terminálu zadejte `brew` ke spuštění Homebrew.</span><span class="sxs-lookup"><span data-stu-id="3da50-109">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="3da50-110">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="3da50-110">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="3da50-111">Pokud jste v minulosti nainstalovali Homebrew, je vždy vhodné spustit "brew resetování aktualizací" & & "brew update".</span><span class="sxs-lookup"><span data-stu-id="3da50-111">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

> <span data-ttu-id="3da50-112">Starší verze Homebrew používaly klepněte na "caskroom/cask", který nepoužívá a migrovat do "homebrew/cask".</span><span class="sxs-lookup"><span data-stu-id="3da50-112">Older versions of Homebrew used the tap 'caskroom/cask', which has been deprecated, and migrated into 'homebrew/cask'.</span></span>  <span data-ttu-id="3da50-113">Další informace najdete v [Homebrew cask][cask].</span><span class="sxs-lookup"><span data-stu-id="3da50-113">More information can be found at [Homebrew-cask][cask].</span></span> <span data-ttu-id="3da50-114">Pomocí příkazu "brew klepněte na" vypsat aktuální odposlouchávání.</span><span class="sxs-lookup"><span data-stu-id="3da50-114">Use the 'brew tap' command to list your current taps.</span></span>  <span data-ttu-id="3da50-115">Pokud se zobrazí ' caskroom/cask' můžete použít "brew aktualizace" mít Homebrew migrovat odposlouchávání.</span><span class="sxs-lookup"><span data-stu-id="3da50-115">If you see 'caskroom/cask' you can use 'brew update' to have Homebrew migrate the taps.</span></span>

```sh
brew tap
brew update
```

<span data-ttu-id="3da50-116">Jakmile je nainstalovaný a aktualizovali Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="3da50-116">Once you've installed/updated Homebrew, installing PowerShell is easy.</span></span>

<span data-ttu-id="3da50-117">K instalaci prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3da50-117">To install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="3da50-118">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="3da50-118">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="3da50-119">Ukončete prostředí PowerShell a vraťte se do bash, použijte příkaz "konec".</span><span class="sxs-lookup"><span data-stu-id="3da50-119">To exit PowerShell, and return to bash, use the 'exit' command.</span></span>
```sh
exit
```

<span data-ttu-id="3da50-120">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3da50-120">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="3da50-121">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="3da50-121">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installing-preview-via-homebrew-on-macos-1012"></a><span data-ttu-id="3da50-122">Instalace Preview pomocí Homebrew v systému macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="3da50-122">Installing Preview via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="3da50-123">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="3da50-123">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="3da50-124">V okně terminálu zadejte `brew` ke spuštění Homebrew.</span><span class="sxs-lookup"><span data-stu-id="3da50-124">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="3da50-125">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="3da50-125">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="3da50-126">Pokud jste v minulosti nainstalovali Homebrew, je vždy vhodné spustit "brew resetování aktualizací" & & "brew update".</span><span class="sxs-lookup"><span data-stu-id="3da50-126">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

<span data-ttu-id="3da50-127">Potom musí klepněte `versions` sudech úložišti, abyste si balíček ve verzi preview:</span><span class="sxs-lookup"><span data-stu-id="3da50-127">Then, you must tap the `versions` casks repository to get the preview package:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="3da50-128">Instalace Powershellu ve verzi Preview:</span><span class="sxs-lookup"><span data-stu-id="3da50-128">To install PowerShell Preview:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="3da50-129">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="3da50-129">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="3da50-130">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell ve verzi Preview:</span><span class="sxs-lookup"><span data-stu-id="3da50-130">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell Preview:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="3da50-131">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="3da50-131">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installation-via-direct-download"></a><span data-ttu-id="3da50-132">Instalace přes přímé stažení</span><span class="sxs-lookup"><span data-stu-id="3da50-132">Installation via Direct Download</span></span>

<span data-ttu-id="3da50-133">Stáhněte si balíček PKG `powershell-6.0.2-osx.10.12-x64.pkg` z [uvolní][] stránky na svém počítači s macOS.</span><span class="sxs-lookup"><span data-stu-id="3da50-133">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="3da50-134">Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="3da50-134">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="3da50-135">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="3da50-135">Binary Archives</span></span>

<span data-ttu-id="3da50-136">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro macOS a Linux platformy a povolíte pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="3da50-136">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="3da50-137">Instalace binárních archivy v systému macOS</span><span class="sxs-lookup"><span data-stu-id="3da50-137">Installing binary archives on macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.2

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.2

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.2/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.2/pwsh /usr/local/bin/pwsh
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="3da50-138">Odinstalace Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="3da50-138">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="3da50-139">Pokud jste nainstalovali Powershellu pomocí Homebrew, je snadné odinstalace:</span><span class="sxs-lookup"><span data-stu-id="3da50-139">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="3da50-140">Pokud jste instalovali prostřednictvím přímé stažení prostředí PowerShell, musí ručně odebrat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3da50-140">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="3da50-141">Odebrání dalších cest prostředí PowerShell, najdete [cesty][] části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="3da50-141">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="3da50-142">Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.</span><span class="sxs-lookup"><span data-stu-id="3da50-142">This is not necessary if you installed with Homebrew.</span></span>

[Cesty]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="3da50-144">Cesty</span><span class="sxs-lookup"><span data-stu-id="3da50-144">Paths</span></span>

* <span data-ttu-id="3da50-145">`$PSHOME` je `/usr/local/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="3da50-145">`$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="3da50-146">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="3da50-146">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="3da50-147">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="3da50-147">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="3da50-148">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="3da50-148">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="3da50-149">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="3da50-149">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="3da50-150">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="3da50-150">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="3da50-151">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="3da50-151">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="3da50-152">Profily respektovat konfigurace Powershellu na hostitele.</span><span class="sxs-lookup"><span data-stu-id="3da50-152">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="3da50-153">Proto výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="3da50-153">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="3da50-154">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="3da50-154">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="3da50-155">Protože je odvozený od BSD, předpona macOS `/usr/local` se použije namísto `/opt`.</span><span class="sxs-lookup"><span data-stu-id="3da50-155">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="3da50-156">Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.0.2/`, a symlink je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="3da50-156">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3da50-157">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="3da50-157">Additional Resources</span></span>

* <span data-ttu-id="3da50-158">[Homebrew Web][brew]</span><span class="sxs-lookup"><span data-stu-id="3da50-158">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="3da50-159">[Úložiště Github Homebrew][GitHub]</span><span class="sxs-lookup"><span data-stu-id="3da50-159">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="3da50-160">[Homebrew Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="3da50-160">[Homebrew-Cask][cask]</span></span>


[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="37b1d-101">Instalace PowerShellu Core v macOS</span><span class="sxs-lookup"><span data-stu-id="37b1d-101">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="37b1d-102">PowerShell Core podporuje macOS 10.12 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="37b1d-102">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="37b1d-103">Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="37b1d-103">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="37b1d-104">Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="37b1d-104">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="37b1d-105">Instalace pomocí Homebrew v systému macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="37b1d-105">Installation via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="37b1d-106">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="37b1d-106">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="37b1d-107">V okně terminálu zadejte `brew` ke spuštění Homebrew.</span><span class="sxs-lookup"><span data-stu-id="37b1d-107">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="37b1d-108">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="37b1d-108">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="37b1d-109">Pokud jste v minulosti nainstalovali Homebrew, je vždy vhodné spustit "brew resetování aktualizací" & & "brew update".</span><span class="sxs-lookup"><span data-stu-id="37b1d-109">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

> <span data-ttu-id="37b1d-110">Starší verze Homebrew používaly klepněte na "caskroom/cask", který nepoužívá a migrovat do "homebrew/cask".</span><span class="sxs-lookup"><span data-stu-id="37b1d-110">Older versions of Homebrew used the tap 'caskroom/cask', which has been deprecated, and migrated into 'homebrew/cask'.</span></span>  <span data-ttu-id="37b1d-111">Další informace najdete v [Homebrew cask][cask].</span><span class="sxs-lookup"><span data-stu-id="37b1d-111">More information can be found at [Homebrew-cask][cask].</span></span> <span data-ttu-id="37b1d-112">Pomocí příkazu "brew klepněte na" vypsat aktuální odposlouchávání.</span><span class="sxs-lookup"><span data-stu-id="37b1d-112">Use the 'brew tap' command to list your current taps.</span></span>  <span data-ttu-id="37b1d-113">Pokud se zobrazí ' caskroom/cask' můžete použít "brew aktualizace" mít Homebrew migrovat odposlouchávání.</span><span class="sxs-lookup"><span data-stu-id="37b1d-113">If you see 'caskroom/cask' you can use 'brew update' to have Homebrew migrate the taps.</span></span>

```sh
brew tap
brew update
```

<span data-ttu-id="37b1d-114">Jakmile je nainstalovaný a aktualizovali Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="37b1d-114">Once you've installed/updated Homebrew, installing PowerShell is easy.</span></span>

<span data-ttu-id="37b1d-115">K instalaci prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37b1d-115">To install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="37b1d-116">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="37b1d-116">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="37b1d-117">Ukončete prostředí PowerShell a vraťte se do bash, použijte příkaz "konec".</span><span class="sxs-lookup"><span data-stu-id="37b1d-117">To exit PowerShell, and return to bash, use the 'exit' command.</span></span> 
```sh
exit
```

<span data-ttu-id="37b1d-118">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37b1d-118">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="37b1d-119">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="37b1d-119">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installing-preview-via-homebrew-on-macos-1012"></a><span data-ttu-id="37b1d-120">Instalace Preview pomocí Homebrew v systému macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="37b1d-120">Installing Preview via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="37b1d-121">[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.</span><span class="sxs-lookup"><span data-stu-id="37b1d-121">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="37b1d-122">V okně terminálu zadejte `brew` ke spuštění Homebrew.</span><span class="sxs-lookup"><span data-stu-id="37b1d-122">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="37b1d-123">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="37b1d-123">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="37b1d-124">Pokud jste v minulosti nainstalovali Homebrew, je vždy vhodné spustit "brew resetování aktualizací" & & "brew update".</span><span class="sxs-lookup"><span data-stu-id="37b1d-124">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

<span data-ttu-id="37b1d-125">Potom musí klepněte `versions` sudech úložišti, abyste si balíček ve verzi preview:</span><span class="sxs-lookup"><span data-stu-id="37b1d-125">Then, you must tap the `versions` casks repository to get the preview package:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="37b1d-126">Instalace Powershellu ve verzi Preview:</span><span class="sxs-lookup"><span data-stu-id="37b1d-126">To install PowerShell Preview:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="37b1d-127">Nakonec ověřte, že vaše instalace pracuje správně:</span><span class="sxs-lookup"><span data-stu-id="37b1d-127">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="37b1d-128">Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell ve verzi Preview:</span><span class="sxs-lookup"><span data-stu-id="37b1d-128">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell Preview:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="37b1d-129">Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="37b1d-129">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installation-via-direct-download"></a><span data-ttu-id="37b1d-130">Instalace přes přímé stažení</span><span class="sxs-lookup"><span data-stu-id="37b1d-130">Installation via Direct Download</span></span>

<span data-ttu-id="37b1d-131">Stáhněte si balíček PKG `powershell-6.0.2-osx.10.12-x64.pkg` z [uvolní][] stránky na svém počítači s macOS.</span><span class="sxs-lookup"><span data-stu-id="37b1d-131">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="37b1d-132">Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="37b1d-132">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="37b1d-133">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="37b1d-133">Binary Archives</span></span>

<span data-ttu-id="37b1d-134">Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro macOS a Linux platformy a povolíte pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="37b1d-134">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="37b1d-135">Instalace binárních archivy v systému macOS</span><span class="sxs-lookup"><span data-stu-id="37b1d-135">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="37b1d-136">Odinstalace Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="37b1d-136">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="37b1d-137">Pokud jste nainstalovali Powershellu pomocí Homebrew, je snadné odinstalace:</span><span class="sxs-lookup"><span data-stu-id="37b1d-137">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="37b1d-138">Pokud jste instalovali prostřednictvím přímé stažení prostředí PowerShell, musí ručně odebrat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="37b1d-138">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="37b1d-139">Odebrání dalších cest prostředí PowerShell, najdete [cesty][] části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="37b1d-139">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="37b1d-140">Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.</span><span class="sxs-lookup"><span data-stu-id="37b1d-140">This is not necessary if you installed with Homebrew.</span></span>

[Cesty]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="37b1d-142">Cesty</span><span class="sxs-lookup"><span data-stu-id="37b1d-142">Paths</span></span>

* <span data-ttu-id="37b1d-143">`$PSHOME` je `/usr/local/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="37b1d-143">`$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="37b1d-144">Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="37b1d-144">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="37b1d-145">Výchozí profily se budou číst z `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="37b1d-145">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="37b1d-146">Moduly uživatele bude číst z `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="37b1d-146">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="37b1d-147">Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="37b1d-147">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="37b1d-148">Výchozí moduly se budou číst z `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="37b1d-148">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="37b1d-149">Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="37b1d-149">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="37b1d-150">Profily respektovat konfigurace Powershellu na hostitele.</span><span class="sxs-lookup"><span data-stu-id="37b1d-150">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="37b1d-151">Proto výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="37b1d-151">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="37b1d-152">Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="37b1d-152">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="37b1d-153">Protože je odvozený od BSD, předpona macOS `/usr/local` se použije namísto `/opt`.</span><span class="sxs-lookup"><span data-stu-id="37b1d-153">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="37b1d-154">Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.0.2/`, a symlink je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="37b1d-154">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37b1d-155">Další zdroje informací</span><span class="sxs-lookup"><span data-stu-id="37b1d-155">Additional Resources</span></span>

* <span data-ttu-id="37b1d-156">[Homebrew Web][brew]</span><span class="sxs-lookup"><span data-stu-id="37b1d-156">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="37b1d-157">[Úložiště Github Homebrew][GitHub]</span><span class="sxs-lookup"><span data-stu-id="37b1d-157">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="37b1d-158">[Homebrew Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="37b1d-158">[Homebrew-Cask][cask]</span></span>


[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

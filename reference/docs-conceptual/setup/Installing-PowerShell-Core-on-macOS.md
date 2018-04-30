# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="33f31-101">Instalace jádra prostředí PowerShell v systému macOS</span><span class="sxs-lookup"><span data-stu-id="33f31-101">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="33f31-102">Prostředí PowerShell jádro podporuje systému macOS 10.12 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="33f31-102">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="33f31-103">Všechny balíčky jsou k dispozici na našem Githubu [uvolní][] stránky.</span><span class="sxs-lookup"><span data-stu-id="33f31-103">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="33f31-104">Spustit po instalaci balíčku `pwsh` z terminálu.</span><span class="sxs-lookup"><span data-stu-id="33f31-104">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="33f31-105">Instalaci přes Homebrew v systému macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="33f31-105">Installation via Homebrew on macOS 10.12</span></span>

<span data-ttu-id="33f31-106">[Homebrew] [ brew] je správce upřednostňované balíčků pro systému macOS.</span><span class="sxs-lookup"><span data-stu-id="33f31-106">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="33f31-107">Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].</span><span class="sxs-lookup"><span data-stu-id="33f31-107">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="33f31-108">Jakmile jste nainstalovali Homebrew, instalace prostředí PowerShell je snadné.</span><span class="sxs-lookup"><span data-stu-id="33f31-108">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="33f31-109">Nejdřív nainstalujte [obalového Homebrew souboru][cask], takže můžete nainstalovat další balíčky:</span><span class="sxs-lookup"><span data-stu-id="33f31-109">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="33f31-110">Nyní můžete nainstalovat prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="33f31-110">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="33f31-111">Nakonec ověřte, zda je správně funguje instalaci vaší:</span><span class="sxs-lookup"><span data-stu-id="33f31-111">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="33f31-112">Když jsou vydávány nové verze prostředí PowerShell, jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="33f31-112">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="33f31-113">Výše uvedených příkazů můžete volat v rámci hostitele prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.</span><span class="sxs-lookup"><span data-stu-id="33f31-113">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="33f31-114">a aktualizujte hodnoty zobrazené v $PSVersionTable.</span><span class="sxs-lookup"><span data-stu-id="33f31-114">and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download"></a><span data-ttu-id="33f31-115">Instalace prostřednictvím přímé stahování</span><span class="sxs-lookup"><span data-stu-id="33f31-115">Installation via Direct Download</span></span>

<span data-ttu-id="33f31-116">Stáhněte si balíček PKG `powershell-6.0.2-osx.10.12-x64.pkg` z [uvolní][] stránky do systému macOS počítače.</span><span class="sxs-lookup"><span data-stu-id="33f31-116">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="33f31-117">Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:</span><span class="sxs-lookup"><span data-stu-id="33f31-117">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="33f31-118">Binární archivy</span><span class="sxs-lookup"><span data-stu-id="33f31-118">Binary Archives</span></span>

<span data-ttu-id="33f31-119">Prostředí PowerShell binární `tar.gz` archivy jsou k dispozici pro systému macOS a platformy Linux k povolení pokročilé scénáře nasazení.</span><span class="sxs-lookup"><span data-stu-id="33f31-119">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="33f31-120">V systému macOS instalaci binární archivy</span><span class="sxs-lookup"><span data-stu-id="33f31-120">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="33f31-121">Odinstalace základní prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="33f31-121">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="33f31-122">Pokud jste nainstalovali prostředí PowerShell s Homebrew, je snadné odinstalace:</span><span class="sxs-lookup"><span data-stu-id="33f31-122">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="33f31-123">Pokud jste nainstalovali PowerShell prostřednictvím přímé stahování, musíte ručně odstranit prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="33f31-123">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="33f31-124">Odebrat další cesty prostředí PowerShell, najdete [cesty][] části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="33f31-124">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="33f31-125">Toto není nutné v případě, že jste nainstalovali s Homebrew.</span><span class="sxs-lookup"><span data-stu-id="33f31-125">This is not necessary if you installed with Homebrew.</span></span>

[cesty]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="33f31-127">Cesty</span><span class="sxs-lookup"><span data-stu-id="33f31-127">Paths</span></span>

* <span data-ttu-id="33f31-128">`$PSHOME` je `/opt/microsoft/powershell/6.0.0/`</span><span class="sxs-lookup"><span data-stu-id="33f31-128">`$PSHOME` is `/opt/microsoft/powershell/6.0.0/`</span></span>
* <span data-ttu-id="33f31-129">Profily uživatelů, bude číst ze `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="33f31-129">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="33f31-130">Výchozí profily bude číst ze `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="33f31-130">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="33f31-131">Moduly uživatele bude číst ze `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="33f31-131">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="33f31-132">Sdílené moduly, bude číst ze `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="33f31-132">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="33f31-133">Výchozí moduly, bude číst ze `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="33f31-133">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="33f31-134">Historie PSReadline budou zaznamenány do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="33f31-134">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="33f31-135">Profily respektují konfigurace prostředí PowerShell pro jednotlivé hostitele.</span><span class="sxs-lookup"><span data-stu-id="33f31-135">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="33f31-136">Proto výchozí konkrétního hostitele profily existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.</span><span class="sxs-lookup"><span data-stu-id="33f31-136">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="33f31-137">Prostředí PowerShell respektuje [XDG základní Directory specifikace] [ xdg-bds] v systému macOS.</span><span class="sxs-lookup"><span data-stu-id="33f31-137">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="33f31-138">Protože je odvozený od BSD, předponu systému macOS `/usr/local` se používá místo `/opt`.</span><span class="sxs-lookup"><span data-stu-id="33f31-138">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="33f31-139">Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.0.0/`, a symlink je umístěn na `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="33f31-139">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

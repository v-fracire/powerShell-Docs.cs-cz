# <a name="installing-powershell-core-on-macos"></a>Instalace jádra prostředí PowerShell v systému macOS

Prostředí PowerShell jádro podporuje systému macOS 10.12 a vyšší.
Všechny balíčky jsou k dispozici na našem Githubu [uvolní][] stránky.
Spustit po instalaci balíčku `pwsh` z terminálu.

### <a name="installation-via-homebrew-on-macos-1012"></a>Instalaci přes Homebrew v systému macOS 10.12

[Homebrew] [ brew] je správce upřednostňované balíčků pro systému macOS.
Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].

Jakmile jste nainstalovali Homebrew, instalace prostředí PowerShell je snadné.
Nejdřív nainstalujte [obalového Homebrew souboru][cask], takže můžete nainstalovat další balíčky:

```sh
brew tap caskroom/cask
```

Nyní můžete nainstalovat prostředí PowerShell:

```sh
brew cask install powershell
```

Nakonec ověřte, zda je správně funguje instalaci vaší:

```sh
pwsh
```

Když jsou vydávány nové verze prostředí PowerShell, jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> Výše uvedených příkazů můžete volat v rámci hostitele prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.
> a aktualizujte hodnoty zobrazené v $PSVersionTable.

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download"></a>Instalace prostřednictvím přímé stahování

Stáhněte si balíček PKG `powershell-6.0.2-osx.10.12-x64.pkg` z [uvolní][] stránky do systému macOS počítače.

Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a>Binární archivy

Prostředí PowerShell binární `tar.gz` archivy jsou k dispozici pro systému macOS a platformy Linux k povolení pokročilé scénáře nasazení.

### <a name="installing-binary-archives-on-macos"></a>V systému macOS instalaci binární archivy

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

## <a name="uninstalling-powershell-core"></a>Odinstalace základní prostředí PowerShell

Pokud jste nainstalovali prostředí PowerShell s Homebrew, je snadné odinstalace:

```sh
brew cask uninstall powershell
```

Pokud jste nainstalovali PowerShell prostřednictvím přímé stahování, musíte ručně odstranit prostředí PowerShell:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Odebrat další cesty prostředí PowerShell, najdete [cesty][] části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.

> [!NOTE]
> Toto není nutné v případě, že jste nainstalovali s Homebrew.

[cesty]:#paths

## <a name="paths"></a>Cesty

* `$PSHOME` je `/opt/microsoft/powershell/6.0.0/`
* Profily uživatelů, bude číst ze `~/.config/powershell/profile.ps1`
* Výchozí profily bude číst ze `$PSHOME/profile.ps1`
* Moduly uživatele bude číst ze `~/.local/share/powershell/Modules`
* Sdílené moduly, bude číst ze `/usr/local/share/powershell/Modules`
* Výchozí moduly, bude číst ze `$PSHOME/Modules`
* Historie PSReadline budou zaznamenány do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

Profily respektují konfigurace prostředí PowerShell pro jednotlivé hostitele.
Proto výchozí konkrétního hostitele profily existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.

Prostředí PowerShell respektuje [XDG základní Directory specifikace] [ xdg-bds] v systému macOS.

Protože je odvozený od BSD, předponu systému macOS `/usr/local` se používá místo `/opt`.
Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.0.0/`, a symlink je umístěn na `/usr/local/bin/pwsh`.

[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

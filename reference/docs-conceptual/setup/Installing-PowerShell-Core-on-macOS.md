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
# <a name="installing-powershell-core-on-macos"></a>Instalace PowerShellu Core v macOS

PowerShell Core podporuje macOS 10.12 a vyšší.
Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.
Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.

### <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší

[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.
Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].

Po instalaci Homebrew, instalace prostředí PowerShell je snadné.
Nejdřív nainstalujte [Homebrew Cask][cask], takže můžete nainstalovat další balíčky a instalace [Cask-verze] [cask verze], která vám umožní nainstalovat alternativní verze balíčků:

```sh
brew tap caskroom/cask
brew tap caskroom/versions
```

Nyní můžete nainstalovat prostředí PowerShell:

```sh
brew cask install powershell-preview
```

Nakonec ověřte, že vaše instalace pracuje správně:

```sh
pwsh-preview
```

Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.
> a aktualizujte hodnoty zobrazené v $PSVersionTable.

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions

### <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší

[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.
Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].

Po instalaci Homebrew, instalace prostředí PowerShell je snadné.
Nejdřív nainstalujte [Homebrew Cask][cask], takže můžete nainstalovat další balíčky a instalace [Cask-verze] [cask verze], která vám umožní nainstalovat alternativní verze balíčků:

```sh
brew tap caskroom/cask
brew tap caskroom/versions
```

Nyní můžete nainstalovat prostředí PowerShell:

```sh
brew cask install powershell-preview
```

Nakonec ověřte, že vaše instalace pracuje správně:

```sh
pwsh-preview
```

Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat a dokončit upgrade.
> a aktualizujte hodnoty zobrazené v $PSVersionTable.

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions

### <a name="installation-via-direct-download"></a>Instalace přes přímé stažení

Stáhněte si balíček PKG `powershell-6.1.0-osx-x64.pkg`
z [uvolní][] stránky na svém počítači s macOS.

Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

## <a name="binary-archives"></a>Binární archivy

Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro macOS a Linux platformy a povolíte pokročilé scénáře nasazení.

### <a name="installing-binary-archives-on-macos"></a>Instalace binárních archivy v systému macOS

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

## <a name="uninstalling-powershell-core"></a>Odinstalace Powershellu Core

Pokud jste nainstalovali Powershellu pomocí Homebrew, je snadné odinstalace:

```sh
brew cask uninstall powershell
```

Pokud jste instalovali prostřednictvím přímé stažení prostředí PowerShell, musí ručně odebrat prostředí PowerShell:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Odebrání dalších cest prostředí PowerShell, najdete [cesty][] části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.

> [!NOTE]
> Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.

[Cesty]:#paths

## <a name="paths"></a>Cesty

* `$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`
* Uživatelské profily se budou číst z `~/.config/powershell/profile.ps1`
* Výchozí profily se budou číst z `$PSHOME/profile.ps1`
* Moduly uživatele bude číst z `~/.local/share/powershell/Modules`
* Sdílené moduly se budou číst z `/usr/local/share/powershell/Modules`
* Výchozí moduly se budou číst z `$PSHOME/Modules`
* Historie PSReadline se zaznamená do `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

Profily respektovat konfigurace Powershellu na hostitele.
Proto výchozí profily hostitelů konkrétní existuje v `Microsoft.PowerShell_profile.ps1` ve stejném umístění.

Respektuje prostředí PowerShell [XDG Base adresářovou specifikaci] [ xdg-bds] v systému macOS.

Protože je odvozený od BSD, předpona macOS `/usr/local` se použije namísto `/opt`.
Proto `$PSHOME` je `/usr/local/microsoft/powershell/6.1.0/`, a symlink je umístěn na `/usr/local/bin/pwsh`.

## <a name="additional-resources"></a>Další zdroje informací

* [Homebrew Web][brew]
* [Úložiště Github Homebrew][GitHub]
* [Homebrew Cask][cask]

[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

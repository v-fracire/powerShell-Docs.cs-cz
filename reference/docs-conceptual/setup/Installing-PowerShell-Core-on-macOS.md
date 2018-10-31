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
# <a name="installing-powershell-core-on-macos"></a>Instalace PowerShellu Core v macOS

PowerShell Core podporuje macOS 10.12 a vyšší.
Všechny balíčky jsou k dispozici na náš GitHub [uvolní][] stránky.
Jakmile je balíček nainstalován, spustit `pwsh` z terminálu.

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a>Instalace nejnovější stabilní verze pomocí Homebrew v systému macOS 10.12 nebo vyšší

[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.
Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].

Nyní můžete nainstalovat prostředí PowerShell:

```sh
brew cask install powershell
```

Nakonec ověřte, že vaše instalace pracuje správně:

```sh
pwsh
```

Po vydání nové verze powershellu jsou jednoduše aktualizovat na Homebrew vzorce a upgrade prostředí PowerShell:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> Výše uvedené příkazy mohou být volány v hostitelském prostředí PowerShell (pwsh), ale pak musí být prostředí PowerShell byl ukončen a restartovat, aby upgrade dokončil a aktualizujte hodnoty zobrazené v $PSVersionTable.

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>Instalace nejnovější verze preview verzi pomocí Homebrew v systému macOS 10.12 nebo vyšší

[Homebrew] [ brew] je správce upřednostňované balíček pro macOS.
Pokud `brew` příkaz nebyl nalezen, je nutné nainstalovat následující Homebrew [podle pokynů v nich][brew].

Po instalaci Homebrew, instalace prostředí PowerShell je snadné.
Nejdřív nainstalujte [Cask verze] [ cask-versions] který umožňuje nainstalovat alternativní verze cask balíčků:

```sh
brew tap homebrew/cask-versions
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

## <a name="installation-via-direct-download"></a>Instalace přes přímé stažení

Stáhněte si balíček PKG `powershell-6.1.0-osx-x64.pkg`
z [uvolní][] stránky na svém počítači s macOS.

Poklikejte na soubor a postupujte podle pokynů nebo ji nainstalovat z terminálu:

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

## <a name="binary-archives"></a>Binární archivy

Binární soubor prostředí PowerShell `tar.gz` archivy jsou k dispozici pro platformu macOS umožňující pokročilé scénáře nasazení.

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

Odebrání dalších cest prostředí PowerShell, najdete [cesty](#paths) části v tomto dokumentu a odeberte požadovanou cesty pomocí `sudo rm`.

> [!NOTE]
> Toto není nutné v případě, že jste nainstalovali pomocí Homebrew.

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
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[uvolní]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html

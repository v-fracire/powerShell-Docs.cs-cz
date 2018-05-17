---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 64a29aa87507e65a182837df538c5e695c420cb3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="uninstallation-instructions"></a>Odinstalace pokyny

## <a name="using-command-prompt"></a>Pomocí příkazového řádku
1.  Otevřete **příkazového řádku.**
2.  Spustit [Spouštěč samostatné aktualizace Windows](https://support.microsoft.com/en-us/kb/934307) jak je uvedeno níže:

V systému Windows Server 2012 R2 a Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
On Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
Na Windows Server 2008 R2 SP1 a Windows 7 SP1:
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a>Pomocí ovládacích panelů
1.  Otevřete **ovládací panely.**
2.  Otevřete **programy**, pak otevřete **odinstalovat program.**
3.  Klikněte na tlačítko **zobrazit nainstalované aktualizace.**
4.  Vyberte **Windows Management Framework 5.0** ze seznamu nainstalovaných aktualizací. To odpovídá *KB3134758*, *KB3134759*, nebo *KB3134760*. Klikněte na tlačítko **odinstalovat.**

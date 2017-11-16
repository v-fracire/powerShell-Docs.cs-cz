---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 3392db954c22030bb64ae5093619d23952e1fcdb
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="uninstallation-instructions"></a>Odinstalace pokyny

## <a name="using-command-prompt"></a>Pomocí příkazového řádku
1.  Otevřete **příkazového řádku.**
2.  Spustit [Spouštěč samostatné aktualizace Windows](https://support.microsoft.com/en-us/kb/934307) jak je uvedeno níže:

V systému Windows Server 2012 R2 a Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
V systému Windows Server 2012:
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


---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 64a29aa87507e65a182837df538c5e695c420cb3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222050"
---
# <a name="uninstallation-instructions"></a><span data-ttu-id="9ff70-102">Odinstalace pokyny</span><span class="sxs-lookup"><span data-stu-id="9ff70-102">Uninstallation Instructions</span></span>

## <a name="using-command-prompt"></a><span data-ttu-id="9ff70-103">Pomocí příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="9ff70-103">Using Command Prompt</span></span>
1.  <span data-ttu-id="9ff70-104">Otevřete **příkazového řádku.**</span><span class="sxs-lookup"><span data-stu-id="9ff70-104">Open **Command Prompt.**</span></span>
2.  <span data-ttu-id="9ff70-105">Spustit [Spouštěč samostatné aktualizace Windows](https://support.microsoft.com/en-us/kb/934307) jak je uvedeno níže:</span><span class="sxs-lookup"><span data-stu-id="9ff70-105">Run the [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) as shown below:</span></span>

<span data-ttu-id="9ff70-106">V systému Windows Server 2012 R2 a Windows 8.1:</span><span class="sxs-lookup"><span data-stu-id="9ff70-106">On Windows Server 2012 R2 and Windows 8.1:</span></span>
```powershell
wusa /uninstall /kb:3134758
```
<span data-ttu-id="9ff70-107">On Windows Server 2012:</span><span class="sxs-lookup"><span data-stu-id="9ff70-107">On Windows Server 2012:</span></span>
```powershell
wusa /uninstall /kb:3134759
```
<span data-ttu-id="9ff70-108">Na Windows Server 2008 R2 SP1 a Windows 7 SP1:</span><span class="sxs-lookup"><span data-stu-id="9ff70-108">On Windows Server 2008 R2 SP1 and Windows 7 SP1:</span></span>
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a><span data-ttu-id="9ff70-109">Pomocí ovládacích panelů</span><span class="sxs-lookup"><span data-stu-id="9ff70-109">Using Control Panel</span></span>
1.  <span data-ttu-id="9ff70-110">Otevřete **ovládací panely.**</span><span class="sxs-lookup"><span data-stu-id="9ff70-110">Open **Control Panel.**</span></span>
2.  <span data-ttu-id="9ff70-111">Otevřete **programy**, pak otevřete **odinstalovat program.**</span><span class="sxs-lookup"><span data-stu-id="9ff70-111">Open **Programs**, then open **Uninstall a program.**</span></span>
3.  <span data-ttu-id="9ff70-112">Klikněte na tlačítko **zobrazit nainstalované aktualizace.**</span><span class="sxs-lookup"><span data-stu-id="9ff70-112">Click **View installed updates.**</span></span>
4.  <span data-ttu-id="9ff70-113">Vyberte **Windows Management Framework 5.0** ze seznamu nainstalovaných aktualizací.</span><span class="sxs-lookup"><span data-stu-id="9ff70-113">Select **Windows Management Framework 5.0** from the list of installed updates.</span></span> <span data-ttu-id="9ff70-114">To odpovídá *KB3134758*, *KB3134759*, nebo *KB3134760*.</span><span class="sxs-lookup"><span data-stu-id="9ff70-114">This corresponds to *KB3134758*, *KB3134759*, or *KB3134760*.</span></span> <span data-ttu-id="9ff70-115">Klikněte na tlačítko **odinstalovat.**</span><span class="sxs-lookup"><span data-stu-id="9ff70-115">Click **Uninstall.**</span></span>

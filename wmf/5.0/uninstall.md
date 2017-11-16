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
# <a name="uninstallation-instructions"></a><span data-ttu-id="5d3f3-102">Odinstalace pokyny</span><span class="sxs-lookup"><span data-stu-id="5d3f3-102">Uninstallation Instructions</span></span>

## <a name="using-command-prompt"></a><span data-ttu-id="5d3f3-103">Pomocí příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="5d3f3-103">Using Command Prompt</span></span>
1.  <span data-ttu-id="5d3f3-104">Otevřete **příkazového řádku.**</span><span class="sxs-lookup"><span data-stu-id="5d3f3-104">Open **Command Prompt.**</span></span>
2.  <span data-ttu-id="5d3f3-105">Spustit [Spouštěč samostatné aktualizace Windows](https://support.microsoft.com/en-us/kb/934307) jak je uvedeno níže:</span><span class="sxs-lookup"><span data-stu-id="5d3f3-105">Run the [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) as shown below:</span></span>

<span data-ttu-id="5d3f3-106">V systému Windows Server 2012 R2 a Windows 8.1:</span><span class="sxs-lookup"><span data-stu-id="5d3f3-106">On Windows Server 2012 R2 and Windows 8.1:</span></span>
```powershell
wusa /uninstall /kb:3134758
```
<span data-ttu-id="5d3f3-107">V systému Windows Server 2012:</span><span class="sxs-lookup"><span data-stu-id="5d3f3-107">On Windows Server 2012:</span></span>
```powershell
wusa /uninstall /kb:3134759
```
<span data-ttu-id="5d3f3-108">Na Windows Server 2008 R2 SP1 a Windows 7 SP1:</span><span class="sxs-lookup"><span data-stu-id="5d3f3-108">On Windows Server 2008 R2 SP1 and Windows 7 SP1:</span></span>
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a><span data-ttu-id="5d3f3-109">Pomocí ovládacích panelů</span><span class="sxs-lookup"><span data-stu-id="5d3f3-109">Using Control Panel</span></span>
1.  <span data-ttu-id="5d3f3-110">Otevřete **ovládací panely.**</span><span class="sxs-lookup"><span data-stu-id="5d3f3-110">Open **Control Panel.**</span></span>
2.  <span data-ttu-id="5d3f3-111">Otevřete **programy**, pak otevřete **odinstalovat program.**</span><span class="sxs-lookup"><span data-stu-id="5d3f3-111">Open **Programs**, then open **Uninstall a program.**</span></span>
3.  <span data-ttu-id="5d3f3-112">Klikněte na tlačítko **zobrazit nainstalované aktualizace.**</span><span class="sxs-lookup"><span data-stu-id="5d3f3-112">Click **View installed updates.**</span></span>
4.  <span data-ttu-id="5d3f3-113">Vyberte **Windows Management Framework 5.0** ze seznamu nainstalovaných aktualizací.</span><span class="sxs-lookup"><span data-stu-id="5d3f3-113">Select **Windows Management Framework 5.0** from the list of installed updates.</span></span> <span data-ttu-id="5d3f3-114">To odpovídá *KB3134758*, *KB3134759*, nebo *KB3134760*.</span><span class="sxs-lookup"><span data-stu-id="5d3f3-114">This corresponds to *KB3134758*, *KB3134759*, or *KB3134760*.</span></span> <span data-ttu-id="5d3f3-115">Klikněte na tlačítko **odinstalovat.**</span><span class="sxs-lookup"><span data-stu-id="5d3f3-115">Click **Uninstall.**</span></span>


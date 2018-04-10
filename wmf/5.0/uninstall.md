---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 78ae7ecd40b4d8ad0a6750f43002986483ab18a7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="uninstallation-instructions"></a><span data-ttu-id="68b03-102">Odinstalace pokyny</span><span class="sxs-lookup"><span data-stu-id="68b03-102">Uninstallation Instructions</span></span>

## <a name="using-command-prompt"></a><span data-ttu-id="68b03-103">Pomocí příkazového řádku</span><span class="sxs-lookup"><span data-stu-id="68b03-103">Using Command Prompt</span></span>
1.  <span data-ttu-id="68b03-104">Otevřete **příkazového řádku.**</span><span class="sxs-lookup"><span data-stu-id="68b03-104">Open **Command Prompt.**</span></span>
2.  <span data-ttu-id="68b03-105">Spustit [Spouštěč samostatné aktualizace Windows](https://support.microsoft.com/en-us/kb/934307) jak je uvedeno níže:</span><span class="sxs-lookup"><span data-stu-id="68b03-105">Run the [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) as shown below:</span></span>

<span data-ttu-id="68b03-106">V systému Windows Server 2012 R2 a Windows 8.1:</span><span class="sxs-lookup"><span data-stu-id="68b03-106">On Windows Server 2012 R2 and Windows 8.1:</span></span>
```powershell
wusa /uninstall /kb:3134758
```
<span data-ttu-id="68b03-107">On Windows Server 2012:</span><span class="sxs-lookup"><span data-stu-id="68b03-107">On Windows Server 2012:</span></span>
```powershell
wusa /uninstall /kb:3134759
```
<span data-ttu-id="68b03-108">Na Windows Server 2008 R2 SP1 a Windows 7 SP1:</span><span class="sxs-lookup"><span data-stu-id="68b03-108">On Windows Server 2008 R2 SP1 and Windows 7 SP1:</span></span>
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a><span data-ttu-id="68b03-109">Pomocí ovládacích panelů</span><span class="sxs-lookup"><span data-stu-id="68b03-109">Using Control Panel</span></span>
1.  <span data-ttu-id="68b03-110">Otevřete **ovládací panely.**</span><span class="sxs-lookup"><span data-stu-id="68b03-110">Open **Control Panel.**</span></span>
2.  <span data-ttu-id="68b03-111">Otevřete **programy**, pak otevřete **odinstalovat program.**</span><span class="sxs-lookup"><span data-stu-id="68b03-111">Open **Programs**, then open **Uninstall a program.**</span></span>
3.  <span data-ttu-id="68b03-112">Klikněte na tlačítko **zobrazit nainstalované aktualizace.**</span><span class="sxs-lookup"><span data-stu-id="68b03-112">Click **View installed updates.**</span></span>
4.  <span data-ttu-id="68b03-113">Vyberte **Windows Management Framework 5.0** ze seznamu nainstalovaných aktualizací.</span><span class="sxs-lookup"><span data-stu-id="68b03-113">Select **Windows Management Framework 5.0** from the list of installed updates.</span></span> <span data-ttu-id="68b03-114">To odpovídá *KB3134758*, *KB3134759*, nebo *KB3134760*.</span><span class="sxs-lookup"><span data-stu-id="68b03-114">This corresponds to *KB3134758*, *KB3134759*, or *KB3134760*.</span></span> <span data-ttu-id="68b03-115">Klikněte na tlačítko **odinstalovat.**</span><span class="sxs-lookup"><span data-stu-id="68b03-115">Click **Uninstall.**</span></span>
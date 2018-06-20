---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: f491e30859cbe6cbaa58f94389382ff231c52956
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225687"
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="e59f3-102">Podporu modulů pro deklarování verze rozsahy (1.\* atd.)</span><span class="sxs-lookup"><span data-stu-id="e59f3-102">Modules support for declaring version ranges (1.\*, etc)</span></span>
<span data-ttu-id="e59f3-103">V kombinaci s **- MinimumVersion**, **- MaximumVersion** teď umožňuje uživateli get nebo importovat modul v rámci určitého rozsahu.</span><span class="sxs-lookup"><span data-stu-id="e59f3-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="e59f3-104">Parametr také podporují **.** \*.</span><span class="sxs-lookup"><span data-stu-id="e59f3-104">The parameter also support **.**\*.</span></span> <span data-ttu-id="e59f3-105">Následující příklad ukazuje, jak to funguje:</span><span class="sxs-lookup"><span data-stu-id="e59f3-105">The following example shows how it works:</span></span>

<span data-ttu-id="e59f3-106">Teď můžete kombinovat **- MinimumVersion** a **- MaximumVersion** k importu modulu v rámci určitého rozsahu:</span><span class="sxs-lookup"><span data-stu-id="e59f3-106">Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:</span></span>

```powershell
PS C:\> Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*

VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```

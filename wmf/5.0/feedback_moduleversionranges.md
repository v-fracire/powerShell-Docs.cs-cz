---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 89e908969641afd9ad9541dcfedcc8eb6315d07c
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/16/2018
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="eccad-102">Podporu modulů pro deklarování verze rozsahy (1.\* atd.)</span><span class="sxs-lookup"><span data-stu-id="eccad-102">Modules support for declaring version ranges (1.\*, etc)</span></span>
<span data-ttu-id="eccad-103">V kombinaci s **- MinimumVersion**, **- MaximumVersion** teď umožňuje uživateli get nebo importovat modul v rámci určitého rozsahu.</span><span class="sxs-lookup"><span data-stu-id="eccad-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="eccad-104">Parametr také podporují **.** \*.</span><span class="sxs-lookup"><span data-stu-id="eccad-104">The parameter also support **.**\*.</span></span> <span data-ttu-id="eccad-105">Následující příklad ukazuje, jak to funguje:</span><span class="sxs-lookup"><span data-stu-id="eccad-105">The following example shows how it works:</span></span>

<span data-ttu-id="eccad-106">Teď můžete kombinovat **- MinimumVersion** a **- MaximumVersion** k importu modulu v rámci určitého rozsahu:</span><span class="sxs-lookup"><span data-stu-id="eccad-106">Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:</span></span>

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

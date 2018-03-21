---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: fa972b68015d9b6e14508ccda562cfa5ebd632ac
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/20/2018
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="ec216-102">Podporu modulů pro deklarování verze rozsahy (1.\* atd.)</span><span class="sxs-lookup"><span data-stu-id="ec216-102">Modules support for declaring version ranges (1.\*, etc)</span></span>
<span data-ttu-id="ec216-103">V kombinaci s **- MinimumVersion**, **- MaximumVersion** teď umožňuje uživateli get nebo importovat modul v rámci určitého rozsahu.</span><span class="sxs-lookup"><span data-stu-id="ec216-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="ec216-104">Parametr také podporují **.**\*.</span><span class="sxs-lookup"><span data-stu-id="ec216-104">The parameter also support \*\*.\*\*\*.</span></span> <span data-ttu-id="ec216-105">Následující příklad ukazuje, jak to funguje:</span><span class="sxs-lookup"><span data-stu-id="ec216-105">The following example shows how it works:</span></span>

```powershell
Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:

PS C:\> Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*

VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```


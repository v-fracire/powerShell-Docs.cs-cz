---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 269f4112704067f291728e4c1d745d68ec6ccd6f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="register-a-powershell-repository"></a><span data-ttu-id="24ede-102">Registrace powershellového úložiště</span><span class="sxs-lookup"><span data-stu-id="24ede-102">Register a PowerShell Repository</span></span>
<span data-ttu-id="24ede-103">Můžete nakonfigurovat PowerShellGet pracovat s interní úložiště.</span><span class="sxs-lookup"><span data-stu-id="24ede-103">You can configure PowerShellGet to operate against internal repositories.</span></span> <span data-ttu-id="24ede-104">To se provádí pomocí těmito přídavky:</span><span class="sxs-lookup"><span data-stu-id="24ede-104">This is done by using the following additions:</span></span>
- <span data-ttu-id="24ede-105">Register-PSRepository: Zaregistruje úložiště pro aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="24ede-105">Register-PSRepository: Registers a repository for the current user.</span></span>
- <span data-ttu-id="24ede-106">Zrušit registraci PSRepository: Odebere registrované úložiště pro aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="24ede-106">Unregister-PSRepository: Removes a registered repository for the current user.</span></span>
- <span data-ttu-id="24ede-107">Set-PSRepository: Nastavte hodnoty pro registrované úložiště.</span><span class="sxs-lookup"><span data-stu-id="24ede-107">Set-PSRepository: Set values for a registered repository.</span></span>
- <span data-ttu-id="24ede-108">Get-PSRepository: Získání všech registrovaných úložišť pro aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="24ede-108">Get-PSRepository: Get all registered repositories for the current user.</span></span>

<span data-ttu-id="24ede-109">Po registraci úložiště můžete najít modul a nainstalujte modul s ním pracovat.</span><span class="sxs-lookup"><span data-stu-id="24ede-109">After a repository is registered, you can use Find-Module and Install-Module to work with it.</span></span>

```powershell
\#Register a default repository
Register-PSRepository –Name DemoRepo –SourceLocation “https://www.myget.org/F/powershellgetdemo/api/v2” –PublishLocation “<https://www.myget.org/F/powershellgetdemo/api/v2>/package” –InstallationPolicy –Trusted

\#Get all of the registered repositories
Get-PSRepository
Name SourceLocation
---- --------------
PSGallery https://msconfiggallery.cloudapp...
DemoRepo https://www.myget.org/F/powershe...

\#Search only the new repository for modules
Find-Module -Repository DemoRepo
Repository Version Name
---------- ------- ----
DemoRepo 1.0.1 xActiveDirectory
DemoRepo 1.1.1 SomeModule

\#By default, PowerShellGet operates against all registered repositories when none is specified. In this example, the “SomeModule” module is installed from the DemoRepo.
Install-Module SomeModule

\#Removing a repository
Unregister-PSRepository DemoRepo
```
---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 81ce13a082ad1d7a13ba5fd76a7595b55708f54e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="register-a-powershell-repository"></a>Zaregistrovat úložiště v prostředí PowerShell
Můžete nakonfigurovat PowerShellGet pracovat s interní úložiště. To se provádí pomocí těmito přídavky:
- Register-PSRepository: Zaregistruje úložiště pro aktuálního uživatele.
- Zrušit registraci PSRepository: Odebere registrované úložiště pro aktuálního uživatele.
- Set-PSRepository: Nastavte hodnoty pro registrované úložiště.
- Get-PSRepository: Získání všech registrovaných úložišť pro aktuálního uživatele.

Po registraci úložiště můžete najít modul a nainstalujte modul s ním pracovat.

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


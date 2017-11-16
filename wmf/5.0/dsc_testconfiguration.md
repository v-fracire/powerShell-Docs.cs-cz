---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: ce60b240045acf538edae1a08007971e538588ca
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a>Rutina test-DscConfiguration podporuje konfigurace odkazu

Rutina Test-DscConfiguration byla aktualizována umožňující testování požadované konfigurace stavu jednoho nebo více cílových uzlů tak, že zadáte odkaz na dokument konfigurace pro porovnání.

Následující nové sady parametrů v cestě zadané do pouze testu použít konfigurace DSC a nikdy použití každé konfiguraci na zadané cílové uzly. Stejně jako u počáteční DscConfiguration a ostatní rutiny DSC, název každé MOF slouží k určení cílový uzel pro otestovat konfiguraci na. 

```powershell
Test-DscConfiguration   [-Path] <string> 
                        [[-ComputerName] <string[]>] 
                        [-Credential <pscredential>] 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]

Test-DscConfiguration   [-Path] <string> 
                        -CimSession <CimSession[]> 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]
```

Následující nové sady parametr používat jeden konfigurace DSC a testovat jenom nikdy použití konfigurace na zadané cílové uzly. 

```powershell
Test-DscConfiguration   -ReferenceConfiguration <string> 
                        [[-ComputerName] <string[]>]
                        [-Credential <pscredential>] 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]

Test-DscConfiguration   -ReferenceConfiguration <string> 
                        -CimSession <CimSession[]> 
                        [-ThrottleLimit <int>] 
                        [-AsJob] 
                        [<CommonParameters>]
```


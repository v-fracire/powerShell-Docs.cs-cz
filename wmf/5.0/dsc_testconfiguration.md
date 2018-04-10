---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 18c1dab7412b8e9d31960507b612dd6cc56d31d5
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
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
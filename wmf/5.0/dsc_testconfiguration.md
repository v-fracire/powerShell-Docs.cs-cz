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
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a><span data-ttu-id="b4aca-102">Rutina test-DscConfiguration podporuje konfigurace odkazu</span><span class="sxs-lookup"><span data-stu-id="b4aca-102">Test-DscConfiguration cmdlet supports Reference Configurations</span></span>

<span data-ttu-id="b4aca-103">Rutina Test-DscConfiguration byla aktualizována umožňující testování požadované konfigurace stavu jednoho nebo více cílových uzlů tak, že zadáte odkaz na dokument konfigurace pro porovnání.</span><span class="sxs-lookup"><span data-stu-id="b4aca-103">The Test-DscConfiguration cmdlet has been updated to allow testing of desired configuration state of one or more target nodes by specifying a reference configuration document to compare against.</span></span>

<span data-ttu-id="b4aca-104">Následující nové sady parametrů v cestě zadané do pouze testu použít konfigurace DSC a nikdy použití každé konfiguraci na zadané cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="b4aca-104">The following new parameter sets use DSC configurations in the path specified to only test and never apply each configuration on the specified target node(s).</span></span> <span data-ttu-id="b4aca-105">Stejně jako u počáteční DscConfiguration a ostatní rutiny DSC, název každé MOF slouží k určení cílový uzel pro otestovat konfiguraci na.</span><span class="sxs-lookup"><span data-stu-id="b4aca-105">As with Start-DscConfiguration and other DSC cmdlets, the name of each MOF is used to determine which target node to test the configuration on.</span></span>

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

<span data-ttu-id="b4aca-106">Následující nové sady parametr používat jeden konfigurace DSC a testovat jenom nikdy použití konfigurace na zadané cílové uzly.</span><span class="sxs-lookup"><span data-stu-id="b4aca-106">The following new parameter sets use a single DSC configuration to only test and never apply the configuration on the specified target node(s).</span></span>

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
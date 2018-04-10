---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 27f8fab6a72e7f3a3f510f5a9e503bbfb8a8f618
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="on-demand-pull-of-dsc-configurations"></a><span data-ttu-id="57303-102">Načítání konfigurací DSC na vyžádání</span><span class="sxs-lookup"><span data-stu-id="57303-102">On-demand PULL of DSC Configurations</span></span>

<span data-ttu-id="57303-103">K dispozici novou rutinu Update-DscConfiguration aktivuje vyžádání obsahu z servery vyžádání definované v konfiguraci meta.</span><span class="sxs-lookup"><span data-stu-id="57303-103">The new Update-DscConfiguration cmdlet triggers a pull from the pull server(s) defined in the meta-configuration.</span></span> <span data-ttu-id="57303-104">Chování se často označuje jako pro vyžádání obsahu teď.</span><span class="sxs-lookup"><span data-stu-id="57303-104">The behavior is often referred to as 'Pull Now'.</span></span>


<span data-ttu-id="57303-105">Po aktivaci vyžádání se chová stejně jako by měla mít, když aktivuje během regulární frekvence:</span><span class="sxs-lookup"><span data-stu-id="57303-105">Once triggered, the pull behaves exactly the same as it would have when triggered during the regular frequency:</span></span>

1. <span data-ttu-id="57303-106">Kontrolní součet pro aktuální konfiguraci se porovnává se kontrolního součtu pro konfiguraci na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="57303-106">The checksum for current configuration is compared to the checksum for the configuration on the pull server.</span></span>
2. <span data-ttu-id="57303-107">Pokud jsou stejné, dokončí úspěšně bez použití konfigurace.</span><span class="sxs-lookup"><span data-stu-id="57303-107">If they are the same, it completes successfully without applying the configuration.</span></span>
3. <span data-ttu-id="57303-108">Pokud se liší, je konfigurace vyžádat z načítacího serveru a použít.</span><span class="sxs-lookup"><span data-stu-id="57303-108">If they are different, the configuration is pulled down from the pull server and applied.</span></span>

<span data-ttu-id="57303-109">**Poznámka:** Pokud Meta-konfigurace RefreshMode = "Push" Tato rutina je vrátila chybu, aby tato rutina bude vždy nic nestane. Pokud cílový uzel je v režimu "Push".</span><span class="sxs-lookup"><span data-stu-id="57303-109">**Note:** If the Meta-Configuration RefreshMode = 'Push' an error is returned by this cmdlet so this cmdlet will always do nothing when a target node is in 'Push' Mode.</span></span>

```powershell
Update-DscConfiguration     [[-ComputerName] <string[]>]
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-Credential<pscredential>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]

Update-DscConfiguration     -CimSession <CimSession[]>
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]
```
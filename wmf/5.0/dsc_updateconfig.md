---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: f2ddde78f436e6f03f521a9a8246dbda93e7a57a
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/27/2017
---
# <a name="on-demand-pull-of-dsc-configurations"></a><span data-ttu-id="f8d3f-102">Vyžádání obsahu na vyžádání konfigurací DSC</span><span class="sxs-lookup"><span data-stu-id="f8d3f-102">On-demand PULL of DSC Configurations</span></span>

<span data-ttu-id="f8d3f-103">K dispozici novou rutinu Update-DscConfiguration aktivuje vyžádání obsahu z servery vyžádání definované v konfiguraci meta.</span><span class="sxs-lookup"><span data-stu-id="f8d3f-103">The new Update-DscConfiguration cmdlet triggers a pull from the pull server(s) defined in the meta-configuration.</span></span> <span data-ttu-id="f8d3f-104">Chování se často označuje jako pro vyžádání obsahu teď.</span><span class="sxs-lookup"><span data-stu-id="f8d3f-104">The behavior is often referred to as 'Pull Now'.</span></span> 


<span data-ttu-id="f8d3f-105">Po aktivaci vyžádání se chová stejně jako by měla mít, když aktivuje během regulární frekvence:</span><span class="sxs-lookup"><span data-stu-id="f8d3f-105">Once triggered, the pull behaves exactly the same as it would have when triggered during the regular frequency:</span></span>

1. <span data-ttu-id="f8d3f-106">Kontrolní součet pro aktuální konfiguraci se porovnává se kontrolního součtu pro konfiguraci na tomto serveru.</span><span class="sxs-lookup"><span data-stu-id="f8d3f-106">The checksum for current configuration is compared to the checksum for the configuration on the pull server.</span></span> 
2. <span data-ttu-id="f8d3f-107">Pokud jsou stejné, dokončí úspěšně bez použití konfigurace.</span><span class="sxs-lookup"><span data-stu-id="f8d3f-107">If they are the same, it completes successfully without applying the configuration.</span></span> 
3. <span data-ttu-id="f8d3f-108">Pokud se liší, je konfigurace vyžádat z načítacího serveru a použít.</span><span class="sxs-lookup"><span data-stu-id="f8d3f-108">If they are different, the configuration is pulled down from the pull server and applied.</span></span>

<span data-ttu-id="f8d3f-109">**Poznámka:** Pokud Meta-konfigurace RefreshMode = "Push" Tato rutina je vrátila chybu, aby tato rutina bude vždy nic nestane. Pokud cílový uzel je v režimu "Push".</span><span class="sxs-lookup"><span data-stu-id="f8d3f-109">**Note:** If the Meta-Configuration RefreshMode = 'Push' an error is returned by this cmdlet so this cmdlet will always do nothing when a target node is in 'Push' Mode.</span></span>

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


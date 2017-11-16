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
# <a name="on-demand-pull-of-dsc-configurations"></a>Vyžádání obsahu na vyžádání konfigurací DSC

K dispozici novou rutinu Update-DscConfiguration aktivuje vyžádání obsahu z servery vyžádání definované v konfiguraci meta. Chování se často označuje jako pro vyžádání obsahu teď. 


Po aktivaci vyžádání se chová stejně jako by měla mít, když aktivuje během regulární frekvence:

1. Kontrolní součet pro aktuální konfiguraci se porovnává se kontrolního součtu pro konfiguraci na tomto serveru. 
2. Pokud jsou stejné, dokončí úspěšně bez použití konfigurace. 
3. Pokud se liší, je konfigurace vyžádat z načítacího serveru a použít.

**Poznámka:** Pokud Meta-konfigurace RefreshMode = "Push" Tato rutina je vrátila chybu, aby tato rutina bude vždy nic nestane. Pokud cílový uzel je v režimu "Push".

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


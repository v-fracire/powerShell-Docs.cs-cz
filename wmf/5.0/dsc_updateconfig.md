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
# <a name="on-demand-pull-of-dsc-configurations"></a>Načítání konfigurací DSC na vyžádání

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
---
ms.date: 2017-10-16
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Přijetí konfigurace"
ms.openlocfilehash: 4285dbe04c9745ec2a859e479848da2881c18de0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="enacting-configurations"></a>Přijetí konfigurace

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Existují dva způsoby, jak uplatní požadovaného stavu konfigurace (konfiguracích DSC Powershellu): push režim a režim vyžádání obsahu.

## <a name="push-mode"></a>Push režimu

![Režim push](images/pushModel.png "jak funguje režim push")

Režim push odkazuje na uživatele aktivně použití konfigurace na cílový uzel voláním [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny.

Po vytváření a kompilování konfigurace, můžete můžete uplatní je v režimu nabízení voláním [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny nastavení parametr - Path rutiny na cestu, kde se nachází v konfiguraci MOF.
Například, pokud se nachází v konfiguraci MOF `C:\DSC\Configurations\localhost.mof`, by ho použít k místnímu počítači pomocí následujícího příkazu:`Start-DscConfiguration -Path 'C:\DSC\Configurations'`

> __Poznámka:__: ve výchozím nastavení spouští DSC konfigurace jako úlohu na pozadí. Konfigurace běžet interaktivně, volání [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) s __-počkejte__ parametr.

## <a name="pull-mode"></a>Režim pro vyžádání obsahu

![Režim pro vyžádání obsahu](images/pullModel.png "vyžádané funguje režim")

V režimu pro vyžádání obsahu klienti vyžádání obsahu umožňují získat jejich požadovaný stav konfigurace ze služby vzdálené vyžádání obsahu.
Podobně služba vyžádání obsahu je nastaven pro hostitele DSC služby a zřízená s prostředky, které jsou vyžadovány klienty pro vyžádání obsahu a konfigurace.
Každý z klientů vyžádání obsahu má plánovaná událost, která provádí kontrolu pravidelné dodržování předpisů v konfiguraci uzlu.
Při prvním je aktivována událost, místní Configuration Manager (LCM) na vyžádání klient odešle požadavek službu vyžádání obsahu a získat konfiguraci zadanou v LCM.
Pokud tato konfigurace existuje ve službě vyžádání obsahu a předává počáteční ověřovacích kontrol, konfigurace se stáhne do klienta vyžádání obsahu, kde je pak provést pomocí LCM.

LCM ověří, že klient je v souladu s konfigurací v pravidelných intervalech určeného **ConfigurationModeFrequencyMins** vlastnost LCM.
LCM vyhledává aktualizované konfigurace ve službě vyžádání obsahu v pravidelných intervalech určeného **RefreshModeFrequency** vlastnost LCM.
Informace o konfiguraci LCM najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md).

Doporučené řešení pro hostování služby pro vyžádání obsahu, je Cloudová služba DSC, [Azure Automation](https://azure.microsoft.com/en-us/services/automation/).
To je hostovaná řešení poskytuje správu grafického rozhraní, vytváření sestav a centralizovanou správu.

Další informace o nastavení vyžadování služby v systému Windows Server najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).
Porozumět však, že tato implementace má omezené funkce a nevyžaduje některé integrace "provést sami".

Následující témata popisují vyžádání služby a klienti:

- [Přehled služby Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [Nastavení vyžadování serveru SMB](pullServerSMB.md)
- [Konfigurace klienta vyžádání obsahu](pullClientConfigID.md)

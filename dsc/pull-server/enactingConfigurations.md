---
ms.date: 10/16/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Přijetí konfigurace
ms.openlocfilehash: 4a6e7e511446ab27307683ad3d5676391e7c791c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404041"
---
# <a name="enacting-configurations"></a>Přijetí konfigurace

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Existují dva způsoby, jak přijmout konfigurace prostředí PowerShell Desired State Configuration (DSC): push a pull režimu.

## <a name="push-mode"></a>Režim nabízených oznámení

![Režimu nabízení](../images/pushModel.png "nabízená replikace funguje režim")

Režimu nabízení odkazuje na uživatele aktivně použití konfigurace k cílovému uzlu voláním [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.

Po vytvoření a kompilace konfigurace, je můžete přijmout ho v režimu nabízení voláním [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny nastavení parametr - Path rutiny na cestu, kde se nachází konfigurační soubor MOF.
Například, pokud se nachází v konfiguraci MOF `C:\DSC\Configurations\localhost.mof`, by ho použít v místním počítači pomocí následujícího příkazu: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`

> __Poznámka:__: Ve výchozím nastavení spouští DSC konfigurace jako úlohu na pozadí. Chcete-li spustit konfiguraci interaktivně, zavolejte [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) s __– počkejte__ parametru.

## <a name="pull-mode"></a>Režim načítání

![Režim načítání](../images/pullModel.png "vyžádané funguje režim")

V režimu o přijetí změn jsou o přijetí změn klienti nakonfigurováni na získání jejich konfigurace požadovaného stavu ze služby vzdálené o přijetí změn.
Podobně službu přijetí změn je nastavený na hostitele DSC služby a zřízení s konfigurací a prostředků, které jsou vyžadovány klienty o přijetí změn.
Každá z klientů o přijetí změn obsahuje naplánované události, která provádí kontrolu dodržování předpisů pravidelné konfigurace uzlu.
Když událost se aktivuje poprvé, místní Configuration Manageru (LCM) na straně klienta o přijetí změn učiní žádost vůči službě o přijetí změn a získat konfiguraci zadanou v LCM.
Pokud tuto konfiguraci existuje ve službě o přijetí změn, a předá počáteční ověřovacích kontrol, konfigurace se stáhne do klienta o přijetí změn, kde ji potom provádí LCM.

LCM kontroluje, zda klient je v souladu s konfigurací v pravidelných intervalech, které jsou určené **ConfigurationModeFrequencyMins** vlastnost LCM.
LCM kontroluje aktualizace konfigurace na službu přijetí změn v pravidelných intervalech, které jsou určené **RefreshModeFrequency** vlastnost LCM.
Informace o konfiguraci LCM najdete v tématu [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md).

Doporučené řešení pro hostování služby o přijetí změn, je Cloudová služba DSC, [Azure Automation](https://azure.microsoft.com/services/automation/).
To je hostované řešení poskytuje správu grafického rozhraní, vytváření sestav a centralizovanou správu.

Další informace o nastavení služby o přijetí změn ve Windows serveru najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).
Seznamte se však, že tato implementace má omezené funkce a potřebuje k fungování integraci některé "to sami".

Následující témata popisují službu přijetí změn a klienti:

- [Přehled Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [Nastavení serveru vyžádané replikace SMB](pullServerSMB.md)
- [Konfigurace načítacího klienta](pullClientConfigID.md)

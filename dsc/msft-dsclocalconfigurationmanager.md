---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "MSFT_DSCLocalConfigurationManager – třída"
ms.openlocfilehash: b2d2ce000988f2c10ab04c4ba5a4650bd3c75ec7
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="msftdsclocalconfigurationmanager-class"></a>MSFT_DSCLocalConfigurationManager – třída

Místní Configuration Manager (LCM), které řídí stavy konfigurace soubory a používá konfiguraci agenta použít konfiguraci.

Následující syntaxe je jednodušší z kódu formátu MOF (Managed Object) a zahrnuje všechny zděděné vlastnosti.

## <a name="syntax"></a>Syntaxe
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a>Členové
-------

**MSFT_DSCLocalConfigurationManager** třída má následující členy:

-   [Metody] []

### <a name="methods"></a>Metody

**MSFT_DSCLocalConfigurationManager** třída má tyto metody.

|Metoda |Popis |
|:--- |:---|
| [ApplyConfiguration](msft-dsclocalconfigurationmanager-applyconfiguration.md)| Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.| 
| [DisableDebugConfiguration](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| Zakáže ladění prostředků DSC.| 
| [EnableDebugConfiguration](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| Povolí ladění na prostředek DSC.| 
| [Getconfiguration –](msft-dsclocalconfigurationmanager-getconfiguration.md)| Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.| 
| [GetConfigurationResultOutput](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| Získá výstup Agent konfigurace týkající se určité úlohy.| 
| [GetConfigurationStatus](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| Načtení historie stav konfigurace.| 
| [GetMetaConfiguration](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| Získá LCM nastavení, která slouží k řízení konfigurace agenta.| 
| [PerformRequiredConfigurationChecks](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| Spustí kontrolu konzistence.| 
| [RemoveConfiguration](msft-dsclocalconfigurationmanager-removeconfiguration.md)| Odebere konfigurační soubory.| 
| [ResourceGet](msft-dsclocalconfigurationmanager-resourceget.md)| Volá přímo **získat** metoda prostředek DSC.| 
| [ResourceSet](msft-dsclocalconfigurationmanager-resourceset.md)| Volá přímo **nastavit** metoda prostředek DSC.| 
| [ResourceTest](msft-dsclocalconfigurationmanager-resourcetest.md)| Volá přímo **Test** metoda prostředek DSC.| 
| [RollBack](msft-dsclocalconfigurationmanager-rollback.md)| Zobrazí souhrn zpět na předchozí konfiguraci.| 
| [SendConfiguration](msft-dsclocalconfigurationmanager-sendconfiguration.md)| Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.| 
| [SendConfigurationApply](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.| 
| [SendConfigurationApplyAsync](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| Poslat spravovaný uzel dokumentu konfigurace a spustí pomocí konfigurace agenta pro použití v konfiguraci. Pomocí GetConfigurationResultOutput načíst výstup výsledků.| 
| [SendMetaConfigurationApply](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| Nastaví LCM nastavení, která slouží k řízení konfigurace agenta.| 
| [StopConfiguration](msft-dsclocalconfigurationmanager-stopconfiguration.md)| Zastaví konfiguraci, která je v průběhu.| 
| [TestConfiguration](msft-dsclocalconfigurationmanager-testconfiguration.md)| Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.| 



 

## <a name="requirements"></a>Požadavky
------------
>**MOF:** DscCore.mof

>**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration



 

 




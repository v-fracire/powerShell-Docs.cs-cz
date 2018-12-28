---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Třída MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 7f6aaf209601e99b0120407eb301d32fcfda9eb8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403817"
---
# <a name="msftdsclocalconfigurationmanager-class"></a>Třída MSFT_DSCLocalConfigurationManager

Místní Configuration Manageru (LCM), který řídí stavy konfigurační soubory a používá konfiguraci agenta použít konfigurace.

Následující syntaxe je zjednodušená z kódu formátu MOF (Managed Object) a zahrnuje všechny zděděné vlastnosti.

## <a name="syntax"></a>Syntaxe

```
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## <a name="members"></a>Členové

**MSFT_DSCLocalConfigurationManager** třída má následující členy:

- [Metody] []

### <a name="methods"></a>Metody

**MSFT_DSCLocalConfigurationManager** třída má tyto metody.

|Metoda |Popis |
|:--- |:---|
| [Třída ApplyConfiguration](msft-dsclocalconfigurationmanager-applyconfiguration.md)| Pomocí agenta konfigurace použije konfiguraci, která čeká na vyřízení.|
| [DisableDebugConfiguration](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| Zakáže ladění prostředků DSC.|
| [EnableDebugConfiguration](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| Povolí ladění prostředků DSC.|
| [GetConfiguration](msft-dsclocalconfigurationmanager-getconfiguration.md)| Odešle dokument konfigurace spravovaných uzlů a používá **získat** metody konfigurace agenta použít danou konfiguraci.|
| [GetConfigurationResultOutput](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| Získá výstup agenta konfigurace týkající se určité úlohy.|
| [GetConfigurationStatus](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| Zobrazit historii stavu konfigurace.|
| [GetMetaConfiguration](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| Získá LCM nastavení, které se používají k řízení konfigurace agenta.|
| [PerformRequiredConfigurationChecks](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| Spustí kontrolu konzistence.|
| [RemoveConfiguration](msft-dsclocalconfigurationmanager-removeconfiguration.md)| Odstraní konfigurační soubory.|
| [ResourceGet](msft-dsclocalconfigurationmanager-resourceget.md)| Volá přímo **získat** metoda prostředek DSC.|
| [ResourceSet](msft-dsclocalconfigurationmanager-resourceset.md)| Volá přímo **nastavit** metoda prostředek DSC.|
| [ResourceTest](msft-dsclocalconfigurationmanager-resourcetest.md)| Volá přímo **Test** metoda prostředek DSC.|
| [Vrácení zpět](msft-dsclocalconfigurationmanager-rollback.md)| Zobrazí souhrn po zpět předchozí konfiguraci.|
| [SendConfiguration](msft-dsclocalconfigurationmanager-sendconfiguration.md)| Odešle dokument konfigurace spravovaných uzlů a uloží ho jako nedokončená změna.|
| [SendConfigurationApply](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| Odešle dokument konfigurace spravovaných uzlů a použít danou konfiguraci pomocí konfigurace agenta.|
| [SendConfigurationApplyAsync](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| Poslat dokument konfigurace spravovaných uzlů a začnete používat konfigurace agenta pro použití konfigurace. Použijte GetConfigurationResultOutput k načtení výsledků výstupu.|
| [SendMetaConfigurationApply](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| Nastaví LCM nastavení, které se používají k řízení konfigurace agenta.|
| [StopConfiguration](msft-dsclocalconfigurationmanager-stopconfiguration.md)| Zastaví probíhající konfigurace.|
| [TestConfiguration](msft-dsclocalconfigurationmanager-testconfiguration.md)| Odešle dokument konfigurace spravovaných uzlů a ověří aktuální konfiguraci proti dokumentu.|

## <a name="requirements"></a>Požadavky

**SOUBOR MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration
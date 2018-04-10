---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 9cc4384088fcc39b09979b8ae4d023fc46307b13
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager

Spustí kontrolu konzistence pomocí plánovače úloh.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a>Parameters
----------

*Příznaky* \[v\] bitová maska, která určuje typ spuštění kontroly konzistence. Následující hodnoty jsou platné a mohou být kombinovány s použitím bitové **nebo** operace:

|Hodnota |Popis |
|:--- |:---|
|**1** | Kontrola konzistence normální. |
|**2** | Pokračování kontrolu konzistence po restartu systému. Tato hodnota by neměla kombinovat s další hodnoty. |
|**4** | Konfigurace by měl být vyžádány z načítacího serveru zadaný v metakonfiguraci pro uzel. Tato hodnota by měla vždycky kombinovat s **1**, pro hodnotu **5**. |
|**8** | Stav odeslat na server sestav. |

## <a name="return-value"></a>Návratová hodnota
------------

Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Jde o statickou metodu.

## <a name="requirements"></a>Požadavky
------------
>**MOF:** DscCore.mof

>**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration


## <a name="see-also"></a>Viz taky


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
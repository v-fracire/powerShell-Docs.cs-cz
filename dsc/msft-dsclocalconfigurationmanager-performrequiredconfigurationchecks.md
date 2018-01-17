---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda PerformRequiredConfigurationChecks MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 687c92f2dac5e8855731713e81390ac67615231e
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda PerformRequiredConfigurationChecks MSFT_DSCLocalConfigurationManager třídy

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

*Příznaky* \[v\]  
Bitová maska, která určuje typ spuštění kontroly konzistence. Následující hodnoty jsou platné a mohou být kombinovány s použitím bitové **nebo** operace:

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


 

 




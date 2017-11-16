---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda PerformRequiredConfigurationChecks MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 26110b3920104da7343b8d55cf63440c12accbbc
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
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


 

 




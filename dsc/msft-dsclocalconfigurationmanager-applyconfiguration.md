---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 2844e354e0d054b13b92267ce314536d88a1c33e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager

Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.

Pokud není žádná konfigurace čekající na vyřízení, tato metoda znovu použije aktuální konfiguraci.


## <a name="syntax"></a>Syntaxe
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a>Parameters
----------

*Vynutit* \[v\] Pokud je to **true**, aktuální konfiguraci se znovu použije, i když je v konfiguraci čekající na vyřízení.

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
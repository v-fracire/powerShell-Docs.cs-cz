---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ApplyConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 72fbedf30e5058d8003ed620400d6b443d50dff6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda ApplyConfiguration MSFT_DSCLocalConfigurationManager třídy

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

*Vynutit* \[v\]  
Pokud je to **true**, aktuální konfiguraci se znovu použije, i když je v konfiguraci čekající na vyřízení.

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

 

 




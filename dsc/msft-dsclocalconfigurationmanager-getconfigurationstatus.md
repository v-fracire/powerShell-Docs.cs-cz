---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda GetConfigurationStatus MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: a41e7a15fc935c2cd5fd4cb66d0ab13509d5d4e0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfigurationStatus MSFT_DSCLocalConfigurationManager třídy

Načtení historie stav konfigurace.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a>Parameters
----------

*Všechny* \[v\]  
**Hodnota TRUE,** Pokud tato metoda by měla vrátit informace o všech konfigurace běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.

*configurationStatus* \[out\]  
Při návratu, obsahuje vložené instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.

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


 

 




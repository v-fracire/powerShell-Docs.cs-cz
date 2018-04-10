---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: dde4ac003b346018561481e05ca7374475f9ff1d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager

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

*Všechny* \[v\] **true** Pokud tato metoda by měla vrátit informace o všech konfigurace běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.

*configurationStatus* \[out\] na vrátí, obsahuje vložené instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.

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
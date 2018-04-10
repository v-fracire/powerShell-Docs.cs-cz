---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 07d7db9dcc4288e6b72d5df37d82e44eb6f72ad2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager

Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a>Parameters
----------

*configurationData* \[v\] Určuje konfigurační data k odeslání.

*konfigurace* \[out\] na vrátí, obsahuje vložené instance konfigurace.

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
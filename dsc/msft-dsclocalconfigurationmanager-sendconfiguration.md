---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 07ae48dd456e68be4ad0b09127ba9801359fd101
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda SendConfiguration třídy MSFT_DSCLocalConfigurationManager

Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a>Parameters
----------

*ConfigurationData* \[v\] data prostředí pro konfiguraci.

*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.

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
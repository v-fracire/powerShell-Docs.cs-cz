---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda SendConfigurationApply MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 20f732d35860cccde4e507dc6916e27d0cf8c5f6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda SendConfigurationApply MSFT_DSCLocalConfigurationManager třídy

Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a>Parameters
----------

*ConfigurationData* \[v\]  
Data prostředí pro konfiguraci.

*Vynutit* \[v\]  
**Hodnota TRUE,** vynutit konfiguraci zastavit.

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


 

 




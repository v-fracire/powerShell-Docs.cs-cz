---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda SendConfigurationApplyAsync MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: e680bfd1c5b39d364c90cf5ef6b43d0a568af23a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda SendConfigurationApplyAsync MSFT_DSCLocalConfigurationManager třídy

Asynchronně odešle dokumentu konfigurace na spravovaných uzel a používá Agent konfigurace můžete použít konfiguraci.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a>Parameters
----------

*ConfigurationData* \[v\]  
Data prostředí pro konfiguraci.

*Vynutit* \[v\]  
**Hodnota TRUE,** vynutit konfiguraci zastavit.

*jobId* \[v\]  
ID úlohy, pro které chcete odeslat konfiguraci.

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


 

 




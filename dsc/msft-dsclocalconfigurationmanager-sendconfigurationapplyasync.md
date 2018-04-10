---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 7ff821a277a548869862741551ee9897e417ea45
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager

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

*ConfigurationData* \[v\] data prostředí pro konfiguraci.

*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.

*jobId* \[v\] ID úlohy, pro které chcete odeslat konfiguraci.

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
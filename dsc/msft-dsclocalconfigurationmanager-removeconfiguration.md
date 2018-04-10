---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: e0ae8a50212b70841d210d7b2d666a2855218d1a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager

Odebere konfigurační soubory.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a>Parameters
----------

*Fáze* \[v\] Určuje, který dokument konfigurace odebrat. Platné jsou následující hodnoty:

|Hodnota |Popis |
|:--- |:---|
|**1** | **Aktuální** dokumentu konfigurace (current.mof). |
|**2** | **Čekající** dokumentu konfigurace (pending.mof).  |
|**4** | **Předchozí** dokumentu konfigurace (previous.mof). |

*Vynutit* \[v\] **true** vynutit odebrání konfigurace.

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
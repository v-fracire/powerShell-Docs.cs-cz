---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda RemoveConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: faa113c442b80eea3ac474220b098b7d80ec50a8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda RemoveConfiguration MSFT_DSCLocalConfigurationManager třídy

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

*Fáze* \[v\]  
Určuje, který dokument konfigurace odebrat. Platné jsou následující hodnoty:

|Hodnota |Popis |
|:--- |:---|
|**1** | **Aktuální** dokumentu konfigurace (current.mof). |
|**2** | **Čekající** dokumentu konfigurace (pending.mof).  |
|**4** | **Předchozí** dokumentu konfigurace (previous.mof). |

*Platnost* \[v\]  
**Hodnota TRUE,** vynutit odebrání konfigurace.

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


 

 




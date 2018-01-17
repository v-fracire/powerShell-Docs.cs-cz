---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda RemoveConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: fed45836293adedbce18f01cfe53cdfa1a474975
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
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


 

 




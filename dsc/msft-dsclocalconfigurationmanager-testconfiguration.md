---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda TestConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 04f0f3146473dc71f492086449d9dce5467c55db
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda TestConfiguration MSFT_DSCLocalConfigurationManager třídy

Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a>Parameters
----------

*configurationData* \[v\]  
Data confuguration prostředí.

*InDesiredState* \[out\]  
Při návratu Určuje, zda spravovaný uzel je ve stavu určeného dokumentu konfigurace.

*ResourcesInDesiredState* \[out\]  
Při návratu, obsahuje vložené instance **MSFT_ResourceInDesiredState** třídu, která určuje prostředky, které jsou v požadovaném stavu.

*ResourcesNotInDesiredState* \[out\]  
Při návratu, obsahuje vložené instance **MSFT_ResourceNotInDesiredState** třídu, která určuje prostředky, které nejsou v požadovaném stavu.

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


 

 




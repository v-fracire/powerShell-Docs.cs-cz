---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 7d8b185c49778253dcb4e983ad948775c4cb0842
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy

Volá přímo **získat** metoda prostředek DSC.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a>Parameters
----------

*Typ prostředku* \[v\]  
Název prostředku k volání.

*Název modulu* \[v\]  
Název modulu, který obsahuje prostředek k volání.

*resourceProperty* \[v\]  
Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí. Použití [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.

*konfigurace* \[out\]  
Při návratu obsahuje vložené instance konfigurace.

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


 

 




---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ResourceSet MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 7291641098578226449f8cbd360da0a3f9842598
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda ResourceSet MSFT_DSCLocalConfigurationManager třídy

Volá přímo **nastavit** metoda prostředek DSC.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a>Parameters
----------

*Typ prostředku* \[v\]  
Název prostředku k volání.

*ModuleName* \[in\]  
Název modulu, který obsahuje prostředek k volání.

*resourceProperty* \[v\]  
Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí. Použití [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.

*RebootRequired* \[out\]  
Při návratu, je tato vlastnost nastavená na **true** Pokud je potřeba restartovat cílový uzel.

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

 

 




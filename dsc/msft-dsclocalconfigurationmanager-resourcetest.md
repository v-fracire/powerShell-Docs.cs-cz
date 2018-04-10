---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda ResourceTest třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: f03a034329a9cde5cd44dbaf42ba1789c2b8f4f9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda ResourceTest třídy MSFT_DSCLocalConfigurationManager

Volá přímo **Test** metoda prostředek DSC.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a>Parameters
----------

*Typ prostředku* \[v\] název prostředku k volání.

*Název modulu* \[v\] název modul, který obsahuje prostředek, který volání.

*resourceProperty* \[v\] Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí. Použití [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.

*InDesiredState* \[out\] na vrátit, je tato vlastnost nastavená na **true** Pokud cílový uzel je v požadovaném stavu.

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
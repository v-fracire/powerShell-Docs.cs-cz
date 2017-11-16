---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda vrácení zpět MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: b8597e3eb7872d9894863fb02d927c9f475da44c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda vrácení zpět MSFT_DSCLocalConfigurationManager třídy

Vrátí konfiguraci zpět na předchozí verzi.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a>Parameters
----------

*configurationNumber* \[v\]  
Určuje požadovanou konfiguraci. 

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


 

 




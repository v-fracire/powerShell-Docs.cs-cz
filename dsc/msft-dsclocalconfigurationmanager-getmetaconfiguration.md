---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda GetMetaConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 4f209014e9fde5841a9bce743f5364e6677d1e41
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetMetaConfiguration MSFT_DSCLocalConfigurationManager třídy

Získá místní nastavení nástroje Configuration Manager, která slouží k řízení konfigurace agenta.

<a name="syntax"></a>Syntaxe
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a>Parameters
----------

*Metakonfiguraci* \[out\]  
Při návratu, obsahuje vložené instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.

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


 

 




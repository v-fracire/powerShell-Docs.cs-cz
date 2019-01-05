---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048207"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager

Odešle dokument konfigurace spravovaných uzlů a používá **získat** metody konfigurace agenta použít danou konfiguraci.

## <a name="syntax"></a>Syntaxe

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a>Parametry

*configurationData* \[v\] konfigurační data určená k odeslání.

*konfigurace* \[si\] na vrátit, obsahuje vložený instance konfigurace.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**SOUBOR MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz také

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892538"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager

Odešle dokument konfigurace spravovaných uzlů a používá **získat** metody konfigurace agenta použít danou konfiguraci.

## <a name="syntax"></a>Syntaxe

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a>Parameters

*configurationData* \[v\] konfigurační data určená k odeslání.

*konfigurace* \[si\] na vrátit, obsahuje vložený instance konfigurace.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**Soubor MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz taky

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
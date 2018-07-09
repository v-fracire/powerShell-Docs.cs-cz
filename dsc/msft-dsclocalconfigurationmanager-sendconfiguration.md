---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda SendConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 3529bc56ecba19ed0fbbf070a4e86d0692824d39
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892439"
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda SendConfiguration třídy MSFT_DSCLocalConfigurationManager

Odešle dokument konfigurace spravovaných uzlů a uloží ho jako nedokončená změna.

## <a name="syntax"></a>Syntaxe

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a>Parameters

*ConfigurationData* \[v\] dat prostředí pro konfiguraci.

*Vynutit* \[v\] **true** vynutit konfiguraci tak, aby zastavit.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**Soubor MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz taky

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
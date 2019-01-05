---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: d746832b01310f43a7aae33dd0fa70c0928bb3e0
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048125"
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager

Odešle dokument konfigurace spravovaných uzlů a ověří aktuální konfiguraci proti dokumentu.

## <a name="syntax"></a>Syntaxe

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

## <a name="parameters"></a>Parametry

*configurationData* \[v\] dat prostředí pro confuguration.

*InDesiredState* \[si\] na vrátit, určuje, zda spravovaných uzlů je ve stavu určené dokument konfigurace.

*ResourcesInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceInDesiredState** třída, která určuje prostředky, které jsou v požadovaném stavu.

*ResourcesNotInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceNotInDesiredState** třída, která určuje prostředky, které nejsou v požadovaném stavu.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**SOUBOR MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz také

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
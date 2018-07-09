---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: d746832b01310f43a7aae33dd0fa70c0928bb3e0
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893922"
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager

Odešle dokument konfigurace spravovaných uzlů a ověří aktuální konfiguraci proti dokumentu.

## <a name="syntax"></a>Syntaxe

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

## <a name="parameters"></a>Parameters

*configurationData* \[v\] dat prostředí pro confuguration.

*InDesiredState* \[si\] na vrátit, určuje, zda spravovaných uzlů je ve stavu určené dokument konfigurace.

*ResourcesInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceInDesiredState** třída, která určuje prostředky, které jsou v požadovaném stavu.

*ResourcesNotInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceNotInDesiredState** třída, která určuje prostředky, které nejsou v požadovaném stavu.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**Soubor MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz taky

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
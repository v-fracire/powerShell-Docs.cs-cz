---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: c66ccc4eefaef2d0c3a68fa8a96c5abb9bda6e4c
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893055"
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager

Zobrazit historii stavu konfigurace.

## <a name="syntax"></a>Syntaxe

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

## <a name="parameters"></a>Parameters

*Všechny* \[v\] **true** Pokud tato metoda by měla vrátit informace o všech konfiguraci běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.

*configurationStatus* \[si\] na vrátit, obsahuje vložený instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**Soubor MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz taky

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
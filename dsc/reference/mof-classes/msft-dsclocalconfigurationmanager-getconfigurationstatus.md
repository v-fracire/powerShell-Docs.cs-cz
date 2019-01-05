---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: c66ccc4eefaef2d0c3a68fa8a96c5abb9bda6e4c
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048165"
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfigurationStatus třídy MSFT_DSCLocalConfigurationManager

Zobrazit historii stavu konfigurace.

## <a name="syntax"></a>Syntaxe

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

## <a name="parameters"></a>Parametry

*Všechny* \[v\] **true** Pokud tato metoda by měla vrátit informace o všech konfiguraci běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.

*configurationStatus* \[si\] na vrátit, obsahuje vložený instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**SOUBOR MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz také

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
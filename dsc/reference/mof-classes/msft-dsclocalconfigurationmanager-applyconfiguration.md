---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 559ff1793a18e28dad2f176bdb20eb53bc08630d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048110"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager

Pomocí agenta konfigurace použije konfiguraci, která čeká na vyřízení.

Pokud není žádná konfigurace čekající, tato metoda znovu použije aktuální konfiguraci.

## <a name="syntax"></a>Syntaxe

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a>Parametry

*Vynutit* \[v\] Pokud je to **true**, aktuální konfigurace je znovu použita, i v případě konfigurace čekající.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**SOUBOR MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz také

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 03555cc73da1272bdebebc3d93b26aaf8fabc18e
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048150"
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager

Odstraní konfigurační soubory.

## <a name="syntax"></a>Syntaxe

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

## <a name="parameters"></a>Parametry

*Fáze* \[v\] Určuje, který dokument konfigurace odebrat. Platné jsou následující hodnoty:

|Hodnota |Popis |
|:--- |:---|
|**1** | **Aktuální** konfiguračního dokumentu (current.mof). |
|**2** | **Čekající** konfiguračního dokumentu (pending.mof).  |
|**4** | **Předchozí** konfiguračního dokumentu (previous.mof). |

*Vynutit* \[v\] **true** k vynucení odebrání konfigurace.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**SOUBOR MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz také

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
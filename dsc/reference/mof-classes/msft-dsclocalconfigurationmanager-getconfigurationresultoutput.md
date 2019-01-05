---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ea572a4a66befd4e4b8d83e2957632b1b5ed7d93
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048124"
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager

Získá konfiguraci agenta výstup přidružené k určité úlohy.

## <a name="syntax"></a>Syntaxe

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

## <a name="parameters"></a>Parametry

*jobId* \[v\] ID úlohy, pro který má být získána výstupní data.

*resumeOutputBookmark* \[v\] Určuje, že výstup by měl být pokračování z předchozí záložku.

*výstup* \[si\] výstup pro zadanou úlohu.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**SOUBOR MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz také

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
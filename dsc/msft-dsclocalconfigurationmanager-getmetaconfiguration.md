---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: e14237ef68b95d68e2f14071aa1fa6ba0717f39f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892837"
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager

Získá místní nastavení nástroje Configuration Manager, které se používají k řízení konfigurace agenta.

## <a name="syntax"></a>Syntaxe

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

## <a name="parameters"></a>Parameters

*MetaConfiguration* \[si\] na vrátit, obsahuje vložený instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.

## <a name="return-value"></a>Návratová hodnota

Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.

## <a name="remarks"></a>Poznámky

Toto je statické metody.

## <a name="requirements"></a>Požadavky

**Soubor MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Viz taky

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
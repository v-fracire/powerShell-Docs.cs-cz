---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: Příklad šablony o známý problém nebo omezení průpis
ms.openlocfilehash: cecf31127aaa1942471877a2056230ab592bd095
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
>Poznámka: Zadejte navrhovaný popisný název a stručný popis

## <a name="example-erroneous-executionpolicy-errors"></a>Příklad: Chybné ExecutionPolicy chyby ##
Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.

### <a name="resolution"></a>Řešení

Chcete-li vyřešit, nastavte **ExecutionPolicy** k **RemoteSigned** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):

```powershell
Set-ExecutionPolicy RemoteSigned
```
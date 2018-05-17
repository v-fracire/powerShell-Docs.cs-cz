---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.topic: conceptual
title: Příklad šablony o známý problém nebo omezení průpis
ms.openlocfilehash: 453d4e40b906ebcab7314f04e138ded271338846
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
>Poznámka: Zadejte navrhovaný popisný název a stručný popis

## <a name="example-erroneous-executionpolicy-errors"></a>Příklad: Chybné ExecutionPolicy chyby ##
Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.

### <a name="resolution"></a>Řešení

Chcete-li vyřešit, nastavte **ExecutionPolicy** k **RemoteSigned** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):

```powershell
Set-ExecutionPolicy RemoteSigned
```

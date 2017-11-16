---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
title: "Příklad šablony o známý problém nebo omezení průpis"
ms.openlocfilehash: b93393b2c84e76a301e6406d1388e82e95a2959c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
>Poznámka: Zadejte navrhovaný popisný název a stručný popis

## <a name="example-erroneous-executionpolicy-errors"></a>Příklad: Chybné ExecutionPolicy chyby ##
Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.

### <a name="resolution"></a>Řešení

Chcete-li vyřešit, nastavte **ExecutionPolicy** k **RemoteSigned** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):

```powershell
Set-ExecutionPolicy RemoteSigned
```


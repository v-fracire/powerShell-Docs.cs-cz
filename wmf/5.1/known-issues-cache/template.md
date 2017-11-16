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
><span data-ttu-id="03973-103">Poznámka: Zadejte navrhovaný popisný název a stručný popis</span><span class="sxs-lookup"><span data-stu-id="03973-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="03973-104">Příklad: Chybné ExecutionPolicy chyby</span><span class="sxs-lookup"><span data-stu-id="03973-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="03973-105">Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="03973-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="03973-106">Řešení</span><span class="sxs-lookup"><span data-stu-id="03973-106">Resolution</span></span>

<span data-ttu-id="03973-107">Chcete-li vyřešit, nastavte **ExecutionPolicy** k **RemoteSigned** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):</span><span class="sxs-lookup"><span data-stu-id="03973-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```


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
><span data-ttu-id="ad9a5-103">Poznámka: Zadejte navrhovaný popisný název a stručný popis</span><span class="sxs-lookup"><span data-stu-id="ad9a5-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="ad9a5-104">Příklad: Chybné ExecutionPolicy chyby</span><span class="sxs-lookup"><span data-stu-id="ad9a5-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="ad9a5-105">Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="ad9a5-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="ad9a5-106">Řešení</span><span class="sxs-lookup"><span data-stu-id="ad9a5-106">Resolution</span></span>

<span data-ttu-id="ad9a5-107">Chcete-li vyřešit, nastavte **ExecutionPolicy** k **RemoteSigned** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):</span><span class="sxs-lookup"><span data-stu-id="ad9a5-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```
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
><span data-ttu-id="496ef-103">Poznámka: Zadejte navrhovaný popisný název a stručný popis</span><span class="sxs-lookup"><span data-stu-id="496ef-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="496ef-104">Příklad: Chybné ExecutionPolicy chyby</span><span class="sxs-lookup"><span data-stu-id="496ef-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="496ef-105">Ve Windows 7 může způsobit chyby oznámené o ExecutionPolicy používání modulů Powershellu a prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="496ef-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="496ef-106">Řešení</span><span class="sxs-lookup"><span data-stu-id="496ef-106">Resolution</span></span>

<span data-ttu-id="496ef-107">Chcete-li vyřešit, nastavte **ExecutionPolicy** k **RemoteSigned** spuštěním následujícího příkazu v relaci prostředí PowerShell zvýšenými oprávněními (Spustit jako správce):</span><span class="sxs-lookup"><span data-stu-id="496ef-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

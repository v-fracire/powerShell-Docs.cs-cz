---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 9cc4384088fcc39b09979b8ae4d023fc46307b13
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5c58d-103">Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="5c58d-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5c58d-104">Spustí kontrolu konzistence pomocí plánovače úloh.</span><span class="sxs-lookup"><span data-stu-id="5c58d-104">Starts a consistency check by using the Task Scheduler.</span></span>

<a name="syntax"></a><span data-ttu-id="5c58d-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="5c58d-105">Syntax</span></span>
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a><span data-ttu-id="5c58d-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="5c58d-106">Parameters</span></span>
----------

<span data-ttu-id="5c58d-107">*Příznaky* \[v\] bitová maska, která určuje typ spuštění kontroly konzistence.</span><span class="sxs-lookup"><span data-stu-id="5c58d-107">*Flags* \[in\] A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="5c58d-108">Následující hodnoty jsou platné a mohou být kombinovány s použitím bitové **nebo** operace:</span><span class="sxs-lookup"><span data-stu-id="5c58d-108">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="5c58d-109">Hodnota</span><span class="sxs-lookup"><span data-stu-id="5c58d-109">Value</span></span> |<span data-ttu-id="5c58d-110">Popis</span><span class="sxs-lookup"><span data-stu-id="5c58d-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="5c58d-111">**1**</span><span class="sxs-lookup"><span data-stu-id="5c58d-111">**1**</span></span> | <span data-ttu-id="5c58d-112">Kontrola konzistence normální.</span><span class="sxs-lookup"><span data-stu-id="5c58d-112">A normal consistency check.</span></span> |
|<span data-ttu-id="5c58d-113">**2**</span><span class="sxs-lookup"><span data-stu-id="5c58d-113">**2**</span></span> | <span data-ttu-id="5c58d-114">Pokračování kontrolu konzistence po restartu systému.</span><span class="sxs-lookup"><span data-stu-id="5c58d-114">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="5c58d-115">Tato hodnota by neměla kombinovat s další hodnoty.</span><span class="sxs-lookup"><span data-stu-id="5c58d-115">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="5c58d-116">**4**</span><span class="sxs-lookup"><span data-stu-id="5c58d-116">**4**</span></span> | <span data-ttu-id="5c58d-117">Konfigurace by měl být vyžádány z načítacího serveru zadaný v metakonfiguraci pro uzel.</span><span class="sxs-lookup"><span data-stu-id="5c58d-117">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="5c58d-118">Tato hodnota by měla vždycky kombinovat s **1**, pro hodnotu **5**.</span><span class="sxs-lookup"><span data-stu-id="5c58d-118">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="5c58d-119">**8**</span><span class="sxs-lookup"><span data-stu-id="5c58d-119">**8**</span></span> | <span data-ttu-id="5c58d-120">Stav odeslat na server sestav.</span><span class="sxs-lookup"><span data-stu-id="5c58d-120">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="5c58d-121">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="5c58d-121">Return value</span></span>
------------

<span data-ttu-id="5c58d-122">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="5c58d-122">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5c58d-123">Poznámky</span><span class="sxs-lookup"><span data-stu-id="5c58d-123">Remarks</span></span>

<span data-ttu-id="5c58d-124">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="5c58d-124">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5c58d-125">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5c58d-125">Requirements</span></span>
------------
><span data-ttu-id="5c58d-126">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5c58d-126">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="5c58d-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c58d-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="5c58d-128">Viz taky</span><span class="sxs-lookup"><span data-stu-id="5c58d-128">See also</span></span>


[<span data-ttu-id="5c58d-129">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5c58d-129">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
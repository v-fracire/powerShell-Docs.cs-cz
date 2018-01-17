---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda PerformRequiredConfigurationChecks MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 687c92f2dac5e8855731713e81390ac67615231e
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4a03f-103">Metoda PerformRequiredConfigurationChecks MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="4a03f-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4a03f-104">Spustí kontrolu konzistence pomocí plánovače úloh.</span><span class="sxs-lookup"><span data-stu-id="4a03f-104">Starts a consistency check by using the Task Scheduler.</span></span>

<a name="syntax"></a><span data-ttu-id="4a03f-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4a03f-105">Syntax</span></span>
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a><span data-ttu-id="4a03f-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="4a03f-106">Parameters</span></span>
----------

<span data-ttu-id="4a03f-107">*Příznaky* \[v\]</span><span class="sxs-lookup"><span data-stu-id="4a03f-107">*Flags* \[in\]</span></span>  
<span data-ttu-id="4a03f-108">Bitová maska, která určuje typ spuštění kontroly konzistence.</span><span class="sxs-lookup"><span data-stu-id="4a03f-108">A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="4a03f-109">Následující hodnoty jsou platné a mohou být kombinovány s použitím bitové **nebo** operace:</span><span class="sxs-lookup"><span data-stu-id="4a03f-109">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="4a03f-110">Hodnota</span><span class="sxs-lookup"><span data-stu-id="4a03f-110">Value</span></span> |<span data-ttu-id="4a03f-111">Popis</span><span class="sxs-lookup"><span data-stu-id="4a03f-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="4a03f-112">**1**</span><span class="sxs-lookup"><span data-stu-id="4a03f-112">**1**</span></span> | <span data-ttu-id="4a03f-113">Kontrola konzistence normální.</span><span class="sxs-lookup"><span data-stu-id="4a03f-113">A normal consistency check.</span></span> |
|<span data-ttu-id="4a03f-114">**2**</span><span class="sxs-lookup"><span data-stu-id="4a03f-114">**2**</span></span> | <span data-ttu-id="4a03f-115">Pokračování kontrolu konzistence po restartu systému.</span><span class="sxs-lookup"><span data-stu-id="4a03f-115">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="4a03f-116">Tato hodnota by neměla kombinovat s další hodnoty.</span><span class="sxs-lookup"><span data-stu-id="4a03f-116">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="4a03f-117">**4**</span><span class="sxs-lookup"><span data-stu-id="4a03f-117">**4**</span></span> | <span data-ttu-id="4a03f-118">Konfigurace by měl být vyžádány z načítacího serveru zadaný v metakonfiguraci pro uzel.</span><span class="sxs-lookup"><span data-stu-id="4a03f-118">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="4a03f-119">Tato hodnota by měla vždycky kombinovat s **1**, pro hodnotu **5**.</span><span class="sxs-lookup"><span data-stu-id="4a03f-119">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="4a03f-120">**8**</span><span class="sxs-lookup"><span data-stu-id="4a03f-120">**8**</span></span> | <span data-ttu-id="4a03f-121">Stav odeslat na server sestav.</span><span class="sxs-lookup"><span data-stu-id="4a03f-121">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="4a03f-122">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="4a03f-122">Return value</span></span>
------------

<span data-ttu-id="4a03f-123">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="4a03f-123">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4a03f-124">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4a03f-124">Remarks</span></span>

<span data-ttu-id="4a03f-125">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="4a03f-125">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4a03f-126">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4a03f-126">Requirements</span></span>
------------
><span data-ttu-id="4a03f-127">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4a03f-127">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4a03f-128">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4a03f-128">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4a03f-129">Viz taky</span><span class="sxs-lookup"><span data-stu-id="4a03f-129">See also</span></span>


[<span data-ttu-id="4a03f-130">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4a03f-130">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




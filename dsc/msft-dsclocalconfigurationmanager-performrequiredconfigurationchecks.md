---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: c3fdaa23875815b1cf5cbf0b6e21c633e00664aa
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186690"
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="678bd-103">Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="678bd-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="678bd-104">Spustí kontrolu konzistence pomocí plánovače úloh.</span><span class="sxs-lookup"><span data-stu-id="678bd-104">Starts a consistency check by using the Task Scheduler.</span></span>

<a name="syntax"></a><span data-ttu-id="678bd-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="678bd-105">Syntax</span></span>
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a><span data-ttu-id="678bd-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="678bd-106">Parameters</span></span>
----------

<span data-ttu-id="678bd-107">*Příznaky* \[v\] bitová maska, která určuje typ spuštění kontroly konzistence.</span><span class="sxs-lookup"><span data-stu-id="678bd-107">*Flags* \[in\] A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="678bd-108">Následující hodnoty jsou platné a mohou být kombinovány s použitím bitové **nebo** operace:</span><span class="sxs-lookup"><span data-stu-id="678bd-108">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="678bd-109">Hodnota</span><span class="sxs-lookup"><span data-stu-id="678bd-109">Value</span></span> |<span data-ttu-id="678bd-110">Popis</span><span class="sxs-lookup"><span data-stu-id="678bd-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="678bd-111">**1**</span><span class="sxs-lookup"><span data-stu-id="678bd-111">**1**</span></span> | <span data-ttu-id="678bd-112">Kontrola konzistence normální.</span><span class="sxs-lookup"><span data-stu-id="678bd-112">A normal consistency check.</span></span> |
|<span data-ttu-id="678bd-113">**2**</span><span class="sxs-lookup"><span data-stu-id="678bd-113">**2**</span></span> | <span data-ttu-id="678bd-114">Pokračování kontrolu konzistence po restartu systému.</span><span class="sxs-lookup"><span data-stu-id="678bd-114">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="678bd-115">Tato hodnota by neměla kombinovat s další hodnoty.</span><span class="sxs-lookup"><span data-stu-id="678bd-115">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="678bd-116">**4**</span><span class="sxs-lookup"><span data-stu-id="678bd-116">**4**</span></span> | <span data-ttu-id="678bd-117">Konfigurace by měl být vyžádány z načítacího serveru zadaný v metakonfiguraci pro uzel.</span><span class="sxs-lookup"><span data-stu-id="678bd-117">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="678bd-118">Tato hodnota by měla vždycky kombinovat s **1**, pro hodnotu **5**.</span><span class="sxs-lookup"><span data-stu-id="678bd-118">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="678bd-119">**8**</span><span class="sxs-lookup"><span data-stu-id="678bd-119">**8**</span></span> | <span data-ttu-id="678bd-120">Stav odeslat na server sestav.</span><span class="sxs-lookup"><span data-stu-id="678bd-120">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="678bd-121">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="678bd-121">Return value</span></span>
------------

<span data-ttu-id="678bd-122">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="678bd-122">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="678bd-123">Poznámky</span><span class="sxs-lookup"><span data-stu-id="678bd-123">Remarks</span></span>

<span data-ttu-id="678bd-124">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="678bd-124">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="678bd-125">Požadavky</span><span class="sxs-lookup"><span data-stu-id="678bd-125">Requirements</span></span>
------------
><span data-ttu-id="678bd-126">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="678bd-126">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="678bd-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="678bd-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="678bd-128">Viz taky</span><span class="sxs-lookup"><span data-stu-id="678bd-128">See also</span></span>


[<span data-ttu-id="678bd-129">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="678bd-129">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
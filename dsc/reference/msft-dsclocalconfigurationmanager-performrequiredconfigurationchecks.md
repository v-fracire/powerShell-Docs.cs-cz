---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b92eefb7fbea6d96afa31f6b802ba10fe20d4103
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403637"
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="c0611-103">Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="c0611-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="c0611-104">Spustí kontrolu konzistence pomocí plánovače úloh.</span><span class="sxs-lookup"><span data-stu-id="c0611-104">Starts a consistency check by using the Task Scheduler.</span></span>

## <a name="syntax"></a><span data-ttu-id="c0611-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c0611-105">Syntax</span></span>

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

## <a name="parameters"></a><span data-ttu-id="c0611-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="c0611-106">Parameters</span></span>

<span data-ttu-id="c0611-107">*Příznaky* \[v\] bitová maska, která určuje typ spuštění kontroly konzistence.</span><span class="sxs-lookup"><span data-stu-id="c0611-107">*Flags* \[in\] A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="c0611-108">Následující hodnoty jsou platné a je možné kombinovat pomocí logické bitové **nebo** operace:</span><span class="sxs-lookup"><span data-stu-id="c0611-108">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="c0611-109">Hodnota</span><span class="sxs-lookup"><span data-stu-id="c0611-109">Value</span></span> |<span data-ttu-id="c0611-110">Popis</span><span class="sxs-lookup"><span data-stu-id="c0611-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="c0611-111">**1**</span><span class="sxs-lookup"><span data-stu-id="c0611-111">**1**</span></span> | <span data-ttu-id="c0611-112">Normální konzistence.</span><span class="sxs-lookup"><span data-stu-id="c0611-112">A normal consistency check.</span></span> |
|<span data-ttu-id="c0611-113">**2**</span><span class="sxs-lookup"><span data-stu-id="c0611-113">**2**</span></span> | <span data-ttu-id="c0611-114">Pokračování kontrolu konzistence po restartu.</span><span class="sxs-lookup"><span data-stu-id="c0611-114">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="c0611-115">Tato hodnota by neměla kombinovat s jinými hodnotami.</span><span class="sxs-lookup"><span data-stu-id="c0611-115">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="c0611-116">**4**</span><span class="sxs-lookup"><span data-stu-id="c0611-116">**4**</span></span> | <span data-ttu-id="c0611-117">Konfigurace by měl být vyžádány z načítacího serveru zadaný v metaconfiguration pro uzel.</span><span class="sxs-lookup"><span data-stu-id="c0611-117">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="c0611-118">Tato hodnota by měla vždy zkombinuje s **1**, pro hodnotu **5**.</span><span class="sxs-lookup"><span data-stu-id="c0611-118">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="c0611-119">**8**</span><span class="sxs-lookup"><span data-stu-id="c0611-119">**8**</span></span> | <span data-ttu-id="c0611-120">Stav odeslání na server sestav.</span><span class="sxs-lookup"><span data-stu-id="c0611-120">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="c0611-121">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="c0611-121">Return value</span></span>

<span data-ttu-id="c0611-122">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="c0611-122">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="c0611-123">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c0611-123">Remarks</span></span>

<span data-ttu-id="c0611-124">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="c0611-124">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="c0611-125">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c0611-125">Requirements</span></span>

<span data-ttu-id="c0611-126">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="c0611-126">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="c0611-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c0611-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="c0611-128">Viz taky</span><span class="sxs-lookup"><span data-stu-id="c0611-128">See also</span></span>

[<span data-ttu-id="c0611-129">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c0611-129">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
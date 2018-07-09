---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b92eefb7fbea6d96afa31f6b802ba10fe20d4103
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893225"
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d494b-103">Metoda PerformRequiredConfigurationChecks třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="d494b-103">PerformRequiredConfigurationChecks method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d494b-104">Spustí kontrolu konzistence pomocí plánovače úloh.</span><span class="sxs-lookup"><span data-stu-id="d494b-104">Starts a consistency check by using the Task Scheduler.</span></span>

## <a name="syntax"></a><span data-ttu-id="d494b-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d494b-105">Syntax</span></span>

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

## <a name="parameters"></a><span data-ttu-id="d494b-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="d494b-106">Parameters</span></span>

<span data-ttu-id="d494b-107">*Příznaky* \[v\] bitová maska, která určuje typ spuštění kontroly konzistence.</span><span class="sxs-lookup"><span data-stu-id="d494b-107">*Flags* \[in\] A bitmask that specifies the type of consistency check to run.</span></span> <span data-ttu-id="d494b-108">Následující hodnoty jsou platné a je možné kombinovat pomocí logické bitové **nebo** operace:</span><span class="sxs-lookup"><span data-stu-id="d494b-108">The following values are valid, and can be combined by using a bitwise **OR** operation:</span></span>

|<span data-ttu-id="d494b-109">Hodnota</span><span class="sxs-lookup"><span data-stu-id="d494b-109">Value</span></span> |<span data-ttu-id="d494b-110">Popis</span><span class="sxs-lookup"><span data-stu-id="d494b-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="d494b-111">**1**</span><span class="sxs-lookup"><span data-stu-id="d494b-111">**1**</span></span> | <span data-ttu-id="d494b-112">Normální konzistence.</span><span class="sxs-lookup"><span data-stu-id="d494b-112">A normal consistency check.</span></span> |
|<span data-ttu-id="d494b-113">**2**</span><span class="sxs-lookup"><span data-stu-id="d494b-113">**2**</span></span> | <span data-ttu-id="d494b-114">Pokračování kontrolu konzistence po restartu.</span><span class="sxs-lookup"><span data-stu-id="d494b-114">A continuation of a consistency check after a reboot.</span></span> <span data-ttu-id="d494b-115">Tato hodnota by neměla kombinovat s jinými hodnotami.</span><span class="sxs-lookup"><span data-stu-id="d494b-115">This value should not be combined with other values.</span></span> |
|<span data-ttu-id="d494b-116">**4**</span><span class="sxs-lookup"><span data-stu-id="d494b-116">**4**</span></span> | <span data-ttu-id="d494b-117">Konfigurace by měl být vyžádány z načítacího serveru zadaný v metaconfiguration pro uzel.</span><span class="sxs-lookup"><span data-stu-id="d494b-117">The configuration should be pulled from the pull server specified in the metaconfiguration for the node.</span></span> <span data-ttu-id="d494b-118">Tato hodnota by měla vždy zkombinuje s **1**, pro hodnotu **5**.</span><span class="sxs-lookup"><span data-stu-id="d494b-118">This value should always be combined with **1**, for a value of **5**.</span></span> |
|<span data-ttu-id="d494b-119">**8**</span><span class="sxs-lookup"><span data-stu-id="d494b-119">**8**</span></span> | <span data-ttu-id="d494b-120">Stav odeslání na server sestav.</span><span class="sxs-lookup"><span data-stu-id="d494b-120">Send status to the report server.</span></span> |

## <a name="return-value"></a><span data-ttu-id="d494b-121">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="d494b-121">Return value</span></span>

<span data-ttu-id="d494b-122">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="d494b-122">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d494b-123">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d494b-123">Remarks</span></span>

<span data-ttu-id="d494b-124">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="d494b-124">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d494b-125">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d494b-125">Requirements</span></span>

<span data-ttu-id="d494b-126">**Soubor MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d494b-126">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="d494b-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d494b-127">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="d494b-128">Viz taky</span><span class="sxs-lookup"><span data-stu-id="d494b-128">See also</span></span>

[<span data-ttu-id="d494b-129">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d494b-129">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
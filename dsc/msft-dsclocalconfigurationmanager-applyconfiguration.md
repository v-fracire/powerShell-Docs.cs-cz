---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 2844e354e0d054b13b92267ce314536d88a1c33e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="8d9ff-103">Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="8d9ff-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="8d9ff-104">Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="8d9ff-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="8d9ff-105">Pokud není žádná konfigurace čekající na vyřízení, tato metoda znovu použije aktuální konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="8d9ff-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="8d9ff-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="8d9ff-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="8d9ff-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="8d9ff-107">Parameters</span></span>
----------

<span data-ttu-id="8d9ff-108">*Vynutit* \[v\] Pokud je to **true**, aktuální konfiguraci se znovu použije, i když je v konfiguraci čekající na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="8d9ff-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="8d9ff-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="8d9ff-109">Return value</span></span>
------------

<span data-ttu-id="8d9ff-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="8d9ff-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="8d9ff-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="8d9ff-111">Remarks</span></span>

<span data-ttu-id="8d9ff-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="8d9ff-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="8d9ff-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8d9ff-113">Requirements</span></span>
------------
><span data-ttu-id="8d9ff-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="8d9ff-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="8d9ff-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="8d9ff-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="8d9ff-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="8d9ff-116">See also</span></span>


[<span data-ttu-id="8d9ff-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="8d9ff-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
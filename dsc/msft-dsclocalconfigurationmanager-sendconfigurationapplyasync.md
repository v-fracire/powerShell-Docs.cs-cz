---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 7ff821a277a548869862741551ee9897e417ea45
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f8133-103">Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="f8133-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f8133-104">Asynchronně odešle dokumentu konfigurace na spravovaných uzel a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f8133-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="f8133-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f8133-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="f8133-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="f8133-106">Parameters</span></span>
----------

<span data-ttu-id="f8133-107">*ConfigurationData* \[v\] data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f8133-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="f8133-108">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="f8133-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="f8133-109">*jobId* \[v\] ID úlohy, pro které chcete odeslat konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f8133-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="f8133-110">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="f8133-110">Return value</span></span>
------------

<span data-ttu-id="f8133-111">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="f8133-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f8133-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f8133-112">Remarks</span></span>

<span data-ttu-id="f8133-113">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="f8133-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f8133-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f8133-114">Requirements</span></span>
------------
><span data-ttu-id="f8133-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f8133-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="f8133-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f8133-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="f8133-117">Viz taky</span><span class="sxs-lookup"><span data-stu-id="f8133-117">See also</span></span>


[<span data-ttu-id="f8133-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f8133-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
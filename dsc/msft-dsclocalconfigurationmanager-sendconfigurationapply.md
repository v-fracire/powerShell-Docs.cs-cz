---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendConfigurationApply třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 8edf8c55089e767394ba21b42fe74072777a45c9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e1e05-103">Metoda SendConfigurationApply třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e1e05-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e1e05-104">Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e1e05-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="e1e05-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e1e05-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="e1e05-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="e1e05-106">Parameters</span></span>
----------

<span data-ttu-id="e1e05-107">*ConfigurationData* \[v\] data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e1e05-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="e1e05-108">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="e1e05-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="e1e05-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="e1e05-109">Return value</span></span>
------------

<span data-ttu-id="e1e05-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="e1e05-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e1e05-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e1e05-111">Remarks</span></span>

<span data-ttu-id="e1e05-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="e1e05-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e1e05-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e1e05-113">Requirements</span></span>
------------
><span data-ttu-id="e1e05-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e1e05-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="e1e05-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e1e05-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="e1e05-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="e1e05-116">See also</span></span>


[<span data-ttu-id="e1e05-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e1e05-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
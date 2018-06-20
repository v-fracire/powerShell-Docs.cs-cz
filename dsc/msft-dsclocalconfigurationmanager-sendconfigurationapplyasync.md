---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: acd8f380f1c49eb008563398c2c3de3fce5477f9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186673"
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="89fc1-103">Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="89fc1-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="89fc1-104">Asynchronně odešle dokumentu konfigurace na spravovaných uzel a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="89fc1-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="89fc1-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="89fc1-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="89fc1-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="89fc1-106">Parameters</span></span>
----------

<span data-ttu-id="89fc1-107">*ConfigurationData* \[v\] data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="89fc1-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="89fc1-108">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="89fc1-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="89fc1-109">*jobId* \[v\] ID úlohy, pro které chcete odeslat konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="89fc1-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="89fc1-110">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="89fc1-110">Return value</span></span>
------------

<span data-ttu-id="89fc1-111">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="89fc1-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="89fc1-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="89fc1-112">Remarks</span></span>

<span data-ttu-id="89fc1-113">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="89fc1-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="89fc1-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="89fc1-114">Requirements</span></span>
------------
><span data-ttu-id="89fc1-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="89fc1-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="89fc1-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="89fc1-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="89fc1-117">Viz taky</span><span class="sxs-lookup"><span data-stu-id="89fc1-117">See also</span></span>


[<span data-ttu-id="89fc1-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="89fc1-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
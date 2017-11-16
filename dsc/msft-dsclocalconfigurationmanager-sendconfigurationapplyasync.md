---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda SendConfigurationApplyAsync MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: e680bfd1c5b39d364c90cf5ef6b43d0a568af23a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e9ce9-103">Metoda SendConfigurationApplyAsync MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="e9ce9-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e9ce9-104">Asynchronně odešle dokumentu konfigurace na spravovaných uzel a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e9ce9-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="e9ce9-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e9ce9-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="e9ce9-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="e9ce9-106">Parameters</span></span>
----------

<span data-ttu-id="e9ce9-107">*ConfigurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="e9ce9-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="e9ce9-108">Data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e9ce9-108">The environment data for the configuration.</span></span>

<span data-ttu-id="e9ce9-109">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="e9ce9-109">*force* \[in\]</span></span>  
<span data-ttu-id="e9ce9-110">**Hodnota TRUE,** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="e9ce9-110">**true** to force the configuration to stop.</span></span>

<span data-ttu-id="e9ce9-111">*jobId* \[v\]</span><span class="sxs-lookup"><span data-stu-id="e9ce9-111">*jobId* \[in\]</span></span>  
<span data-ttu-id="e9ce9-112">ID úlohy, pro které chcete odeslat konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e9ce9-112">The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="e9ce9-113">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="e9ce9-113">Return value</span></span>
------------

<span data-ttu-id="e9ce9-114">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="e9ce9-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e9ce9-115">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e9ce9-115">Remarks</span></span>

<span data-ttu-id="e9ce9-116">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="e9ce9-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e9ce9-117">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e9ce9-117">Requirements</span></span>
------------
><span data-ttu-id="e9ce9-118">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e9ce9-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="e9ce9-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e9ce9-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="e9ce9-120">Viz taky</span><span class="sxs-lookup"><span data-stu-id="e9ce9-120">See also</span></span>


[<span data-ttu-id="e9ce9-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e9ce9-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




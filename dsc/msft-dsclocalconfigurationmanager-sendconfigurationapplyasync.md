---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda SendConfigurationApplyAsync MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: e680d510aaac097f4f0de80660274230e028ed45
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1be66-103">Metoda SendConfigurationApplyAsync MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="1be66-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1be66-104">Asynchronně odešle dokumentu konfigurace na spravovaných uzel a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1be66-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="1be66-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1be66-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a><span data-ttu-id="1be66-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="1be66-106">Parameters</span></span>
----------

<span data-ttu-id="1be66-107">*ConfigurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1be66-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="1be66-108">Data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1be66-108">The environment data for the configuration.</span></span>

<span data-ttu-id="1be66-109">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1be66-109">*force* \[in\]</span></span>  
<span data-ttu-id="1be66-110">**Hodnota TRUE,** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="1be66-110">**true** to force the configuration to stop.</span></span>

<span data-ttu-id="1be66-111">*jobId* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1be66-111">*jobId* \[in\]</span></span>  
<span data-ttu-id="1be66-112">ID úlohy, pro které chcete odeslat konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1be66-112">The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="1be66-113">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="1be66-113">Return value</span></span>
------------

<span data-ttu-id="1be66-114">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="1be66-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1be66-115">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1be66-115">Remarks</span></span>

<span data-ttu-id="1be66-116">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="1be66-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1be66-117">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1be66-117">Requirements</span></span>
------------
><span data-ttu-id="1be66-118">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1be66-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1be66-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1be66-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1be66-120">Viz taky</span><span class="sxs-lookup"><span data-stu-id="1be66-120">See also</span></span>


[<span data-ttu-id="1be66-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1be66-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




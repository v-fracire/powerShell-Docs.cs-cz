---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: f4c2ddaa37cdafeff1a442f3f1fa656788a1c6c8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="90871-103">Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="90871-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="90871-104">Získá výstup Agent konfigurace přidružené k určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="90871-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="90871-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="90871-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="90871-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="90871-106">Parameters</span></span>
----------

<span data-ttu-id="90871-107">*jobId* \[v\] ID úlohy, pro které chcete získat výstupní data.</span><span class="sxs-lookup"><span data-stu-id="90871-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="90871-108">*resumeOutputBookmark* \[v\] Určuje, že výstup by měl být pokračování z předchozí záložku.</span><span class="sxs-lookup"><span data-stu-id="90871-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="90871-109">*výstup* \[out\] výstup pro zadanou úlohu.</span><span class="sxs-lookup"><span data-stu-id="90871-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="90871-110">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="90871-110">Return value</span></span>
------------

<span data-ttu-id="90871-111">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="90871-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="90871-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="90871-112">Remarks</span></span>

<span data-ttu-id="90871-113">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="90871-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="90871-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="90871-114">Requirements</span></span>
------------
><span data-ttu-id="90871-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="90871-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="90871-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="90871-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="90871-117">Viz taky</span><span class="sxs-lookup"><span data-stu-id="90871-117">See also</span></span>


[<span data-ttu-id="90871-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="90871-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
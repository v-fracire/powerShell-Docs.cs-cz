---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda GetConfigurationResultOutput MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: f6106bb28dc20004b5bbb6df2d8e719cf0c453f0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d3700-103">Metoda GetConfigurationResultOutput MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="d3700-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d3700-104">Získá výstup Agent konfigurace přidružené k určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="d3700-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="d3700-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d3700-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="d3700-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="d3700-106">Parameters</span></span>
----------

<span data-ttu-id="d3700-107">*jobId* \[v\]</span><span class="sxs-lookup"><span data-stu-id="d3700-107">*jobId* \[in\]</span></span>  
<span data-ttu-id="d3700-108">ID úlohy, pro které chcete získat výstupní data.</span><span class="sxs-lookup"><span data-stu-id="d3700-108">The ID of the job for which to get output data.</span></span>

<span data-ttu-id="d3700-109">*resumeOutputBookmark* \[v\]</span><span class="sxs-lookup"><span data-stu-id="d3700-109">*resumeOutputBookmark* \[in\]</span></span>  
<span data-ttu-id="d3700-110">Určuje, že výstup by měl být pokračování z předchozí záložku.</span><span class="sxs-lookup"><span data-stu-id="d3700-110">Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="d3700-111">*výstup* \[out\]</span><span class="sxs-lookup"><span data-stu-id="d3700-111">*output* \[out\]</span></span>  
<span data-ttu-id="d3700-112">Výstup pro zadanou úlohu.</span><span class="sxs-lookup"><span data-stu-id="d3700-112">The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="d3700-113">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="d3700-113">Return value</span></span>
------------

<span data-ttu-id="d3700-114">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="d3700-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d3700-115">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d3700-115">Remarks</span></span>

<span data-ttu-id="d3700-116">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="d3700-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d3700-117">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d3700-117">Requirements</span></span>
------------
><span data-ttu-id="d3700-118">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d3700-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="d3700-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d3700-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="d3700-120">Viz taky</span><span class="sxs-lookup"><span data-stu-id="d3700-120">See also</span></span>


[<span data-ttu-id="d3700-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d3700-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 




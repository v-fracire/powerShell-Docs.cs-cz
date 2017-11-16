---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda GetConfigurationResultOutput MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 09862fd3c19e1e517c9bf5df878113ba3f10d8a6
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1fb7b-103">Metoda GetConfigurationResultOutput MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="1fb7b-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1fb7b-104">Získá výstup Agent konfigurace přidružené k určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="1fb7b-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="1fb7b-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1fb7b-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="1fb7b-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="1fb7b-106">Parameters</span></span>
----------

<span data-ttu-id="1fb7b-107">*jobId* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1fb7b-107">*jobId* \[in\]</span></span>  
<span data-ttu-id="1fb7b-108">ID úlohy, pro které chcete získat výstupní data.</span><span class="sxs-lookup"><span data-stu-id="1fb7b-108">The ID of the job for which to get output data.</span></span>

<span data-ttu-id="1fb7b-109">*resumeOutputBookmark* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1fb7b-109">*resumeOutputBookmark* \[in\]</span></span>  
<span data-ttu-id="1fb7b-110">Určuje, že výstup by měl být pokračování z předchozí záložku.</span><span class="sxs-lookup"><span data-stu-id="1fb7b-110">Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="1fb7b-111">*výstup* \[out\]</span><span class="sxs-lookup"><span data-stu-id="1fb7b-111">*output* \[out\]</span></span>  
<span data-ttu-id="1fb7b-112">Výstup pro zadanou úlohu.</span><span class="sxs-lookup"><span data-stu-id="1fb7b-112">The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="1fb7b-113">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="1fb7b-113">Return value</span></span>
------------

<span data-ttu-id="1fb7b-114">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="1fb7b-114">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1fb7b-115">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1fb7b-115">Remarks</span></span>

<span data-ttu-id="1fb7b-116">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="1fb7b-116">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1fb7b-117">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1fb7b-117">Requirements</span></span>
------------
><span data-ttu-id="1fb7b-118">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1fb7b-118">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1fb7b-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1fb7b-119">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1fb7b-120">Viz taky</span><span class="sxs-lookup"><span data-stu-id="1fb7b-120">See also</span></span>


[<span data-ttu-id="1fb7b-121">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1fb7b-121">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 




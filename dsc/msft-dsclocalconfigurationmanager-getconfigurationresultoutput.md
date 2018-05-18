---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 73d10a8b44e5056e3fce1598518630a84aff6ceb
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b08f8-103">Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="b08f8-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b08f8-104">Získá výstup Agent konfigurace přidružené k určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="b08f8-104">Gets the Configuration Agent output associated with a specific job.</span></span>

<a name="syntax"></a><span data-ttu-id="b08f8-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b08f8-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

<a name="parameters"></a><span data-ttu-id="b08f8-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="b08f8-106">Parameters</span></span>
----------

<span data-ttu-id="b08f8-107">*jobId* \[v\] ID úlohy, pro které chcete získat výstupní data.</span><span class="sxs-lookup"><span data-stu-id="b08f8-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="b08f8-108">*resumeOutputBookmark* \[v\] Určuje, že výstup by měl být pokračování z předchozí záložku.</span><span class="sxs-lookup"><span data-stu-id="b08f8-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="b08f8-109">*výstup* \[out\] výstup pro zadanou úlohu.</span><span class="sxs-lookup"><span data-stu-id="b08f8-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="b08f8-110">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="b08f8-110">Return value</span></span>
------------

<span data-ttu-id="b08f8-111">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="b08f8-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b08f8-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="b08f8-112">Remarks</span></span>

<span data-ttu-id="b08f8-113">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="b08f8-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b08f8-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b08f8-114">Requirements</span></span>
------------
><span data-ttu-id="b08f8-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b08f8-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="b08f8-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b08f8-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="b08f8-117">Viz taky</span><span class="sxs-lookup"><span data-stu-id="b08f8-117">See also</span></span>


[<span data-ttu-id="b08f8-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b08f8-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
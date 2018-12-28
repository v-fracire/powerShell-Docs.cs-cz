---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ea572a4a66befd4e4b8d83e2957632b1b5ed7d93
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403783"
---
# <a name="getconfigurationresultoutput-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="aca0d-103">Metoda GetConfigurationResultOutput třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="aca0d-103">GetConfigurationResultOutput method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="aca0d-104">Získá konfiguraci agenta výstup přidružené k určité úlohy.</span><span class="sxs-lookup"><span data-stu-id="aca0d-104">Gets the Configuration Agent output associated with a specific job.</span></span>

## <a name="syntax"></a><span data-ttu-id="aca0d-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="aca0d-105">Syntax</span></span>

```mof
uint32 GetConfigurationResultOutput(
  [in]  string                      jobId,
  [in]  uint8                       resumeOutputBookmark[],
  [out] MSFT_DSCConfigurationOutput output[]
);
```

## <a name="parameters"></a><span data-ttu-id="aca0d-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="aca0d-106">Parameters</span></span>

<span data-ttu-id="aca0d-107">*jobId* \[v\] ID úlohy, pro který má být získána výstupní data.</span><span class="sxs-lookup"><span data-stu-id="aca0d-107">*jobId* \[in\] The ID of the job for which to get output data.</span></span>

<span data-ttu-id="aca0d-108">*resumeOutputBookmark* \[v\] Určuje, že výstup by měl být pokračování z předchozí záložku.</span><span class="sxs-lookup"><span data-stu-id="aca0d-108">*resumeOutputBookmark* \[in\] Specifies that the output should be a continuation from a previous bookmark.</span></span>

<span data-ttu-id="aca0d-109">*výstup* \[si\] výstup pro zadanou úlohu.</span><span class="sxs-lookup"><span data-stu-id="aca0d-109">*output* \[out\] The output for the specified job.</span></span>

## <a name="return-value"></a><span data-ttu-id="aca0d-110">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="aca0d-110">Return value</span></span>

<span data-ttu-id="aca0d-111">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="aca0d-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="aca0d-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="aca0d-112">Remarks</span></span>

<span data-ttu-id="aca0d-113">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="aca0d-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="aca0d-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="aca0d-114">Requirements</span></span>

<span data-ttu-id="aca0d-115">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="aca0d-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="aca0d-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="aca0d-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="aca0d-117">Viz taky</span><span class="sxs-lookup"><span data-stu-id="aca0d-117">See also</span></span>

[<span data-ttu-id="aca0d-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="aca0d-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
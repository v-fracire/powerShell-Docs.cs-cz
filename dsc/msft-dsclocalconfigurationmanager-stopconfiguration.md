---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: dadb6912af2e4450381958ed465799056da49946
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="bb9ff-103">Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="bb9ff-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="bb9ff-104">Zastaví změny konfigurace, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="bb9ff-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="bb9ff-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="bb9ff-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="bb9ff-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="bb9ff-106">Parameters</span></span>
----------

<span data-ttu-id="bb9ff-107">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="bb9ff-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="bb9ff-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="bb9ff-108">Return value</span></span>
------------

<span data-ttu-id="bb9ff-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="bb9ff-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="bb9ff-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="bb9ff-110">Remarks</span></span>

<span data-ttu-id="bb9ff-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="bb9ff-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="bb9ff-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="bb9ff-112">Requirements</span></span>
------------
><span data-ttu-id="bb9ff-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="bb9ff-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="bb9ff-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="bb9ff-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="bb9ff-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="bb9ff-115">See also</span></span>


[<span data-ttu-id="bb9ff-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="bb9ff-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
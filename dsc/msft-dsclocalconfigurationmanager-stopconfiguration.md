---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: aaed29cb81e2079c4673b621b81c52e109aa7b48
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d8d8d-103">Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="d8d8d-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d8d8d-104">Zastaví změny konfigurace, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="d8d8d-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="d8d8d-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d8d8d-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="d8d8d-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="d8d8d-106">Parameters</span></span>
----------

<span data-ttu-id="d8d8d-107">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="d8d8d-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="d8d8d-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="d8d8d-108">Return value</span></span>
------------

<span data-ttu-id="d8d8d-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="d8d8d-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d8d8d-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="d8d8d-110">Remarks</span></span>

<span data-ttu-id="d8d8d-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="d8d8d-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d8d8d-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="d8d8d-112">Requirements</span></span>
------------
><span data-ttu-id="d8d8d-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d8d8d-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="d8d8d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d8d8d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="d8d8d-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="d8d8d-115">See also</span></span>


[<span data-ttu-id="d8d8d-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d8d8d-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
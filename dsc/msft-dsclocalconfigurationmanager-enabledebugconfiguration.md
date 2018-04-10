---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 9fe41fa806a6abff1d36dadd0c041a5cf0e78caf
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="cdb05-103">Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="cdb05-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="cdb05-104">Povolí ladění na prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="cdb05-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="cdb05-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="cdb05-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="cdb05-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="cdb05-106">Parameters</span></span>
----------

<span data-ttu-id="cdb05-107">*BreakAll* \[v\] Nastaví zarážku na každém řádku ve skriptu prostředků.</span><span class="sxs-lookup"><span data-stu-id="cdb05-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="cdb05-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="cdb05-108">Return value</span></span>
------------

<span data-ttu-id="cdb05-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="cdb05-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="cdb05-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="cdb05-110">Remarks</span></span>

<span data-ttu-id="cdb05-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="cdb05-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="cdb05-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="cdb05-112">Requirements</span></span>
------------
><span data-ttu-id="cdb05-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="cdb05-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="cdb05-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="cdb05-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="cdb05-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="cdb05-115">See also</span></span>


[<span data-ttu-id="cdb05-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="cdb05-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
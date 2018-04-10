---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda RollBack třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: c0a801c4037921e700e447d1434e246df0a63a4f
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="28919-103">Metoda RollBack třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="28919-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="28919-104">Vrátí konfiguraci zpět na předchozí verzi.</span><span class="sxs-lookup"><span data-stu-id="28919-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="28919-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="28919-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="28919-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="28919-106">Parameters</span></span>
----------

<span data-ttu-id="28919-107">*configurationNumber* \[v\] určuje požadovanou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="28919-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="28919-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="28919-108">Return value</span></span>
------------

<span data-ttu-id="28919-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="28919-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="28919-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="28919-110">Remarks</span></span>

<span data-ttu-id="28919-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="28919-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="28919-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="28919-112">Requirements</span></span>
------------
><span data-ttu-id="28919-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="28919-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="28919-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="28919-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="28919-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="28919-115">See also</span></span>


[<span data-ttu-id="28919-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="28919-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
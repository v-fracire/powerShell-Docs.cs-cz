---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: e0ae8a50212b70841d210d7b2d666a2855218d1a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="2a6d5-103">Metoda RemoveConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="2a6d5-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="2a6d5-104">Odebere konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="2a6d5-104">Removes the configuration files.</span></span>

<a name="syntax"></a><span data-ttu-id="2a6d5-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2a6d5-105">Syntax</span></span>
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a><span data-ttu-id="2a6d5-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="2a6d5-106">Parameters</span></span>
----------

<span data-ttu-id="2a6d5-107">*Fáze* \[v\] Určuje, který dokument konfigurace odebrat.</span><span class="sxs-lookup"><span data-stu-id="2a6d5-107">*Stage* \[in\] Specifies which configuration document to remove.</span></span> <span data-ttu-id="2a6d5-108">Platné jsou následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="2a6d5-108">The following values are valid:</span></span>

|<span data-ttu-id="2a6d5-109">Hodnota</span><span class="sxs-lookup"><span data-stu-id="2a6d5-109">Value</span></span> |<span data-ttu-id="2a6d5-110">Popis</span><span class="sxs-lookup"><span data-stu-id="2a6d5-110">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="2a6d5-111">**1**</span><span class="sxs-lookup"><span data-stu-id="2a6d5-111">**1**</span></span> | <span data-ttu-id="2a6d5-112">**Aktuální** dokumentu konfigurace (current.mof).</span><span class="sxs-lookup"><span data-stu-id="2a6d5-112">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="2a6d5-113">**2**</span><span class="sxs-lookup"><span data-stu-id="2a6d5-113">**2**</span></span> | <span data-ttu-id="2a6d5-114">**Čekající** dokumentu konfigurace (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="2a6d5-114">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="2a6d5-115">**4**</span><span class="sxs-lookup"><span data-stu-id="2a6d5-115">**4**</span></span> | <span data-ttu-id="2a6d5-116">**Předchozí** dokumentu konfigurace (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="2a6d5-116">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="2a6d5-117">*Vynutit* \[v\] **true** vynutit odebrání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2a6d5-117">*Force* \[in\] **true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="2a6d5-118">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="2a6d5-118">Return value</span></span>
------------

<span data-ttu-id="2a6d5-119">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="2a6d5-119">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="2a6d5-120">Poznámky</span><span class="sxs-lookup"><span data-stu-id="2a6d5-120">Remarks</span></span>

<span data-ttu-id="2a6d5-121">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="2a6d5-121">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="2a6d5-122">Požadavky</span><span class="sxs-lookup"><span data-stu-id="2a6d5-122">Requirements</span></span>
------------
><span data-ttu-id="2a6d5-123">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="2a6d5-123">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="2a6d5-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="2a6d5-124">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="2a6d5-125">Viz taky</span><span class="sxs-lookup"><span data-stu-id="2a6d5-125">See also</span></span>


[<span data-ttu-id="2a6d5-126">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="2a6d5-126">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda RemoveConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: faa113c442b80eea3ac474220b098b7d80ec50a8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="97747-103">Metoda RemoveConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="97747-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="97747-104">Odebere konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="97747-104">Removes the configuration files.</span></span>

<a name="syntax"></a><span data-ttu-id="97747-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="97747-105">Syntax</span></span>
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a><span data-ttu-id="97747-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="97747-106">Parameters</span></span>
----------

<span data-ttu-id="97747-107">*Fáze* \[v\]</span><span class="sxs-lookup"><span data-stu-id="97747-107">*Stage* \[in\]</span></span>  
<span data-ttu-id="97747-108">Určuje, který dokument konfigurace odebrat.</span><span class="sxs-lookup"><span data-stu-id="97747-108">Specifies which configuration document to remove.</span></span> <span data-ttu-id="97747-109">Platné jsou následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="97747-109">The following values are valid:</span></span>

|<span data-ttu-id="97747-110">Hodnota</span><span class="sxs-lookup"><span data-stu-id="97747-110">Value</span></span> |<span data-ttu-id="97747-111">Popis</span><span class="sxs-lookup"><span data-stu-id="97747-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="97747-112">**1**</span><span class="sxs-lookup"><span data-stu-id="97747-112">**1**</span></span> | <span data-ttu-id="97747-113">**Aktuální** dokumentu konfigurace (current.mof).</span><span class="sxs-lookup"><span data-stu-id="97747-113">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="97747-114">**2**</span><span class="sxs-lookup"><span data-stu-id="97747-114">**2**</span></span> | <span data-ttu-id="97747-115">**Čekající** dokumentu konfigurace (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="97747-115">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="97747-116">**4**</span><span class="sxs-lookup"><span data-stu-id="97747-116">**4**</span></span> | <span data-ttu-id="97747-117">**Předchozí** dokumentu konfigurace (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="97747-117">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="97747-118">*Platnost* \[v\]</span><span class="sxs-lookup"><span data-stu-id="97747-118">*Force* \[in\]</span></span>  
<span data-ttu-id="97747-119">**Hodnota TRUE,** vynutit odebrání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="97747-119">**true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="97747-120">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="97747-120">Return value</span></span>
------------

<span data-ttu-id="97747-121">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="97747-121">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="97747-122">Poznámky</span><span class="sxs-lookup"><span data-stu-id="97747-122">Remarks</span></span>

<span data-ttu-id="97747-123">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="97747-123">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="97747-124">Požadavky</span><span class="sxs-lookup"><span data-stu-id="97747-124">Requirements</span></span>
------------
><span data-ttu-id="97747-125">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="97747-125">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="97747-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="97747-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="97747-127">Viz taky</span><span class="sxs-lookup"><span data-stu-id="97747-127">See also</span></span>


[<span data-ttu-id="97747-128">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="97747-128">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




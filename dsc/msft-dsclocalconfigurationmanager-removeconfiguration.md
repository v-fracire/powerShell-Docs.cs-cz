---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda RemoveConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: fed45836293adedbce18f01cfe53cdfa1a474975
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1863c-103">Metoda RemoveConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="1863c-103">RemoveConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1863c-104">Odebere konfigurační soubory.</span><span class="sxs-lookup"><span data-stu-id="1863c-104">Removes the configuration files.</span></span>

<a name="syntax"></a><span data-ttu-id="1863c-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1863c-105">Syntax</span></span>
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a><span data-ttu-id="1863c-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="1863c-106">Parameters</span></span>
----------

<span data-ttu-id="1863c-107">*Fáze* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1863c-107">*Stage* \[in\]</span></span>  
<span data-ttu-id="1863c-108">Určuje, který dokument konfigurace odebrat.</span><span class="sxs-lookup"><span data-stu-id="1863c-108">Specifies which configuration document to remove.</span></span> <span data-ttu-id="1863c-109">Platné jsou následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="1863c-109">The following values are valid:</span></span>

|<span data-ttu-id="1863c-110">Hodnota</span><span class="sxs-lookup"><span data-stu-id="1863c-110">Value</span></span> |<span data-ttu-id="1863c-111">Popis</span><span class="sxs-lookup"><span data-stu-id="1863c-111">Description</span></span> |
|:--- |:---|
|<span data-ttu-id="1863c-112">**1**</span><span class="sxs-lookup"><span data-stu-id="1863c-112">**1**</span></span> | <span data-ttu-id="1863c-113">**Aktuální** dokumentu konfigurace (current.mof).</span><span class="sxs-lookup"><span data-stu-id="1863c-113">The **Current** configuration document (current.mof).</span></span> |
|<span data-ttu-id="1863c-114">**2**</span><span class="sxs-lookup"><span data-stu-id="1863c-114">**2**</span></span> | <span data-ttu-id="1863c-115">**Čekající** dokumentu konfigurace (pending.mof).</span><span class="sxs-lookup"><span data-stu-id="1863c-115">The **Pending** configuration document (pending.mof).</span></span>  |
|<span data-ttu-id="1863c-116">**4**</span><span class="sxs-lookup"><span data-stu-id="1863c-116">**4**</span></span> | <span data-ttu-id="1863c-117">**Předchozí** dokumentu konfigurace (previous.mof).</span><span class="sxs-lookup"><span data-stu-id="1863c-117">The **Previous** configuration document (previous.mof).</span></span> |

<span data-ttu-id="1863c-118">*Platnost* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1863c-118">*Force* \[in\]</span></span>  
<span data-ttu-id="1863c-119">**Hodnota TRUE,** vynutit odebrání konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1863c-119">**true** to force the removal of the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="1863c-120">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="1863c-120">Return value</span></span>
------------

<span data-ttu-id="1863c-121">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="1863c-121">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1863c-122">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1863c-122">Remarks</span></span>

<span data-ttu-id="1863c-123">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="1863c-123">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1863c-124">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1863c-124">Requirements</span></span>
------------
><span data-ttu-id="1863c-125">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1863c-125">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1863c-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1863c-126">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1863c-127">Viz taky</span><span class="sxs-lookup"><span data-stu-id="1863c-127">See also</span></span>


[<span data-ttu-id="1863c-128">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1863c-128">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




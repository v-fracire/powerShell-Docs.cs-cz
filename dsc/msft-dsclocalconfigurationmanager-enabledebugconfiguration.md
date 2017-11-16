---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda EnableDebugConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 7220c972b3f43b4697cf71df54d2d43881938367
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9b853-103">Metoda EnableDebugConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="9b853-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9b853-104">Povolí ladění na prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="9b853-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="9b853-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9b853-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="9b853-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="9b853-106">Parameters</span></span>
----------

<span data-ttu-id="9b853-107">*BreakAll* \[v\]</span><span class="sxs-lookup"><span data-stu-id="9b853-107">*BreakAll* \[in\]</span></span>  
<span data-ttu-id="9b853-108">Nastaví zarážku na každém řádku ve skriptu prostředků.</span><span class="sxs-lookup"><span data-stu-id="9b853-108">Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="9b853-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="9b853-109">Return value</span></span>
------------

<span data-ttu-id="9b853-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="9b853-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9b853-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="9b853-111">Remarks</span></span>

<span data-ttu-id="9b853-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="9b853-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9b853-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9b853-113">Requirements</span></span>
------------
><span data-ttu-id="9b853-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9b853-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="9b853-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9b853-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="9b853-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="9b853-116">See also</span></span>


[<span data-ttu-id="9b853-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9b853-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 




---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 9e2a978f9d16abaed959be022229db4da5fd65bd
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="67734-103">Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="67734-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="67734-104">Povolí ladění na prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="67734-104">Enables DSC resource debugging.</span></span>

<a name="syntax"></a><span data-ttu-id="67734-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="67734-105">Syntax</span></span>
------

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

<a name="parameters"></a><span data-ttu-id="67734-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="67734-106">Parameters</span></span>
----------

<span data-ttu-id="67734-107">*BreakAll* \[v\] Nastaví zarážku na každém řádku ve skriptu prostředků.</span><span class="sxs-lookup"><span data-stu-id="67734-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="67734-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="67734-108">Return value</span></span>
------------

<span data-ttu-id="67734-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="67734-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="67734-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="67734-110">Remarks</span></span>

<span data-ttu-id="67734-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="67734-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="67734-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="67734-112">Requirements</span></span>
------------
><span data-ttu-id="67734-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="67734-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="67734-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="67734-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="67734-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="67734-115">See also</span></span>


[<span data-ttu-id="67734-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="67734-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
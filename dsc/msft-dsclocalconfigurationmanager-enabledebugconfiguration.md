---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b2eaebfa901cb5d93fd0183287073e6b31f975d1
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892395"
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e929e-103">Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e929e-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e929e-104">Povolí ladění prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="e929e-104">Enables DSC resource debugging.</span></span>

## <a name="syntax"></a><span data-ttu-id="e929e-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e929e-105">Syntax</span></span>

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a><span data-ttu-id="e929e-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="e929e-106">Parameters</span></span>

<span data-ttu-id="e929e-107">*BreakAll* \[v\] Nastaví zarážku na každý jednotlivý řádek ve skriptu prostředků.</span><span class="sxs-lookup"><span data-stu-id="e929e-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="e929e-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="e929e-108">Return value</span></span>

<span data-ttu-id="e929e-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="e929e-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e929e-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e929e-110">Remarks</span></span>

<span data-ttu-id="e929e-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="e929e-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e929e-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e929e-112">Requirements</span></span>

<span data-ttu-id="e929e-113">**Soubor MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e929e-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="e929e-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e929e-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="e929e-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="e929e-115">See also</span></span>

[<span data-ttu-id="e929e-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e929e-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
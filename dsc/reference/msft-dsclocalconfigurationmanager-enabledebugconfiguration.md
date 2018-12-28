---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b2eaebfa901cb5d93fd0183287073e6b31f975d1
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403627"
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="629a9-103">Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="629a9-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="629a9-104">Povolí ladění prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="629a9-104">Enables DSC resource debugging.</span></span>

## <a name="syntax"></a><span data-ttu-id="629a9-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="629a9-105">Syntax</span></span>

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a><span data-ttu-id="629a9-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="629a9-106">Parameters</span></span>

<span data-ttu-id="629a9-107">*BreakAll* \[v\] Nastaví zarážku na každý jednotlivý řádek ve skriptu prostředků.</span><span class="sxs-lookup"><span data-stu-id="629a9-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="629a9-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="629a9-108">Return value</span></span>

<span data-ttu-id="629a9-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="629a9-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="629a9-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="629a9-110">Remarks</span></span>

<span data-ttu-id="629a9-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="629a9-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="629a9-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="629a9-112">Requirements</span></span>

<span data-ttu-id="629a9-113">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="629a9-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="629a9-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="629a9-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="629a9-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="629a9-115">See also</span></span>

[<span data-ttu-id="629a9-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="629a9-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
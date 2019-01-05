---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b2eaebfa901cb5d93fd0183287073e6b31f975d1
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048128"
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9add7-103">Metoda EnableDebugConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="9add7-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9add7-104">Povolí ladění prostředků DSC.</span><span class="sxs-lookup"><span data-stu-id="9add7-104">Enables DSC resource debugging.</span></span>

## <a name="syntax"></a><span data-ttu-id="9add7-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9add7-105">Syntax</span></span>

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a><span data-ttu-id="9add7-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="9add7-106">Parameters</span></span>

<span data-ttu-id="9add7-107">*BreakAll* \[v\] Nastaví zarážku na každý jednotlivý řádek ve skriptu prostředků.</span><span class="sxs-lookup"><span data-stu-id="9add7-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="9add7-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="9add7-108">Return value</span></span>

<span data-ttu-id="9add7-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="9add7-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9add7-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="9add7-110">Remarks</span></span>

<span data-ttu-id="9add7-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="9add7-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9add7-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9add7-112">Requirements</span></span>

<span data-ttu-id="9add7-113">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9add7-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="9add7-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9add7-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="9add7-115">Viz také</span><span class="sxs-lookup"><span data-stu-id="9add7-115">See also</span></span>

[<span data-ttu-id="9add7-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9add7-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
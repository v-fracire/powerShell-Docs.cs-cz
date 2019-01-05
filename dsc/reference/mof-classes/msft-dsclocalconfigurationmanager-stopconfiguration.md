---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 1cd887d205967c3d282143df4e6199027639230e
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048112"
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="69206-103">Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="69206-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="69206-104">Zastaví probíhající změna konfigurace.</span><span class="sxs-lookup"><span data-stu-id="69206-104">Stops the configuration change that is in progress.</span></span>

## <a name="syntax"></a><span data-ttu-id="69206-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="69206-105">Syntax</span></span>

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="69206-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="69206-106">Parameters</span></span>

<span data-ttu-id="69206-107">*Vynutit* \[v\] **true** vynutit konfiguraci tak, aby zastavit.</span><span class="sxs-lookup"><span data-stu-id="69206-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="69206-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="69206-108">Return value</span></span>

<span data-ttu-id="69206-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="69206-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="69206-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="69206-110">Remarks</span></span>

<span data-ttu-id="69206-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="69206-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="69206-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="69206-112">Requirements</span></span>

<span data-ttu-id="69206-113">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="69206-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="69206-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="69206-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="69206-115">Viz také</span><span class="sxs-lookup"><span data-stu-id="69206-115">See also</span></span>

[<span data-ttu-id="69206-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="69206-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
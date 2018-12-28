---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 1cd887d205967c3d282143df4e6199027639230e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403827"
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="6c37f-103">Metoda StopConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="6c37f-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="6c37f-104">Zastaví probíhající změna konfigurace.</span><span class="sxs-lookup"><span data-stu-id="6c37f-104">Stops the configuration change that is in progress.</span></span>

## <a name="syntax"></a><span data-ttu-id="6c37f-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="6c37f-105">Syntax</span></span>

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="6c37f-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="6c37f-106">Parameters</span></span>

<span data-ttu-id="6c37f-107">*Vynutit* \[v\] **true** vynutit konfiguraci tak, aby zastavit.</span><span class="sxs-lookup"><span data-stu-id="6c37f-107">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="6c37f-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="6c37f-108">Return value</span></span>

<span data-ttu-id="6c37f-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="6c37f-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="6c37f-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6c37f-110">Remarks</span></span>

<span data-ttu-id="6c37f-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="6c37f-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="6c37f-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6c37f-112">Requirements</span></span>

<span data-ttu-id="6c37f-113">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="6c37f-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="6c37f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="6c37f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="6c37f-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="6c37f-115">See also</span></span>

[<span data-ttu-id="6c37f-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="6c37f-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
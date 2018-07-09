---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda RollBack třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 4956900ecd2c9cb7f2e2b5bcab94616f9f5d5565
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893014"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="50960-103">Metoda RollBack třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="50960-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="50960-104">Vrátí konfiguraci zpátky na předchozí verzi.</span><span class="sxs-lookup"><span data-stu-id="50960-104">Rolls back the configuration to a previous version.</span></span>

## <a name="syntax"></a><span data-ttu-id="50960-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="50960-105">Syntax</span></span>

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

## <a name="parameters"></a><span data-ttu-id="50960-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="50960-106">Parameters</span></span>

<span data-ttu-id="50960-107">*configurationNumber* \[v\] určuje požadovanou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="50960-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="50960-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="50960-108">Return value</span></span>

<span data-ttu-id="50960-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="50960-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="50960-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="50960-110">Remarks</span></span>

<span data-ttu-id="50960-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="50960-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="50960-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="50960-112">Requirements</span></span>

<span data-ttu-id="50960-113">**Soubor MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="50960-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="50960-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="50960-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="50960-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="50960-115">See also</span></span>

[<span data-ttu-id="50960-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="50960-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
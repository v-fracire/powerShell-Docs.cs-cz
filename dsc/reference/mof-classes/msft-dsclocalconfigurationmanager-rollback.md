---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda RollBack třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 4956900ecd2c9cb7f2e2b5bcab94616f9f5d5565
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048163"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="6ae1c-103">Metoda RollBack třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="6ae1c-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="6ae1c-104">Vrátí konfiguraci zpátky na předchozí verzi.</span><span class="sxs-lookup"><span data-stu-id="6ae1c-104">Rolls back the configuration to a previous version.</span></span>

## <a name="syntax"></a><span data-ttu-id="6ae1c-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="6ae1c-105">Syntax</span></span>

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

## <a name="parameters"></a><span data-ttu-id="6ae1c-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="6ae1c-106">Parameters</span></span>

<span data-ttu-id="6ae1c-107">*configurationNumber* \[v\] určuje požadovanou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="6ae1c-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="6ae1c-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="6ae1c-108">Return value</span></span>

<span data-ttu-id="6ae1c-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="6ae1c-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="6ae1c-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="6ae1c-110">Remarks</span></span>

<span data-ttu-id="6ae1c-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="6ae1c-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="6ae1c-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="6ae1c-112">Requirements</span></span>

<span data-ttu-id="6ae1c-113">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="6ae1c-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="6ae1c-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="6ae1c-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="6ae1c-115">Viz také</span><span class="sxs-lookup"><span data-stu-id="6ae1c-115">See also</span></span>

[<span data-ttu-id="6ae1c-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="6ae1c-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
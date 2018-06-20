---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda RollBack třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: d2f9b7025d611912e119800408e25fcb66bc0228
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219874"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="10e6f-103">Metoda RollBack třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="10e6f-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="10e6f-104">Vrátí konfiguraci zpět na předchozí verzi.</span><span class="sxs-lookup"><span data-stu-id="10e6f-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="10e6f-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="10e6f-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="10e6f-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="10e6f-106">Parameters</span></span>
----------

<span data-ttu-id="10e6f-107">*configurationNumber* \[v\] určuje požadovanou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="10e6f-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="10e6f-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="10e6f-108">Return value</span></span>
------------

<span data-ttu-id="10e6f-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="10e6f-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="10e6f-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="10e6f-110">Remarks</span></span>

<span data-ttu-id="10e6f-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="10e6f-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="10e6f-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="10e6f-112">Requirements</span></span>
------------
><span data-ttu-id="10e6f-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="10e6f-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="10e6f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="10e6f-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="10e6f-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="10e6f-115">See also</span></span>


[<span data-ttu-id="10e6f-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="10e6f-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
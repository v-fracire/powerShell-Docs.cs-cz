---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ef8488246b2c8614452d32009e45535f0ff2e184
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222135"
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4013d-103">Metoda ApplyConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="4013d-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4013d-104">Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="4013d-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span>

<span data-ttu-id="4013d-105">Pokud není žádná konfigurace čekající na vyřízení, tato metoda znovu použije aktuální konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="4013d-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="4013d-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4013d-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="4013d-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="4013d-107">Parameters</span></span>
----------

<span data-ttu-id="4013d-108">*Vynutit* \[v\] Pokud je to **true**, aktuální konfiguraci se znovu použije, i když je v konfiguraci čekající na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="4013d-108">*force* \[in\] If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="4013d-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="4013d-109">Return value</span></span>
------------

<span data-ttu-id="4013d-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="4013d-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4013d-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4013d-111">Remarks</span></span>

<span data-ttu-id="4013d-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="4013d-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4013d-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4013d-113">Requirements</span></span>
------------
><span data-ttu-id="4013d-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4013d-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4013d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4013d-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4013d-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="4013d-116">See also</span></span>


[<span data-ttu-id="4013d-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4013d-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
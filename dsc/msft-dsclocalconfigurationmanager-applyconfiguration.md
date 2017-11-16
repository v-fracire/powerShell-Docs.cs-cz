---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ApplyConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: febaf972a2a452eb9aaf3ec7fbc5e41f3f463a58
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1e5f5-103">Metoda ApplyConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="1e5f5-103">ApplyConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1e5f5-104">Používá Agent konfigurace můžete použít konfiguraci, která čeká na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="1e5f5-104">Uses the Configuration Agent to apply the configuration that is pending.</span></span> 

<span data-ttu-id="1e5f5-105">Pokud není žádná konfigurace čekající na vyřízení, tato metoda znovu použije aktuální konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1e5f5-105">If there is no configuration pending, this method reapplies the current configuration.</span></span>


## <a name="syntax"></a><span data-ttu-id="1e5f5-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1e5f5-106">Syntax</span></span>
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="1e5f5-107">Parameters</span><span class="sxs-lookup"><span data-stu-id="1e5f5-107">Parameters</span></span>
----------

<span data-ttu-id="1e5f5-108">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="1e5f5-108">*force* \[in\]</span></span>  
<span data-ttu-id="1e5f5-109">Pokud je to **true**, aktuální konfiguraci se znovu použije, i když je v konfiguraci čekající na vyřízení.</span><span class="sxs-lookup"><span data-stu-id="1e5f5-109">If this is **true**, the current configuration is reapplied, even if there is a configuration pending.</span></span>

## <a name="return-value"></a><span data-ttu-id="1e5f5-110">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="1e5f5-110">Return value</span></span>
------------

<span data-ttu-id="1e5f5-111">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="1e5f5-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1e5f5-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1e5f5-112">Remarks</span></span>

<span data-ttu-id="1e5f5-113">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="1e5f5-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1e5f5-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1e5f5-114">Requirements</span></span>
------------
><span data-ttu-id="1e5f5-115">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1e5f5-115">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1e5f5-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1e5f5-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1e5f5-117">Viz taky</span><span class="sxs-lookup"><span data-stu-id="1e5f5-117">See also</span></span>


[<span data-ttu-id="1e5f5-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1e5f5-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 




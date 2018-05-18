---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendConfigurationApply třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: c578f4f52d3ea70e7bcf683ac204d6e484d4630d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4dc4c-103">Metoda SendConfigurationApply třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="4dc4c-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4dc4c-104">Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="4dc4c-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="4dc4c-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4dc4c-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="4dc4c-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="4dc4c-106">Parameters</span></span>
----------

<span data-ttu-id="4dc4c-107">*ConfigurationData* \[v\] data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="4dc4c-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="4dc4c-108">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="4dc4c-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="4dc4c-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="4dc4c-109">Return value</span></span>
------------

<span data-ttu-id="4dc4c-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="4dc4c-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4dc4c-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4dc4c-111">Remarks</span></span>

<span data-ttu-id="4dc4c-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="4dc4c-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4dc4c-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4dc4c-113">Requirements</span></span>
------------
><span data-ttu-id="4dc4c-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4dc4c-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4dc4c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4dc4c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4dc4c-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="4dc4c-116">See also</span></span>


[<span data-ttu-id="4dc4c-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4dc4c-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda SendConfigurationApply MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 20f732d35860cccde4e507dc6916e27d0cf8c5f6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e4ea3-103">Metoda SendConfigurationApply MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="e4ea3-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e4ea3-104">Odešle spravovaný uzel dokumentu konfigurace a používá Agent konfigurace můžete použít konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e4ea3-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="e4ea3-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e4ea3-105">Syntax</span></span>
------

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="e4ea3-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="e4ea3-106">Parameters</span></span>
----------

<span data-ttu-id="e4ea3-107">*ConfigurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="e4ea3-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="e4ea3-108">Data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="e4ea3-108">The environment data for the configuration.</span></span>

<span data-ttu-id="e4ea3-109">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="e4ea3-109">*force* \[in\]</span></span>  
<span data-ttu-id="e4ea3-110">**Hodnota TRUE,** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="e4ea3-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="e4ea3-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="e4ea3-111">Return value</span></span>
------------

<span data-ttu-id="e4ea3-112">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="e4ea3-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e4ea3-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e4ea3-113">Remarks</span></span>

<span data-ttu-id="e4ea3-114">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="e4ea3-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e4ea3-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e4ea3-115">Requirements</span></span>
------------
><span data-ttu-id="e4ea3-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e4ea3-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="e4ea3-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e4ea3-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="e4ea3-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="e4ea3-118">See also</span></span>


[<span data-ttu-id="e4ea3-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e4ea3-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




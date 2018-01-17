---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Getconfiguration – metoda MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 60f4b49575dbb28ce74af0500e6982ec5d2e7a66
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="36c2c-103">Getconfiguration – metoda MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="36c2c-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="36c2c-104">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="36c2c-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="36c2c-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="36c2c-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="36c2c-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="36c2c-106">Parameters</span></span>
----------

<span data-ttu-id="36c2c-107">*configurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="36c2c-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="36c2c-108">Určuje konfigurační data k odeslání.</span><span class="sxs-lookup"><span data-stu-id="36c2c-108">Specifies the configuration data to send.</span></span>

<span data-ttu-id="36c2c-109">*konfigurace* \[out\]</span><span class="sxs-lookup"><span data-stu-id="36c2c-109">*configurations* \[out\]</span></span>  
<span data-ttu-id="36c2c-110">Při návratu obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="36c2c-110">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="36c2c-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="36c2c-111">Return value</span></span>
------------

<span data-ttu-id="36c2c-112">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="36c2c-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="36c2c-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="36c2c-113">Remarks</span></span>

<span data-ttu-id="36c2c-114">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="36c2c-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="36c2c-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="36c2c-115">Requirements</span></span>
------------
><span data-ttu-id="36c2c-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="36c2c-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="36c2c-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="36c2c-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="36c2c-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="36c2c-118">See also</span></span>


[<span data-ttu-id="36c2c-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="36c2c-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 




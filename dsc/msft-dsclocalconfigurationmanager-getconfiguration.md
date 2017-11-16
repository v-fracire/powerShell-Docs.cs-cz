---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Getconfiguration – metoda MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 96676a76a0302543e5e4a214c82ed952d7f52a71
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="33acc-103">Getconfiguration – metoda MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="33acc-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="33acc-104">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="33acc-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="33acc-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="33acc-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="33acc-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="33acc-106">Parameters</span></span>
----------

<span data-ttu-id="33acc-107">*configurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="33acc-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="33acc-108">Určuje konfigurační data k odeslání.</span><span class="sxs-lookup"><span data-stu-id="33acc-108">Specifies the configuration data to send.</span></span>

<span data-ttu-id="33acc-109">*konfigurace* \[out\]</span><span class="sxs-lookup"><span data-stu-id="33acc-109">*configurations* \[out\]</span></span>  
<span data-ttu-id="33acc-110">Při návratu obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="33acc-110">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="33acc-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="33acc-111">Return value</span></span>
------------

<span data-ttu-id="33acc-112">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="33acc-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="33acc-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="33acc-113">Remarks</span></span>

<span data-ttu-id="33acc-114">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="33acc-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="33acc-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="33acc-115">Requirements</span></span>
------------
><span data-ttu-id="33acc-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="33acc-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="33acc-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="33acc-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="33acc-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="33acc-118">See also</span></span>


[<span data-ttu-id="33acc-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="33acc-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
 

 




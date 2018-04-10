---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 07d7db9dcc4288e6b72d5df37d82e44eb6f72ad2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="1e74c-103">Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="1e74c-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="1e74c-104">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="1e74c-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="1e74c-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1e74c-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="1e74c-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="1e74c-106">Parameters</span></span>
----------

<span data-ttu-id="1e74c-107">*configurationData* \[v\] Určuje konfigurační data k odeslání.</span><span class="sxs-lookup"><span data-stu-id="1e74c-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="1e74c-108">*konfigurace* \[out\] na vrátí, obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1e74c-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="1e74c-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="1e74c-109">Return value</span></span>
------------

<span data-ttu-id="1e74c-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="1e74c-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="1e74c-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="1e74c-111">Remarks</span></span>

<span data-ttu-id="1e74c-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="1e74c-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="1e74c-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="1e74c-113">Requirements</span></span>
------------
><span data-ttu-id="1e74c-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="1e74c-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="1e74c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="1e74c-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="1e74c-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="1e74c-116">See also</span></span>


[<span data-ttu-id="1e74c-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="1e74c-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
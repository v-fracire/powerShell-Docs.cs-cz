---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 46eec896df643996bea5f2c371a9294034caae6b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218412"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4dbea-103">Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="4dbea-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4dbea-104">Odešle spravovaný uzel dokumentu konfigurace a používá **získat** metoda konfigurace agenta pro použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="4dbea-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

<a name="syntax"></a><span data-ttu-id="4dbea-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4dbea-105">Syntax</span></span>
------

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

<a name="parameters"></a><span data-ttu-id="4dbea-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="4dbea-106">Parameters</span></span>
----------

<span data-ttu-id="4dbea-107">*configurationData* \[v\] Určuje konfigurační data k odeslání.</span><span class="sxs-lookup"><span data-stu-id="4dbea-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="4dbea-108">*konfigurace* \[out\] na vrátí, obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="4dbea-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="4dbea-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="4dbea-109">Return value</span></span>
------------

<span data-ttu-id="4dbea-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="4dbea-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4dbea-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4dbea-111">Remarks</span></span>

<span data-ttu-id="4dbea-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="4dbea-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4dbea-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4dbea-113">Requirements</span></span>
------------
><span data-ttu-id="4dbea-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4dbea-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="4dbea-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4dbea-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="4dbea-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="4dbea-116">See also</span></span>


[<span data-ttu-id="4dbea-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4dbea-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
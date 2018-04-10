---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ab82b239ddfdb4075d9440cd66343266b3c08eda
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="67b1b-103">Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="67b1b-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="67b1b-104">Nastaví správce místní konfigurace nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="67b1b-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="67b1b-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="67b1b-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="67b1b-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="67b1b-106">Parameters</span></span>
----------

<span data-ttu-id="67b1b-107">*ConfigurationData* \[v\] data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="67b1b-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="67b1b-108">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="67b1b-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="67b1b-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="67b1b-109">Return value</span></span>
------------

<span data-ttu-id="67b1b-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="67b1b-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="67b1b-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="67b1b-111">Remarks</span></span>

<span data-ttu-id="67b1b-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="67b1b-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="67b1b-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="67b1b-113">Requirements</span></span>
------------
><span data-ttu-id="67b1b-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="67b1b-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="67b1b-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="67b1b-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="67b1b-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="67b1b-116">See also</span></span>


[<span data-ttu-id="67b1b-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="67b1b-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
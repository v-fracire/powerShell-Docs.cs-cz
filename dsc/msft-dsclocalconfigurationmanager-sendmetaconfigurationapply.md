---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 46acd86ac52b7b6b39f06fc65af2498b4f5348ed
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218837"
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a5488-103">Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a5488-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a5488-104">Nastaví správce místní konfigurace nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="a5488-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="a5488-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a5488-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="a5488-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="a5488-106">Parameters</span></span>
----------

<span data-ttu-id="a5488-107">*ConfigurationData* \[v\] data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="a5488-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="a5488-108">*Vynutit* \[v\] **true** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="a5488-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="a5488-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="a5488-109">Return value</span></span>
------------

<span data-ttu-id="a5488-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="a5488-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a5488-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a5488-111">Remarks</span></span>

<span data-ttu-id="a5488-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="a5488-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a5488-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a5488-113">Requirements</span></span>
------------
><span data-ttu-id="a5488-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a5488-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="a5488-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a5488-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="a5488-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="a5488-116">See also</span></span>


[<span data-ttu-id="a5488-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a5488-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
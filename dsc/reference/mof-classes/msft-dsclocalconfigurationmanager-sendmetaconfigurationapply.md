---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b372a6c0ab9d4561dcf67026275e7d3ca6aa2584
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048202"
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="48626-103">Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="48626-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="48626-104">Nastaví Local Configuration Manageru, které se používají k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="48626-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="48626-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="48626-105">Syntax</span></span>

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="48626-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="48626-106">Parameters</span></span>

<span data-ttu-id="48626-107">*ConfigurationData* \[v\] dat prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="48626-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="48626-108">*Vynutit* \[v\] **true** vynutit konfiguraci tak, aby zastavit.</span><span class="sxs-lookup"><span data-stu-id="48626-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="48626-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="48626-109">Return value</span></span>

<span data-ttu-id="48626-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="48626-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="48626-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="48626-111">Remarks</span></span>

<span data-ttu-id="48626-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="48626-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="48626-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="48626-113">Requirements</span></span>

<span data-ttu-id="48626-114">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="48626-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="48626-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="48626-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="48626-116">Viz také</span><span class="sxs-lookup"><span data-stu-id="48626-116">See also</span></span>

[<span data-ttu-id="48626-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="48626-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
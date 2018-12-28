---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b372a6c0ab9d4561dcf67026275e7d3ca6aa2584
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403669"
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ee7df-103">Metoda SendMetaConfigurationApply třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="ee7df-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ee7df-104">Nastaví Local Configuration Manageru, které se používají k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="ee7df-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="ee7df-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ee7df-105">Syntax</span></span>

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="ee7df-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="ee7df-106">Parameters</span></span>

<span data-ttu-id="ee7df-107">*ConfigurationData* \[v\] dat prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="ee7df-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="ee7df-108">*Vynutit* \[v\] **true** vynutit konfiguraci tak, aby zastavit.</span><span class="sxs-lookup"><span data-stu-id="ee7df-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="ee7df-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="ee7df-109">Return value</span></span>

<span data-ttu-id="ee7df-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="ee7df-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="ee7df-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="ee7df-111">Remarks</span></span>

<span data-ttu-id="ee7df-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="ee7df-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="ee7df-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ee7df-113">Requirements</span></span>

<span data-ttu-id="ee7df-114">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ee7df-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="ee7df-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ee7df-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="ee7df-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="ee7df-116">See also</span></span>

[<span data-ttu-id="ee7df-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ee7df-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
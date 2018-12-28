---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b028079cf826719967858f50e357b441ba8f9d79
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403628"
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="c6005-103">Metoda SendConfigurationApplyAsync třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="c6005-103">SendConfigurationApplyAsync method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="c6005-104">Asynchronně odešle dokument konfigurace spravovaných uzlů a použít danou konfiguraci pomocí konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="c6005-104">Sends the configuration document asynchronously to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="c6005-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c6005-105">Syntax</span></span>

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

## <a name="parameters"></a><span data-ttu-id="c6005-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="c6005-106">Parameters</span></span>

<span data-ttu-id="c6005-107">*ConfigurationData* \[v\] dat prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="c6005-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="c6005-108">*Vynutit* \[v\] **true** vynutit konfiguraci tak, aby zastavit.</span><span class="sxs-lookup"><span data-stu-id="c6005-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

<span data-ttu-id="c6005-109">*jobId* \[v\] ID úlohy, pro které se mají poslat konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="c6005-109">*jobId* \[in\] The ID of the job for which to send the configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="c6005-110">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="c6005-110">Return value</span></span>

<span data-ttu-id="c6005-111">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="c6005-111">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="c6005-112">Poznámky</span><span class="sxs-lookup"><span data-stu-id="c6005-112">Remarks</span></span>

<span data-ttu-id="c6005-113">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="c6005-113">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="c6005-114">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c6005-114">Requirements</span></span>

<span data-ttu-id="c6005-115">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="c6005-115">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="c6005-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c6005-116">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="c6005-117">Viz taky</span><span class="sxs-lookup"><span data-stu-id="c6005-117">See also</span></span>

[<span data-ttu-id="c6005-118">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="c6005-118">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
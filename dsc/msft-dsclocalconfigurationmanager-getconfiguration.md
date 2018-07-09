---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892538"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="209ab-103">Metoda GetConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="209ab-103">GetConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="209ab-104">Odešle dokument konfigurace spravovaných uzlů a používá **získat** metody konfigurace agenta použít danou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="209ab-104">Sends the configuration document to the managed node and uses the **Get** method of the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="209ab-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="209ab-105">Syntax</span></span>

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a><span data-ttu-id="209ab-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="209ab-106">Parameters</span></span>

<span data-ttu-id="209ab-107">*configurationData* \[v\] konfigurační data určená k odeslání.</span><span class="sxs-lookup"><span data-stu-id="209ab-107">*configurationData* \[in\] Specifies the configuration data to send.</span></span>

<span data-ttu-id="209ab-108">*konfigurace* \[si\] na vrátit, obsahuje vložený instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="209ab-108">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="209ab-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="209ab-109">Return value</span></span>

<span data-ttu-id="209ab-110">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="209ab-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="209ab-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="209ab-111">Remarks</span></span>

<span data-ttu-id="209ab-112">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="209ab-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="209ab-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="209ab-113">Requirements</span></span>

<span data-ttu-id="209ab-114">**Soubor MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="209ab-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="209ab-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="209ab-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="209ab-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="209ab-116">See also</span></span>

[<span data-ttu-id="209ab-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="209ab-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
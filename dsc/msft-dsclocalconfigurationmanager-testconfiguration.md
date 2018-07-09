---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: d746832b01310f43a7aae33dd0fa70c0928bb3e0
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893922"
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="0f711-103">Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="0f711-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="0f711-104">Odešle dokument konfigurace spravovaných uzlů a ověří aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="0f711-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

## <a name="syntax"></a><span data-ttu-id="0f711-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0f711-105">Syntax</span></span>

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

## <a name="parameters"></a><span data-ttu-id="0f711-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="0f711-106">Parameters</span></span>

<span data-ttu-id="0f711-107">*configurationData* \[v\] dat prostředí pro confuguration.</span><span class="sxs-lookup"><span data-stu-id="0f711-107">*configurationData* \[in\] Environment data for the confuguration.</span></span>

<span data-ttu-id="0f711-108">*InDesiredState* \[si\] na vrátit, určuje, zda spravovaných uzlů je ve stavu určené dokument konfigurace.</span><span class="sxs-lookup"><span data-stu-id="0f711-108">*InDesiredState* \[out\] On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="0f711-109">*ResourcesInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceInDesiredState** třída, která určuje prostředky, které jsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="0f711-109">*ResourcesInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="0f711-110">*ResourcesNotInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceNotInDesiredState** třída, která určuje prostředky, které nejsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="0f711-110">*ResourcesNotInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="0f711-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="0f711-111">Return value</span></span>

<span data-ttu-id="0f711-112">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="0f711-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="0f711-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="0f711-113">Remarks</span></span>

<span data-ttu-id="0f711-114">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="0f711-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="0f711-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0f711-115">Requirements</span></span>

<span data-ttu-id="0f711-116">**Soubor MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0f711-116">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="0f711-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0f711-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="0f711-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="0f711-118">See also</span></span>

[<span data-ttu-id="0f711-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0f711-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
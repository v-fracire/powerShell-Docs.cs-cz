---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: d746832b01310f43a7aae33dd0fa70c0928bb3e0
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048125"
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="5c4c0-103">Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="5c4c0-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="5c4c0-104">Odešle dokument konfigurace spravovaných uzlů a ověří aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

## <a name="syntax"></a><span data-ttu-id="5c4c0-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="5c4c0-105">Syntax</span></span>

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

## <a name="parameters"></a><span data-ttu-id="5c4c0-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="5c4c0-106">Parameters</span></span>

<span data-ttu-id="5c4c0-107">*configurationData* \[v\] dat prostředí pro confuguration.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-107">*configurationData* \[in\] Environment data for the confuguration.</span></span>

<span data-ttu-id="5c4c0-108">*InDesiredState* \[si\] na vrátit, určuje, zda spravovaných uzlů je ve stavu určené dokument konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-108">*InDesiredState* \[out\] On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="5c4c0-109">*ResourcesInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceInDesiredState** třída, která určuje prostředky, které jsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-109">*ResourcesInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="5c4c0-110">*ResourcesNotInDesiredState* \[si\] na vrátit, obsahuje vložený instance **MSFT_ResourceNotInDesiredState** třída, která určuje prostředky, které nejsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-110">*ResourcesNotInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="5c4c0-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="5c4c0-111">Return value</span></span>

<span data-ttu-id="5c4c0-112">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="5c4c0-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="5c4c0-113">Remarks</span></span>

<span data-ttu-id="5c4c0-114">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="5c4c0-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="5c4c0-115">Requirements</span></span>

<span data-ttu-id="5c4c0-116">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="5c4c0-116">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="5c4c0-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c4c0-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="5c4c0-118">Viz také</span><span class="sxs-lookup"><span data-stu-id="5c4c0-118">See also</span></span>

[<span data-ttu-id="5c4c0-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="5c4c0-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
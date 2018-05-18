---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 2df04d317bd5e7a5c2a713d92be57c5c9a9f5e8c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="240cb-103">Metoda TestConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="240cb-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="240cb-104">Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="240cb-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

<a name="syntax"></a><span data-ttu-id="240cb-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="240cb-105">Syntax</span></span>
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a><span data-ttu-id="240cb-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="240cb-106">Parameters</span></span>
----------

<span data-ttu-id="240cb-107">*configurationData* \[v\] prostředí dat pro confuguration.</span><span class="sxs-lookup"><span data-stu-id="240cb-107">*configurationData* \[in\] Environment data for the confuguration.</span></span>

<span data-ttu-id="240cb-108">*InDesiredState* \[out\] na vrátit, určuje, zda spravovaný uzel je ve stavu určeného dokumentu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="240cb-108">*InDesiredState* \[out\] On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="240cb-109">*ResourcesInDesiredState* \[out\] na vrátí, obsahuje vložené instance **MSFT_ResourceInDesiredState** třídu, která určuje prostředky, které jsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="240cb-109">*ResourcesInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="240cb-110">*ResourcesNotInDesiredState* \[out\] na vrátí, obsahuje vložené instance **MSFT_ResourceNotInDesiredState** třídu, která určuje prostředky, které nejsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="240cb-110">*ResourcesNotInDesiredState* \[out\] On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="240cb-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="240cb-111">Return value</span></span>
------------

<span data-ttu-id="240cb-112">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="240cb-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="240cb-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="240cb-113">Remarks</span></span>

<span data-ttu-id="240cb-114">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="240cb-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="240cb-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="240cb-115">Requirements</span></span>
------------
><span data-ttu-id="240cb-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="240cb-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="240cb-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="240cb-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="240cb-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="240cb-118">See also</span></span>


[<span data-ttu-id="240cb-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="240cb-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
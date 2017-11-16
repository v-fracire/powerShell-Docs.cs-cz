---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda TestConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 8e9986837aaf41b1396a2399c58675bc51b0b708
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="8025c-103">Metoda TestConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="8025c-103">TestConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="8025c-104">Odešle spravovaný uzel dokumentu konfigurace a zkontroluje aktuální konfiguraci proti dokumentu.</span><span class="sxs-lookup"><span data-stu-id="8025c-104">Sends the configuration document to the managed node and verifies the current configuration against the document.</span></span>

<a name="syntax"></a><span data-ttu-id="8025c-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="8025c-105">Syntax</span></span>
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a><span data-ttu-id="8025c-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="8025c-106">Parameters</span></span>
----------

<span data-ttu-id="8025c-107">*configurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="8025c-107">*configurationData* \[in\]</span></span>  
<span data-ttu-id="8025c-108">Data confuguration prostředí.</span><span class="sxs-lookup"><span data-stu-id="8025c-108">Environment data for the confuguration.</span></span>

<span data-ttu-id="8025c-109">*InDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="8025c-109">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="8025c-110">Při návratu Určuje, zda spravovaný uzel je ve stavu určeného dokumentu konfigurace.</span><span class="sxs-lookup"><span data-stu-id="8025c-110">On return, specifies whether the managed node is in the state specified by the configuration document.</span></span>

<span data-ttu-id="8025c-111">*ResourcesInDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="8025c-111">*ResourcesInDesiredState* \[out\]</span></span>  
<span data-ttu-id="8025c-112">Při návratu, obsahuje vložené instance **MSFT_ResourceInDesiredState** třídu, která určuje prostředky, které jsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="8025c-112">On return, contains an embedded instance of the **MSFT_ResourceInDesiredState** class that specifies resources that are in the desired state.</span></span>

<span data-ttu-id="8025c-113">*ResourcesNotInDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="8025c-113">*ResourcesNotInDesiredState* \[out\]</span></span>  
<span data-ttu-id="8025c-114">Při návratu, obsahuje vložené instance **MSFT_ResourceNotInDesiredState** třídu, která určuje prostředky, které nejsou v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="8025c-114">On return, contains an embedded instance of the **MSFT_ResourceNotInDesiredState** class that specifies resources that are not in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="8025c-115">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="8025c-115">Return value</span></span>
------------

<span data-ttu-id="8025c-116">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="8025c-116">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="8025c-117">Poznámky</span><span class="sxs-lookup"><span data-stu-id="8025c-117">Remarks</span></span>

<span data-ttu-id="8025c-118">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="8025c-118">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="8025c-119">Požadavky</span><span class="sxs-lookup"><span data-stu-id="8025c-119">Requirements</span></span>
------------
><span data-ttu-id="8025c-120">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="8025c-120">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="8025c-121">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="8025c-121">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="8025c-122">Viz taky</span><span class="sxs-lookup"><span data-stu-id="8025c-122">See also</span></span>


[<span data-ttu-id="8025c-123">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="8025c-123">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



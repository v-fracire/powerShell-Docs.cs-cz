---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 7d8b185c49778253dcb4e983ad948775c4cb0842
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="58189-103">Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="58189-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="58189-104">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="58189-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="58189-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="58189-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="58189-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="58189-106">Parameters</span></span>
----------

<span data-ttu-id="58189-107">*Typ prostředku* \[v\]</span><span class="sxs-lookup"><span data-stu-id="58189-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="58189-108">Název prostředku k volání.</span><span class="sxs-lookup"><span data-stu-id="58189-108">The name of the resource to call.</span></span>

<span data-ttu-id="58189-109">*Název modulu* \[v\]</span><span class="sxs-lookup"><span data-stu-id="58189-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="58189-110">Název modulu, který obsahuje prostředek k volání.</span><span class="sxs-lookup"><span data-stu-id="58189-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="58189-111">*resourceProperty* \[v\]</span><span class="sxs-lookup"><span data-stu-id="58189-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="58189-112">Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="58189-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="58189-113">Použití [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="58189-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="58189-114">*konfigurace* \[out\]</span><span class="sxs-lookup"><span data-stu-id="58189-114">*configurations* \[out\]</span></span>  
<span data-ttu-id="58189-115">Při návratu obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="58189-115">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="58189-116">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="58189-116">Return value</span></span>
------------

<span data-ttu-id="58189-117">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="58189-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="58189-118">Poznámky</span><span class="sxs-lookup"><span data-stu-id="58189-118">Remarks</span></span>

<span data-ttu-id="58189-119">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="58189-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="58189-120">Požadavky</span><span class="sxs-lookup"><span data-stu-id="58189-120">Requirements</span></span>
------------
><span data-ttu-id="58189-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="58189-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="58189-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="58189-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="58189-123">Viz taky</span><span class="sxs-lookup"><span data-stu-id="58189-123">See also</span></span>


[<span data-ttu-id="58189-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="58189-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



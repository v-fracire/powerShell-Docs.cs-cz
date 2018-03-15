---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 2c055b3fab468f85c9e2f91cf1eaf1a4353b4660
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="f8adc-103">Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="f8adc-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="f8adc-104">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="f8adc-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="f8adc-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f8adc-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="f8adc-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="f8adc-106">Parameters</span></span>
----------

<span data-ttu-id="f8adc-107">*Typ prostředku* \[v\]</span><span class="sxs-lookup"><span data-stu-id="f8adc-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="f8adc-108">Název prostředku k volání.</span><span class="sxs-lookup"><span data-stu-id="f8adc-108">The name of the resource to call.</span></span>

<span data-ttu-id="f8adc-109">*ModuleName* \[in\]</span><span class="sxs-lookup"><span data-stu-id="f8adc-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="f8adc-110">Název modulu, který obsahuje prostředek k volání.</span><span class="sxs-lookup"><span data-stu-id="f8adc-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="f8adc-111">*resourceProperty* \[v\]</span><span class="sxs-lookup"><span data-stu-id="f8adc-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="f8adc-112">Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="f8adc-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="f8adc-113">Použití [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="f8adc-113">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="f8adc-114">*konfigurace* \[out\]</span><span class="sxs-lookup"><span data-stu-id="f8adc-114">*configurations* \[out\]</span></span>  
<span data-ttu-id="f8adc-115">Při návratu obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="f8adc-115">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="f8adc-116">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="f8adc-116">Return value</span></span>
------------

<span data-ttu-id="f8adc-117">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="f8adc-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="f8adc-118">Poznámky</span><span class="sxs-lookup"><span data-stu-id="f8adc-118">Remarks</span></span>

<span data-ttu-id="f8adc-119">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="f8adc-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="f8adc-120">Požadavky</span><span class="sxs-lookup"><span data-stu-id="f8adc-120">Requirements</span></span>
------------
><span data-ttu-id="f8adc-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="f8adc-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="f8adc-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="f8adc-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="f8adc-123">Viz taky</span><span class="sxs-lookup"><span data-stu-id="f8adc-123">See also</span></span>


[<span data-ttu-id="f8adc-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="f8adc-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




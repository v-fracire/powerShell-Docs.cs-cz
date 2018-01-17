---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: df90cb6859413c94be992c8cbc30171e9bd3d6de
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="0c53f-103">Metoda ResourceGet MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="0c53f-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="0c53f-104">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="0c53f-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="0c53f-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0c53f-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="0c53f-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="0c53f-106">Parameters</span></span>
----------

<span data-ttu-id="0c53f-107">*Typ prostředku* \[v\]</span><span class="sxs-lookup"><span data-stu-id="0c53f-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="0c53f-108">Název prostředku k volání.</span><span class="sxs-lookup"><span data-stu-id="0c53f-108">The name of the resource to call.</span></span>

<span data-ttu-id="0c53f-109">*ModuleName* \[in\]</span><span class="sxs-lookup"><span data-stu-id="0c53f-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="0c53f-110">Název modulu, který obsahuje prostředek k volání.</span><span class="sxs-lookup"><span data-stu-id="0c53f-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="0c53f-111">*resourceProperty* \[v\]</span><span class="sxs-lookup"><span data-stu-id="0c53f-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="0c53f-112">Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="0c53f-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="0c53f-113">Použití [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="0c53f-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="0c53f-114">*konfigurace* \[out\]</span><span class="sxs-lookup"><span data-stu-id="0c53f-114">*configurations* \[out\]</span></span>  
<span data-ttu-id="0c53f-115">Při návratu obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="0c53f-115">On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="0c53f-116">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="0c53f-116">Return value</span></span>
------------

<span data-ttu-id="0c53f-117">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="0c53f-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="0c53f-118">Poznámky</span><span class="sxs-lookup"><span data-stu-id="0c53f-118">Remarks</span></span>

<span data-ttu-id="0c53f-119">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="0c53f-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="0c53f-120">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0c53f-120">Requirements</span></span>
------------
><span data-ttu-id="0c53f-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0c53f-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="0c53f-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0c53f-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="0c53f-123">Viz taky</span><span class="sxs-lookup"><span data-stu-id="0c53f-123">See also</span></span>


[<span data-ttu-id="0c53f-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0c53f-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 




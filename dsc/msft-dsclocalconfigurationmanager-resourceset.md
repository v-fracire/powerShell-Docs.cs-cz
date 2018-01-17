---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda ResourceSet MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 7291641098578226449f8cbd360da0a3f9842598
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="caab5-103">Metoda ResourceSet MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="caab5-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="caab5-104">Volá přímo **nastavit** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="caab5-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="caab5-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="caab5-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="caab5-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="caab5-106">Parameters</span></span>
----------

<span data-ttu-id="caab5-107">*Typ prostředku* \[v\]</span><span class="sxs-lookup"><span data-stu-id="caab5-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="caab5-108">Název prostředku k volání.</span><span class="sxs-lookup"><span data-stu-id="caab5-108">The name of the resource to call.</span></span>

<span data-ttu-id="caab5-109">*ModuleName* \[in\]</span><span class="sxs-lookup"><span data-stu-id="caab5-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="caab5-110">Název modulu, který obsahuje prostředek k volání.</span><span class="sxs-lookup"><span data-stu-id="caab5-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="caab5-111">*resourceProperty* \[v\]</span><span class="sxs-lookup"><span data-stu-id="caab5-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="caab5-112">Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="caab5-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="caab5-113">Použití [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="caab5-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="caab5-114">*RebootRequired* \[out\]</span><span class="sxs-lookup"><span data-stu-id="caab5-114">*RebootRequired* \[out\]</span></span>  
<span data-ttu-id="caab5-115">Při návratu, je tato vlastnost nastavená na **true** Pokud je potřeba restartovat cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="caab5-115">On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="caab5-116">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="caab5-116">Return value</span></span>
------------

<span data-ttu-id="caab5-117">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="caab5-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="caab5-118">Poznámky</span><span class="sxs-lookup"><span data-stu-id="caab5-118">Remarks</span></span>

<span data-ttu-id="caab5-119">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="caab5-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="caab5-120">Požadavky</span><span class="sxs-lookup"><span data-stu-id="caab5-120">Requirements</span></span>
------------
><span data-ttu-id="caab5-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="caab5-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="caab5-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="caab5-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="caab5-123">Viz taky</span><span class="sxs-lookup"><span data-stu-id="caab5-123">See also</span></span>


[<span data-ttu-id="caab5-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="caab5-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)

 

 




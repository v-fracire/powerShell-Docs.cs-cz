---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda ResourceGet třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 30cbaa907d4dc3a921c9e5fe61ffddc5d61c2347
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="aa299-103">Metoda ResourceGet třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="aa299-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="aa299-104">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="aa299-104">Directly calls the **Get** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="aa299-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="aa299-105">Syntax</span></span>
------

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

<a name="parameters"></a><span data-ttu-id="aa299-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="aa299-106">Parameters</span></span>
----------

<span data-ttu-id="aa299-107">*Typ prostředku* \[v\] název prostředku k volání.</span><span class="sxs-lookup"><span data-stu-id="aa299-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="aa299-108">*Název modulu* \[v\] název modul, který obsahuje prostředek, který volání.</span><span class="sxs-lookup"><span data-stu-id="aa299-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="aa299-109">*resourceProperty* \[v\] Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="aa299-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="aa299-110">Použití [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="aa299-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="aa299-111">*konfigurace* \[out\] na vrátí, obsahuje vložené instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="aa299-111">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="aa299-112">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="aa299-112">Return value</span></span>
------------

<span data-ttu-id="aa299-113">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="aa299-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="aa299-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="aa299-114">Remarks</span></span>

<span data-ttu-id="aa299-115">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="aa299-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="aa299-116">Požadavky</span><span class="sxs-lookup"><span data-stu-id="aa299-116">Requirements</span></span>
------------
><span data-ttu-id="aa299-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="aa299-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="aa299-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="aa299-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="aa299-119">Viz taky</span><span class="sxs-lookup"><span data-stu-id="aa299-119">See also</span></span>


[<span data-ttu-id="aa299-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="aa299-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
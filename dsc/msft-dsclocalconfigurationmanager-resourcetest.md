---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda ResourceTest třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: f03a034329a9cde5cd44dbaf42ba1789c2b8f4f9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="06dcf-103">Metoda ResourceTest třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="06dcf-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="06dcf-104">Volá přímo **Test** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="06dcf-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="06dcf-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="06dcf-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="06dcf-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="06dcf-106">Parameters</span></span>
----------

<span data-ttu-id="06dcf-107">*Typ prostředku* \[v\] název prostředku k volání.</span><span class="sxs-lookup"><span data-stu-id="06dcf-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="06dcf-108">*Název modulu* \[v\] název modul, který obsahuje prostředek, který volání.</span><span class="sxs-lookup"><span data-stu-id="06dcf-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="06dcf-109">*resourceProperty* \[v\] Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="06dcf-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="06dcf-110">Použití [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="06dcf-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="06dcf-111">*InDesiredState* \[out\] na vrátit, je tato vlastnost nastavená na **true** Pokud cílový uzel je v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="06dcf-111">*InDesiredState* \[out\] On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="06dcf-112">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="06dcf-112">Return value</span></span>
------------

<span data-ttu-id="06dcf-113">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="06dcf-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="06dcf-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="06dcf-114">Remarks</span></span>

<span data-ttu-id="06dcf-115">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="06dcf-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="06dcf-116">Požadavky</span><span class="sxs-lookup"><span data-stu-id="06dcf-116">Requirements</span></span>
------------
><span data-ttu-id="06dcf-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="06dcf-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="06dcf-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="06dcf-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="06dcf-119">Viz taky</span><span class="sxs-lookup"><span data-stu-id="06dcf-119">See also</span></span>


[<span data-ttu-id="06dcf-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="06dcf-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
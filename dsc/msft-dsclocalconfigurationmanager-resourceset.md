---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda ResourceSet třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: b5f437a123bd38df21f30d11e71d2c3b36bc9f3a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b001d-103">Metoda ResourceSet třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="b001d-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b001d-104">Volá přímo **nastavit** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="b001d-104">Directly calls the **Set** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="b001d-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b001d-105">Syntax</span></span>
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

<a name="parameters"></a><span data-ttu-id="b001d-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="b001d-106">Parameters</span></span>
----------

<span data-ttu-id="b001d-107">*Typ prostředku* \[v\] název prostředku k volání.</span><span class="sxs-lookup"><span data-stu-id="b001d-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="b001d-108">*Název modulu* \[v\] název modul, který obsahuje prostředek, který volání.</span><span class="sxs-lookup"><span data-stu-id="b001d-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="b001d-109">*resourceProperty* \[v\] Určuje název vlastnosti prostředku a jeho hodnotu v zatřiďovací tabulku jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="b001d-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="b001d-110">Použití [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) rutiny zjistit vlastnosti prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="b001d-110">Use the [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="b001d-111">*RebootRequired* \[out\] na vrátit, je tato vlastnost nastavená na **true** Pokud je potřeba restartovat cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="b001d-111">*RebootRequired* \[out\] On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="b001d-112">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="b001d-112">Return value</span></span>
------------

<span data-ttu-id="b001d-113">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="b001d-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b001d-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="b001d-114">Remarks</span></span>

<span data-ttu-id="b001d-115">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="b001d-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b001d-116">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b001d-116">Requirements</span></span>
------------
><span data-ttu-id="b001d-117">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b001d-117">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="b001d-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b001d-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="b001d-119">Viz taky</span><span class="sxs-lookup"><span data-stu-id="b001d-119">See also</span></span>


[<span data-ttu-id="b001d-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b001d-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
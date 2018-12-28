---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda ResourceGet třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 1b74adf2327af2e0f9416f1d00eac4e3b75e9013
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403658"
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="e1ae2-103">Metoda ResourceGet třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e1ae2-103">ResourceGet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="e1ae2-104">Volá přímo **získat** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-104">Directly calls the **Get** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="e1ae2-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e1ae2-105">Syntax</span></span>

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

## <a name="parameters"></a><span data-ttu-id="e1ae2-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="e1ae2-106">Parameters</span></span>

<span data-ttu-id="e1ae2-107">*Element ResourceType* \[v\] název prostředku, který chcete volat.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="e1ae2-108">*Název modulu* \[v\] názvu modulu, který obsahuje prostředek, který chcete volat.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="e1ae2-109">*Vlastnost resourceProperty* \[v\] Určuje název vlastnosti prostředků a její hodnotu v zatřiďovací tabulce jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="e1ae2-110">Použití [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) rutiny ke zjišťování vlastností prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="e1ae2-111">*konfigurace* \[si\] na vrátit, obsahuje vložený instance konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-111">*configurations* \[out\] On return, contains an embedded instance of the configurations.</span></span>

## <a name="return-value"></a><span data-ttu-id="e1ae2-112">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="e1ae2-112">Return value</span></span>

<span data-ttu-id="e1ae2-113">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="e1ae2-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="e1ae2-114">Remarks</span></span>

<span data-ttu-id="e1ae2-115">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="e1ae2-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="e1ae2-116">Požadavky</span><span class="sxs-lookup"><span data-stu-id="e1ae2-116">Requirements</span></span>

<span data-ttu-id="e1ae2-117">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="e1ae2-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="e1ae2-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e1ae2-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="e1ae2-119">Viz taky</span><span class="sxs-lookup"><span data-stu-id="e1ae2-119">See also</span></span>

[<span data-ttu-id="e1ae2-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e1ae2-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
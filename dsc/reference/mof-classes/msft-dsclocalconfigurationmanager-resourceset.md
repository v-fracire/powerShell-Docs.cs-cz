---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda ResourceSet třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: 2712b7ff0a19e643c1f343d436c084f8970c9dd4
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048146"
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="caffe-103">Metoda ResourceSet třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="caffe-103">ResourceSet method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="caffe-104">Volá přímo **nastavit** metoda prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="caffe-104">Directly calls the **Set** method of a DSC resource.</span></span>

## <a name="syntax"></a><span data-ttu-id="caffe-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="caffe-105">Syntax</span></span>

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
);
```

## <a name="parameters"></a><span data-ttu-id="caffe-106">Parametry</span><span class="sxs-lookup"><span data-stu-id="caffe-106">Parameters</span></span>

<span data-ttu-id="caffe-107">*Element ResourceType* \[v\] název prostředku, který chcete volat.</span><span class="sxs-lookup"><span data-stu-id="caffe-107">*ResourceType* \[in\] The name of the resource to call.</span></span>

<span data-ttu-id="caffe-108">*Název modulu* \[v\] názvu modulu, který obsahuje prostředek, který chcete volat.</span><span class="sxs-lookup"><span data-stu-id="caffe-108">*ModuleName* \[in\] The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="caffe-109">*Vlastnost resourceProperty* \[v\] Určuje název vlastnosti prostředků a její hodnotu v zatřiďovací tabulce jako klíč a hodnotu, v uvedeném pořadí.</span><span class="sxs-lookup"><span data-stu-id="caffe-109">*resourceProperty* \[in\] Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="caffe-110">Použití [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) rutiny ke zjišťování vlastností prostředku a jejich typy.</span><span class="sxs-lookup"><span data-stu-id="caffe-110">Use the [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="caffe-111">*RebootRequired* \[si\] návratu, je tato vlastnost nastavená na **true** Pokud cílový uzel je potřeba restartovat.</span><span class="sxs-lookup"><span data-stu-id="caffe-111">*RebootRequired* \[out\] On return, this property is set to **true** if the target node needs to be rebooted.</span></span>

## <a name="return-value"></a><span data-ttu-id="caffe-112">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="caffe-112">Return value</span></span>

<span data-ttu-id="caffe-113">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="caffe-113">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="caffe-114">Poznámky</span><span class="sxs-lookup"><span data-stu-id="caffe-114">Remarks</span></span>

<span data-ttu-id="caffe-115">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="caffe-115">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="caffe-116">Požadavky</span><span class="sxs-lookup"><span data-stu-id="caffe-116">Requirements</span></span>

<span data-ttu-id="caffe-117">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="caffe-117">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="caffe-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="caffe-118">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="caffe-119">Viz také</span><span class="sxs-lookup"><span data-stu-id="caffe-119">See also</span></span>

[<span data-ttu-id="caffe-120">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="caffe-120">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)
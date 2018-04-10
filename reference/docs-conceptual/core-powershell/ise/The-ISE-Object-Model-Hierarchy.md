---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Hierarchie objektového modelu prostředí ISE
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-ise-object-model-hierarchy"></a><span data-ttu-id="f3273-103">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="f3273-103">The ISE Object Model Hierarchy</span></span>

<span data-ttu-id="f3273-104">Toto téma ukazuje hierarchii objektů, které jsou součástí systému Windows PowerShell Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="f3273-104">This topic shows the hierarchy of objects that are part of Windows PowerShell Integrated Scripting Environment (ISE).</span></span>
<span data-ttu-id="f3273-105">Windows PowerShell ISE je součástí prostředí Windows PowerShell 3.0 a v prostředí Windows PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="f3273-105">Windows PowerShell ISE is included in Windows PowerShell 3.0 and in Windows PowerShell 4.0.</span></span>
<span data-ttu-id="f3273-106">Klikněte na objekt tak, aby vás zavedou na referenční dokumentaci k nástroji pro třídu, která definuje objekt.</span><span class="sxs-lookup"><span data-stu-id="f3273-106">Click an object to take you to the reference documentation for the class that defines the object.</span></span>

## <a name="psise-object"></a><span data-ttu-id="f3273-107">objekt $psISE</span><span class="sxs-lookup"><span data-stu-id="f3273-107">$psISE Object</span></span>

<span data-ttu-id="f3273-108">**$PsISE** objekt je [kořenový objekt](The-ObjectModelRoot-Object.md) hierarchie objektů Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f3273-108">The **$psISE** object is the [root object](The-ObjectModelRoot-Object.md) of the Windows PowerShell ISE object hierarchy.</span></span>
<span data-ttu-id="f3273-109">Umístěný na nejvyšší úrovni, se zpřístupní následující objekty pro skriptování:</span><span class="sxs-lookup"><span data-stu-id="f3273-109">Located at the top level, it makes the following objects available for scripting:</span></span>

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[<span data-ttu-id="f3273-110">$psISE.CurrentFile</span><span class="sxs-lookup"><span data-stu-id="f3273-110">$psISE.CurrentFile</span></span>](The-ISEFile-Object.md)

<span data-ttu-id="f3273-111">**$PsISE.CurrentFile** objekt je instance [ISEFile](The-ISEFile-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="f3273-111">The **$psISE.CurrentFile** object is an instance of the [ISEFile](The-ISEFile-Object.md) class.</span></span>

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[<span data-ttu-id="f3273-112">$psISE.CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="f3273-112">$psISE.CurrentPowerShellTab</span></span>](The-PowerShellTab-Object.md)

<span data-ttu-id="f3273-113">**$PsISE.CurrentPowerShellTab** objekt je instance [PowerShellTab](The-PowerShellTab-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="f3273-113">The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="psisecurrentvisiblehorizontaltool"></a><span data-ttu-id="f3273-114">$psISE.CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="f3273-114">$psISE.CurrentVisibleHorizontalTool</span></span>

<span data-ttu-id="f3273-115">**$PsISE.CurrentVisibleHorizontalTool** objekt je instance [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="f3273-115">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="f3273-116">Reprezentuje nástroj nainstalovaný doplněk, který je aktuálně ukotven na horní okraj okna Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f3273-116">It represents the installed add-on tool that is currently docked to the top edge of the Windows PowerShell ISE window.</span></span>

## <a name="psisecurrentvisibleverticaltool"></a><span data-ttu-id="f3273-117">$psISE.CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="f3273-117">$psISE.CurrentVisibleVerticalTool</span></span>

<span data-ttu-id="f3273-118">**$PsISE.CurrentVisibleHorizontalTool** objekt je instance [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="f3273-118">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="f3273-119">Reprezentuje nástroj nainstalovaný doplněk, který je aktuálně ukotven pravé hrany okna Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f3273-119">It represents the installed add-on tool that is currently docked to the right-hand edge of the Windows PowerShell ISE window.</span></span>

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[<span data-ttu-id="f3273-120">$psISE.Options</span><span class="sxs-lookup"><span data-stu-id="f3273-120">$psISE.Options</span></span>](The-ISEOptions-Object.md)

<span data-ttu-id="f3273-121">**$PsISE.Options** objekt je instance [ISEOptions](The-ISEOptions-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="f3273-121">The **$psISE.Options** object is an instance of the [ISEOptions](The-ISEOptions-Object.md) class.</span></span>
<span data-ttu-id="f3273-122">Objekt ISEOptions představuje různá nastavení pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f3273-122">The ISEOptions object represents various settings for Windows PowerShell ISE.</span></span>
<span data-ttu-id="f3273-123">Je instance třídy Microsoft.PowerShell.Host.ISE.ISEOptions.</span><span class="sxs-lookup"><span data-stu-id="f3273-123">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEOptions class.</span></span>

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[<span data-ttu-id="f3273-124">$psISE.PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="f3273-124">$psISE.PowerShellTabs</span></span>](The-PowerShellTabCollection-Object.md)

<span data-ttu-id="f3273-125">**$PsISE.PowerShellTabs** objekt je instance [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="f3273-125">The **$psISE.PowerShellTabs** object is an instance of the [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) class.</span></span>
<span data-ttu-id="f3273-126">Jedná se o kolekci všechny aktuálně otevřené prostředí PowerShell karet, které představují spustit prostředí v místním počítači nebo na vzdálených počítačích připojených k dispozici prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3273-126">It is a collection of all the currently open PowerShell tabs that represent the available Windows PowerShell run environments on the local computer or on connected remote computers.</span></span>
<span data-ttu-id="f3273-127">Každý člen v kolekci je instance [PowerShellTab](The-PowerShellTab-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="f3273-127">Each member in the collection is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="f3273-128">Viz také</span><span class="sxs-lookup"><span data-stu-id="f3273-128">See Also</span></span>

- [<span data-ttu-id="f3273-129">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="f3273-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="f3273-130">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="f3273-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
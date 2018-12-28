---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Hierarchie objektového modelu prostředí ISE
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403869"
---
# <a name="the-ise-object-model-hierarchy"></a><span data-ttu-id="08e68-103">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="08e68-103">The ISE Object Model Hierarchy</span></span>

<span data-ttu-id="08e68-104">Toto téma ukazuje hierarchii objektů, které jsou součástí sady Windows Powershellu integrovaném skriptovacím prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="08e68-104">This topic shows the hierarchy of objects that are part of Windows PowerShell Integrated Scripting Environment (ISE).</span></span>
<span data-ttu-id="08e68-105">Windows PowerShell ISE je součástí Windows PowerShell 3.0 a ve Windows Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="08e68-105">Windows PowerShell ISE is included in Windows PowerShell 3.0 and in Windows PowerShell 4.0.</span></span>
<span data-ttu-id="08e68-106">Klikněte na objekt, které vás přesměrují na referenční dokumentaci pro třídy, která definuje objekt.</span><span class="sxs-lookup"><span data-stu-id="08e68-106">Click an object to take you to the reference documentation for the class that defines the object.</span></span>

## <a name="psise-object"></a><span data-ttu-id="08e68-107">objekt $psISE</span><span class="sxs-lookup"><span data-stu-id="08e68-107">$psISE Object</span></span>

<span data-ttu-id="08e68-108">**$PsISE** je objekt [kořenový objekt](The-ObjectModelRoot-Object.md) hierarchie objektů prostředí PowerShell ISE Windows.</span><span class="sxs-lookup"><span data-stu-id="08e68-108">The **$psISE** object is the [root object](The-ObjectModelRoot-Object.md) of the Windows PowerShell ISE object hierarchy.</span></span>
<span data-ttu-id="08e68-109">Umístěné na nejvyšší úrovni, díky němu následující objekty dostupné pro skriptování:</span><span class="sxs-lookup"><span data-stu-id="08e68-109">Located at the top level, it makes the following objects available for scripting:</span></span>

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[<span data-ttu-id="08e68-110">$psISE.CurrentFile</span><span class="sxs-lookup"><span data-stu-id="08e68-110">$psISE.CurrentFile</span></span>](The-ISEFile-Object.md)

<span data-ttu-id="08e68-111">**$PsISE.CurrentFile** objekt je instancí [ISEFile](The-ISEFile-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="08e68-111">The **$psISE.CurrentFile** object is an instance of the [ISEFile](The-ISEFile-Object.md) class.</span></span>

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[<span data-ttu-id="08e68-112">$psISE.CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="08e68-112">$psISE.CurrentPowerShellTab</span></span>](The-PowerShellTab-Object.md)

<span data-ttu-id="08e68-113">**$PsISE.CurrentPowerShellTab** objekt je instancí [PowerShellTab](The-PowerShellTab-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="08e68-113">The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="psisecurrentvisiblehorizontaltool"></a><span data-ttu-id="08e68-114">$psISE.CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="08e68-114">$psISE.CurrentVisibleHorizontalTool</span></span>

<span data-ttu-id="08e68-115">**$PsISE.CurrentVisibleHorizontalTool** objekt je instancí [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="08e68-115">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="08e68-116">Představuje nástroj nainstalovaný doplněk, který je aktuálně ukotven na horním okraji okna Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="08e68-116">It represents the installed add-on tool that is currently docked to the top edge of the Windows PowerShell ISE window.</span></span>

## <a name="psisecurrentvisibleverticaltool"></a><span data-ttu-id="08e68-117">$psISE.CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="08e68-117">$psISE.CurrentVisibleVerticalTool</span></span>

<span data-ttu-id="08e68-118">**$PsISE.CurrentVisibleHorizontalTool** objekt je instancí [ISEAddOnTool](The-ISEAddOnTool-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="08e68-118">The **$psISE.CurrentVisibleHorizontalTool** object is an instance of the [ISEAddOnTool](The-ISEAddOnTool-Object.md) class.</span></span>
<span data-ttu-id="08e68-119">Představuje nástroj nainstalovaný doplněk, který je aktuálně ukotven na pravém okraji okna Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="08e68-119">It represents the installed add-on tool that is currently docked to the right-hand edge of the Windows PowerShell ISE window.</span></span>

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[<span data-ttu-id="08e68-120">$psISE.Options</span><span class="sxs-lookup"><span data-stu-id="08e68-120">$psISE.Options</span></span>](The-ISEOptions-Object.md)

<span data-ttu-id="08e68-121">**$PsISE.Options** objekt je instancí [ISEOptions](The-ISEOptions-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="08e68-121">The **$psISE.Options** object is an instance of the [ISEOptions](The-ISEOptions-Object.md) class.</span></span>
<span data-ttu-id="08e68-122">Objekt ISEOptions představuje různá nastavení pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="08e68-122">The ISEOptions object represents various settings for Windows PowerShell ISE.</span></span>
<span data-ttu-id="08e68-123">Je instancí třídy Microsoft.PowerShell.Host.ISE.ISEOptions.</span><span class="sxs-lookup"><span data-stu-id="08e68-123">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEOptions class.</span></span>

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[<span data-ttu-id="08e68-124">$psISE.PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="08e68-124">$psISE.PowerShellTabs</span></span>](The-PowerShellTabCollection-Object.md)

<span data-ttu-id="08e68-125">**$PsISE.PowerShellTabs** objekt je instancí [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="08e68-125">The **$psISE.PowerShellTabs** object is an instance of the [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) class.</span></span>
<span data-ttu-id="08e68-126">Jde o kolekci všechny aktuálně otevřené Powershellu karty, které představují k dispozici Windows Powershellu spusťte prostředí v místním počítači nebo na připojených vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="08e68-126">It is a collection of all the currently open PowerShell tabs that represent the available Windows PowerShell run environments on the local computer or on connected remote computers.</span></span>
<span data-ttu-id="08e68-127">Každý člen v kolekci je instance [PowerShellTab](The-PowerShellTab-Object.md) třídy.</span><span class="sxs-lookup"><span data-stu-id="08e68-127">Each member in the collection is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="08e68-128">Viz také</span><span class="sxs-lookup"><span data-stu-id="08e68-128">See Also</span></span>

- [<span data-ttu-id="08e68-129">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="08e68-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="08e68-130">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="08e68-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
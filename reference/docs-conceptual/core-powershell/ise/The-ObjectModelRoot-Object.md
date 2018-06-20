---
ms.date: 08/25/2017
keywords: rutiny prostředí PowerShell
title: Objekt ObjectModelRoot
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954598"
---
# <a name="the-objectmodelroot-object"></a><span data-ttu-id="05172-103">Objekt ObjectModelRoot</span><span class="sxs-lookup"><span data-stu-id="05172-103">The ObjectModelRoot Object</span></span>

<span data-ttu-id="05172-104">**$PsISE** objekt, který je hlavní kořenový objekt ve Windows PowerShell® Integrované skriptovací prostředí (ISE) je instance třídy Microsoft.PowerShell.Host.ISE.ObjectModelRoot.</span><span class="sxs-lookup"><span data-stu-id="05172-104">The **$psISE** object, which is the principal root object in Windows PowerShell® Integrated Scripting Environment (ISE) is an instance of the Microsoft.PowerShell.Host.ISE.ObjectModelRoot class.</span></span>
<span data-ttu-id="05172-105">Toto téma popisuje vlastnosti **ObjectModelRoot** objektu.</span><span class="sxs-lookup"><span data-stu-id="05172-105">This topic describes the properties of the **ObjectModelRoot** object.</span></span>

## <a name="properties"></a><span data-ttu-id="05172-106">Properties</span><span class="sxs-lookup"><span data-stu-id="05172-106">Properties</span></span>

### <a name="currentfile"></a><span data-ttu-id="05172-107">CurrentFile</span><span class="sxs-lookup"><span data-stu-id="05172-107">CurrentFile</span></span>

> <span data-ttu-id="05172-108">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="05172-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="05172-109">Vlastnost jen pro čtení, získá soubor, který je přidružen k tomuto objektu hostitele, který je aktuálně aktivní.</span><span class="sxs-lookup"><span data-stu-id="05172-109">The read-only property that gets the file, which is associated with this host object that currently has the focus.</span></span>

### <a name="currentpowershelltab"></a><span data-ttu-id="05172-110">CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="05172-110">CurrentPowerShellTab</span></span>

> <span data-ttu-id="05172-111">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="05172-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="05172-112">Vlastnost jen pro čtení, získá kartě prostředí PowerShell, který je aktivní.</span><span class="sxs-lookup"><span data-stu-id="05172-112">The read-only property that gets the PowerShell tab that has the focus.</span></span>

### <a name="currentvisiblehorizontaltool"></a><span data-ttu-id="05172-113">CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="05172-113">CurrentVisibleHorizontalTool</span></span>

> <span data-ttu-id="05172-114">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="05172-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="05172-115">Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj rozšíření Windows PowerShell ISE, který se nachází v podokně vodorovné nástrojů v dolní části editoru.</span><span class="sxs-lookup"><span data-stu-id="05172-115">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the horizontal tool pane at the bottom of the editor.</span></span>

### <a name="currentvisibleverticaltool"></a><span data-ttu-id="05172-116">CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="05172-116">CurrentVisibleVerticalTool</span></span>

> <span data-ttu-id="05172-117">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="05172-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="05172-118">Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj rozšíření Windows PowerShell ISE, který se nachází v podokně svislý nástroj na pravé straně editoru.</span><span class="sxs-lookup"><span data-stu-id="05172-118">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the vertical tool pane on the right side of the editor.</span></span>

### <a name="options"></a><span data-ttu-id="05172-119">Možnosti</span><span class="sxs-lookup"><span data-stu-id="05172-119">Options</span></span>

> <span data-ttu-id="05172-120">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="05172-120">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="05172-121">Vlastnost jen pro čtení, který získá různé možnosti, které mohou změnit nastavení v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="05172-121">The read-only property that gets the various options that can change settings in Windows PowerShell ISE.</span></span>

### <a name="powershelltabs"></a><span data-ttu-id="05172-122">PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="05172-122">PowerShellTabs</span></span>

> <span data-ttu-id="05172-123">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="05172-123">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="05172-124">Vlastnost jen pro čtení, získá kolekci karet prostředí PowerShell, které jsou otevřeny v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="05172-124">The read-only property that gets the collection of the PowerShell tabs, which are open in Windows PowerShell ISE.</span></span> <span data-ttu-id="05172-125">Ve výchozím nastavení tento objekt obsahuje jedné karty prostředí PowerShell. Můžete ale přidat další karty prostředí PowerShell k tomuto objektu, pomocí skriptů nebo pomocí nabídek v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="05172-125">By default, this object contains one PowerShell tab. However, you can add more PowerShell tabs to this object by using scripts or by using the menus in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="05172-126">Viz také</span><span class="sxs-lookup"><span data-stu-id="05172-126">See Also</span></span>

- [<span data-ttu-id="05172-127">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="05172-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="05172-128">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="05172-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
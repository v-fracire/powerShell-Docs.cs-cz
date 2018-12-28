---
ms.date: 08/25/2017
keywords: rutiny prostředí PowerShell
title: Objekt ObjectModelRoot
ms.openlocfilehash: 2670321ebac1eac4ecc8457afb796f9f260da471
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404106"
---
# <a name="the-objectmodelroot-object"></a><span data-ttu-id="af194-103">Objekt ObjectModelRoot</span><span class="sxs-lookup"><span data-stu-id="af194-103">The ObjectModelRoot Object</span></span>

<span data-ttu-id="af194-104">**$PsISE** instance třídy Microsoft.PowerShell.Host.ISE.ObjectModelRoot je objekt, který je hlavní kořenový objekt ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="af194-104">The **$psISE** object, which is the principal root object in Windows PowerShell® Integrated Scripting Environment (ISE) is an instance of the Microsoft.PowerShell.Host.ISE.ObjectModelRoot class.</span></span>
<span data-ttu-id="af194-105">Toto téma popisuje vlastnosti **ObjectModelRoot** objektu.</span><span class="sxs-lookup"><span data-stu-id="af194-105">This topic describes the properties of the **ObjectModelRoot** object.</span></span>

## <a name="properties"></a><span data-ttu-id="af194-106">Properties</span><span class="sxs-lookup"><span data-stu-id="af194-106">Properties</span></span>

### <a name="currentfile"></a><span data-ttu-id="af194-107">CurrentFile</span><span class="sxs-lookup"><span data-stu-id="af194-107">CurrentFile</span></span>

> <span data-ttu-id="af194-108">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="af194-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="af194-109">Vlastnost jen pro čtení, která načte soubor, který je spojen s tímto objektem hostitele, který má aktuálně fokus.</span><span class="sxs-lookup"><span data-stu-id="af194-109">The read-only property that gets the file, which is associated with this host object that currently has the focus.</span></span>

### <a name="currentpowershelltab"></a><span data-ttu-id="af194-110">CurrentPowerShellTab</span><span class="sxs-lookup"><span data-stu-id="af194-110">CurrentPowerShellTab</span></span>

> <span data-ttu-id="af194-111">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="af194-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="af194-112">Vlastnost jen pro čtení, který získává PowerShell tab, ke kterému má fokus.</span><span class="sxs-lookup"><span data-stu-id="af194-112">The read-only property that gets the PowerShell tab that has the focus.</span></span>

### <a name="currentvisiblehorizontaltool"></a><span data-ttu-id="af194-113">CurrentVisibleHorizontalTool</span><span class="sxs-lookup"><span data-stu-id="af194-113">CurrentVisibleHorizontalTool</span></span>

> <span data-ttu-id="af194-114">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="af194-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="af194-115">Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj Windows PowerShell ISE doplněk, který se nachází v podokně nástroj vodorovný v dolní části editoru.</span><span class="sxs-lookup"><span data-stu-id="af194-115">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the horizontal tool pane at the bottom of the editor.</span></span>

### <a name="currentvisibleverticaltool"></a><span data-ttu-id="af194-116">CurrentVisibleVerticalTool</span><span class="sxs-lookup"><span data-stu-id="af194-116">CurrentVisibleVerticalTool</span></span>

> <span data-ttu-id="af194-117">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="af194-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="af194-118">Vlastnost jen pro čtení, který získá aktuálně viditelné nástroj Windows PowerShell ISE doplněk, který se nachází v podokně svislý nástroj na pravé straně editoru.</span><span class="sxs-lookup"><span data-stu-id="af194-118">The read-only property that gets the currently visible Windows PowerShell ISE add-on tool that is located in the vertical tool pane on the right side of the editor.</span></span>

### <a name="options"></a><span data-ttu-id="af194-119">Možnosti</span><span class="sxs-lookup"><span data-stu-id="af194-119">Options</span></span>

> <span data-ttu-id="af194-120">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="af194-120">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="af194-121">Vlastnost jen pro čtení, který získá různé možnosti, které můžete změnit nastavení v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="af194-121">The read-only property that gets the various options that can change settings in Windows PowerShell ISE.</span></span>

### <a name="powershelltabs"></a><span data-ttu-id="af194-122">PowerShellTabs</span><span class="sxs-lookup"><span data-stu-id="af194-122">PowerShellTabs</span></span>

> <span data-ttu-id="af194-123">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="af194-123">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="af194-124">Vlastnost jen pro čtení, která získá kolekci karet prostředí PowerShell, které jsou otevřeny v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="af194-124">The read-only property that gets the collection of the PowerShell tabs, which are open in Windows PowerShell ISE.</span></span> <span data-ttu-id="af194-125">Ve výchozím nastavení tento objekt obsahuje jedné karty Powershellu. Můžete však přidat další karty Powershellu k tomuto objektu, pomocí skriptů nebo použijte nabídky v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="af194-125">By default, this object contains one PowerShell tab. However, you can add more PowerShell tabs to this object by using scripts or by using the menus in Windows PowerShell ISE.</span></span>

## <a name="see-also"></a><span data-ttu-id="af194-126">Viz také</span><span class="sxs-lookup"><span data-stu-id="af194-126">See Also</span></span>

- [<span data-ttu-id="af194-127">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="af194-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="af194-128">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="af194-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
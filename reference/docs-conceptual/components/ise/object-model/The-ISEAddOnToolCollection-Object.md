---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEAddOnToolCollection
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ff4f19d1a85a592f2f4f09c62caa0971751bdff7
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403870"
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="144c7-103">Objekt ISEAddOnToolCollection</span><span class="sxs-lookup"><span data-stu-id="144c7-103">The ISEAddOnToolCollection Object</span></span>

<span data-ttu-id="144c7-104">**ISEAddOnToolCollection** objektu je kolekce **ISEAddOnTool** objekty.</span><span class="sxs-lookup"><span data-stu-id="144c7-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="144c7-105">Příkladem je **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektu.</span><span class="sxs-lookup"><span data-stu-id="144c7-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="144c7-106">Metody</span><span class="sxs-lookup"><span data-stu-id="144c7-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="144c7-107">Přidat\( název, ControlType, \[IsVisible\] \)</span><span class="sxs-lookup"><span data-stu-id="144c7-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>

<span data-ttu-id="144c7-108">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="144c7-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="144c7-109">Přidá nový nástroj doplněk do kolekce.</span><span class="sxs-lookup"><span data-stu-id="144c7-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="144c7-110">Vrací doplněk nově přidaný nástroj.</span><span class="sxs-lookup"><span data-stu-id="144c7-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="144c7-111">Před spuštěním tohoto příkazu, musíte nainstalovat doplněk nástroje v místním počítači a načtení sestavení.</span><span class="sxs-lookup"><span data-stu-id="144c7-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

<span data-ttu-id="144c7-112">**Název** -řetězec Určuje zobrazovaný název doplňku nástroj, který se přidá do prostředí PowerShell ISE Windows.</span><span class="sxs-lookup"><span data-stu-id="144c7-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

<span data-ttu-id="144c7-113">**ControlType** – Určuje typ ovládacího prvku, který je přidán.</span><span class="sxs-lookup"><span data-stu-id="144c7-113">**ControlType** -Type Specifies the control that is added.</span></span>

<span data-ttu-id="144c7-114">**\[IsVisible\]**  – volitelný logický-li nastavena na **$true**, nástroj pro doplněk je okamžitě viditelné v podokně související nástroje.</span><span class="sxs-lookup"><span data-stu-id="144c7-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="144c7-115">Odebrat\( položky \)</span><span class="sxs-lookup"><span data-stu-id="144c7-115">Remove\( Item \)</span></span>

<span data-ttu-id="144c7-116">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="144c7-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="144c7-117">Odebere nástroj zadaný doplněk z kolekce.</span><span class="sxs-lookup"><span data-stu-id="144c7-117">Removes the specified add-on tool from the collection.</span></span>

<span data-ttu-id="144c7-118">**Položka** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool určuje objekt, který má být odebrán z Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="144c7-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="144c7-119">SetSelectedPowerShellTab\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="144c7-119">SetSelectedPowerShellTab\( psTab \)</span></span>

<span data-ttu-id="144c7-120">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="144c7-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="144c7-121">Vybere prostředí PowerShell karty, která **psTab** parametrem.</span><span class="sxs-lookup"><span data-stu-id="144c7-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="144c7-122">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab Powershellu kartu k výběru.</span><span class="sxs-lookup"><span data-stu-id="144c7-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a><span data-ttu-id="144c7-123">Odebrat\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="144c7-123">Remove\( psTab \)</span></span>

<span data-ttu-id="144c7-124">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="144c7-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="144c7-125">Odebere prostředí PowerShell karty, která **psTab** parametrem.</span><span class="sxs-lookup"><span data-stu-id="144c7-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="144c7-126">**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab Powershellu odebrat.</span><span class="sxs-lookup"><span data-stu-id="144c7-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="144c7-127">Viz také</span><span class="sxs-lookup"><span data-stu-id="144c7-127">See Also</span></span>

- [<span data-ttu-id="144c7-128">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="144c7-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="144c7-129">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="144c7-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="144c7-130">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="144c7-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
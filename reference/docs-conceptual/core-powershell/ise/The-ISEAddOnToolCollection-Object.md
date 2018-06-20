---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEAddOnToolCollection
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ff4f19d1a85a592f2f4f09c62caa0971751bdff7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953051"
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="0494c-103">Objekt ISEAddOnToolCollection</span><span class="sxs-lookup"><span data-stu-id="0494c-103">The ISEAddOnToolCollection Object</span></span>

<span data-ttu-id="0494c-104">**ISEAddOnToolCollection** objektu je kolekce **ISEAddOnTool** objekty.</span><span class="sxs-lookup"><span data-stu-id="0494c-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="0494c-105">Příkladem je **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektu.</span><span class="sxs-lookup"><span data-stu-id="0494c-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="0494c-106">Metody</span><span class="sxs-lookup"><span data-stu-id="0494c-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="0494c-107">Přidat\( název, ControlType, \[IsVisible\] \)</span><span class="sxs-lookup"><span data-stu-id="0494c-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>

<span data-ttu-id="0494c-108">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="0494c-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="0494c-109">Přidá nový nástroj rozšíření do kolekce.</span><span class="sxs-lookup"><span data-stu-id="0494c-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="0494c-110">Vrátí nástroj nově přidaného rozšíření.</span><span class="sxs-lookup"><span data-stu-id="0494c-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="0494c-111">Než spustíte tento příkaz, musíte nainstalovat nástroje rozšíření v místním počítači a načtení sestavení.</span><span class="sxs-lookup"><span data-stu-id="0494c-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

<span data-ttu-id="0494c-112">**Název** -řetězec Určuje zobrazovaný název rozšíření nástroj, který je přidán do systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="0494c-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

<span data-ttu-id="0494c-113">**ControlType** – typ určuje ovládací prvek, který je přidán.</span><span class="sxs-lookup"><span data-stu-id="0494c-113">**ControlType** -Type Specifies the control that is added.</span></span>

<span data-ttu-id="0494c-114">**\[IsVisible –\]**  -volitelné Boolean Pokud nastavit **$true**, nástroj rozšíření je okamžitě viditelné v podokně související nástroje.</span><span class="sxs-lookup"><span data-stu-id="0494c-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="0494c-115">Odebrat\( položky \)</span><span class="sxs-lookup"><span data-stu-id="0494c-115">Remove\( Item \)</span></span>

<span data-ttu-id="0494c-116">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="0494c-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="0494c-117">Odebere zadané rozšíření nástroj z kolekce.</span><span class="sxs-lookup"><span data-stu-id="0494c-117">Removes the specified add-on tool from the collection.</span></span>

<span data-ttu-id="0494c-118">**Položka** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool určuje objekt, který má být odebrán ze systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="0494c-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="0494c-119">SetSelectedPowerShellTab\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="0494c-119">SetSelectedPowerShellTab\( psTab \)</span></span>

<span data-ttu-id="0494c-120">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="0494c-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="0494c-121">Vybere PowerShell kartě **psTab** parametrem.</span><span class="sxs-lookup"><span data-stu-id="0494c-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="0494c-122">**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab prostředí PowerShell k výběru.</span><span class="sxs-lookup"><span data-stu-id="0494c-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a><span data-ttu-id="0494c-123">Odebrat\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="0494c-123">Remove\( psTab \)</span></span>

<span data-ttu-id="0494c-124">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="0494c-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="0494c-125">Odebere PowerShell kartě **psTab** parametrem.</span><span class="sxs-lookup"><span data-stu-id="0494c-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="0494c-126">**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab prostředí PowerShell k odebrání.</span><span class="sxs-lookup"><span data-stu-id="0494c-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="0494c-127">Viz také</span><span class="sxs-lookup"><span data-stu-id="0494c-127">See Also</span></span>

- [<span data-ttu-id="0494c-128">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="0494c-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="0494c-129">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="0494c-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="0494c-130">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="0494c-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
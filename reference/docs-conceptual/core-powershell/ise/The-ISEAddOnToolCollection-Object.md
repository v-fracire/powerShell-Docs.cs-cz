---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEAddOnToolCollection
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ba8b4e0e3952226407f00dea8b32785633256089
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="90995-103">Objekt ISEAddOnToolCollection</span><span class="sxs-lookup"><span data-stu-id="90995-103">The ISEAddOnToolCollection Object</span></span>
  <span data-ttu-id="90995-104">**ISEAddOnToolCollection** objektu je kolekce **ISEAddOnTool** objekty.</span><span class="sxs-lookup"><span data-stu-id="90995-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="90995-105">Příkladem je **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektu.</span><span class="sxs-lookup"><span data-stu-id="90995-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="90995-106">Metody</span><span class="sxs-lookup"><span data-stu-id="90995-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="90995-107">Přidat\( název, ControlType, \[IsVisible\]\)</span><span class="sxs-lookup"><span data-stu-id="90995-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>
  <span data-ttu-id="90995-108">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="90995-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="90995-109">Přidá nový nástroj rozšíření do kolekce.</span><span class="sxs-lookup"><span data-stu-id="90995-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="90995-110">Vrátí nástroj nově přidaného rozšíření.</span><span class="sxs-lookup"><span data-stu-id="90995-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="90995-111">Než spustíte tento příkaz, musíte nainstalovat nástroje rozšíření v místním počítači a načtení sestavení.</span><span class="sxs-lookup"><span data-stu-id="90995-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

 <span data-ttu-id="90995-112">**Název** -řetězec Určuje zobrazovaný název rozšíření nástroj, který je přidán do systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="90995-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

 <span data-ttu-id="90995-113">**ControlType** – typ určuje ovládací prvek, který je přidán.</span><span class="sxs-lookup"><span data-stu-id="90995-113">**ControlType** -Type Specifies the control that is added.</span></span>

 <span data-ttu-id="90995-114">**\[IsVisible –\]**  -volitelné Boolean Pokud nastavit **$true**, nástroj rozšíření je okamžitě viditelné v podokně související nástroje.</span><span class="sxs-lookup"><span data-stu-id="90995-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="90995-115">Odebrat\( položky\)</span><span class="sxs-lookup"><span data-stu-id="90995-115">Remove\( Item \)</span></span>
  <span data-ttu-id="90995-116">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="90995-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="90995-117">Odebere zadané rozšíření nástroj z kolekce.</span><span class="sxs-lookup"><span data-stu-id="90995-117">Removes the specified add-on tool from the collection.</span></span>

 <span data-ttu-id="90995-118">**Položka** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool určuje objekt, který má být odebrán ze systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="90995-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="90995-119">SetSelectedPowerShellTab\( psTab\)</span><span class="sxs-lookup"><span data-stu-id="90995-119">SetSelectedPowerShellTab\( psTab \)</span></span>
  <span data-ttu-id="90995-120">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="90995-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="90995-121">Vybere PowerShell kartě **psTab** parametrem.</span><span class="sxs-lookup"><span data-stu-id="90995-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

 <span data-ttu-id="90995-122">**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab prostředí PowerShell k výběru.</span><span class="sxs-lookup"><span data-stu-id="90995-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
      $newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

### <a name="remove-pstab-"></a><span data-ttu-id="90995-123">Odebrat\( psTab\)</span><span class="sxs-lookup"><span data-stu-id="90995-123">Remove\( psTab \)</span></span>
  <span data-ttu-id="90995-124">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="90995-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="90995-125">Odebere PowerShell kartě **psTab** parametrem.</span><span class="sxs-lookup"><span data-stu-id="90995-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

 <span data-ttu-id="90995-126">**psTab** – karta Microsoft.PowerShell.Host.ISE.PowerShellTab prostředí PowerShell k odebrání.</span><span class="sxs-lookup"><span data-stu-id="90995-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="90995-127">Viz také</span><span class="sxs-lookup"><span data-stu-id="90995-127">See Also</span></span>
- [<span data-ttu-id="90995-128">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="90995-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="90995-129">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="90995-129">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="90995-130">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="90995-130">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="90995-131">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="90995-131">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  

---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt PowerShellTabCollection
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: dcdc16ae126453b6ade64917ac4950cc05e5f8ad
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="682d7-103">Objekt PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="682d7-103">The PowerShellTabCollection Object</span></span>
  <span data-ttu-id="682d7-104">**PowerShellTab** objektu kolekce je kolekce **PowerShellTab** objekty.</span><span class="sxs-lookup"><span data-stu-id="682d7-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="682d7-105">Každý **PowerShellTab** objekt funguje jako samostatné běhového prostředí.</span><span class="sxs-lookup"><span data-stu-id="682d7-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="682d7-106">Je instance třídy Microsoft.PowerShell.Host.ISE.PowerShellTabs.</span><span class="sxs-lookup"><span data-stu-id="682d7-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="682d7-107">Příkladem je **$psISE.PowerShellTabs** objektu.</span><span class="sxs-lookup"><span data-stu-id="682d7-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="682d7-108">Metody</span><span class="sxs-lookup"><span data-stu-id="682d7-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="682d7-109">Přidat\(\)</span><span class="sxs-lookup"><span data-stu-id="682d7-109">Add\(\)</span></span>
  <span data-ttu-id="682d7-110">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="682d7-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="682d7-111">Přidá novou kartu prostředí PowerShell do kolekce.</span><span class="sxs-lookup"><span data-stu-id="682d7-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="682d7-112">Vrátí kartě nově přidaný.</span><span class="sxs-lookup"><span data-stu-id="682d7-112">It returns the newly added tab.</span></span>

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="682d7-113">Odebrat\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="682d7-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>
  <span data-ttu-id="682d7-114">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="682d7-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="682d7-115">Odebere kartu, která je zadána **psTab** parametr.</span><span class="sxs-lookup"><span data-stu-id="682d7-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

 <span data-ttu-id="682d7-116">**psTab** karty prostředí PowerShell k odebrání.</span><span class="sxs-lookup"><span data-stu-id="682d7-116">**psTab** The PowerShell tab to remove.</span></span>

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="682d7-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="682d7-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>
  <span data-ttu-id="682d7-118">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="682d7-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="682d7-119">Vybere kartě prostředí PowerShell, která je zadána **psTab** parametr aby kartě aktuálně aktivní prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="682d7-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

 <span data-ttu-id="682d7-120">**psTab** karty prostředí PowerShell k výběru.</span><span class="sxs-lookup"><span data-stu-id="682d7-120">**psTab** The PowerShell tab to select.</span></span>

```
# Save the current tab in a variable and rename it
$OldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName="Old Tab"
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab" 
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab=$oldtab
```

## <a name="see-also"></a><span data-ttu-id="682d7-121">Viz také</span><span class="sxs-lookup"><span data-stu-id="682d7-121">See Also</span></span>
- [<span data-ttu-id="682d7-122">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="682d7-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="682d7-123">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="682d7-123">The Windows PowerShell ISE Scripting Object Model</span></span>](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="682d7-124">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="682d7-124">Windows PowerShell ISE Object Model Reference</span></span>](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="682d7-125">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="682d7-125">The ISE Object Model Hierarchy</span></span>](../ise/The-ISE-Object-Model-Hierarchy.md)

  

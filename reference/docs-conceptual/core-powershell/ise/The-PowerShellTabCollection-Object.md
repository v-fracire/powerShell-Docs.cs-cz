---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt PowerShellTabCollection
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="1b481-103">Objekt PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="1b481-103">The PowerShellTabCollection Object</span></span>

<span data-ttu-id="1b481-104">**PowerShellTab** objektu kolekce je kolekce **PowerShellTab** objekty.</span><span class="sxs-lookup"><span data-stu-id="1b481-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="1b481-105">Každý **PowerShellTab** objekt funguje jako samostatné běhového prostředí.</span><span class="sxs-lookup"><span data-stu-id="1b481-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="1b481-106">Je instance třídy Microsoft.PowerShell.Host.ISE.PowerShellTabs.</span><span class="sxs-lookup"><span data-stu-id="1b481-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="1b481-107">Příkladem je **$psISE.PowerShellTabs** objektu.</span><span class="sxs-lookup"><span data-stu-id="1b481-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="1b481-108">Metody</span><span class="sxs-lookup"><span data-stu-id="1b481-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="1b481-109">Přidat\(\)</span><span class="sxs-lookup"><span data-stu-id="1b481-109">Add\(\)</span></span>

<span data-ttu-id="1b481-110">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1b481-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1b481-111">Přidá novou kartu prostředí PowerShell do kolekce.</span><span class="sxs-lookup"><span data-stu-id="1b481-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="1b481-112">Vrátí kartě nově přidaný.</span><span class="sxs-lookup"><span data-stu-id="1b481-112">It returns the newly added tab.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="1b481-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="1b481-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="1b481-114">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1b481-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1b481-115">Odebere kartu, která je zadána **psTab** parametr.</span><span class="sxs-lookup"><span data-stu-id="1b481-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

<span data-ttu-id="1b481-116">**psTab** karty prostředí PowerShell k odebrání.</span><span class="sxs-lookup"><span data-stu-id="1b481-116">**psTab** The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="1b481-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="1b481-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="1b481-118">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="1b481-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1b481-119">Vybere kartě prostředí PowerShell, která je zadána **psTab** parametr aby kartě aktuálně aktivní prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b481-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

<span data-ttu-id="1b481-120">**psTab** karty prostředí PowerShell k výběru.</span><span class="sxs-lookup"><span data-stu-id="1b481-120">**psTab** The PowerShell tab to select.</span></span>

```powershell
# Save the current tab in a variable and rename it
$oldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName = 'Old Tab'
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab = $oldTab
```

## <a name="see-also"></a><span data-ttu-id="1b481-121">Viz také</span><span class="sxs-lookup"><span data-stu-id="1b481-121">See Also</span></span>

- [<span data-ttu-id="1b481-122">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="1b481-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="1b481-123">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="1b481-123">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="1b481-124">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="1b481-124">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt PowerShellTabCollection
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403874"
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="1b981-103">Objekt PowerShellTabCollection</span><span class="sxs-lookup"><span data-stu-id="1b981-103">The PowerShellTabCollection Object</span></span>

<span data-ttu-id="1b981-104">**PowerShellTab** objektu kolekce je kolekce **PowerShellTab** objekty.</span><span class="sxs-lookup"><span data-stu-id="1b981-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="1b981-105">Každý **PowerShellTab** objekt funguje jako samostatné běhové prostředí.</span><span class="sxs-lookup"><span data-stu-id="1b981-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="1b981-106">Je instancí třídy Microsoft.PowerShell.Host.ISE.PowerShellTabs.</span><span class="sxs-lookup"><span data-stu-id="1b981-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="1b981-107">Příkladem je **$psISE.PowerShellTabs** objektu.</span><span class="sxs-lookup"><span data-stu-id="1b981-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="1b981-108">Metody</span><span class="sxs-lookup"><span data-stu-id="1b981-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="1b981-109">Přidat\(\)</span><span class="sxs-lookup"><span data-stu-id="1b981-109">Add\(\)</span></span>

<span data-ttu-id="1b981-110">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="1b981-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1b981-111">Na nové kartě Powershellu přidá do kolekce.</span><span class="sxs-lookup"><span data-stu-id="1b981-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="1b981-112">Vrátí nově přidanou kartu.</span><span class="sxs-lookup"><span data-stu-id="1b981-112">It returns the newly added tab.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="1b981-113">Odebrat\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="1b981-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="1b981-114">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="1b981-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1b981-115">Odebere kartu, která je zadána **psTab** parametru.</span><span class="sxs-lookup"><span data-stu-id="1b981-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

<span data-ttu-id="1b981-116">**psTab** karty Powershellu k odebrání.</span><span class="sxs-lookup"><span data-stu-id="1b981-116">**psTab** The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="1b981-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="1b981-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="1b981-118">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="1b981-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="1b981-119">Vybere PowerShell tab, která je zadána **psTab** k němu na aktivní kartě prostředí PowerShell parametr.</span><span class="sxs-lookup"><span data-stu-id="1b981-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

<span data-ttu-id="1b981-120">**psTab** Powershellu kartu k výběru.</span><span class="sxs-lookup"><span data-stu-id="1b981-120">**psTab** The PowerShell tab to select.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="1b981-121">Viz také</span><span class="sxs-lookup"><span data-stu-id="1b981-121">See Also</span></span>

- [<span data-ttu-id="1b981-122">Objekt PowerShellTab</span><span class="sxs-lookup"><span data-stu-id="1b981-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="1b981-123">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="1b981-123">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="1b981-124">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="1b981-124">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
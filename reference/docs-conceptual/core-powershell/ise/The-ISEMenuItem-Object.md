---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEMenuItem
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 5561955040e56110a6af0619c286548f5812fb47
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="98617-103">Objekt ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="98617-103">The ISEMenuItem Object</span></span>
  <span data-ttu-id="98617-104">**ISEMenuItem** objekt je instance třídy Microsoft.PowerShell.Host.ISE.ISEMenuItem.</span><span class="sxs-lookup"><span data-stu-id="98617-104">An **ISEMenuItem** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItem class.</span></span> <span data-ttu-id="98617-105">Všechny objekty nabídky na **doplňky** nabídky jsou instancemi třídy **Microsoft.PowerShell.Host.ISE.ISEMenuItem** třídy.</span><span class="sxs-lookup"><span data-stu-id="98617-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="98617-106">Properties</span><span class="sxs-lookup"><span data-stu-id="98617-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="98617-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="98617-107">DisplayName</span></span>
  <span data-ttu-id="98617-108">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="98617-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="98617-109">Vlastnost jen pro čtení, získá zobrazovaný název položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="98617-109">The read-only property that gets the display name of the menu item.</span></span>

```
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName

```

### <a name="action"></a><span data-ttu-id="98617-110">Akce</span><span class="sxs-lookup"><span data-stu-id="98617-110">Action</span></span>
  <span data-ttu-id="98617-111">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="98617-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="98617-112">Vlastnost jen pro čtení, získá blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="98617-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="98617-113">Po kliknutí na položku nabídky vyvolá akci.</span><span class="sxs-lookup"><span data-stu-id="98617-113">It invokes the action when you click the menu item.</span></span>

```
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item 
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="98617-114">Zástupce</span><span class="sxs-lookup"><span data-stu-id="98617-114">Shortcut</span></span>
  <span data-ttu-id="98617-115">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="98617-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="98617-116">Vlastnost jen pro čtení, který získá Windows zadejte klávesové zkratky pro položku nabídky.</span><span class="sxs-lookup"><span data-stu-id="98617-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="98617-117">Dílčích</span><span class="sxs-lookup"><span data-stu-id="98617-117">Submenus</span></span>
  <span data-ttu-id="98617-118">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="98617-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="98617-119">Vlastnost jen pro čtení, který získá [seznam dílčích](The-ISEMenuItemCollection-Object.md) položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="98617-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="98617-120">Příklad skriptování</span><span class="sxs-lookup"><span data-stu-id="98617-120">Scripting example</span></span>
 <span data-ttu-id="98617-121">Abyste lépe pochopili, použití v nabídce doplňky a jeho Skriptovatelná vlastnosti, přečíst v následujícím příkladu skriptování.</span><span class="sxs-lookup"><span data-stu-id="98617-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```

# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu - a parent and a child submenu item. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")

```

## <a name="see-also"></a><span data-ttu-id="98617-122">Viz také</span><span class="sxs-lookup"><span data-stu-id="98617-122">See Also</span></span>
- [<span data-ttu-id="98617-123">Objekt ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="98617-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md) 
- [<span data-ttu-id="98617-124">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="98617-124">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="98617-125">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="98617-125">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [<span data-ttu-id="98617-126">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="98617-126">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

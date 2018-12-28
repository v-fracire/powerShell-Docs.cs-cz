---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEMenuItem
ms.assetid: a16660bd-0aee-46fd-ac17-3f022165d089
ms.openlocfilehash: 556f88117c07100b1734c8ffd8956dce6efe6fb1
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404081"
---
# <a name="the-isemenuitem-object"></a><span data-ttu-id="219b0-103">Objekt ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="219b0-103">The ISEMenuItem Object</span></span>

<span data-ttu-id="219b0-104">**ISEMenuItem** je objekt instancí třídy Microsoft.PowerShell.Host.ISE.ISEMenuItem.</span><span class="sxs-lookup"><span data-stu-id="219b0-104">An **ISEMenuItem** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItem class.</span></span> <span data-ttu-id="219b0-105">Všechny objekty nabídky **doplňky** nabídky jsou instance **Microsoft.PowerShell.Host.ISE.ISEMenuItem** třídy.</span><span class="sxs-lookup"><span data-stu-id="219b0-105">All menu objects on the **Add-ons** menu are instances of the **Microsoft.PowerShell.Host.ISE.ISEMenuItem** class.</span></span>

## <a name="properties"></a><span data-ttu-id="219b0-106">Properties</span><span class="sxs-lookup"><span data-stu-id="219b0-106">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="219b0-107">DisplayName</span><span class="sxs-lookup"><span data-stu-id="219b0-107">DisplayName</span></span>

<span data-ttu-id="219b0-108">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="219b0-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="219b0-109">Vlastnost jen pro čtení, která získá zobrazovaný název položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="219b0-109">The read-only property that gets the display name of the menu item.</span></span>

```powershell
# Get the display name of the Add-ons menu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.DisplayName
```

### <a name="action"></a><span data-ttu-id="219b0-110">Akce</span><span class="sxs-lookup"><span data-stu-id="219b0-110">Action</span></span>

<span data-ttu-id="219b0-111">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="219b0-111">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="219b0-112">Vlastnost jen pro čtení, která získá blok skriptu.</span><span class="sxs-lookup"><span data-stu-id="219b0-112">The read-only property that gets the block of script.</span></span> <span data-ttu-id="219b0-113">Vyvolá akci po kliknutí na položku nabídky.</span><span class="sxs-lookup"><span data-stu-id="219b0-113">It invokes the action when you click the menu item.</span></span>

```powershell
# Get the action associated with the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action

# Invoke the script associated with the first submenu item
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Action.Invoke()
```

### <a name="shortcut"></a><span data-ttu-id="219b0-114">Místní</span><span class="sxs-lookup"><span data-stu-id="219b0-114">Shortcut</span></span>

<span data-ttu-id="219b0-115">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="219b0-115">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="219b0-116">Vlastnost jen pro čtení, který získá Windows zadejte klávesovou zkratku pro položku nabídky.</span><span class="sxs-lookup"><span data-stu-id="219b0-116">The read-only property that gets the Windows input keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

### <a name="submenus"></a><span data-ttu-id="219b0-117">Podnabídky</span><span class="sxs-lookup"><span data-stu-id="219b0-117">Submenus</span></span>

<span data-ttu-id="219b0-118">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="219b0-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="219b0-119">Vlastnost jen pro čtení, který získá [seznam podnabídek](The-ISEMenuItemCollection-Object.md) položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="219b0-119">The read-only property that gets the [list of submenus](The-ISEMenuItemCollection-Object.md) of the menu item.</span></span>

```powershell
# List the submenus of the Add-ons menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus
```

## <a name="scripting-example"></a><span data-ttu-id="219b0-120">Příklad skriptu</span><span class="sxs-lookup"><span data-stu-id="219b0-120">Scripting example</span></span>

<span data-ttu-id="219b0-121">Pro lepší pochopení použití nabídky Doplňky a skriptovatelný vlastností, přečtěte si následující příklad skriptování.</span><span class="sxs-lookup"><span data-stu-id="219b0-121">To better understand the use of the Add-ons menu and its scriptable properties, read through the following scripting example.</span></span>

```powershell
# This is a scripting example that shows the use of the Add-ons menu.
# Clear the Add-ons menu if any entries currently exist
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

# Add an Add-ons menu item with an shortcut and fast access key.
# Note the use of “_”  as opposed to the “&” for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu - a parent and a child submenu item.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
```

## <a name="see-also"></a><span data-ttu-id="219b0-122">Viz také</span><span class="sxs-lookup"><span data-stu-id="219b0-122">See Also</span></span>

- [<span data-ttu-id="219b0-123">Objekt ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="219b0-123">The ISEMenuItemCollection Object</span></span>](The-ISEMenuItemCollection-Object.md)
- [<span data-ttu-id="219b0-124">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="219b0-124">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="219b0-125">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="219b0-125">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
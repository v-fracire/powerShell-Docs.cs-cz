---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEMenuItemCollection
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7e5030416df394aaa9e9d3f63978e204a7faabf1
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403877"
---
# <a name="the-isemenuitemcollection-object"></a><span data-ttu-id="d7849-103">Objekt ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="d7849-103">The ISEMenuItemCollection Object</span></span>

<span data-ttu-id="d7849-104">**ISEMenuItemCollection** objektu je kolekce **ISEMenuItem** objekty.</span><span class="sxs-lookup"><span data-stu-id="d7849-104">An **ISEMenuItemCollection** object is a collection of **ISEMenuItem** objects.</span></span> <span data-ttu-id="d7849-105">Je instancí třídy Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection.</span><span class="sxs-lookup"><span data-stu-id="d7849-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection class.</span></span> <span data-ttu-id="d7849-106">Příkladem je **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objekt, který se používá k úpravě **doplněk** nabídky ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="d7849-106">An example is the **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** object that is used to customize the **Add-On** menu in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span>

## <a name="method"></a><span data-ttu-id="d7849-107">Metoda</span><span class="sxs-lookup"><span data-stu-id="d7849-107">Method</span></span>

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a><span data-ttu-id="d7849-108">Přidat\(řetězec DisplayName, akce System.Management.Automation.ScriptBlock System.Windows.Input.KeyGesture zástupce \)</span><span class="sxs-lookup"><span data-stu-id="d7849-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span></span>

<span data-ttu-id="d7849-109">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="d7849-109">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="d7849-110">Přidá položku nabídky do kolekce.</span><span class="sxs-lookup"><span data-stu-id="d7849-110">Adds a menu item to the collection.</span></span>

<span data-ttu-id="d7849-111">**DisplayName** zobrazovaný název nabídky, které mají být přidány.</span><span class="sxs-lookup"><span data-stu-id="d7849-111">**DisplayName** The display name of the menu to be added.</span></span>

<span data-ttu-id="d7849-112">**Akce** **System.Management.Automation.ScriptBlock** objekt, který určuje akci, která souvisí s touto položkou nabídky.</span><span class="sxs-lookup"><span data-stu-id="d7849-112">**Action** The **System.Management.Automation.ScriptBlock** object that specifies the action that is associated with this menu item.</span></span>

<span data-ttu-id="d7849-113">**Místní** klávesové zkratky pro akci.</span><span class="sxs-lookup"><span data-stu-id="d7849-113">**Shortcut** The keyboard shortcut for the action.</span></span>

<span data-ttu-id="d7849-114">**Vrátí** The ISEMenuItem objekt, který byl právě přidali.</span><span class="sxs-lookup"><span data-stu-id="d7849-114">**Returns** The ISEMenuItem object that was just added.</span></span>

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a><span data-ttu-id="d7849-115">Vymazat\(\)</span><span class="sxs-lookup"><span data-stu-id="d7849-115">Clear\(\)</span></span>

<span data-ttu-id="d7849-116">Podporováno ve Windows PowerShell ISE 2.0 a novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="d7849-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="d7849-117">Odebere všechny podnabídek z položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="d7849-117">Removes all submenus from the menu item.</span></span>

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a><span data-ttu-id="d7849-118">Viz také</span><span class="sxs-lookup"><span data-stu-id="d7849-118">See Also</span></span>

- [<span data-ttu-id="d7849-119">Objekt ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="d7849-119">The ISEMenuItem Object</span></span>](The-ISEMenuItem-Object.md)
- [<span data-ttu-id="d7849-120">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="d7849-120">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="d7849-121">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="d7849-121">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEMenuItemCollection
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7ce9132021d4d5e755503e0adb355beb388a625a
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="the-isemenuitemcollection-object"></a><span data-ttu-id="f4783-103">Objekt ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="f4783-103">The ISEMenuItemCollection Object</span></span>
  <span data-ttu-id="f4783-104">**ISEMenuItemCollection** objektu je kolekce **ISEMenuItem** objekty.</span><span class="sxs-lookup"><span data-stu-id="f4783-104">An **ISEMenuItemCollection** object is a collection of **ISEMenuItem** objects.</span></span> <span data-ttu-id="f4783-105">Je instance třídy Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection.</span><span class="sxs-lookup"><span data-stu-id="f4783-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection class.</span></span> <span data-ttu-id="f4783-106">Příkladem je **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objekt, který slouží k přizpůsobení **rozšíření** nabídky v systému Windows PowerShell® Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="f4783-106">An example is the **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** object that is used to customize the **Add-On** menu in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span>

## <a name="method"></a><span data-ttu-id="f4783-107">Metoda</span><span class="sxs-lookup"><span data-stu-id="f4783-107">Method</span></span>

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a><span data-ttu-id="f4783-108">Přidat\(řetězec zástupce System.Windows.Input.KeyGesture DisplayName, System.Management.Automation.ScriptBlock akce\)</span><span class="sxs-lookup"><span data-stu-id="f4783-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span></span>
  <span data-ttu-id="f4783-109">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f4783-109">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="f4783-110">Přidá položku nabídky do kolekce.</span><span class="sxs-lookup"><span data-stu-id="f4783-110">Adds a menu item to the collection.</span></span>

 <span data-ttu-id="f4783-111">**DisplayName** zobrazovaný název v nabídce Přidat.</span><span class="sxs-lookup"><span data-stu-id="f4783-111">**DisplayName** The display name of the menu to be added.</span></span>

 <span data-ttu-id="f4783-112">**Akce** **System.Management.Automation.ScriptBlock** objekt, který určuje akci, která je pro tuto položku nabídky.</span><span class="sxs-lookup"><span data-stu-id="f4783-112">**Action** The **System.Management.Automation.ScriptBlock** object that specifies the action that is associated with this menu item.</span></span>

 <span data-ttu-id="f4783-113">**Zástupce** klávesové zkratky pro akci.</span><span class="sxs-lookup"><span data-stu-id="f4783-113">**Shortcut** The keyboard shortcut for the action.</span></span>

 <span data-ttu-id="f4783-114">**Vrátí** The ISEMenuItem objekt, který byl právě přidali.</span><span class="sxs-lookup"><span data-stu-id="f4783-114">**Returns** The ISEMenuItem object that was just added.</span></span>

```
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
```

### <a name="clear"></a><span data-ttu-id="f4783-115">Zrušte zaškrtnutí\(\)</span><span class="sxs-lookup"><span data-stu-id="f4783-115">Clear\(\)</span></span>
  <span data-ttu-id="f4783-116">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="f4783-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="f4783-117">Odebere všechny dílčích z položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="f4783-117">Removes all submenus from the menu item.</span></span>

```
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()

```

## <a name="see-also"></a><span data-ttu-id="f4783-118">Viz také</span><span class="sxs-lookup"><span data-stu-id="f4783-118">See Also</span></span>
- [<span data-ttu-id="f4783-119">Objekt ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="f4783-119">The ISEMenuItem Object</span></span>](The-ISEMenuItem-Object.md) 
- [<span data-ttu-id="f4783-120">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="f4783-120">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="f4783-121">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="f4783-121">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="f4783-122">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="f4783-122">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  

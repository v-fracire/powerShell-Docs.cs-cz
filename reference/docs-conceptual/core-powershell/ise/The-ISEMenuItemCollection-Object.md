---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEMenuItemCollection
ms.assetid: 0c0f5484-3320-408e-8534-5bd1c8e48512
ms.openlocfilehash: 7e5030416df394aaa9e9d3f63978e204a7faabf1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="the-isemenuitemcollection-object"></a><span data-ttu-id="a91ad-103">Objekt ISEMenuItemCollection</span><span class="sxs-lookup"><span data-stu-id="a91ad-103">The ISEMenuItemCollection Object</span></span>

<span data-ttu-id="a91ad-104">**ISEMenuItemCollection** objektu je kolekce **ISEMenuItem** objekty.</span><span class="sxs-lookup"><span data-stu-id="a91ad-104">An **ISEMenuItemCollection** object is a collection of **ISEMenuItem** objects.</span></span> <span data-ttu-id="a91ad-105">Je instance třídy Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection.</span><span class="sxs-lookup"><span data-stu-id="a91ad-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEMenuItemCollection class.</span></span> <span data-ttu-id="a91ad-106">Příkladem je **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** objekt, který slouží k přizpůsobení **rozšíření** nabídky v systému Windows PowerShell® Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="a91ad-106">An example is the **$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus** object that is used to customize the **Add-On** menu in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span>

## <a name="method"></a><span data-ttu-id="a91ad-107">Metoda</span><span class="sxs-lookup"><span data-stu-id="a91ad-107">Method</span></span>

### <a name="addstring-displayname-systemmanagementautomationscriptblock-action-systemwindowsinputkeygesture-shortcut-"></a><span data-ttu-id="a91ad-108">Přidat\(řetězec zástupce System.Windows.Input.KeyGesture DisplayName, System.Management.Automation.ScriptBlock akce \)</span><span class="sxs-lookup"><span data-stu-id="a91ad-108">Add\(string DisplayName, System.Management.Automation.ScriptBlock Action, System.Windows.Input.KeyGesture Shortcut \)</span></span>

<span data-ttu-id="a91ad-109">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="a91ad-109">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="a91ad-110">Přidá položku nabídky do kolekce.</span><span class="sxs-lookup"><span data-stu-id="a91ad-110">Adds a menu item to the collection.</span></span>

<span data-ttu-id="a91ad-111">**DisplayName** zobrazovaný název v nabídce Přidat.</span><span class="sxs-lookup"><span data-stu-id="a91ad-111">**DisplayName** The display name of the menu to be added.</span></span>

<span data-ttu-id="a91ad-112">**Akce** **System.Management.Automation.ScriptBlock** objekt, který určuje akci, která je pro tuto položku nabídky.</span><span class="sxs-lookup"><span data-stu-id="a91ad-112">**Action** The **System.Management.Automation.ScriptBlock** object that specifies the action that is associated with this menu item.</span></span>

<span data-ttu-id="a91ad-113">**Zástupce** klávesové zkratky pro akci.</span><span class="sxs-lookup"><span data-stu-id="a91ad-113">**Shortcut** The keyboard shortcut for the action.</span></span>

<span data-ttu-id="a91ad-114">**Vrátí** The ISEMenuItem objekt, který byl právě přidali.</span><span class="sxs-lookup"><span data-stu-id="a91ad-114">**Returns** The ISEMenuItem object that was just added.</span></span>

```powershell
# Create an Add-ons menu with an fast access key and a shortcut.
# Note the use of "_"  as opposed to the "&" for mapping to the fast access key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
```

### <a name="clear"></a><span data-ttu-id="a91ad-115">Zrušte zaškrtnutí\(\)</span><span class="sxs-lookup"><span data-stu-id="a91ad-115">Clear\(\)</span></span>

<span data-ttu-id="a91ad-116">Podporuje se v prostředí Windows PowerShell ISE 2.0 nebo novější.</span><span class="sxs-lookup"><span data-stu-id="a91ad-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="a91ad-117">Odebere všechny dílčích z položky nabídky.</span><span class="sxs-lookup"><span data-stu-id="a91ad-117">Removes all submenus from the menu item.</span></span>

```powershell
# Remove all custom submenu items from the AddOns menu
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
```

## <a name="see-also"></a><span data-ttu-id="a91ad-118">Viz také</span><span class="sxs-lookup"><span data-stu-id="a91ad-118">See Also</span></span>

- [<span data-ttu-id="a91ad-119">Objekt ISEMenuItem</span><span class="sxs-lookup"><span data-stu-id="a91ad-119">The ISEMenuItem Object</span></span>](The-ISEMenuItem-Object.md)
- [<span data-ttu-id="a91ad-120">Účelem ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="a91ad-120">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="a91ad-121">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="a91ad-121">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
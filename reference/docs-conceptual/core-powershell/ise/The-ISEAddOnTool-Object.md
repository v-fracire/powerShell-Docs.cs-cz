---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: Objekt ISEAddOnTool
ms.assetid: ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
ms.openlocfilehash: b813fcac547c8069e84741081a3ceb00044bab87
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2017
---
# <a name="the-iseaddontool-object"></a><span data-ttu-id="15254-103">Objekt ISEAddOnTool</span><span class="sxs-lookup"><span data-stu-id="15254-103">The ISEAddOnTool Object</span></span>
  <span data-ttu-id="15254-104">**ISEAddonTool** objekt představuje nástroj nainstalovaný doplněk, který poskytuje další funkce týká programu Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="15254-104">An **ISEAddonTool** object represents an installed add-on tool that provides additional functionality toWindows PowerShell ISE.</span></span> <span data-ttu-id="15254-105">Příkladem je **příkazy** nástroj, který můžete zobrazit kliknutím na **zobrazení**, pak **zobrazit příkaz rozšíření**.</span><span class="sxs-lookup"><span data-stu-id="15254-105">An example is the **Commands** tool that you can display by clicking **View**, then **Show Command Add-on**.</span></span> <span data-ttu-id="15254-106">Tento nástroj je pak můžete přistupovat k dispozici různé manipulací **ISEAddOnTool** objekty.</span><span class="sxs-lookup"><span data-stu-id="15254-106">This tool is then accessible to you by manipulating the various available **ISEAddOnTool** objects.</span></span>

 <span data-ttu-id="15254-107">Každé rozšíření nástroj může být přidružen podokně svislé nebo vodorovné podokně.</span><span class="sxs-lookup"><span data-stu-id="15254-107">Each add-on tool can be associated with either the vertical pane or the horizontal pane.</span></span> <span data-ttu-id="15254-108">V podokně svislé ukotven pravé hrany Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="15254-108">The vertical pane is docked to the right edge of Windows PowerShell ISE.</span></span> <span data-ttu-id="15254-109">V podokně vodorovné ukotven na dolní okraj.</span><span class="sxs-lookup"><span data-stu-id="15254-109">The horizontal pane is docked to the bottom edge.</span></span>

 <span data-ttu-id="15254-110">Každé kartě prostředí PowerShell v systému Windows PowerShell ISE může mít vlastní sadu rozšíření nástroje nainstalované.</span><span class="sxs-lookup"><span data-stu-id="15254-110">Each PowerShell tab in Windows PowerShell ISE can have its own set of add-on tools installed.</span></span> <span data-ttu-id="15254-111">V tématu [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) a [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) získat přístup ke kolekci nástroje dostupné pro aktuálně vybrané kartě nebo stejné vlastnosti na žádném z **PowerShellTab** objekty v [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) objektu kolekce.</span><span class="sxs-lookup"><span data-stu-id="15254-111">See [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) and [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) to access the collection of tools available to the currently selected tab or the same properties on any of the **PowerShellTab** objects in the [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) collection object.</span></span>

## <a name="methods"></a><span data-ttu-id="15254-112">Metody</span><span class="sxs-lookup"><span data-stu-id="15254-112">Methods</span></span>
 <span data-ttu-id="15254-113">Nejsou k dispozici pro objekty této třídy žádné metody ISE specifické pro systém Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15254-113">There are no Windows PowerShell ISE-specific methods available for objects of this class.</span></span>

## <a name="properties"></a><span data-ttu-id="15254-114">Properties</span><span class="sxs-lookup"><span data-stu-id="15254-114">Properties</span></span>

### <a name="control"></a><span data-ttu-id="15254-115">Řízení</span><span class="sxs-lookup"><span data-stu-id="15254-115">Control</span></span>
  <span data-ttu-id="15254-116">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="15254-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="15254-117">**Řízení** vlastnost poskytuje přístup pro čtení k mnoha podrobnosti doplněk nástroje příkazy.</span><span class="sxs-lookup"><span data-stu-id="15254-117">The **Control** property provides read access to many of the details of the Commands add-on tool.</span></span>

```
# View the properties of the Commands add-on tool.
# (assumes that it is visible in the vertical pane)
$psISE.CurrentVisibleVerticalTool.Control
HostObject                  : Microsoft.PowerShell.Host.ISE.ObjectModelRoot
Content                     :
HasContent                  :
ContentTemplate             :
ContentTemplateSelector     :
ContentStringFormat         :
BorderBrush                 :
BorderThickness             :
Background                  :
Foreground                  :
FontFamily                  :
FontSize                    :
FontStretch                 :
FontStyle                   :
FontWeight                  :
HorizontalContentAlignment  :
VerticalContentAlignment    :
TabIndex                    :
IsTabStop                   :
Padding                     :
Template                    : System.Windows.Controls.ControlTemplate
Style                       :
OverridesDefaultStyle       :
UseLayoutRounding           :
Triggers                    : {}
TemplatedParent             :
Resources                   : {System.Windows.Controls.TabItem}
DataContext                 :
BindingGroup                :
Language                    :
Name                        :
Tag                         :
InputScope                  :
ActualWidth                 : 370.75
ActualHeight                : 676.559097412109
LayoutTransform             :
Width                       :
MinWidth                    :
MaxWidth                    :
Height                      :
MinHeight                   :
MaxHeight                   :
FlowDirection               : LeftToRight
Margin                      :
HorizontalAlignment         :
VerticalAlignment           :
FocusVisualStyle            :
Cursor                      :
ForceCursor                 :
IsInitialized               : True
IsLoaded                    :
ToolTip                     :
ContextMenu                 :
Parent                      :
HasAnimatedProperties       :
InputBindings               :
CommandBindings             :
AllowDrop                   :
DesiredSize                 : 227.66,676.559097412109
IsMeasureValid              : True
IsArrangeValid              : True
RenderSize                  : 370.75,676.559097412109
RenderTransform             :
RenderTransformOrigin       :
IsMouseDirectlyOver         : False
IsMouseOver                 : False
IsStylusOver                : False
IsKeyboardFocusWithin       : False
IsMouseCaptured             :
IsMouseCaptureWithin        : False
IsStylusDirectlyOver        : False
IsStylusCaptured            :
IsStylusCaptureWithin       : False
IsKeyboardFocused           : False
IsInputMethodEnabled        :
Opacity                     :
OpacityMask                 :
BitmapEffect                :
Effect                      :
BitmapEffectInput           :
CacheMode                   :
Uid                         :
Visibility                  : Visible
ClipToBounds                : False
Clip                        :
SnapsToDevicePixels         : False
IsFocused                   :
IsEnabled                   :
IsHitTestVisible            :
IsVisible                   : True
Focusable                   :
PersistId                   : 1
IsManipulationEnabled       :
AreAnyTouchesOver           : False
AreAnyTouchesDirectlyOver   :
AreAnyTouchesCapturedWithin : False
AreAnyTouchesCaptured       :
TouchesCaptured             : {}
TouchesCapturedWithin       : {}
TouchesOver                 : {}
TouchesDirectlyOver         : {}
DependencyObjectType        : System.Windows.DependencyObjectType
IsSealed                    : False
Dispatcher                  : System.Windows.Threading.Dispatcher

```

### <a name="isvisible"></a><span data-ttu-id="15254-118">IsVisible –</span><span class="sxs-lookup"><span data-stu-id="15254-118">IsVisible</span></span>
  <span data-ttu-id="15254-119">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="15254-119">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="15254-120">Vlastnost typu Boolean, která určuje, zda je aktuálně viditelné v příslušné přiřazené podokno nástroje rozšíření.</span><span class="sxs-lookup"><span data-stu-id="15254-120">The Boolean property that indicates whether the add-on tool is currently visible in its assigned pane.</span></span> <span data-ttu-id="15254-121">Pokud je zobrazen, můžete nastavit **IsVisible** vlastnost, která má **$false** skrýt nástroj nebo nastavit **IsVisible –** vlastnost **$true** aby rozšíření nástrojů, viditelné na své kartě prostředí PowerShell. Poté, co nástroj na rozšíření skryt, je už přístupné prostřednictvím **CurrentVisibleHorizontalTool** nebo **CurrentVisibleVerticalTool** objektů a proto nemůže být viditelné pomocí Tato vlastnost na tento objekt.</span><span class="sxs-lookup"><span data-stu-id="15254-121">If it is visible, you can set the **IsVisible** property to **$false** to hide the tool, or set the **IsVisible** property to **$true** to make an add-on tool visible on its PowerShell tab. Note that after an add-on tool is hidden, it is no longer accessible through the **CurrentVisibleHorizontalTool** or **CurrentVisibleVerticalTool** objects, and therefore cannot be made visible by using this property on that object.</span></span>

```
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible=$true

```

### <a name="name"></a><span data-ttu-id="15254-122">Název</span><span class="sxs-lookup"><span data-stu-id="15254-122">Name</span></span>
  <span data-ttu-id="15254-123">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="15254-123">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="15254-124">Vlastnost jen pro čtení, získá název rozšíření nástroje.</span><span class="sxs-lookup"><span data-stu-id="15254-124">The read-only property that gets the name of the add-on tool.</span></span>

```
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.name
Commands

```

## <a name="see-also"></a><span data-ttu-id="15254-125">Viz také</span><span class="sxs-lookup"><span data-stu-id="15254-125">See Also</span></span>
- [<span data-ttu-id="15254-126">Objekt ISEAddOnToolCollection</span><span class="sxs-lookup"><span data-stu-id="15254-126">The ISEAddOnToolCollection Object</span></span>](The-ISEAddOnToolCollection-Object.md)
- [<span data-ttu-id="15254-127">ISE Windows PowerShell skriptování objektový Model</span><span class="sxs-lookup"><span data-stu-id="15254-127">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="15254-128">Odkaz na objekt modelu Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="15254-128">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [<span data-ttu-id="15254-129">Hierarchie ISE objektů modelu</span><span class="sxs-lookup"><span data-stu-id="15254-129">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)


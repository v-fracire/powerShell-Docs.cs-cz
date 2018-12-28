---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Objekt ISEAddOnTool
ms.assetid: ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
ms.openlocfilehash: e091f37601c7a4fdaf5deff8c668b18ee7369e74
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404073"
---
# <a name="the-iseaddontool-object"></a><span data-ttu-id="8bf8c-103">Objekt ISEAddOnTool</span><span class="sxs-lookup"><span data-stu-id="8bf8c-103">The ISEAddOnTool Object</span></span>

<span data-ttu-id="8bf8c-104">**ISEAddonTool** objekt představuje nástroj nainstalovaný doplněk, který poskytuje další funkce týká programu Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-104">An **ISEAddonTool** object represents an installed add-on tool that provides additional functionality toWindows PowerShell ISE.</span></span> <span data-ttu-id="8bf8c-105">Příkladem je **příkazy** nástroj, který lze zobrazit klepnutím **zobrazení**, pak **zobrazit příkaz doplňku**.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-105">An example is the **Commands** tool that you can display by clicking **View**, then **Show Command Add-on**.</span></span> <span data-ttu-id="8bf8c-106">Tento nástroj je pak můžete přistupovat k dispozici různé manipulací **ISEAddOnTool** objekty.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-106">This tool is then accessible to you by manipulating the various available **ISEAddOnTool** objects.</span></span>

<span data-ttu-id="8bf8c-107">Každý doplněk nástroje můžou být spojené s podokně svislé nebo vodorovné podokno.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-107">Each add-on tool can be associated with either the vertical pane or the horizontal pane.</span></span> <span data-ttu-id="8bf8c-108">Svislé podokně je ukotven na pravém okraji Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-108">The vertical pane is docked to the right edge of Windows PowerShell ISE.</span></span> <span data-ttu-id="8bf8c-109">Vodorovné podokno je ukotven k dolnímu okraji.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-109">The horizontal pane is docked to the bottom edge.</span></span>

<span data-ttu-id="8bf8c-110">Každá karta prostředí PowerShell v prostředí Windows PowerShell ISE může mít svou vlastní sadu nainstalované nástroje pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-110">Each PowerShell tab in Windows PowerShell ISE can have its own set of add-on tools installed.</span></span> <span data-ttu-id="8bf8c-111">Zobrazit [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) a [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) získat přístup ke kolekci nástroje, které jsou k dispozici pro aktuálně vybraná karta nebo stejné vlastnosti u některého **PowerShellTab** objekty v [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) objektu kolekce.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-111">See [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) and [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) to access the collection of tools available to the currently selected tab or the same properties on any of the **PowerShellTab** objects in the [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) collection object.</span></span>

## <a name="methods"></a><span data-ttu-id="8bf8c-112">Metody</span><span class="sxs-lookup"><span data-stu-id="8bf8c-112">Methods</span></span>

<span data-ttu-id="8bf8c-113">Nejsou k dispozici pro objekty této třídy bez Windows PowerShell ISE konkrétní metody.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-113">There are no Windows PowerShell ISE-specific methods available for objects of this class.</span></span>

## <a name="properties"></a><span data-ttu-id="8bf8c-114">Properties</span><span class="sxs-lookup"><span data-stu-id="8bf8c-114">Properties</span></span>

### <a name="control"></a><span data-ttu-id="8bf8c-115">Řízení</span><span class="sxs-lookup"><span data-stu-id="8bf8c-115">Control</span></span>

<span data-ttu-id="8bf8c-116">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="8bf8c-117">**Ovládací prvek** vlastnost poskytuje přístup pro čtení k mnoho podrobností nástroj příkazy doplňku.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-117">The **Control** property provides read access to many of the details of the Commands add-on tool.</span></span>

```powershell
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

### <a name="isvisible"></a><span data-ttu-id="8bf8c-118">IsVisible</span><span class="sxs-lookup"><span data-stu-id="8bf8c-118">IsVisible</span></span>

<span data-ttu-id="8bf8c-119">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-119">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="8bf8c-120">Logická vlastnost, která určuje, zda nástroj doplněk je aktuálně zobrazené v podokně své přiřazené.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-120">The Boolean property that indicates whether the add-on tool is currently visible in its assigned pane.</span></span> <span data-ttu-id="8bf8c-121">Pokud je zobrazen, můžete nastavit **IsVisible** vlastnost **$false** skrýt nástroj nebo nastavit **IsVisible** vlastnost **$true** aby doplněk nástroj viditelný na kartě prostředí PowerShell. Všimněte si, že po nástroj doplněk je skrytý, už nejsou přístupné prostřednictvím **CurrentVisibleHorizontalTool** nebo **CurrentVisibleVerticalTool** objekty a proto nemůže být viditelný pomocí Tato vlastnost k tomuto objektu.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-121">If it is visible, you can set the **IsVisible** property to **$false** to hide the tool, or set the **IsVisible** property to **$true** to make an add-on tool visible on its PowerShell tab. Note that after an add-on tool is hidden, it is no longer accessible through the **CurrentVisibleHorizontalTool** or **CurrentVisibleVerticalTool** objects, and therefore cannot be made visible by using this property on that object.</span></span>

```powershell
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible = $true
```

### <a name="name"></a><span data-ttu-id="8bf8c-122">Název</span><span class="sxs-lookup"><span data-stu-id="8bf8c-122">Name</span></span>

<span data-ttu-id="8bf8c-123">Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-123">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="8bf8c-124">Vlastnost jen pro čtení, která získá název nástroje pro doplněk.</span><span class="sxs-lookup"><span data-stu-id="8bf8c-124">The read-only property that gets the name of the add-on tool.</span></span>

```powershell
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.Name
Commands
```

## <a name="see-also"></a><span data-ttu-id="8bf8c-125">Viz také</span><span class="sxs-lookup"><span data-stu-id="8bf8c-125">See Also</span></span>

- [<span data-ttu-id="8bf8c-126">Objekt ISEAddOnToolCollection</span><span class="sxs-lookup"><span data-stu-id="8bf8c-126">The ISEAddOnToolCollection Object</span></span>](The-ISEAddOnToolCollection-Object.md)
- [<span data-ttu-id="8bf8c-127">Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="8bf8c-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="8bf8c-128">Hierarchie objektového modelu prostředí ISE</span><span class="sxs-lookup"><span data-stu-id="8bf8c-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
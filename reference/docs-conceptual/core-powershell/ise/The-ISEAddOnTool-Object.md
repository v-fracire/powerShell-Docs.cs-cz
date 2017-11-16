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
# <a name="the-iseaddontool-object"></a>Objekt ISEAddOnTool
  **ISEAddonTool** objekt představuje nástroj nainstalovaný doplněk, který poskytuje další funkce týká programu Windows PowerShell ISE. Příkladem je **příkazy** nástroj, který můžete zobrazit kliknutím na **zobrazení**, pak **zobrazit příkaz rozšíření**. Tento nástroj je pak můžete přistupovat k dispozici různé manipulací **ISEAddOnTool** objekty.

 Každé rozšíření nástroj může být přidružen podokně svislé nebo vodorovné podokně. V podokně svislé ukotven pravé hrany Windows PowerShell ISE. V podokně vodorovné ukotven na dolní okraj.

 Každé kartě prostředí PowerShell v systému Windows PowerShell ISE může mít vlastní sadu rozšíření nástroje nainstalované. V tématu [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) a [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) získat přístup ke kolekci nástroje dostupné pro aktuálně vybrané kartě nebo stejné vlastnosti na žádném z **PowerShellTab** objekty v [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) objektu kolekce.

## <a name="methods"></a>Metody
 Nejsou k dispozici pro objekty této třídy žádné metody ISE specifické pro systém Windows PowerShell.

## <a name="properties"></a>Properties

### <a name="control"></a>Řízení
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 **Řízení** vlastnost poskytuje přístup pro čtení k mnoha podrobnosti doplněk nástroje příkazy.

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

### <a name="isvisible"></a>IsVisible –
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Vlastnost typu Boolean, která určuje, zda je aktuálně viditelné v příslušné přiřazené podokno nástroje rozšíření. Pokud je zobrazen, můžete nastavit **IsVisible** vlastnost, která má **$false** skrýt nástroj nebo nastavit **IsVisible –** vlastnost **$true** aby rozšíření nástrojů, viditelné na své kartě prostředí PowerShell. Poté, co nástroj na rozšíření skryt, je už přístupné prostřednictvím **CurrentVisibleHorizontalTool** nebo **CurrentVisibleVerticalTool** objektů a proto nemůže být viditelné pomocí Tato vlastnost na tento objekt.

```
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible=$true

```

### <a name="name"></a>Název
  Podporované v prostředí Windows PowerShell ISE 3.0 a novější a nejsou k dispozici v dřívějších verzích.

 Vlastnost jen pro čtení, získá název rozšíření nástroje.

```
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.name
Commands

```

## <a name="see-also"></a>Viz také
- [Objekt ISEAddOnToolCollection](The-ISEAddOnToolCollection-Object.md)
- [ISE Windows PowerShell skriptování objektový Model](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Odkaz na objekt modelu Windows PowerShell ISE](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [Hierarchie ISE objektů modelu](The-ISE-Object-Model-Hierarchy.md)


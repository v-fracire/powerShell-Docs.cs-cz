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
# <a name="the-iseaddontool-object"></a>Objekt ISEAddOnTool

**ISEAddonTool** objekt představuje nástroj nainstalovaný doplněk, který poskytuje další funkce týká programu Windows PowerShell ISE. Příkladem je **příkazy** nástroj, který lze zobrazit klepnutím **zobrazení**, pak **zobrazit příkaz doplňku**. Tento nástroj je pak můžete přistupovat k dispozici různé manipulací **ISEAddOnTool** objekty.

Každý doplněk nástroje můžou být spojené s podokně svislé nebo vodorovné podokno. Svislé podokně je ukotven na pravém okraji Windows PowerShell ISE. Vodorovné podokno je ukotven k dolnímu okraji.

Každá karta prostředí PowerShell v prostředí Windows PowerShell ISE může mít svou vlastní sadu nainstalované nástroje pro doplněk. Zobrazit [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) a [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) získat přístup ke kolekci nástroje, které jsou k dispozici pro aktuálně vybraná karta nebo stejné vlastnosti u některého **PowerShellTab** objekty v [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) objektu kolekce.

## <a name="methods"></a>Metody

Nejsou k dispozici pro objekty této třídy bez Windows PowerShell ISE konkrétní metody.

## <a name="properties"></a>Properties

### <a name="control"></a>Řízení

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

**Ovládací prvek** vlastnost poskytuje přístup pro čtení k mnoho podrobností nástroj příkazy doplňku.

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

### <a name="isvisible"></a>IsVisible

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Logická vlastnost, která určuje, zda nástroj doplněk je aktuálně zobrazené v podokně své přiřazené. Pokud je zobrazen, můžete nastavit **IsVisible** vlastnost **$false** skrýt nástroj nebo nastavit **IsVisible** vlastnost **$true** aby doplněk nástroj viditelný na kartě prostředí PowerShell. Všimněte si, že po nástroj doplněk je skrytý, už nejsou přístupné prostřednictvím **CurrentVisibleHorizontalTool** nebo **CurrentVisibleVerticalTool** objekty a proto nemůže být viditelný pomocí Tato vlastnost k tomuto objektu.

```powershell
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible = $true
```

### <a name="name"></a>Název

Podporované v prostředí Windows PowerShell ISE 3.0 a novější a není k dispozici v dřívějších verzích.

Vlastnost jen pro čtení, která získá název nástroje pro doplněk.

```powershell
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.Name
Commands
```

## <a name="see-also"></a>Viz také

- [Objekt ISEAddOnToolCollection](The-ISEAddOnToolCollection-Object.md)
- [Účel skriptovacího objektového modelu prostředí Windows PowerShell ISE](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Hierarchie objektového modelu prostředí ISE](The-ISE-Object-Model-Hierarchy.md)
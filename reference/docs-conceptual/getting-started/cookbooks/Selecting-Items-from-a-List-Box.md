---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Výběr položek ze seznamu
ms.assetid: 327c7cc5-21d0-4ace-b151-aa1491d1d3c2
ms.openlocfilehash: 6ff6bff8f6ce4e9236d7877c4cca24a10932cbe0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="selecting-items-from-a-list-box"></a>Výběr položek ze seznamu

K vytvoření dialogu, který umožňuje uživatelům výběru položek z ovládací prvek seznamu, použijte prostředí Windows PowerShell 3.0 a novějších verzí.

## <a name="create-a-list-box-control-and-select-items-from-it"></a>Vytvořte ovládací prvek seznamu a vyberte položky z něj

Zkopírujte a vložte následující do systému Windows PowerShell ISE a pak ho uložte jako skript prostředí Windows PowerShell (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Select a Computer'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please select a computer:'
$form.Controls.Add($label)

$listBox = New-Object System.Windows.Forms.ListBox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
$listBox.Height = 80

[void] $listBox.Items.Add('atl-dc-001')
[void] $listBox.Items.Add('atl-dc-002')
[void] $listBox.Items.Add('atl-dc-003')
[void] $listBox.Items.Add('atl-dc-004')
[void] $listBox.Items.Add('atl-dc-005')
[void] $listBox.Items.Add('atl-dc-006')
[void] $listBox.Items.Add('atl-dc-007')

$form.Controls.Add($listBox)

$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

Zahájí skript načtením dvě třídy rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**. Spusťte novou instanci třídy rozhraní .NET Framework **formuláře System.Windows.Forms.Form**; který poskytuje prázdného formuláře nebo okna, do kterého můžete začít přidávat ovládací prvky.

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

Po vytvoření instance třídy formuláře, hodnoty přiřadíte tři vlastnosti této třídy.

- **Text.** To všechno bude v záhlaví okna.

- **Velikost.** Toto je velikost formuláře v pixelech. Předchozí skript vytvoří formulář, který je 300 × široké 200 pixelů vysoký.

- **StartingPosition.** Tato volitelná vlastnost nastavena na **CenterScreen** v předchozí skript. Pokud přidáte nemusíte tuto vlastnost, systém Windows vybere umístění při otevření formuláře. Nastavením **StartingPosition** k **CenterScreen**, automaticky zobrazujete formuláře uprostřed obrazovky pokaždé, když ho načte.

```powershell
$form.Text = 'Select a Computer'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Dále vytvořte **OK** tlačítko pro daný formulář. Zadejte velikost a chování **OK** tlačítko. V tomto příkladu je pozice tlačítko 120 pixelů od horního okraje formuláře a 75 pixelů od levého okraje. Výška tlačítko je 23 pixelů, zatímco tlačítko délka je 75 pixelů. Skript používá předdefinovaných typů Windows Forms k určení chování tlačítko.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Podobně můžete vytvořit **zrušit** tlačítko. **Zrušit** tlačítko je 120 pixelů z horní části, ale 150 pixelů od levého okraje okna.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Potom zadejte text popisku na vaše okno, které popisuje informace, které chcete, aby uživatelé zadali. V takovém případě budete chtít uživatelům vyberte počítač.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please select a computer:'
$form.Controls.Add($label)
```

Přidání ovládacího prvku (v tomto případě pole se seznamem), která umožňuje uživatelům poskytnout informace, které jste popsaných v textu popisku. Existuje mnoho dalších ovládacích prvků, které můžete použít kromě seznamy; pro další ovládací prvky, najdete v části [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) na webu MSDN.

```powershell
$listBox = New-Object System.Windows.Forms.ListBox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
$listBox.Height = 80
```

V další části zadejte hodnoty, které chcete zobrazit uživatelům v rozevíracím seznamu.

> [!NOTE]
> Pole se seznamem tento skript vytvořený umožňuje pouze jeden výběr. Pokud chcete vytvořit rozevírací seznam, který umožňuje více výběrů, zadejte hodnotu pro **SelectionMode** vlastnost, podobně jako následující: `$listBox.SelectionMode = 'MultiExtended'`. Další informace najdete v tématu [vícenásobného výběru seznamy](Multiple-selection-List-Boxes.md).

```powershell
[void] $listBox.Items.Add('atl-dc-001')
[void] $listBox.Items.Add('atl-dc-002')
[void] $listBox.Items.Add('atl-dc-003')
[void] $listBox.Items.Add('atl-dc-004')
[void] $listBox.Items.Add('atl-dc-005')
[void] $listBox.Items.Add('atl-dc-006')
[void] $listBox.Items.Add('atl-dc-007')
```

Přidejte do svého formuláře ovládací prvek seznam a Vyzvěte Windows otevřete formulář na jiné windows a dialogových oken při otevření.

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

Přidejte následující řádek kódu k zobrazení formuláře v systému Windows.

```powershell
$result = $form.ShowDialog()
```

Nakonec se kód uvnitř **Pokud** bloku dá pokyn Windows co dělat s formulářem po uživatelů vyberte možnost ze seznamu a pak klikněte na tlačítko **OK** tlačítko nebo klikněte na tlačítko **Enter**klíč.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## <a name="see-also"></a>Viz také

- [Hey Scripting Guy: Proč se nepodporují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?](http://go.microsoft.com/fwlink/?LinkId=506644)
- [Githubu: WinFormsExampleUpdates Dave Wyatt](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip v týdnu: výběr položek ze seznamu](http://technet.microsoft.com/library/ff730949.aspx)
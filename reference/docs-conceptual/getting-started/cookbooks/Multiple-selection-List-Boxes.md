---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Pole se seznamem umožňujícím vícenásobný výběr
ms.assetid: f74cd5d9-da57-4802-b614-0b194a7bc8f8
ms.openlocfilehash: 81708fd5d7204fb7d136e9d8e808303f4d3f4c30
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="multiple-selection-list-boxes"></a>Výběr více seznamy

Vytvoření ovládacího prvku seznam s vícenásobným výběrem pole ve formuláři Windows vlastní pomocí prostředí Windows PowerShell 3.0 a novějších verzí.

## <a name="create-list-box-controls-that-allow-multiple-selections"></a>Vytvoření seznamu ovládacích prvků pole, které umožňují více výběrů

Zkopírujte a vložte následující do systému Windows PowerShell ISE a pak ho uložte jako skript prostředí Windows PowerShell (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form
$form.Text = 'Data Entry Form'
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
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)

$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)

$listBox.SelectionMode = 'MultiExtended'

[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')

$listBox.Height = 70
$form.Controls.Add($listBox)
$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

Zahájí skript načtením dvě třídy rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**. Spusťte novou instanci třídy rozhraní .NET Framework **formuláře System.Windows.Forms.Form**; který poskytuje prázdného formuláře nebo okna, do kterého můžete začít přidávat ovládací prvky.

```powershell
$form = New-Object System.Windows.Forms.Form
```

Po vytvoření instance třídy formuláře, hodnoty přiřadíte tři vlastnosti této třídy.

- **Text.** To všechno bude v záhlaví okna.

- **Velikost.** Toto je velikost formuláře v pixelech. Předchozí skript vytvoří formulář, který je 300 × široké 200 pixelů vysoký.

- **StartingPosition.** Tato volitelná vlastnost nastavena na **CenterScreen** v předchozí skript. Pokud přidáte nemusíte tuto vlastnost, systém Windows vybere umístění při otevření formuláře. Nastavením **StartingPosition** k **CenterScreen**, automaticky zobrazujete formuláře uprostřed obrazovky pokaždé, když ho načte.

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Dále vytvořte **OK** tlačítko pro daný formulář. Zadejte velikost a chování **OK** tlačítko. V tomto příkladu je pozice tlačítko 120 pixelů od horního okraje formuláře a 75 pixelů od levého okraje. Výška tlačítko je 23 pixelů, zatímco tlačítko délka je 75 pixelů. Skript používá předdefinovaných typů Windows Forms k určení chování tlačítko.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
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

Potom zadejte text popisku na vaše okno, které popisuje informace, které chcete, aby uživatelé zadali.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)
```

Přidání ovládacího prvku (v tomto případě pole se seznamem), která umožňuje uživatelům poskytnout informace, které jste popsaných v textu popisku. Existuje mnoho dalších ovládacích prvků, které můžete použít kromě polí; pro další ovládací prvky, najdete v části [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) na webu MSDN.

```powershell
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
```

Zde je, jak určíte, že chcete povolit uživatelům výběr více hodnot v seznamu.

```powershell
$listBox.SelectionMode = 'MultiExtended'
```

V další části zadejte hodnoty, které chcete zobrazit uživatelům v rozevíracím seznamu.

```powershell
[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')
```

Zadejte maximální výšku ovládací prvek seznam.

```powershell
$listBox.Height = 70
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

Nakonec se kód uvnitř **Pokud** bloku dá pokyn Windows co dělat s formulářem po uživatele ze seznamu vyberte jednu nebo více možností a pak klikněte na tlačítko **OK** tlačítko nebo klikněte na tlačítko **Enter**  klíč.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a>Viz také

- [Hey Scripting Guy: Proč se nepodporují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?](http://go.microsoft.com/fwlink/?LinkId=506644)
- [Githubu: WinFormsExampleUpdates Dave Wyatt](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip v týdnu: vícenásobný výběr v seznamu polí - a další!](http://technet.microsoft.com/library/ff730950.aspx)
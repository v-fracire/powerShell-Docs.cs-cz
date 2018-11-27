---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření vlastního vstupního pole
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 2d04ad6df65cdb4ff13d136dea47bbba6a01f3a2
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320393"
---
# <a name="creating-a-custom-input-box"></a>Vytvoření vlastního vstupního pole

Skript grafické vlastního vstupního pole pomocí funkce vytváření formulářů rozhraní Microsoft .NET Framework ve Windows Powershellu 3.0 a novějších verzí.

## <a name="create-a-custom-graphical-input-box"></a>Vytvořit vlastní grafické vstupního pole

Zkopírujte a vložte následující do Windows PowerShell ISE a pak ho uložte jako skript Windows Powershellu (.ps1).

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
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)

$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)

$form.Topmost = $true

$form.Add_Shown({$textBox.Select()})
$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

Spustí skript načtením dvou tříd rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**. Spusťte novou instanci třídy rozhraní .NET Framework **formuláře System.Windows.Forms.Form**; který obsahuje prázdný formulář nebo ovládací prvky okna, do kterého můžete začít přidávat.

```powershell
$form = New-Object System.Windows.Forms.Form
```

Po vytvoření instance třídy formuláře přiřadíte hodnoty třem vlastnostem této třídy.

- **Text.** Tím se změní záhlaví okna.

- **Velikost.** Toto je velikost formuláře v pixelech. Předchozí skript vytvoří formulář, který je 300 pixelů na šířku a 200 pixelů na výšku.

- **Počáteční pozice.** Tato volitelná vlastnost nastavena na **CenterScreen** v předchozím skriptu. Pokud tuto vlastnost nepřidáte, vybere Windows umístění při otevření formuláře. Tím, že nastavíte **počáteční pozice** k **CenterScreen**, automaticky zobrazená formuláři uprostřed obrazovky pokaždé, když ho načte.

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

Dále vytvořte **OK** tlačítko pro daný formulář. Zadejte velikost a chování **OK** tlačítko. V tomto příkladu je pozice tlačítko 120 pixelů od horního okraje formuláře a 75 pixelů od levého okraje. Výška tlačítka je 23 pixelů, zatímco tlačítko délka je 75 pixelů. Tento skript využívá k určení chování tlačítka předdefinovaných typů formulářů Windows.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Podobně můžete vytvořit **zrušit** tlačítko. **Zrušit** tlačítko je 120 pixelů od horního, ale 150 pixelů od levého okraje okna.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Pak zadejte popisek v okně, který popisuje informace, na kterých chcete, aby uživatelé zadali.

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

Přidejte ovládací prvek (v tomto případě textové pole), která umožňuje uživatelům poskytnout informace, které jste je popsáno v textu popisku. Existuje mnoho dalších ovládacích prvků, platí kromě textová pole; pro větší počet kontrolních mechanismů, naleznete v tématu [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) na webové stránce MSDN.

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

Nastavte **nejvíce nahoře** vlastnost **$true** přinutit okně pro otevření imitovaná otevřená okna a dialogová okna.

```powershell
$form.Topmost = $true
```

V dalším kroku přidejte následující řádek kódu k aktivaci formuláře a nastaví fokus do textového pole, který jste vytvořili.

```powershell
$form.Add_Shown({$textBox.Select()})
```

Přidejte následující řádek kódu k zobrazení formuláře ve Windows.

```powershell
$result = $form.ShowDialog()
```

Nakonec se kód uvnitř **Pokud** bloku instruuje Windows, co dělat s formulářem, poté, co uživatelé zadejte text do textového pole a potom klikněte na tlačítko **OK** tlačítko nebo stisknutím klávesy **Enter** klíč.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a>Viz také

- [Hey Scripting Guy: Proč nefungují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?](https://go.microsoft.com/fwlink/?LinkId=506644)
- [Githubu: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell tipu týdne přišel: vytvoření vlastního vstupního pole](https://technet.microsoft.com/library/ff730941.aspx)
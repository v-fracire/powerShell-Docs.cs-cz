---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření grafického ovládacího prvku pro výběr data
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 6dd43a3b1f4c67633ad1755de3db88eb8c6772c8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403631"
---
# <a name="creating-a-graphical-date-picker"></a>Vytvoření grafického ovládacího prvku pro výběr data

Vytvořit formulář s grafické, kalendář – vizuální styl ovládacího prvku, který umožňuje uživateli vybrat den v měsíci pomocí Windows Powershellu 3.0 a novějších verzí.

## <a name="create-a-graphical-date-picker-control"></a>Vytvoření ovládacího prvku grafického výběr data

Zkopírujte a vložte následující do Windows PowerShell ISE a pak ho uložte jako skript Windows Powershellu (.ps1).

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object Windows.Forms.Form

$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'

$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$form.Topmost = $true

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

Skript se začne načtením dvou tříd rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**. Spusťte novou instanci třídy rozhraní .NET Framework **Windows.Forms.Form**; který obsahuje prázdný formulář nebo ovládací prvky okna, do kterého můžete začít přidávat.

```powershell
$form = New-Object Windows.Forms.Form
```

Po vytvoření instance třídy formuláře přiřadíte hodnoty třem vlastnostem této třídy.

- **Text.** Tím se změní záhlaví okna.

- **Velikost.** Toto je velikost formuláře v pixelech. Předchozí skript vytvoří formulář, který je 243 pixelů na šířku a 230 pixelů na výšku.

- **Počáteční pozice.** Tato volitelná vlastnost nastavena na **CenterScreen** v předchozím skriptu. Pokud tuto vlastnost nepřidáte, vybere Windows umístění při otevření formuláře. Tím, že nastavíte **počáteční pozice** k **CenterScreen**, automaticky zobrazená formuláři uprostřed obrazovky pokaždé, když ho načte.

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

V dalším kroku vytvořte a pak přidejte ovládací prvek calendar ve formuláři. V tomto příkladu není aktuální den zvýrazněny nebo v kruhu. Uživatelé mohou vybrat pouze jeden den v kalendáři najednou.

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

Dále vytvořte **OK** tlačítko pro daný formulář. Zadejte velikost a chování **OK** tlačítko. V tomto příkladu je pozice tlačítko 165 pixelů od horního okraje formuláře a 38 pixelů od levého okraje. Výška tlačítka je 23 pixelů, zatímco tlačítko délka je 75 pixelů. Tento skript využívá k určení chování tlačítka předdefinovaných typů formulářů Windows.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Podobně můžete vytvořit **zrušit** tlačítko. **Zrušit** je tlačítko 165 pixelů od horního, ale 113 pixelů od levého okraje okna.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Nastavte **nejvíce nahoře** vlastnost **$true** přinutit okně pro otevření imitovaná otevřená okna a dialogová okna.

```powershell
$form.Topmost = $true
```

Přidejte následující řádek kódu k zobrazení formuláře ve Windows.

```powershell
$result = $form.ShowDialog()
```

Nakonec se kód uvnitř **Pokud** bloku instruuje Windows, co dělat s formuláři uživatele vyberte den v kalendáři a pak klikněte na tlačítko **OK** tlačítko nebo stisknutím klávesy **Enter** klíč. Prostředí Windows PowerShell zobrazí vybrané datum pro uživatele.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a>Viz také

- [Dobrý den Scripting Guy:  Proč tyto příklady prostředí PowerShell grafickým uživatelským rozhraním nefungují?](https://go.microsoft.com/fwlink/?LinkId=506644)
- [GitHub: Dave Wyatt WinFormsExampleUpdates](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell tipu týdne přišel:  Vytvoření ovládacího prvku pro výběr grafické datum](https://technet.microsoft.com/library/ff730942.aspx)
---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření grafického ovládacího prvku pro výběr data
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 3727c90c314a6fc1b3a338ec60e44259f153d954
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954836"
---
# <a name="creating-a-graphical-date-picker"></a>Vytvoření grafického ovládacího prvku pro výběr data

Pomocí prostředí Windows PowerShell 3.0 a novějších verzí vytvořit formulář s grafickým rozhraním, styl kalendáře ovládací prvek, který umožňuje uživateli vybrat den v měsíci.

## <a name="create-a-graphical-date-picker-control"></a>Vytvoření ovládacího prvku grafické výběr data

Zkopírujte a vložte následující do systému Windows PowerShell ISE a pak ho uložte jako skript prostředí Windows PowerShell (.ps1).

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

Zahájí skript načtením dvě třídy rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**. Spusťte novou instanci třídy rozhraní .NET Framework **Windows.Forms.Form**; který poskytuje prázdného formuláře nebo okna, do kterého můžete začít přidávat ovládací prvky.

```powershell
$form = New-Object Windows.Forms.Form
```

Po vytvoření instance třídy formuláře, hodnoty přiřadíte tři vlastnosti této třídy.

- **Text.** To všechno bude v záhlaví okna.

- **Velikost.** Toto je velikost formuláře v pixelech. Předchozí skript vytvoří formulář, který je 243 pixelů o talovat 230 pixelů.

- **StartingPosition.** Tato volitelná vlastnost nastavena na **CenterScreen** v předchozí skript. Pokud přidáte nemusíte tuto vlastnost, systém Windows vybere umístění při otevření formuláře. Nastavením **StartingPosition** k **CenterScreen**, automaticky zobrazujete formuláře uprostřed obrazovky pokaždé, když ho načte.

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

V dalším kroku vytvořte a pak přidejte ovládacího prvku kalendář do formuláře. V tomto příkladu není po aktuálním dni zvýrazněná nebo v kroužku. Uživatelé mohou vybrat pouze jeden den v kalendáři v jednom okamžiku.

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

Dále vytvořte **OK** tlačítko pro daný formulář. Zadejte velikost a chování **OK** tlačítko. V tomto příkladu je pozice tlačítko 165 pixelů od horního okraje formuláře a 38 pixelů od levého okraje. Výška tlačítko je 23 pixelů, zatímco tlačítko délka je 75 pixelů. Skript používá předdefinovaných typů Windows Forms k určení chování tlačítko.

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

Podobně můžete vytvořit **zrušit** tlačítko. **Zrušit** tlačítko je 165 pixelů z horní části, ale 113 pixelů od levého okraje okna.

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

Nastavte **Topmost** vlastnost **$true** vynutit okno Otevřít na otevřená okna a dialogová okna.

```powershell
$form.Topmost = $true
```

Přidejte následující řádek kódu k zobrazení formuláře v systému Windows.

```powershell
$result = $form.ShowDialog()
```

Nakonec se kód uvnitř **Pokud** bloku dá pokyn Windows co dělat s formulářem po uživatelům vybrat den v kalendáři a pak klikněte na tlačítko **OK** tlačítko nebo klikněte na tlačítko **Enter** klíč. Prostředí Windows PowerShell zobrazí vybraným datem pro uživatele.

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a>Viz také

- [Hey Scripting Guy: Proč se nepodporují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?](http://go.microsoft.com/fwlink/?LinkId=506644)
- [Githubu: WinFormsExampleUpdates Dave Wyatt](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [Windows PowerShell Tip v týdnu: vytváření výběr grafické data](http://technet.microsoft.com/library/ff730942.aspx)
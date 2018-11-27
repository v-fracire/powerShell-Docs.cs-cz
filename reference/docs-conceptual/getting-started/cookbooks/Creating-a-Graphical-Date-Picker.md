---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření grafického ovládacího prvku pro výběr data
ms.assetid: c1cb722c-41e9-4baa-be83-59b4653222e9
ms.openlocfilehash: 6dd43a3b1f4c67633ad1755de3db88eb8c6772c8
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320325"
---
# <a name="creating-a-graphical-date-picker"></a><span data-ttu-id="a7171-103">Vytvoření grafického ovládacího prvku pro výběr data</span><span class="sxs-lookup"><span data-stu-id="a7171-103">Creating a Graphical Date Picker</span></span>

<span data-ttu-id="a7171-104">Vytvořit formulář s grafické, kalendář – vizuální styl ovládacího prvku, který umožňuje uživateli vybrat den v měsíci pomocí Windows Powershellu 3.0 a novějších verzí.</span><span class="sxs-lookup"><span data-stu-id="a7171-104">Use Windows PowerShell 3.0 and later releases to create a form with a graphical, calendar-style control that lets users select a day of the month.</span></span>

## <a name="create-a-graphical-date-picker-control"></a><span data-ttu-id="a7171-105">Vytvoření ovládacího prvku grafického výběr data</span><span class="sxs-lookup"><span data-stu-id="a7171-105">Create a graphical date-picker control</span></span>

<span data-ttu-id="a7171-106">Zkopírujte a vložte následující do Windows PowerShell ISE a pak ho uložte jako skript Windows Powershellu (.ps1).</span><span class="sxs-lookup"><span data-stu-id="a7171-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="a7171-107">Spustí skript načtením dvou tříd rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="a7171-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="a7171-108">Spusťte novou instanci třídy rozhraní .NET Framework **Windows.Forms.Form**; který obsahuje prázdný formulář nebo ovládací prvky okna, do kterého můžete začít přidávat.</span><span class="sxs-lookup"><span data-stu-id="a7171-108">You then start a new instance of the .NET Framework class **Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object Windows.Forms.Form
```

<span data-ttu-id="a7171-109">Po vytvoření instance třídy formuláře přiřadíte hodnoty třem vlastnostem této třídy.</span><span class="sxs-lookup"><span data-stu-id="a7171-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="a7171-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="a7171-110">**Text.**</span></span> <span data-ttu-id="a7171-111">Tím se změní záhlaví okna.</span><span class="sxs-lookup"><span data-stu-id="a7171-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="a7171-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="a7171-112">**Size.**</span></span> <span data-ttu-id="a7171-113">Toto je velikost formuláře v pixelech.</span><span class="sxs-lookup"><span data-stu-id="a7171-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="a7171-114">Předchozí skript vytvoří formulář, který je 243 pixelů na šířku a 230 pixelů na výšku.</span><span class="sxs-lookup"><span data-stu-id="a7171-114">The preceding script creates a form that’s 243 pixels wide by 230 pixels tall.</span></span>

- <span data-ttu-id="a7171-115">**Počáteční pozice.**</span><span class="sxs-lookup"><span data-stu-id="a7171-115">**StartingPosition.**</span></span> <span data-ttu-id="a7171-116">Tato volitelná vlastnost nastavena na **CenterScreen** v předchozím skriptu.</span><span class="sxs-lookup"><span data-stu-id="a7171-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="a7171-117">Pokud tuto vlastnost nepřidáte, vybere Windows umístění při otevření formuláře.</span><span class="sxs-lookup"><span data-stu-id="a7171-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="a7171-118">Tím, že nastavíte **počáteční pozice** k **CenterScreen**, automaticky zobrazená formuláři uprostřed obrazovky pokaždé, když ho načte.</span><span class="sxs-lookup"><span data-stu-id="a7171-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="a7171-119">V dalším kroku vytvořte a pak přidejte ovládací prvek calendar ve formuláři.</span><span class="sxs-lookup"><span data-stu-id="a7171-119">Next, create and then add a calendar control in your form.</span></span> <span data-ttu-id="a7171-120">V tomto příkladu není aktuální den zvýrazněny nebo v kruhu.</span><span class="sxs-lookup"><span data-stu-id="a7171-120">In this example, the current day is not highlighted or circled.</span></span> <span data-ttu-id="a7171-121">Uživatelé mohou vybrat pouze jeden den v kalendáři najednou.</span><span class="sxs-lookup"><span data-stu-id="a7171-121">Users can select only one day on the calendar at one time.</span></span>

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

<span data-ttu-id="a7171-122">Dále vytvořte **OK** tlačítko pro daný formulář.</span><span class="sxs-lookup"><span data-stu-id="a7171-122">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="a7171-123">Zadejte velikost a chování **OK** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="a7171-123">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="a7171-124">V tomto příkladu je pozice tlačítko 165 pixelů od horního okraje formuláře a 38 pixelů od levého okraje.</span><span class="sxs-lookup"><span data-stu-id="a7171-124">In this example, the button position is 165 pixels from the form’s top edge, and 38 pixels from the left edge.</span></span> <span data-ttu-id="a7171-125">Výška tlačítka je 23 pixelů, zatímco tlačítko délka je 75 pixelů.</span><span class="sxs-lookup"><span data-stu-id="a7171-125">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="a7171-126">Tento skript využívá k určení chování tlačítka předdefinovaných typů formulářů Windows.</span><span class="sxs-lookup"><span data-stu-id="a7171-126">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="a7171-127">Podobně můžete vytvořit **zrušit** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="a7171-127">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="a7171-128">**Zrušit** je tlačítko 165 pixelů od horního, ale 113 pixelů od levého okraje okna.</span><span class="sxs-lookup"><span data-stu-id="a7171-128">The **Cancel** button is 165 pixels from the top, but 113 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="a7171-129">Nastavte **nejvíce nahoře** vlastnost **$true** přinutit okně pro otevření imitovaná otevřená okna a dialogová okna.</span><span class="sxs-lookup"><span data-stu-id="a7171-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="a7171-130">Přidejte následující řádek kódu k zobrazení formuláře ve Windows.</span><span class="sxs-lookup"><span data-stu-id="a7171-130">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="a7171-131">Nakonec se kód uvnitř **Pokud** bloku instruuje Windows, co dělat s formuláři uživatele vyberte den v kalendáři a pak klikněte na tlačítko **OK** tlačítko nebo stisknutím klávesy **Enter** klíč.</span><span class="sxs-lookup"><span data-stu-id="a7171-131">Finally, the code inside the **If** block instructs Windows what to do with the form after users select a day on the calendar, and then click the **OK** button or press the **Enter** key.</span></span> <span data-ttu-id="a7171-132">Prostředí Windows PowerShell zobrazí vybrané datum pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="a7171-132">Windows PowerShell displays the selected date to users.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a><span data-ttu-id="a7171-133">Viz také</span><span class="sxs-lookup"><span data-stu-id="a7171-133">See Also</span></span>

- [<span data-ttu-id="a7171-134">Hey Scripting Guy: Proč nefungují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?</span><span class="sxs-lookup"><span data-stu-id="a7171-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="a7171-135">Githubu: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="a7171-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="a7171-136">Windows PowerShell tipu týdne přišel: vytvoření ovládacího prvku pro výběr grafické datum</span><span class="sxs-lookup"><span data-stu-id="a7171-136">Windows PowerShell Tip of the Week:  Creating a Graphical Date Picker</span></span>](https://technet.microsoft.com/library/ff730942.aspx)
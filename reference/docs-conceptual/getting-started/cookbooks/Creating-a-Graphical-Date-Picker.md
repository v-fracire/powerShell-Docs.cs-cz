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
# <a name="creating-a-graphical-date-picker"></a><span data-ttu-id="5413a-103">Vytvoření grafického ovládacího prvku pro výběr data</span><span class="sxs-lookup"><span data-stu-id="5413a-103">Creating a Graphical Date Picker</span></span>

<span data-ttu-id="5413a-104">Pomocí prostředí Windows PowerShell 3.0 a novějších verzí vytvořit formulář s grafickým rozhraním, styl kalendáře ovládací prvek, který umožňuje uživateli vybrat den v měsíci.</span><span class="sxs-lookup"><span data-stu-id="5413a-104">Use Windows PowerShell 3.0 and later releases to create a form with a graphical, calendar-style control that lets users select a day of the month.</span></span>

## <a name="create-a-graphical-date-picker-control"></a><span data-ttu-id="5413a-105">Vytvoření ovládacího prvku grafické výběr data</span><span class="sxs-lookup"><span data-stu-id="5413a-105">Create a graphical date-picker control</span></span>

<span data-ttu-id="5413a-106">Zkopírujte a vložte následující do systému Windows PowerShell ISE a pak ho uložte jako skript prostředí Windows PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="5413a-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="5413a-107">Zahájí skript načtením dvě třídy rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="5413a-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="5413a-108">Spusťte novou instanci třídy rozhraní .NET Framework **Windows.Forms.Form**; který poskytuje prázdného formuláře nebo okna, do kterého můžete začít přidávat ovládací prvky.</span><span class="sxs-lookup"><span data-stu-id="5413a-108">You then start a new instance of the .NET Framework class **Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object Windows.Forms.Form
```

<span data-ttu-id="5413a-109">Po vytvoření instance třídy formuláře, hodnoty přiřadíte tři vlastnosti této třídy.</span><span class="sxs-lookup"><span data-stu-id="5413a-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="5413a-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="5413a-110">**Text.**</span></span> <span data-ttu-id="5413a-111">To všechno bude v záhlaví okna.</span><span class="sxs-lookup"><span data-stu-id="5413a-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="5413a-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="5413a-112">**Size.**</span></span> <span data-ttu-id="5413a-113">Toto je velikost formuláře v pixelech.</span><span class="sxs-lookup"><span data-stu-id="5413a-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="5413a-114">Předchozí skript vytvoří formulář, který je 243 pixelů o talovat 230 pixelů.</span><span class="sxs-lookup"><span data-stu-id="5413a-114">The preceding script creates a form that’s 243 pixels wide by 230 pixels tall.</span></span>

- <span data-ttu-id="5413a-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="5413a-115">**StartingPosition.**</span></span> <span data-ttu-id="5413a-116">Tato volitelná vlastnost nastavena na **CenterScreen** v předchozí skript.</span><span class="sxs-lookup"><span data-stu-id="5413a-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="5413a-117">Pokud přidáte nemusíte tuto vlastnost, systém Windows vybere umístění při otevření formuláře.</span><span class="sxs-lookup"><span data-stu-id="5413a-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="5413a-118">Nastavením **StartingPosition** k **CenterScreen**, automaticky zobrazujete formuláře uprostřed obrazovky pokaždé, když ho načte.</span><span class="sxs-lookup"><span data-stu-id="5413a-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Select a Date'
$form.Size = New-Object Drawing.Size @(243,230)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="5413a-119">V dalším kroku vytvořte a pak přidejte ovládacího prvku kalendář do formuláře.</span><span class="sxs-lookup"><span data-stu-id="5413a-119">Next, create and then add a calendar control in your form.</span></span> <span data-ttu-id="5413a-120">V tomto příkladu není po aktuálním dni zvýrazněná nebo v kroužku.</span><span class="sxs-lookup"><span data-stu-id="5413a-120">In this example, the current day is not highlighted or circled.</span></span> <span data-ttu-id="5413a-121">Uživatelé mohou vybrat pouze jeden den v kalendáři v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="5413a-121">Users can select only one day on the calendar at one time.</span></span>

```powershell
$calendar = New-Object System.Windows.Forms.MonthCalendar
$calendar.ShowTodayCircle = $false
$calendar.MaxSelectionCount = 1
$form.Controls.Add($calendar)
```

<span data-ttu-id="5413a-122">Dále vytvořte **OK** tlačítko pro daný formulář.</span><span class="sxs-lookup"><span data-stu-id="5413a-122">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="5413a-123">Zadejte velikost a chování **OK** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="5413a-123">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="5413a-124">V tomto příkladu je pozice tlačítko 165 pixelů od horního okraje formuláře a 38 pixelů od levého okraje.</span><span class="sxs-lookup"><span data-stu-id="5413a-124">In this example, the button position is 165 pixels from the form’s top edge, and 38 pixels from the left edge.</span></span> <span data-ttu-id="5413a-125">Výška tlačítko je 23 pixelů, zatímco tlačítko délka je 75 pixelů.</span><span class="sxs-lookup"><span data-stu-id="5413a-125">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="5413a-126">Skript používá předdefinovaných typů Windows Forms k určení chování tlačítko.</span><span class="sxs-lookup"><span data-stu-id="5413a-126">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(38,165)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="5413a-127">Podobně můžete vytvořit **zrušit** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="5413a-127">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="5413a-128">**Zrušit** tlačítko je 165 pixelů z horní části, ale 113 pixelů od levého okraje okna.</span><span class="sxs-lookup"><span data-stu-id="5413a-128">The **Cancel** button is 165 pixels from the top, but 113 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(113,165)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="5413a-129">Nastavte **Topmost** vlastnost **$true** vynutit okno Otevřít na otevřená okna a dialogová okna.</span><span class="sxs-lookup"><span data-stu-id="5413a-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="5413a-130">Přidejte následující řádek kódu k zobrazení formuláře v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="5413a-130">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="5413a-131">Nakonec se kód uvnitř **Pokud** bloku dá pokyn Windows co dělat s formulářem po uživatelům vybrat den v kalendáři a pak klikněte na tlačítko **OK** tlačítko nebo klikněte na tlačítko **Enter** klíč.</span><span class="sxs-lookup"><span data-stu-id="5413a-131">Finally, the code inside the **If** block instructs Windows what to do with the form after users select a day on the calendar, and then click the **OK** button or press the **Enter** key.</span></span> <span data-ttu-id="5413a-132">Prostředí Windows PowerShell zobrazí vybraným datem pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="5413a-132">Windows PowerShell displays the selected date to users.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $date = $calendar.SelectionStart
    Write-Host "Date selected: $($date.ToShortDateString())"
}
```

## <a name="see-also"></a><span data-ttu-id="5413a-133">Viz také</span><span class="sxs-lookup"><span data-stu-id="5413a-133">See Also</span></span>

- [<span data-ttu-id="5413a-134">Hey Scripting Guy: Proč se nepodporují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?</span><span class="sxs-lookup"><span data-stu-id="5413a-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="5413a-135">Githubu: WinFormsExampleUpdates Dave Wyatt</span><span class="sxs-lookup"><span data-stu-id="5413a-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="5413a-136">Windows PowerShell Tip v týdnu: vytváření výběr grafické data</span><span class="sxs-lookup"><span data-stu-id="5413a-136">Windows PowerShell Tip of the Week:  Creating a Graphical Date Picker</span></span>](http://technet.microsoft.com/library/ff730942.aspx)
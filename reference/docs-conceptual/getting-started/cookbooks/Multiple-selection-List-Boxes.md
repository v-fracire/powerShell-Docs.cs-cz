---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Vícenásobný výběr seznamy"
ms.assetid: f74cd5d9-da57-4802-b614-0b194a7bc8f8
ms.openlocfilehash: 122014888bc5cf93c1c709b9d534d572037f5ffe
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="multiple-selection-list-boxes"></a><span data-ttu-id="632bd-103">Výběr více seznamy</span><span class="sxs-lookup"><span data-stu-id="632bd-103">Multiple-selection List Boxes</span></span>
<span data-ttu-id="632bd-104">Vytvoření ovládacího prvku seznam s vícenásobným výběrem pole ve formuláři Windows vlastní pomocí prostředí Windows PowerShell 3.0 a novějších verzí.</span><span class="sxs-lookup"><span data-stu-id="632bd-104">Use Windows PowerShell 3.0 and later releases to create a multiple-selection list box control in a custom Windows Form.</span></span>

## <a name="create-list-box-controls-that-allow-multiple-selections"></a><span data-ttu-id="632bd-105">Vytvoření seznamu ovládacích prvků pole, které umožňují více výběrů</span><span class="sxs-lookup"><span data-stu-id="632bd-105">Create list box controls that allow multiple selections</span></span>
<span data-ttu-id="632bd-106">Zkopírujte a vložte následující do systému Windows PowerShell ISE a pak ho uložte jako skript prostředí Windows PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="632bd-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

```
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

$form = New-Object System.Windows.Forms.Form 
$form.Text = "Data Entry Form"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"

$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)

$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)

$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please make a selection from the list below:"
$form.Controls.Add($label) 

$listBox = New-Object System.Windows.Forms.Listbox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20) 

$listBox.SelectionMode = "MultiExtended"

[void] $listBox.Items.Add("Item 1")
[void] $listBox.Items.Add("Item 2")
[void] $listBox.Items.Add("Item 3")
[void] $listBox.Items.Add("Item 4")
[void] $listBox.Items.Add("Item 5")

$listBox.Height = 70
$form.Controls.Add($listBox) 
$form.Topmost = $True

$result = $form.ShowDialog()

if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

<span data-ttu-id="632bd-107">Zahájí skript načtením dvě třídy rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="632bd-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="632bd-108">Spusťte novou instanci třídy rozhraní .NET Framework **formuláře System.Windows.Forms.Form**; který poskytuje prázdného formuláře nebo okna, do kterého můžete začít přidávat ovládací prvky.</span><span class="sxs-lookup"><span data-stu-id="632bd-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="632bd-109">Po vytvoření instance třídy formuláře, hodnoty přiřadíte tři vlastnosti této třídy.</span><span class="sxs-lookup"><span data-stu-id="632bd-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="632bd-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="632bd-110">**Text.**</span></span> <span data-ttu-id="632bd-111">To všechno bude v záhlaví okna.</span><span class="sxs-lookup"><span data-stu-id="632bd-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="632bd-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="632bd-112">**Size.**</span></span> <span data-ttu-id="632bd-113">Toto je velikost formuláře v pixelech.</span><span class="sxs-lookup"><span data-stu-id="632bd-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="632bd-114">Předchozí skript vytvoří formulář, který je 300 × široké 200 pixelů vysoký.</span><span class="sxs-lookup"><span data-stu-id="632bd-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="632bd-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="632bd-115">**StartingPosition.**</span></span> <span data-ttu-id="632bd-116">Tato volitelná vlastnost nastavena na **CenterScreen** v předchozí skript.</span><span class="sxs-lookup"><span data-stu-id="632bd-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="632bd-117">Pokud přidáte nemusíte tuto vlastnost, systém Windows vybere umístění při otevření formuláře.</span><span class="sxs-lookup"><span data-stu-id="632bd-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="632bd-118">Nastavením **StartingPosition** k **CenterScreen**, automaticky zobrazujete formuláře uprostřed obrazovky pokaždé, když ho načte.</span><span class="sxs-lookup"><span data-stu-id="632bd-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```
$form.Text = "Data Entry Form"
$form.Size = New-Object System.Drawing.Size(300,200) 
$form.StartPosition = "CenterScreen"
```

<span data-ttu-id="632bd-119">Dále vytvořte **OK** tlačítko pro daný formulář.</span><span class="sxs-lookup"><span data-stu-id="632bd-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="632bd-120">Zadejte velikost a chování **OK** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="632bd-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="632bd-121">V tomto příkladu je pozice tlačítko 120 pixelů od horního okraje formuláře a 75 pixelů od levého okraje.</span><span class="sxs-lookup"><span data-stu-id="632bd-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="632bd-122">Výška tlačítko je 23 pixelů, zatímco tlačítko délka je 75 pixelů.</span><span class="sxs-lookup"><span data-stu-id="632bd-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="632bd-123">Skript používá předdefinovaných typů Windows Forms k určení chování tlačítko.</span><span class="sxs-lookup"><span data-stu-id="632bd-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = "OK"
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="632bd-124">Podobně můžete vytvořit **zrušit** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="632bd-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="632bd-125">**Zrušit** tlačítko je 120 pixelů z horní části, ale 150 pixelů od levého okraje okna.</span><span class="sxs-lookup"><span data-stu-id="632bd-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = "Cancel"
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="632bd-126">Potom zadejte text popisku na vaše okno, které popisuje informace, které chcete, aby uživatelé zadali.</span><span class="sxs-lookup"><span data-stu-id="632bd-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20) 
$label.Size = New-Object System.Drawing.Size(280,20) 
$label.Text = "Please make a selection from the list below:"
$form.Controls.Add($label)
```

<span data-ttu-id="632bd-127">Přidání ovládacího prvku (v tomto případě pole se seznamem), která umožňuje uživatelům poskytnout informace, které jste popsaných v textu popisku.</span><span class="sxs-lookup"><span data-stu-id="632bd-127">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="632bd-128">Existuje mnoho dalších ovládacích prvků, které můžete použít kromě polí; pro další ovládací prvky, najdete v části [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="632bd-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```
$listBox = New-Object System.Windows.Forms.Listbox 
$listBox.Location = New-Object System.Drawing.Point(10,40) 
$listBox.Size = New-Object System.Drawing.Size(260,20)
```


<span data-ttu-id="632bd-129">Zde je, jak určíte, že chcete povolit uživatelům výběr více hodnot v seznamu.</span><span class="sxs-lookup"><span data-stu-id="632bd-129">Here’s how you specify that you want to allow users to select multiple values from the list.</span></span>

```
$listBox.SelectionMode = "MultiExtended"
```

<span data-ttu-id="632bd-130">V další části zadejte hodnoty, které chcete zobrazit uživatelům v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="632bd-130">In the next section, you specify the values you want the list box to display to users.</span></span>

```
[void] $listBox.Items.Add("Item 1")
[void] $listBox.Items.Add("Item 2")
[void] $listBox.Items.Add("Item 3")
[void] $listBox.Items.Add("Item 4")
[void] $listBox.Items.Add("Item 5")
```

<span data-ttu-id="632bd-131">Zadejte maximální výšku ovládací prvek seznam.</span><span class="sxs-lookup"><span data-stu-id="632bd-131">Specify the maximum height of the list box control.</span></span>

```
$listBox.Height = 70
```

<span data-ttu-id="632bd-132">Přidejte do svého formuláře ovládací prvek seznam a Vyzvěte Windows otevřete formulář na jiné windows a dialogových oken při otevření.</span><span class="sxs-lookup"><span data-stu-id="632bd-132">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```
$form.Controls.Add($listBox) 
$form.Topmost = $True
```

<span data-ttu-id="632bd-133">Přidejte následující řádek kódu k zobrazení formuláře v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="632bd-133">Add the following line of code to display the form in Windows.</span></span>

```
$result = $form.ShowDialog()
```

<span data-ttu-id="632bd-134">Nakonec se kód uvnitř **Pokud** bloku dá pokyn Windows co dělat s formulářem po uživatele ze seznamu vyberte jednu nebo více možností a pak klikněte na tlačítko **OK** tlačítko nebo klikněte na tlačítko **Enter**  klíč.</span><span class="sxs-lookup"><span data-stu-id="632bd-134">Finally, the code inside the **If** block instructs Windows what to do with the form after users select one or more options from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="632bd-135">Viz také</span><span class="sxs-lookup"><span data-stu-id="632bd-135">See Also</span></span>
- [<span data-ttu-id="632bd-136">Hey Scripting Guy: Proč se nepodporují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?</span><span class="sxs-lookup"><span data-stu-id="632bd-136">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="632bd-137">Githubu: WinFormsExampleUpdates Dave Wyatt</span><span class="sxs-lookup"><span data-stu-id="632bd-137">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="632bd-138">Windows PowerShell Tip v týdnu: vícenásobný výběr v seznamu polí - a další!</span><span class="sxs-lookup"><span data-stu-id="632bd-138">Windows PowerShell Tip of the Week:  Multi-Select List Boxes - And More!</span></span>](http://technet.microsoft.com/library/ff730950.aspx)


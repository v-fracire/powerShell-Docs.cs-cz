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
ms.locfileid: "30951677"
---
# <a name="selecting-items-from-a-list-box"></a><span data-ttu-id="f596a-103">Výběr položek ze seznamu</span><span class="sxs-lookup"><span data-stu-id="f596a-103">Selecting Items from a List Box</span></span>

<span data-ttu-id="f596a-104">K vytvoření dialogu, který umožňuje uživatelům výběru položek z ovládací prvek seznamu, použijte prostředí Windows PowerShell 3.0 a novějších verzí.</span><span class="sxs-lookup"><span data-stu-id="f596a-104">Use Windows PowerShell 3.0 and later releases to create a dialog box that lets users select items from a list box control.</span></span>

## <a name="create-a-list-box-control-and-select-items-from-it"></a><span data-ttu-id="f596a-105">Vytvořte ovládací prvek seznamu a vyberte položky z něj</span><span class="sxs-lookup"><span data-stu-id="f596a-105">Create a list box control, and select items from it</span></span>

<span data-ttu-id="f596a-106">Zkopírujte a vložte následující do systému Windows PowerShell ISE a pak ho uložte jako skript prostředí Windows PowerShell (.ps1).</span><span class="sxs-lookup"><span data-stu-id="f596a-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="f596a-107">Zahájí skript načtením dvě třídy rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="f596a-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="f596a-108">Spusťte novou instanci třídy rozhraní .NET Framework **formuláře System.Windows.Forms.Form**; který poskytuje prázdného formuláře nebo okna, do kterého můžete začít přidávat ovládací prvky.</span><span class="sxs-lookup"><span data-stu-id="f596a-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
```

<span data-ttu-id="f596a-109">Po vytvoření instance třídy formuláře, hodnoty přiřadíte tři vlastnosti této třídy.</span><span class="sxs-lookup"><span data-stu-id="f596a-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="f596a-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="f596a-110">**Text.**</span></span> <span data-ttu-id="f596a-111">To všechno bude v záhlaví okna.</span><span class="sxs-lookup"><span data-stu-id="f596a-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="f596a-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="f596a-112">**Size.**</span></span> <span data-ttu-id="f596a-113">Toto je velikost formuláře v pixelech.</span><span class="sxs-lookup"><span data-stu-id="f596a-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="f596a-114">Předchozí skript vytvoří formulář, který je 300 × široké 200 pixelů vysoký.</span><span class="sxs-lookup"><span data-stu-id="f596a-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="f596a-115">**StartingPosition.**</span><span class="sxs-lookup"><span data-stu-id="f596a-115">**StartingPosition.**</span></span> <span data-ttu-id="f596a-116">Tato volitelná vlastnost nastavena na **CenterScreen** v předchozí skript.</span><span class="sxs-lookup"><span data-stu-id="f596a-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="f596a-117">Pokud přidáte nemusíte tuto vlastnost, systém Windows vybere umístění při otevření formuláře.</span><span class="sxs-lookup"><span data-stu-id="f596a-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="f596a-118">Nastavením **StartingPosition** k **CenterScreen**, automaticky zobrazujete formuláře uprostřed obrazovky pokaždé, když ho načte.</span><span class="sxs-lookup"><span data-stu-id="f596a-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Select a Computer'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="f596a-119">Dále vytvořte **OK** tlačítko pro daný formulář.</span><span class="sxs-lookup"><span data-stu-id="f596a-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="f596a-120">Zadejte velikost a chování **OK** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="f596a-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="f596a-121">V tomto příkladu je pozice tlačítko 120 pixelů od horního okraje formuláře a 75 pixelů od levého okraje.</span><span class="sxs-lookup"><span data-stu-id="f596a-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="f596a-122">Výška tlačítko je 23 pixelů, zatímco tlačítko délka je 75 pixelů.</span><span class="sxs-lookup"><span data-stu-id="f596a-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="f596a-123">Skript používá předdefinovaných typů Windows Forms k určení chování tlačítko.</span><span class="sxs-lookup"><span data-stu-id="f596a-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="f596a-124">Podobně můžete vytvořit **zrušit** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="f596a-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="f596a-125">**Zrušit** tlačítko je 120 pixelů z horní části, ale 150 pixelů od levého okraje okna.</span><span class="sxs-lookup"><span data-stu-id="f596a-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="f596a-126">Potom zadejte text popisku na vaše okno, které popisuje informace, které chcete, aby uživatelé zadali.</span><span class="sxs-lookup"><span data-stu-id="f596a-126">Next, provide label text on your window that describes the information you want users to provide.</span></span> <span data-ttu-id="f596a-127">V takovém případě budete chtít uživatelům vyberte počítač.</span><span class="sxs-lookup"><span data-stu-id="f596a-127">In this case, you want users to select a computer.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please select a computer:'
$form.Controls.Add($label)
```

<span data-ttu-id="f596a-128">Přidání ovládacího prvku (v tomto případě pole se seznamem), která umožňuje uživatelům poskytnout informace, které jste popsaných v textu popisku.</span><span class="sxs-lookup"><span data-stu-id="f596a-128">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="f596a-129">Existuje mnoho dalších ovládacích prvků, které můžete použít kromě seznamy; pro další ovládací prvky, najdete v části [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="f596a-129">There are many other controls you can apply besides list boxes; for more controls, see [System.Windows.Forms Namespace](http://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$listBox = New-Object System.Windows.Forms.ListBox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
$listBox.Height = 80
```

<span data-ttu-id="f596a-130">V další části zadejte hodnoty, které chcete zobrazit uživatelům v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="f596a-130">In the next section, you specify the values you want the list box to display to users.</span></span>

> [!NOTE]
> <span data-ttu-id="f596a-131">Pole se seznamem tento skript vytvořený umožňuje pouze jeden výběr.</span><span class="sxs-lookup"><span data-stu-id="f596a-131">The list box created by this script allows only one selection.</span></span> <span data-ttu-id="f596a-132">Pokud chcete vytvořit rozevírací seznam, který umožňuje více výběrů, zadejte hodnotu pro **SelectionMode** vlastnost, podobně jako následující: `$listBox.SelectionMode = 'MultiExtended'`.</span><span class="sxs-lookup"><span data-stu-id="f596a-132">To create a list box control that allows multiple selections, specify a value for the **SelectionMode** property, similarly to the following:  `$listBox.SelectionMode = 'MultiExtended'`.</span></span> <span data-ttu-id="f596a-133">Další informace najdete v tématu [vícenásobného výběru seznamy](Multiple-selection-List-Boxes.md).</span><span class="sxs-lookup"><span data-stu-id="f596a-133">For more information, see [Multiple-selection List Boxes](Multiple-selection-List-Boxes.md).</span></span>

```powershell
[void] $listBox.Items.Add('atl-dc-001')
[void] $listBox.Items.Add('atl-dc-002')
[void] $listBox.Items.Add('atl-dc-003')
[void] $listBox.Items.Add('atl-dc-004')
[void] $listBox.Items.Add('atl-dc-005')
[void] $listBox.Items.Add('atl-dc-006')
[void] $listBox.Items.Add('atl-dc-007')
```

<span data-ttu-id="f596a-134">Přidejte do svého formuláře ovládací prvek seznam a Vyzvěte Windows otevřete formulář na jiné windows a dialogových oken při otevření.</span><span class="sxs-lookup"><span data-stu-id="f596a-134">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

<span data-ttu-id="f596a-135">Přidejte následující řádek kódu k zobrazení formuláře v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="f596a-135">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="f596a-136">Nakonec se kód uvnitř **Pokud** bloku dá pokyn Windows co dělat s formulářem po uživatelů vyberte možnost ze seznamu a pak klikněte na tlačítko **OK** tlačítko nebo klikněte na tlačítko **Enter**klíč.</span><span class="sxs-lookup"><span data-stu-id="f596a-136">Finally, the code inside the **If** block instructs Windows what to do with the form after users select an option from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItem
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="f596a-137">Viz také</span><span class="sxs-lookup"><span data-stu-id="f596a-137">See Also</span></span>

- [<span data-ttu-id="f596a-138">Hey Scripting Guy: Proč se nepodporují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?</span><span class="sxs-lookup"><span data-stu-id="f596a-138">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](http://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="f596a-139">Githubu: WinFormsExampleUpdates Dave Wyatt</span><span class="sxs-lookup"><span data-stu-id="f596a-139">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="f596a-140">Windows PowerShell Tip v týdnu: výběr položek ze seznamu</span><span class="sxs-lookup"><span data-stu-id="f596a-140">Windows PowerShell Tip of the Week:  Selecting Items from a List Box</span></span>](http://technet.microsoft.com/library/ff730949.aspx)
---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Pole se seznamem umožňujícím vícenásobný výběr
ms.assetid: f74cd5d9-da57-4802-b614-0b194a7bc8f8
ms.openlocfilehash: a762145dc197ec7e1424b2fbdcef5e7380d13803
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320971"
---
# <a name="multiple-selection-list-boxes"></a><span data-ttu-id="f81e4-103">Pole se seznamem vícenásobného výběru</span><span class="sxs-lookup"><span data-stu-id="f81e4-103">Multiple-selection List Boxes</span></span>

<span data-ttu-id="f81e4-104">Vytvoření ovládacího prvku seznamu s vícenásobným výběrem pole ve formuláři Windows vlastní pomocí Windows Powershellu 3.0 a novějších verzí.</span><span class="sxs-lookup"><span data-stu-id="f81e4-104">Use Windows PowerShell 3.0 and later releases to create a multiple-selection list box control in a custom Windows Form.</span></span>

## <a name="create-list-box-controls-that-allow-multiple-selections"></a><span data-ttu-id="f81e4-105">Vytvoření seznamu ovládací prvky, které umožňují více výběrů</span><span class="sxs-lookup"><span data-stu-id="f81e4-105">Create list box controls that allow multiple selections</span></span>

<span data-ttu-id="f81e4-106">Zkopírujte a vložte následující do Windows PowerShell ISE a pak ho uložte jako skript Windows Powershellu (.ps1).</span><span class="sxs-lookup"><span data-stu-id="f81e4-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="f81e4-107">Spustí skript načtením dvou tříd rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="f81e4-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="f81e4-108">Spusťte novou instanci třídy rozhraní .NET Framework **formuláře System.Windows.Forms.Form**; který obsahuje prázdný formulář nebo ovládací prvky okna, do kterého můžete začít přidávat.</span><span class="sxs-lookup"><span data-stu-id="f81e4-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="f81e4-109">Po vytvoření instance třídy formuláře přiřadíte hodnoty třem vlastnostem této třídy.</span><span class="sxs-lookup"><span data-stu-id="f81e4-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="f81e4-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="f81e4-110">**Text.**</span></span> <span data-ttu-id="f81e4-111">Tím se změní záhlaví okna.</span><span class="sxs-lookup"><span data-stu-id="f81e4-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="f81e4-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="f81e4-112">**Size.**</span></span> <span data-ttu-id="f81e4-113">Toto je velikost formuláře v pixelech.</span><span class="sxs-lookup"><span data-stu-id="f81e4-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="f81e4-114">Předchozí skript vytvoří formulář, který je 300 pixelů na šířku a 200 pixelů na výšku.</span><span class="sxs-lookup"><span data-stu-id="f81e4-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="f81e4-115">**Počáteční pozice.**</span><span class="sxs-lookup"><span data-stu-id="f81e4-115">**StartingPosition.**</span></span> <span data-ttu-id="f81e4-116">Tato volitelná vlastnost nastavena na **CenterScreen** v předchozím skriptu.</span><span class="sxs-lookup"><span data-stu-id="f81e4-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="f81e4-117">Pokud tuto vlastnost nepřidáte, vybere Windows umístění při otevření formuláře.</span><span class="sxs-lookup"><span data-stu-id="f81e4-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="f81e4-118">Tím, že nastavíte **počáteční pozice** k **CenterScreen**, automaticky zobrazená formuláři uprostřed obrazovky pokaždé, když ho načte.</span><span class="sxs-lookup"><span data-stu-id="f81e4-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="f81e4-119">Dále vytvořte **OK** tlačítko pro daný formulář.</span><span class="sxs-lookup"><span data-stu-id="f81e4-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="f81e4-120">Zadejte velikost a chování **OK** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="f81e4-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="f81e4-121">V tomto příkladu je pozice tlačítko 120 pixelů od horního okraje formuláře a 75 pixelů od levého okraje.</span><span class="sxs-lookup"><span data-stu-id="f81e4-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="f81e4-122">Výška tlačítka je 23 pixelů, zatímco tlačítko délka je 75 pixelů.</span><span class="sxs-lookup"><span data-stu-id="f81e4-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="f81e4-123">Tento skript využívá k určení chování tlačítka předdefinovaných typů formulářů Windows.</span><span class="sxs-lookup"><span data-stu-id="f81e4-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Size(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="f81e4-124">Podobně můžete vytvořit **zrušit** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="f81e4-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="f81e4-125">**Zrušit** tlačítko je 120 pixelů od horního, ale 150 pixelů od levého okraje okna.</span><span class="sxs-lookup"><span data-stu-id="f81e4-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="f81e4-126">Pak zadejte popisek v okně, který popisuje informace, na kterých chcete, aby uživatelé zadali.</span><span class="sxs-lookup"><span data-stu-id="f81e4-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please make a selection from the list below:'
$form.Controls.Add($label)
```

<span data-ttu-id="f81e4-127">Přidejte ovládací prvek (v tomto případě seznamu), která umožňuje uživatelům poskytnout informace, které jste je popsáno v textu popisku.</span><span class="sxs-lookup"><span data-stu-id="f81e4-127">Add the control (in this case, a list box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="f81e4-128">Existuje mnoho dalších ovládacích prvků, platí kromě textová pole; pro větší počet kontrolních mechanismů, naleznete v tématu [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) na webové stránce MSDN.</span><span class="sxs-lookup"><span data-stu-id="f81e4-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$listBox = New-Object System.Windows.Forms.Listbox
$listBox.Location = New-Object System.Drawing.Point(10,40)
$listBox.Size = New-Object System.Drawing.Size(260,20)
```

<span data-ttu-id="f81e4-129">Zde je, jak určit, že chcete povolit uživatelům výběr více hodnot v seznamu.</span><span class="sxs-lookup"><span data-stu-id="f81e4-129">Here’s how you specify that you want to allow users to select multiple values from the list.</span></span>

```powershell
$listBox.SelectionMode = 'MultiExtended'
```

<span data-ttu-id="f81e4-130">V další části zadejte hodnoty, které chcete uživatelům zobrazit v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="f81e4-130">In the next section, you specify the values you want the list box to display to users.</span></span>

```powershell
[void] $listBox.Items.Add('Item 1')
[void] $listBox.Items.Add('Item 2')
[void] $listBox.Items.Add('Item 3')
[void] $listBox.Items.Add('Item 4')
[void] $listBox.Items.Add('Item 5')
```

<span data-ttu-id="f81e4-131">Zadejte maximální výšku ovládacího prvku seznam pole.</span><span class="sxs-lookup"><span data-stu-id="f81e4-131">Specify the maximum height of the list box control.</span></span>

```powershell
$listBox.Height = 70
```

<span data-ttu-id="f81e4-132">Přidejte do svého formuláře ovládací prvek seznamu a dáte pokyn, aby Windows otevřete formulář imitovaná další windows a dialogových oknech při otevření.</span><span class="sxs-lookup"><span data-stu-id="f81e4-132">Add the list box control to your form, and instruct Windows to open the form atop other windows and dialog boxes when it’s opened.</span></span>

```powershell
$form.Controls.Add($listBox)
$form.Topmost = $true
```

<span data-ttu-id="f81e4-133">Přidejte následující řádek kódu k zobrazení formuláře ve Windows.</span><span class="sxs-lookup"><span data-stu-id="f81e4-133">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="f81e4-134">Nakonec se kód uvnitř **Pokud** bloku instruuje Windows, co dělat s formuláři uživatele ze seznamu vyberte jednu nebo více možností a pak klikněte na tlačítko **OK** tlačítko nebo stisknutím klávesy **Enter**  klíč.</span><span class="sxs-lookup"><span data-stu-id="f81e4-134">Finally, the code inside the **If** block instructs Windows what to do with the form after users select one or more options from the list box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $listBox.SelectedItems
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="f81e4-135">Viz také</span><span class="sxs-lookup"><span data-stu-id="f81e4-135">See Also</span></span>

- [<span data-ttu-id="f81e4-136">Hey Scripting Guy: Proč nefungují tyto příklady prostředí PowerShell grafického uživatelského rozhraní?</span><span class="sxs-lookup"><span data-stu-id="f81e4-136">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="f81e4-137">Githubu: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="f81e4-137">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="f81e4-138">Windows PowerShell tipu týdne přišel: vícenásobný výběr v seznamu polí – a další!</span><span class="sxs-lookup"><span data-stu-id="f81e4-138">Windows PowerShell Tip of the Week:  Multi-Select List Boxes - And More!</span></span>](https://technet.microsoft.com/library/ff730950.aspx)
---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření vlastního vstupního pole
ms.assetid: 0b12e56c-299f-40ee-afbf-d30d23ed2565
ms.openlocfilehash: 2d04ad6df65cdb4ff13d136dea47bbba6a01f3a2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403643"
---
# <a name="creating-a-custom-input-box"></a><span data-ttu-id="eb25e-103">Vytvoření vlastního vstupního pole</span><span class="sxs-lookup"><span data-stu-id="eb25e-103">Creating a Custom Input Box</span></span>

<span data-ttu-id="eb25e-104">Skript grafické vlastního vstupního pole pomocí funkce vytváření formulářů rozhraní Microsoft .NET Framework ve Windows Powershellu 3.0 a novějších verzí.</span><span class="sxs-lookup"><span data-stu-id="eb25e-104">Script a graphical custom input box by using Microsoft .NET Framework form-building features in Windows PowerShell 3.0 and later releases.</span></span>

## <a name="create-a-custom-graphical-input-box"></a><span data-ttu-id="eb25e-105">Vytvořit vlastní grafické vstupního pole</span><span class="sxs-lookup"><span data-stu-id="eb25e-105">Create a custom, graphical input box</span></span>

<span data-ttu-id="eb25e-106">Zkopírujte a vložte následující do Windows PowerShell ISE a pak ho uložte jako skript Windows Powershellu (.ps1).</span><span class="sxs-lookup"><span data-stu-id="eb25e-106">Copy and then paste the following into Windows PowerShell ISE, and then save it as a Windows PowerShell script (.ps1).</span></span>

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

<span data-ttu-id="eb25e-107">Skript se začne načtením dvou tříd rozhraní .NET Framework: **System.Drawing** a **System.Windows.Forms**.</span><span class="sxs-lookup"><span data-stu-id="eb25e-107">The script begins by loading two .NET Framework classes: **System.Drawing** and **System.Windows.Forms**.</span></span> <span data-ttu-id="eb25e-108">Spusťte novou instanci třídy rozhraní .NET Framework **formuláře System.Windows.Forms.Form**; který obsahuje prázdný formulář nebo ovládací prvky okna, do kterého můžete začít přidávat.</span><span class="sxs-lookup"><span data-stu-id="eb25e-108">You then start a new instance of the .NET Framework class **System.Windows.Forms.Form**; that provides a blank form or window to which you can start adding controls.</span></span>

```powershell
$form = New-Object System.Windows.Forms.Form
```

<span data-ttu-id="eb25e-109">Po vytvoření instance třídy formuláře přiřadíte hodnoty třem vlastnostem této třídy.</span><span class="sxs-lookup"><span data-stu-id="eb25e-109">After you create an instance of the Form class, assign values to three properties of this class.</span></span>

- <span data-ttu-id="eb25e-110">**Text.**</span><span class="sxs-lookup"><span data-stu-id="eb25e-110">**Text.**</span></span> <span data-ttu-id="eb25e-111">Tím se změní záhlaví okna.</span><span class="sxs-lookup"><span data-stu-id="eb25e-111">This becomes the title of the window.</span></span>

- <span data-ttu-id="eb25e-112">**Velikost.**</span><span class="sxs-lookup"><span data-stu-id="eb25e-112">**Size.**</span></span> <span data-ttu-id="eb25e-113">Toto je velikost formuláře v pixelech.</span><span class="sxs-lookup"><span data-stu-id="eb25e-113">This is the size of the form, in pixels.</span></span> <span data-ttu-id="eb25e-114">Předchozí skript vytvoří formulář, který je 300 pixelů na šířku a 200 pixelů na výšku.</span><span class="sxs-lookup"><span data-stu-id="eb25e-114">The preceding script creates a form that’s 300 pixels wide by 200 pixels tall.</span></span>

- <span data-ttu-id="eb25e-115">**Počáteční pozice.**</span><span class="sxs-lookup"><span data-stu-id="eb25e-115">**StartingPosition.**</span></span> <span data-ttu-id="eb25e-116">Tato volitelná vlastnost nastavena na **CenterScreen** v předchozím skriptu.</span><span class="sxs-lookup"><span data-stu-id="eb25e-116">This optional property is set to **CenterScreen** in the preceding script.</span></span> <span data-ttu-id="eb25e-117">Pokud tuto vlastnost nepřidáte, vybere Windows umístění při otevření formuláře.</span><span class="sxs-lookup"><span data-stu-id="eb25e-117">If you don’t add this property, Windows selects a location when the form is opened.</span></span> <span data-ttu-id="eb25e-118">Tím, že nastavíte **počáteční pozice** k **CenterScreen**, automaticky zobrazená formuláři uprostřed obrazovky pokaždé, když ho načte.</span><span class="sxs-lookup"><span data-stu-id="eb25e-118">By setting the **StartingPosition** to **CenterScreen**, you’re automatically displaying the form in the middle of the screen each time it loads.</span></span>

```powershell
$form.Text = 'Data Entry Form'
$form.Size = New-Object System.Drawing.Size(300,200)
$form.StartPosition = 'CenterScreen'
```

<span data-ttu-id="eb25e-119">Dále vytvořte **OK** tlačítko pro daný formulář.</span><span class="sxs-lookup"><span data-stu-id="eb25e-119">Next, create an **OK** button for your form.</span></span> <span data-ttu-id="eb25e-120">Zadejte velikost a chování **OK** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="eb25e-120">Specify the size and behavior of the **OK** button.</span></span> <span data-ttu-id="eb25e-121">V tomto příkladu je pozice tlačítko 120 pixelů od horního okraje formuláře a 75 pixelů od levého okraje.</span><span class="sxs-lookup"><span data-stu-id="eb25e-121">In this example, the button position is 120 pixels from the form’s top edge, and 75 pixels from the left edge.</span></span> <span data-ttu-id="eb25e-122">Výška tlačítka je 23 pixelů, zatímco tlačítko délka je 75 pixelů.</span><span class="sxs-lookup"><span data-stu-id="eb25e-122">The button height is 23 pixels, while the button length is 75 pixels.</span></span> <span data-ttu-id="eb25e-123">Tento skript využívá k určení chování tlačítka předdefinovaných typů formulářů Windows.</span><span class="sxs-lookup"><span data-stu-id="eb25e-123">The script uses predefined Windows Forms types to determine the button behaviors.</span></span>

```powershell
$OKButton = New-Object System.Windows.Forms.Button
$OKButton.Location = New-Object System.Drawing.Point(75,120)
$OKButton.Size = New-Object System.Drawing.Size(75,23)
$OKButton.Text = 'OK'
$OKButton.DialogResult = [System.Windows.Forms.DialogResult]::OK
$form.AcceptButton = $OKButton
$form.Controls.Add($OKButton)
```

<span data-ttu-id="eb25e-124">Podobně můžete vytvořit **zrušit** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="eb25e-124">Similarly, you create a **Cancel** button.</span></span> <span data-ttu-id="eb25e-125">**Zrušit** tlačítko je 120 pixelů od horního, ale 150 pixelů od levého okraje okna.</span><span class="sxs-lookup"><span data-stu-id="eb25e-125">The **Cancel** button is 120 pixels from the top, but 150 pixels from the left edge of the window.</span></span>

```powershell
$CancelButton = New-Object System.Windows.Forms.Button
$CancelButton.Location = New-Object System.Drawing.Point(150,120)
$CancelButton.Size = New-Object System.Drawing.Size(75,23)
$CancelButton.Text = 'Cancel'
$CancelButton.DialogResult = [System.Windows.Forms.DialogResult]::Cancel
$form.CancelButton = $CancelButton
$form.Controls.Add($CancelButton)
```

<span data-ttu-id="eb25e-126">Pak zadejte popisek v okně, který popisuje informace, na kterých chcete, aby uživatelé zadali.</span><span class="sxs-lookup"><span data-stu-id="eb25e-126">Next, provide label text on your window that describes the information you want users to provide.</span></span>

```powershell
$label = New-Object System.Windows.Forms.Label
$label.Location = New-Object System.Drawing.Point(10,20)
$label.Size = New-Object System.Drawing.Size(280,20)
$label.Text = 'Please enter the information in the space below:'
$form.Controls.Add($label)
```

<span data-ttu-id="eb25e-127">Přidejte ovládací prvek (v tomto případě textové pole), která umožňuje uživatelům poskytnout informace, které jste je popsáno v textu popisku.</span><span class="sxs-lookup"><span data-stu-id="eb25e-127">Add the control (in this case, a text box) that lets users provide the information you’ve described in your label text.</span></span> <span data-ttu-id="eb25e-128">Existuje mnoho dalších ovládacích prvků, platí kromě textová pole; pro větší počet kontrolních mechanismů, naleznete v tématu [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) na webové stránce MSDN.</span><span class="sxs-lookup"><span data-stu-id="eb25e-128">There are many other controls you can apply besides text boxes; for more controls, see [System.Windows.Forms Namespace](https://msdn.microsoft.com/library/k50ex0x9(v=vs.110).aspx) on MSDN.</span></span>

```powershell
$textBox = New-Object System.Windows.Forms.TextBox
$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(260,20)
$form.Controls.Add($textBox)
```

<span data-ttu-id="eb25e-129">Nastavte **nejvíce nahoře** vlastnost **$true** přinutit okně pro otevření imitovaná otevřená okna a dialogová okna.</span><span class="sxs-lookup"><span data-stu-id="eb25e-129">Set the **Topmost** property to **$true** to force the window to open atop other open windows and dialog boxes.</span></span>

```powershell
$form.Topmost = $true
```

<span data-ttu-id="eb25e-130">V dalším kroku přidejte následující řádek kódu k aktivaci formuláře a nastaví fokus do textového pole, který jste vytvořili.</span><span class="sxs-lookup"><span data-stu-id="eb25e-130">Next, add this line of code to activate the form, and set the focus to the text box that you created.</span></span>

```powershell
$form.Add_Shown({$textBox.Select()})
```

<span data-ttu-id="eb25e-131">Přidejte následující řádek kódu k zobrazení formuláře ve Windows.</span><span class="sxs-lookup"><span data-stu-id="eb25e-131">Add the following line of code to display the form in Windows.</span></span>

```powershell
$result = $form.ShowDialog()
```

<span data-ttu-id="eb25e-132">Nakonec se kód uvnitř **Pokud** bloku instruuje Windows, co dělat s formulářem, poté, co uživatelé zadejte text do textového pole a potom klikněte na tlačítko **OK** tlačítko nebo stisknutím klávesy **Enter** klíč.</span><span class="sxs-lookup"><span data-stu-id="eb25e-132">Finally, the code inside the **If** block instructs Windows what to do with the form after users provide text in the text box, and then click the **OK** button or press the **Enter** key.</span></span>

```powershell
if ($result -eq [System.Windows.Forms.DialogResult]::OK)
{
    $x = $textBox.Text
    $x
}
```

## <a name="see-also"></a><span data-ttu-id="eb25e-133">Viz také</span><span class="sxs-lookup"><span data-stu-id="eb25e-133">See Also</span></span>

- [<span data-ttu-id="eb25e-134">Dobrý den Scripting Guy:  Proč tyto příklady prostředí PowerShell grafickým uživatelským rozhraním nefungují?</span><span class="sxs-lookup"><span data-stu-id="eb25e-134">Hey Scripting Guy:  Why don’t these PowerShell GUI examples work?</span></span>](https://go.microsoft.com/fwlink/?LinkId=506644)
- [<span data-ttu-id="eb25e-135">GitHub: Dave Wyatt WinFormsExampleUpdates</span><span class="sxs-lookup"><span data-stu-id="eb25e-135">GitHub: Dave Wyatt's WinFormsExampleUpdates</span></span>](https://github.com/dlwyatt/WinFormsExampleUpdates)
- [<span data-ttu-id="eb25e-136">Windows PowerShell tipu týdne přišel:  Vytvoření vlastního vstupního pole</span><span class="sxs-lookup"><span data-stu-id="eb25e-136">Windows PowerShell Tip of the Week:  Creating a Custom Input Box</span></span>](https://technet.microsoft.com/library/ff730941.aspx)
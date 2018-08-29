---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Získání podrobné nápovědy
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 88f0357b935a7c75df07d667e3f2f2d0e493f89d
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134030"
---
# <a name="getting-detailed-help-information"></a><span data-ttu-id="c87ed-103">Získání podrobné nápovědy</span><span class="sxs-lookup"><span data-stu-id="c87ed-103">Getting detailed help information</span></span>

<span data-ttu-id="c87ed-104">PowerShell zahrnuje podrobné články nápovědy, které vysvětluje koncepty prostředí PowerShell a jazyku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c87ed-104">PowerShell includes detailed Help articles that explain PowerShell concepts and the PowerShell language.</span></span> <span data-ttu-id="c87ed-105">Existují také články nápovědy pro jednotlivé rutiny a zprostředkovatele a pro mnoho funkcí a skriptů.</span><span class="sxs-lookup"><span data-stu-id="c87ed-105">There are also Help articles for each cmdlet and provider and for many functions and scripts.</span></span>

<span data-ttu-id="c87ed-106">Tyto články nápovědy může zobrazit na příkazovém řádku nebo zobrazení naposledy aktualizované verze v těchto článcích [Powershellu](/powershell/scripting/powershell-scripting) online dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="c87ed-106">You can display these Help articles at the command prompt or view the most recently updated versions of these articles in the [PowerShell](/powershell/scripting/powershell-scripting) documentation online.</span></span>

## <a name="getting-help-for-cmdlets"></a><span data-ttu-id="c87ed-107">Získání nápovědy pro rutiny</span><span class="sxs-lookup"><span data-stu-id="c87ed-107">Getting help for cmdlets</span></span>

<span data-ttu-id="c87ed-108">Chcete-li získat nápovědu o rutinách prostředí PowerShell, použijte [Get-Help](/powershell/module/microsoft.powershell.core/Get-Help) rutiny.</span><span class="sxs-lookup"><span data-stu-id="c87ed-108">To get Help about PowerShell cmdlets, use the [Get-Help](/powershell/module/microsoft.powershell.core/Get-Help) cmdlet.</span></span> <span data-ttu-id="c87ed-109">Například, chcete-li získat nápovědu pro `Get-ChildItem` rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="c87ed-109">For example, to get Help for the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem
```

<span data-ttu-id="c87ed-110">nebo</span><span class="sxs-lookup"><span data-stu-id="c87ed-110">or</span></span>

```powershell
Get-ChildItem -?
```

<span data-ttu-id="c87ed-111">Nápovědu získáte i o rutinu Get-Help.</span><span class="sxs-lookup"><span data-stu-id="c87ed-111">You can even get Help about the Get-Help cmdlet.</span></span> <span data-ttu-id="c87ed-112">Příklad:</span><span class="sxs-lookup"><span data-stu-id="c87ed-112">For example:</span></span>

```powershell
Get-Help Get-Help
```

<span data-ttu-id="c87ed-113">Pokud chcete získat seznam všech rutin články nápovědy v relaci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="c87ed-113">To get a list of all the cmdlet Help articles in your session, type:</span></span>

```powershell
Get-Help -Category Cmdlet
```

<span data-ttu-id="c87ed-114">Chcete-li zobrazit jednu stránku každého článku nápovědy v čase, použijte `help` funkci nebo její alias `man`.</span><span class="sxs-lookup"><span data-stu-id="c87ed-114">To display one page of each Help article at a time, use the `help` function or its alias `man`.</span></span>
<span data-ttu-id="c87ed-115">Například chcete-li zobrazit nápovědu pro `Get-ChildItem` rutiny, typ</span><span class="sxs-lookup"><span data-stu-id="c87ed-115">For example, to display Help for the `Get-ChildItem` cmdlet, type</span></span>

```powershell
man Get-ChildItem
```

<span data-ttu-id="c87ed-116">nebo</span><span class="sxs-lookup"><span data-stu-id="c87ed-116">or</span></span>

```powershell
help Get-ChildItem
```

<span data-ttu-id="c87ed-117">Chcete-li zobrazit podrobné informace, použijte **podrobné** parametr `Get-Help` rutiny.</span><span class="sxs-lookup"><span data-stu-id="c87ed-117">To display detailed information, use the **Detailed** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="c87ed-118">Například, chcete-li získat podrobné informace `Get-ChildItem` rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="c87ed-118">For example, to get detailed information about the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Detailed
```

<span data-ttu-id="c87ed-119">Chcete-li zobrazit veškerý obsah v článku nápovědy, použijte **úplné** parametr `Get-Help` rutiny.</span><span class="sxs-lookup"><span data-stu-id="c87ed-119">To display all content in the Help article, use the **Full** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="c87ed-120">Například, chcete-li zobrazit veškerý obsah v článku nápovědy `Get-ChildItem` rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="c87ed-120">For example, to display all content in the Help article for the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Full
```

<span data-ttu-id="c87ed-121">Chcete-li získat podrobnou nápovědu k parametry rutiny, použijte **parametr** parametr `Get-Help` rutiny.</span><span class="sxs-lookup"><span data-stu-id="c87ed-121">To get detailed Help about the parameters of a cmdlet, use the **Parameter** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="c87ed-122">Například, chcete-li získat podrobnou nápovědu pro všechny parametry `Get-ChildItem` rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="c87ed-122">For example, to get detailed Help for all of the parameters of the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Parameter *
```

<span data-ttu-id="c87ed-123">Chcete-li zobrazit pouze v příkladech v článku nápovědy, použijte **příklady** parametr `Get-Help`.</span><span class="sxs-lookup"><span data-stu-id="c87ed-123">To display only the examples in a Help article, use the **Examples** parameter of the `Get-Help`.</span></span>
<span data-ttu-id="c87ed-124">Chcete-li například zobrazit pouze v příkladech v tomto článku nápovědy pro `Get-ChildItem `rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="c87ed-124">For example, to display only the examples in the Help article for the `Get-ChildItem `cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Examples
```

<span data-ttu-id="c87ed-125">Informace o tom, jak psát články nápovědy pro rutiny, které píšete, naleznete v tématu [jak napsat nápovědě k rutině](/powershell/developer/help/writing-help-for-windows-powershell-cmdlets).</span><span class="sxs-lookup"><span data-stu-id="c87ed-125">For information about how to write Help articles for the cmdlets that you write, see [How to Write Cmdlet Help](/powershell/developer/help/writing-help-for-windows-powershell-cmdlets).</span></span>

## <a name="getting-conceptual-help"></a><span data-ttu-id="c87ed-126">Koncepční nápovědy</span><span class="sxs-lookup"><span data-stu-id="c87ed-126">Getting conceptual help</span></span>

<span data-ttu-id="c87ed-127">`Get-Help` Rutina taky zobrazí informace o koncepčních článků v prostředí PowerShell, včetně články o jazyce Powershellu.</span><span class="sxs-lookup"><span data-stu-id="c87ed-127">The `Get-Help` cmdlet also displays information about conceptual articles in PowerShell, including articles about the PowerShell language.</span></span> <span data-ttu-id="c87ed-128">Koncepční články začínají předponou "about_", například about_line_editing nápovědy.</span><span class="sxs-lookup"><span data-stu-id="c87ed-128">Conceptual Help articles begin with the "about_" prefix, such as about_line_editing.</span></span> <span data-ttu-id="c87ed-129">(Název konceptuální článek musí být zadaná v angličtině i na jiných než anglických verzí Powershellu.)</span><span class="sxs-lookup"><span data-stu-id="c87ed-129">(The name of the conceptual article must be entered in English even on non-English versions of PowerShell.)</span></span>

<span data-ttu-id="c87ed-130">Pokud chcete zobrazit seznam koncepčních článků, zadejte:</span><span class="sxs-lookup"><span data-stu-id="c87ed-130">To display a list of conceptual articles, type:</span></span>

```powershell
Get-Help about_*
```

<span data-ttu-id="c87ed-131">Pokud chcete zobrazit konkrétní článek nápovědy, zadejte název článku, například:</span><span class="sxs-lookup"><span data-stu-id="c87ed-131">To display a particular Help article, type the article name, for example:</span></span>

```powershell
Get-Help about_command_syntax
```

<span data-ttu-id="c87ed-132">Parametry `Get-Help`, jako například **podrobné**, **parametr**, a **příklady**, nemají žádný vliv na displeji koncepční články nápovědy.</span><span class="sxs-lookup"><span data-stu-id="c87ed-132">The parameters of `Get-Help`, such as **Detailed**, **Parameter**, and **Examples**, have no effect on the display of conceptual Help articles.</span></span>

## <a name="getting-help-about-providers"></a><span data-ttu-id="c87ed-133">Získání nápovědy o zprostředkovatelích</span><span class="sxs-lookup"><span data-stu-id="c87ed-133">Getting help about providers</span></span>

<span data-ttu-id="c87ed-134">`Get-Help` Rutina zobrazí informace o poskytovatelích prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c87ed-134">The `Get-Help` cmdlet displays information about PowerShell providers.</span></span> <span data-ttu-id="c87ed-135">Chcete-li získat nápovědu pro zprostředkovatele, zadejte `Get-Help` za nímž následuje název zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="c87ed-135">To get Help for a provider, type `Get-Help` followed by the provider name.</span></span> <span data-ttu-id="c87ed-136">Chcete-li získat nápovědu pro zprostředkovatele registru, zadejte například:</span><span class="sxs-lookup"><span data-stu-id="c87ed-136">For example, to get Help for the Registry provider, type:</span></span>

```powershell
Get-Help registry
```

<span data-ttu-id="c87ed-137">Chcete-li získat seznam všech poskytovatele články nápovědy v relaci, zadejte</span><span class="sxs-lookup"><span data-stu-id="c87ed-137">To get a list of all the provider Help articles in your session, type</span></span>

```powershell
Get-Help -Category provider
```

<span data-ttu-id="c87ed-138">Parametry `Get-Help`, jako například **podrobné**, **parametr**, a **příklady**, nemají žádný vliv na displeji články nápovědy zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="c87ed-138">The parameters of `Get-Help`, such as **Detailed**, **Parameter**, and **Examples**, have no effect on the display of provider Help articles.</span></span>

## <a name="getting-help-about-scripts-and-functions"></a><span data-ttu-id="c87ed-139">Získání nápovědy o skriptech a funkcích</span><span class="sxs-lookup"><span data-stu-id="c87ed-139">Getting help about scripts and functions</span></span>

<span data-ttu-id="c87ed-140">Mnoho funkcí v prostředí PowerShell a skripty mají články nápovědy.</span><span class="sxs-lookup"><span data-stu-id="c87ed-140">Many scripts and functions in PowerShell have Help articles.</span></span> <span data-ttu-id="c87ed-141">Použití `Get-Help` rutiny článků nápovědy, skriptech a funkcích.</span><span class="sxs-lookup"><span data-stu-id="c87ed-141">Use the `Get-Help` cmdlet to display the Help articles for scripts and functions.</span></span>

<span data-ttu-id="c87ed-142">Chcete-li zobrazit nápovědu pro funkci, zadejte `Get-Help` následovaný názvem funkce.</span><span class="sxs-lookup"><span data-stu-id="c87ed-142">To display the Help for a function, type `Get-Help` followed by the function name.</span></span> <span data-ttu-id="c87ed-143">Například, chcete-li získat nápovědu pro `Disable-PSRemoting` funkci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="c87ed-143">For example, to get Help for the `Disable-PSRemoting` function, type:</span></span>

```powershell
Get-Help Disable-PSRemoting
```

<span data-ttu-id="c87ed-144">Chcete-li zobrazit nápovědu pro skript, zadejte cestu k souboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="c87ed-144">To display the Help for a script, type the path to the script file.</span></span> <span data-ttu-id="c87ed-145">Pokud skript není v cestě uvedené v proměnné prostředí Path, musíte použít plně kvalifikovanou cestu.</span><span class="sxs-lookup"><span data-stu-id="c87ed-145">If the script is not in a path listed in the Path environment variable, you must use the fully qualified path.</span></span>

<span data-ttu-id="c87ed-146">Například, pokud máte skript volá "TestScript.ps1" c:\\PS testovací adresář, chcete-li zobrazit článek nápovědy pro skript, typ:</span><span class="sxs-lookup"><span data-stu-id="c87ed-146">For example, if you have a script called "TestScript.ps1" in your C:\\PS-Test directory, to display the Help article for the script, type:</span></span>

```powershell
Get-Help c:\ps-test\TestScript.ps1
```

<span data-ttu-id="c87ed-147">Parametry, které jsou navržené k zobrazování pracovní nápovědy rutiny pro skript a funkce pomáhají příliš.</span><span class="sxs-lookup"><span data-stu-id="c87ed-147">The parameters that are designed for displaying cmdlet Help work for script and function Help, too.</span></span> <span data-ttu-id="c87ed-148">Však není nápovědy pro funkce a skripty zobrazený při spuštění `Get-Help *`.</span><span class="sxs-lookup"><span data-stu-id="c87ed-148">However, help for functions and scripts is not shown when you run `Get-Help *`.</span></span>

<span data-ttu-id="c87ed-149">Informace o psaní článků nápovědy, funkcí a skriptů najdete v následujících článcích:</span><span class="sxs-lookup"><span data-stu-id="c87ed-149">For information about writing Help articles for your functions and scripts, see the following articles:</span></span>

- [<span data-ttu-id="c87ed-150">about_Functions</span><span class="sxs-lookup"><span data-stu-id="c87ed-150">about_Functions</span></span>](/powershell/module/microsoft.powershell.core/about/about_functions)
- [<span data-ttu-id="c87ed-151">about_Scripts</span><span class="sxs-lookup"><span data-stu-id="c87ed-151">about_Scripts</span></span>](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [<span data-ttu-id="c87ed-152">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="c87ed-152">about_Comment_Based_Help</span></span>](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)

## <a name="getting-help-online"></a><span data-ttu-id="c87ed-153">Získat online nápovědu</span><span class="sxs-lookup"><span data-stu-id="c87ed-153">Getting help online</span></span>

<span data-ttu-id="c87ed-154">Zobrazení online článků nápovědy, který je jedním z nejlepších způsobů, jak získat pomoc.</span><span class="sxs-lookup"><span data-stu-id="c87ed-154">Viewing the Help articles online is one of the best ways to get help.</span></span> <span data-ttu-id="c87ed-155">Online články jsou snáze aktualizovat a poskytovat nejaktuálnější obsah.</span><span class="sxs-lookup"><span data-stu-id="c87ed-155">Online articles are easier to update and provide the most current content.</span></span>

<span data-ttu-id="c87ed-156">Chcete-li získat nápovědu online, použijte **Online** parametr `Get-Help` rutiny.</span><span class="sxs-lookup"><span data-stu-id="c87ed-156">To get Help online, use the **Online** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="c87ed-157">Všech článků nápovědy, které jsou součástí prostředí PowerShell, včetně zprostředkovatele nápovědy a koncepční (články nápovědy o) jsou k dispozici online v [Powershellu](/powershell/scripting/powershell-scripting) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="c87ed-157">All the Help articles that come with PowerShell, including provider Help and conceptual (About) Help articles, are available online in the [PowerShell](/powershell/scripting/powershell-scripting) documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="c87ed-158">Nelze použít **Online** parametr s koncepční (about_ \*) nebo zprostředkovatele články nápovědy.</span><span class="sxs-lookup"><span data-stu-id="c87ed-158">You can't use the **Online** parameter with conceptual (about_\*) or provider Help articles.</span></span>
> <span data-ttu-id="c87ed-159">Online nápovědy je volitelné, takže nefunguje pro všechny rutiny, funkce nebo skriptu.</span><span class="sxs-lookup"><span data-stu-id="c87ed-159">Online help is optional, so it does not work for every cmdlet, function, or script.</span></span>

<span data-ttu-id="c87ed-160">Například, chcete-li získat online verzi nápovědy článku `Get-ChildItem` rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="c87ed-160">For example, to get the online version of the Help article about the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Online
```

<span data-ttu-id="c87ed-161">Prostředí PowerShell otevře článek ve vašem výchozím prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="c87ed-161">PowerShell opens the article in your default browser.</span></span> <span data-ttu-id="c87ed-162">Pokud se podporuje online nápovědy pro článek nápovědy, můžete také zobrazit adresu URL článek nápovědy.</span><span class="sxs-lookup"><span data-stu-id="c87ed-162">If online Help is supported for a Help article, you can also view the URL of the Help article.</span></span> <span data-ttu-id="c87ed-163">Adresa URL se zobrazí v části související odkazy na článek nápovědy.</span><span class="sxs-lookup"><span data-stu-id="c87ed-163">The URL appears in the Related Links section of a Help article.</span></span>

<span data-ttu-id="c87ed-164">Pokud chcete zobrazit adresu URL pro online verzi rutinu Add-Computer, zadejte například:</span><span class="sxs-lookup"><span data-stu-id="c87ed-164">For example, to see the URL for the online version of the Add-Computer cmdlet, type:</span></span>

```powershell
Get-Help Add-Computer
```

<span data-ttu-id="c87ed-165">První řádek v souvisejících odkazů části tohoto článku je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="c87ed-165">The first line in the Related Links section of the article is shown below.</span></span>

```Output
Online version: http://go.microsoft.com/fwlink/?LinkId=821564
```

<span data-ttu-id="c87ed-166">Informace o tom, jak poskytovat online podporu pro vaše články nápovědy najdete v tématu [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span><span class="sxs-lookup"><span data-stu-id="c87ed-166">For information about how to provide online support for your Help articles, see [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span></span>

## <a name="see-also"></a><span data-ttu-id="c87ed-167">Viz taky</span><span class="sxs-lookup"><span data-stu-id="c87ed-167">See also</span></span>

- [<span data-ttu-id="c87ed-168">about_Functions</span><span class="sxs-lookup"><span data-stu-id="c87ed-168">about_Functions</span></span>](/powershell/module/microsoft.powershell.core/about/about_functions)
- [<span data-ttu-id="c87ed-169">about_Scripts</span><span class="sxs-lookup"><span data-stu-id="c87ed-169">about_Scripts</span></span>](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [<span data-ttu-id="c87ed-170">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="c87ed-170">about_Comment_Based_Help</span></span>](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)
- [<span data-ttu-id="c87ed-171">Get-Help</span><span class="sxs-lookup"><span data-stu-id="c87ed-171">Get-Help</span></span>](/powershell/module/microsoft.powershell.core/get-help)

---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Získání podrobné nápovědy
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 29c24af3f688f9388893044952442910e793842d
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/25/2018
---
# <a name="getting-detailed-help-information"></a><span data-ttu-id="8c61b-103">Získání podrobné nápovědy</span><span class="sxs-lookup"><span data-stu-id="8c61b-103">Getting Detailed Help Information</span></span>
<span data-ttu-id="8c61b-104">Prostředí Windows PowerShell obsahuje podrobné témata nápovědy, které vysvětlují koncepty prostředí Windows PowerShell a jazyk prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c61b-104">Windows PowerShell includes detailed Help topics that explain Windows PowerShell concepts and the Windows PowerShell language.</span></span> <span data-ttu-id="8c61b-105">Existují také témata nápovědy pro každou rutiny a zprostředkovatele a témata nápovědy pro mnoho funkcí a skriptů.</span><span class="sxs-lookup"><span data-stu-id="8c61b-105">There are also Help topics for each cmdlet and provider and Help topics for many functions and scripts.</span></span>

<span data-ttu-id="8c61b-106">Můžete zobrazit tato témata nápovědy na příkazovém řádku nebo zobrazit nedávno aktualizované verze těchto témat v Microsoft TechNet Library.</span><span class="sxs-lookup"><span data-stu-id="8c61b-106">You can display these Help topics at the command prompt or view the most recently updated versions of these topics in the Microsoft TechNet Library.</span></span> <span data-ttu-id="8c61b-107">Mnoho programy, které hostí prostředí Windows PowerShell, jako je Windows Integrované skriptovací prostředí PowerShell, zadejte další pomoc funkce, jako je kontextová nápověda a zkompilovaný soubor nápovědy (CHM.).</span><span class="sxs-lookup"><span data-stu-id="8c61b-107">Many programs that host Windows PowerShell, such as Windows PowerShell Integrated Scripting Environment, provide additional Help features, such as context-sensitive Help and compiled Help file (.chm).</span></span>

## <a name="getting-help-for-cmdlets"></a><span data-ttu-id="8c61b-108">Získání nápovědy k rutinám</span><span class="sxs-lookup"><span data-stu-id="8c61b-108">Getting Help for Cmdlets</span></span>
<span data-ttu-id="8c61b-109">Chcete-li získat nápovědu o rutinách prostředí Windows PowerShell, použijte [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) rutiny.</span><span class="sxs-lookup"><span data-stu-id="8c61b-109">To get Help about Windows PowerShell cmdlets, use the [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) cmdlet.</span></span> <span data-ttu-id="8c61b-110">Například pro získání nápovědy pro [Get-ChildItem [m2]](https://technet.microsoft.com/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) rutiny, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-110">For example, to get Help for the [Get-ChildItem [m2]](https://technet.microsoft.com/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) cmdlet, type:</span></span>

```
get-help get-childitem
```

<span data-ttu-id="8c61b-111">nebo</span><span class="sxs-lookup"><span data-stu-id="8c61b-111">or</span></span>

```
get-childitem -?
```

<span data-ttu-id="8c61b-112">Dokonce můžete získat nápovědu o rutinu Get-Help.</span><span class="sxs-lookup"><span data-stu-id="8c61b-112">You can even get Help about the Get-Help cmdlet.</span></span> <span data-ttu-id="8c61b-113">Příklad:</span><span class="sxs-lookup"><span data-stu-id="8c61b-113">For example:</span></span>

```
get-help get-help
```

<span data-ttu-id="8c61b-114">Pokud chcete získat seznam všech témat nápovědy rutinu v relaci, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-114">To get a list of all the cmdlet Help topics in your session, type:</span></span>

```
get-help -category cmdlet
```

<span data-ttu-id="8c61b-115">Chcete-li zobrazit jednu stránku každého tématu nápovědy v čase, použijte **pomoci** funkce nebo jeho alias **man**.</span><span class="sxs-lookup"><span data-stu-id="8c61b-115">To display one page of each Help topic at a time, use the **help** function or its alias **man**.</span></span> <span data-ttu-id="8c61b-116">Například pokud chcete zobrazit nápovědu pro rutinu Get-ChildItem, zadejte</span><span class="sxs-lookup"><span data-stu-id="8c61b-116">For example, to display Help for the Get-ChildItem cmdlet, type</span></span>

```
man get-childitem
```

<span data-ttu-id="8c61b-117">nebo</span><span class="sxs-lookup"><span data-stu-id="8c61b-117">or</span></span>

```
help get-childitem
```

<span data-ttu-id="8c61b-118">Chcete-li zobrazit podrobné informace o rutiny, funkce nebo skriptu, včetně popisu jeho parametry a příkladů jeho použití, použijte *podrobné* parametru rutiny Get-Help.</span><span class="sxs-lookup"><span data-stu-id="8c61b-118">To display detailed information about a cmdlet, function, or script, including descriptions of its parameters and examples of its use, use the *Detailed* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="8c61b-119">Chcete-li získat podrobné informace o rutině Get-ChildItem, zadejte například:</span><span class="sxs-lookup"><span data-stu-id="8c61b-119">For example, to get detailed information about the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -detailed
```

<span data-ttu-id="8c61b-120">Chcete-li zobrazit veškerý obsah v tématu nápovědy, použijte *úplné* parametru rutiny Get-Help.</span><span class="sxs-lookup"><span data-stu-id="8c61b-120">To display all content in the Help topic, use the *Full* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="8c61b-121">Například pokud chcete zobrazit veškerý obsah v tématu nápovědy pro rutinu Get-ChildItem, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-121">For example, to display all content in the Help topic for the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -full
```

<span data-ttu-id="8c61b-122">Chcete-li získat podrobnou nápovědu k parametry rutiny, použijte *parametr* parametru rutiny Get-Help.</span><span class="sxs-lookup"><span data-stu-id="8c61b-122">To get detailed Help about the parameters of a cmdlet, use the *Parameter* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="8c61b-123">Například získat podrobné nápovědy pro všechny parametry rutiny Get-ChildItem, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-123">For example, to get detailed Help for all of the parameters of the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -parameter *
```

<span data-ttu-id="8c61b-124">Chcete-li zobrazit pouze v příkladech v tématu nápovědy, použijte *příklad* parametr Get-Help.</span><span class="sxs-lookup"><span data-stu-id="8c61b-124">To display only the examples in a Help topic, use the *Example* parameter of the Get-Help.</span></span> <span data-ttu-id="8c61b-125">Například pokud chcete zobrazit jenom příklady v tématu nápovědy pro rutinu Get-ChildItem, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-125">For example, to display only the examples in the Help topic for the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -examples
```

<span data-ttu-id="8c61b-126">Informace o tom, jak psát témata nápovědy k rutinám, které můžete psát najdete v tématu [postup nápovědě k rutině zápisu](https://go.microsoft.com/fwlink/?LinkID=123415) v knihovně MSDN.</span><span class="sxs-lookup"><span data-stu-id="8c61b-126">For information about how to write Help topics for the cmdlets that you write, see [How to Write Cmdlet Help](https://go.microsoft.com/fwlink/?LinkID=123415) in the MSDN library.</span></span>

## <a name="getting-conceptual-help"></a><span data-ttu-id="8c61b-127">Koncepční nápovědy</span><span class="sxs-lookup"><span data-stu-id="8c61b-127">Getting Conceptual Help</span></span>
<span data-ttu-id="8c61b-128">Rutinu Get-Help také zobrazí informace o koncepční témata v prostředí Windows PowerShell, včetně témata týkající se jazyka prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c61b-128">The Get-Help cmdlet also displays information about conceptual topics in Windows PowerShell, including topics about the Windows PowerShell language.</span></span> <span data-ttu-id="8c61b-129">Koncepční témata nápovědy začínat předponu "about_", jako je například about_line_editing.</span><span class="sxs-lookup"><span data-stu-id="8c61b-129">Conceptual Help topics begin with the "about_" prefix, such as about_line_editing.</span></span> <span data-ttu-id="8c61b-130">(Název koncepční téma je třeba zadat v angličtině i na jiných než anglických verzí prostředí Windows PowerShell.)</span><span class="sxs-lookup"><span data-stu-id="8c61b-130">(The name of the conceptual topic must be entered in English even on non-English versions of Windows PowerShell.)</span></span>

<span data-ttu-id="8c61b-131">Chcete-li zobrazit seznam koncepční témata, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-131">To display a list of conceptual topics, type:</span></span>

```
get-help about_*
```

<span data-ttu-id="8c61b-132">Pokud chcete zobrazit na určité téma nápovědy, zadejte například název tématu:</span><span class="sxs-lookup"><span data-stu-id="8c61b-132">To display a particular Help topic, type the topic name, for example:</span></span>

```
get-help about_command_syntax
```

<span data-ttu-id="8c61b-133">Parametry Get-Help, jako například *podrobné*, *parametr*, a *příklady*, nemají vliv na zobrazení koncepční témata nápovědy.</span><span class="sxs-lookup"><span data-stu-id="8c61b-133">The parameters of Get-Help, such as *Detailed*, *Parameter*, and *Examples*, have no effect on the display of conceptual Help topics.</span></span>

## <a name="getting-help-about-providers"></a><span data-ttu-id="8c61b-134">Získání nápovědy o zprostředkovatelích</span><span class="sxs-lookup"><span data-stu-id="8c61b-134">Getting Help About Providers</span></span>
<span data-ttu-id="8c61b-135">Rutina Get-Help zobrazí informace o poskytovatelích prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c61b-135">The Get-Help cmdlet displays information about Windows PowerShell providers.</span></span> <span data-ttu-id="8c61b-136">Chcete-li získat nápovědu pro zprostředkovatele, zadejte "Get-Help" následuje název zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="8c61b-136">To get Help for a provider, type "Get-Help" followed by the provider name.</span></span> <span data-ttu-id="8c61b-137">Například chcete-li získat nápovědu pro zprostředkovatele registru, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-137">For example, to get Help for the Registry provider, type:</span></span>

```
get-help registry
```

<span data-ttu-id="8c61b-138">Chcete-li získat seznam všech témat nápovědy zprostředkovatele v relaci, zadejte</span><span class="sxs-lookup"><span data-stu-id="8c61b-138">To get a list of all the provider Help topics in your session, type</span></span>

```
get-help -category provider
```

<span data-ttu-id="8c61b-139">Parametry Get-Help, jako například *podrobné*, *parametr*, a *příklady*, nemají vliv na zobrazení témat nápovědy zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="8c61b-139">The parameters of Get-Help, such as *Detailed*, *Parameter*, and *Examples*, have no effect on the display of provider Help topics.</span></span>

## <a name="getting-help-about-scripts-and-functions"></a><span data-ttu-id="8c61b-140">Získání nápovědy o skriptech a funkcích</span><span class="sxs-lookup"><span data-stu-id="8c61b-140">Getting Help About Scripts and Functions</span></span>
<span data-ttu-id="8c61b-141">Mnoho funkcí v prostředí Windows PowerShell a skriptů mít témata nápovědy.</span><span class="sxs-lookup"><span data-stu-id="8c61b-141">Many scripts and functions in Windows PowerShell have Help topics.</span></span> <span data-ttu-id="8c61b-142">Použijte rutinu Get-Help zobrazíte témata nápovědy pro skriptech a funkcích.</span><span class="sxs-lookup"><span data-stu-id="8c61b-142">Use the Get-Help cmdlet to display the Help topics for scripts and functions.</span></span>

<span data-ttu-id="8c61b-143">Pokud chcete zobrazit nápovědu pro funkci, zadejte "get-help" následuje název funkce.</span><span class="sxs-lookup"><span data-stu-id="8c61b-143">To display the Help for a function, type "get-help" followed by the function name.</span></span> <span data-ttu-id="8c61b-144">Například pro získání nápovědy pro funkce Disable-PSRemoting, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-144">For example, to get Help for the Disable-PSRemoting function, type:</span></span>

```
get-help disable-psremoting
```

<span data-ttu-id="8c61b-145">Chcete-li zobrazit nápovědu pro skript, zadejte plně kvalifikovanou cestu k souboru skriptu.</span><span class="sxs-lookup"><span data-stu-id="8c61b-145">To display the Help for a script, type the fully qualified path to the script file.</span></span> <span data-ttu-id="8c61b-146">Pokud se skript v cestě, která je uvedena v proměnné prostředí Path, můžete vynechat cestu z příkazu.</span><span class="sxs-lookup"><span data-stu-id="8c61b-146">If the script is in a path that is listed in the Path environment variable, you can omit the path from the command.</span></span>

<span data-ttu-id="8c61b-147">Pokud máte skript s názvem "TestScript.ps1" v jednotce C:, například\\directory PS testu chcete zobrazit téma nápovědy pro skript, typ:</span><span class="sxs-lookup"><span data-stu-id="8c61b-147">For example, if you have a script called "TestScript.ps1" in your C:\\PS-Test directory, to display the Help topic for the script, type:</span></span>

```
get-help c:\ps-test\TestScript.ps1
```

<span data-ttu-id="8c61b-148">Parametry, které byly navrženy pro zobrazení rutiny pomoci, jako například *podrobné*, *úplné*, *příklady*, a *parametr*, pracovní pro skript nápovědy a funkce Nápověda, příliš.</span><span class="sxs-lookup"><span data-stu-id="8c61b-148">The parameters that were designed for displaying cmdlet Help, such as *Detailed*, *Full*, *Examples*, and *Parameter*, work for script Help and function Help, too.</span></span> <span data-ttu-id="8c61b-149">Ale když zobrazit všechny nápovědu zadáním "get-help \*", Nápověda pro funkce a skripty se nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="8c61b-149">However, when you display all Help, by typing "get-help \*", Help for functions and scripts does not appear.</span></span>

<span data-ttu-id="8c61b-150">Informace o vytváření témata nápovědy pro funkce a skripty, najdete v tématu [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af), a [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).</span><span class="sxs-lookup"><span data-stu-id="8c61b-150">For information about writing Help topics for your functions and scripts, see [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af), and [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).</span></span>

## <a name="getting-help-online"></a><span data-ttu-id="8c61b-151">Online nápovědy</span><span class="sxs-lookup"><span data-stu-id="8c61b-151">Getting Help Online</span></span>
<span data-ttu-id="8c61b-152">Pokud jste připojeni k Internetu, je jedním z nejlepší způsoby, jak získat nápovědu zobrazte témata nápovědy online.</span><span class="sxs-lookup"><span data-stu-id="8c61b-152">If you are connected to the Internet, one of the best ways to get Help is to view the Help topics online.</span></span> <span data-ttu-id="8c61b-153">Protože online téma se dají snadno aktualizovat, jsou může zajistit nejaktuálnější obsah.</span><span class="sxs-lookup"><span data-stu-id="8c61b-153">Because online topics are easy to update, they are likely to provide the most current content.</span></span>

<span data-ttu-id="8c61b-154">Chcete-li získat online nápovědu, zkuste *Online* parametru rutiny Get-Help.</span><span class="sxs-lookup"><span data-stu-id="8c61b-154">To get Help online, try the *Online* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="8c61b-155">*Online* parametr funguje rutiny Get-Help jenom pro rutinu nápovědy, funkce nápovědy a skriptu nápovědy.</span><span class="sxs-lookup"><span data-stu-id="8c61b-155">The *Online* parameter of the Get-Help cmdlet works only for cmdlet Help, function Help, and script Help.</span></span> <span data-ttu-id="8c61b-156">Nelze použít *Online* parametr s koncepční (o) témata nebo témata nápovědy zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="8c61b-156">You cannot use the *Online* parameter with conceptual (About) topics or provider Help topics.</span></span> <span data-ttu-id="8c61b-157">Navíc vzhledem k tomu, že tato funkce je volitelný, ale nefunguje pro všechny rutiny, funkce nebo téma nápovědy skriptu.</span><span class="sxs-lookup"><span data-stu-id="8c61b-157">Also, because this feature is optional, it does not work for every cmdlet, function, or script Help topic.</span></span>

<span data-ttu-id="8c61b-158">Ale všechna témata nápovědy pocházející pomocí prostředí Windows PowerShell, včetně zprostředkovatele nápovědy a koncepční (témata nápovědy o) jsou k dispozici online v [prostředí Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) části Microsoft TechNet Library.</span><span class="sxs-lookup"><span data-stu-id="8c61b-158">However, all the Help topics that come with Windows PowerShell, including provider Help and conceptual (About) Help topics, are available online in the [Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) section of the Microsoft TechNet Library.</span></span>

<span data-ttu-id="8c61b-159">Použít *Online* parametru rutiny Get-Help, použijte následující příkaz Formát.</span><span class="sxs-lookup"><span data-stu-id="8c61b-159">To use the *Online* parameter of the Get-Help cmdlet, use the following command format.</span></span>

```
get-help <command-name> -online
```

<span data-ttu-id="8c61b-160">Například získat online verzi tématu nápovědy o rutinu Get-ChildItem, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-160">For example, to get the online version of the Help topic about the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -online
```

<span data-ttu-id="8c61b-161">Pokud je k dispozici online verzi tématu nápovědy, otevře se ve výchozím prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="8c61b-161">If an online version of the Help topic is available, it will open in your default browser.</span></span>

<span data-ttu-id="8c61b-162">Pokud online nápovědy je podporováno pro téma nápovědy, můžete také zobrazit internetové adresy (URL) tématu nápovědy.</span><span class="sxs-lookup"><span data-stu-id="8c61b-162">If online Help is supported for a Help topic, you can also view the Internet address (URL) of the Help topic.</span></span> <span data-ttu-id="8c61b-163">Internetové adresy se zobrazí v části tématu nápovědy související odkazy.</span><span class="sxs-lookup"><span data-stu-id="8c61b-163">The Internet address appears in the Related Links section of a Help topic.</span></span>

<span data-ttu-id="8c61b-164">Například najdete v části Adresa URL pro online verzi rutinu Add-Computer, zadejte:</span><span class="sxs-lookup"><span data-stu-id="8c61b-164">For example, to see the URL for the online version of the Add-Computer cmdlet, type:</span></span>

```
get-help add-computer
```

<span data-ttu-id="8c61b-165">V prvním řádku související odkazy části tohoto tématu jsou uvedeny níže.</span><span class="sxs-lookup"><span data-stu-id="8c61b-165">The first line in the Related Links section of the topic is shown below.</span></span>

```
Online version: http://go.microsoft.com/fwlink/?LinkID=135194
```

<span data-ttu-id="8c61b-166">Informace o tom, jak poskytnout online podpory společnosti Microsoft pro vaše témata nápovědy najdete v tématu [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)a zobrazit [postup nápovědě k rutině zápisu](https://go.microsoft.com/fwlink/?LinkID=123415) v knihovně MSDN.</span><span class="sxs-lookup"><span data-stu-id="8c61b-166">For information about how to provide online support for your Help topics, see [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf), and see [How to Write Cmdlet Help](https://go.microsoft.com/fwlink/?LinkID=123415) in the MSDN library.</span></span>

## <a name="see-also"></a><span data-ttu-id="8c61b-167">Viz také</span><span class="sxs-lookup"><span data-stu-id="8c61b-167">See Also</span></span>
- <span data-ttu-id="8c61b-168">[about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105)</span><span class="sxs-lookup"><span data-stu-id="8c61b-168">[about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105)</span></span>
- [<span data-ttu-id="8c61b-169">about_Scripts</span><span class="sxs-lookup"><span data-stu-id="8c61b-169">about_Scripts</span></span>](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af)
- [<span data-ttu-id="8c61b-170">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="8c61b-170">about_Comment_Based_Help</span></span>](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)
- <span data-ttu-id="8c61b-171">[Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)</span><span class="sxs-lookup"><span data-stu-id="8c61b-171">[Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)</span></span>
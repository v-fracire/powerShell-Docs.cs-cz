---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Přesměrování dat rutinami Out
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: 3ca7984e831a995e80cbd8a4d83ae9225c2a4f4c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="redirecting-data-with-out--cmdlets"></a><span data-ttu-id="81810-103">Přesměrování dat s Out-\* rutiny</span><span class="sxs-lookup"><span data-stu-id="81810-103">Redirecting Data with Out-\* Cmdlets</span></span>

<span data-ttu-id="81810-104">Prostředí Windows PowerShell poskytuje několik rutiny, která umožňují řídit přímo výstupní data.</span><span class="sxs-lookup"><span data-stu-id="81810-104">Windows PowerShell provides several cmdlets that let you control data output directly.</span></span> <span data-ttu-id="81810-105">Tyto rutiny sdílet dvě důležité charakteristiky.</span><span class="sxs-lookup"><span data-stu-id="81810-105">These cmdlets share two important characteristics.</span></span>

<span data-ttu-id="81810-106">Nejprve se obecně transformovat data na určitou formu text.</span><span class="sxs-lookup"><span data-stu-id="81810-106">First, they generally transform data to some form of text.</span></span> <span data-ttu-id="81810-107">Je to proto, že výstupní data do komponent systému, které vyžadují zadávání textu.</span><span class="sxs-lookup"><span data-stu-id="81810-107">They do this because they output the data to system components that require text input.</span></span> <span data-ttu-id="81810-108">To znamená, že potřebují k reprezentaci objektů jako text.</span><span class="sxs-lookup"><span data-stu-id="81810-108">This means they need to represent the objects as text.</span></span> <span data-ttu-id="81810-109">Text je proto naformátován, jak můžete vidět v okně konzoly prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81810-109">Therefore, the text is formatted as you see it in the Windows PowerShell console window.</span></span>

<span data-ttu-id="81810-110">Druhý, tyto rutiny použít příkaz prostředí Windows PowerShell **Out** protože odesílají informace z prostředí Windows PowerShell do jiné oblasti.</span><span class="sxs-lookup"><span data-stu-id="81810-110">Second, these cmdlets use the Windows PowerShell verb **Out** because they send information out from Windows PowerShell to somewhere else.</span></span> <span data-ttu-id="81810-111">**Odesílací hostitele** rutiny není žádná výjimka: zobrazení okna hostitele je mimo prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81810-111">The **Out-Host** cmdlet is no exception: the host window display is outside of Windows PowerShell.</span></span> <span data-ttu-id="81810-112">To je důležité, protože při odesílání dat mimo prostředí Windows PowerShell je ve skutečnosti odstraněna.</span><span class="sxs-lookup"><span data-stu-id="81810-112">This is important because when data is sent out of Windows PowerShell, it is actually removed.</span></span> <span data-ttu-id="81810-113">To můžete vidět, pokud se pokusíte vytvořit kanál data stránek do okna hostitele a pak se pokusíte formátovat jako seznam, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="81810-113">You can see this if you try to create a pipeline that pages data to the host window, and then attempt to format it as a list, as shown here:</span></span>

```powershell
Get-Process | Out-Host -Paging | Format-List
```

<span data-ttu-id="81810-114">Příkaz k zobrazení stránky informace o procesu ve formátu seznamu můžou očekávat.</span><span class="sxs-lookup"><span data-stu-id="81810-114">You might expect the command to display pages of process information in list format.</span></span> <span data-ttu-id="81810-115">Místo toho zobrazí výchozí tabulkového seznamu:</span><span class="sxs-lookup"><span data-stu-id="81810-115">Instead, it displays the default tabular list:</span></span>

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    101       5     1076       3316    32     0.05   2888 alg
...
    618      18    39348      51108   143   211.20    740 explorer
    257       8     9752      16828    79     3.02   2560 explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="81810-116">**Odesílací hostitele** rutiny odešle data přímo do konzoly, proto **Format-List** příkaz nikdy obdrží nic k formátování.</span><span class="sxs-lookup"><span data-stu-id="81810-116">The **Out-Host** cmdlet sends the data directly to the console, so the **Format-List** command never receives anything to format.</span></span>

<span data-ttu-id="81810-117">Správný způsob struktury tento příkaz je uvést **odesílací hostitele** rutinu na konci kanálu, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="81810-117">The correct way to structure this command is to put the **Out-Host** cmdlet at the end of the pipeline as shown below.</span></span> <span data-ttu-id="81810-118">To způsobí, že proces data, která mají být ve formátu v seznamu před je stránkovaného fondu a zobrazí.</span><span class="sxs-lookup"><span data-stu-id="81810-118">This causes the process data to be formatted in a list before being paged and displayed.</span></span>

```
PS> Get-Process | Format-List | Out-Host -Paging

Id      : 2888
Handles : 101
CPU     : 0.046875
Name    : alg
...

Id      : 740
Handles : 612
CPU     : 211.703125
Name    : explorer

Id      : 2560
Handles : 257
CPU     : 3.015625
Name    : explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="81810-119">To platí pro všechny **Out** rutiny.</span><span class="sxs-lookup"><span data-stu-id="81810-119">This applies to all of the **Out** cmdlets.</span></span> <span data-ttu-id="81810-120">**Out** rutiny se vždy zobrazí na konci kanálu.</span><span class="sxs-lookup"><span data-stu-id="81810-120">An **Out** cmdlet should always appear at the end of the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="81810-121">Všechny **Out** rutiny vykreslení výstupu jako text použití formátování, které platí pro v okně konzoly, včetně omezení délky řádku.</span><span class="sxs-lookup"><span data-stu-id="81810-121">All the **Out** cmdlets render output as text, using the formatting in effect for the console window, including line length limits.</span></span>

#### <a name="paging-console-output-out-host"></a><span data-ttu-id="81810-122">Stránkování výstupu konzoly (odesílací hostitele)</span><span class="sxs-lookup"><span data-stu-id="81810-122">Paging Console Output (Out-Host)</span></span>

<span data-ttu-id="81810-123">Ve výchozím nastavení, prostředí Windows PowerShell, odešle data do okna hostitele, který je co odesílací hostitele rutiny nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="81810-123">By default, Windows PowerShell sends data to the host window, which is exactly what the Out-Host cmdlet does.</span></span> <span data-ttu-id="81810-124">Primárním použitím pro odesílací hostitele rutina je stránkování dat, jak již bylo zmíněno dříve.</span><span class="sxs-lookup"><span data-stu-id="81810-124">The primary use for the Out-Host cmdlet is paging data as we discussed earlier.</span></span> <span data-ttu-id="81810-125">Například následující příkaz používá odesílací hostitele na stránku výstup rutiny Get-Command:</span><span class="sxs-lookup"><span data-stu-id="81810-125">For example, the following command uses Out-Host to page the output of the Get-Command cmdlet:</span></span>

```powershell
Get-Command | Out-Host -Paging
```

<span data-ttu-id="81810-126">Můžete také **Další** funkce k datům stránky.</span><span class="sxs-lookup"><span data-stu-id="81810-126">You can also use the **more** function to page data.</span></span> <span data-ttu-id="81810-127">V prostředí Windows PowerShell **Další** je funkce, která volá **odesílací hostitel-stránkování**.</span><span class="sxs-lookup"><span data-stu-id="81810-127">In Windows PowerShell, **more** is a function that calls **Out-Host -Paging**.</span></span> <span data-ttu-id="81810-128">Následující příkaz ukazuje, jak pomocí **Další** funkce na stránku výstup Get-Command:</span><span class="sxs-lookup"><span data-stu-id="81810-128">The following command demonstrates using the **more** function to page the output of Get-Command:</span></span>

```powershell
Get-Command | more
```

<span data-ttu-id="81810-129">Pokud jeden nebo více názvů souborů zahrnete jako argumenty pro další funkce, funkce přečte zadané soubory a stránka jejich obsah na hostitele:</span><span class="sxs-lookup"><span data-stu-id="81810-129">If you include one or more filenames as arguments to the more function, the function will read the specified files and page their contents to the host:</span></span>

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a><span data-ttu-id="81810-130">Výstupních zahození (odesílací Null)</span><span class="sxs-lookup"><span data-stu-id="81810-130">Discarding Output (Out-Null)</span></span>

<span data-ttu-id="81810-131">**Odesílací Null** rutina umožňuje okamžitě zahodit žádný vstup obdrží.</span><span class="sxs-lookup"><span data-stu-id="81810-131">The **Out-Null** cmdlet is designed to immediately discard any input it receives.</span></span> <span data-ttu-id="81810-132">To je užitečné pro zahození nepotřebná data, který jste získali v vedlejším účinkem spuštění příkazu.</span><span class="sxs-lookup"><span data-stu-id="81810-132">This is useful for discarding unnecessary data that you get as a side-effect of running a command.</span></span> <span data-ttu-id="81810-133">Když zadáte následující příkaz, obdržíte nic zpět z tohoto příkazu:</span><span class="sxs-lookup"><span data-stu-id="81810-133">When type the following command, you do not get anything back from the command:</span></span>

```powreshell
Get-Command | Out-Null
```

<span data-ttu-id="81810-134">**Odesílací Null** rutiny není zahodit výstupní chybě.</span><span class="sxs-lookup"><span data-stu-id="81810-134">The **Out-Null** cmdlet does not discard error output.</span></span> <span data-ttu-id="81810-135">Například pokud zadáte následující příkaz, zobrazí se zpráva oznamující, že prostředí Windows PowerShell nebyl rozpoznán 'Je NotACommand':</span><span class="sxs-lookup"><span data-stu-id="81810-135">For example, if you enter the following command, a message is displayed informing you that Windows PowerShell does not recognize 'Is-NotACommand':</span></span>

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a><span data-ttu-id="81810-136">Tisk dat (domáčtí tiskárny)</span><span class="sxs-lookup"><span data-stu-id="81810-136">Printing Data (Out-Printer)</span></span>

<span data-ttu-id="81810-137">Data můžete vytisknout pomocí **domáčtí tiskárny** rutiny.</span><span class="sxs-lookup"><span data-stu-id="81810-137">You can print data by using the **Out-Printer** cmdlet.</span></span> <span data-ttu-id="81810-138">**Domáčtí tiskárny** rutiny bude používat výchozí tiskárny, pokud nezadáte název tiskárny.</span><span class="sxs-lookup"><span data-stu-id="81810-138">The **Out-Printer** cmdlet will use your default printer if you do not provide a printer name.</span></span> <span data-ttu-id="81810-139">Všechny tiskárny systému Windows můžete použít zadáním jeho zobrazovaný název.</span><span class="sxs-lookup"><span data-stu-id="81810-139">You can use any Windows-based printer by specifying its display name.</span></span> <span data-ttu-id="81810-140">Není nutné pro jakýkoli druh mapování portů tiskáren nebo i skutečných fyzické tiskárny.</span><span class="sxs-lookup"><span data-stu-id="81810-140">There is no need for any kind of printer port mapping or even a real physical printer.</span></span> <span data-ttu-id="81810-141">Například pokud máte nástroje pro vytváření bitových kopií dokumentu aplikace Microsoft Office nainstalované, může posílat data do souboru bitové kopie zadáním:</span><span class="sxs-lookup"><span data-stu-id="81810-141">For example, if you have the Microsoft Office document imaging tools installed, you can send the data to an image file by typing:</span></span>

```powershell
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'
```

#### <a name="saving-data-out-file"></a><span data-ttu-id="81810-142">Ukládání dat (out-File)</span><span class="sxs-lookup"><span data-stu-id="81810-142">Saving Data (Out-File)</span></span>

<span data-ttu-id="81810-143">Můžete odesílat výstup do souboru místo v okně konzoly pomocí **out-File** rutiny.</span><span class="sxs-lookup"><span data-stu-id="81810-143">You can send output to a file instead of the console window by using the **Out-File** cmdlet.</span></span> <span data-ttu-id="81810-144">Následující příkazový řádek odešle seznam procesů do souboru **C:\\temp\\processlist.txt**:</span><span class="sxs-lookup"><span data-stu-id="81810-144">The following command line sends a list of processes to the file **C:\\temp\\processlist.txt**:</span></span>

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

<span data-ttu-id="81810-145">Výsledky pomocí **out-File** rutiny nemusí být toho, co očekáváte, pokud se používají k přesměrování tradiční výstupu.</span><span class="sxs-lookup"><span data-stu-id="81810-145">The results of using the **Out-File** cmdlet may not be what you expect if you are used to traditional output redirection.</span></span> <span data-ttu-id="81810-146">Pochopit své chování, musí mít přehled o kontextu, ve kterém **out-File** rutiny funguje.</span><span class="sxs-lookup"><span data-stu-id="81810-146">To understand its behavior, you must be aware of the context in which the **Out-File** cmdlet operates.</span></span>

<span data-ttu-id="81810-147">Ve výchozím nastavení **out-File** rutina vytvoří soubor kódování Unicode.</span><span class="sxs-lookup"><span data-stu-id="81810-147">By default, the **Out-File** cmdlet creates a Unicode file.</span></span> <span data-ttu-id="81810-148">Toto je nejlepší výchozí dlouhodobě, ale znamená, že nástroje, které očekávají soubory ASCII nebude správně fungovat s výchozí formát výstupu.</span><span class="sxs-lookup"><span data-stu-id="81810-148">This is the best default in the long run, but it means that tools that expect ASCII files will not work correctly with the default output format.</span></span> <span data-ttu-id="81810-149">Výchozí formát výstupu do ASCII můžete změnit pomocí **kódování** parametr:</span><span class="sxs-lookup"><span data-stu-id="81810-149">You can change the default output format to ASCII by using the **Encoding** parameter:</span></span>

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

<span data-ttu-id="81810-150">**Out-File** formátů souboru obsahu, aby vypadala jako výstup konzoly.</span><span class="sxs-lookup"><span data-stu-id="81810-150">**Out-file** formats file contents to look like console output.</span></span> <span data-ttu-id="81810-151">To způsobí, že výstup k oříznutí stejně, jako je v okně konzoly ve většině případů.</span><span class="sxs-lookup"><span data-stu-id="81810-151">This causes the output to be truncated just as it is in a console window in most circumstances.</span></span> <span data-ttu-id="81810-152">Například pokud spustíte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="81810-152">For example, if you run the following command:</span></span>

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt
```

<span data-ttu-id="81810-153">Výstup bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="81810-153">The output will look like this:</span></span>

```output
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

<span data-ttu-id="81810-154">Chcete-li získat výstup, který bez vynucení zalomení řádků tak, aby odpovídaly šířku obrazovky, můžete použít **šířka** parametr k určení šířka čáry.</span><span class="sxs-lookup"><span data-stu-id="81810-154">To get output that does not force line wraps to match the screen width, you can use the **Width** parameter to specify line width.</span></span> <span data-ttu-id="81810-155">Protože **šířka** je parametr 32bitové celé číslo, může mít maximální hodnota je 2147483647.</span><span class="sxs-lookup"><span data-stu-id="81810-155">Because **Width** is a 32-bit integer parameter, the maximum value it can have is 2147483647.</span></span> <span data-ttu-id="81810-156">Zadejte následující příkaz a nastavte šířku čáry na tuto maximální hodnotu:</span><span class="sxs-lookup"><span data-stu-id="81810-156">Type the following to set the line width to this maximum value:</span></span>

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

<span data-ttu-id="81810-157">**Out-File** rutina je velmi užitečné, pokud chcete uložit výstup, který by mají zobrazovat v konzole.</span><span class="sxs-lookup"><span data-stu-id="81810-157">The **Out-File** cmdlet is most useful when you want to save output as it would have displayed on the console.</span></span> <span data-ttu-id="81810-158">Pro lepší kontrolu nad výstupní formát budete potřebovat pokročilejší nástroje.</span><span class="sxs-lookup"><span data-stu-id="81810-158">For finer control over output format, you need more advanced tools.</span></span> <span data-ttu-id="81810-159">Podíváme se na těch, které v další kapitoly, společně s některé podrobnosti o manipulaci s objektu.</span><span class="sxs-lookup"><span data-stu-id="81810-159">We will look at those in the next chapter, along with some details about object manipulation.</span></span>
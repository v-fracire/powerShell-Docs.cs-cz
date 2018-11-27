---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Přesměrování dat rutinami Out
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: f08879f436ce751b176af020aba21e90f09aa61f
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321005"
---
# <a name="redirecting-data-with-out--cmdlets"></a><span data-ttu-id="7f576-103">Přesměrování dat Out-\* rutiny</span><span class="sxs-lookup"><span data-stu-id="7f576-103">Redirecting Data with Out-\* Cmdlets</span></span>

<span data-ttu-id="7f576-104">Prostředí Windows PowerShell poskytuje několik rutin, které umožňují řídit přímo výstupní data.</span><span class="sxs-lookup"><span data-stu-id="7f576-104">Windows PowerShell provides several cmdlets that let you control data output directly.</span></span> <span data-ttu-id="7f576-105">Tyto rutiny sdílet dvě důležité charakteristiky.</span><span class="sxs-lookup"><span data-stu-id="7f576-105">These cmdlets share two important characteristics.</span></span>

<span data-ttu-id="7f576-106">Nejprve se obecně transformovat data na nějakou formu text.</span><span class="sxs-lookup"><span data-stu-id="7f576-106">First, they generally transform data to some form of text.</span></span> <span data-ttu-id="7f576-107">Je to proto, že výstupní data do systémových komponent, které vyžadují vaše zadání textu.</span><span class="sxs-lookup"><span data-stu-id="7f576-107">They do this because they output the data to system components that require text input.</span></span> <span data-ttu-id="7f576-108">To znamená, že potřebují k reprezentaci objektů jako text.</span><span class="sxs-lookup"><span data-stu-id="7f576-108">This means they need to represent the objects as text.</span></span> <span data-ttu-id="7f576-109">Proto se text formátovaný jako se zobrazí v okně konzoly Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="7f576-109">Therefore, the text is formatted as you see it in the Windows PowerShell console window.</span></span>

<span data-ttu-id="7f576-110">Za druhé, tyto rutiny použít příkaz prostředí Windows PowerShell **si** vzhledem k tomu, že odesílat informace z prostředí Windows PowerShell někde jinde.</span><span class="sxs-lookup"><span data-stu-id="7f576-110">Second, these cmdlets use the Windows PowerShell verb **Out** because they send information out from Windows PowerShell to somewhere else.</span></span> <span data-ttu-id="7f576-111">**Out-Buffer: hostování** rutina není žádná výjimka: zobrazení okna hostitele je mimo prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f576-111">The **Out-Host** cmdlet is no exception: the host window display is outside of Windows PowerShell.</span></span> <span data-ttu-id="7f576-112">To je důležité, protože když se data odesílají z prostředí Windows PowerShell, ve skutečnosti se odebere.</span><span class="sxs-lookup"><span data-stu-id="7f576-112">This is important because when data is sent out of Windows PowerShell, it is actually removed.</span></span> <span data-ttu-id="7f576-113">To můžete vidět, pokud při pokusu o vytvoření kanálu data stránek do okna hostitele a pak se pokusíte naformátovat jako seznam, jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="7f576-113">You can see this if you try to create a pipeline that pages data to the host window, and then attempt to format it as a list, as shown here:</span></span>

```powershell
Get-Process | Out-Host -Paging | Format-List
```

<span data-ttu-id="7f576-114">Očekáváte příkaz pro zobrazování stránek informace o procesu ve formátu seznamu.</span><span class="sxs-lookup"><span data-stu-id="7f576-114">You might expect the command to display pages of process information in list format.</span></span> <span data-ttu-id="7f576-115">Místo toho zobrazí výchozí tabulkového seznamu:</span><span class="sxs-lookup"><span data-stu-id="7f576-115">Instead, it displays the default tabular list:</span></span>

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

<span data-ttu-id="7f576-116">**Out-Buffer: hostování** rutiny odešle data přímo do konzoly, proto **Format-List** příkaz nikdy obdrží nic k formátování.</span><span class="sxs-lookup"><span data-stu-id="7f576-116">The **Out-Host** cmdlet sends the data directly to the console, so the **Format-List** command never receives anything to format.</span></span>

<span data-ttu-id="7f576-117">Správný způsob strukturování tento příkaz je umístit **out-Buffer: hostování** rutiny na konci kanálu, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="7f576-117">The correct way to structure this command is to put the **Out-Host** cmdlet at the end of the pipeline as shown below.</span></span> <span data-ttu-id="7f576-118">To způsobí, že zpracování dat, který má být formátována v seznamu před se stránkováním a zobrazí.</span><span class="sxs-lookup"><span data-stu-id="7f576-118">This causes the process data to be formatted in a list before being paged and displayed.</span></span>

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

<span data-ttu-id="7f576-119">To platí pro všechny **si** rutiny.</span><span class="sxs-lookup"><span data-stu-id="7f576-119">This applies to all of the **Out** cmdlets.</span></span> <span data-ttu-id="7f576-120">**Si** rutiny by se měla vždy zobrazit na konci kanálu.</span><span class="sxs-lookup"><span data-stu-id="7f576-120">An **Out** cmdlet should always appear at the end of the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="7f576-121">Všechny **si** rutiny vykreslení výstupu jako text, použití v platnosti formátování okna konzoly, včetně omezení délky řádku.</span><span class="sxs-lookup"><span data-stu-id="7f576-121">All the **Out** cmdlets render output as text, using the formatting in effect for the console window, including line length limits.</span></span>

#### <a name="paging-console-output-out-host"></a><span data-ttu-id="7f576-122">Stránkování výstupu konzoly (out-Buffer: hostitelské)</span><span class="sxs-lookup"><span data-stu-id="7f576-122">Paging Console Output (Out-Host)</span></span>

<span data-ttu-id="7f576-123">Ve výchozím nastavení, prostředí Windows PowerShell, odesílá data do okna hostitele, což je přesně to, co hostování odesílací rutina nemá.</span><span class="sxs-lookup"><span data-stu-id="7f576-123">By default, Windows PowerShell sends data to the host window, which is exactly what the Out-Host cmdlet does.</span></span> <span data-ttu-id="7f576-124">Primárně používají k hostování odesílací rutina je stránkování dat, jak jsme probírali výše.</span><span class="sxs-lookup"><span data-stu-id="7f576-124">The primary use for the Out-Host cmdlet is paging data as we discussed earlier.</span></span> <span data-ttu-id="7f576-125">Například následující použití příkazu out-Buffer: hostovat na stránce výstupem rutiny Get-– příkaz:</span><span class="sxs-lookup"><span data-stu-id="7f576-125">For example, the following command uses Out-Host to page the output of the Get-Command cmdlet:</span></span>

```powershell
Get-Command | Out-Host -Paging
```

<span data-ttu-id="7f576-126">Můžete také použít **Další** funkce k datům stránky.</span><span class="sxs-lookup"><span data-stu-id="7f576-126">You can also use the **more** function to page data.</span></span> <span data-ttu-id="7f576-127">V prostředí Windows PowerShell **Další** je funkce, která volá **out-Buffer: hostování-stránkování**.</span><span class="sxs-lookup"><span data-stu-id="7f576-127">In Windows PowerShell, **more** is a function that calls **Out-Host -Paging**.</span></span> <span data-ttu-id="7f576-128">Následující příkaz ukazuje použití **Další** funkce na stránce výstup Get-– příkaz:</span><span class="sxs-lookup"><span data-stu-id="7f576-128">The following command demonstrates using the **more** function to page the output of Get-Command:</span></span>

```powershell
Get-Command | more
```

<span data-ttu-id="7f576-129">Zadáte-li jeden nebo více názvů souborů jako argumenty, které mají další funkce, funkce se načíst zadané soubory a stránek jejich obsah na hostitele:</span><span class="sxs-lookup"><span data-stu-id="7f576-129">If you include one or more filenames as arguments to the more function, the function will read the specified files and page their contents to the host:</span></span>

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a><span data-ttu-id="7f576-130">Zahazuje se výstup (out-Buffer: Null)</span><span class="sxs-lookup"><span data-stu-id="7f576-130">Discarding Output (Out-Null)</span></span>

<span data-ttu-id="7f576-131">**Out-Buffer: Null** rutina slouží k okamžitě zrušit všechny vstupní přijme.</span><span class="sxs-lookup"><span data-stu-id="7f576-131">The **Out-Null** cmdlet is designed to immediately discard any input it receives.</span></span> <span data-ttu-id="7f576-132">To je užitečné pro nepotřebná data, abyste získali jako vedlejší efekt spuštění příkazu se zahodí.</span><span class="sxs-lookup"><span data-stu-id="7f576-132">This is useful for discarding unnecessary data that you get as a side-effect of running a command.</span></span> <span data-ttu-id="7f576-133">Když zadáte následující příkaz, se nezobrazí nic zpět z tohoto příkazu:</span><span class="sxs-lookup"><span data-stu-id="7f576-133">When type the following command, you do not get anything back from the command:</span></span>

```powershell
Get-Command | Out-Null
```

<span data-ttu-id="7f576-134">**Out-Buffer: Null** rutina není zahodit chybový výstup.</span><span class="sxs-lookup"><span data-stu-id="7f576-134">The **Out-Null** cmdlet does not discard error output.</span></span> <span data-ttu-id="7f576-135">Například pokud zadáte následující příkaz, zobrazí se zpráva oznamující, že prostředí Windows PowerShell nerozpozná "Je NotACommand":</span><span class="sxs-lookup"><span data-stu-id="7f576-135">For example, if you enter the following command, a message is displayed informing you that Windows PowerShell does not recognize 'Is-NotACommand':</span></span>

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a><span data-ttu-id="7f576-136">Tisk Data (domáčtí tiskárny)</span><span class="sxs-lookup"><span data-stu-id="7f576-136">Printing Data (Out-Printer)</span></span>

<span data-ttu-id="7f576-137">Data lze vytisknout pomocí **domáčtí tiskárny** rutiny.</span><span class="sxs-lookup"><span data-stu-id="7f576-137">You can print data by using the **Out-Printer** cmdlet.</span></span> <span data-ttu-id="7f576-138">**Domáčtí tiskárny** rutiny použije výchozí tiskárna, pokud nezadáte název tiskárny.</span><span class="sxs-lookup"><span data-stu-id="7f576-138">The **Out-Printer** cmdlet will use your default printer if you do not provide a printer name.</span></span> <span data-ttu-id="7f576-139">Tiskárny založené na Windows můžete použít tak, že zadáte jeho zobrazované jméno.</span><span class="sxs-lookup"><span data-stu-id="7f576-139">You can use any Windows-based printer by specifying its display name.</span></span> <span data-ttu-id="7f576-140">Není nutné pro jakýkoli druh mapování portů tiskáren nebo dokonce skutečné fyzické tiskárny.</span><span class="sxs-lookup"><span data-stu-id="7f576-140">There is no need for any kind of printer port mapping or even a real physical printer.</span></span> <span data-ttu-id="7f576-141">Například pokud máte nástroje pro vytváření bitových kopií dokumentu aplikace Microsoft Office nainstalovaný, můžete odeslat data na soubor obrázku tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="7f576-141">For example, if you have the Microsoft Office document imaging tools installed, you can send the data to an image file by typing:</span></span>

```powershell
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'
```

#### <a name="saving-data-out-file"></a><span data-ttu-id="7f576-142">Ukládání dat (out-File)</span><span class="sxs-lookup"><span data-stu-id="7f576-142">Saving Data (Out-File)</span></span>

<span data-ttu-id="7f576-143">S použitím může odeslat výstup do souboru místo v okně konzoly **out-File** rutiny.</span><span class="sxs-lookup"><span data-stu-id="7f576-143">You can send output to a file instead of the console window by using the **Out-File** cmdlet.</span></span> <span data-ttu-id="7f576-144">Následující příkazový řádek odešle seznam procesů k souboru **C:\\temp\\processlist.txt**:</span><span class="sxs-lookup"><span data-stu-id="7f576-144">The following command line sends a list of processes to the file **C:\\temp\\processlist.txt**:</span></span>

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

<span data-ttu-id="7f576-145">Výsledky použití **out-File** rutiny nemusí být co očekáváte, že pokud se používají k přesměrování tradiční výstupu.</span><span class="sxs-lookup"><span data-stu-id="7f576-145">The results of using the **Out-File** cmdlet may not be what you expect if you are used to traditional output redirection.</span></span> <span data-ttu-id="7f576-146">Informace o tom své chování, musí mít přehled o kontextu, ve kterém **out-File** rutina funguje.</span><span class="sxs-lookup"><span data-stu-id="7f576-146">To understand its behavior, you must be aware of the context in which the **Out-File** cmdlet operates.</span></span>

<span data-ttu-id="7f576-147">Ve výchozím nastavení **out-File** rutina vytvoří soubor Unicode.</span><span class="sxs-lookup"><span data-stu-id="7f576-147">By default, the **Out-File** cmdlet creates a Unicode file.</span></span> <span data-ttu-id="7f576-148">Toto je doporučené výchozí dlouhodobě, ale znamená, že nástroje, které očekávají soubory ASCII nebudou fungovat správně s výchozí formát výstupu.</span><span class="sxs-lookup"><span data-stu-id="7f576-148">This is the best default in the long run, but it means that tools that expect ASCII files will not work correctly with the default output format.</span></span> <span data-ttu-id="7f576-149">Můžete změnit výchozí formát výstupu na ASCII pomocí **kódování** parametr:</span><span class="sxs-lookup"><span data-stu-id="7f576-149">You can change the default output format to ASCII by using the **Encoding** parameter:</span></span>

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

<span data-ttu-id="7f576-150">**Out-File** formátů souboru obsahu, aby vypadala jako výstup na konzole.</span><span class="sxs-lookup"><span data-stu-id="7f576-150">**Out-file** formats file contents to look like console output.</span></span> <span data-ttu-id="7f576-151">To způsobí, že výstupní má být zkráceno stejně, jako je v okně konzoly ve většině případů.</span><span class="sxs-lookup"><span data-stu-id="7f576-151">This causes the output to be truncated just as it is in a console window in most circumstances.</span></span> <span data-ttu-id="7f576-152">Například pokud spustíte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="7f576-152">For example, if you run the following command:</span></span>

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt
```

<span data-ttu-id="7f576-153">Výstup bude vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="7f576-153">The output will look like this:</span></span>

```output
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

<span data-ttu-id="7f576-154">Chcete-li získat výstup, který se nevynutí zalomení řádků tak, aby odpovídaly šířka obrazovky, můžete použít **šířka** parametr k určení tloušťka čáry.</span><span class="sxs-lookup"><span data-stu-id="7f576-154">To get output that does not force line wraps to match the screen width, you can use the **Width** parameter to specify line width.</span></span> <span data-ttu-id="7f576-155">Protože **šířka** je parametr 32bitové celé číslo, může mít maximální hodnota je 2147483647.</span><span class="sxs-lookup"><span data-stu-id="7f576-155">Because **Width** is a 32-bit integer parameter, the maximum value it can have is 2147483647.</span></span> <span data-ttu-id="7f576-156">Zadejte následující příkaz pro nastavení tloušťka čáry této maximální hodnotě:</span><span class="sxs-lookup"><span data-stu-id="7f576-156">Type the following to set the line width to this maximum value:</span></span>

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

<span data-ttu-id="7f576-157">**Out-File** rutina je nejužitečnější, pokud chcete uložit výstup, který bude mít zobrazí v konzole.</span><span class="sxs-lookup"><span data-stu-id="7f576-157">The **Out-File** cmdlet is most useful when you want to save output as it would have displayed on the console.</span></span> <span data-ttu-id="7f576-158">Pro lepší kontrolu nad formátem výstupu budete potřebovat další pokročilé nástroje.</span><span class="sxs-lookup"><span data-stu-id="7f576-158">For finer control over output format, you need more advanced tools.</span></span> <span data-ttu-id="7f576-159">Podíváme se na ty v následující kapitole spolu s některé podrobnosti o manipulaci s objekty.</span><span class="sxs-lookup"><span data-stu-id="7f576-159">We will look at those in the next chapter, along with some details about object manipulation.</span></span>
---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vysvětlení kanálu Windows PowerShellu
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: c3f1d17432cf3a77c0f5ecae137a4233a28a19d7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="understanding-the-windows-powershell-pipeline"></a><span data-ttu-id="dbc4c-103">Vysvětlení kanálu Windows PowerShellu</span><span class="sxs-lookup"><span data-stu-id="dbc4c-103">Understanding the Windows PowerShell Pipeline</span></span>
<span data-ttu-id="dbc4c-104">Zřetězení prakticky všude, kde funguje v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-104">Piping works virtually everywhere in Windows PowerShell.</span></span> <span data-ttu-id="dbc4c-105">I když text se zobrazí na obrazovce, nejsou prostřednictvím prostředí Windows PowerShell kanálu text mezi příkazy.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-105">Although you see text on the screen, Windows PowerShell does not pipe text between commands.</span></span> <span data-ttu-id="dbc4c-106">Místo toho ji prostřednictvím kanálu předá objekty.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-106">Instead, it pipes objects.</span></span>

<span data-ttu-id="dbc4c-107">Zápis použitý pro kanály je podobný které byly použity v jiné prostředí shell, takže na první pohled nemusí být zřejmé, že prostředí Windows PowerShell zavádí nové.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-107">The notation used for pipelines is similar to that used in other shells, so at first glance, it may not be apparent that Windows PowerShell introduces something new.</span></span> <span data-ttu-id="dbc4c-108">Například pokud použijete **odesílací hostitele** k vynucení po stránkách zobrazení výstupu z jiného příkazu, výstup vypadá stejně jako běžný text zobrazené na obrazovce, rozdělené stránky:</span><span class="sxs-lookup"><span data-stu-id="dbc4c-108">For example, if you use the **Out-Host** cmdlet to force a page-by-page display of output from another command, the output looks just like the normal text displayed on the screen, broken up into pages:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\system32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2005-10-22  11:04 PM        315 $winnt$.inf
-a---        2004-08-04   8:00 AM      68608 access.cpl
-a---        2004-08-04   8:00 AM      64512 acctres.dll
-a---        2004-08-04   8:00 AM     183808 accwiz.exe
-a---        2004-08-04   8:00 AM      61952 acelpdec.ax
-a---        2004-08-04   8:00 AM     129536 acledit.dll
-a---        2004-08-04   8:00 AM     114688 aclui.dll
-a---        2004-08-04   8:00 AM     194048 activeds.dll
-a---        2004-08-04   8:00 AM     111104 activeds.tlb
-a---        2004-08-04   8:00 AM       4096 actmovie.exe
-a---        2004-08-04   8:00 AM     101888 actxprxy.dll
-a---        2003-02-21   6:50 PM     143150 admgmt.msc
-a---        2006-01-25   3:35 PM      53760 admparse.dll
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="dbc4c-109">Out-Host-příkaz stránkování je element užitečné kanálu vždy, když máte zdlouhavé výstupu, který chcete zobrazit pomalu.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-109">The Out-Host -Paging command is a useful pipeline element whenever you have lengthy output that you would like to display slowly.</span></span> <span data-ttu-id="dbc4c-110">Je obzvláště užitečná pokud operace je velmi náročná na prostředky procesoru.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-110">It is especially useful if the operation is very CPU-intensive.</span></span> <span data-ttu-id="dbc4c-111">Protože zpracování se přenese do odesílací hostitele rutiny pokud obsahuje kompletní stránku připravena k zobrazení, rutin, které předcházet v kanálu zastaví operaci, dokud na další stránku výstupu je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-111">Because processing is transferred to the Out-Host cmdlet when it has a complete page ready to display, cmdlets that precede it in the pipeline halt operation until the next page of output is available.</span></span> <span data-ttu-id="dbc4c-112">Pokud použijete Správce úloh systému Windows ke sledování procesoru a paměti pomocí prostředí Windows PowerShell najdete v to.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-112">You can see this if you use the Windows Task Manager to monitor CPU and memory use by Windows PowerShell.</span></span>

<span data-ttu-id="dbc4c-113">Spusťte následující příkaz: **C: Get-ChildItem\\Windows-Recurse**.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-113">Run the following command: **Get-ChildItem C:\\Windows -Recurse**.</span></span> <span data-ttu-id="dbc4c-114">Porovnání využití procesoru a paměti na tento příkaz: **Get-ChildItem C:\\Windows-Recurse | Odesílací Host-stránkování**.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-114">Compare the CPU and memory usage to this command: **Get-ChildItem C:\\Windows -Recurse | Out-Host -Paging**.</span></span> <span data-ttu-id="dbc4c-115">Zobrazte na obrazovce je text, ale je to způsobeno je nezbytné k reprezentaci objektů jako text v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-115">What you see on the screen is text, but that is because it is necessary to represent objects as text in a console window.</span></span> <span data-ttu-id="dbc4c-116">To je právě reprezentace co je skutečně probíhající v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-116">This is just a representation of what is really going on inside Windows PowerShell.</span></span> <span data-ttu-id="dbc4c-117">Zvažte například rutinu Get-umístění.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-117">For example, consider the Get-Location cmdlet.</span></span> <span data-ttu-id="dbc4c-118">Pokud zadáte **Get-umístění** sice vaše aktuální umístění kořenové složce jednotky C, zobrazí se následující výstup:</span><span class="sxs-lookup"><span data-stu-id="dbc4c-118">If you type **Get-Location** while your current location is the root of the C drive, you would see the following output:</span></span>

```
PS> Get-Location

Path
----
C:\
```

<span data-ttu-id="dbc4c-119">Pokud prostředí Windows PowerShell zřetězena text, vydání příkazu, jako **Get-umístění | Odesílací hostitele**, by úspěšně prošel zpracováním z **Get-umístění** k **odesílací hostitele** sadu znaků v pořadí, jsou zobrazeny na obrazovce.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-119">If Windows PowerShell pipelined text, issuing a command such as **Get-Location | Out-Host**, would pass from **Get-Location** to **Out-Host** a set of characters in the order they are displayed onscreen.</span></span> <span data-ttu-id="dbc4c-120">Jinými slovy, pokud byste chtěli ignorovat informace záhlaví, **odesílací hostitele** nejprve obdrží znak '**C'**, pak znak '**:'**, pak znak ' **\\'**.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-120">In other words, if you were to ignore the heading information, **Out-Host** would first receive the character '**C'**, then the character '**:'**, then the character '**\\'**.</span></span> <span data-ttu-id="dbc4c-121">**Odesílací hostitele** rutiny nelze určit, co znamená přidružit výstup znaků pomocí **Get-umístění** rutiny.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-121">The **Out-Host** cmdlet could not determine what meaning to associate with the characters output by the **Get-Location** cmdlet.</span></span>

<span data-ttu-id="dbc4c-122">Místo použití text umožníte příkazy v kanálu komunikovat, prostředí Windows PowerShell pomocí objektů.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-122">Instead of using text to let commands in a pipeline communicate, Windows PowerShell uses objects.</span></span> <span data-ttu-id="dbc4c-123">Z hlediska uživatelů objekty balíček související informace do formuláře, který usnadňuje manipulovat s informacemi jako jednotku a extrahovat konkrétní položky, které potřebujete.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-123">From the standpoint of a user, objects package related information into a form that makes it easier to manipulate the information as a unit, and extract specific items that you need.</span></span>

<span data-ttu-id="dbc4c-124">**Get-umístění** příkaz nevrací text, který obsahuje aktuální cestě.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-124">The **Get-Location** command does not return text that contains the current path.</span></span> <span data-ttu-id="dbc4c-125">Vrátí balíček informace nazývané **PathInfo** objekt, který obsahuje aktuální cestě společně s některé další informace.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-125">It returns a package of information called a **PathInfo** object that contains the current path along with some other information.</span></span> <span data-ttu-id="dbc4c-126">**Odesílací hostitele** rutiny pak odešle tento **PathInfo** objekt, který chcete obrazovky a prostředí Windows PowerShell rozhodne informace k zobrazení a jak ji zobrazit založené na jeho pravidla formátování.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-126">The **Out-Host** cmdlet then sends this **PathInfo** object to the screen, and Windows PowerShell decides what information to display and how to display it based on its formatting rules.</span></span>

<span data-ttu-id="dbc4c-127">Ve skutečnosti výstupem informace v hlavičce **Get-umístění** rutiny je přidána pouze na konci procesu, jako součást procesu formátování data pro zobrazení na obrazovce.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-127">In fact, the heading information output by the **Get-Location** cmdlet is added only at the end of the process, as part of the process of formatting the data for onscreen display.</span></span> <span data-ttu-id="dbc4c-128">Co se zobrazí na obrazovce je souhrnné informace a úplný reprezentace objektu výstup.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-128">What you see onscreen is a summary of information, and not a complete representation of the output object.</span></span>

<span data-ttu-id="dbc4c-129">Vzhledem k tomu, že může být další informace o výstupní z prostředí Windows PowerShell příkaz než budeme najdete v okně konzoly zobrazí jak může načtete neviditelné prvky?</span><span class="sxs-lookup"><span data-stu-id="dbc4c-129">Given that there may be more information output from a Windows PowerShell command than what we see displayed in the console window, how can you retrieve the non-visible elements?</span></span> <span data-ttu-id="dbc4c-130">Jak si zobrazit doplňující data?</span><span class="sxs-lookup"><span data-stu-id="dbc4c-130">How do you view the extra data?</span></span> <span data-ttu-id="dbc4c-131">A co dělat, když chcete zobrazit data ve formátu, liší od jednoho prostředí Windows PowerShell normálně používá?</span><span class="sxs-lookup"><span data-stu-id="dbc4c-131">And what if you want to view the data in a format different than the one Windows PowerShell normally uses?</span></span>

<span data-ttu-id="dbc4c-132">Zbytek této kapitoly popisuje, jak můžete zjistit struktura konkrétní objektů prostředí Windows PowerShell, vyberete konkrétní položky a formátování je snazší zobrazení a jak odesílat výše uvedené informace, jako alternativní výstupní umístění souborů a tiskárny.</span><span class="sxs-lookup"><span data-stu-id="dbc4c-132">The rest of this chapter discusses how you can discover the structure of specific Windows PowerShell objects, selecting specific items and formatting them for easier display, and how to send this information to alternative output locations such as files and printers.</span></span>
---
ms.date: 08/23/2018
keywords: rutiny prostředí PowerShell
title: Principy kanály v Powershellu
ms.assetid: 6be50926-7943-4ef7-9499-4490d72a63fb
ms.openlocfilehash: 3ee03f001668fb24ff9be1ea6ecb3817e319d0ee
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134212"
---
# <a name="understanding-pipelines"></a><span data-ttu-id="dc0bc-103">Principy kanály</span><span class="sxs-lookup"><span data-stu-id="dc0bc-103">Understanding pipelines</span></span>

<span data-ttu-id="dc0bc-104">Kanály fungují jako řada připojených segmenty kanálu.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-104">Pipelines act like a series of connected segments of pipe.</span></span> <span data-ttu-id="dc0bc-105">Položky přesun podél kanálu prochází každý segment.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-105">Items moving along the pipeline pass through each segment.</span></span> <span data-ttu-id="dc0bc-106">K vytvoření kanálu v prostředí PowerShell, připojíte příkazy spolu s operátorem kanálu "|".</span><span class="sxs-lookup"><span data-stu-id="dc0bc-106">To create a pipeline in PowerShell, you connect commands together with the pipe operator "|".</span></span> <span data-ttu-id="dc0bc-107">Tento výstup každý příkaz se používá jako vstup pro další příkaz.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-107">The output of each command is used as input to the next command.</span></span>

<span data-ttu-id="dc0bc-108">Zápis použitý pro kanály se podobá notaci používané v jiných prostředí.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-108">The notation used for pipelines is similar to the notation used in other shells.</span></span> <span data-ttu-id="dc0bc-109">Na první pohled nemusí být zřejmé, jak se liší v prostředí PowerShell kanály.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-109">At first glance, it may not be apparent how pipelines are different in PowerShell.</span></span> <span data-ttu-id="dc0bc-110">I když se text zobrazí na obrazovce, prostředí PowerShell prostřednictvím kanálu předá objekty, není text mezi příkazy.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-110">Although you see text on the screen, PowerShell pipes objects, not text, between commands.</span></span>

## <a name="the-powershell-pipeline"></a><span data-ttu-id="dc0bc-111">Kanál prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc0bc-111">The PowerShell pipeline</span></span>

<span data-ttu-id="dc0bc-112">Kanály jsou pravděpodobně nejcennější pojem v rozhraní příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-112">Pipelines are arguably the most valuable concept used in command-line interfaces.</span></span> <span data-ttu-id="dc0bc-113">Při použití správně, kanály úsilí použití komplexní příkazy a usnadňují naleznete v tématu Postup pro příkazy.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-113">When used properly, pipelines reduce the effort of using complex commands and make it easier to see the flow of work for the commands.</span></span> <span data-ttu-id="dc0bc-114">Každý příkaz v kanálu (označované jako element kanálu) se předá výstup další příkaz v rámci kanálu jednotlivých položkách.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-114">Each command in a pipeline (called a pipeline element) passes its output to the next command in the pipeline, item-by-item.</span></span> <span data-ttu-id="dc0bc-115">Příkazy nemusí zpracovávat více položek najednou.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-115">Commands don't have to handle more than one item at a time.</span></span> <span data-ttu-id="dc0bc-116">Výsledkem je snížení spotřebovaných a možnost začít okamžitě získávání výstupu.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-116">The result is reduced resource consumption and the ability to begin getting the output immediately.</span></span>

<span data-ttu-id="dc0bc-117">Například, pokud použijete `Out-Host` k vynucení stránku po stránce zobrazení výstupu z jiného příkazu, výstup vypadá stejně jako normální text zobrazený na obrazovce, rozdělit do stránky:</span><span class="sxs-lookup"><span data-stu-id="dc0bc-117">For example, if you use the `Out-Host` cmdlet to force a page-by-page display of output from another command, the output looks just like the normal text displayed on the screen, broken up into pages:</span></span>

```powershell
Get-ChildItem -Path C:\WINDOWS\System32 | Out-Host -Paging
```

```Output
    Directory: C:\WINDOWS\system32

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        4/12/2018   2:15 AM                0409
d-----        5/13/2018  11:31 PM                1033
d-----        4/11/2018   4:38 PM                AdvancedInstallers
d-----        5/13/2018  11:13 PM                af-ZA
d-----        5/13/2018  11:13 PM                am-et
d-----        4/11/2018   4:38 PM                AppLocker
d-----        5/13/2018  11:31 PM                appmgmt
d-----        7/11/2018   2:05 AM                appraiser
d---s-        4/12/2018   2:20 AM                AppV
d-----        5/13/2018  11:10 PM                ar-SA
d-----        5/13/2018  11:13 PM                as-IN
d-----        8/14/2018   9:03 PM                az-Latn-AZ
d-----        5/13/2018  11:13 PM                be-BY
d-----        5/13/2018  11:10 PM                BestPractices
d-----        5/13/2018  11:10 PM                bg-BG
d-----        5/13/2018  11:13 PM                bn-BD
d-----        5/13/2018  11:13 PM                bn-IN
d-----        8/14/2018   9:03 PM                Boot
d-----        8/14/2018   9:03 PM                bs-Latn-BA
d-----        4/11/2018   4:38 PM                Bthprops
d-----        4/12/2018   2:19 AM                ca-ES
d-----        8/14/2018   9:03 PM                ca-ES-valencia
d-----        5/13/2018  10:46 PM                CatRoot
d-----        8/23/2018   5:07 PM                catroot2
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="dc0bc-118">Stránkování také snižuje nároky na CPU, protože zpracování přenese `Out-Host` rutiny po dokončení stránky připravený k zobrazení.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-118">Paging also reduces CPU utilization because processing transfers to the `Out-Host` cmdlet when it has a complete page ready to display.</span></span> <span data-ttu-id="dc0bc-119">Rutiny, které jej předcházejí v kanálu pozastavit provádění, dokud nebude k dispozici na další stránku výstup.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-119">The cmdlets that precede it in the pipeline pause execution until the next page of output is available.</span></span>

<span data-ttu-id="dc0bc-120">Uvidíte rozdíl Správce úloh Windows ke sledování procesoru a paměti používá PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-120">You can see the difference Windows Task Manager to monitor CPU and memory used by PowerShell.</span></span> <span data-ttu-id="dc0bc-121">Spusťte následující příkaz: `Get-ChildItem C:\\Windows -Recurse`.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-121">Run the following command: `Get-ChildItem C:\\Windows -Recurse`.</span></span> <span data-ttu-id="dc0bc-122">Porovnání využití procesoru a paměti pro tento příkaz: `Get-ChildItem C:\\Windows -Recurse | Out-Host -Paging`.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-122">Compare the CPU and memory usage to this command: `Get-ChildItem C:\\Windows -Recurse | Out-Host -Paging`.</span></span>

## <a name="objects-in-the-pipeline"></a><span data-ttu-id="dc0bc-123">Objekty v kanálu</span><span class="sxs-lookup"><span data-stu-id="dc0bc-123">Objects in the pipeline</span></span>

<span data-ttu-id="dc0bc-124">Při spuštění rutiny v prostředí PowerShell se zobrazí textový výstup, protože je nezbytná k reprezentaci objektů jako text v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-124">When you run a cmdlet in PowerShell, you see text output because it is necessary to represent objects as text in a console window.</span></span> <span data-ttu-id="dc0bc-125">Textový výstup nemusí být zobrazeny všechny vlastnosti objekt, který je výstup.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-125">The text output may not display all of the properties of the object being output.</span></span>

<span data-ttu-id="dc0bc-126">Představme si třeba, `Get-Location` rutiny.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-126">For example, consider the `Get-Location` cmdlet.</span></span> <span data-ttu-id="dc0bc-127">Pokud spustíte `Get-Location` své aktuální polohy je kořenové jednotce C, zobrazí se následující výstup:</span><span class="sxs-lookup"><span data-stu-id="dc0bc-127">If you run `Get-Location` while your current location is the root of the C drive, you see the following output:</span></span>

```
PS> Get-Location

Path
----
C:\
```

<span data-ttu-id="dc0bc-128">Textový výstup je uveden seznam informací, ne úplnou reprezentaci objekt vrácený rutinou `Get-Location`.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-128">The text output is a summary of information, not a complete representation of the object returned by `Get-Location`.</span></span> <span data-ttu-id="dc0bc-129">Záhlaví ve výstupu se přidal proces, který zformátuje data pro zobrazení na obrazovce.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-129">The heading in the output is added by the process that formats the data for onscreen display.</span></span>

<span data-ttu-id="dc0bc-130">Když přesměrujte výstup do `Get-Member` rutinu můžete získat informace o objekt vrácený rutinou `Get-Location`.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-130">When you pipe the output to the `Get-Member` cmdlet you get information about the object returned by `Get-Location`.</span></span>

```powershell
PS> Get-Location | Get-Member
```

```Output
   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Equals       Method     bool Equals(System.Object obj)
GetHashCode  Method     int GetHashCode()
GetType      Method     type GetType()
ToString     Method     string ToString()
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   string Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {get;}
ProviderPath Property   string ProviderPath {get;}
```

<span data-ttu-id="dc0bc-131">`Get-Location` Vrátí **PathInfo** objekt, který obsahuje aktuální cestě a dalších informací.</span><span class="sxs-lookup"><span data-stu-id="dc0bc-131">`Get-Location` returns a **PathInfo** object that contains the current path and other information.</span></span>

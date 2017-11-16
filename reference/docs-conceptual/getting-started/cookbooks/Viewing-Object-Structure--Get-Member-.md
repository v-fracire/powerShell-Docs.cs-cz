---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Zobrazení objektu struktura Get člena"
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: 618f34bca7bfb76ce5d48ada642a687e279c8aad
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2017
---
# <a name="viewing-object-structure-get-member"></a><span data-ttu-id="f65a3-103">Zobrazení struktury objektu (Get člen)</span><span class="sxs-lookup"><span data-stu-id="f65a3-103">Viewing Object Structure (Get-Member)</span></span>
<span data-ttu-id="f65a3-104">Protože objekty centrální roli hrají v prostředí Windows PowerShell, existuje několik nativní příkazy, které jsou navrženy pro práci s typy libovolného objektu.</span><span class="sxs-lookup"><span data-stu-id="f65a3-104">Because objects play such a central role in Windows PowerShell, there are several native commands designed to work with arbitrary object types.</span></span> <span data-ttu-id="f65a3-105">Je nejdůležitějším **Get-člen** příkaz.</span><span class="sxs-lookup"><span data-stu-id="f65a3-105">The most important one is the **Get-Member** command.</span></span>

<span data-ttu-id="f65a3-106">Nejjednodušším způsobem pro analýzu objekty, které vrátí příkaz je výstup tohoto příkazu **Get-člen** rutiny.</span><span class="sxs-lookup"><span data-stu-id="f65a3-106">The simplest technique for analyzing the objects that a command returns is to pipe the output of that command to the **Get-Member** cmdlet.</span></span> <span data-ttu-id="f65a3-107">**Get-člen** rutiny uvádí formální název tohoto typu objektu a úplný seznam všech jejích členů.</span><span class="sxs-lookup"><span data-stu-id="f65a3-107">The **Get-Member** cmdlet shows you the formal name of the object type and a complete listing of its members.</span></span> <span data-ttu-id="f65a3-108">Počet elementů, které jsou vráceny, v některých případech může být čtenáře.</span><span class="sxs-lookup"><span data-stu-id="f65a3-108">The number of elements that are returned can sometimes be overwhelming.</span></span> <span data-ttu-id="f65a3-109">Například objekt procesu můžete mít více než 100 členy.</span><span class="sxs-lookup"><span data-stu-id="f65a3-109">For example, a process object can have over 100 members.</span></span>

<span data-ttu-id="f65a3-110">Aby se zobrazily všechny členy objekt procesu a stránky výstup, můžete zobrazit všechny, zadejte:</span><span class="sxs-lookup"><span data-stu-id="f65a3-110">To see all the members of a Process object and page the output so you can view all of it, type:</span></span>

```
PS> Get-Process | Get-Member | Out-Host -Paging
```

<span data-ttu-id="f65a3-111">Výstup tohoto příkazu bude vypadat přibližně takto:</span><span class="sxs-lookup"><span data-stu-id="f65a3-111">The output from this command will look something like this:</span></span>

```
TypeName: System.Diagnostics.Process

Name                           MemberType     Definition
----                           ----------     ----------
Handles                        AliasProperty  Handles = Handlecount
Name                           AliasProperty  Name = ProcessName
NPM                            AliasProperty  NPM = NonpagedSystemMemorySize
PM                             AliasProperty  PM = PagedMemorySize
VM                             AliasProperty  VM = VirtualMemorySize
WS                             AliasProperty  WS = WorkingSet
add_Disposed                   Method         System.Void add_Disposed(Event...
...
```

<span data-ttu-id="f65a3-112">Abychom mohli provádět tento dlouhý seznam informace více použitelné pomocí filtrování pro prvky, které chcete v tématu.</span><span class="sxs-lookup"><span data-stu-id="f65a3-112">We can make this long list of information more usable by filtering for elements we want to see.</span></span> <span data-ttu-id="f65a3-113">**Get-člen** příkaz umožňuje zobrazit seznam pouze členové, které jsou vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="f65a3-113">The **Get-Member** command lets you list only members that are properties.</span></span> <span data-ttu-id="f65a3-114">Existuje několik typů vlastností.</span><span class="sxs-lookup"><span data-stu-id="f65a3-114">There are several forms of properties.</span></span> <span data-ttu-id="f65a3-115">Rutiny zobrazuje vlastnosti všech typů jsme nastaveného **Get-člen MemberType** parametr na hodnotu **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="f65a3-115">The cmdlet displays properties of any type if we set the **Get-Member MemberType** parameter to the value **Properties**.</span></span> <span data-ttu-id="f65a3-116">V rozevíracím seznamu je stále velmi dlouhé, ale trochu udržitelnější:</span><span class="sxs-lookup"><span data-stu-id="f65a3-116">The resulting list is still very long, but a bit more manageable:</span></span>

```
PS> Get-Process | Get-Member -MemberType Properties

   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
...
ExitCode                   Property       System.Int32 ExitCode {get;}
...
Handle                     Property       System.IntPtr Handle {get;}
...
CPU                        ScriptProperty System.Object CPU {get=$this.Total...
...
Path                       ScriptProperty System.Object Path {get=$this.Main...
...
```

> [!NOTE]
> <span data-ttu-id="f65a3-117">Povolené hodnoty MemberType jsou AliasProperty, CodeProperty, vlastnost, NoteProperty, ScriptProperty, vlastnosti, PropertySet, metoda, CodeMethod, ScriptMethod, metody, ParameterizedProperty, členů a všechny.</span><span class="sxs-lookup"><span data-stu-id="f65a3-117">The allowed values of MemberType are AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet, and All.</span></span>

<span data-ttu-id="f65a3-118">Nejsou k dispozici více než 60 vlastnosti procesu.</span><span class="sxs-lookup"><span data-stu-id="f65a3-118">There are over 60 properties for a process.</span></span> <span data-ttu-id="f65a3-119">Z důvodu, prostředí Windows PowerShell často zobrazuje, že je jen několik vlastností pro všechny známé objekt, který zobrazuje všechny z nich vytvoří nezvladatelné množství informací.</span><span class="sxs-lookup"><span data-stu-id="f65a3-119">The reason Windows PowerShell often shows only a handful of properties for any well-known object is that showing all of them would produce an unmanageable amount of information.</span></span>

> [!NOTE]
> <span data-ttu-id="f65a3-120">Postupy: zobrazení pomocí informace uložené v souborech XML, které mají názvy končící na typ objektu, který určuje, prostředí Windows PowerShell. format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="f65a3-120">Windows PowerShell determines how to display an object type by using information stored in XML files that have names ending in .format.ps1xml.</span></span> <span data-ttu-id="f65a3-121">Formátování dat pro proces objekty, které jsou objekty .NET System.Diagnostics.Process, je uložen v DotNetTypes.format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="f65a3-121">The formatting data for process objects, which are .NET System.Diagnostics.Process objects, is stored in DotNetTypes.format.ps1xml.</span></span>

<span data-ttu-id="f65a3-122">Pokud potřebujete podívejte se na vlastnosti kromě těch, které ve výchozím nastavení zobrazí prostředí Windows PowerShell, musíte se k formátování výstupní data sami.</span><span class="sxs-lookup"><span data-stu-id="f65a3-122">If you need to look at properties other than those that Windows PowerShell displays by default, you will need to format the output data yourself.</span></span> <span data-ttu-id="f65a3-123">Tento krok můžete provést pomocí rutiny formátu.</span><span class="sxs-lookup"><span data-stu-id="f65a3-123">This can be done by using the format cmdlets.</span></span>


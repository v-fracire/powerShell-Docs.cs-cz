---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Člen Get struktury objekt zobrazení
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: cc93e45e4306b3d623c1d3d1096dd20c1afc59c8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404043"
---
# <a name="viewing-object-structure-get-member"></a><span data-ttu-id="6d10d-103">Zobrazení struktury objektu (Get-Member)</span><span class="sxs-lookup"><span data-stu-id="6d10d-103">Viewing Object Structure (Get-Member)</span></span>

<span data-ttu-id="6d10d-104">Protože objekty hrají hlavní roli ve Windows Powershellu, existuje několik nativních příkazů, které jsou navrženy pro práci s typy libovolného objektu.</span><span class="sxs-lookup"><span data-stu-id="6d10d-104">Because objects play such a central role in Windows PowerShell, there are several native commands designed to work with arbitrary object types.</span></span> <span data-ttu-id="6d10d-105">Nejdůležitějším je **Get-Member** příkazu.</span><span class="sxs-lookup"><span data-stu-id="6d10d-105">The most important one is the **Get-Member** command.</span></span>

<span data-ttu-id="6d10d-106">Nejjednodušší techniku pro analýzu objekty, které příkaz vrátí je do kanálu výstup tohoto příkazu **Get-Member** rutiny.</span><span class="sxs-lookup"><span data-stu-id="6d10d-106">The simplest technique for analyzing the objects that a command returns is to pipe the output of that command to the **Get-Member** cmdlet.</span></span> <span data-ttu-id="6d10d-107">**Get-Member** rutina ukazuje formální název typu objektu a úplný seznam všech jejích členů.</span><span class="sxs-lookup"><span data-stu-id="6d10d-107">The **Get-Member** cmdlet shows you the formal name of the object type and a complete listing of its members.</span></span> <span data-ttu-id="6d10d-108">Počet prvků, které jsou vráceny, které může být někdy náročné.</span><span class="sxs-lookup"><span data-stu-id="6d10d-108">The number of elements that are returned can sometimes be overwhelming.</span></span> <span data-ttu-id="6d10d-109">Například objekt procesu může obsahovat více než 100 členy.</span><span class="sxs-lookup"><span data-stu-id="6d10d-109">For example, a process object can have over 100 members.</span></span>

<span data-ttu-id="6d10d-110">Pokud chcete zobrazit všechny členy objektu Process a stránky výstupu, abyste mohli zobrazit všechno, zadejte:</span><span class="sxs-lookup"><span data-stu-id="6d10d-110">To see all the members of a Process object and page the output so you can view all of it, type:</span></span>

```powershell
Get-Process | Get-Member | Out-Host -Paging
```

<span data-ttu-id="6d10d-111">Výstup tohoto příkazu bude vypadat přibližně takto:</span><span class="sxs-lookup"><span data-stu-id="6d10d-111">The output from this command will look something like this:</span></span>

```output
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

<span data-ttu-id="6d10d-112">Můžeme provádět tento dlouhý seznam informace použitelnější pomocí filtrování pro prvky, které chceme vidět.</span><span class="sxs-lookup"><span data-stu-id="6d10d-112">We can make this long list of information more usable by filtering for elements we want to see.</span></span> <span data-ttu-id="6d10d-113">**Get-Member** příkaz umožňuje zobrazit seznam pouze členů, které jsou vlastnostmi.</span><span class="sxs-lookup"><span data-stu-id="6d10d-113">The **Get-Member** command lets you list only members that are properties.</span></span> <span data-ttu-id="6d10d-114">Existuje několik tvarů vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6d10d-114">There are several forms of properties.</span></span> <span data-ttu-id="6d10d-115">Rutiny zobrazuje vlastnosti libovolného typu, pokud jsme si nastavili **Get-Member MemberType** parametr na hodnotu **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="6d10d-115">The cmdlet displays properties of any type if we set the **Get-Member MemberType** parameter to the value **Properties**.</span></span> <span data-ttu-id="6d10d-116">V rozevíracím seznamu je stále velmi dlouhý, ale o něco lépe zvládnutelné:</span><span class="sxs-lookup"><span data-stu-id="6d10d-116">The resulting list is still very long, but a bit more manageable:</span></span>

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
> <span data-ttu-id="6d10d-117">Povolené hodnoty MemberType jsou AliasProperty, CodeProperty, vlastnost, NoteProperty, ScriptProperty, vlastnosti, PropertySet, metoda, CodeMethod, ScriptMethod, metody, ParameterizedProperty, členů a všechny.</span><span class="sxs-lookup"><span data-stu-id="6d10d-117">The allowed values of MemberType are AliasProperty, CodeProperty, Property, NoteProperty, ScriptProperty, Properties, PropertySet, Method, CodeMethod, ScriptMethod, Methods, ParameterizedProperty, MemberSet, and All.</span></span>

<span data-ttu-id="6d10d-118">Existuje více než 60 vlastnosti pro proces.</span><span class="sxs-lookup"><span data-stu-id="6d10d-118">There are over 60 properties for a process.</span></span> <span data-ttu-id="6d10d-119">Prostředí Windows PowerShell ukazuje, často že pouze několik vlastností pro libovolný objekt dobře známé, zobrazuje všechny z nich je důvod, proč byste mohli vytvořit nezvladatelné množství informací.</span><span class="sxs-lookup"><span data-stu-id="6d10d-119">The reason Windows PowerShell often shows only a handful of properties for any well-known object is that showing all of them would produce an unmanageable amount of information.</span></span>

> [!NOTE]
> <span data-ttu-id="6d10d-120">Určuje způsob zobrazení typ objektu, který s použitím informací uložených v soubory XML, které mají jména končící na prostředí Windows PowerShell. format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="6d10d-120">Windows PowerShell determines how to display an object type by using information stored in XML files that have names ending in .format.ps1xml.</span></span> <span data-ttu-id="6d10d-121">Formátování dat pro proces objekty, které jsou objekty .NET System.Diagnostics.Process, je uložen v DotNetTypes.format.ps1xml.</span><span class="sxs-lookup"><span data-stu-id="6d10d-121">The formatting data for process objects, which are .NET System.Diagnostics.Process objects, is stored in DotNetTypes.format.ps1xml.</span></span>

<span data-ttu-id="6d10d-122">Pokud potřebujete, podívejte se na vlastnosti než ty, které prostředí Windows PowerShell zobrazí ve výchozím nastavení, je potřeba formátovat sami výstupní data.</span><span class="sxs-lookup"><span data-stu-id="6d10d-122">If you need to look at properties other than those that Windows PowerShell displays by default, you will need to format the output data yourself.</span></span> <span data-ttu-id="6d10d-123">To můžete udělat pomocí rutin formátu.</span><span class="sxs-lookup"><span data-stu-id="6d10d-123">This can be done by using the format cmdlets.</span></span>
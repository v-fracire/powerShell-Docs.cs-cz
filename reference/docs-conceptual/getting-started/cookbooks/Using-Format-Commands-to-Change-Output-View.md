---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití formátovacích příkazů ke změně zobrazení výstupů
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 97d3a9e04abb61bb80a0b8c67d9fb9e885a0b91b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="using-format-commands-to-change-output-view"></a><span data-ttu-id="5afa8-103">Použití formátovacích příkazů ke změně zobrazení výstupů</span><span class="sxs-lookup"><span data-stu-id="5afa8-103">Using Format Commands to Change Output View</span></span>

<span data-ttu-id="5afa8-104">Prostředí Windows PowerShell obsahuje sadu rutin, které umožňují řídit vlastnosti, které se zobrazují pro konkrétní objekty.</span><span class="sxs-lookup"><span data-stu-id="5afa8-104">Windows PowerShell has a set of cmdlets that allow you to control which properties are displayed for particular objects.</span></span> <span data-ttu-id="5afa8-105">Názvy všechny rutiny začít s příkazem **formátu**.</span><span class="sxs-lookup"><span data-stu-id="5afa8-105">The names of all the cmdlets begin with the verb **Format**.</span></span> <span data-ttu-id="5afa8-106">Můžete vybrat jednu nebo více vlastností zobrazíte umožňují.</span><span class="sxs-lookup"><span data-stu-id="5afa8-106">They let you select one or more properties to show.</span></span>

<span data-ttu-id="5afa8-107">**Formátu** jsou rutiny **formátu celou**, **Format-List**, **Format-Table**, a **formát vlastních**.</span><span class="sxs-lookup"><span data-stu-id="5afa8-107">The **Format** cmdlets are **Format-Wide**, **Format-List**, **Format-Table**, and **Format-Custom**.</span></span> <span data-ttu-id="5afa8-108">Jsme popíše pouze **formátu celou**, **Format-List**, a **Format-Table** rutiny v této uživatelské příručce.</span><span class="sxs-lookup"><span data-stu-id="5afa8-108">We will only describe the **Format-Wide**, **Format-List**, and **Format-Table** cmdlets in this user's guide.</span></span>

<span data-ttu-id="5afa8-109">Každá rutina formátu má výchozí vlastnosti, které se použijí, pokud nezadáte vlastnosti specifické pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5afa8-109">Each format cmdlet has default properties that will be used if you do not specify specific properties to display.</span></span> <span data-ttu-id="5afa8-110">Každá rutina také používá stejný název parametru, **vlastnost**, chcete-li určit vlastnosti, které chcete zobrazit.</span><span class="sxs-lookup"><span data-stu-id="5afa8-110">Each cmdlet also uses the same parameter name, **Property**, to specify which properties you want to display.</span></span> <span data-ttu-id="5afa8-111">Protože **formátu celou** se zobrazí pouze jednu vlastnost jeho **vlastnost** přebírá parametr pouze jednu hodnotu, ale vlastnost parametry **Format-List** a **Format-Table** přijme seznam názvů vlastností.</span><span class="sxs-lookup"><span data-stu-id="5afa8-111">Because **Format-Wide** only shows a single property, its **Property** parameter only takes a single value, but the property parameters of **Format-List** and **Format-Table** will accept a list of property names.</span></span>

<span data-ttu-id="5afa8-112">Pokud použijete příkaz **Get-Process - powershell název** se dvěma instancemi spuštění prostředí Windows PowerShell získat výstup, který vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="5afa8-112">If you use the command **Get-Process -Name powershell** with two instances of Windows PowerShell running, you get output that looks like this:</span></span>

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

<span data-ttu-id="5afa8-113">Ve zbývající části této části, se podíváme na tom, jak používat **formát** rutiny změnit způsob výstup tohoto příkazu se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="5afa8-113">In the rest of this section, we will explore how to use **Format** cmdlets to change the way the output of this command is displayed.</span></span>

### <a name="using-format-wide-for-single-item-output"></a><span data-ttu-id="5afa8-114">Pomocí formátu celou pro výstup jedné položky</span><span class="sxs-lookup"><span data-stu-id="5afa8-114">Using Format-Wide for Single-Item Output</span></span>

<span data-ttu-id="5afa8-115">**Formátu celou** rutinu, ve výchozím nastavení, zobrazí jenom výchozí vlastnost objektu.</span><span class="sxs-lookup"><span data-stu-id="5afa8-115">The **Format-Wide** cmdlet, by default, displays only the default property of an object.</span></span> <span data-ttu-id="5afa8-116">V jednom sloupci se zobrazují informace související s každého objektu:</span><span class="sxs-lookup"><span data-stu-id="5afa8-116">The information associated with each object is displayed in a single column:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

<span data-ttu-id="5afa8-117">Můžete také určit jiné než výchozí vlastnost:</span><span class="sxs-lookup"><span data-stu-id="5afa8-117">You can also specify a non-default property:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a><span data-ttu-id="5afa8-118">Řízení zobrazení formátu celou se sloupcem</span><span class="sxs-lookup"><span data-stu-id="5afa8-118">Controlling Format-Wide Display with Column</span></span>

<span data-ttu-id="5afa8-119">S **formátu celou** rutiny současně může zobrazit pouze jednu vlastnost.</span><span class="sxs-lookup"><span data-stu-id="5afa8-119">With the **Format-Wide** cmdlet, you can only display a single property at a time.</span></span> <span data-ttu-id="5afa8-120">Díky tomu je užitečné pro zobrazení jednoduchých seznamů, které se zobrazí pouze jeden element na každý řádek.</span><span class="sxs-lookup"><span data-stu-id="5afa8-120">This makes it useful for displaying simple lists that show only one element per line.</span></span> <span data-ttu-id="5afa8-121">Pokud chcete získat jednoduchý seznam, nastavte hodnotu **sloupec** parametr 1 zadáním:</span><span class="sxs-lookup"><span data-stu-id="5afa8-121">To get a simple listing, set the value of the **Column** parameter to 1 by typing:</span></span>

```powershell
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a><span data-ttu-id="5afa8-122">Použití Format-List pro zobrazení seznamu</span><span class="sxs-lookup"><span data-stu-id="5afa8-122">Using Format-List for a List View</span></span>

<span data-ttu-id="5afa8-123">**Format-List** rutina zobrazí objekt ve formátu v seznamu, s každou vlastnost s názvem bez přípony a zobrazují na samostatném řádku:</span><span class="sxs-lookup"><span data-stu-id="5afa8-123">The **Format-List** cmdlet displays an object in the form of a listing, with each property labeled and displayed on a separate line:</span></span>

```
PS> Get-Process -Name powershell | Format-List

Id      : 2760
Handles : 1242
CPU     : 3.03125
Name    : powershell

Id      : 3448
Handles : 328
CPU     : 1.0625
Name    : powershell
```

<span data-ttu-id="5afa8-124">Můžete zadat libovolný počet vlastnosti tak, jak chcete:</span><span class="sxs-lookup"><span data-stu-id="5afa8-124">You can specify as many properties as you want:</span></span>

```
PS> Get-Process -Name powershell | Format-List -Property ProcessName,FileVersion
,StartTime,Id

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:42:00
Id          : 2760

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:54:28
Id          : 3448
```

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a><span data-ttu-id="5afa8-125">Získávání podrobné informace pomocí seznamu formát se zástupnými znaky</span><span class="sxs-lookup"><span data-stu-id="5afa8-125">Getting Detailed Information by Using Format-List with Wildcards</span></span>

<span data-ttu-id="5afa8-126">**Format-List** rutina umožňuje použít zástupný znak jako hodnota jeho **vlastnost** parametr.</span><span class="sxs-lookup"><span data-stu-id="5afa8-126">The **Format-List** cmdlet lets you use a wildcard as the value of its **Property** parameter.</span></span> <span data-ttu-id="5afa8-127">Díky tomu můžete zobrazit podrobné informace.</span><span class="sxs-lookup"><span data-stu-id="5afa8-127">This lets you display detailed information.</span></span> <span data-ttu-id="5afa8-128">Často objekty zahrnují více informací, než budete potřebovat, proto prostředí Windows PowerShell nezobrazuje ve výchozím nastavení všechny hodnoty vlastností.</span><span class="sxs-lookup"><span data-stu-id="5afa8-128">Often, objects include more information than you need, which is why Windows PowerShell does not show all property values by default.</span></span> <span data-ttu-id="5afa8-129">Chcete-li zobrazit všechny vlastnosti objektu, použijte **Format-List-vlastnost \&#42;** příkaz.</span><span class="sxs-lookup"><span data-stu-id="5afa8-129">To show all of properties of an object, use the **Format-List -Property \&#42;** command.</span></span> <span data-ttu-id="5afa8-130">Následující příkaz se vytvoří víc než 60 řádky výstupu pro jeden procesu:</span><span class="sxs-lookup"><span data-stu-id="5afa8-130">The following command generates over 60 lines of output for a single process:</span></span>

```powershell
Get-Process -Name powershell | Format-List -Property *
```

<span data-ttu-id="5afa8-131">I když **Format-List** příkaz je užitečný pro zobrazení podrobností, pokud chcete přehled výstupu, který obsahuje mnoho položek, jednodušší tabulkové zobrazení je často užitečné.</span><span class="sxs-lookup"><span data-stu-id="5afa8-131">Although the **Format-List** command is useful for showing detail, if you want an overview of output that includes many items, a simpler tabular view is often more useful.</span></span>

### <a name="using-format-table-for-tabular-output"></a><span data-ttu-id="5afa8-132">Použití formátu tabulky pro tabulkový výstup</span><span class="sxs-lookup"><span data-stu-id="5afa8-132">Using Format-Table for Tabular Output</span></span>

<span data-ttu-id="5afa8-133">Pokud použijete **Format-Table** rutiny s žádné názvy vlastností zadaný k formátování výstupu z **Get-Process** příkazu, získáte stejně výstup jako bez žádné formátování.</span><span class="sxs-lookup"><span data-stu-id="5afa8-133">If you use the **Format-Table** cmdlet with no property names specified to format the output of the **Get-Process** command, you get exactly the same output as you do without performing any formatting.</span></span> <span data-ttu-id="5afa8-134">Důvodem je, že procesy se obvykle zobrazují v tabulkovém formátu, jsou většinu objektů prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5afa8-134">The reason is that processes are usually displayed in a tabular format, as are most Windows PowerShell objects.</span></span>

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a><span data-ttu-id="5afa8-135">Vylepšení výstup Format-Table (AutoSize)</span><span class="sxs-lookup"><span data-stu-id="5afa8-135">Improving Format-Table Output (AutoSize)</span></span>

<span data-ttu-id="5afa8-136">I když tabulkové zobrazení je užitečná pro zobrazení spousty porovnatelný z hlediska informací, může být obtížné vysvětlit, pokud je příliš úzké pro data zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5afa8-136">Although a tabular view is useful for displaying a lot of comparable information, it may be difficult to interpret if the display is too narrow for the data.</span></span> <span data-ttu-id="5afa8-137">Například pokud se pokusíte zobrazit cesta procesu, ID, názvu a společnosti, zobrazí se zkrácený výstup pro cestu proces a ve sloupci společnosti:</span><span class="sxs-lookup"><span data-stu-id="5afa8-137">For example, if you try to display process path, ID, name, and company, you get truncated output for the process path and the company column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

<span data-ttu-id="5afa8-138">Pokud zadáte **AutoSize** parametr při spuštění **Format-Table** příkazu prostředí Windows PowerShell se vypočítat šířku sloupců, které jsou založené na skutečná data chcete zobrazit.</span><span class="sxs-lookup"><span data-stu-id="5afa8-138">If you specify the **AutoSize** parameter when you run the **Format-Table** command, Windows PowerShell will calculate column widths based on the actual data you are going to display.</span></span> <span data-ttu-id="5afa8-139">Díky tomu **cesta** sloupec čitelný, ale sloupec společnosti zůstává zkrácený:</span><span class="sxs-lookup"><span data-stu-id="5afa8-139">This makes the **Path** column readable, but the company column remains truncated:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

<span data-ttu-id="5afa8-140">**Format-Table** rutiny může stále zkrátit data, ale ho bude tak učinit pouze na konci části obrazovky.</span><span class="sxs-lookup"><span data-stu-id="5afa8-140">The **Format-Table** cmdlet might still truncate data, but it will only do so at the end of the screen.</span></span> <span data-ttu-id="5afa8-141">Vlastnosti, než byl naposledy zobrazí, mají stejnou velikost jako potřebují pro jejich nejdelší datový prvek ke správnému zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5afa8-141">Properties, other than the last one displayed, are given as much size as they need for their longest data element to display correctly.</span></span> <span data-ttu-id="5afa8-142">Uvidíte, že název společnosti je viditelná, ale cesta je oříznuta, pokud Prohodit umístění **cesta** a **společnosti** v **vlastnost** seznam hodnot:</span><span class="sxs-lookup"><span data-stu-id="5afa8-142">You can see that company name is visible but path is truncated if you swap the locations of **Path** and **Company** in the **Property** value list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

<span data-ttu-id="5afa8-143">**Format-Table** příkaz předpokládá, že nearer vlastnost je na začátek seznamu vlastností je více důležité.</span><span class="sxs-lookup"><span data-stu-id="5afa8-143">The **Format-Table** command assumes that the nearer a property is to the beginning of the property list, the more important it is.</span></span> <span data-ttu-id="5afa8-144">Pokusí se zobrazí vlastnosti nejbližší začátku úplně.</span><span class="sxs-lookup"><span data-stu-id="5afa8-144">So it attempts to display the properties nearest the beginning completely.</span></span> <span data-ttu-id="5afa8-145">Pokud **Format-Table** příkaz nelze zobrazit všechny vlastnosti, bude ze zobrazení odeberte některé sloupce a zobrazit upozornění.</span><span class="sxs-lookup"><span data-stu-id="5afa8-145">If the **Format-Table** command cannot display all the properties, it will remove some columns from the display and provide a warning.</span></span> <span data-ttu-id="5afa8-146">Toto chování můžete zobrazit, jestliže provedete **název** vlastnost poslední v seznamu:</span><span class="sxs-lookup"><span data-stu-id="5afa8-146">You can see this behavior if you make **Name** the last property in the list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

<span data-ttu-id="5afa8-147">Ve výstupu výše sloupec ID zkrácen lze přizpůsobit do seznam a záhlaví sloupců jsou skládaný.</span><span class="sxs-lookup"><span data-stu-id="5afa8-147">In the output above, the ID column is truncated to make it fit into the listing, and the column headings are stacked up.</span></span> <span data-ttu-id="5afa8-148">Automatická změna velikosti sloupců vždy neprovádí co chcete použít.</span><span class="sxs-lookup"><span data-stu-id="5afa8-148">Automatically resizing the columns does not always do what you want.</span></span>

#### <a name="wrapping-format-table-output-in-columns-wrap"></a><span data-ttu-id="5afa8-149">Výstupní formát tabulky zabalení ve sloupcích (zkrácení)</span><span class="sxs-lookup"><span data-stu-id="5afa8-149">Wrapping Format-Table Output in Columns (Wrap)</span></span>

<span data-ttu-id="5afa8-150">Můžete vynutit zdlouhavé **Format-Table** data v rámci jeho sloupec zobrazení zabalit pomocí **zabalení** parametr.</span><span class="sxs-lookup"><span data-stu-id="5afa8-150">You can force lengthy **Format-Table** data to wrap within its display column by using the **Wrap** parameter.</span></span> <span data-ttu-id="5afa8-151">Pomocí **zabalení** parametr samostatně nebude provádět nutně očekávat, protože používá výchozí nastavení, pokud taky nezadáte **AutoSize**:</span><span class="sxs-lookup"><span data-stu-id="5afa8-151">Using the **Wrap** parameter alone will not necessarily do what you expect, since it uses default settings if you do not also specify **AutoSize**:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

<span data-ttu-id="5afa8-152">Výhodou **zabalení** parametr sám o sobě je, že ho nedošlo ke zpomalení zpracování velmi velká.</span><span class="sxs-lookup"><span data-stu-id="5afa8-152">An advantage of using the **Wrap** parameter by itself is that it does not slow down processing very much.</span></span> <span data-ttu-id="5afa8-153">Pokud provádíte rekurzivní souboru výpis velkého adresáře systému, může být časově velmi náročná a použít velké množství paměti, než se zobrazí první položky výstupu, pokud používáte **AutoSize**.</span><span class="sxs-lookup"><span data-stu-id="5afa8-153">If you perform a recursive file listing of a large directory system, it might take a very long time and use a lot of memory before displaying the first output items if you use **AutoSize**.</span></span>

<span data-ttu-id="5afa8-154">Pokud si nejste zajímá zatížení systému, potom **AutoSize** dobře funguje s **zabalení** parametr.</span><span class="sxs-lookup"><span data-stu-id="5afa8-154">If you are not concerned about system load, then **AutoSize** works well with the **Wrap** parameter.</span></span> <span data-ttu-id="5afa8-155">Počáteční sloupce jsou vždy vyhrazených tolik šířka podle potřeby k zobrazení položek na jeden řádek, stejně jako při zadání **AutoSize** bez **zabalení** parametr.</span><span class="sxs-lookup"><span data-stu-id="5afa8-155">The initial columns are always allotted as much width as they need to display items on one line, just as when you specify **AutoSize** without the **Wrap** parameter.</span></span> <span data-ttu-id="5afa8-156">Jediným rozdílem je, že bude zalomit posledního sloupce v případě potřeby:</span><span class="sxs-lookup"><span data-stu-id="5afa8-156">The only difference is that the final column will be wrapped if necessary:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

<span data-ttu-id="5afa8-157">Některé sloupce nemusí zobrazit, pokud nejprve zadejte nejširší sloupce, proto je nejbezpečnější nejprve vybrat nejmenší datové prvky.</span><span class="sxs-lookup"><span data-stu-id="5afa8-157">Some columns might not be displayed if you specify the widest columns first, so it is safest to specify the smallest data elements first.</span></span> <span data-ttu-id="5afa8-158">V následujícím příkladu určíme element velmi široké cesty nejprve a i obtékané jsme konečné stále ztratit **název** sloupce:</span><span class="sxs-lookup"><span data-stu-id="5afa8-158">In the following example, we specify the extremely wide path element first, and even with wrapping, we still lose the final **Name** column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a><span data-ttu-id="5afa8-159">Uspořádání výstupní tabulky (-GroupBy)</span><span class="sxs-lookup"><span data-stu-id="5afa8-159">Organizing Table Output (-GroupBy)</span></span>

<span data-ttu-id="5afa8-160">Další užitečné parametr pro ovládací prvek Tabulkový výstup **GroupBy**.</span><span class="sxs-lookup"><span data-stu-id="5afa8-160">Another useful parameter for tabular output control is **GroupBy**.</span></span> <span data-ttu-id="5afa8-161">Již tabulkové výpisech zejména může být obtížné porovnat.</span><span class="sxs-lookup"><span data-stu-id="5afa8-161">Longer tabular listings in particular may be hard to compare.</span></span> <span data-ttu-id="5afa8-162">**GroupBy** parametr skupin výstup v závislosti na hodnotu vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="5afa8-162">The **GroupBy** parameter groups output based on a property value.</span></span> <span data-ttu-id="5afa8-163">Například můžeme můžete seskupit procesy ve společnosti pro snazší kontroly vynechání společnosti hodnotu ze seznamu vlastností:</span><span class="sxs-lookup"><span data-stu-id="5afa8-163">For example, we can group processes by company for easier inspection, omitting the company value from the property listing:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```
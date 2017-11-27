---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Práce se složkami soubory a klíče registru"
ms.assetid: e6cf87aa-b5f8-48d5-a75a-7cb7ecb482dc
ms.openlocfilehash: 22a2390686659033bfd8b02a151b3397cfd46a22
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="working-with-files-folders-and-registry-keys"></a><span data-ttu-id="344fa-103">Práce se soubory, složky a klíče registru</span><span class="sxs-lookup"><span data-stu-id="344fa-103">Working With Files, Folders and Registry Keys</span></span>
<span data-ttu-id="344fa-104">Prostředí Windows PowerShell používá podstatným jménem **položky** odkazovat na položky najít na jednotku prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="344fa-104">Windows PowerShell uses the noun **Item** to refer to items found on a Windows PowerShell drive.</span></span> <span data-ttu-id="344fa-105">Při plánování práce s poskytovateli Windows PowerShell FileSystem **položky** může být soubor, složku nebo jednotku prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="344fa-105">When dealing with the Windows PowerShell FileSystem provider, an **Item** might be a file, a folder, or the Windows PowerShell drive.</span></span> <span data-ttu-id="344fa-106">Výpis a práci s těmito položkami je důležité základní úloha v většinu nastavení pro správu, tak chceme tyto úlohy podrobně popisují.</span><span class="sxs-lookup"><span data-stu-id="344fa-106">Listing and working with these items is a critical basic task in most administrative settings, so we want to discuss these tasks in detail.</span></span>

### <a name="enumerating-files-folders-and-registry-keys-get-childitem"></a><span data-ttu-id="344fa-107">Vytváření výčtu souborů, složek a klíčů registru (Get-ChildItem)</span><span class="sxs-lookup"><span data-stu-id="344fa-107">Enumerating Files, Folders, and Registry Keys (Get-ChildItem)</span></span>
<span data-ttu-id="344fa-108">Vzhledem k tomu, že získání kolekce položek z konkrétního umístění, je takový běžné úlohy, **Get-ChildItem** rutiny je navrženo konkrétně k vrátí všechny položky v rámci kontejneru, například do složky nalezen.</span><span class="sxs-lookup"><span data-stu-id="344fa-108">Since getting a collection of items from a particular location is such a common task, the **Get-ChildItem** cmdlet is designed specifically to return all items found within a container such as a folder.</span></span>

<span data-ttu-id="344fa-109">Pokud chcete vrátit všechny soubory a složky, které jsou obsažena přímo ve složce C:\\Windows, zadejte:</span><span class="sxs-lookup"><span data-stu-id="344fa-109">If you want to return all files and folders that are contained directly within the folder C:\\Windows, type:</span></span>

```
PS> Get-ChildItem -Path C:\Windows
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-16   8:10 AM          0 0.log
-a---        2005-11-29   3:16 PM         97 acc1.txt
-a---        2005-10-23  11:21 PM       3848 actsetup.log
...
```

<span data-ttu-id="344fa-110">Seznam bude vypadat podobně jako co uvidí, když zadáte **dir** v **Cmd.exe**, nebo **ls** příkazu v příkazovém prostředí UNIX.</span><span class="sxs-lookup"><span data-stu-id="344fa-110">The listing looks similar to what you would see when you enter the **dir** command in **Cmd.exe**, or the **ls** command in a UNIX command shell.</span></span>

<span data-ttu-id="344fa-111">Velmi složité výpisech můžete provádět pomocí parametrů **Get-ChildItem** rutiny.</span><span class="sxs-lookup"><span data-stu-id="344fa-111">You can perform very complex listings by using parameters of the **Get-ChildItem** cmdlet.</span></span> <span data-ttu-id="344fa-112">Podíváme se na několik scénářů Další.</span><span class="sxs-lookup"><span data-stu-id="344fa-112">We will look at a few scenarios next.</span></span> <span data-ttu-id="344fa-113">Zobrazí se syntaxe **Get-ChildItem** rutiny zadáním:</span><span class="sxs-lookup"><span data-stu-id="344fa-113">You can see the syntax the **Get-ChildItem** cmdlet by typing:</span></span>

```
PS> Get-Command -Name Get-ChildItem -Syntax
```

<span data-ttu-id="344fa-114">Tyto parametry můžete ve smíšeném a namapovat na získat vysoce přizpůsobenou výstup.</span><span class="sxs-lookup"><span data-stu-id="344fa-114">These parameters can be mixed and matched to get highly customized output.</span></span>

#### <a name="listing-all-contained-items--recurse"></a><span data-ttu-id="344fa-115">Výpis všech obsažených položek (-Recurse)</span><span class="sxs-lookup"><span data-stu-id="344fa-115">Listing all Contained Items (-Recurse)</span></span>
<span data-ttu-id="344fa-116">Pokud chcete zobrazit položky ve složce Windows a všechny položky, které jsou obsaženy v rámci podsložky, použijte **Recurse** parametr **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="344fa-116">To see both the items inside a Windows folder and any items that are contained within the subfolders, use the **Recurse** parameter of **Get-ChildItem**.</span></span> <span data-ttu-id="344fa-117">Seznam všechno, co zobrazí ve složce Windows a položek v jejích podsložkách.</span><span class="sxs-lookup"><span data-stu-id="344fa-117">The listing displays everything within the Windows folder and the items in its subfolders.</span></span> <span data-ttu-id="344fa-118">Příklad:</span><span class="sxs-lookup"><span data-stu-id="344fa-118">For example:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS -Recurse

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\WINDOWS\AppPatch
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM    1852416 AcGenral.dll
...
```

#### <a name="filtering-items-by-name--name"></a><span data-ttu-id="344fa-119">Filtrování položek podle názvu (-název)</span><span class="sxs-lookup"><span data-stu-id="344fa-119">Filtering Items by Name (-Name)</span></span>
<span data-ttu-id="344fa-120">Chcete-li zobrazit pouze názvy položek, použijte **název** parametr **Get-Childitem**:</span><span class="sxs-lookup"><span data-stu-id="344fa-120">To display only the names of items, use the **Name** parameter of **Get-Childitem**:</span></span>

```
PS> Get-ChildItem -Path C:\WINDOWS -Name
addins
AppPatch
assembly
...
```

#### <a name="forcibly-listing-hidden-items--force"></a><span data-ttu-id="344fa-121">Vynuceně seznam skrytých položky (-Force)</span><span class="sxs-lookup"><span data-stu-id="344fa-121">Forcibly Listing Hidden Items (-Force)</span></span>
<span data-ttu-id="344fa-122">Položky, které jsou obvykle neviditelná v Průzkumníkovi souborů nebo Cmd.exe nejsou zobrazeny ve výstupu **Get-ChildItem** příkaz.</span><span class="sxs-lookup"><span data-stu-id="344fa-122">Items that are normally invisible in File Explorer or Cmd.exe are not displayed in the output of a **Get-ChildItem** command.</span></span> <span data-ttu-id="344fa-123">Chcete-li zobrazit skryté položky, použijte **Force** parametr **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="344fa-123">To display hidden items, use the **Force** parameter of **Get-ChildItem**.</span></span> <span data-ttu-id="344fa-124">Příklad:</span><span class="sxs-lookup"><span data-stu-id="344fa-124">For example:</span></span>

```
Get-ChildItem -Path C:\Windows -Force
```

<span data-ttu-id="344fa-125">Tento parametr je s názvem Force, protože normální chování můžete přepsat vynuceně **Get-ChildItem** příkaz.</span><span class="sxs-lookup"><span data-stu-id="344fa-125">This parameter is named Force because you can forcibly override the normal behavior of the **Get-ChildItem** command.</span></span> <span data-ttu-id="344fa-126">Platnost je často používaný parametr, který vynutí akci, která rutina nebude fungovat normálně, i když ho nebude provádět žádnou akci, která ohrožuje zabezpečení systému.</span><span class="sxs-lookup"><span data-stu-id="344fa-126">Force is a widely used parameter that forces an action that a cmdlet would not normally perform, although it will not perform any action that compromises the security of the system.</span></span>

#### <a name="matching-item-names-with-wildcards"></a><span data-ttu-id="344fa-127">Odpovídající názvy položek se zástupnými znaky</span><span class="sxs-lookup"><span data-stu-id="344fa-127">Matching Item Names with Wildcards</span></span>
<span data-ttu-id="344fa-128">**Get-ChildItem** příkaz přijímá zástupné znaky v cestě položky k zobrazení seznamu.</span><span class="sxs-lookup"><span data-stu-id="344fa-128">**The Get-ChildItem** command accepts wildcards in the path of the items to list.</span></span>

<span data-ttu-id="344fa-129">Vzhledem k porovnávání se zástupnými znaky se zpracovává souborem modul prostředí Windows PowerShell, všechny rutiny, které přijímá zástupné znaky použít stejný zápis a mít stejné odpovídající chování.</span><span class="sxs-lookup"><span data-stu-id="344fa-129">Because wildcard matching is handled by the Windows PowerShell engine, all cmdlets that accepts wildcards use the same notation and have the same matching behavior.</span></span> <span data-ttu-id="344fa-130">Zápis zástupný znak prostředí Windows PowerShell obsahuje:</span><span class="sxs-lookup"><span data-stu-id="344fa-130">The Windows PowerShell wildcard notation includes:</span></span>

- <span data-ttu-id="344fa-131">Znak hvězdičky (\*) odpovídá počtu nula či více výskytů libovolného znaku.</span><span class="sxs-lookup"><span data-stu-id="344fa-131">Asterisk (\*)matches zero or more occurrences of any character.</span></span>

- <span data-ttu-id="344fa-132">Otazník (?) odpovídá přesně jeden znak.</span><span class="sxs-lookup"><span data-stu-id="344fa-132">Question mark (?) matches exactly one character.</span></span>

- <span data-ttu-id="344fa-133">Levé závorky (\[) znak a znak pravé závorky (]), uzavřete sadu znaků lze porovnat.</span><span class="sxs-lookup"><span data-stu-id="344fa-133">Left bracket (\[) character and right bracket (]) character surround a set of characters to be matched.</span></span>

<span data-ttu-id="344fa-134">Zde jsou některé příklady, jak funguje specifikace zástupný znak.</span><span class="sxs-lookup"><span data-stu-id="344fa-134">Here are some examples of how wildcard specification works.</span></span>

<span data-ttu-id="344fa-135">Chcete-li vyhledat všechny soubory v adresáři systému Windows s příponou **.log** a přesně 5 znaků v základním názvem, zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="344fa-135">To find all files in the Windows directory with the suffix **.log** and exactly five characters in the base name, enter the following command:</span></span>

```
PS> Get-ChildItem -Path C:\Windows\?????.log
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
...
-a---        2006-05-11   6:31 PM     204276 ocgen.log
-a---        2006-05-11   6:31 PM      22365 ocmsn.log
...
-a---        2005-11-11   4:55 AM         64 setup.log
-a---        2005-12-15   2:24 PM      17719 VxSDM.log
...
```

<span data-ttu-id="344fa-136">Najít všechny soubory, které začínají písmenem **x** v adresáři systému Windows, zadejte:</span><span class="sxs-lookup"><span data-stu-id="344fa-136">To find all files that begin with the letter **x** in the Windows directory, type:</span></span>

```
Get-ChildItem -Path C:\Windows\x*
```

<span data-ttu-id="344fa-137">Chcete-li vyhledat všechny soubory, jejichž názvy začínají řetězcem **x** nebo **z**, zadejte:</span><span class="sxs-lookup"><span data-stu-id="344fa-137">To find all files whose names begin with **x** or **z**, type:</span></span>

```
Get-ChildItem -Path C:\Windows\[xz]*
```

#### <a name="excluding-items--exclude"></a><span data-ttu-id="344fa-138">Vyloučení položek (-vyloučení)</span><span class="sxs-lookup"><span data-stu-id="344fa-138">Excluding Items (-Exclude)</span></span>
<span data-ttu-id="344fa-139">Můžete vyloučit konkrétní položky pomocí **vyloučit** parametr Get-ChildItem.</span><span class="sxs-lookup"><span data-stu-id="344fa-139">You can exclude specific items by using the **Exclude** parameter of Get-ChildItem.</span></span> <span data-ttu-id="344fa-140">To umožňuje provádět komplexní filtrování v jediném příkazu.</span><span class="sxs-lookup"><span data-stu-id="344fa-140">This lets you perform complex filtering in a single statement.</span></span>

<span data-ttu-id="344fa-141">Předpokládejme například chcete najít knihovnu DLL čas služby systému Windows ve složce System32, a všechny, které si pamatujete týkající se názvu DLL je, že začíná "W" a "32" je v ní.</span><span class="sxs-lookup"><span data-stu-id="344fa-141">For example, suppose you are trying to find the Windows Time Service DLL in the System32 folder, and all you can remember about the DLL name is that it begins with "W" and has "32" in it.</span></span>

<span data-ttu-id="344fa-142">Výraz jako **w\&#42; 32\&#42;. knihovny DLL** najdete všechny knihovny DLL, které splňují podmínky, ale také může vrátit systém Windows 95 a Windows kompatibility 16bitové knihovny DLL, které zahrnují "95" nebo "16" v jejich názvy.</span><span class="sxs-lookup"><span data-stu-id="344fa-142">An expression like **w\&#42;32\&#42;.dll** will find all DLLs that satisfy the conditions, but it may also return the Windows 95 and 16-bit Windows compatibility DLLs that include "95" or "16" in their names.</span></span> <span data-ttu-id="344fa-143">Je možné vynechat soubory, které mají některou z těchto čísla v jejich názvy pomocí **vyloučit** parametr se vzorkem  **\&#42;\[ 9516]\&#42;**:</span><span class="sxs-lookup"><span data-stu-id="344fa-143">You can omit files that have any of these numbers in their names by using the **Exclude** parameter with the pattern **\&#42;\[9516]\&#42;**:</span></span>

<pre>PS> Get-ChildItem -Path C:\WINDOWS\System32\w*32*.dll -Exclude *[9516]*
Directory: Microsoft.PowerShell.Core\FileSystem::C:\WINDOWS\System32
Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     174592 w32time.dll
-a---        2004-08-04   8:00 AM      22016 w32topl.dll
-a---        2004-08-04   8:00 AM     101888 win32spl.dll
-a---        2004-08-04   8:00 AM     172032 wldap32.dll
-a---        2004-08-04   8:00 AM     264192 wow32.dll
-a---        2004-08-04   8:00 AM      82944 ws2_32.dll
-a---        2004-08-04   8:00 AM      42496 wsnmp32.dll
-a---        2004-08-04   8:00 AM      22528 wsock32.dll
-a---        2004-08-04   8:00 AM      18432 wtsapi32.dll</pre>

#### <a name="mixing-get-childitem-parameters"></a><span data-ttu-id="344fa-144">Kombinování parametry Get-ChildItem</span><span class="sxs-lookup"><span data-stu-id="344fa-144">Mixing Get-ChildItem Parameters</span></span>
<span data-ttu-id="344fa-145">Můžete použít několik parametrů **Get-ChildItem** rutiny v jednom příkazu.</span><span class="sxs-lookup"><span data-stu-id="344fa-145">You can use several of the parameters of the **Get-ChildItem** cmdlet in the same command.</span></span> <span data-ttu-id="344fa-146">Předtím, než můžete kombinovat parametry, ujistěte se, že rozumíte porovnávání se zástupnými znaky.</span><span class="sxs-lookup"><span data-stu-id="344fa-146">Before you mix parameters, be sure that you understand wildcard matching.</span></span> <span data-ttu-id="344fa-147">Například následující příkaz vrátí žádné výsledky:</span><span class="sxs-lookup"><span data-stu-id="344fa-147">For example, the following command returns no results:</span></span>

```
PS> Get-ChildItem -Path C:\Windows\*.dll -Recurse -Exclude [a-y]*.dll
```

<span data-ttu-id="344fa-148">Nebyly nalezeny žádné výsledky, i když se dvě knihovny DLL, která začínají znakem "z" ve složce Windows.</span><span class="sxs-lookup"><span data-stu-id="344fa-148">There are no results, even though there are two DLLs that begin with the letter "z" in the Windows folder.</span></span>

<span data-ttu-id="344fa-149">Nebyly vráceny žádné výsledky, protože jsme zadali zástupného jako část této cesty.</span><span class="sxs-lookup"><span data-stu-id="344fa-149">No results were returned because we specified the wildcard as part of the path.</span></span> <span data-ttu-id="344fa-150">I když příkaz byl rekurzivní, **Get-ChildItem** rutiny omezený položky na ty, které se nacházejí ve složce Windows s názvy konče ".dll".</span><span class="sxs-lookup"><span data-stu-id="344fa-150">Even though the command was recursive, the **Get-ChildItem** cmdlet restricted the items to those that are in the Windows folder with names ending with ".dll".</span></span>

<span data-ttu-id="344fa-151">Pokud chcete zadat rekurzivní hledání pro soubory, jejichž názvy odpovídají speciální vzorku, použijte **-zahrnují** parametr.</span><span class="sxs-lookup"><span data-stu-id="344fa-151">To specify a recursive search for files whose names match a special pattern, use the **-Include** parameter.</span></span>

```
PS> Get-ChildItem -Path C:\Windows -Include *.dll -Recurse -Exclude [a-y]*.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32\Setup

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM       8261 zoneoc.dll

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\Windows\System32

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2004-08-04   8:00 AM     337920 zipfldr.dll
```


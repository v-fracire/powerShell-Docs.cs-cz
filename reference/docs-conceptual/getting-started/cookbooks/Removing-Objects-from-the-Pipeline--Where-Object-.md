---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Odebírání objektů z kanálu kde objektu
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: 46f210e1418098f4809174cd975ab8d783580285
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753834"
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="6f68f-103">Odebírání objektů z kanálu (Where-Object)</span><span class="sxs-lookup"><span data-stu-id="6f68f-103">Removing Objects from the Pipeline (Where-Object)</span></span>

<span data-ttu-id="6f68f-104">V prostředí Windows PowerShell často generovat a další objekty předají pro kanál, než má.</span><span class="sxs-lookup"><span data-stu-id="6f68f-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="6f68f-105">Můžete zadat vlastnosti konkrétní objekty, které chcete zobrazit pomocí **formát** rutiny, ale nepomůže s problémem odebrání celé objekty ze zobrazení.</span><span class="sxs-lookup"><span data-stu-id="6f68f-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="6f68f-106">Můžete filtrovat objekty před koncem kanálu, tak můžete provádět akce na pouze podmnožinu objektů původně vytvořil.</span><span class="sxs-lookup"><span data-stu-id="6f68f-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="6f68f-107">Prostředí Windows PowerShell zahrnuje `Where-Object` rutinu, která umožňuje testování jednotlivých objektů v kanálu a pouze předat podél kanálu pokud splňuje podmínku konkrétní test.</span><span class="sxs-lookup"><span data-stu-id="6f68f-107">Windows PowerShell includes a `Where-Object` cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="6f68f-108">Objekty, které se nepředají test se odeberou z kanálu.</span><span class="sxs-lookup"><span data-stu-id="6f68f-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="6f68f-109">Zadejte podmínky testu jako hodnota `Where-Object` **FilterScript** parametr.</span><span class="sxs-lookup"><span data-stu-id="6f68f-109">You supply the test condition as the value of the `Where-Object` **FilterScript** parameter.</span></span>

### <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="6f68f-110">Provádění jednoduchých testů s Where-Object</span><span class="sxs-lookup"><span data-stu-id="6f68f-110">Performing Simple Tests with Where-Object</span></span>

<span data-ttu-id="6f68f-111">Hodnota **FilterScript** je *bloku skriptu* – jeden nebo více příkazů prostředí Windows PowerShell, které jsou v závorkách {} – který se vyhodnotí na true nebo false.</span><span class="sxs-lookup"><span data-stu-id="6f68f-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="6f68f-112">Tyto bloky skriptu může být velmi jednoduchý, ale jejich vytváření vyžaduje znalost o jiný koncept prostředí Windows PowerShell, operátory porovnání.</span><span class="sxs-lookup"><span data-stu-id="6f68f-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="6f68f-113">Relační operátor porovnání položek, které se zobrazí na každé straně ho.</span><span class="sxs-lookup"><span data-stu-id="6f68f-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="6f68f-114">Operátory porovnání začínat '-' znak a jsou následuje název.</span><span class="sxs-lookup"><span data-stu-id="6f68f-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="6f68f-115">Operátory porovnání základní fungovat na téměř k libovolnému druhu objektu.</span><span class="sxs-lookup"><span data-stu-id="6f68f-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="6f68f-116">Pokročilejší operátory porovnání může fungovat jenom na text nebo pole.</span><span class="sxs-lookup"><span data-stu-id="6f68f-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="6f68f-117">Operátory porovnání prostředí Windows PowerShell jsou ve výchozím nastavení se při práci s textem velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="6f68f-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="6f68f-118">Z důvodu analýzy aspekty symboly, například <>, a = nejsou používány jako relační operátory.</span><span class="sxs-lookup"><span data-stu-id="6f68f-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="6f68f-119">Operátory porovnání místo toho se skládají z písmena.</span><span class="sxs-lookup"><span data-stu-id="6f68f-119">Instead, comparison operators are comprised of letters.</span></span> <span data-ttu-id="6f68f-120">V následující tabulce jsou uvedeny základní relační operátory.</span><span class="sxs-lookup"><span data-stu-id="6f68f-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="6f68f-121">Relační operátor</span><span class="sxs-lookup"><span data-stu-id="6f68f-121">Comparison Operator</span></span>|<span data-ttu-id="6f68f-122">Význam</span><span class="sxs-lookup"><span data-stu-id="6f68f-122">Meaning</span></span>|<span data-ttu-id="6f68f-123">Příklad (vrací hodnotu true)</span><span class="sxs-lookup"><span data-stu-id="6f68f-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="6f68f-124">-eq</span><span class="sxs-lookup"><span data-stu-id="6f68f-124">-eq</span></span>|<span data-ttu-id="6f68f-125">je rovno</span><span class="sxs-lookup"><span data-stu-id="6f68f-125">is equal to</span></span>|<span data-ttu-id="6f68f-126">1 - eq 1</span><span class="sxs-lookup"><span data-stu-id="6f68f-126">1 -eq 1</span></span>|
|<span data-ttu-id="6f68f-127">-ne</span><span class="sxs-lookup"><span data-stu-id="6f68f-127">-ne</span></span>|<span data-ttu-id="6f68f-128">Není rovno</span><span class="sxs-lookup"><span data-stu-id="6f68f-128">Is not equal to</span></span>|<span data-ttu-id="6f68f-129">1 – ne 2</span><span class="sxs-lookup"><span data-stu-id="6f68f-129">1 -ne 2</span></span>|
|<span data-ttu-id="6f68f-130">-lt</span><span class="sxs-lookup"><span data-stu-id="6f68f-130">-lt</span></span>|<span data-ttu-id="6f68f-131">Je menší než</span><span class="sxs-lookup"><span data-stu-id="6f68f-131">Is less than</span></span>|<span data-ttu-id="6f68f-132">1 - lt 2</span><span class="sxs-lookup"><span data-stu-id="6f68f-132">1 -lt 2</span></span>|
|<span data-ttu-id="6f68f-133">-le</span><span class="sxs-lookup"><span data-stu-id="6f68f-133">-le</span></span>|<span data-ttu-id="6f68f-134">Je menší než nebo rovno</span><span class="sxs-lookup"><span data-stu-id="6f68f-134">Is less than or equal to</span></span>|<span data-ttu-id="6f68f-135">1 - le 2</span><span class="sxs-lookup"><span data-stu-id="6f68f-135">1 -le 2</span></span>|
|<span data-ttu-id="6f68f-136">-gt</span><span class="sxs-lookup"><span data-stu-id="6f68f-136">-gt</span></span>|<span data-ttu-id="6f68f-137">Je větší než</span><span class="sxs-lookup"><span data-stu-id="6f68f-137">Is greater than</span></span>|<span data-ttu-id="6f68f-138">2 - gt 1</span><span class="sxs-lookup"><span data-stu-id="6f68f-138">2 -gt 1</span></span>|
|<span data-ttu-id="6f68f-139">-ge</span><span class="sxs-lookup"><span data-stu-id="6f68f-139">-ge</span></span>|<span data-ttu-id="6f68f-140">Je větší než nebo rovno</span><span class="sxs-lookup"><span data-stu-id="6f68f-140">Is greater than or equal to</span></span>|<span data-ttu-id="6f68f-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="6f68f-141">2 -ge 1</span></span>|
|<span data-ttu-id="6f68f-142">-jako</span><span class="sxs-lookup"><span data-stu-id="6f68f-142">-like</span></span>|<span data-ttu-id="6f68f-143">Je třeba (porovnání zástupný text)</span><span class="sxs-lookup"><span data-stu-id="6f68f-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="6f68f-144">"soubor.doc"-jako "f\*.používat?"</span><span class="sxs-lookup"><span data-stu-id="6f68f-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="6f68f-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="6f68f-145">-notlike</span></span>|<span data-ttu-id="6f68f-146">Není třeba (porovnání zástupný text)</span><span class="sxs-lookup"><span data-stu-id="6f68f-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="6f68f-147">"soubor.doc"-notlike "p\*.doc"</span><span class="sxs-lookup"><span data-stu-id="6f68f-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="6f68f-148">-obsahuje</span><span class="sxs-lookup"><span data-stu-id="6f68f-148">-contains</span></span>|<span data-ttu-id="6f68f-149">Obsahuje</span><span class="sxs-lookup"><span data-stu-id="6f68f-149">Contains</span></span>|<span data-ttu-id="6f68f-150">1,2,3 – obsahuje 1</span><span class="sxs-lookup"><span data-stu-id="6f68f-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="6f68f-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="6f68f-151">-notcontains</span></span>|<span data-ttu-id="6f68f-152">Neobsahuje</span><span class="sxs-lookup"><span data-stu-id="6f68f-152">Does not contain</span></span>|<span data-ttu-id="6f68f-153">1,2,3 - notcontains 4</span><span class="sxs-lookup"><span data-stu-id="6f68f-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="6f68f-154">WHERE-Object blocích skriptu použít speciální proměnná ($_)' k odkazování na aktuální objekt v kanálu.</span><span class="sxs-lookup"><span data-stu-id="6f68f-154">Where-Object script blocks use the special variable '$_' to refer to the current object in the pipeline.</span></span> <span data-ttu-id="6f68f-155">Tady je příklad toho, jak funguje.</span><span class="sxs-lookup"><span data-stu-id="6f68f-155">Here is an example of how it works.</span></span> <span data-ttu-id="6f68f-156">Pokud máte seznam čísel a chcete pouze vrátit ty, které jsou menší než 3, můžete filtrovat čísla zadáním Where-Object:</span><span class="sxs-lookup"><span data-stu-id="6f68f-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a><span data-ttu-id="6f68f-157">Filtrování podle vlastnosti objektu</span><span class="sxs-lookup"><span data-stu-id="6f68f-157">Filtering Based on Object Properties</span></span>

<span data-ttu-id="6f68f-158">Vzhledem k tomu, že $_ odkazuje na aktuální objekt kanálu, jsme pro naše testy otevřete jeho vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="6f68f-158">Since $_ refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="6f68f-159">Jako příklad může podíváme na třídě Win32_SystemDriver v rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="6f68f-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="6f68f-160">Může být stovky ovladače systému na konkrétní systém, ale pouze může být zájem o konkrétní sadu ovladačů systému, jako jsou ty, které jsou aktuálně spuštěné.</span><span class="sxs-lookup"><span data-stu-id="6f68f-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="6f68f-161">Pokud chcete zobrazit členy Win32_SystemDriver použít Get-člen (**Get-WmiObject – Třída Win32_SystemDriver | Vlastnost Get-Member - MemberType**) uvidíte, že je odpovídající vlastnost stavu a jeho má hodnotu "Spuštěný", když běží ovladače.</span><span class="sxs-lookup"><span data-stu-id="6f68f-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="6f68f-162">Můžete filtrovat ovladače systému výběr jenom spuštěné ty zadáním:</span><span class="sxs-lookup"><span data-stu-id="6f68f-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

<span data-ttu-id="6f68f-163">To vytváří ještě dlouhý seznam.</span><span class="sxs-lookup"><span data-stu-id="6f68f-163">This still produces a long list.</span></span> <span data-ttu-id="6f68f-164">Chcete filtrovat, aby pouze vyberte ovladače nastavená na automatické spouštění testování hodnotě StartMode:</span><span class="sxs-lookup"><span data-stu-id="6f68f-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

<span data-ttu-id="6f68f-165">To nám dává velké množství informací, které již nepotřebujete, protože víme, že jsou spuštěny ovladače.</span><span class="sxs-lookup"><span data-stu-id="6f68f-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="6f68f-166">Ve skutečnosti jenom informace, které pravděpodobně potřebujeme v tomto okamžiku jsou název a zobrazovaný název.</span><span class="sxs-lookup"><span data-stu-id="6f68f-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="6f68f-167">Následující příkaz obsahuje pouze tyto dvě vlastnosti, což vede k mnohem jednodušší výstup:</span><span class="sxs-lookup"><span data-stu-id="6f68f-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

<span data-ttu-id="6f68f-168">Existují dva elementy Where-Object ve výše uvedeném příkazu, ale mohou být vyjádřeny v jednom elementu Where-Object pomocí- a logickým operátorem takto:</span><span class="sxs-lookup"><span data-stu-id="6f68f-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="6f68f-169">Standardní logické operátory jsou uvedeny v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="6f68f-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="6f68f-170">Logický operátor</span><span class="sxs-lookup"><span data-stu-id="6f68f-170">Logical Operator</span></span>|<span data-ttu-id="6f68f-171">Význam</span><span class="sxs-lookup"><span data-stu-id="6f68f-171">Meaning</span></span>|<span data-ttu-id="6f68f-172">Příklad (vrací hodnotu true)</span><span class="sxs-lookup"><span data-stu-id="6f68f-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="6f68f-173">- a</span><span class="sxs-lookup"><span data-stu-id="6f68f-173">-and</span></span>|<span data-ttu-id="6f68f-174">Logické a; Hodnota TRUE, pokud jsou splněny obě strany</span><span class="sxs-lookup"><span data-stu-id="6f68f-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="6f68f-175">(1 - eq 1) - a (2 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="6f68f-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="6f68f-176">- nebo</span><span class="sxs-lookup"><span data-stu-id="6f68f-176">-or</span></span>|<span data-ttu-id="6f68f-177">Logické nebo; Hodnota TRUE, pokud má jedna strana hodnotu true</span><span class="sxs-lookup"><span data-stu-id="6f68f-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="6f68f-178">(1 - eq 1) - nebo (1 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="6f68f-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="6f68f-179">-není</span><span class="sxs-lookup"><span data-stu-id="6f68f-179">-not</span></span>|<span data-ttu-id="6f68f-180">Logický operátor not; obrátí hodnotu true a false</span><span class="sxs-lookup"><span data-stu-id="6f68f-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="6f68f-181">-není (1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="6f68f-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="6f68f-182">Logický operátor not; obrátí hodnotu true a false</span><span class="sxs-lookup"><span data-stu-id="6f68f-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="6f68f-183">\!(1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="6f68f-183">\!(1 -eq 2)</span></span>|

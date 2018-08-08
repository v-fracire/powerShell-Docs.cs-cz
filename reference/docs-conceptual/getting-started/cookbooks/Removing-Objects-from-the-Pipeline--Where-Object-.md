---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Odebrání objektů z kanálu Where-Object
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: c060b93a3823be26ad6c7757acc633bb4fc2fcfa
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587138"
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="a450d-103">Odebrání objektů z kanálu (Where-Object)</span><span class="sxs-lookup"><span data-stu-id="a450d-103">Removing Objects from the Pipeline (Where-Object)</span></span>

<span data-ttu-id="a450d-104">V prostředí Windows PowerShell často generovat a předali více objektů do kanálu, než se.</span><span class="sxs-lookup"><span data-stu-id="a450d-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="a450d-105">Můžete zadat vlastnosti konkrétní objekty zobrazíte pomocí **formátu** rutiny, ale to nepomůže s problémem, který odebrat celé objekty ze zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a450d-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="a450d-106">Můžete filtrovat objekty do konce profilace, abyste mohli provádět akce s pouze podmnožinu původně vytvořil objekty.</span><span class="sxs-lookup"><span data-stu-id="a450d-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="a450d-107">Obsahuje prostředí Windows PowerShell `Where-Object` rutinu, která umožňuje testování jednotlivých objektů v kanálu a pouze předat podél kanálu pokud splňuje podmínku určitého testu.</span><span class="sxs-lookup"><span data-stu-id="a450d-107">Windows PowerShell includes a `Where-Object` cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="a450d-108">Objekty, které nepředávejte testu se odeberou z kanálu.</span><span class="sxs-lookup"><span data-stu-id="a450d-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="a450d-109">Jako hodnotu zadáte testovací podmínku `Where-Object` **FilterScript** parametru.</span><span class="sxs-lookup"><span data-stu-id="a450d-109">You supply the test condition as the value of the `Where-Object` **FilterScript** parameter.</span></span>

### <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="a450d-110">Provedením jednoduchých testů s Where-Object</span><span class="sxs-lookup"><span data-stu-id="a450d-110">Performing Simple Tests with Where-Object</span></span>

<span data-ttu-id="a450d-111">Hodnota **FilterScript** je *bloku skriptu* – jeden nebo více příkazů prostředí Windows PowerShell, které jsou uzavřeny ve složených závorkách {} –, který se vyhodnotí na hodnotu true nebo false.</span><span class="sxs-lookup"><span data-stu-id="a450d-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="a450d-112">Tyto bloky skriptu může být velmi jednoduchý, ale vytváří, je nutné, abyste znali o jiné koncept prostředí Windows PowerShell, operátory porovnání.</span><span class="sxs-lookup"><span data-stu-id="a450d-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="a450d-113">Operátor porovnání porovná položky, které se zobrazí na každé straně.</span><span class="sxs-lookup"><span data-stu-id="a450d-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="a450d-114">Operátory porovnání začínat "-" znaků a jsou následována název.</span><span class="sxs-lookup"><span data-stu-id="a450d-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="a450d-115">Operátory porovnání základní pracovat na téměř jakýkoli druh objektu.</span><span class="sxs-lookup"><span data-stu-id="a450d-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="a450d-116">Rozšířené operátory porovnání může fungovat jenom na text nebo pole.</span><span class="sxs-lookup"><span data-stu-id="a450d-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="a450d-117">Ve výchozím nastavení se při práci s textem operátory porovnání prostředí Windows PowerShell jsou malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="a450d-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="a450d-118">Z důvodu důležité informace o analýze, symboly, jako je například <>, a = nejsou používány jako operátory porovnání.</span><span class="sxs-lookup"><span data-stu-id="a450d-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="a450d-119">Místo toho operátory porovnání se skládají z písmen.</span><span class="sxs-lookup"><span data-stu-id="a450d-119">Instead, comparison operators are comprised of letters.</span></span> <span data-ttu-id="a450d-120">Základní porovnávací operátory jsou uvedeny v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="a450d-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="a450d-121">Operátor porovnání</span><span class="sxs-lookup"><span data-stu-id="a450d-121">Comparison Operator</span></span>|<span data-ttu-id="a450d-122">Význam</span><span class="sxs-lookup"><span data-stu-id="a450d-122">Meaning</span></span>|<span data-ttu-id="a450d-123">Příklad (vrátí hodnotu true)</span><span class="sxs-lookup"><span data-stu-id="a450d-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="a450d-124">-eq</span><span class="sxs-lookup"><span data-stu-id="a450d-124">-eq</span></span>|<span data-ttu-id="a450d-125">je rovno</span><span class="sxs-lookup"><span data-stu-id="a450d-125">is equal to</span></span>|<span data-ttu-id="a450d-126">1 - eq 1</span><span class="sxs-lookup"><span data-stu-id="a450d-126">1 -eq 1</span></span>|
|<span data-ttu-id="a450d-127">-ne</span><span class="sxs-lookup"><span data-stu-id="a450d-127">-ne</span></span>|<span data-ttu-id="a450d-128">Není rovno</span><span class="sxs-lookup"><span data-stu-id="a450d-128">Is not equal to</span></span>|<span data-ttu-id="a450d-129">1 - ne 2</span><span class="sxs-lookup"><span data-stu-id="a450d-129">1 -ne 2</span></span>|
|<span data-ttu-id="a450d-130">-lt</span><span class="sxs-lookup"><span data-stu-id="a450d-130">-lt</span></span>|<span data-ttu-id="a450d-131">je menší než</span><span class="sxs-lookup"><span data-stu-id="a450d-131">Is less than</span></span>|<span data-ttu-id="a450d-132">1 - lt 2</span><span class="sxs-lookup"><span data-stu-id="a450d-132">1 -lt 2</span></span>|
|<span data-ttu-id="a450d-133">-le.</span><span class="sxs-lookup"><span data-stu-id="a450d-133">-le</span></span>|<span data-ttu-id="a450d-134">Je menší než nebo rovno</span><span class="sxs-lookup"><span data-stu-id="a450d-134">Is less than or equal to</span></span>|<span data-ttu-id="a450d-135">1 - le 2</span><span class="sxs-lookup"><span data-stu-id="a450d-135">1 -le 2</span></span>|
|<span data-ttu-id="a450d-136">-gt</span><span class="sxs-lookup"><span data-stu-id="a450d-136">-gt</span></span>|<span data-ttu-id="a450d-137">je větší než</span><span class="sxs-lookup"><span data-stu-id="a450d-137">Is greater than</span></span>|<span data-ttu-id="a450d-138">2 - gt 1</span><span class="sxs-lookup"><span data-stu-id="a450d-138">2 -gt 1</span></span>|
|<span data-ttu-id="a450d-139">-ge</span><span class="sxs-lookup"><span data-stu-id="a450d-139">-ge</span></span>|<span data-ttu-id="a450d-140">Je větší než nebo rovno</span><span class="sxs-lookup"><span data-stu-id="a450d-140">Is greater than or equal to</span></span>|<span data-ttu-id="a450d-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="a450d-141">2 -ge 1</span></span>|
|<span data-ttu-id="a450d-142">– například</span><span class="sxs-lookup"><span data-stu-id="a450d-142">-like</span></span>|<span data-ttu-id="a450d-143">Je třeba (porovnání zástupný text)</span><span class="sxs-lookup"><span data-stu-id="a450d-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="a450d-144">"soubor.doc"-jako "f\*.používat?"</span><span class="sxs-lookup"><span data-stu-id="a450d-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="a450d-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="a450d-145">-notlike</span></span>|<span data-ttu-id="a450d-146">Není podobné (porovnání zástupný text)</span><span class="sxs-lookup"><span data-stu-id="a450d-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="a450d-147">"soubor.doc"-notlike "p\*doc"</span><span class="sxs-lookup"><span data-stu-id="a450d-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="a450d-148">-obsahuje</span><span class="sxs-lookup"><span data-stu-id="a450d-148">-contains</span></span>|<span data-ttu-id="a450d-149">obsahuje</span><span class="sxs-lookup"><span data-stu-id="a450d-149">Contains</span></span>|<span data-ttu-id="a450d-150">1,2,3 – obsahuje 1</span><span class="sxs-lookup"><span data-stu-id="a450d-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="a450d-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="a450d-151">-notcontains</span></span>|<span data-ttu-id="a450d-152">neobsahuje</span><span class="sxs-lookup"><span data-stu-id="a450d-152">Does not contain</span></span>|<span data-ttu-id="a450d-153">1,2,3 - notcontains 4</span><span class="sxs-lookup"><span data-stu-id="a450d-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="a450d-154">Bloky skriptu Where-Object používat speciální proměnné `$_` pro odkazování na aktuální objekt v kanálu.</span><span class="sxs-lookup"><span data-stu-id="a450d-154">Where-Object script blocks use the special variable `$_` to refer to the current object in the pipeline.</span></span> <span data-ttu-id="a450d-155">Tady je příklad toho, jak funguje.</span><span class="sxs-lookup"><span data-stu-id="a450d-155">Here is an example of how it works.</span></span> <span data-ttu-id="a450d-156">Pokud máte seznam čísel a pouze chcete vrátit těch, které jsou kratší než 3, můžete filtrovat tak, že zadáte čísla Where-Object:</span><span class="sxs-lookup"><span data-stu-id="a450d-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a><span data-ttu-id="a450d-157">Filtrování podle vlastností objektu</span><span class="sxs-lookup"><span data-stu-id="a450d-157">Filtering Based on Object Properties</span></span>

<span data-ttu-id="a450d-158">Protože `$_` odkazuje na aktuální objekt kanálu jsme můžete získat přístup k vlastnostem pro naše testy.</span><span class="sxs-lookup"><span data-stu-id="a450d-158">Since `$_` refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="a450d-159">Jako příklad abychom se mohli podívat na Win32_SystemDriver třídu v rozhraní WMI.</span><span class="sxs-lookup"><span data-stu-id="a450d-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="a450d-160">Může být stovky ovladače systému na konkrétní systém, ale pouze byste měli zájem konkrétní sadu ovladačů systému, jako jsou ty, které jsou aktuálně spuštěny.</span><span class="sxs-lookup"><span data-stu-id="a450d-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="a450d-161">Pokud používáte k zobrazení členů Win32_SystemDriver Get-Member (**Get-WmiObject – Třída Win32_SystemDriver | Vlastnost Get-Member - MemberType**) uvidíte, že je odpovídající vlastnost stavu, a aby měla hodnotu "Spustit" při spuštění ovladače.</span><span class="sxs-lookup"><span data-stu-id="a450d-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="a450d-162">Můžete filtrovat ovladače systému vyberete pouze spuštěné ty zadáním:</span><span class="sxs-lookup"><span data-stu-id="a450d-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

<span data-ttu-id="a450d-163">To vytváří ještě dlouhý seznam.</span><span class="sxs-lookup"><span data-stu-id="a450d-163">This still produces a long list.</span></span> <span data-ttu-id="a450d-164">Můžete chtít filtrovat jenom vybraným nastavená na automatické spouštění otestováním hodnotu StartMode ovladače:</span><span class="sxs-lookup"><span data-stu-id="a450d-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

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

<span data-ttu-id="a450d-165">Tento produkt nám nabízí velké množství informací, které už nepotřebujete, protože víme, že jsou spuštěny ovladače.</span><span class="sxs-lookup"><span data-stu-id="a450d-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="a450d-166">Ve skutečnosti pouze informace, které pravděpodobně potřebujeme v tomto okamžiku jsou název a zobrazovaný název.</span><span class="sxs-lookup"><span data-stu-id="a450d-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="a450d-167">Následující příkaz zahrnuje pouze tyto dvě vlastnosti, což vede k mnohem jednodušší výstup:</span><span class="sxs-lookup"><span data-stu-id="a450d-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

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

<span data-ttu-id="a450d-168">Existují dva prvky Where-Object v předchozím příkazu, ale dají se vyjádřit v jednom elementu Where-Object s použitím- a logický operátor, následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a450d-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="a450d-169">Standardní logické operátory jsou uvedeny v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="a450d-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="a450d-170">Logický operátor</span><span class="sxs-lookup"><span data-stu-id="a450d-170">Logical Operator</span></span>|<span data-ttu-id="a450d-171">Význam</span><span class="sxs-lookup"><span data-stu-id="a450d-171">Meaning</span></span>|<span data-ttu-id="a450d-172">Příklad (vrátí hodnotu true)</span><span class="sxs-lookup"><span data-stu-id="a450d-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="a450d-173">- a</span><span class="sxs-lookup"><span data-stu-id="a450d-173">-and</span></span>|<span data-ttu-id="a450d-174">Logické a; Hodnota TRUE, pokud jsou splněny obě strany</span><span class="sxs-lookup"><span data-stu-id="a450d-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="a450d-175">(1 - eq 1) - a (2 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="a450d-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="a450d-176">- nebo</span><span class="sxs-lookup"><span data-stu-id="a450d-176">-or</span></span>|<span data-ttu-id="a450d-177">Logická nebo; Hodnota TRUE, pokud obě strany hodnotu true</span><span class="sxs-lookup"><span data-stu-id="a450d-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="a450d-178">(1 - eq 1) - nebo (1 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="a450d-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="a450d-179">– Ne</span><span class="sxs-lookup"><span data-stu-id="a450d-179">-not</span></span>|<span data-ttu-id="a450d-180">Logický operátor not; Vrátí hodnotu true a false</span><span class="sxs-lookup"><span data-stu-id="a450d-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="a450d-181">-není (1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="a450d-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="a450d-182">Logický operátor not; Vrátí hodnotu true a false</span><span class="sxs-lookup"><span data-stu-id="a450d-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="a450d-183">\!(1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="a450d-183">\!(1 -eq 2)</span></span>|

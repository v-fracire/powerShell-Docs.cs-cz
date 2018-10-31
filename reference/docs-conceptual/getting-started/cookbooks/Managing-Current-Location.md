---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa aktuálního umístění
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: d1ebc9507a45841e6d4d8219e45c002990e1328c
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225773"
---
# <a name="managing-current-location"></a><span data-ttu-id="71e1d-103">Správa aktuálního umístění</span><span class="sxs-lookup"><span data-stu-id="71e1d-103">Managing Current Location</span></span>

<span data-ttu-id="71e1d-104">Při navigaci systémy složku v Průzkumníku souborů, obvykle mají konkrétní pracovní umístění – konkrétně, aktuální otevřít složku.</span><span class="sxs-lookup"><span data-stu-id="71e1d-104">When navigating folder systems in File Explorer, you usually have a specific working location - namely, the current open folder.</span></span> <span data-ttu-id="71e1d-105">Položky v aktuální složce lze snadno ovládat klepnutím.</span><span class="sxs-lookup"><span data-stu-id="71e1d-105">Items in the current folder can be manipulated easily by clicking them.</span></span> <span data-ttu-id="71e1d-106">Pro rozhraní příkazového řádku, jako je například Cmd.exe když jsou ve stejné složce jako soubor konkrétní můžete přistupovat ho zadání relativně krátký název, spíše než by bylo potřeba zadat celou cestu k souboru.</span><span class="sxs-lookup"><span data-stu-id="71e1d-106">For command-line interfaces such as Cmd.exe, when you are in the same folder as a particular file, you can access it by specifying a relatively short name, rather than needing to specify the entire path to the file.</span></span> <span data-ttu-id="71e1d-107">Aktuální adresář je volána v pracovním adresáři.</span><span class="sxs-lookup"><span data-stu-id="71e1d-107">The current directory is called the working directory.</span></span>

<span data-ttu-id="71e1d-108">Prostředí Windows PowerShell používá podstatným jménem **umístění** odkazovat do pracovního adresáře a implementuje řadu rutin k prozkoumání a manipulaci s umístěním.</span><span class="sxs-lookup"><span data-stu-id="71e1d-108">Windows PowerShell uses the noun **Location** to refer to the working directory, and implements a family of cmdlets to examine and manipulate your location.</span></span>

### <a name="getting-your-current-location-get-location"></a><span data-ttu-id="71e1d-109">Získávání aktuální polohu (Get umístění)</span><span class="sxs-lookup"><span data-stu-id="71e1d-109">Getting Your Current Location (Get-Location)</span></span>

<span data-ttu-id="71e1d-110">Pokud chcete zjistit cestu aktuální umístění adresáře, zadejte **Get-umístění** příkaz:</span><span class="sxs-lookup"><span data-stu-id="71e1d-110">To determine the path of your current directory location, enter the **Get-Location** command:</span></span>

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="71e1d-111">Rutina Get-umístění je podobná **pwd** příkazu v prostředí BASH.</span><span class="sxs-lookup"><span data-stu-id="71e1d-111">The Get-Location cmdlet is similar to the **pwd** command in the BASH shell.</span></span> <span data-ttu-id="71e1d-112">Rutina Set-umístění je podobná **cd** v Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="71e1d-112">The Set-Location cmdlet is similar to the **cd** command in Cmd.exe.</span></span>

### <a name="setting-your-current-location-set-location"></a><span data-ttu-id="71e1d-113">Nastavení vašeho aktuálního umístění (nastavení umístění)</span><span class="sxs-lookup"><span data-stu-id="71e1d-113">Setting Your Current Location (Set-Location)</span></span>

<span data-ttu-id="71e1d-114">**Get-umístění** příkaz se používá s **nastavení umístění** příkazu.</span><span class="sxs-lookup"><span data-stu-id="71e1d-114">The **Get-Location** command is used with the **Set-Location** command.</span></span> <span data-ttu-id="71e1d-115">**Nastavení umístění** příkazu můžete zadat vaše aktuální umístění adresáře.</span><span class="sxs-lookup"><span data-stu-id="71e1d-115">The **Set-Location** command allows you to specify your current directory location.</span></span>

```powershell
Set-Location -Path C:\Windows
```

<span data-ttu-id="71e1d-116">Po zadání příkazu, můžete si všimnout, neobdržíte žádné přímé zpětnou vazbu efekt příkazu.</span><span class="sxs-lookup"><span data-stu-id="71e1d-116">After you enter the command, you will notice that you do not receive any direct feedback about the effect of the command.</span></span> <span data-ttu-id="71e1d-117">Většina příkazů prostředí Windows PowerShell, které provádějí akce vytvořit žádné nebo téměř žádné výstupní, protože není ve výstupu vždy užitečný.</span><span class="sxs-lookup"><span data-stu-id="71e1d-117">Most Windows PowerShell commands that perform an action produce little or no output because the output is not always useful.</span></span> <span data-ttu-id="71e1d-118">Chcete-li ověřit, že došlo ke změně úspěšné adresáře při zadání **nastavení umístění** příkazu, zahrnují **- PassThru** parametr při zadání **Set-umístění**příkaz:</span><span class="sxs-lookup"><span data-stu-id="71e1d-118">To verify that a successful directory change has occurred when you enter the **Set-Location** command, include the **-PassThru** parameter when you enter the **Set-Location** command:</span></span>

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

<span data-ttu-id="71e1d-119">**- PassThru** parametr je možné mnoho sady příkazů v prostředí Windows PowerShell k vrácení informací o výsledek v případech, ve kterých není žádný výchozí výstup.</span><span class="sxs-lookup"><span data-stu-id="71e1d-119">The **-PassThru** parameter can be used with many Set commands in Windows PowerShell to return information about the result in cases in which there is no default output.</span></span>

<span data-ttu-id="71e1d-120">Můžete určit cest vzhledem ke své aktuální polohy stejným způsobem jako vám by ve většině systému UNIX a Windows command Shell.</span><span class="sxs-lookup"><span data-stu-id="71e1d-120">You can specify paths relative to your current location in the same way as you would in most UNIX and Windows command shells.</span></span> <span data-ttu-id="71e1d-121">Ve standardním zápisu pro relativní cesty tečku (**.**) představuje aktuální složky a dvojnásobná období (**...** ) představuje nadřazený adresář složky vašeho aktuálního umístění.</span><span class="sxs-lookup"><span data-stu-id="71e1d-121">In standard notation for relative paths, a period (**.**)represents your current folder, and a doubled period (**..**) represents the parent directory of your current location.</span></span>

<span data-ttu-id="71e1d-122">Například, pokud jste **C:\\Windows** složky, tečku (**.**) představuje **C:\\Windows** a dvakrát období (**...** ) představují **C:**.</span><span class="sxs-lookup"><span data-stu-id="71e1d-122">For example, if you are in the **C:\\Windows** folder, a period (**.**)represents **C:\\Windows** and double periods (**..**) represent **C:**.</span></span> <span data-ttu-id="71e1d-123">Můžete změnit z aktuálního umístění na kořenové jednotce C: zadáním:</span><span class="sxs-lookup"><span data-stu-id="71e1d-123">You can change from your current location to the root of the C: drive by typing:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

<span data-ttu-id="71e1d-124">Stejný postup funguje u jednotek Windows Powershellu, které nejsou jednotky systému souborů, jako například **HKLM:**.</span><span class="sxs-lookup"><span data-stu-id="71e1d-124">The same technique works on Windows PowerShell drives that are not file system drives, such as **HKLM:**.</span></span> <span data-ttu-id="71e1d-125">Můžete nastavit vaši polohu k HKLM\\softwarového klíče v registru tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="71e1d-125">You can set your location to the HKLM\\Software key in the registry by typing:</span></span>

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

<span data-ttu-id="71e1d-126">Dá se změnit umístění adresáře na nadřazeném adresáři, která je kořenem HKLM Windows Powershellu: jednotky pomocí relativní cesty:</span><span class="sxs-lookup"><span data-stu-id="71e1d-126">You can then change the directory location to the parent directory, which is the root of the Windows PowerShell HKLM: drive, by using a relative path:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

<span data-ttu-id="71e1d-127">Můžete zadat nastavení umístění nebo použijte některý z předdefinovaných aliasy prostředí Windows PowerShell pro nastavení umístění (cd, chdir, sl).</span><span class="sxs-lookup"><span data-stu-id="71e1d-127">You can type Set-Location or use any of the built-in Windows PowerShell aliases for Set-Location (cd, chdir, sl).</span></span> <span data-ttu-id="71e1d-128">Příklad:</span><span class="sxs-lookup"><span data-stu-id="71e1d-128">For example:</span></span>

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a><span data-ttu-id="71e1d-129">Ukládání a vrací nedávných umístění (umístění nabízených oznámení a umístění Pop)</span><span class="sxs-lookup"><span data-stu-id="71e1d-129">Saving and Recalling Recent Locations (Push-Location and Pop-Location)</span></span>

<span data-ttu-id="71e1d-130">Při změně umístění, je vhodné zaznamenávat kdy byly a bude moct vrátit do předchozího umístění.</span><span class="sxs-lookup"><span data-stu-id="71e1d-130">When changing locations, it is helpful to keep track of where you have been and to be able to return to your previous location.</span></span> <span data-ttu-id="71e1d-131">**Nabízených umístění** rutiny v prostředí Windows PowerShell vytvoří seřazený historii ("zásobníku") adresář cesty, kde máte, a můžete krokovat zpět historie cesty k adresářům s využitím doplňující  **Umístění POP** rutiny.</span><span class="sxs-lookup"><span data-stu-id="71e1d-131">The **Push-Location** cmdlet in Windows PowerShell creates a ordered history (a "stack") of directory paths where you have been, and you can step back through the history of directory paths by using the complementary **Pop-Location** cmdlet.</span></span>

<span data-ttu-id="71e1d-132">Například prostředí Windows PowerShell se obvykle spouští domovského adresáře uživatele.</span><span class="sxs-lookup"><span data-stu-id="71e1d-132">For example, Windows PowerShell typically starts in the user's home directory.</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="71e1d-133">Slovo *zásobníku* má zvláštní význam v mnoha programovacích nastavení, včetně rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="71e1d-133">The word *stack* has a special meaning in many programming settings, including .NET Framework.</span></span> <span data-ttu-id="71e1d-134">Podobně jako fyzického zásobníku položky poslední položky, kterou chcete vložit do zásobníku je první položka, která si můžete vyžádat ze zásobníku.</span><span class="sxs-lookup"><span data-stu-id="71e1d-134">Like a physical stack of items, the last item you put onto the stack is the first item that you can pull off the stack.</span></span> <span data-ttu-id="71e1d-135">Přidání položky do zásobníku je colloquially označuje jako "doručením (push)" položky do zásobníku.</span><span class="sxs-lookup"><span data-stu-id="71e1d-135">Adding an item to a stack is colloquially known as "pushing" the item onto the stack.</span></span> <span data-ttu-id="71e1d-136">Stahování položky ze zásobníku se colloquially označuje jako "vyjímání" položky ze zásobníku.</span><span class="sxs-lookup"><span data-stu-id="71e1d-136">Pulling an item off the stack is colloquially known as "popping" the item off the stack.</span></span>

<span data-ttu-id="71e1d-137">Pokud chcete vložit do aktuálního umístění do zásobníku a pak přejděte do složky místní nastavení, zadejte:</span><span class="sxs-lookup"><span data-stu-id="71e1d-137">To push the current location onto the stack, and then move to the Local Settings folder, type:</span></span>

```powershell
Push-Location -Path "Local Settings"
```

<span data-ttu-id="71e1d-138">Potom můžete vložit umístění místní nastavení do zásobníku a přejít ke složce Temp tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="71e1d-138">You can then push the Local Settings location onto the stack and move to the Temp folder by typing:</span></span>

```powershell
Push-Location -Path Temp
```

<span data-ttu-id="71e1d-139">Můžete ověřit, že jste změnili adresáře tak, že zadáte **Get-umístění** příkaz:</span><span class="sxs-lookup"><span data-stu-id="71e1d-139">You can verify that you changed directories by entering the **Get-Location** command:</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

<span data-ttu-id="71e1d-140">Můžete se pak automaticky zpátky do naposledy navštívenému adresáři zadáním **umístění Pop** příkaz a zkontrolujte změnu tak, že zadáte **Get-umístění** příkaz:</span><span class="sxs-lookup"><span data-stu-id="71e1d-140">You can then pop back into the most recently visited directory by entering the **Pop-Location** command, and verify the change by entering the **Get-Location** command:</span></span>

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

<span data-ttu-id="71e1d-141">Stejně jako u **nastavení umístění** rutiny, můžete zahrnout **- PassThru** parametr při zadání **umístění Pop** rutiny adresáře, který jste zadali:</span><span class="sxs-lookup"><span data-stu-id="71e1d-141">Just as with the **Set-Location** cmdlet, you can include the **-PassThru** parameter when you enter the **Pop-Location** cmdlet to display the directory that you entered:</span></span>

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

<span data-ttu-id="71e1d-142">Můžete také použít rutiny umístění s síťových cest.</span><span class="sxs-lookup"><span data-stu-id="71e1d-142">You can also use the Location cmdlets with network paths.</span></span> <span data-ttu-id="71e1d-143">Pokud máte server s názvem FS01 se do sdílené složky s názvem veřejné své umístění můžete změnit tak, že zadáte</span><span class="sxs-lookup"><span data-stu-id="71e1d-143">If you have a server named FS01 with an share named Public, you can change your location by typing</span></span>

```powershell
Set-Location \\FS01\Public
```

<span data-ttu-id="71e1d-144">nebo</span><span class="sxs-lookup"><span data-stu-id="71e1d-144">or</span></span>

```powershell
Push-Location \\FS01\Public
```

<span data-ttu-id="71e1d-145">Můžete použít **nabízených umístění** a **nastavení umístění** příkazy a změňte umístění pro všechny dostupnou jednotku.</span><span class="sxs-lookup"><span data-stu-id="71e1d-145">You can use the **Push-Location** and **Set-Location** commands to change the location to any available drive.</span></span> <span data-ttu-id="71e1d-146">Například pokud máte místní jednotku CD-ROM s písmenem jednotky D, která obsahuje datový disk CD, můžete změnit umístění na jednotce CD tak, že zadáte **D: nastavení umístění** příkazu.</span><span class="sxs-lookup"><span data-stu-id="71e1d-146">For example, if you have a local CD-ROM drive with drive letter D that contains a data CD, you can change the location to the CD drive by entering the **Set-Location D:** command.</span></span>

<span data-ttu-id="71e1d-147">Pokud jednotka je prázdná, zobrazí se následující chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="71e1d-147">If the drive is empty, you will get the following error message:</span></span>

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

<span data-ttu-id="71e1d-148">Při použití rozhraní příkazového řádku, není vhodné používat Průzkumníka souborů pro zjištění dostupné fyzické disky.</span><span class="sxs-lookup"><span data-stu-id="71e1d-148">When you are using a command-line interface, it is not convenient to use File Explorer to examine the available physical drives.</span></span> <span data-ttu-id="71e1d-149">Také Průzkumníka souborů by ukazují, všechny jednotky prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71e1d-149">Also, File Explorer would not show you the all of the Windows PowerShell drives.</span></span> <span data-ttu-id="71e1d-150">Prostředí Windows PowerShell poskytuje sadu příkazů pro zpracování jednotky Windows Powershellu a mluvíme o tyto další.</span><span class="sxs-lookup"><span data-stu-id="71e1d-150">Windows PowerShell provides a set of commands for manipulating Windows PowerShell drives, and we will talk about these next.</span></span>

---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa aktuálního umístění
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: 8d529bf4a85553b95a9cab2739016859662486f2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952218"
---
# <a name="managing-current-location"></a><span data-ttu-id="7798d-103">Správa aktuálního umístění</span><span class="sxs-lookup"><span data-stu-id="7798d-103">Managing Current Location</span></span>

<span data-ttu-id="7798d-104">Při přechodu systémy složky v Průzkumníku souborů, obvykle mají konkrétní pracovní umístění – konkrétně, aktuální otevřít složku.</span><span class="sxs-lookup"><span data-stu-id="7798d-104">When navigating folder systems in File Explorer, you usually have a specific working location - namely, the current open folder.</span></span> <span data-ttu-id="7798d-105">Položky v aktuální složce se dá snadno upravit kliknutím je.</span><span class="sxs-lookup"><span data-stu-id="7798d-105">Items in the current folder can be manipulated easily by clicking them.</span></span> <span data-ttu-id="7798d-106">Pro rozhraní příkazového řádku, jako je například Cmd.exe když jsou ve stejné složce jako konkrétní soubor, můžete k němu přístup zadání relativně krátkého názvu, namísto nutnosti zadat celou cestu k souboru.</span><span class="sxs-lookup"><span data-stu-id="7798d-106">For command-line interfaces such as Cmd.exe, when you are in the same folder as a particular file, you can access it by specifying a relatively short name, rather than needing to specify the entire path to the file.</span></span> <span data-ttu-id="7798d-107">Aktuální adresář se nazývá pracovní adresář.</span><span class="sxs-lookup"><span data-stu-id="7798d-107">The current directory is called the working directory.</span></span>

<span data-ttu-id="7798d-108">Prostředí Windows PowerShell používá podstatným jménem **umístění** odkazovat na pracovní adresář a implementuje řadu rutin sloužící ke zkoumání a manipulaci s vaši polohu.</span><span class="sxs-lookup"><span data-stu-id="7798d-108">Windows PowerShell uses the noun **Location** to refer to the working directory, and implements a family of cmdlets to examine and manipulate your location.</span></span>

### <a name="getting-your-current-location-get-location"></a><span data-ttu-id="7798d-109">Získávání aktuální umístění (Get umístění)</span><span class="sxs-lookup"><span data-stu-id="7798d-109">Getting Your Current Location (Get-Location)</span></span>

<span data-ttu-id="7798d-110">Chcete-li zjistit cestu vaše aktuální umístění adresáře, zadejte **Get-umístění** příkaz:</span><span class="sxs-lookup"><span data-stu-id="7798d-110">To determine the path of your current directory location, enter the **Get-Location** command:</span></span>

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="7798d-111">Rutina Get-umístění je podobná **pwd** příkazu v prostředí BASH.</span><span class="sxs-lookup"><span data-stu-id="7798d-111">The Get-Location cmdlet is similar to the **pwd** command in the BASH shell.</span></span> <span data-ttu-id="7798d-112">Nastavení umístění rutina je podobná **cd** v Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="7798d-112">The Set-Location cmdlet is similar to the **cd** command in Cmd.exe.</span></span>

### <a name="setting-your-current-location-set-location"></a><span data-ttu-id="7798d-113">Nastavení vaše aktuální umístění (Set umístění)</span><span class="sxs-lookup"><span data-stu-id="7798d-113">Setting Your Current Location (Set-Location)</span></span>

<span data-ttu-id="7798d-114">**Get-umístění** příkaz se používá s **nastavení umístění** příkaz.</span><span class="sxs-lookup"><span data-stu-id="7798d-114">The **Get-Location** command is used with the **Set-Location** command.</span></span> <span data-ttu-id="7798d-115">**Nastavení umístění** příkaz umožňuje zadat vaše aktuální umístění adresáře.</span><span class="sxs-lookup"><span data-stu-id="7798d-115">The **Set-Location** command allows you to specify your current directory location.</span></span>

```powershell
Set-Location -Path C:\Windows
```

<span data-ttu-id="7798d-116">Po zadání příkazu si všimnete, že neobdržíte žádné přímé zpětnou vazbu o efekt příkazu.</span><span class="sxs-lookup"><span data-stu-id="7798d-116">After you enter the command, you will notice that you do not receive any direct feedback about the effect of the command.</span></span> <span data-ttu-id="7798d-117">Většina příkazů prostředí Windows PowerShell, které provádějí akce vytvořit žádné nebo téměř žádné výstup, protože výstup není vždy užitečné.</span><span class="sxs-lookup"><span data-stu-id="7798d-117">Most Windows PowerShell commands that perform an action produce little or no output because the output is not always useful.</span></span> <span data-ttu-id="7798d-118">Chcete-li ověřit, že došlo ke změně úspěšné directory při zadávání **nastavení umístění** příkaz, zahrnují **- PassThru** parametr při zadání **Set-umístění**příkaz:</span><span class="sxs-lookup"><span data-stu-id="7798d-118">To verify that a successful directory change has occurred when you enter the **Set-Location** command, include the **-PassThru** parameter when you enter the **Set-Location** command:</span></span>

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

<span data-ttu-id="7798d-119">**- PassThru** parametr můžete použít s mnoha sady příkazů v prostředí Windows PowerShell k vrácení informací o výsledek v případech, ve kterých je žádný výchozí výstup.</span><span class="sxs-lookup"><span data-stu-id="7798d-119">The **-PassThru** parameter can be used with many Set commands in Windows PowerShell to return information about the result in cases in which there is no default output.</span></span>

<span data-ttu-id="7798d-120">Můžete určit cest relativně k vaše aktuální umístění stejným způsobem, jako je by ve většině systému UNIX a Windows příkazu prostředí shell.</span><span class="sxs-lookup"><span data-stu-id="7798d-120">You can specify paths relative to your current location in the same way as you would in most UNIX and Windows command shells.</span></span> <span data-ttu-id="7798d-121">Ve standardním zápisu pro relativní cesty tečku (**.**) představuje aktuální složce a zdvojených období (**...** ) představuje nadřazeném adresáři vaše aktuální umístění.</span><span class="sxs-lookup"><span data-stu-id="7798d-121">In standard notation for relative paths, a period (**.**)represents your current folder, and a doubled period (**..**) represents the parent directory of your current location.</span></span>

<span data-ttu-id="7798d-122">Například, pokud jste v **C:\\Windows** složku, tečku (**.**) představuje **C:\\Windows** a dvakrát tečky (**...** ) představují **C:**.</span><span class="sxs-lookup"><span data-stu-id="7798d-122">For example, if you are in the **C:\\Windows** folder, a period (**.**)represents **C:\\Windows** and double periods (**..**) represent **C:**.</span></span> <span data-ttu-id="7798d-123">Můžete změnit z aktuálního umístění do kořenového adresáře jednotky C: zadáním:</span><span class="sxs-lookup"><span data-stu-id="7798d-123">You can change from your current location to the root of the C: drive by typing:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

<span data-ttu-id="7798d-124">Stejný postup funguje na jednotkách prostředí Windows PowerShell, které nejsou jednotky systému souborů, jako například **HKLM:**.</span><span class="sxs-lookup"><span data-stu-id="7798d-124">The same technique works on Windows PowerShell drives that are not file system drives, such as **HKLM:**.</span></span> <span data-ttu-id="7798d-125">Můžete nastavit vaši polohu, aby HKLM\\softwarového klíče v registru zadáním:</span><span class="sxs-lookup"><span data-stu-id="7798d-125">You can set your location to the HKLM\\Software key in the registry by typing:</span></span>

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

<span data-ttu-id="7798d-126">Můžete změnit umístění adresáře na nadřazeném adresáři, který je kořenem HKLM prostředí PowerShell systému Windows: jednotky pomocí relativní cesty:</span><span class="sxs-lookup"><span data-stu-id="7798d-126">You can then change the directory location to the parent directory, which is the root of the Windows PowerShell HKLM: drive, by using a relative path:</span></span>

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

<span data-ttu-id="7798d-127">Můžete zadat nastavení umístění nebo použít některou z předdefinovaných aliasy prostředí Windows PowerShell pro nastavení umístění (cd, chdir, sl).</span><span class="sxs-lookup"><span data-stu-id="7798d-127">You can type Set-Location or use any of the built-in Windows PowerShell aliases for Set-Location (cd, chdir, sl).</span></span> <span data-ttu-id="7798d-128">Příklad:</span><span class="sxs-lookup"><span data-stu-id="7798d-128">For example:</span></span>

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a><span data-ttu-id="7798d-129">Ukládání a vrací poslední umístění (nabízené umístění a umístění Pop)</span><span class="sxs-lookup"><span data-stu-id="7798d-129">Saving and Recalling Recent Locations (Push-Location and Pop-Location)</span></span>

<span data-ttu-id="7798d-130">Při změně umístění, je užitečné, chcete-li zaznamenávat, kde jste a mohli vrátit do předchozího umístění.</span><span class="sxs-lookup"><span data-stu-id="7798d-130">When changing locations, it is helpful to keep track of where you have been and to be able to return to your previous location.</span></span> <span data-ttu-id="7798d-131">**Nabízené umístění** rutiny v prostředí Windows PowerShell vytvoří seřazené historii ("zásobník") directory cesty, kde jste, a můžete krokovat zpět v historii cesty adresářů pomocí doplňkové  **Umístění POP** rutiny.</span><span class="sxs-lookup"><span data-stu-id="7798d-131">The **Push-Location** cmdlet in Windows PowerShell creates a ordered history (a "stack") of directory paths where you have been, and you can step back through the history of directory paths by using the complementary **Pop-Location** cmdlet.</span></span>

<span data-ttu-id="7798d-132">Například prostředí Windows PowerShell se obvykle spustí v domovskému adresáři uživatele.</span><span class="sxs-lookup"><span data-stu-id="7798d-132">For example, Windows PowerShell typically starts in the user's home directory.</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> <span data-ttu-id="7798d-133">Slovo *zásobníku* má zvláštní význam v mnoha programovací nastavení, včetně rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="7798d-133">The word *stack* has a special meaning in many programming settings, including .NET Framework.</span></span> <span data-ttu-id="7798d-134">Poslední položky, které vložíte do zásobníku jako fyzické zásobníky položek, je první položka, který můžete použít ze zásobníku.</span><span class="sxs-lookup"><span data-stu-id="7798d-134">Like a physical stack of items, the last item you put onto the stack is the first item that you can pull off the stack.</span></span> <span data-ttu-id="7798d-135">Přidání položky do zásobníku se colloquially označuje jako "vkládání" položky do zásobníku.</span><span class="sxs-lookup"><span data-stu-id="7798d-135">Adding an item to a stack is colloquially known as "pushing" the item onto the stack.</span></span> <span data-ttu-id="7798d-136">Stahování položky ze zásobníku se colloquially označuje jako "odebrání" položku ze zásobníku.</span><span class="sxs-lookup"><span data-stu-id="7798d-136">Pulling an item off the stack is colloquially known as "popping" the item off the stack.</span></span>

<span data-ttu-id="7798d-137">Chcete-li nabízená aktuální umístění do zásobníku a pak přejděte do složky místní nastavení, zadejte:</span><span class="sxs-lookup"><span data-stu-id="7798d-137">To push the current location onto the stack, and then move to the Local Settings folder, type:</span></span>

```powershell
Push-Location -Path "Local Settings"
```

<span data-ttu-id="7798d-138">Potom můžete posouvat nastavení místního umístění do zásobníku a a přesuňte do dočasné složky zadáním:</span><span class="sxs-lookup"><span data-stu-id="7798d-138">You can then push the Local Settings location onto the stack and and move to the Temp folder by typing:</span></span>

```powershell
Push-Location -Path Temp
```

<span data-ttu-id="7798d-139">Můžete ověřit, že jste změnili adresáře zadáním **Get-umístění** příkaz:</span><span class="sxs-lookup"><span data-stu-id="7798d-139">You can verify that you changed directories by entering the **Get-Location** command:</span></span>

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

<span data-ttu-id="7798d-140">Můžete se zpět do naposledy navštívené adresáře zadáním pak pop **umístění Pop** příkazů a změnu ověřit tak, že zadáte **Get-umístění** příkaz:</span><span class="sxs-lookup"><span data-stu-id="7798d-140">You can then pop back into the most recently visited directory by entering the **Pop-Location** command, and verify the change by entering the **Get-Location** command:</span></span>

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

<span data-ttu-id="7798d-141">Jenom jako s **nastavení umístění** rutiny, můžete zahrnout **- PassThru** parametr při zadání **umístění Pop** rutiny zobrazíte adresáře, který jste zadali:</span><span class="sxs-lookup"><span data-stu-id="7798d-141">Just as with the **Set-Location** cmdlet, you can include the **-PassThru** parameter when you enter the **Pop-Location** cmdlet to display the directory that you entered:</span></span>

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

<span data-ttu-id="7798d-142">Můžete taky rutiny umístění s síťových cest.</span><span class="sxs-lookup"><span data-stu-id="7798d-142">You can also use the Location cmdlets with network paths.</span></span> <span data-ttu-id="7798d-143">Pokud máte server s názvem FS01 se sdílenou složku s názvem veřejné, vaše umístění můžete změnit zadáním</span><span class="sxs-lookup"><span data-stu-id="7798d-143">If you have a server named FS01 with an share named Public, you can change your location by typing</span></span>

```powershell
Set-Location \\FS01\Public
```

<span data-ttu-id="7798d-144">nebo</span><span class="sxs-lookup"><span data-stu-id="7798d-144">or</span></span>

```powershell
Push-Location \\FS01\Public
```

<span data-ttu-id="7798d-145">Můžete použít **nabízené umístění** a **nastavení umístění** příkazy a změňte umístění na všechny dostupnou jednotku.</span><span class="sxs-lookup"><span data-stu-id="7798d-145">You can use the **Push-Location** and **Set-Location** commands to change the location to any available drive.</span></span> <span data-ttu-id="7798d-146">Například pokud máte místní jednotku CD-ROM s písmenem jednotky D, který obsahuje datový disk CD, můžete změnit umístění na jednotce CD zadáním **D: nastavení umístění** příkaz.</span><span class="sxs-lookup"><span data-stu-id="7798d-146">For example, if you have a local CD-ROM drive with drive letter D that contains a data CD, you can change the location to the CD drive by entering the **Set-Location D:** command.</span></span>

<span data-ttu-id="7798d-147">Pokud jednotku je prázdná, zobrazí se následující chybová zpráva:</span><span class="sxs-lookup"><span data-stu-id="7798d-147">If the drive is empty, you will get the following error message:</span></span>

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

<span data-ttu-id="7798d-148">Pokud používáte rozhraní příkazového řádku, není vhodné Průzkumníkovi souborů zkontrolujte dostupné fyzické disky.</span><span class="sxs-lookup"><span data-stu-id="7798d-148">When you are using a command-line interface, it is not convenient to use File Explorer to examine the available physical drives.</span></span> <span data-ttu-id="7798d-149">Průzkumníka souborů můžete by také zobrazit všechna jednotek prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7798d-149">Also, File Explorer would not show you the all of the Windows PowerShell drives.</span></span> <span data-ttu-id="7798d-150">Prostředí Windows PowerShell poskytuje sadu příkazů pro manipulaci s jednotky prostředí Windows PowerShell a se věnuje tyto další.</span><span class="sxs-lookup"><span data-stu-id="7798d-150">Windows PowerShell provides a set of commands for manipulating Windows PowerShell drives, and we will talk about these next.</span></span>
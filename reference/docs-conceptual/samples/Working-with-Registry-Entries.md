---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s položkami registru
ms.assetid: fd254570-27ac-4cc9-81d4-011afd29b7dc
ms.openlocfilehash: bffdf80931fc4dc570b584623487077dc5d449dc
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403866"
---
# <a name="working-with-registry-entries"></a><span data-ttu-id="53684-103">Práce s položkami registru</span><span class="sxs-lookup"><span data-stu-id="53684-103">Working with Registry Entries</span></span>

<span data-ttu-id="53684-104">Protože položky registru jsou vlastnosti klíče a v důsledku toho nelze procházet přímo, musíme provést trochu jiný přístup při práci s nimi.</span><span class="sxs-lookup"><span data-stu-id="53684-104">Because registry entries are properties of keys and, as such, cannot be directly browsed, we need to take a slightly different approach when working with them.</span></span>

### <a name="listing-registry-entries"></a><span data-ttu-id="53684-105">Výpis položky registru</span><span class="sxs-lookup"><span data-stu-id="53684-105">Listing Registry Entries</span></span>

<span data-ttu-id="53684-106">Zkontrolujte položky registru mnoha různými způsoby.</span><span class="sxs-lookup"><span data-stu-id="53684-106">There are many different ways to examine registry entries.</span></span> <span data-ttu-id="53684-107">Nejjednodušší způsob je získat názvy vlastností, které jsou spojené s klíčem.</span><span class="sxs-lookup"><span data-stu-id="53684-107">The simplest way is to get the property names associated with a key.</span></span> <span data-ttu-id="53684-108">Například, pokud chcete zobrazit názvy položek v klíči registru **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**, použijte **Get-Item** .</span><span class="sxs-lookup"><span data-stu-id="53684-108">For example, to see the names of the entries in the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion**, use **Get-Item**.</span></span> <span data-ttu-id="53684-109">Klíče registru mají vlastnost s obecným názvem "Vlastnosti", který je uveden seznam položky registru v klíči.</span><span class="sxs-lookup"><span data-stu-id="53684-109">Registry keys have a property with the generic name of "Property" that is a list of registry entries in the key.</span></span> <span data-ttu-id="53684-110">Následující příkaz vybere vlastnost Property a rozbalí položky tak, aby se zobrazí v seznamu:</span><span class="sxs-lookup"><span data-stu-id="53684-110">The following command selects the Property property and expands the items so that they are displayed in a list:</span></span>

```
PS> Get-Item -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion | Select-Object -ExpandProperty Property
DevicePath
MediaPathUnexpanded
ProgramFilesDir
CommonFilesDir
ProductId
```

<span data-ttu-id="53684-111">Chcete-li zobrazit položky registru ve formě lépe čitelný, použijte **Get-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="53684-111">To view the registry entries in a more readable form, use **Get-ItemProperty**:</span></span>

```
PS> Get-ItemProperty -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion

PSPath              : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows\CurrentVersion
PSParentPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SO
                      FTWARE\Microsoft\Windows
PSChildName         : CurrentVersion
PSDrive             : HKLM
PSProvider          : Microsoft.PowerShell.Core\Registry
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
CommonFilesDir      : C:\Program Files\Common Files
ProductId           : 76487-338-1167776-22465
WallPaperDir        : C:\WINDOWS\Web\Wallpaper
MediaPath           : C:\WINDOWS\Media
ProgramFilesPath    : C:\Program Files
PF_AccessoriesName  : Accessories
(default)           :
```

<span data-ttu-id="53684-112">Vlastnosti související s prostředí Windows PowerShell pro klíč jsou předponu "PS", jako například **PSPath**, **PSParentPath**, **PSChildName**, a **PSProvider** .</span><span class="sxs-lookup"><span data-stu-id="53684-112">The Windows PowerShell-related properties for the key are all prefixed with "PS", such as **PSPath**, **PSParentPath**, **PSChildName**, and **PSProvider**.</span></span>

<span data-ttu-id="53684-113">Můžete použít "**.**" notace pro odkazování na aktuální umístění.</span><span class="sxs-lookup"><span data-stu-id="53684-113">You can use the "**.**" notation for referring to the current location.</span></span> <span data-ttu-id="53684-114">Můžete použít **nastavení umístění** změnit **CurrentVersion** registru kontejneru první:</span><span class="sxs-lookup"><span data-stu-id="53684-114">You can use **Set-Location** to change to the **CurrentVersion** registry container first:</span></span>

```powershell
Set-Location -Path Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="53684-115">Alternativně můžete použít předdefinované PSDrive HKLM s **nastavení umístění**:</span><span class="sxs-lookup"><span data-stu-id="53684-115">Alternatively, you can use the built-in HKLM PSDrive with **Set-Location**:</span></span>

```powershell
Set-Location -Path hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion
```

<span data-ttu-id="53684-116">Pak můžete použít "**.**" podle aktuálního umístění do seznamu vlastností bez zadání úplné cesty:</span><span class="sxs-lookup"><span data-stu-id="53684-116">You can then use the "**.**" notation for the current location to list the properties without specifying a full path:</span></span>

```
PS> Get-ItemProperty -Path .
...
DevicePath          : C:\WINDOWS\inf
MediaPathUnexpanded : C:\WINDOWS\Media
ProgramFilesDir     : C:\Program Files
...
```

<span data-ttu-id="53684-117">Rozšíření cesty funguje stejně jako v systému souborů, takže z tohoto místa můžete získat **ItemProperty** výpis pro **HKLM:\\softwaru\\Microsoft\\Windows \\Pomáhají** pomocí **Get-ItemProperty-cesta... \\Pomáhají**.</span><span class="sxs-lookup"><span data-stu-id="53684-117">Path expansion works the same as it does within the file system, so from this location you can get the **ItemProperty** listing for **HKLM:\\SOFTWARE\\Microsoft\\Windows\\Help** by using **Get-ItemProperty -Path ..\\Help**.</span></span>

### <a name="getting-a-single-registry-entry"></a><span data-ttu-id="53684-118">Získání položky jednoho registru</span><span class="sxs-lookup"><span data-stu-id="53684-118">Getting a Single Registry Entry</span></span>

<span data-ttu-id="53684-119">Pokud chcete načíst konkrétní položky klíče registru, můžete použít jeden z několika možných přístupů.</span><span class="sxs-lookup"><span data-stu-id="53684-119">If you want to retrieve a specific entry in a registry key, you can use one of several possible approaches.</span></span> <span data-ttu-id="53684-120">Tento příklad vyhledá hodnotu **DevicePath** v **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="53684-120">This example finds the value of **DevicePath** in **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span>

<span data-ttu-id="53684-121">Pomocí **Get-ItemProperty**, použijte **cesta** parametru určete název klíče a **název** parametr zadejte název **DevicePath** položka.</span><span class="sxs-lookup"><span data-stu-id="53684-121">Using **Get-ItemProperty**, use the **Path** parameter to specify the name of the key, and the **Name** parameter to specify the name of the **DevicePath** entry.</span></span>

```
PS> Get-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion -Name DevicePath

PSPath       : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows\CurrentVersion
PSParentPath : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\
               Microsoft\Windows
PSChildName  : CurrentVersion
PSDrive      : HKLM
PSProvider   : Microsoft.PowerShell.Core\Registry
DevicePath   : C:\WINDOWS\inf
```

<span data-ttu-id="53684-122">Tento příkaz vrátí standardní vlastnosti prostředí Windows PowerShell společně s **DevicePath** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="53684-122">This command returns the standard Windows PowerShell properties as well as the **DevicePath** property.</span></span>

> [!NOTE]
> <span data-ttu-id="53684-123">I když **Get-ItemProperty** má **filtr**, **zahrnout**, a **vyloučit** parametry, nelze je použít k filtrování podle názvu vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="53684-123">Although **Get-ItemProperty** has **Filter**, **Include**, and **Exclude** parameters, they cannot be used to filter by property name.</span></span> <span data-ttu-id="53684-124">Přečtěte si tyto parametry ke klíčům registru – což jsou cesty položky – a položky registru není – které jsou vlastnosti položky.</span><span class="sxs-lookup"><span data-stu-id="53684-124">These parameters refer to registry keys—which are item paths—and not registry entries—which are item properties.</span></span>

<span data-ttu-id="53684-125">Další možností je použít nástroj příkazového řádku Reg.exe.</span><span class="sxs-lookup"><span data-stu-id="53684-125">Another option is to use the Reg.exe command line tool.</span></span> <span data-ttu-id="53684-126">Nápovědu k reg.exe, zadejte **reg.exe /?**</span><span class="sxs-lookup"><span data-stu-id="53684-126">For help with reg.exe, type **reg.exe /?**</span></span> <span data-ttu-id="53684-127">na příkazovém řádku.</span><span class="sxs-lookup"><span data-stu-id="53684-127">at a command prompt.</span></span> <span data-ttu-id="53684-128">Pokud chcete zjistit položce, použijte reg.exe, jak je znázorněno v následujícím příkazu:</span><span class="sxs-lookup"><span data-stu-id="53684-128">To find the DevicePath entry, use reg.exe as shown in the following command:</span></span>

```
PS> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion /v DevicePath

! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion
    DevicePath  REG_EXPAND_SZ   %SystemRoot%\inf
```

<span data-ttu-id="53684-129">Můžete také použít **WshShell COM** objekt také najít některé položky registru, i když tato metoda nebude fungovat s velkými binárními datovými nebo s názvy položky registru, které obsahují znaky, například "\\").</span><span class="sxs-lookup"><span data-stu-id="53684-129">You can also use the **WshShell COM** object as well to find some registry entries, although this method does not work with large binary data or with registry entry names that include characters such as "\\").</span></span> <span data-ttu-id="53684-130">Připojit k cesta položky s názvem vlastnosti \\ oddělovač:</span><span class="sxs-lookup"><span data-stu-id="53684-130">Append the property name to the item path with a \\ separator:</span></span>

```
PS> (New-Object -ComObject WScript.Shell).RegRead("HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\DevicePath")
%SystemRoot%\inf
```

### <a name="creating-new-registry-entries"></a><span data-ttu-id="53684-131">Vytvoření nové položky registru</span><span class="sxs-lookup"><span data-stu-id="53684-131">Creating New Registry Entries</span></span>

<span data-ttu-id="53684-132">Chcete-li přidat novou položku s názvem "PowerShellPath" k **CurrentVersion** použití klíčů, **New-ItemProperty** s cestou ke klíči, název položky a hodnotu položky.</span><span class="sxs-lookup"><span data-stu-id="53684-132">To add a new entry named "PowerShellPath" to the **CurrentVersion** key, use **New-ItemProperty** with the path to the key, the entry name, and the value of the entry.</span></span> <span data-ttu-id="53684-133">V tomto příkladu my podnikneme hodnotu proměnné prostředí Windows PowerShell **$PSHome**, která ukládá ji do instalačního adresáře pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53684-133">For this example, we will take the value of the Windows PowerShell variable **$PSHome**, which stores the path to the installation directory for Windows PowerShell.</span></span>

<span data-ttu-id="53684-134">Pomocí následujícího příkazu můžete přidat novou položku klíče a příkaz také vrátí informace o nové položky:</span><span class="sxs-lookup"><span data-stu-id="53684-134">You can add the new entry to the key by using the following command, and the command also returns information about the new entry:</span></span>

```
PS> New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome

PSPath         : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows\CurrentVersion
PSParentPath   : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWAR
                 E\Microsoft\Windows
PSChildName    : CurrentVersion
PSDrive        : HKLM
PSProvider     : Microsoft.PowerShell.Core\Registry
PowerShellPath : C:\Program Files\Windows PowerShell\v1.0
```

<span data-ttu-id="53684-135">**Typ PropertyType** musí být název **Microsoft.Win32.RegistryValueKind** člena výčtu v následující tabulce:</span><span class="sxs-lookup"><span data-stu-id="53684-135">The **PropertyType** must be the name of a **Microsoft.Win32.RegistryValueKind** enumeration member from the following table:</span></span>

|<span data-ttu-id="53684-136">Typ hodnoty</span><span class="sxs-lookup"><span data-stu-id="53684-136">PropertyType Value</span></span>|<span data-ttu-id="53684-137">Význam</span><span class="sxs-lookup"><span data-stu-id="53684-137">Meaning</span></span>|
|----------------------|-----------|
|<span data-ttu-id="53684-138">Binární</span><span class="sxs-lookup"><span data-stu-id="53684-138">Binary</span></span>|<span data-ttu-id="53684-139">Binární data</span><span class="sxs-lookup"><span data-stu-id="53684-139">Binary data</span></span>|
|<span data-ttu-id="53684-140">DWord</span><span class="sxs-lookup"><span data-stu-id="53684-140">DWord</span></span>|<span data-ttu-id="53684-141">Číslo, které je platný typ UInt32</span><span class="sxs-lookup"><span data-stu-id="53684-141">A number that is a valid UInt32</span></span>|
|<span data-ttu-id="53684-142">ExpandString</span><span class="sxs-lookup"><span data-stu-id="53684-142">ExpandString</span></span>|<span data-ttu-id="53684-143">Řetězec, který může obsahovat proměnné prostředí, které jsou dynamicky rozbaleny</span><span class="sxs-lookup"><span data-stu-id="53684-143">A string that can contain environment variables that are dynamically expanded</span></span>|
|<span data-ttu-id="53684-144">Řetězci FixedLength multiString</span><span class="sxs-lookup"><span data-stu-id="53684-144">MultiString</span></span>|<span data-ttu-id="53684-145">Víceřádkový řetězec</span><span class="sxs-lookup"><span data-stu-id="53684-145">A multiline string</span></span>|
|<span data-ttu-id="53684-146">Řetězec</span><span class="sxs-lookup"><span data-stu-id="53684-146">String</span></span>|<span data-ttu-id="53684-147">Libovolnou hodnotou řetězce</span><span class="sxs-lookup"><span data-stu-id="53684-147">Any string value</span></span>|
|<span data-ttu-id="53684-148">QWord</span><span class="sxs-lookup"><span data-stu-id="53684-148">QWord</span></span>|<span data-ttu-id="53684-149">8 bajtů binárních dat</span><span class="sxs-lookup"><span data-stu-id="53684-149">8 bytes of binary data</span></span>|

> [!NOTE]
> <span data-ttu-id="53684-150">Můžete přidat položku registru do víc umístění tak, že zadáte pole hodnot **cesta** parametr:</span><span class="sxs-lookup"><span data-stu-id="53684-150">You can add a registry entry to multiple locations by specifying an array of values for the **Path** parameter:</span></span>

```powershell
New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion, HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -PropertyType String -Value $PSHome
```

<span data-ttu-id="53684-151">Můžete také přepsat existující hodnotu položky registru tak, že přidáte **platnost** parametr k libovolnému **New-ItemProperty** příkazu.</span><span class="sxs-lookup"><span data-stu-id="53684-151">You can also overwrite a pre-existing registry entry value by adding the **Force** parameter to any **New-ItemProperty** command.</span></span>

### <a name="renaming-registry-entries"></a><span data-ttu-id="53684-152">Přejmenování položky registru</span><span class="sxs-lookup"><span data-stu-id="53684-152">Renaming Registry Entries</span></span>

<span data-ttu-id="53684-153">Přejmenovat **PowerShellPath** položku "PSHome," použití **Rename-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="53684-153">To rename the **PowerShellPath** entry to "PSHome," use **Rename-ItemProperty**:</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome
```

<span data-ttu-id="53684-154">Chcete-li zobrazit hodnotu byl přejmenován, přidejte **PassThru** parametr k příkazu.</span><span class="sxs-lookup"><span data-stu-id="53684-154">To display the renamed value, add the **PassThru** parameter to the command.</span></span>

```powershell
Rename-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath -NewName PSHome -passthru
```

### <a name="deleting-registry-entries"></a><span data-ttu-id="53684-155">Odstranění položky registru</span><span class="sxs-lookup"><span data-stu-id="53684-155">Deleting Registry Entries</span></span>

<span data-ttu-id="53684-156">Chcete-li odstranit PSHome i PowerShellPath položky registru, použijte **Remove-ItemProperty**:</span><span class="sxs-lookup"><span data-stu-id="53684-156">To delete both the PSHome and PowerShellPath registry entries, use **Remove-ItemProperty**:</span></span>

```powershell
Remove-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PSHome
Remove-ItemProperty -Path HKCU:\SOFTWARE\Microsoft\Windows\CurrentVersion -Name PowerShellPath
```
---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Manipulace s nimi přímo položky"
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: d9aa95dcb0da2e8203cbe32d64b95bf33d914166
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="manipulating-items-directly"></a><span data-ttu-id="2c308-103">Manipulace s nimi přímo položky</span><span class="sxs-lookup"><span data-stu-id="2c308-103">Manipulating Items Directly</span></span>
<span data-ttu-id="2c308-104">Prvky, které se zobrazí v prostředí Windows PowerShell jednotky, jako jsou soubory a složky v jednotky systému souborů a klíčů registru v registru jednotky prostředí Windows PowerShell, se nazývají *položky* v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c308-104">The elements that you see in Windows PowerShell drives, such as the files and folders in the file system drives, and the registry keys in the Windows PowerShell registry drives, are called *items* in Windows PowerShell.</span></span> <span data-ttu-id="2c308-105">Rutiny pro práci s nimi položky mají podstatným jménem **položky** v jejich názvy.</span><span class="sxs-lookup"><span data-stu-id="2c308-105">The cmdlets for working with them item have the noun **Item** in their names.</span></span>

<span data-ttu-id="2c308-106">Výstup **Get-Command - podstatné jméno položky** příkaz zobrazí, že jsou devět položky rutiny prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c308-106">The output of the **Get-Command -Noun Item** command shows that there are nine Windows PowerShell item cmdlets.</span></span>

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

### <a name="creating-new-items-new-item"></a><span data-ttu-id="2c308-107">Vytvoření nové položky (nová položka)</span><span class="sxs-lookup"><span data-stu-id="2c308-107">Creating New Items (New-Item)</span></span>
<span data-ttu-id="2c308-108">Chcete-li vytvořit novou položku v systému souborů, použijte **nové položky** rutiny.</span><span class="sxs-lookup"><span data-stu-id="2c308-108">To create a new item in the file system, use the **New-Item** cmdlet.</span></span> <span data-ttu-id="2c308-109">Zahrnout **cesta** parametr s cestou k položce a **ItemType** parametr s hodnotou "soubor" nebo "adresář".</span><span class="sxs-lookup"><span data-stu-id="2c308-109">Include the **Path** parameter with path to the item, and the **ItemType** parameter with a value of "file" or "directory".</span></span>

<span data-ttu-id="2c308-110">Například vytvořte nový adresář s názvem "New.Directory"in jednotce C:\\dočasné složky, zadejte:</span><span class="sxs-lookup"><span data-stu-id="2c308-110">For example, to create a new directory named "New.Directory"in the C:\\Temp directory,  type:</span></span>

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

<span data-ttu-id="2c308-111">Pokud chcete vytvořit soubor, změňte hodnotu **ItemType** parametr "soubor".</span><span class="sxs-lookup"><span data-stu-id="2c308-111">To create a file, change the value of the **ItemType** parameter to "file".</span></span> <span data-ttu-id="2c308-112">Například pokud chcete vytvořit soubor s názvem "file1.txt" v adresáři New.Directory, zadejte:</span><span class="sxs-lookup"><span data-stu-id="2c308-112">For example, to create a file named "file1.txt" in the New.Directory directory, type:</span></span>

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

<span data-ttu-id="2c308-113">Chcete-li vytvořit nový klíč registru můžete použít stejný postup.</span><span class="sxs-lookup"><span data-stu-id="2c308-113">You can use the same technique to create a new registry key.</span></span> <span data-ttu-id="2c308-114">Klíč registru je ve skutečnosti jednodušší vytvořit, protože klíč je jediným typem položku v registru systému Windows.</span><span class="sxs-lookup"><span data-stu-id="2c308-114">In fact, a registry key is easier to create because the only item type in the Windows registry is a key.</span></span> <span data-ttu-id="2c308-115">(Položky registru jsou položky *vlastnosti*.) Například pokud chcete vytvořit klíč s názvem "_Test" v podklíči CurrentVersion, zadejte:</span><span class="sxs-lookup"><span data-stu-id="2c308-115">(Registry entries are item *properties*.) For example, to create a key named "_Test" in the CurrentVersion subkey, type:</span></span>

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

<span data-ttu-id="2c308-116">Pokud zadáte cestu registru, nezapomeňte zahrnout dvojtečkou (**:**) v prostředí Windows PowerShell jednotka názvy, HKLM: a HKCU:.</span><span class="sxs-lookup"><span data-stu-id="2c308-116">When typing a registry path, be sure to include the colon (**:**) in the Windows PowerShell drive names, HKLM: and HKCU:.</span></span> <span data-ttu-id="2c308-117">Bez dvojtečky prostředí Windows PowerShell nelze rozpoznat název jednotky v cestě.</span><span class="sxs-lookup"><span data-stu-id="2c308-117">Without the colon, Windows PowerShell does not recognize the drive name in the path.</span></span>

### <a name="why-registry-values-are-not-items"></a><span data-ttu-id="2c308-118">Proč hodnoty registru, které nejsou žádné položky</span><span class="sxs-lookup"><span data-stu-id="2c308-118">Why Registry Values are not Items</span></span>
<span data-ttu-id="2c308-119">Při použití **Get-ChildItem** rutiny a vyhledání položek v klíči registru a nikdy se zobrazí skutečné registru nebo jejich hodnot.</span><span class="sxs-lookup"><span data-stu-id="2c308-119">When you use the **Get-ChildItem** cmdlet to find the items in a registry key, you will never see actual registry entries or their values.</span></span>

<span data-ttu-id="2c308-120">Například klíč registru **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion\\spustit** obvykle obsahuje několik položky registru které představují aplikace, které jsou spuštěny při spuštění systému.</span><span class="sxs-lookup"><span data-stu-id="2c308-120">For example, the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** usually contains several registry entries that represent applications that run when the system starts.</span></span>

<span data-ttu-id="2c308-121">Ale při použití **Get-ChildItem** a hledat podřízené položky v klíči, uvidíte je **OptionalComponents** podklíčů klíče:</span><span class="sxs-lookup"><span data-stu-id="2c308-121">However, when you use **Get-ChildItem** to look for child items in the key, all you will see is the **OptionalComponents** subkey of the key:</span></span>

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run
   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

<span data-ttu-id="2c308-122">Přestože by bylo vhodnější položky registru považovat za položky, nelze zadat cestu k položce registru způsobem, který zajistí, že bude jedinečný.</span><span class="sxs-lookup"><span data-stu-id="2c308-122">Although it would be convenient to treat registry entries as items, you cannot specify a path to a registry entry in a way that ensures that it is unique.</span></span> <span data-ttu-id="2c308-123">Zápis cesty se nerozlišují podklíč registru s názvem **spustit** a **(výchozí)** položky registru v **spustit** podklíč.</span><span class="sxs-lookup"><span data-stu-id="2c308-123">The path notation does not distinguish between the registry subkey named **Run** and the **(Default)** registry entry in the **Run** subkey.</span></span> <span data-ttu-id="2c308-124">Navíc vzhledem k tomu, že názvy položek registru může obsahovat znak zpětného lomítka (**\\**), pokud regsitry položky byly položek, zápis cesty nelze použít k rozlišení položku registru s názvem  **Windows\\CurrentVersion\\spustit** z podklíče, který je umístěný v této cestě.</span><span class="sxs-lookup"><span data-stu-id="2c308-124">Furthermore, because registry entry names can contain the backslash character (**\\**), if regsitry entries were items, then you could not use the path notation to distinguish a registry entry named **Windows\\CurrentVersion\\Run** from the subkey that is located in that path.</span></span>

### <a name="renaming-existing-items-rename-item"></a><span data-ttu-id="2c308-125">Přejmenování existující položky (přejmenování položky)</span><span class="sxs-lookup"><span data-stu-id="2c308-125">Renaming Existing Items (Rename-Item)</span></span>
<span data-ttu-id="2c308-126">Chcete-li změnit název souboru nebo složky, použijte **přejmenování položky** rutiny.</span><span class="sxs-lookup"><span data-stu-id="2c308-126">To change the name of a file or folder, use the **Rename-Item** cmdlet.</span></span> <span data-ttu-id="2c308-127">Tento příkaz změní název **file1.txt** do souboru **fileOne.txt**.</span><span class="sxs-lookup"><span data-stu-id="2c308-127">The following command changes the name of the **file1.txt** file to **fileOne.txt**.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

<span data-ttu-id="2c308-128">**Přejmenování položky** rutiny můžete změnit název souboru nebo složce, ale nemůžete ho přesunout položku.</span><span class="sxs-lookup"><span data-stu-id="2c308-128">The **Rename-Item** cmdlet can change the name of a file or a folder, but it cannot move an item.</span></span> <span data-ttu-id="2c308-129">Následující příkaz selže, protože se pokouší přesunout soubor z adresáře New.Directory do dočasné složky.</span><span class="sxs-lookup"><span data-stu-id="2c308-129">The following command fails because it attempts to move the file from the New.Directory directory to the Temp directory.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### <a name="moving-items-move-item"></a><span data-ttu-id="2c308-130">Přesouvání položek (Move-Item)</span><span class="sxs-lookup"><span data-stu-id="2c308-130">Moving Items (Move-Item)</span></span>
<span data-ttu-id="2c308-131">Chcete-li přesunout soubor nebo složku, použijte **přesunout položku** rutiny.</span><span class="sxs-lookup"><span data-stu-id="2c308-131">To move a file or folder, use the **Move-Item** cmdlet.</span></span>

<span data-ttu-id="2c308-132">Například následující příkaz přesune adresáři New.Directory z jednotce C:\\dočasný adresář na kořenové jednotce C:.</span><span class="sxs-lookup"><span data-stu-id="2c308-132">For example, the following command moves the New.Directory directory from the C:\\temp directory to the root of the C: drive.</span></span> <span data-ttu-id="2c308-133">Chcete-li ověřit, že položka byla přesunuta, zahrňte **PassThru** parametr **přesunout položku** rutiny.</span><span class="sxs-lookup"><span data-stu-id="2c308-133">To verify that the item was moved, include the **PassThru** parameter of the **Move-Item** cmdlet.</span></span> <span data-ttu-id="2c308-134">Bez **Passthru**, **přesunout položku** rutiny nezobrazí žádné výsledky.</span><span class="sxs-lookup"><span data-stu-id="2c308-134">Without **Passthru**, the **Move-Item** cmdlet does not display any results.</span></span>

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### <a name="copying-items-copy-item"></a><span data-ttu-id="2c308-135">Kopírování položek (Copy-Item)</span><span class="sxs-lookup"><span data-stu-id="2c308-135">Copying Items (Copy-Item)</span></span>
<span data-ttu-id="2c308-136">Pokud jste obeznámeni s operace kopírování v jiné prostředí, můžete zjistit, chování **Copy-Item** rutiny v prostředí Windows PowerShell jako neobvyklé.</span><span class="sxs-lookup"><span data-stu-id="2c308-136">If you are familiar with the copy operations in other shells, you might find the behavior of the **Copy-Item** cmdlet in Windows PowerShell to be unusual.</span></span> <span data-ttu-id="2c308-137">Při kopírování položku z jednoho umístění do druhého, Copy-Item nekopíruje obsah ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="2c308-137">When you copy an item from one location to another, Copy-Item does not copy its contents by default.</span></span>

<span data-ttu-id="2c308-138">Například pokud zkopírujete **New.Directory** adresář z jednotky C: na jednotce C:\\dočasného adresáře příkazu úspěšné, ale soubory v adresáři New.Directory nebudou zkopírovány.</span><span class="sxs-lookup"><span data-stu-id="2c308-138">For example, if you copy the **New.Directory** directory from the C: drive to the C:\\temp directory, the command succeeds, but the files in the New.Directory directory are not copied.</span></span>

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp
```

<span data-ttu-id="2c308-139">Pokud chcete zobrazovat obsah **C:\\temp\\New.Directory**, zjistíte, že neobsahuje žádné soubory:</span><span class="sxs-lookup"><span data-stu-id="2c308-139">If you display the contents of **C:\\temp\\New.Directory**, you will find that it contains no files:</span></span>

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

<span data-ttu-id="2c308-140">Proč není **Copy-Item** rutiny zkopírujte obsah do nového umístění?</span><span class="sxs-lookup"><span data-stu-id="2c308-140">Why doesn't the **Copy-Item** cmdlet copy the contents to the new location?</span></span>

<span data-ttu-id="2c308-141">**Copy-Item** rutiny byla navržená tak, aby být obecný; není právě pro kopírování souborů a složek.</span><span class="sxs-lookup"><span data-stu-id="2c308-141">The **Copy-Item** cmdlet was designed to be generic; it is not just for copying files and folders.</span></span> <span data-ttu-id="2c308-142">Navíc i v případě, že kopírování souborů a složek, můžete chtít kopírovat pouze kontejneru a není položky v něm.</span><span class="sxs-lookup"><span data-stu-id="2c308-142">Also, even when copying files and folders, you might want to copy only the container and not the items within it.</span></span>

<span data-ttu-id="2c308-143">Kopírovat veškerý obsah složky, zahrňte **Recurse** parametr **Copy-Item** rutiny v příkazu.</span><span class="sxs-lookup"><span data-stu-id="2c308-143">To copy all of the contents of a folder, include the **Recurse** parameter of the **Copy-Item** cmdlet in the command.</span></span> <span data-ttu-id="2c308-144">Pokud jste již zkopírovali adresáři bez obsahu, přidejte **Force** parametr, který můžete přepsat prázdné složky.</span><span class="sxs-lookup"><span data-stu-id="2c308-144">If you have already copied the directory without its contents, add the **Force** parameter, which allows you to overwrite the empty folder.</span></span>

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

### <a name="deleting-items-remove-item"></a><span data-ttu-id="2c308-145">Odstraňování položek (Remove-Item)</span><span class="sxs-lookup"><span data-stu-id="2c308-145">Deleting Items (Remove-Item)</span></span>
<span data-ttu-id="2c308-146">Chcete-li odstranit soubory a složky, použijte **odebrat položky** rutiny.</span><span class="sxs-lookup"><span data-stu-id="2c308-146">To delete files and folders, use the **Remove-Item** cmdlet.</span></span> <span data-ttu-id="2c308-147">Rutiny prostředí Windows PowerShell, jako například **odebrat položky**, který způsobit významné, nedá se vrátit změny se často výzvu k potvrzení, když zadáte jeho příkazy.</span><span class="sxs-lookup"><span data-stu-id="2c308-147">Windows PowerShell cmdlets, such as **Remove-Item**, that can make significant, irreversible changes will often prompt for confirmation when you enter its commands.</span></span> <span data-ttu-id="2c308-148">Například pokud se pokusíte odebrat **New.Directory** složku, zobrazí se výzva k potvrzení příkazu, protože složka obsahuje soubory:</span><span class="sxs-lookup"><span data-stu-id="2c308-148">For example, if you try to remove the **New.Directory** folder, you will be prompted to confirm the command, because the folder contains files:</span></span>

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="2c308-149">Protože **Ano** je výchozí odpověď, a odstranit složku a její soubory, stiskněte **Enter** klíč.</span><span class="sxs-lookup"><span data-stu-id="2c308-149">Because **Yes** is the default response, to delete the folder and its files, press the **Enter** key.</span></span> <span data-ttu-id="2c308-150">Chcete-li odebrat složku bez potvrzení, použijte **-Recurse** parametr.</span><span class="sxs-lookup"><span data-stu-id="2c308-150">To remove the folder without confirming, use the **-Recurse** parameter.</span></span>

```
PS> Remove-Item C:\temp\New.Directory -Recurse
```

### <a name="executing-items-invoke-item"></a><span data-ttu-id="2c308-151">Provádění položky (Invoke-Item)</span><span class="sxs-lookup"><span data-stu-id="2c308-151">Executing Items (Invoke-Item)</span></span>
<span data-ttu-id="2c308-152">Používá prostředí Windows PowerShell **Invoke-Item** rutina k provedení výchozí akce pro soubor nebo složku.</span><span class="sxs-lookup"><span data-stu-id="2c308-152">Windows PowerShell uses the **Invoke-Item** cmdlet to perform a default action for a file or folder.</span></span> <span data-ttu-id="2c308-153">Tato výchozí akce je dáno výchozí obslužnou rutinu aplikace v registru; účinek je stejný jako v případě, že dvakrát kliknete na položky v Průzkumníku souborů.</span><span class="sxs-lookup"><span data-stu-id="2c308-153">This default action is determined by the default application handler in the registry; the effect is the same as if you double-click the item in File Explorer.</span></span>

<span data-ttu-id="2c308-154">Předpokládejme například, že spustíte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="2c308-154">For example, suppose you run the following command:</span></span>

```
PS> Invoke-Item C:\WINDOWS
```

<span data-ttu-id="2c308-155">Okno Průzkumníka, který je umístěný v C:\\se zobrazí Windows, stejně jako kdyby měl dvakrát kliknuli jednotce C:\\složka systému Windows.</span><span class="sxs-lookup"><span data-stu-id="2c308-155">An Explorer window that is located in C:\\Windows appears, just as if you had double-clicked the C:\\Windows folder.</span></span>

<span data-ttu-id="2c308-156">Pokud jste vyvolání **Boot.ini** souboru v systému starší než Windows Vista:</span><span class="sxs-lookup"><span data-stu-id="2c308-156">If you invoke the **Boot.ini** file on a system prior to Windows Vista:</span></span>

```
PS> Invoke-Item C:\boot.ini
```

<span data-ttu-id="2c308-157">Pokud je typ souboru .ini přidružený Poznámkový blok, soubor boot.ini se otevře v poznámkovém bloku.</span><span class="sxs-lookup"><span data-stu-id="2c308-157">If the .ini file type is associated with Notepad, the boot.ini file opens in Notepad.</span></span>


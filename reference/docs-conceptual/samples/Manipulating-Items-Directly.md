---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Přímá manipulace s položkami
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: 688f9194bd16793331325999c69e88df3e94c976
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404066"
---
# <a name="manipulating-items-directly"></a><span data-ttu-id="d000a-103">Přímá manipulace s položkami</span><span class="sxs-lookup"><span data-stu-id="d000a-103">Manipulating Items Directly</span></span>

<span data-ttu-id="d000a-104">Prvky, které se zobrazí v prostředí Windows PowerShell jednotky, jako jsou soubory a složkami v jednotky systému souborů a klíči registru v registru jednotek Windows Powershellu, se nazývají *položky* v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d000a-104">The elements that you see in Windows PowerShell drives, such as the files and folders in the file system drives, and the registry keys in the Windows PowerShell registry drives, are called *items* in Windows PowerShell.</span></span> <span data-ttu-id="d000a-105">Rutiny pro práci s nimi položky mají podstatným jménem **položky** v jejich názvy.</span><span class="sxs-lookup"><span data-stu-id="d000a-105">The cmdlets for working with them item have the noun **Item** in their names.</span></span>

<span data-ttu-id="d000a-106">Výstup **Get-Command - podstatné jméno položky** příkaz znázorňuje, že jsou devět položky rutiny prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d000a-106">The output of the **Get-Command -Noun Item** command shows that there are nine Windows PowerShell item cmdlets.</span></span>

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

### <a name="creating-new-items-new-item"></a><span data-ttu-id="d000a-107">Vytvoření nové položky (nová položka)</span><span class="sxs-lookup"><span data-stu-id="d000a-107">Creating New Items (New-Item)</span></span>

<span data-ttu-id="d000a-108">Chcete-li vytvořit novou položku v systému souborů, použijte **New-Item** rutiny.</span><span class="sxs-lookup"><span data-stu-id="d000a-108">To create a new item in the file system, use the **New-Item** cmdlet.</span></span> <span data-ttu-id="d000a-109">Zahrnout **cesta** parametr s cestou k položce a **ItemType** parametr s hodnotou "file" nebo "directory".</span><span class="sxs-lookup"><span data-stu-id="d000a-109">Include the **Path** parameter with path to the item, and the **ItemType** parameter with a value of "file" or "directory".</span></span>

<span data-ttu-id="d000a-110">Například, chcete-li vytvořit nový adresář s názvem "New.Directory"in C:\\dočasný adresář, zadejte:</span><span class="sxs-lookup"><span data-stu-id="d000a-110">For example, to create a new directory named "New.Directory"in the C:\\Temp directory,  type:</span></span>

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

<span data-ttu-id="d000a-111">Vytvoření souboru, změňte hodnotu **ItemType** parametr "file".</span><span class="sxs-lookup"><span data-stu-id="d000a-111">To create a file, change the value of the **ItemType** parameter to "file".</span></span> <span data-ttu-id="d000a-112">Například pokud chcete vytvořit soubor s názvem "file1.txt" v adresáři New.Directory, zadejte:</span><span class="sxs-lookup"><span data-stu-id="d000a-112">For example, to create a file named "file1.txt" in the New.Directory directory, type:</span></span>

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

<span data-ttu-id="d000a-113">Stejný postup můžete použít k vytvoření nového klíče registru.</span><span class="sxs-lookup"><span data-stu-id="d000a-113">You can use the same technique to create a new registry key.</span></span> <span data-ttu-id="d000a-114">Ve skutečnosti klíč registru je snazší vytvářet, protože klíč je jediným typem položky v registru Windows.</span><span class="sxs-lookup"><span data-stu-id="d000a-114">In fact, a registry key is easier to create because the only item type in the Windows registry is a key.</span></span> <span data-ttu-id="d000a-115">(Položky registru jsou položky *vlastnosti*.) Například pokud chcete vytvořit klíč s názvem "_testovat" v podklíči CurrentVersion, zadejte:</span><span class="sxs-lookup"><span data-stu-id="d000a-115">(Registry entries are item *properties*.) For example, to create a key named "_Test" in the CurrentVersion subkey, type:</span></span>

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

<span data-ttu-id="d000a-116">Pokud zadáte cestu k registru, nezapomeňte zahrnout dvojtečka (**:**) v prostředí Windows PowerShell jednotka názvy, HKLM: a HKCU:.</span><span class="sxs-lookup"><span data-stu-id="d000a-116">When typing a registry path, be sure to include the colon (**:**) in the Windows PowerShell drive names, HKLM: and HKCU:.</span></span> <span data-ttu-id="d000a-117">Bez dvojtečky prostředí Windows PowerShell nedokáže rozpoznat název jednotky v cestě.</span><span class="sxs-lookup"><span data-stu-id="d000a-117">Without the colon, Windows PowerShell does not recognize the drive name in the path.</span></span>

### <a name="why-registry-values-are-not-items"></a><span data-ttu-id="d000a-118">Proč hodnoty registru nejsou položky</span><span class="sxs-lookup"><span data-stu-id="d000a-118">Why Registry Values are not Items</span></span>

<span data-ttu-id="d000a-119">Při použití **Get-ChildItem** rutiny a vyhledání položek v klíči registru a nikdy se zobrazí položky skutečné registru nebo jejich hodnoty.</span><span class="sxs-lookup"><span data-stu-id="d000a-119">When you use the **Get-ChildItem** cmdlet to find the items in a registry key, you will never see actual registry entries or their values.</span></span>

<span data-ttu-id="d000a-120">Například klíč registru **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion\\spustit** obvykle obsahuje několik položek registru které představují aplikace, které běží při spuštění systému.</span><span class="sxs-lookup"><span data-stu-id="d000a-120">For example, the registry key **HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Run** usually contains several registry entries that represent applications that run when the system starts.</span></span>

<span data-ttu-id="d000a-121">Ale při použití **Get-ChildItem** hledání podřízených položek v klíči, všechny uvidíte je **OptionalComponents** podklíčů klíče:</span><span class="sxs-lookup"><span data-stu-id="d000a-121">However, when you use **Get-ChildItem** to look for child items in the key, all you will see is the **OptionalComponents** subkey of the key:</span></span>

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

<span data-ttu-id="d000a-122">I když bylo by vhodné položky registru považovat za položky, nelze zadat cestu k položce registru způsobem, který zajistí, že se jedná o jedinečný.</span><span class="sxs-lookup"><span data-stu-id="d000a-122">Although it would be convenient to treat registry entries as items, you cannot specify a path to a registry entry in a way that ensures that it is unique.</span></span> <span data-ttu-id="d000a-123">Cesta notation nerozlišuje mezi podklíč registru s názvem **spustit** a **(výchozí)** položky registru v **spustit** podklíči.</span><span class="sxs-lookup"><span data-stu-id="d000a-123">The path notation does not distinguish between the registry subkey named **Run** and the **(Default)** registry entry in the **Run** subkey.</span></span> <span data-ttu-id="d000a-124">Navíc vzhledem k tomu, že názvy položek registru může obsahovat znak zpětného lomítka (**\\**), kdyby položky registru položek, cesta notation nejde použít k rozlišení položku registru s názvem  **Windows\\CurrentVersion\\spustit** z podklíče, který se nachází v této cestě.</span><span class="sxs-lookup"><span data-stu-id="d000a-124">Furthermore, because registry entry names can contain the backslash character (**\\**), if regsitry entries were items, then you could not use the path notation to distinguish a registry entry named **Windows\\CurrentVersion\\Run** from the subkey that is located in that path.</span></span>

### <a name="renaming-existing-items-rename-item"></a><span data-ttu-id="d000a-125">Přejmenování existujících položek (přejmenování položek)</span><span class="sxs-lookup"><span data-stu-id="d000a-125">Renaming Existing Items (Rename-Item)</span></span>

<span data-ttu-id="d000a-126">Chcete-li změnit název souboru nebo složky, použijte **přejmenovat položku** rutiny.</span><span class="sxs-lookup"><span data-stu-id="d000a-126">To change the name of a file or folder, use the **Rename-Item** cmdlet.</span></span> <span data-ttu-id="d000a-127">Následující příkaz změní název **file1.txt** do souboru **fileOne.txt**.</span><span class="sxs-lookup"><span data-stu-id="d000a-127">The following command changes the name of the **file1.txt** file to **fileOne.txt**.</span></span>

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

<span data-ttu-id="d000a-128">**Přejmenovat položku** rutiny můžete změnit název souboru nebo složky, ale nelze jej přesunout položku.</span><span class="sxs-lookup"><span data-stu-id="d000a-128">The **Rename-Item** cmdlet can change the name of a file or a folder, but it cannot move an item.</span></span> <span data-ttu-id="d000a-129">Následující příkaz se nezdaří, protože se pokusí přesunout soubor z adresáře New.Directory do svého adresáře Temp.</span><span class="sxs-lookup"><span data-stu-id="d000a-129">The following command fails because it attempts to move the file from the New.Directory directory to the Temp directory.</span></span>

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### <a name="moving-items-move-item"></a><span data-ttu-id="d000a-130">Přesun položek (přesunutí položek)</span><span class="sxs-lookup"><span data-stu-id="d000a-130">Moving Items (Move-Item)</span></span>

<span data-ttu-id="d000a-131">Chcete-li přesunout soubor nebo složku, použijte **přesunout položku** rutiny.</span><span class="sxs-lookup"><span data-stu-id="d000a-131">To move a file or folder, use the **Move-Item** cmdlet.</span></span>

<span data-ttu-id="d000a-132">Například následující příkaz přesune New.Directory adresáře C:\\dočasný adresář na kořenové jednotce C:.</span><span class="sxs-lookup"><span data-stu-id="d000a-132">For example, the following command moves the New.Directory directory from the C:\\temp directory to the root of the C: drive.</span></span> <span data-ttu-id="d000a-133">Chcete-li ověřit, že položka byla přesunuta, zahrňte **PassThru** parametr **přesunout položku** rutiny.</span><span class="sxs-lookup"><span data-stu-id="d000a-133">To verify that the item was moved, include the **PassThru** parameter of the **Move-Item** cmdlet.</span></span> <span data-ttu-id="d000a-134">Bez **Passthru**, **přesunout položku** rutiny nezobrazí žádné výsledky.</span><span class="sxs-lookup"><span data-stu-id="d000a-134">Without **Passthru**, the **Move-Item** cmdlet does not display any results.</span></span>

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### <a name="copying-items-copy-item"></a><span data-ttu-id="d000a-135">Kopírování položek (Copy-Item)</span><span class="sxs-lookup"><span data-stu-id="d000a-135">Copying Items (Copy-Item)</span></span>

<span data-ttu-id="d000a-136">Pokud jste se seznámili s operací kopírování v jiné prostředí, můžete se setkat chování **Copy-Item** rutiny v prostředí Windows PowerShell na neobvyklé.</span><span class="sxs-lookup"><span data-stu-id="d000a-136">If you are familiar with the copy operations in other shells, you might find the behavior of the **Copy-Item** cmdlet in Windows PowerShell to be unusual.</span></span> <span data-ttu-id="d000a-137">Při kopírování položky z jednoho umístění do druhého, Copy-Item nekopíruje obsah ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="d000a-137">When you copy an item from one location to another, Copy-Item does not copy its contents by default.</span></span>

<span data-ttu-id="d000a-138">Například pokud kopírujete **New.Directory** z jednotky C: do C: adresáře\\dočasný adresář, příkaz proběhne úspěšně, ale soubory v adresáři New.Directory nejsou zkopírovány.</span><span class="sxs-lookup"><span data-stu-id="d000a-138">For example, if you copy the **New.Directory** directory from the C: drive to the C:\\temp directory, the command succeeds, but the files in the New.Directory directory are not copied.</span></span>

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

<span data-ttu-id="d000a-139">Pokud zobrazíte obsah **C:\\temp\\New.Directory**, zjistíte, že neobsahuje žádné soubory:</span><span class="sxs-lookup"><span data-stu-id="d000a-139">If you display the contents of **C:\\temp\\New.Directory**, you will find that it contains no files:</span></span>

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

<span data-ttu-id="d000a-140">Proč není **Copy-Item** rutiny zkopírovat obsah do nového umístění?</span><span class="sxs-lookup"><span data-stu-id="d000a-140">Why doesn't the **Copy-Item** cmdlet copy the contents to the new location?</span></span>

<span data-ttu-id="d000a-141">**Copy-Item** rutiny byla navržena jako obecný; není jenom pro kopírování souborů a složek.</span><span class="sxs-lookup"><span data-stu-id="d000a-141">The **Copy-Item** cmdlet was designed to be generic; it is not just for copying files and folders.</span></span> <span data-ttu-id="d000a-142">Navíc i v případě, že kopírování souborů a složek, můžete zkopírovat pouze kontejneru a ne na položky v něm.</span><span class="sxs-lookup"><span data-stu-id="d000a-142">Also, even when copying files and folders, you might want to copy only the container and not the items within it.</span></span>

<span data-ttu-id="d000a-143">Kopírovat veškerý obsah do složky, zahrňte **Recurse** parametr **Copy-Item** rutiny v příkazu.</span><span class="sxs-lookup"><span data-stu-id="d000a-143">To copy all of the contents of a folder, include the **Recurse** parameter of the **Copy-Item** cmdlet in the command.</span></span> <span data-ttu-id="d000a-144">Pokud už jste zkopírovali adresáře, aniž by jeho obsah, přidejte **platnost** parametr, který umožňuje přepsat prázdné složky.</span><span class="sxs-lookup"><span data-stu-id="d000a-144">If you have already copied the directory without its contents, add the **Force** parameter, which allows you to overwrite the empty folder.</span></span>

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

### <a name="deleting-items-remove-item"></a><span data-ttu-id="d000a-145">Odstranění položek (Remove-Item)</span><span class="sxs-lookup"><span data-stu-id="d000a-145">Deleting Items (Remove-Item)</span></span>

<span data-ttu-id="d000a-146">Chcete-li odstranit soubory a složky, použijte **Remove-Item** rutiny.</span><span class="sxs-lookup"><span data-stu-id="d000a-146">To delete files and folders, use the **Remove-Item** cmdlet.</span></span> <span data-ttu-id="d000a-147">Rutiny prostředí Windows PowerShell, jako například **odebrat položku**, můžete díky významné, nevratné změny se často výzvu k potvrzení, když zadáte jeho příkazy.</span><span class="sxs-lookup"><span data-stu-id="d000a-147">Windows PowerShell cmdlets, such as **Remove-Item**, that can make significant, irreversible changes will often prompt for confirmation when you enter its commands.</span></span> <span data-ttu-id="d000a-148">Například, pokud se pokusíte odebrat **New.Directory** složky, budete vyzváni k potvrzení příkazu, protože složka obsahuje soubory:</span><span class="sxs-lookup"><span data-stu-id="d000a-148">For example, if you try to remove the **New.Directory** folder, you will be prompted to confirm the command, because the folder contains files:</span></span>

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="d000a-149">Protože **Ano** je výchozí odpovědí, odstraňte složku a její soubory, stiskněte **Enter** klíč.</span><span class="sxs-lookup"><span data-stu-id="d000a-149">Because **Yes** is the default response, to delete the folder and its files, press the **Enter** key.</span></span> <span data-ttu-id="d000a-150">Chcete-li odebrat složku bez potvrzení, použijte **-Recurse** parametru.</span><span class="sxs-lookup"><span data-stu-id="d000a-150">To remove the folder without confirming, use the **-Recurse** parameter.</span></span>

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

### <a name="executing-items-invoke-item"></a><span data-ttu-id="d000a-151">Provádění položky (Invoke-Item)</span><span class="sxs-lookup"><span data-stu-id="d000a-151">Executing Items (Invoke-Item)</span></span>

<span data-ttu-id="d000a-152">Používá prostředí Windows PowerShell **Invoke-Item** rutina k provedení výchozí akce pro soubor nebo složku.</span><span class="sxs-lookup"><span data-stu-id="d000a-152">Windows PowerShell uses the **Invoke-Item** cmdlet to perform a default action for a file or folder.</span></span> <span data-ttu-id="d000a-153">Tato výchozí akce je určená výchozí obslužnou rutinu aplikace v registru. efekt je stejný, jako kdyby jste dvakrát klikněte na položku v Průzkumníku souborů.</span><span class="sxs-lookup"><span data-stu-id="d000a-153">This default action is determined by the default application handler in the registry; the effect is the same as if you double-click the item in File Explorer.</span></span>

<span data-ttu-id="d000a-154">Předpokládejme například, že spustíte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="d000a-154">For example, suppose you run the following command:</span></span>

```powershell
Invoke-Item C:\WINDOWS
```

<span data-ttu-id="d000a-155">Okno Průzkumníka, který se nachází v C:\\se zobrazí Windows, stejně jako v případě, kdyby jste dvakrát kliknuli C:\\složku Windows.</span><span class="sxs-lookup"><span data-stu-id="d000a-155">An Explorer window that is located in C:\\Windows appears, just as if you had double-clicked the C:\\Windows folder.</span></span>

<span data-ttu-id="d000a-156">Pokud vyvoláte **Boot.ini** souboru v systému starší než Windows Vista:</span><span class="sxs-lookup"><span data-stu-id="d000a-156">If you invoke the **Boot.ini** file on a system prior to Windows Vista:</span></span>

```powershell
Invoke-Item C:\boot.ini
```

<span data-ttu-id="d000a-157">Pokud typ souboru INI souvisí s Poznámkový blok, soubor boot.ini se otevře v poznámkovém bloku.</span><span class="sxs-lookup"><span data-stu-id="d000a-157">If the .ini file type is associated with Notepad, the boot.ini file opens in Notepad.</span></span>
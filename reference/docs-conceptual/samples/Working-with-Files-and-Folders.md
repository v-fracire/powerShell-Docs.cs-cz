---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce se soubory a složkami
ms.assetid: c0ceb96b-e708-45f3-803b-d1f61a48f4c1
ms.openlocfilehash: a8d57a1c269d95e692db6c3f1ae10df49e305e4e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403674"
---
# <a name="working-with-files-and-folders"></a><span data-ttu-id="855af-103">Práce se soubory a složkami</span><span class="sxs-lookup"><span data-stu-id="855af-103">Working with Files and Folders</span></span>

<span data-ttu-id="855af-104">Procházení jednotek Windows Powershellu a manipulace s položkami na nich je podobný práce se soubory a složky na fyzických disků Windows.</span><span class="sxs-lookup"><span data-stu-id="855af-104">Navigating through Windows PowerShell drives and manipulating the items on them is similar to manipulating files and folders on Windows physical disk drives.</span></span> <span data-ttu-id="855af-105">Tato část popisuje, jak zacházet s konkrétní souborům a složkám manipulací s použitím prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="855af-105">This section discusses how to deal with specific file and folder manipulation tasks using PowerShell.</span></span>

### <a name="listing-all-the-files-and-folders-within-a-folder"></a><span data-ttu-id="855af-106">Výpis všech souborů a složek ve složce</span><span class="sxs-lookup"><span data-stu-id="855af-106">Listing All the Files and Folders Within a Folder</span></span>

<span data-ttu-id="855af-107">Všechny položky můžete získat přímo ve složce pomocí **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="855af-107">You can get all items directly within a folder by using **Get-ChildItem**.</span></span> <span data-ttu-id="855af-108">Přidat nepovinný **platnost** parametr zobrazení skrytých nebo položky system.</span><span class="sxs-lookup"><span data-stu-id="855af-108">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="855af-109">Tento příkaz například zobrazí přímý obsah Windows Powershellu jednotce C (který je stejný jako fyzický disk Windows C):</span><span class="sxs-lookup"><span data-stu-id="855af-109">For example, this command displays the direct contents of Windows PowerShell Drive C (which is the same as the Windows physical drive C):</span></span>

```powershell
Get-ChildItem -Path C:\ -Force
```

<span data-ttu-id="855af-110">Příkaz vypíše pouze přímo obsažené položky, podobně jako pomocí jeho Cmd.exe **DIR** příkazu nebo **ls** v prostředí systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="855af-110">The command lists only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="855af-111">Chcete-li zobrazit položky obsažené, je třeba zadat **-Recurse** také parametr.</span><span class="sxs-lookup"><span data-stu-id="855af-111">In order to show contained items, you need to specify the **-Recurse** parameter as well.</span></span> <span data-ttu-id="855af-112">(To může trvat extrémně dlouhou dobu pro dokončení.) Chcete-li vypsat vše na jednotce C:</span><span class="sxs-lookup"><span data-stu-id="855af-112">(This can take an extremely long time to complete.) To list everything on the C drive:</span></span>

```powershell
Get-ChildItem -Path C:\ -Force -Recurse
```

<span data-ttu-id="855af-113">**Rutina Get-ChildItem** můžete filtrovat položky, které její **cesta**, **filtr**, **zahrnout**, a **vyloučit** parametry, ale ty jsou obvykle pouze na základě názvu.</span><span class="sxs-lookup"><span data-stu-id="855af-113">**Get-ChildItem** can filter items with its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those are typically based only on name.</span></span> <span data-ttu-id="855af-114">Pokud chcete provádět složité filtrování založené na jiné vlastnosti položek pomocí **Where-Object**.</span><span class="sxs-lookup"><span data-stu-id="855af-114">You can perform complex filtering based on other properties of items by using **Where-Object**.</span></span>

<span data-ttu-id="855af-115">Následující příkaz vyhledá všechny spustitelné soubory ve složce Program Files, které bylo naposledy změněno po 1 říjnu 2005 a které jsou menší než 1 megabajt ani větší než 10 MB:</span><span class="sxs-lookup"><span data-stu-id="855af-115">The following command finds all executables within the Program Files folder that were last modified after October 1, 2005 and which are neither smaller than 1 megabyte nor larger than 10 megabytes:</span></span>

```powershell
Get-ChildItem -Path $env:ProgramFiles -Recurse -Include *.exe | Where-Object -FilterScript {($_.LastWriteTime -gt '2005-10-01') -and ($_.Length -ge 1mb) -and ($_.Length -le 10mb)}
```

### <a name="copying-files-and-folders"></a><span data-ttu-id="855af-116">Kopírování souborů a složek</span><span class="sxs-lookup"><span data-stu-id="855af-116">Copying Files and Folders</span></span>

<span data-ttu-id="855af-117">Kopírování se provádí pomocí **Copy-Item**.</span><span class="sxs-lookup"><span data-stu-id="855af-117">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="855af-118">Následující příkaz vytvoří zálohu C:\\boot.ini do C:\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="855af-118">The following command backs up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak
```

<span data-ttu-id="855af-119">Pokud cílový soubor už existuje, se nezdaří pokus o kopírování.</span><span class="sxs-lookup"><span data-stu-id="855af-119">If the destination file already exists, the copy attempt fails.</span></span> <span data-ttu-id="855af-120">Chcete-li přepsat existující cíl, použijte **platnost** parametr:</span><span class="sxs-lookup"><span data-stu-id="855af-120">To overwrite a pre-existing destination, use the **Force** parameter:</span></span>

```powershell
Copy-Item -Path C:\boot.ini -Destination C:\boot.bak -Force
```

<span data-ttu-id="855af-121">Tento příkaz funguje i v případě, že cíl je jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="855af-121">This command works even when the destination is read-only.</span></span>

<span data-ttu-id="855af-122">Kopírování složek funguje stejným způsobem.</span><span class="sxs-lookup"><span data-stu-id="855af-122">Folder copying works the same way.</span></span> <span data-ttu-id="855af-123">Tento příkaz kopíruje složky C:\\temp\\test1 do nové složky C:\\temp\\nástroji DeleteMe rekurzivně:</span><span class="sxs-lookup"><span data-stu-id="855af-123">This command copies the folder C:\\temp\\test1 to the new folder C:\\temp\\DeleteMe recursively:</span></span>

```powershell
Copy-Item C:\temp\test1 -Recurse C:\temp\DeleteMe
```

<span data-ttu-id="855af-124">Můžete také zkopírovat výběr položek.</span><span class="sxs-lookup"><span data-stu-id="855af-124">You can also copy a selection of items.</span></span> <span data-ttu-id="855af-125">Následující příkaz zkopíruje všechny soubory s příponou .txt kdekoli součástí c:\\data do c:\\temp\\text:</span><span class="sxs-lookup"><span data-stu-id="855af-125">The following command copies all .txt files contained anywhere in c:\\data to c:\\temp\\text:</span></span>

```powershell
Copy-Item -Filter *.txt -Path c:\data -Recurse -Destination C:\temp\text
```

<span data-ttu-id="855af-126">Další nástroje můžete stále použít ke zkopírování souborů systému.</span><span class="sxs-lookup"><span data-stu-id="855af-126">You can still use other tools to perform file system copies.</span></span> <span data-ttu-id="855af-127">Příkazu XCOPY, ROBOCOPY a modelu COM objekty, jako **Scripting.FileSystemObject,** všechny fungují v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="855af-127">XCOPY, ROBOCOPY, and COM objects, such as the **Scripting.FileSystemObject,** all work in Windows PowerShell.</span></span> <span data-ttu-id="855af-128">Například můžete použít modul Windows Script Host **Scripting.FileSystem COM** třídy zálohování C:\\boot.ini do C:\\boot.bak:</span><span class="sxs-lookup"><span data-stu-id="855af-128">For example, you can use the Windows Script Host **Scripting.FileSystem COM** class to back up C:\\boot.ini to C:\\boot.bak:</span></span>

```powershell
(New-Object -ComObject Scripting.FileSystemObject).CopyFile('C:\boot.ini', 'C:\boot.bak')
```

### <a name="creating-files-and-folders"></a><span data-ttu-id="855af-129">Vytváření souborů a složek</span><span class="sxs-lookup"><span data-stu-id="855af-129">Creating Files and Folders</span></span>

<span data-ttu-id="855af-130">Vytvoření nové položky funguje na všichni poskytovatelé Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="855af-130">Creating new items works the same on all Windows PowerShell providers.</span></span> <span data-ttu-id="855af-131">Pokud zprostředkovatele Windows PowerShell obsahuje víc než jeden typ položky – například zprostředkovatele systému souborů Windows Powershellu rozlišuje mezi adresářů a souborů, je třeba zadat typ položky.</span><span class="sxs-lookup"><span data-stu-id="855af-131">If a Windows PowerShell provider has more than one type of item—for example, the FileSystem Windows PowerShell provider distinguishes between directories and files—you need to specify the item type.</span></span>

<span data-ttu-id="855af-132">Tento příkaz vytvoří novou složku C:\\temp\\nová složka:</span><span class="sxs-lookup"><span data-stu-id="855af-132">This command creates a new folder C:\\temp\\New Folder:</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder' -ItemType Directory
```

<span data-ttu-id="855af-133">Tento příkaz vytvoří nový prázdný soubor C:\\temp\\novou složku\\soubor.txt</span><span class="sxs-lookup"><span data-stu-id="855af-133">This command creates a new empty file C:\\temp\\New Folder\\file.txt</span></span>

```powershell
New-Item -Path 'C:\temp\New Folder\file.txt' -ItemType File
```

### <a name="removing-all-files-and-folders-within-a-folder"></a><span data-ttu-id="855af-134">Odebrání všech souborů a složek ve složce</span><span class="sxs-lookup"><span data-stu-id="855af-134">Removing All Files and Folders Within a Folder</span></span>

<span data-ttu-id="855af-135">Můžete odebrat obsažené položky pomocí **Remove-Item**, ale zobrazí se výzva k potvrzení odebrání, pokud položka obsahuje cokoli.</span><span class="sxs-lookup"><span data-stu-id="855af-135">You can remove contained items using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="855af-136">Například, pokud při pokusu o odstranění složky C:\\temp\\nástroji DeleteMe, který obsahuje jiné položky, prostředí Windows PowerShell vás vyzve k potvrzení před odstranit tuto složku:</span><span class="sxs-lookup"><span data-stu-id="855af-136">For example, if you attempt to delete the folder C:\\temp\\DeleteMe that contains other items, Windows PowerShell prompts you for confirmation before deleting the folder:</span></span>

```
Remove-Item -Path C:\temp\DeleteMe

Confirm
The item at C:\temp\DeleteMe has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="855af-137">Pokud nechcete vyzváni k zadání jednotlivých obsažené položky, určete **Recurse** parametr:</span><span class="sxs-lookup"><span data-stu-id="855af-137">If you do not want to be prompted for each contained item, specify the **Recurse** parameter:</span></span>

```powershell
Remove-Item -Path C:\temp\DeleteMe -Recurse
```

### <a name="mapping-a-local-folder-as-a-windows-accessible-drive"></a><span data-ttu-id="855af-138">Mapování do místní složky jako dostupná jednotka Windows</span><span class="sxs-lookup"><span data-stu-id="855af-138">Mapping a Local Folder as a Windows Accessible Drive</span></span>

<span data-ttu-id="855af-139">Můžete také namapovat do místní složky pomocí **subst** příkazu.</span><span class="sxs-lookup"><span data-stu-id="855af-139">You can also map a local folder, using the **subst** command.</span></span> <span data-ttu-id="855af-140">Následující příkaz vytvoří místní jednotku, kterou P: root v místním adresáři Program Files:</span><span class="sxs-lookup"><span data-stu-id="855af-140">The following command creates a local drive P: rooted in the local Program Files directory:</span></span>

```powershell
subst p: $env:programfiles
```

<span data-ttu-id="855af-141">Stejně jako u síťových jednotkách namapované jednotky v rámci prostředí Windows PowerShell pomocí **subst** jsou okamžitě viditelné pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="855af-141">Just as with network drives, drives mapped within Windows PowerShell using **subst** are immediately visible to the Windows PowerShell shell.</span></span>

### <a name="reading-a-text-file-into-an-array"></a><span data-ttu-id="855af-142">Čtení textového souboru do pole</span><span class="sxs-lookup"><span data-stu-id="855af-142">Reading a Text File into an Array</span></span>

<span data-ttu-id="855af-143">Jeden z běžných formátů úložiště pro textová data se v souboru samostatné řádky, které jsou považovány za odlišné datové prvky.</span><span class="sxs-lookup"><span data-stu-id="855af-143">One of the more common storage formats for text data is in a file with separate lines treated as distinct data elements.</span></span> <span data-ttu-id="855af-144">**Get-Content** rutinu je možné číst celý soubor v jednom kroku, jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="855af-144">The **Get-Content** cmdlet can be used to read an entire file in one step, as shown here:</span></span>

```
PS> Get-Content -Path C:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional"
 /noexecute=AlwaysOff /fastdetect
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS=" Microsoft Windows XP Professional
with Data Execution Prevention" /noexecute=optin /fastdetect
```

<span data-ttu-id="855af-145">**Get-Content** již zpracovává data načtená ze souboru jako pole s jedním prvkem na řádek obsah souboru.</span><span class="sxs-lookup"><span data-stu-id="855af-145">**Get-Content** already treats the data read from the file as an array, with one element per line of file content.</span></span> <span data-ttu-id="855af-146">Můžete to ověřit tak, že zkontrolujete **délka** vráceného obsahu:</span><span class="sxs-lookup"><span data-stu-id="855af-146">You can confirm this by checking the **Length** of the returned content:</span></span>

```
PS> (Get-Content -Path C:\boot.ini).Length
6
```

<span data-ttu-id="855af-147">Tento příkaz je zvláště užitečná pro zobrazení seznamů informace do prostředí Windows PowerShell přímo.</span><span class="sxs-lookup"><span data-stu-id="855af-147">This command is most useful for getting lists of information into Windows PowerShell directly.</span></span> <span data-ttu-id="855af-148">Například může ukládat seznam názvů počítačů nebo IP adres v souboru C:\\temp\\domainMembers.txt názvem jednu na každý řádek v souboru.</span><span class="sxs-lookup"><span data-stu-id="855af-148">For example, you might store a list of computer names or IP addresses in a file C:\\temp\\domainMembers.txt, with one name on each line of the file.</span></span> <span data-ttu-id="855af-149">Můžete použít **Get-Content** načíst obsah souboru a umístit je do proměnné **$Computers**:</span><span class="sxs-lookup"><span data-stu-id="855af-149">You can use **Get-Content** to retrieve the file contents and put them in the variable **$Computers**:</span></span>

```powershell
$Computers = Get-Content -Path C:\temp\DomainMembers.txt
```

<span data-ttu-id="855af-150">**$Computers** je nyní pole obsahující název počítače v jednotlivých prvcích.</span><span class="sxs-lookup"><span data-stu-id="855af-150">**$Computers** is now an array containing a computer name in each element.</span></span>

---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s klíči registru
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: a9d08f2f6b5803980dec45a4e266ad66879c8c8d
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404104"
---
# <a name="working-with-registry-keys"></a><span data-ttu-id="e56a9-103">Práce s klíči registru</span><span class="sxs-lookup"><span data-stu-id="e56a9-103">Working with Registry Keys</span></span>

<span data-ttu-id="e56a9-104">Vzhledem k tomu klíče registru položky na jednotkách prostředí Windows PowerShell, práce s nimi je velmi podobně jako při práci se soubory a složkami.</span><span class="sxs-lookup"><span data-stu-id="e56a9-104">Because registry keys are items on Windows PowerShell drives, working with them is very similar to working with files and folders.</span></span> <span data-ttu-id="e56a9-105">Jeden kritický rozdíl je, že všechny položky v prostředí Windows PowerShell jednotku založenou na registru je kontejner, stejně jako složky na jednotce systému souborů.</span><span class="sxs-lookup"><span data-stu-id="e56a9-105">One critical difference is that every item on a registry-based Windows PowerShell drive is a container, just like a folder on a file system drive.</span></span> <span data-ttu-id="e56a9-106">Vlastnosti položek, ne rozdílných položek jsou však položky registru a jejich přidružené hodnoty.</span><span class="sxs-lookup"><span data-stu-id="e56a9-106">However, registry entries and their associated values are properties of the items, not distinct items.</span></span>

### <a name="listing-all-subkeys-of-a-registry-key"></a><span data-ttu-id="e56a9-107">Výpis všech podklíčů klíče registru</span><span class="sxs-lookup"><span data-stu-id="e56a9-107">Listing All Subkeys of a Registry Key</span></span>

<span data-ttu-id="e56a9-108">Můžete zobrazit všechny položky přímo z klíče registru pomocí **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="e56a9-108">You can show all items directly within a registry key by using **Get-ChildItem**.</span></span> <span data-ttu-id="e56a9-109">Přidat nepovinný **platnost** parametr zobrazení skrytých nebo položky system.</span><span class="sxs-lookup"><span data-stu-id="e56a9-109">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="e56a9-110">Tento příkaz například zobrazí položek přímo v rámci jednotku prostředí Windows PowerShell HKCU:, která odpovídá podregistr registru HKEY_CURRENT_USER:</span><span class="sxs-lookup"><span data-stu-id="e56a9-110">For example, this command displays the items directly within Windows PowerShell drive HKCU:, which corresponds to the HKEY_CURRENT_USER registry hive:</span></span>

```
PS> Get-ChildItem -Path hkcu:\

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER

SKC  VC Name                           Property
---  -- ----                           --------
  2   0 AppEvents                      {}
  7  33 Console                        {ColorTable00, ColorTable01, ColorTab...
 25   1 Control Panel                  {Opened}
  0   5 Environment                    {APR_ICONV_PATH, INCLUDE, LIB, TEMP...}
  1   7 Identities                     {Last Username, Last User ...
  4   0 Keyboard Layout                {}
...
```

<span data-ttu-id="e56a9-111">Toto jsou nejvyšší úrovně klíče viditelné v klíči HKEY_CURRENT_USER v editoru registru (Regedit.exe).</span><span class="sxs-lookup"><span data-stu-id="e56a9-111">These are the top-level keys visible under HKEY_CURRENT_USER in the Registry Editor (Regedit.exe).</span></span>

<span data-ttu-id="e56a9-112">Cesta v registru můžete také určit zadáním názvu registru zprostředkovatele, za nímž následuje "**::**".</span><span class="sxs-lookup"><span data-stu-id="e56a9-112">You can also specify this registry path by specifying the registry provider's name, followed by "**::**".</span></span> <span data-ttu-id="e56a9-113">Celý název registru zprostředkovatele **Microsoft.PowerShell.Core\\registru**, ale to lze zkrátit jenom **registru**.</span><span class="sxs-lookup"><span data-stu-id="e56a9-113">The registry provider's full name is **Microsoft.PowerShell.Core\\Registry**, but this can be shortened to just **Registry**.</span></span> <span data-ttu-id="e56a9-114">Některé z následujících příkazů bude zobrazovat obsah přímo pod HKCU:</span><span class="sxs-lookup"><span data-stu-id="e56a9-114">Any of the following commands will list the contents directly under HKCU:</span></span>

```powershell
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

<span data-ttu-id="e56a9-115">Tyto příkazy zobrazí seznam pouze přímo obsažené položky, podobně jako pomocí jeho Cmd.exe **DIR** příkazu nebo **ls** v prostředí systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="e56a9-115">These commands list only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="e56a9-116">Zobrazit položky obsažené, je třeba zadat **Recurse** parametru.</span><span class="sxs-lookup"><span data-stu-id="e56a9-116">To show contained items, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="e56a9-117">Chcete-li vypsat všechny klíče registru v HKCU, použijte následující příkaz (Tato operace může trvat extrémně dlouhou dobu.):</span><span class="sxs-lookup"><span data-stu-id="e56a9-117">To list all registry keys in HKCU, use the following command (This operation can take an extremely long time.):</span></span>

```powershell
Get-ChildItem -Path hkcu:\ -Recurse
```

<span data-ttu-id="e56a9-118">**Rutina Get-ChildItem** můžete provádět složité filtrování možnosti prostřednictvím jeho **cesta**, **filtr**, **zahrnout**, a **vyloučit**parametry, ale tyto parametry jsou obvykle pouze na základě názvu.</span><span class="sxs-lookup"><span data-stu-id="e56a9-118">**Get-ChildItem** can perform complex filtering capabilities through its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those parameters are typically based only on name.</span></span> <span data-ttu-id="e56a9-119">Pokud chcete provádět složité filtrování založené na jiné vlastnosti položek pomocí **Where-Object** rutiny.</span><span class="sxs-lookup"><span data-stu-id="e56a9-119">You can perform complex filtering based on other properties of items by using the **Where-Object** cmdlet.</span></span> <span data-ttu-id="e56a9-120">Následující příkaz vyhledá všechny klíče v rámci HKCU:\\softwaru, které mají více než jedna podklíče a také mít přesně čtyři hodnoty:</span><span class="sxs-lookup"><span data-stu-id="e56a9-120">The following command finds all keys within HKCU:\\Software that have no more than one subkey and also have exactly four values:</span></span>

```powershell
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### <a name="copying-keys"></a><span data-ttu-id="e56a9-121">Kopírování klíčů</span><span class="sxs-lookup"><span data-stu-id="e56a9-121">Copying Keys</span></span>

<span data-ttu-id="e56a9-122">Kopírování se provádí pomocí **Copy-Item**.</span><span class="sxs-lookup"><span data-stu-id="e56a9-122">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="e56a9-123">Následující příkaz zkopíruje HKLM:\\softwaru\\Microsoft\\Windows\\CurrentVersion a všechny jeho vlastnosti na HKCU:\\, vytváří se nový klíč s názvem "CurrentVersion":</span><span class="sxs-lookup"><span data-stu-id="e56a9-123">The following command copies HKLM:\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion and all of its properties to HKCU:\\, creating a new key named "CurrentVersion":</span></span>

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

<span data-ttu-id="e56a9-124">Pokud byste zkontrolovat tento nový klíč v editoru registru nebo pomocí **Get-ChildItem**, všimnete si, že nemáte kopie podklíče obsažené v novém umístění.</span><span class="sxs-lookup"><span data-stu-id="e56a9-124">If you examine this new key in the registry editor or by using **Get-ChildItem**, you will notice that you do not have copies of the contained subkeys in the new location.</span></span> <span data-ttu-id="e56a9-125">Aby bylo možné kopírovat veškerý obsah kontejneru, je třeba zadat **Recurse** parametru.</span><span class="sxs-lookup"><span data-stu-id="e56a9-125">In order to copy all of the contents of a container, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="e56a9-126">Chcete-li předchozí příkaz rekurzivního kopírování, použijete tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="e56a9-126">To make the preceding copy command recursive, you would use this command:</span></span>

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

<span data-ttu-id="e56a9-127">Stále můžete použít jiné nástroje, které už máte k dispozici k provedení kopie systému souborů.</span><span class="sxs-lookup"><span data-stu-id="e56a9-127">You can still use other tools you already have available to perform filesystem copies.</span></span> <span data-ttu-id="e56a9-128">Všechny nástroje pro úpravu registru – včetně reg.exe, regini.exe a regedit.exe—and objektů modelu COM, které podporují úpravy registru (například WScript.Shell a služby WMI StdRegProv třídy) může být použito v rámci prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e56a9-128">Any registry editing tools—including reg.exe, regini.exe, and regedit.exe—and COM objects that support registry editing (such as WScript.Shell and WMI's StdRegProv class) can be used from within Windows PowerShell.</span></span>

### <a name="creating-keys"></a><span data-ttu-id="e56a9-129">Vytvoření klíčů</span><span class="sxs-lookup"><span data-stu-id="e56a9-129">Creating Keys</span></span>

<span data-ttu-id="e56a9-130">Vytvoření nové klíče v registru je jednodušší než vytvoření nové položky v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="e56a9-130">Creating new keys in the registry is simpler than creating a new item in a file system.</span></span> <span data-ttu-id="e56a9-131">Protože všechny klíče registru jsou kontejnery, není nutné určit typ položky; můžete jednoduše zadat explicitní cestu, například:</span><span class="sxs-lookup"><span data-stu-id="e56a9-131">Because all registry keys are containers, you do not need to specify the item type; you simply supply an explicit path, such as:</span></span>

```powershell
New-Item -Path hkcu:\software_DeleteMe
```

<span data-ttu-id="e56a9-132">Můžete také cestu založenou na poskytovateli k zadání klíče:</span><span class="sxs-lookup"><span data-stu-id="e56a9-132">You can also use a provider-based path to specify a key:</span></span>

```powershell
New-Item -Path Registry::HKCU_DeleteMe
```

### <a name="deleting-keys"></a><span data-ttu-id="e56a9-133">Odstranění klíče</span><span class="sxs-lookup"><span data-stu-id="e56a9-133">Deleting Keys</span></span>

<span data-ttu-id="e56a9-134">Odstranění položek je v podstatě stejný pro všechny poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="e56a9-134">Deleting items is essentially the same for all providers.</span></span> <span data-ttu-id="e56a9-135">Následující příkazy odeberou tiše položky:</span><span class="sxs-lookup"><span data-stu-id="e56a9-135">The following commands will silently remove items:</span></span>

```powershell
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### <a name="removing-all-keys-under-a-specific-key"></a><span data-ttu-id="e56a9-136">Odebrat všechny klíče v rámci konkrétního klíče</span><span class="sxs-lookup"><span data-stu-id="e56a9-136">Removing All Keys Under a Specific Key</span></span>

<span data-ttu-id="e56a9-137">Odebírat položky, které můžete odebrat pomocí **Remove-Item**, ale zobrazí se výzva k potvrzení odebrání, pokud položka obsahuje cokoli.</span><span class="sxs-lookup"><span data-stu-id="e56a9-137">You can remove contained items by using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="e56a9-138">Například, pokud jsme pokus o odstranění HKCU:\\CurrentVersion podklíč jsme vytvořili, zobrazí toto:</span><span class="sxs-lookup"><span data-stu-id="e56a9-138">For example, if we attempt to delete the HKCU:\\CurrentVersion subkey we created, we see this:</span></span>

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="e56a9-139">Chcete-li odstranit obsažené položky bez výzvy, zadejte **-Recurse** parametr:</span><span class="sxs-lookup"><span data-stu-id="e56a9-139">To delete contained items without prompting, specify the **-Recurse** parameter:</span></span>

```powershell
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

<span data-ttu-id="e56a9-140">Pokud chcete odebrat všechny položky v rámci HKCU:\\CurrentVersion, ale ne HKCU:\\CurrentVersion samotné, můžete místo toho použít:</span><span class="sxs-lookup"><span data-stu-id="e56a9-140">If you wanted to remove all items within HKCU:\\CurrentVersion but not HKCU:\\CurrentVersion itself, you could instead use:</span></span>

```powershell
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```
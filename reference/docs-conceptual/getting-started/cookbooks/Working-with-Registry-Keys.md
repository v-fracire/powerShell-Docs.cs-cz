---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s klíči registru
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: a9d08f2f6b5803980dec45a4e266ad66879c8c8d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30951694"
---
# <a name="working-with-registry-keys"></a><span data-ttu-id="a9682-103">Práce s klíči registru</span><span class="sxs-lookup"><span data-stu-id="a9682-103">Working with Registry Keys</span></span>

<span data-ttu-id="a9682-104">Protože jsou klíče registru položky v prostředí Windows PowerShell jednotky, je velmi podobné práce se soubory a složky práci s nimi.</span><span class="sxs-lookup"><span data-stu-id="a9682-104">Because registry keys are items on Windows PowerShell drives, working with them is very similar to working with files and folders.</span></span> <span data-ttu-id="a9682-105">Jeden kritické rozdílem je, že každá položka na jednotce založenou na registru prostředí Windows PowerShell je kontejner, stejně jako složky na jednotce systému souborů.</span><span class="sxs-lookup"><span data-stu-id="a9682-105">One critical difference is that every item on a registry-based Windows PowerShell drive is a container, just like a folder on a file system drive.</span></span> <span data-ttu-id="a9682-106">Vlastnosti těchto položek, není odlišné položky jsou však položky registru a jejich přidružené hodnoty.</span><span class="sxs-lookup"><span data-stu-id="a9682-106">However, registry entries and their associated values are properties of the items, not distinct items.</span></span>

### <a name="listing-all-subkeys-of-a-registry-key"></a><span data-ttu-id="a9682-107">Výpis všech podklíčů klíče registru</span><span class="sxs-lookup"><span data-stu-id="a9682-107">Listing All Subkeys of a Registry Key</span></span>

<span data-ttu-id="a9682-108">Můžete zobrazit všechny položky přímo v klíči registru pomocí **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="a9682-108">You can show all items directly within a registry key by using **Get-ChildItem**.</span></span> <span data-ttu-id="a9682-109">Přidejte volitelné **Force** parametr zobrazení skrytý nebo položky system.</span><span class="sxs-lookup"><span data-stu-id="a9682-109">Add the optional **Force** parameter to display hidden or system items.</span></span> <span data-ttu-id="a9682-110">Tento příkaz například zobrazí položky přímo v rámci jednotku prostředí Windows PowerShell HKCU:, která odpovídá podregistr registru HKEY_CURRENT_USER:</span><span class="sxs-lookup"><span data-stu-id="a9682-110">For example, this command displays the items directly within Windows PowerShell drive HKCU:, which corresponds to the HKEY_CURRENT_USER registry hive:</span></span>

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

<span data-ttu-id="a9682-111">Toto jsou nejvyšší úrovně klíče viditelné HKEY_CURRENT_USER v editoru registru (Regedit.exe).</span><span class="sxs-lookup"><span data-stu-id="a9682-111">These are the top-level keys visible under HKEY_CURRENT_USER in the Registry Editor (Regedit.exe).</span></span>

<span data-ttu-id="a9682-112">Cesta v registru můžete také určit tak, že zadáte název zprostředkovatele registru, za nímž následují "**::**".</span><span class="sxs-lookup"><span data-stu-id="a9682-112">You can also specify this registry path by specifying the registry provider's name, followed by "**::**".</span></span> <span data-ttu-id="a9682-113">Celý název zprostředkovatele registru **Microsoft.PowerShell.Core\\registru**, ale to může být zkrátí tak, aby právě **registru**.</span><span class="sxs-lookup"><span data-stu-id="a9682-113">The registry provider's full name is **Microsoft.PowerShell.Core\\Registry**, but this can be shortened to just **Registry**.</span></span> <span data-ttu-id="a9682-114">Některé z následujících příkazů zobrazí seznam obsah přímo pod HKCU:</span><span class="sxs-lookup"><span data-stu-id="a9682-114">Any of the following commands will list the contents directly under HKCU:</span></span>

```powershell
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

<span data-ttu-id="a9682-115">Tyto příkazy seznamu jenom přímo obsažených položek, podobně jako pomocí jeho Cmd.exe **DIR** příkaz nebo **ls** v prostředí systému UNIX.</span><span class="sxs-lookup"><span data-stu-id="a9682-115">These commands list only the directly contained items, much like using Cmd.exe's **DIR** command or **ls** in a UNIX shell.</span></span> <span data-ttu-id="a9682-116">Chcete-li zobrazit položky, je potřeba zadat **Recurse** parametr.</span><span class="sxs-lookup"><span data-stu-id="a9682-116">To show contained items, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="a9682-117">K zobrazení seznamu všechny klíče registru ve HKCU, použijte následující příkaz (Tato operace může trvat velmi dlouho.):</span><span class="sxs-lookup"><span data-stu-id="a9682-117">To list all registry keys in HKCU, use the following command (This operation can take an extremely long time.):</span></span>

```powershell
Get-ChildItem -Path hkcu:\ -Recurse
```

<span data-ttu-id="a9682-118">**Get-ChildItem** můžete provádět komplexní možnosti filtrování prostřednictvím jeho **cesta**, **filtru**, **zahrnout**, a **vyloučit**parametry, ale tyto parametry jsou obvykle pouze na základě názvu.</span><span class="sxs-lookup"><span data-stu-id="a9682-118">**Get-ChildItem** can perform complex filtering capabilities through its **Path**, **Filter**, **Include**, and **Exclude** parameters, but those parameters are typically based only on name.</span></span> <span data-ttu-id="a9682-119">Můžete provádět komplexní filtrování založené na jiné vlastnosti položky pomocí **Where-Object** rutiny.</span><span class="sxs-lookup"><span data-stu-id="a9682-119">You can perform complex filtering based on other properties of items by using the **Where-Object** cmdlet.</span></span> <span data-ttu-id="a9682-120">Následující příkaz vyhledá všechny klíče v rámci HKCU:\\softwaru, které mají více než jeden podklíčů a také mít přesně čtyři hodnoty:</span><span class="sxs-lookup"><span data-stu-id="a9682-120">The following command finds all keys within HKCU:\\Software that have no more than one subkey and also have exactly four values:</span></span>

```powershell
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### <a name="copying-keys"></a><span data-ttu-id="a9682-121">Kopírování klíče</span><span class="sxs-lookup"><span data-stu-id="a9682-121">Copying Keys</span></span>

<span data-ttu-id="a9682-122">Kopírování provádí pomocí **Copy-Item**.</span><span class="sxs-lookup"><span data-stu-id="a9682-122">Copying is done with **Copy-Item**.</span></span> <span data-ttu-id="a9682-123">Následující příkaz zkopíruje HKLM:\\softwaru\\Microsoft\\Windows\\CurrentVersion a všechny její vlastnosti, aby HKCU:\\, vytváří nový klíč s názvem "CurrentVersion":</span><span class="sxs-lookup"><span data-stu-id="a9682-123">The following command copies HKLM:\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion and all of its properties to HKCU:\\, creating a new key named "CurrentVersion":</span></span>

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

<span data-ttu-id="a9682-124">Pokud byste zkontrolovat tento nový klíč, v editoru registru nebo pomocí **Get-ChildItem**, si všimnete nemají kopie podklíče obsažené v novém umístění.</span><span class="sxs-lookup"><span data-stu-id="a9682-124">If you examine this new key in the registry editor or by using **Get-ChildItem**, you will notice that you do not have copies of the contained subkeys in the new location.</span></span> <span data-ttu-id="a9682-125">Aby bylo možné kopírovat veškerý obsah kontejneru, je třeba zadat **Recurse** parametr.</span><span class="sxs-lookup"><span data-stu-id="a9682-125">In order to copy all of the contents of a container, you need to specify the **Recurse** parameter.</span></span> <span data-ttu-id="a9682-126">Chcete-li předchozí příkaz rekurzivní kopírování, použijete tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="a9682-126">To make the preceding copy command recursive, you would use this command:</span></span>

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

<span data-ttu-id="a9682-127">Můžete dál používat jiné nástroje, které už máte k dispozici ke zkopírování souborů.</span><span class="sxs-lookup"><span data-stu-id="a9682-127">You can still use other tools you already have available to perform filesystem copies.</span></span> <span data-ttu-id="a9682-128">Všechny nástroje pro úpravu registru – včetně reg.exe, regini.exe a regedit.exe—and objektů COM, které podporují úpravy registru (například na rozhraní WMI a WScript.Shell třídy StdRegProv) můžete ji použít v rámci prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9682-128">Any registry editing tools—including reg.exe, regini.exe, and regedit.exe—and COM objects that support registry editing (such as WScript.Shell and WMI's StdRegProv class) can be used from within Windows PowerShell.</span></span>

### <a name="creating-keys"></a><span data-ttu-id="a9682-129">Vytváření klíčů</span><span class="sxs-lookup"><span data-stu-id="a9682-129">Creating Keys</span></span>

<span data-ttu-id="a9682-130">Vytvoření nového klíče v registru je jednodušší než vytvoření nové položky v systému souborů.</span><span class="sxs-lookup"><span data-stu-id="a9682-130">Creating new keys in the registry is simpler than creating a new item in a file system.</span></span> <span data-ttu-id="a9682-131">Protože všechny klíče registru jsou kontejnery, není potřeba zadat typ položky; je jednoduše zadat explicitní cestu, jako například:</span><span class="sxs-lookup"><span data-stu-id="a9682-131">Because all registry keys are containers, you do not need to specify the item type; you simply supply an explicit path, such as:</span></span>

```powershell
New-Item -Path hkcu:\software_DeleteMe
```

<span data-ttu-id="a9682-132">Cestu založenou na poskytovateli můžete také zadat klíč:</span><span class="sxs-lookup"><span data-stu-id="a9682-132">You can also use a provider-based path to specify a key:</span></span>

```powershell
New-Item -Path Registry::HKCU_DeleteMe
```

### <a name="deleting-keys"></a><span data-ttu-id="a9682-133">Odstraňování kláves</span><span class="sxs-lookup"><span data-stu-id="a9682-133">Deleting Keys</span></span>

<span data-ttu-id="a9682-134">Odstraňování položek je v podstatě stejný pro všechny poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="a9682-134">Deleting items is essentially the same for all providers.</span></span> <span data-ttu-id="a9682-135">Následující příkazy bezobslužně odebere položky:</span><span class="sxs-lookup"><span data-stu-id="a9682-135">The following commands will silently remove items:</span></span>

```powershell
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### <a name="removing-all-keys-under-a-specific-key"></a><span data-ttu-id="a9682-136">Odebrání všechny klíče v rámci konkrétního klíče</span><span class="sxs-lookup"><span data-stu-id="a9682-136">Removing All Keys Under a Specific Key</span></span>

<span data-ttu-id="a9682-137">Položky lze odebrat pomocí **odebrat položky**, ale zobrazí se výzva k potvrzení odebrání, pokud položka obsahuje cokoliv jiného.</span><span class="sxs-lookup"><span data-stu-id="a9682-137">You can remove contained items by using **Remove-Item**, but you will be prompted to confirm the removal if the item contains anything else.</span></span> <span data-ttu-id="a9682-138">Například, pokud jsme pokusu o odstranění HKCU:\\CurrentVersion podklíč jsme vytvořili, vidíte, toto:</span><span class="sxs-lookup"><span data-stu-id="a9682-138">For example, if we attempt to delete the HKCU:\\CurrentVersion subkey we created, we see this:</span></span>

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

<span data-ttu-id="a9682-139">Chcete-li odstranit položky bez výzvy k potvrzení, zadejte **-Recurse** parametr:</span><span class="sxs-lookup"><span data-stu-id="a9682-139">To delete contained items without prompting, specify the **-Recurse** parameter:</span></span>

```powershell
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

<span data-ttu-id="a9682-140">Pokud chcete odebrat všechny položky v rámci HKCU:\\CurrentVersion, ale není HKCU:\\CurrentVersion sám sebe, můžete místo toho použít:</span><span class="sxs-lookup"><span data-stu-id="a9682-140">If you wanted to remove all items within HKCU:\\CurrentVersion but not HKCU:\\CurrentVersion itself, you could instead use:</span></span>

```powershell
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```
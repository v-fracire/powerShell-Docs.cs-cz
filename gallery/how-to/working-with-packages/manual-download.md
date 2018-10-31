---
ms.date: 09/11/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, psgallery
title: Ruční stažení balíčku
ms.openlocfilehash: 0952aa4ec474850af5219fb2e0e9ee3e954b0f9a
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004009"
---
# <a name="manual-package-download"></a><span data-ttu-id="1c1e1-103">Ruční stažení balíčku</span><span class="sxs-lookup"><span data-stu-id="1c1e1-103">Manual Package Download</span></span>

<span data-ttu-id="1c1e1-104">Galerie prostředí Powershell podporuje stahování balíčku z webu přímo, bez použití rutiny Správce balíčků PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-104">The Powershell Gallery supports downloading a package from the website directly, without using the PowerShellGet cmdlets.</span></span> <span data-ttu-id="1c1e1-105">Balíček se stáhne jako soubor balíčku (.nupkg) NuGet, který je pak snadno zkopírovat do interní úložiště.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-105">The package will be downloaded as a NuGet package (.nupkg) file, which can then be easily copied to an internal repository.</span></span>

> [!NOTE]
> <span data-ttu-id="1c1e1-106">Stažení balíčku ruční **není** určené jako náhrada za rutinu Install-Module.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-106">Manual package download is **not** intended as a replacement for the Install-Module cmdlet.</span></span>
> <span data-ttu-id="1c1e1-107">Stahuje se balíček nenainstaluje modulu nebo skriptu.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-107">Downloading the package does not install the module or script.</span></span> <span data-ttu-id="1c1e1-108">Závislosti nejsou zahrnuté do balíčku NuGet stáhli.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-108">Dependencies are not included in the NuGet package downloaded.</span></span> <span data-ttu-id="1c1e1-109">Následující pokyny jsou k dispozici pouze pro referenční účely.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-109">The following instructions are provided for reference purposes only.</span></span>

## <a name="using-manual-download-to-acquire-a-package"></a><span data-ttu-id="1c1e1-110">Získat balíček pomocí ruční stažení</span><span class="sxs-lookup"><span data-stu-id="1c1e1-110">Using manual download to acquire a package</span></span>

<span data-ttu-id="1c1e1-111">Každá stránka obsahuje odkaz pro ruční stažení, jak je znázorněno zde:</span><span class="sxs-lookup"><span data-stu-id="1c1e1-111">Each page has a link for Manual Download, as shown here:</span></span>

![Ruční stažení](../../Images/packagedisplaypagewithpseditions.png)

<span data-ttu-id="1c1e1-113">Pokud chcete stáhnout ručně, klikněte na **stáhnout soubor nupkg nezpracovaná**.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-113">To download manually, click on **Download the raw nupkg file**.</span></span> <span data-ttu-id="1c1e1-114">Kopii balíčku zkopírován do složky pro stahování pro váš prohlížeč s názvem `<name>.<version>.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-114">A copy of the package copied to the download folder for your browser with the name `<name>.<version>.nupkg`.</span></span>

<span data-ttu-id="1c1e1-115">Balíček NuGet je archiv ZIP s další soubory, které obsahují informace o obsahu balíčku.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-115">A NuGet package is a ZIP archive with extra files containing information about the contents of the package.</span></span> <span data-ttu-id="1c1e1-116">Některé prohlížeče, jako třeba Internet Explorer, automaticky nahradit `.nupkg` s příponou souboru `.zip`.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-116">Some browsers, like Internet Explorer, automatically replace the `.nupkg` file extension with `.zip`.</span></span> <span data-ttu-id="1c1e1-117">Rozbalte balíček, přejmenujte je tak `.nupkg` soubor `.zip`, v případě potřeby extrahujte obsah do místní složky.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-117">To expand the package, rename the `.nupkg` file to `.zip`, if needed, then extract the contents to a local folder.</span></span>

<span data-ttu-id="1c1e1-118">Soubor balíčku NuGet obsahuje následující prvky specifické pro NuGet, které nejsou součástí původní zabaleného kódu:</span><span class="sxs-lookup"><span data-stu-id="1c1e1-118">A NuGet package file includes the following NuGet-specific elements that aren't part of the original packaged code:</span></span>

- <span data-ttu-id="1c1e1-119">Složka s názvem `_rels` – obsahuje `.rels` soubor, který obsahuje seznam závislostí</span><span class="sxs-lookup"><span data-stu-id="1c1e1-119">A folder named `_rels` - contains a `.rels` file that lists the dependencies</span></span>
- <span data-ttu-id="1c1e1-120">Složka s názvem `package` -obsahuje data specifická pro NuGet</span><span class="sxs-lookup"><span data-stu-id="1c1e1-120">A folder named `package` - contains the NuGet-specific data</span></span>
- <span data-ttu-id="1c1e1-121">Soubor s názvem `[Content_Types].xml` – popisuje, jak rozšíření, jako je Správce balíčků PowerShellGet fungují s NuGet</span><span class="sxs-lookup"><span data-stu-id="1c1e1-121">A file named `[Content_Types].xml` - describes how extensions like PowerShellGet work with NuGet</span></span>
- <span data-ttu-id="1c1e1-122">Soubor s názvem `<name>.nuspec` – obsahuje hromadně metadat</span><span class="sxs-lookup"><span data-stu-id="1c1e1-122">A file named `<name>.nuspec` - contains the bulk of the metadata</span></span>

## <a name="installing-powershell-modules-from-a-nuget-package"></a><span data-ttu-id="1c1e1-123">Instalace modulů Powershellu z balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="1c1e1-123">Installing PowerShell Modules from a NuGet package</span></span>

> [!NOTE]
> <span data-ttu-id="1c1e1-124">Tyto pokyny **neměňte** poskytují stejný výsledek jako spuštění `Install-Module`.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-124">These instructions **DO NOT** give the same result as running `Install-Module`.</span></span> <span data-ttu-id="1c1e1-125">Tyto pokyny splňovat minimální požadavky.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-125">These instructions fulfill the minimum requirements.</span></span> <span data-ttu-id="1c1e1-126">Nejsou určeny k jako náhrada za `Install-Module`.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-126">They are not intended to be a replacement for `Install-Module`.</span></span> <span data-ttu-id="1c1e1-127">Některé kroky prováděné `Install-Module` nejsou zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-127">Some steps performed by `Install-Module` are not included.</span></span>

<span data-ttu-id="1c1e1-128">Nejjednodušší způsob je NuGet specifické prvky odeberete ze složky.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-128">The easiest approach is to remove the NuGet-specific elements from the folder.</span></span> <span data-ttu-id="1c1e1-129">Kvůli tomu Powershellu kód vytvořený pomocí autora balíčku.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-129">This leaves the PowerShell code created by the package author.</span></span> <span data-ttu-id="1c1e1-130">Tyto kroky jsou:</span><span class="sxs-lookup"><span data-stu-id="1c1e1-130">The steps are:</span></span>

1. <span data-ttu-id="1c1e1-131">Extrahujte obsah balíčku NuGet do místní složky.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-131">Extract the contents of the NuGet package to a local folder.</span></span>
2. <span data-ttu-id="1c1e1-132">Odstraňte NuGet specifické prvky ze složky.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-132">Delete the NuGet-specific elements from the folder.</span></span>
3. <span data-ttu-id="1c1e1-133">Přejmenujte složku.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-133">Rename the folder.</span></span> <span data-ttu-id="1c1e1-134">Výchozí název složky je obvykle `<name>.<version>`.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-134">The default folder name is usually `<name>.<version>`.</span></span> <span data-ttu-id="1c1e1-135">Verze může obsahovat "-předprodejní" Pokud modul je označený jako zkušební verzi.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-135">The version can include "-prerelease" if the module is tagged as a prerelease version.</span></span> <span data-ttu-id="1c1e1-136">Přejmenujte složku pouze na název modulu.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-136">Rename the folder to just the module name.</span></span> <span data-ttu-id="1c1e1-137">Například "azurerm.storage.5.0.4 ve verzi preview" se změní na "azurerm.storage".</span><span class="sxs-lookup"><span data-stu-id="1c1e1-137">For example, "azurerm.storage.5.0.4-preview" becomes "azurerm.storage".</span></span>
4. <span data-ttu-id="1c1e1-138">Zkopírujte složku pro váš PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-138">Copy the folder to your PSModulePath.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c1e1-139">Ruční stažení neobsahuje žádné závislosti, které vyžaduje modulem.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-139">The manual download does not include any dependencies required by the module.</span></span> <span data-ttu-id="1c1e1-140">Pokud balíček obsahuje závislosti, musí být nainstalovány v systému pro tento modul fungovat správně.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-140">If the package has dependencies, they must be installed on the system for this module to work correctly.</span></span> <span data-ttu-id="1c1e1-141">Galerie prostředí PowerShell ukazuje všechny závislosti, které vyžaduje balíček.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-141">The PowerShell Gallery shows all dependencies required by the package.</span></span>

## <a name="installing-powershell-scripts-from-a-nuget-package"></a><span data-ttu-id="1c1e1-142">Instalace Powershellové skripty z balíčku NuGet</span><span class="sxs-lookup"><span data-stu-id="1c1e1-142">Installing PowerShell Scripts from a NuGet package</span></span>

> [!NOTE]
> <span data-ttu-id="1c1e1-143">Tyto pokyny **neměňte** poskytují stejný výsledek jako spuštění `Install-Script`.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-143">These instructions **DO NOT** give the same result as running `Install-Script`.</span></span> <span data-ttu-id="1c1e1-144">Tyto pokyny splňovat minimální požadavky.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-144">These instructions fulfill the minimum requirements.</span></span> <span data-ttu-id="1c1e1-145">Nejsou určeny k jako náhrada za `Install-Script`.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-145">They are not intended to be a replacement for `Install-Script`.</span></span>

<span data-ttu-id="1c1e1-146">Nejjednodušší způsob je přímo extrahovat balíček NuGet a pak pomocí skriptu.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-146">The easiest approach is to extract the NuGet package, then use the script directly.</span></span> <span data-ttu-id="1c1e1-147">Tyto kroky jsou:</span><span class="sxs-lookup"><span data-stu-id="1c1e1-147">The steps are:</span></span>

1. <span data-ttu-id="1c1e1-148">Extrahujte obsah balíčku NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-148">Extract the contents of the NuGet package.</span></span>
2. <span data-ttu-id="1c1e1-149">`.PS1` Soubor ve složce můžete použít přímo z tohoto umístění.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-149">The `.PS1` file in the folder can be used directly from this location.</span></span>
3. <span data-ttu-id="1c1e1-150">Můžete odstranit prvky specifické pro NuGet ve složce.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-150">You may delete the NuGet-specific elements in the folder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c1e1-151">Ruční stažení neobsahuje žádné závislosti, které vyžaduje modulem.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-151">The manual download does not include any dependencies required by the module.</span></span> <span data-ttu-id="1c1e1-152">Pokud balíček obsahuje závislosti, musí být nainstalovány v systému pro tento modul fungovat správně.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-152">If the package has dependencies, they must be installed on the system for this module to work correctly.</span></span> <span data-ttu-id="1c1e1-153">Galerie prostředí PowerShell ukazuje všechny závislosti, které vyžaduje balíček.</span><span class="sxs-lookup"><span data-stu-id="1c1e1-153">The PowerShell Gallery shows all dependencies required by the package.</span></span>

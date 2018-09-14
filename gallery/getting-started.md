---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Začínáme s Galerie prostředí PowerShell
ms.openlocfilehash: 39998df1a2bf9363dd008dc96a802157c8d691d7
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523025"
---
# <a name="get-started-with-the-powershell-gallery"></a><span data-ttu-id="74166-103">Začínáme s Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74166-103">Get Started with the PowerShell Gallery</span></span>

<span data-ttu-id="74166-104">Správný způsob, jak nainstalovat položky z Galerie prostředí PowerShell je mohli používat rutiny v [PowerShellGet](/powershell/module/powershellget) modulu.</span><span class="sxs-lookup"><span data-stu-id="74166-104">The proper way to install items from the PowerShell Gallery is to use the cmdlets in the [PowerShellGet](/powershell/module/powershellget) module.</span></span> <span data-ttu-id="74166-105">Není nutné se přihlásit ke stažení položek z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74166-105">You do not need to sign in to download items from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="74166-106">Je možné stáhnout balíček přímo z Galerie prostředí PowerShell, ale toto není doporučený postup.</span><span class="sxs-lookup"><span data-stu-id="74166-106">It is possible to download a package from the PowerShell Gallery directly, but this is not a recommended approach.</span></span> <span data-ttu-id="74166-107">Další podrobnosti najdete v tématu [ruční stažení balíčku](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/how-to/working-with-items/manual-download.md).</span><span class="sxs-lookup"><span data-stu-id="74166-107">For more details, see [Manual Package Download](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/how-to/working-with-items/manual-download.md).</span></span>  


## <a name="discovering-items-from-the-powershell-gallery"></a><span data-ttu-id="74166-108">Zjišťují se položky z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74166-108">Discovering items from the PowerShell Gallery</span></span>

<span data-ttu-id="74166-109">Položky v galerii prostředí PowerShell můžete najít pomocí **hledání** ovládacího prvku na tomto webu, nebo tak, že přejdete na stránkách moduly a skripty.</span><span class="sxs-lookup"><span data-stu-id="74166-109">You can find items in the PowerShell Gallery by using the **Search** control on this website, or by browsing through the Modules and Scripts pages.</span></span> <span data-ttu-id="74166-110">Můžete také najít položky z Galerie prostředí PowerShell spuštěním [Find-Module][] a [Find-Script][] rutin, v závislosti na typu položky s `-Repository PSGallery`.</span><span class="sxs-lookup"><span data-stu-id="74166-110">You can also find items from the PowerShell Gallery by running the [Find-Module][] and [Find-Script][] cmdlets, depending on the item type, with `-Repository PSGallery`.</span></span>

<span data-ttu-id="74166-111">Filtrování výsledků z galerie můžete provést pomocí následujících parametrů:</span><span class="sxs-lookup"><span data-stu-id="74166-111">Filtering results from the Gallery can be done by using the following parameters:</span></span>

- <span data-ttu-id="74166-112">Název</span><span class="sxs-lookup"><span data-stu-id="74166-112">Name</span></span>
- <span data-ttu-id="74166-113">AllVersions</span><span class="sxs-lookup"><span data-stu-id="74166-113">AllVersions</span></span>
- <span data-ttu-id="74166-114">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="74166-114">MinimumVersion</span></span>
- <span data-ttu-id="74166-115">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="74166-115">RequiredVersion</span></span>
- <span data-ttu-id="74166-116">Značka</span><span class="sxs-lookup"><span data-stu-id="74166-116">Tag</span></span>
- <span data-ttu-id="74166-117">Zahrnuje</span><span class="sxs-lookup"><span data-stu-id="74166-117">Includes</span></span>
- <span data-ttu-id="74166-118">DscResource</span><span class="sxs-lookup"><span data-stu-id="74166-118">DscResource</span></span>
- <span data-ttu-id="74166-119">RoleCapability</span><span class="sxs-lookup"><span data-stu-id="74166-119">RoleCapability</span></span>
- <span data-ttu-id="74166-120">Příkaz</span><span class="sxs-lookup"><span data-stu-id="74166-120">Command</span></span>
- <span data-ttu-id="74166-121">Filtr</span><span class="sxs-lookup"><span data-stu-id="74166-121">Filter</span></span>

<span data-ttu-id="74166-122">Pokud máte zájem zjišťování konkrétní prostředky DSC v galerii, můžete spustit [Find-DscResource] rutiny.</span><span class="sxs-lookup"><span data-stu-id="74166-122">If you're only interested in discovering specific DSC resources in the Gallery, you can run the [Find-DscResource] cmdlet.</span></span> <span data-ttu-id="74166-123">Find-DscResource vrací data na prostředky DSC obsažené v galerii.</span><span class="sxs-lookup"><span data-stu-id="74166-123">Find-DscResource returns data on DSC resources contained in the Gallery.</span></span>
<span data-ttu-id="74166-124">Protože prostředky DSC se vždy dodávají jako součást modulu, je stále potřeba spustit [Install-Module][] nainstalovat tyto prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="74166-124">Because DSC resources are always delivered as part of a module, you still need to run [Install-Module][] to install those DSC resources.</span></span>

## <a name="learning-about-items-in-the-powershell-gallery"></a><span data-ttu-id="74166-125">Získání informací o položky v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74166-125">Learning about items in the PowerShell Gallery</span></span>

<span data-ttu-id="74166-126">Jakmile identifikujete položky, které vás zajímá, můžete další informace o něm.</span><span class="sxs-lookup"><span data-stu-id="74166-126">Once you've identified an item you're interested in, you may want to learn more about it.</span></span> <span data-ttu-id="74166-127">Můžete to provést tím, že kontroluje konkrétní stránka danou položku v galerii.</span><span class="sxs-lookup"><span data-stu-id="74166-127">You can do this by examining that item's specific page on the Gallery.</span></span> <span data-ttu-id="74166-128">Na této stránce budete moct Zobrazit vše se odeslaly s položku metadat.</span><span class="sxs-lookup"><span data-stu-id="74166-128">On that page, you'll be able to see all of the metadata uploaded with the item.</span></span> <span data-ttu-id="74166-129">Tato metadata pro položku, kterou autorem položky, není ověřená společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74166-129">This metadata for an item is provided by the item's author, and is not verified by Microsoft.</span></span> <span data-ttu-id="74166-130">Vlastník položky se silnou vazbu na galerii účet použitý k publikování položky a důvěryhodný více než pole Author.</span><span class="sxs-lookup"><span data-stu-id="74166-130">The Owner of the item is strongly tied to the Gallery account used to publish the item, and is more trustworthy than the Author field.</span></span>

<span data-ttu-id="74166-131">Pokud zjistíte, že položka, která máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce danou položku.</span><span class="sxs-lookup"><span data-stu-id="74166-131">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

<span data-ttu-id="74166-132">Pokud používáte [Find-Module][] nebo [Find-Script][], zobrazí se tato data v vráceného objektu PSGetModuleInfo.</span><span class="sxs-lookup"><span data-stu-id="74166-132">If you're running [Find-Module][] or [Find-Script][], you can view this data in the returned PSGetModuleInfo object.</span></span> <span data-ttu-id="74166-133">Například systém `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span><span class="sxs-lookup"><span data-stu-id="74166-133">For example, running `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span></span>
<span data-ttu-id="74166-134">Vrátí data o PSReadLine modulu v galerii.</span><span class="sxs-lookup"><span data-stu-id="74166-134">returns data on the PSReadLine module in the Gallery.</span></span>

## <a name="downloading-items-from-the-powershell-gallery"></a><span data-ttu-id="74166-135">Stažení položek z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74166-135">Downloading items from the PowerShell Gallery</span></span>

<span data-ttu-id="74166-136">Při stažení položek z Galerie prostředí PowerShell doporučujeme následující postup:</span><span class="sxs-lookup"><span data-stu-id="74166-136">We encourage the following process when downloading items from the PowerShell Gallery:</span></span>

### <a name="inspect"></a><span data-ttu-id="74166-137">Kontrola</span><span class="sxs-lookup"><span data-stu-id="74166-137">Inspect</span></span>

<span data-ttu-id="74166-138">Stahování položky z Galerie pro kontrolu, spusťte [Save-Module][] nebo [Save-Script][] rutiny, v závislosti na typu položky.</span><span class="sxs-lookup"><span data-stu-id="74166-138">To download an item from the Gallery for inspection, run either the [Save-Module][] or [Save-Script][] cmdlet, depending on the item type.</span></span> <span data-ttu-id="74166-139">To vám umožní uložit položku místně bez nutnosti jeho instalace a zkontrolovat obsah položky.</span><span class="sxs-lookup"><span data-stu-id="74166-139">This lets you save the item locally without installing it, and inspect the item contents.</span></span> <span data-ttu-id="74166-140">Mějte na paměti uložené položky odstraňte ručně.</span><span class="sxs-lookup"><span data-stu-id="74166-140">Remember to delete the saved item manually.</span></span>

<span data-ttu-id="74166-141">Některé z těchto položek jsou vytvořené microsoftem a jiné jsou vytvořené komunitou prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74166-141">Some of these items are authored by Microsoft, and others are authored by the PowerShell community.</span></span>
<span data-ttu-id="74166-142">Společnost Microsoft doporučuje, abyste si obsah a kód položek v této galerii před instalací.</span><span class="sxs-lookup"><span data-stu-id="74166-142">Microsoft recommends that you review the contents and code of items on this gallery prior to installation.</span></span>

<span data-ttu-id="74166-143">Pokud zjistíte, že položka, která máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce danou položku.</span><span class="sxs-lookup"><span data-stu-id="74166-143">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

### <a name="install"></a><span data-ttu-id="74166-144">Install</span><span class="sxs-lookup"><span data-stu-id="74166-144">Install</span></span>

<span data-ttu-id="74166-145">Pokud chcete nainstalovat položky z Galerie pro použití, spusťte [Install-Module][] nebo [Install-Script][] rutiny, v závislosti na typu položky.</span><span class="sxs-lookup"><span data-stu-id="74166-145">To install an item from the Gallery for use, run either the [Install-Module][] or [Install-Script][] cmdlet, depending on the item type.</span></span>

<span data-ttu-id="74166-146">[Install-Module][] nainstaluje modul `$env:ProgramFiles\WindowsPowerShell\Modules` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="74166-146">[Install-Module][] installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.</span></span>
<span data-ttu-id="74166-147">To vyžaduje účet správce.</span><span class="sxs-lookup"><span data-stu-id="74166-147">This requires an administrator account.</span></span> <span data-ttu-id="74166-148">Pokud chcete přidat `-Scope CurrentUser` parametr, je nainstalován modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="74166-148">If you add the `-Scope CurrentUser` parameter, the module is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span></span>

<span data-ttu-id="74166-149">[Install-Script][] skript, který nainstaluje `$env:ProgramFiles\WindowsPowerShell\Scripts` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="74166-149">[Install-Script][] installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.</span></span>
<span data-ttu-id="74166-150">To vyžaduje účet správce.</span><span class="sxs-lookup"><span data-stu-id="74166-150">This requires an administrator account.</span></span> <span data-ttu-id="74166-151">Pokud chcete přidat `-Scope CurrentUser` parametr, skript se nainstaluje do `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span><span class="sxs-lookup"><span data-stu-id="74166-151">If you add the `-Scope CurrentUser` parameter, the script is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span></span>

<span data-ttu-id="74166-152">Ve výchozím nastavení [Install-Module][] a [Install-Script][] nainstaluje nejnovější verzi položky.</span><span class="sxs-lookup"><span data-stu-id="74166-152">By default, [Install-Module][] and [Install-Script][] installs the most current version of an item.</span></span>
<span data-ttu-id="74166-153">Chcete-li nainstalovat starší verzi položky, přidejte `-RequiredVersion` parametru.</span><span class="sxs-lookup"><span data-stu-id="74166-153">To install an older version of the item, add the `-RequiredVersion` parameter.</span></span>

### <a name="deploy"></a><span data-ttu-id="74166-154">Nasazení</span><span class="sxs-lookup"><span data-stu-id="74166-154">Deploy</span></span>

<span data-ttu-id="74166-155">Pokud chcete nasadit položky z Galerie prostředí PowerShell pro Azure Automation, klikněte na tlačítko **nasadit do Azure Automation** na stránce s podrobnostmi položky.</span><span class="sxs-lookup"><span data-stu-id="74166-155">To deploy an item from the PowerShell Gallery to Azure Automation, click **Deploy to Azure Automation** on the item details page.</span></span> <span data-ttu-id="74166-156">Budete přesměrováni na portál pro správu Azure, ve kterém se přihlásíte pomocí přihlašovacích údajů k účtu Azure.</span><span class="sxs-lookup"><span data-stu-id="74166-156">You will be redirected to the Azure Management Portal, where you sign in by using your Azure account credentials.</span></span> <span data-ttu-id="74166-157">Všimněte si, že nasazení položky se závislostmi nasadí všechny závislosti na službě Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="74166-157">Note that deploying items with dependencies will deploy all the dependencies to Azure Automation.</span></span> <span data-ttu-id="74166-158">Tlačítko 'Nasazení do služby Azure Automation' můžete zakázat přidáním **AzureAutomationNotSupported** značka, které vaše metadata položky.</span><span class="sxs-lookup"><span data-stu-id="74166-158">The 'Deploy to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to your item metadata.</span></span>

<span data-ttu-id="74166-159">Další informace o Azure Automation najdete v tématu [Azure Automation](/azure/automation) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="74166-159">To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.</span></span>

## <a name="updating-items-from-the-powershell-gallery"></a><span data-ttu-id="74166-160">Aktualizace položky z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74166-160">Updating items from the PowerShell Gallery</span></span>

<span data-ttu-id="74166-161">Pokud chcete aktualizovat položky v galerii prostředí PowerShell nainstalovali, spusťte rutiny [Update-skriptu] [] nebo [[Update-Module]].</span><span class="sxs-lookup"><span data-stu-id="74166-161">To update items installed from the PowerShell Gallery, run either the [Update-Module][] or [Update-Script][] cmdlet.</span></span> <span data-ttu-id="74166-162">Po spuštění bez žádné další parametry []. [Update-Module] pokusí aktualizovat každý modul nainstalovat spuštěním [Install-Module][].</span><span class="sxs-lookup"><span data-stu-id="74166-162">When run without any additional parameters, [Update-Module][] attempts to update each module installed by running [Install-Module][].</span></span> <span data-ttu-id="74166-163">Pokud chcete selektivně aktualizovat moduly, přidejte `-Name` parametru.</span><span class="sxs-lookup"><span data-stu-id="74166-163">To selectively update modules, add the `-Name` parameter.</span></span>

<span data-ttu-id="74166-164">Podobně při spuštění bez žádné další parametry, [[Update-skriptu]] taky automatický pokus o aktualizaci každý skript instalaci spuštěním [Install-Script][].</span><span class="sxs-lookup"><span data-stu-id="74166-164">Similarly, when run without any additional parameters, [Update-Script][] also attempts to update each script installed by running [Install-Script][].</span></span> <span data-ttu-id="74166-165">Pokud chcete selektivně aktualizovat skripty, přidejte `-Name` parametru.</span><span class="sxs-lookup"><span data-stu-id="74166-165">To selectively update scripts, add the `-Name` parameter.</span></span>

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a><span data-ttu-id="74166-166">Seznam položek, které jste nainstalovali z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="74166-166">List items that you have installed from the PowerShell Gallery</span></span>

<span data-ttu-id="74166-167">Chcete-li zjistit, které moduly, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledModule][] rutiny.</span><span class="sxs-lookup"><span data-stu-id="74166-167">To find out which modules you have installed from the PowerShell Gallery, run the [Get-InstalledModule][] cmdlet.</span></span> <span data-ttu-id="74166-168">Tento příkaz vypíše všechny moduly, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74166-168">This command lists all of the modules you have on your system that were installed directly from the PowerShell Gallery.</span></span>

<span data-ttu-id="74166-169">Podobně, chcete-li zjistit, které skripty, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledScript][] rutiny.</span><span class="sxs-lookup"><span data-stu-id="74166-169">Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the [Get-InstalledScript][] cmdlet.</span></span> <span data-ttu-id="74166-170">Tento příkaz vypíše všechny skripty, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74166-170">This command lists all of the scripts you have on your system that were installed directly from the PowerShell Gallery.</span></span>

[Find-DscResource]: /powershell/module/powershellget/Find-DscResource
[Find-Module]: /powershell/module/powershellget/Find-Module
[Find-Script]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[Install-Module]: /powershell/module/powershellget/Install-Module
[Install-Script]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[Save-Module]: /powershell/module/powershellget/Save-Module
[Save-Script]: /powershell/module/powershellget/Save-Script
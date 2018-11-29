---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Začínáme s Galerie prostředí PowerShell
ms.openlocfilehash: c8beba3009e462ce52cdecd34fc0313d9234f289
ms.sourcegitcommit: 1082b13115c5c5be4b76574ba55307b3e567983f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52576885"
---
# <a name="getting-started-with-the-powershell-gallery"></a><span data-ttu-id="542c2-103">Začínáme s Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="542c2-103">Getting Started with the PowerShell Gallery</span></span>

<span data-ttu-id="542c2-104">Galerie prostředí PowerShell je úložiště balíčků, který obsahuje skripty, moduly a prostředky DSC můžete stáhnout a využít.</span><span class="sxs-lookup"><span data-stu-id="542c2-104">The PowerShell Gallery is a package repository containing scripts, modules, and DSC resources you can download and leverage.</span></span> <span data-ttu-id="542c2-105">Pomocí rutin v [PowerShellGet](/powershell/module/powershellget) modulu k instalaci balíčků z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="542c2-105">You use the cmdlets in the [PowerShellGet](/powershell/module/powershellget) module to install packages from the PowerShell Gallery.</span></span> <span data-ttu-id="542c2-106">Není nutné se přihlásit ke stažení položek z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="542c2-106">You do not need to sign in to download items from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="542c2-107">Je možné stáhnout balíček přímo z Galerie prostředí PowerShell, ale toto není doporučený postup.</span><span class="sxs-lookup"><span data-stu-id="542c2-107">It is possible to download a package from the PowerShell Gallery directly, but this is not a recommended approach.</span></span>
> <span data-ttu-id="542c2-108">Další podrobnosti najdete v tématu [ruční stažení balíčku](/powershell/gallery/how-to/working-with-packages/manual-download).</span><span class="sxs-lookup"><span data-stu-id="542c2-108">For more details, see [Manual Package Download](/powershell/gallery/how-to/working-with-packages/manual-download).</span></span>

## <a name="discovering-packages-from-the-powershell-gallery"></a><span data-ttu-id="542c2-109">Vyhledávání balíčků z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="542c2-109">Discovering packages from the PowerShell Gallery</span></span>

<span data-ttu-id="542c2-110">Balíčky můžete najít v galerii prostředí PowerShell pomocí **hledání** ovládací prvek v galerii prostředí PowerShell [domovskou stránku](https://www.powershellgallery.com), nebo že si projdete moduly a skripty z [balíčky stránky ](https://www.powershellgallery.com/packages).</span><span class="sxs-lookup"><span data-stu-id="542c2-110">You can find packages in the PowerShell Gallery by using the **Search** control on the PowerShell Gallery's [home page](https://www.powershellgallery.com), or by browsing through the Modules and Scripts from the [Packages page](https://www.powershellgallery.com/packages).</span></span> <span data-ttu-id="542c2-111">Můžete také vyhledat balíčky z Galerie prostředí PowerShell spuštěním [Find-Module][], [Find-DscResource], a [Find-Script][] rutin, v závislosti na typu balíčku s `-Repository PSGallery`.</span><span class="sxs-lookup"><span data-stu-id="542c2-111">You can also find packages from the PowerShell Gallery by running the [Find-Module][], [Find-DscResource], and [Find-Script][] cmdlets, depending on the package type, with `-Repository PSGallery`.</span></span>

<span data-ttu-id="542c2-112">Můžete filtrovat výsledky z galerie s použitím následujících parametrů:</span><span class="sxs-lookup"><span data-stu-id="542c2-112">You can filter results from the Gallery by using the following parameters:</span></span>

- <span data-ttu-id="542c2-113">Název</span><span class="sxs-lookup"><span data-stu-id="542c2-113">Name</span></span>
- <span data-ttu-id="542c2-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="542c2-114">AllVersions</span></span>
- <span data-ttu-id="542c2-115">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="542c2-115">MinimumVersion</span></span>
- <span data-ttu-id="542c2-116">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="542c2-116">RequiredVersion</span></span>
- <span data-ttu-id="542c2-117">Značka</span><span class="sxs-lookup"><span data-stu-id="542c2-117">Tag</span></span>
- <span data-ttu-id="542c2-118">Zahrnuje</span><span class="sxs-lookup"><span data-stu-id="542c2-118">Includes</span></span>
- <span data-ttu-id="542c2-119">DscResource</span><span class="sxs-lookup"><span data-stu-id="542c2-119">DscResource</span></span>
- <span data-ttu-id="542c2-120">RoleCapability</span><span class="sxs-lookup"><span data-stu-id="542c2-120">RoleCapability</span></span>
- <span data-ttu-id="542c2-121">Příkaz</span><span class="sxs-lookup"><span data-stu-id="542c2-121">Command</span></span>
- <span data-ttu-id="542c2-122">Filtr</span><span class="sxs-lookup"><span data-stu-id="542c2-122">Filter</span></span>

<span data-ttu-id="542c2-123">Pokud máte zájem zjišťování konkrétní prostředky DSC v galerii, můžete spustit [Find-DscResource] rutiny.</span><span class="sxs-lookup"><span data-stu-id="542c2-123">If you're only interested in discovering specific DSC resources in the Gallery, you can run the [Find-DscResource] cmdlet.</span></span> <span data-ttu-id="542c2-124">Find-DscResource vrací data na prostředky DSC obsažené v galerii.</span><span class="sxs-lookup"><span data-stu-id="542c2-124">Find-DscResource returns data on DSC resources contained in the Gallery.</span></span>
<span data-ttu-id="542c2-125">Protože prostředky DSC se vždy dodávají jako součást modulu, je stále potřeba spustit [Install-Module][] nainstalovat tyto prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="542c2-125">Because DSC resources are always delivered as part of a module, you still need to run [Install-Module][] to install those DSC resources.</span></span>

## <a name="learning-about-packages-in-the-powershell-gallery"></a><span data-ttu-id="542c2-126">Získání informací o balíčky v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="542c2-126">Learning about packages in the PowerShell Gallery</span></span>

<span data-ttu-id="542c2-127">Jakmile identifikujete balíček, který vás zajímá, můžete další informace o něm.</span><span class="sxs-lookup"><span data-stu-id="542c2-127">Once you've identified a package that you're interested in, you may want to learn more about it.</span></span> <span data-ttu-id="542c2-128">Můžete to provést tím, že kontroluje konkrétní stránka tento balíček v galerii.</span><span class="sxs-lookup"><span data-stu-id="542c2-128">You can do this by examining that package's specific page on the Gallery.</span></span> <span data-ttu-id="542c2-129">Na této stránce budete moct zobrazit všechny metadat nahraje spolu s balíčkem.</span><span class="sxs-lookup"><span data-stu-id="542c2-129">On that page, you'll be able to see all of the metadata uploaded with the package.</span></span> <span data-ttu-id="542c2-130">Tato metadata pochází od autora balíčku a není ověřená společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="542c2-130">This metadata is provided by the package's author, and is not verified by Microsoft.</span></span> <span data-ttu-id="542c2-131">Vlastník balíčku se silnou vazbu na galerii účet použitý k publikování balíčku a důvěryhodný více než pole Author.</span><span class="sxs-lookup"><span data-stu-id="542c2-131">The Owner of the package is strongly tied to the Gallery account used to publish the package, and is more trustworthy than the Author field.</span></span>

<span data-ttu-id="542c2-132">Pokud zjistíte, že balíček, který máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce tento balíček.</span><span class="sxs-lookup"><span data-stu-id="542c2-132">If you discover a package that you feel is not published in good faith, click **Report Abuse** on that package's page.</span></span>

<span data-ttu-id="542c2-133">Pokud používáte [Find-Module][] nebo [Find-Script][], zobrazí se tato data v vráceného objektu PSGetModuleInfo.</span><span class="sxs-lookup"><span data-stu-id="542c2-133">If you're running [Find-Module][] or [Find-Script][], you can view this data in the returned PSGetModuleInfo object.</span></span> <span data-ttu-id="542c2-134">Například systém `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span><span class="sxs-lookup"><span data-stu-id="542c2-134">For example, running `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span></span>
<span data-ttu-id="542c2-135">Vrátí data o PSReadLine modulu v galerii.</span><span class="sxs-lookup"><span data-stu-id="542c2-135">returns data on the PSReadLine module in the Gallery.</span></span>

## <a name="downloading-packages-from-the-powershell-gallery"></a><span data-ttu-id="542c2-136">Stahování balíčků z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="542c2-136">Downloading packages from the PowerShell Gallery</span></span>

<span data-ttu-id="542c2-137">Při stahování balíčků z Galerie prostředí PowerShell doporučujeme následující postup:</span><span class="sxs-lookup"><span data-stu-id="542c2-137">We encourage the following process when downloading packages from the PowerShell Gallery:</span></span>

### <a name="inspect"></a><span data-ttu-id="542c2-138">Kontrola</span><span class="sxs-lookup"><span data-stu-id="542c2-138">Inspect</span></span>

<span data-ttu-id="542c2-139">Stáhnout balíček z Galerie pro kontrolu, spusťte [Save-Module][] nebo [Save-Script][] rutiny, v závislosti na typu balíčku.</span><span class="sxs-lookup"><span data-stu-id="542c2-139">To download a package from the Gallery for inspection, run either the [Save-Module][] or [Save-Script][] cmdlet, depending on the package type.</span></span> <span data-ttu-id="542c2-140">Díky tomu můžete balíček uložit místně bez nutnosti jeho instalace a zkontrolovat obsah balíčku.</span><span class="sxs-lookup"><span data-stu-id="542c2-140">This lets you save the package locally without installing it, and inspect the package contents.</span></span> <span data-ttu-id="542c2-141">Nezapomeňte si uložený balíček odstranit ručně.</span><span class="sxs-lookup"><span data-stu-id="542c2-141">Remember to delete the saved package manually.</span></span>

<span data-ttu-id="542c2-142">Některé tyto balíčky jsou vytvořené microsoftem a jiné jsou vytvořené komunitou prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="542c2-142">Some of these packages are authored by Microsoft, and others are authored by the PowerShell community.</span></span>
<span data-ttu-id="542c2-143">Společnost Microsoft doporučuje, abyste si obsah a kód balíčky v této galerii před instalací.</span><span class="sxs-lookup"><span data-stu-id="542c2-143">Microsoft recommends that you review the contents and code of packages on this gallery prior to installation.</span></span>

<span data-ttu-id="542c2-144">Pokud zjistíte, že balíček, který máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce tento balíček.</span><span class="sxs-lookup"><span data-stu-id="542c2-144">If you discover a package that you feel is not published in good faith, click **Report Abuse** on that package's page.</span></span>

### <a name="install"></a><span data-ttu-id="542c2-145">Install</span><span class="sxs-lookup"><span data-stu-id="542c2-145">Install</span></span>

<span data-ttu-id="542c2-146">Chcete-li nainstalovat balíček z Galerie pro použití, spusťte [Install-Module][] nebo [Install-Script][] rutiny, v závislosti na typu balíčku.</span><span class="sxs-lookup"><span data-stu-id="542c2-146">To install a package from the Gallery for use, run either the [Install-Module][] or [Install-Script][] cmdlet, depending on the package type.</span></span>

<span data-ttu-id="542c2-147">[Install-Module][] nainstaluje modul `$env:ProgramFiles\WindowsPowerShell\Modules` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="542c2-147">[Install-Module][] installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.</span></span>
<span data-ttu-id="542c2-148">To vyžaduje účet správce.</span><span class="sxs-lookup"><span data-stu-id="542c2-148">This requires an administrator account.</span></span> <span data-ttu-id="542c2-149">Pokud chcete přidat `-Scope CurrentUser` parametr, je nainstalován modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="542c2-149">If you add the `-Scope CurrentUser` parameter, the module is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span></span>

<span data-ttu-id="542c2-150">[Install-Script][] skript, který nainstaluje `$env:ProgramFiles\WindowsPowerShell\Scripts` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="542c2-150">[Install-Script][] installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.</span></span>
<span data-ttu-id="542c2-151">To vyžaduje účet správce.</span><span class="sxs-lookup"><span data-stu-id="542c2-151">This requires an administrator account.</span></span> <span data-ttu-id="542c2-152">Pokud chcete přidat `-Scope CurrentUser` parametr, skript se nainstaluje do `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span><span class="sxs-lookup"><span data-stu-id="542c2-152">If you add the `-Scope CurrentUser` parameter, the script is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span></span>

<span data-ttu-id="542c2-153">Ve výchozím nastavení [Install-Module][] a [Install-Script][] nainstaluje nejnovější verzi balíčku.</span><span class="sxs-lookup"><span data-stu-id="542c2-153">By default, [Install-Module][] and [Install-Script][] installs the most current version of a package.</span></span>
<span data-ttu-id="542c2-154">Chcete-li nainstalovat starší verzi balíčku, přidejte `-RequiredVersion` parametru.</span><span class="sxs-lookup"><span data-stu-id="542c2-154">To install an older version of the package, add the `-RequiredVersion` parameter.</span></span>

### <a name="deploy"></a><span data-ttu-id="542c2-155">Nasazení</span><span class="sxs-lookup"><span data-stu-id="542c2-155">Deploy</span></span>

<span data-ttu-id="542c2-156">Chcete-li nasadit balíček z Galerie prostředí PowerShell pro Azure Automation, klikněte na tlačítko **Azure Automation**, klikněte na **nasadit do Azure Automation** na stránce s podrobnostmi balíčku.</span><span class="sxs-lookup"><span data-stu-id="542c2-156">To deploy a package from the PowerShell Gallery to Azure Automation, click **Azure Automation**, then click **Deploy to Azure Automation** on the package details page.</span></span> <span data-ttu-id="542c2-157">Budete přesměrováni na portálu pro správu Azure, ve kterém se přihlásíte pomocí přihlašovacích údajů k účtu Azure.</span><span class="sxs-lookup"><span data-stu-id="542c2-157">You are redirected to the Azure Management Portal where you sign in by using your Azure account credentials.</span></span> <span data-ttu-id="542c2-158">Všimněte si, že nasazení balíčků se závislostmi všechny závislosti nasadí do služby Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="542c2-158">Note that deploying packages with dependencies deploys all the dependencies to Azure Automation.</span></span> <span data-ttu-id="542c2-159">Tlačítko 'Nasazení do služby Azure Automation' můžete zakázat přidáním **AzureAutomationNotSupported** značka, které vaše metadata balíčku.</span><span class="sxs-lookup"><span data-stu-id="542c2-159">The 'Deploy to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to your package metadata.</span></span>

<span data-ttu-id="542c2-160">Další informace o Azure Automation najdete v tématu [Azure Automation](/azure/automation) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="542c2-160">To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.</span></span>

## <a name="updating-packages-from-the-powershell-gallery"></a><span data-ttu-id="542c2-161">Aktualizace balíčků z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="542c2-161">Updating packages from the PowerShell Gallery</span></span>

<span data-ttu-id="542c2-162">Pokud chcete aktualizovat balíčky nainstalované z Galerie prostředí PowerShell, spusťte rutiny [Update-skriptu] [] nebo [[Update-Module]].</span><span class="sxs-lookup"><span data-stu-id="542c2-162">To update packages installed from the PowerShell Gallery, run either the [Update-Module][] or [Update-Script][] cmdlet.</span></span> <span data-ttu-id="542c2-163">Při spuštění bez žádné další parametry, [[Update-Module]] pokusí aktualizovat všechny moduly nainstalované spuštěním [Install-Module][].</span><span class="sxs-lookup"><span data-stu-id="542c2-163">When run without any additional parameters, [Update-Module][] attempts to update all modules installed by running [Install-Module][].</span></span> <span data-ttu-id="542c2-164">Pokud chcete selektivně aktualizovat moduly, přidejte `-Name` parametru.</span><span class="sxs-lookup"><span data-stu-id="542c2-164">To selectively update modules, add the `-Name` parameter.</span></span> 

<span data-ttu-id="542c2-165">Podobně při spuštění bez žádné další parametry, [] [-skript pro aktualizaci] taky automatický pokus o aktualizaci nainstalovat spuštěním všechny skripty [Install-Script][].</span><span class="sxs-lookup"><span data-stu-id="542c2-165">Similarly, when run without any additional parameters, [Update-Script][] also attempts to update all scripts installed by running [Install-Script][].</span></span> <span data-ttu-id="542c2-166">Pokud chcete selektivně aktualizovat skripty, přidejte `-Name` parametru.</span><span class="sxs-lookup"><span data-stu-id="542c2-166">To selectively update scripts, add the `-Name` parameter.</span></span>

## <a name="list-packages-that-you-have-installed-from-the-powershell-gallery"></a><span data-ttu-id="542c2-167">Seznam balíčků, které jste nainstalovali z Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="542c2-167">List packages that you have installed from the PowerShell Gallery</span></span>

<span data-ttu-id="542c2-168">Chcete-li zjistit, které moduly, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledModule][] rutiny.</span><span class="sxs-lookup"><span data-stu-id="542c2-168">To find out which modules you have installed from the PowerShell Gallery, run the [Get-InstalledModule][] cmdlet.</span></span> <span data-ttu-id="542c2-169">Tento příkaz vypíše všechny moduly, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="542c2-169">This command lists all of the modules you have on your system that were installed directly from the PowerShell Gallery.</span></span>

<span data-ttu-id="542c2-170">Podobně, chcete-li zjistit, které skripty, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledScript][] rutiny.</span><span class="sxs-lookup"><span data-stu-id="542c2-170">Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the [Get-InstalledScript][] cmdlet.</span></span> <span data-ttu-id="542c2-171">Tento příkaz vypíše všechny skripty, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="542c2-171">This command lists all of the scripts you have on your system that were installed directly from the PowerShell Gallery.</span></span>

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

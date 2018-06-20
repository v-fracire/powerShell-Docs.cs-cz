---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Začínáme s Galerie prostředí PowerShell
ms.openlocfilehash: 83974698152e75efac66ea725a9c220486676d6f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190158"
---
# <a name="get-started-with-the-powershell-gallery"></a><span data-ttu-id="4b714-103">Začínáme s Galerie prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b714-103">Get Started with the PowerShell Gallery</span></span>

<span data-ttu-id="4b714-104">Stahování položky z Galerie prostředí PowerShell k vašemu systému vyžaduje [PowerShellGet](/powershell/module/powershellget) modulu.</span><span class="sxs-lookup"><span data-stu-id="4b714-104">Downloading items from the PowerShell Gallery to your system requires the [PowerShellGet](/powershell/module/powershellget) module.</span></span> <span data-ttu-id="4b714-105">Modul PowerShellGet najdete v některém z následujících akcí.</span><span class="sxs-lookup"><span data-stu-id="4b714-105">You can find the PowerShellGet module in any of the following.</span></span> <span data-ttu-id="4b714-106">Není nutné se přihlásit ke stažení položky z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b714-106">You do not need to sign in to download items from the PowerShell Gallery.</span></span>

## <a name="discovering-items-from-the-powershell-gallery"></a><span data-ttu-id="4b714-107">Zjišťování položky z Galerie Powershellu</span><span class="sxs-lookup"><span data-stu-id="4b714-107">Discovering items from the PowerShell Gallery</span></span>

<span data-ttu-id="4b714-108">Položky v galerii prostředí PowerShell můžete najít pomocí **vyhledávání** ovládacího prvku na tomto webu, nebo procházením prostřednictvím stránky moduly a skripty.</span><span class="sxs-lookup"><span data-stu-id="4b714-108">You can find items in the PowerShell Gallery by using the **Search** control on this website, or by browsing through the Modules and Scripts pages.</span></span> <span data-ttu-id="4b714-109">Můžete také získat položky z Galerie Powershellu spuštěním [najít modul][] a [najít skriptu][] rutin, v závislosti na typu položky s `-Repository PSGallery`.</span><span class="sxs-lookup"><span data-stu-id="4b714-109">You can also find items from the PowerShell Gallery by running the [Find-Module][] and [Find-Script][] cmdlets, depending on the item type, with `-Repository PSGallery`.</span></span>

<span data-ttu-id="4b714-110">Filtrování výsledků z galerie lze provést pomocí následujících parametrů:</span><span class="sxs-lookup"><span data-stu-id="4b714-110">Filtering results from the Gallery can be done by using the following parameters:</span></span>

- <span data-ttu-id="4b714-111">Název</span><span class="sxs-lookup"><span data-stu-id="4b714-111">Name</span></span>
- <span data-ttu-id="4b714-112">AllVersions</span><span class="sxs-lookup"><span data-stu-id="4b714-112">AllVersions</span></span>
- <span data-ttu-id="4b714-113">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="4b714-113">MinimumVersion</span></span>
- <span data-ttu-id="4b714-114">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="4b714-114">RequiredVersion</span></span>
- <span data-ttu-id="4b714-115">Značka</span><span class="sxs-lookup"><span data-stu-id="4b714-115">Tag</span></span>
- <span data-ttu-id="4b714-116">Zahrnuje</span><span class="sxs-lookup"><span data-stu-id="4b714-116">Includes</span></span>
- <span data-ttu-id="4b714-117">DscResource</span><span class="sxs-lookup"><span data-stu-id="4b714-117">DscResource</span></span>
- <span data-ttu-id="4b714-118">RoleCapability</span><span class="sxs-lookup"><span data-stu-id="4b714-118">RoleCapability</span></span>
- <span data-ttu-id="4b714-119">Příkaz</span><span class="sxs-lookup"><span data-stu-id="4b714-119">Command</span></span>
- <span data-ttu-id="4b714-120">Filtr</span><span class="sxs-lookup"><span data-stu-id="4b714-120">Filter</span></span>

<span data-ttu-id="4b714-121">Pokud byste chtěli pouze konkrétní prostředky DSC v galerii zjišťování, můžete spustit [najít DscResource] rutiny.</span><span class="sxs-lookup"><span data-stu-id="4b714-121">If you're only interested in discovering specific DSC resources in the Gallery, you can run the [Find-DscResource] cmdlet.</span></span> <span data-ttu-id="4b714-122">Najít DscResource vrací data na prostředky DSC obsažené v galerii.</span><span class="sxs-lookup"><span data-stu-id="4b714-122">Find-DscResource returns data on DSC resources contained in the Gallery.</span></span>
<span data-ttu-id="4b714-123">Protože prostředky DSC jsou vždy dodávána jako součást modulu, potřebujete stále spustit [instalace modulu][] nainstalovat tyto prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="4b714-123">Because DSC resources are always delivered as part of a module, you still need to run [Install-Module][] to install those DSC resources.</span></span>

## <a name="learning-about-items-in-the-powershell-gallery"></a><span data-ttu-id="4b714-124">Získávání informací o položky v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b714-124">Learning about items in the PowerShell Gallery</span></span>

<span data-ttu-id="4b714-125">Jakmile jste zformulovali položky, které vás zajímají, můžete další informace o něm.</span><span class="sxs-lookup"><span data-stu-id="4b714-125">Once you've identified an item you're interested in, you may want to learn more about it.</span></span> <span data-ttu-id="4b714-126">To provedete tak, že prověří daná položka konkrétní stránky v galerii.</span><span class="sxs-lookup"><span data-stu-id="4b714-126">You can do this by examining that item's specific page on the Gallery.</span></span> <span data-ttu-id="4b714-127">Na této stránce budete moci zobrazit všechny metadat nahrán s položkou.</span><span class="sxs-lookup"><span data-stu-id="4b714-127">On that page, you'll be able to see all of the metadata uploaded with the item.</span></span> <span data-ttu-id="4b714-128">Tato metadata položky od autora položky a není ověřen společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4b714-128">This metadata for an item is provided by the item's author, and is not verified by Microsoft.</span></span> <span data-ttu-id="4b714-129">Vlastník položky je důrazně vázaný na Galerie účet použitý k publikování položku a více důvěryhodný než pole Author.</span><span class="sxs-lookup"><span data-stu-id="4b714-129">The Owner of the item is strongly tied to the Gallery account used to publish the item, and is more trustworthy than the Author field.</span></span>

<span data-ttu-id="4b714-130">Pokud zjistíte, že položku, která si myslíte, že není publikována v dobré víře, klikněte na tlačítko **oznámení zneužití** na stránce této položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-130">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

<span data-ttu-id="4b714-131">Pokud používáte [najít modul][] nebo [najít skriptu][], zobrazí se tato data v vráceného objektu PSGetModuleInfo.</span><span class="sxs-lookup"><span data-stu-id="4b714-131">If you're running [Find-Module][] or [Find-Script][], you can view this data in the returned PSGetModuleInfo object.</span></span> <span data-ttu-id="4b714-132">Například běžet `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member` vrací data v modulu PSReadLine v galerii.</span><span class="sxs-lookup"><span data-stu-id="4b714-132">For example, running `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member` returns data on the PSReadLine module in the Gallery.</span></span>

## <a name="downloading-items-from-the-powershell-gallery"></a><span data-ttu-id="4b714-133">Při stahování položky z Galerie Powershellu</span><span class="sxs-lookup"><span data-stu-id="4b714-133">Downloading items from the PowerShell Gallery</span></span>

<span data-ttu-id="4b714-134">Při stahování položky z Galerie Powershellu doporučujeme následující proces:</span><span class="sxs-lookup"><span data-stu-id="4b714-134">We encourage the following process when downloading items from the PowerShell Gallery:</span></span>

### <a name="inspect"></a><span data-ttu-id="4b714-135">Kontrola</span><span class="sxs-lookup"><span data-stu-id="4b714-135">Inspect</span></span>

<span data-ttu-id="4b714-136">Ke stažení položky z Galerie pro kontrolu, spusťte [uložit modulu][] nebo [uložit skript][] rutiny, v závislosti na typu položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-136">To download an item from the Gallery for inspection, run either the [Save-Module][] or [Save-Script][] cmdlet, depending on the item type.</span></span> <span data-ttu-id="4b714-137">To vám umožní uložit položku místně bez nutnosti její instalace a zkontrolovat obsah položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-137">This lets you save the item locally without installing it, and inspect the item contents.</span></span> <span data-ttu-id="4b714-138">Mějte na paměti, odstraňte uložený položku ručně.</span><span class="sxs-lookup"><span data-stu-id="4b714-138">Remember to delete the saved item manually.</span></span>

<span data-ttu-id="4b714-139">Některé z těchto položek vytvořené společností Microsoft a ostatní vytvořené komunitou prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b714-139">Some of these items are authored by Microsoft, and others are authored by the PowerShell community.</span></span>
<span data-ttu-id="4b714-140">Společnost Microsoft doporučuje zkontrolovat obsah a kód položky v této galerii před instalací.</span><span class="sxs-lookup"><span data-stu-id="4b714-140">Microsoft recommends that you review the contents and code of items on this gallery prior to installation.</span></span>

<span data-ttu-id="4b714-141">Pokud zjistíte, že položku, která si myslíte, že není publikována v dobré víře, klikněte na tlačítko **oznámení zneužití** na stránce této položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-141">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

### <a name="install"></a><span data-ttu-id="4b714-142">Install</span><span class="sxs-lookup"><span data-stu-id="4b714-142">Install</span></span>

<span data-ttu-id="4b714-143">Chcete-li nainstalovat položky z Galerie pro použití, spusťte [instalace modulu][] nebo [instalační skript][] rutiny, v závislosti na typu položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-143">To install an item from the Gallery for use, run either the [Install-Module][] or [Install-Script][] cmdlet, depending on the item type.</span></span>

<span data-ttu-id="4b714-144">[instalace modulu][] nainstaluje modul pro `$env:ProgramFiles\WindowsPowerShell\Modules` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="4b714-144">[Install-Module][] installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.</span></span>
<span data-ttu-id="4b714-145">To vyžaduje účet správce.</span><span class="sxs-lookup"><span data-stu-id="4b714-145">This requires an administrator account.</span></span> <span data-ttu-id="4b714-146">Pokud přidáte `-Scope CurrentUser` parametru, je nainstalován modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="4b714-146">If you add the `-Scope CurrentUser` parameter, the module is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span></span>

<span data-ttu-id="4b714-147">[instalační skript][] nainstaluje skript, který chcete `$env:ProgramFiles\WindowsPowerShell\Scripts` ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="4b714-147">[Install-Script][] installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.</span></span>
<span data-ttu-id="4b714-148">To vyžaduje účet správce.</span><span class="sxs-lookup"><span data-stu-id="4b714-148">This requires an administrator account.</span></span> <span data-ttu-id="4b714-149">Pokud přidáte `-Scope CurrentUser` parametr skript je nainstalován do `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span><span class="sxs-lookup"><span data-stu-id="4b714-149">If you add the `-Scope CurrentUser` parameter, the script is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span></span>

<span data-ttu-id="4b714-150">Ve výchozím nastavení [instalace modulu][] a [instalační skript][] nainstaluje nejnovější verzi položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-150">By default, [Install-Module][] and [Install-Script][] installs the most current version of an item.</span></span>
<span data-ttu-id="4b714-151">Chcete-li nainstalovat starší verzi položky, přidejte `-RequiredVersion` parametr.</span><span class="sxs-lookup"><span data-stu-id="4b714-151">To install an older version of the item, add the `-RequiredVersion` parameter.</span></span>

### <a name="deploy"></a><span data-ttu-id="4b714-152">Nasazení</span><span class="sxs-lookup"><span data-stu-id="4b714-152">Deploy</span></span>

<span data-ttu-id="4b714-153">Chcete-li nasadit položky z Galerie prostředí PowerShell pro Azure Automation, klikněte na tlačítko **nasadit do Azure Automation** na stránce podrobností položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-153">To deploy an item from the PowerShell Gallery to Azure Automation, click **Deploy to Azure Automation** on the item details page.</span></span> <span data-ttu-id="4b714-154">Budete přesměrováni na portálu Azure Management Portal, kde se přihlásíte pomocí svých přihlašovacích údajů účtu Azure.</span><span class="sxs-lookup"><span data-stu-id="4b714-154">You will be redirected to the Azure Management Portal, where you sign in by using your Azure account credentials.</span></span> <span data-ttu-id="4b714-155">Všimněte si, že nasazení položky se závislostmi nasadí všechny závislosti pro Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4b714-155">Note that deploying items with dependencies will deploy all the dependencies to Azure Automation.</span></span> <span data-ttu-id="4b714-156">Tlačítko "nasadit do Azure Automation, lze zakázat tak, že přidáte **AzureAutomationNotSupported** značku metadata položky.</span><span class="sxs-lookup"><span data-stu-id="4b714-156">The 'Deploy to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to your item metadata.</span></span>

<span data-ttu-id="4b714-157">Další informace o Azure Automation najdete v tématu [Azure Automation](/azure/automation) dokumentaci.</span><span class="sxs-lookup"><span data-stu-id="4b714-157">To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.</span></span>

## <a name="updating-items-from-the-powershell-gallery"></a><span data-ttu-id="4b714-158">Aktualizace položky z Galerie Powershellu</span><span class="sxs-lookup"><span data-stu-id="4b714-158">Updating items from the PowerShell Gallery</span></span>

<span data-ttu-id="4b714-159">Pokud chcete aktualizovat položky nainstalovat z Galerie prostředí PowerShell, spusťte buď [] – [aktualizace-Module] nebo [skript aktualizace] [] rutiny.</span><span class="sxs-lookup"><span data-stu-id="4b714-159">To update items installed from the PowerShell Gallery, run either the [Update-Module][] or [Update-Script][] cmdlet.</span></span> <span data-ttu-id="4b714-160">Když se spustí bez dalších parametrů, [] – [aktualizace-Module] pokusí aktualizovat každý modul nainstalovaný spuštěním [instalace modulu][].</span><span class="sxs-lookup"><span data-stu-id="4b714-160">When run without any additional parameters, [Update-Module][] attempts to update each module installed by running [Install-Module][].</span></span> <span data-ttu-id="4b714-161">Chcete-li selektivně aktualizovat moduly, přidejte `-Name` parametr.</span><span class="sxs-lookup"><span data-stu-id="4b714-161">To selectively update modules, add the `-Name` parameter.</span></span>

<span data-ttu-id="4b714-162">Podobně když se spustí bez dalších parametrů, [] – [skript aktualizace] také pokusí aktualizovat každý skript nainstalovaná, spuštěním [instalační skript][].</span><span class="sxs-lookup"><span data-stu-id="4b714-162">Similarly, when run without any additional parameters, [Update-Script][] also attempts to update each script installed by running [Install-Script][].</span></span> <span data-ttu-id="4b714-163">Chcete-li selektivně aktualizovat skripty, přidejte `-Name` parametr.</span><span class="sxs-lookup"><span data-stu-id="4b714-163">To selectively update scripts, add the `-Name` parameter.</span></span>

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a><span data-ttu-id="4b714-164">Seznam položek, které jste nainstalovali z Galerie Powershellu</span><span class="sxs-lookup"><span data-stu-id="4b714-164">List items that you have installed from the PowerShell Gallery</span></span>

<span data-ttu-id="4b714-165">Chcete-li zjistit, které moduly, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledModule][] rutiny.</span><span class="sxs-lookup"><span data-stu-id="4b714-165">To find out which modules you have installed from the PowerShell Gallery, run the [Get-InstalledModule][] cmdlet.</span></span> <span data-ttu-id="4b714-166">Tento příkaz vypíše všechny moduly, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b714-166">This command lists all of the modules you have on your system that were installed directly from the PowerShell Gallery.</span></span>

<span data-ttu-id="4b714-167">Podobně, chcete-li zjistit, které skripty, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledScript][] rutiny.</span><span class="sxs-lookup"><span data-stu-id="4b714-167">Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the [Get-InstalledScript][] cmdlet.</span></span> <span data-ttu-id="4b714-168">Tento příkaz vypíše všechny skripty, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b714-168">This command lists all of the scripts you have on your system that were installed directly from the PowerShell Gallery.</span></span>

[najít DscResource]: /powershell/module/powershellget/Find-DscResource
[Find-DscResource]: /powershell/module/powershellget/Find-DscResource
[najít modul]: /powershell/module/powershellget/Find-Module
[Find-Module]: /powershell/module/powershellget/Find-Module
[najít skriptu]: /powershell/module/powershellget/Find-Script
[Find-Script]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[instalace modulu]: /powershell/module/powershellget/Install-Module
[Install-Module]: /powershell/module/powershellget/Install-Module
[instalační skript]: /powershell/module/powershellget/Install-Script
[Install-Script]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[uložit modulu]: /powershell/module/powershellget/Save-Module
[Save-Module]: /powershell/module/powershellget/Save-Module
[uložit skript]: /powershell/module/powershellget/Save-Script
[Save-Script]: /powershell/module/powershellget/Save-Script
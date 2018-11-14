---
ms.date: 11/06/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery, psget
title: Práce s místním PSRepositories
ms.openlocfilehash: 94824ea584c097838b24c6f2cd02407b6147a781
ms.sourcegitcommit: 91786b03704fbd2d185f674df0bc67faddfb6288
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2018
ms.locfileid: "51619250"
---
# <a name="working-with-local-powershellget-repositories"></a><span data-ttu-id="14c6c-103">Práce s místním úložišti PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="14c6c-103">Working with local PowerShellGet Repositories</span></span>

<span data-ttu-id="14c6c-104">Modul PowerShellGet podporu úložišť než v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14c6c-104">The PowerShellGet module support repositories other than the PowerShell Gallery.</span></span>
<span data-ttu-id="14c6c-105">Tyto rutiny se podporují následující scénáře:</span><span class="sxs-lookup"><span data-stu-id="14c6c-105">These cmdlets enable the following scenarios:</span></span>

- <span data-ttu-id="14c6c-106">Podpora důvěryhodné, předběžně ověřená sadu moduly Powershellu pro použití ve vašem prostředí</span><span class="sxs-lookup"><span data-stu-id="14c6c-106">Support a trusted, pre-validated set of PowerShell modules for use in your environment</span></span>
- <span data-ttu-id="14c6c-107">Testování kanálu CI/CD, který sestaví moduly Powershellu nebo skriptů</span><span class="sxs-lookup"><span data-stu-id="14c6c-107">Testing a CI/CD pipeline that builds PowerShell modules or scripts</span></span>
- <span data-ttu-id="14c6c-108">Doručování Powershellové skripty a moduly pro systémy, které nemá přístup k Internetu</span><span class="sxs-lookup"><span data-stu-id="14c6c-108">Deliver PowerShell scripts and modules to systems that can't access the internet</span></span>

<span data-ttu-id="14c6c-109">Tento článek popisuje, jak nastavit místní úložiště prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14c6c-109">This article describes how to set up a local PowerShell repository.</span></span> <span data-ttu-id="14c6c-110">Tento článek také popisuje [OfflinePowerShellGetDeploy][] modulu k dispozici z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14c6c-110">The article also covers the [OfflinePowerShellGetDeploy][] module available from the PowerShell Gallery.</span></span> <span data-ttu-id="14c6c-111">Tento modul obsahuje rutiny pro instalaci na nejnovější verzi modulu PowerShellGet do svého místního úložiště.</span><span class="sxs-lookup"><span data-stu-id="14c6c-111">This module contains cmdlets to install the latest version of PowerShellGet into your local repository.</span></span>

## <a name="local-repository-types"></a><span data-ttu-id="14c6c-112">Typy místního úložiště</span><span class="sxs-lookup"><span data-stu-id="14c6c-112">Local repository types</span></span>

<span data-ttu-id="14c6c-113">Existují dva způsoby, jak vytvořit místní PSRepository: NuGet server nebo sdílená složka.</span><span class="sxs-lookup"><span data-stu-id="14c6c-113">There are two ways to create a local PSRepository: NuGet server or file share.</span></span> <span data-ttu-id="14c6c-114">Každý typ má své výhody a nevýhody:</span><span class="sxs-lookup"><span data-stu-id="14c6c-114">Each type has advantages and disadvantages:</span></span>

<span data-ttu-id="14c6c-115">NuGet Server</span><span class="sxs-lookup"><span data-stu-id="14c6c-115">NuGet Server</span></span>

| <span data-ttu-id="14c6c-116">Výhody</span><span class="sxs-lookup"><span data-stu-id="14c6c-116">Advantages</span></span>| <span data-ttu-id="14c6c-117">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="14c6c-117">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="14c6c-118">Úzce napodobuje funkce PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="14c6c-118">Closely mimics PowerShellGallery functionality</span></span> | <span data-ttu-id="14c6c-119">Vícevrstvé aplikace vyžaduje plánování operací a podpora</span><span class="sxs-lookup"><span data-stu-id="14c6c-119">Multi-tier app requires operations planning & support</span></span> |
| <span data-ttu-id="14c6c-120">NuGet se integruje se sadou Visual Studio a další nástroje</span><span class="sxs-lookup"><span data-stu-id="14c6c-120">NuGet integrates with Visual Studio, other tools</span></span> | <span data-ttu-id="14c6c-121">Model ověřování a správy účtů NuGet</span><span class="sxs-lookup"><span data-stu-id="14c6c-121">Authentication model and NuGet accounts management needed</span></span> |
| <span data-ttu-id="14c6c-122">Podporuje metadata v NuGet `.Nupkg` balíčky</span><span class="sxs-lookup"><span data-stu-id="14c6c-122">NuGet supports metadata in `.Nupkg` packages</span></span> | <span data-ttu-id="14c6c-123">Publikování vyžaduje klíč rozhraní API pro správu a údržbu</span><span class="sxs-lookup"><span data-stu-id="14c6c-123">Publishing requires API Key management & maintenance</span></span> |
| <span data-ttu-id="14c6c-124">Poskytuje hledání, Správa balíčků, atd.</span><span class="sxs-lookup"><span data-stu-id="14c6c-124">Provides search, package administration, etc.</span></span> | |

<span data-ttu-id="14c6c-125">Sdílené složky</span><span class="sxs-lookup"><span data-stu-id="14c6c-125">File Share</span></span>

| <span data-ttu-id="14c6c-126">Výhody</span><span class="sxs-lookup"><span data-stu-id="14c6c-126">Advantages</span></span>| <span data-ttu-id="14c6c-127">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="14c6c-127">Disadvantages</span></span> |
| --- | --- |
| <span data-ttu-id="14c6c-128">Snadné nastavení, zálohování a údržbě</span><span class="sxs-lookup"><span data-stu-id="14c6c-128">Easy to set up, back up, and maintain</span></span> | <span data-ttu-id="14c6c-129">Metadata, používá modul PowerShellGet není k dispozici</span><span class="sxs-lookup"><span data-stu-id="14c6c-129">Metadata used by PowerShellGet isn't available</span></span> |
| <span data-ttu-id="14c6c-130">Model zabezpečení Simple - uživatelských oprávnění pro sdílenou složku</span><span class="sxs-lookup"><span data-stu-id="14c6c-130">Simple security model - user permissions on the share</span></span> | <span data-ttu-id="14c6c-131">Žádné uživatelské rozhraní nad rámec základní sdílenou složku</span><span class="sxs-lookup"><span data-stu-id="14c6c-131">No UI beyond basic file share</span></span> |
| <span data-ttu-id="14c6c-132">Bez omezení, jako je například nahrazení existujících položek</span><span class="sxs-lookup"><span data-stu-id="14c6c-132">No constraints such as replacing existing items</span></span> | <span data-ttu-id="14c6c-133">Omezené zabezpečení a žádný záznam, co aktualizace</span><span class="sxs-lookup"><span data-stu-id="14c6c-133">Limited security and no recording of who updates what</span></span> |

<span data-ttu-id="14c6c-134">Správce balíčků PowerShellGet funguje s typem a podporuje vyhledávání verze a instalace závislostí.</span><span class="sxs-lookup"><span data-stu-id="14c6c-134">PowerShellGet works with either type and supports locating versions and dependency installation.</span></span>
<span data-ttu-id="14c6c-135">Ale některé funkce, které fungují pro galerii prostředí PowerShell nejsou k dispozici pro základní servery NuGet nebo sdílené složky.</span><span class="sxs-lookup"><span data-stu-id="14c6c-135">However, some features that work for the PowerShell Gallery aren't available for base NuGet servers or file shares.</span></span>

- <span data-ttu-id="14c6c-136">Všechno, co je balíček – bez rozdílů mezi skripty, moduly, prostředky DSC nebo funkce role.</span><span class="sxs-lookup"><span data-stu-id="14c6c-136">Everything is a package - no differentiation of scripts, modules, DSC resources, or role capabilities.</span></span>
- <span data-ttu-id="14c6c-137">Souborové servery se sdílená složka neuvidí metadata balíčků, včetně značek.</span><span class="sxs-lookup"><span data-stu-id="14c6c-137">File share servers can't see package metadata, including tags.</span></span>

## <a name="creating-a-local-repository"></a><span data-ttu-id="14c6c-138">Vytvořit místní úložiště</span><span class="sxs-lookup"><span data-stu-id="14c6c-138">Creating a local repository</span></span>

<span data-ttu-id="14c6c-139">V následujícím článku jsou uvedené kroky pro nastavení serveru NuGet.</span><span class="sxs-lookup"><span data-stu-id="14c6c-139">The following article lists the steps for setting up your own NuGet Server.</span></span>

- <span data-ttu-id="14c6c-140">[NuGet.Server][]</span><span class="sxs-lookup"><span data-stu-id="14c6c-140">[NuGet.Server][]</span></span>

<span data-ttu-id="14c6c-141">Postupujte podle pokynů až do okamžiku přidávání balíčků.</span><span class="sxs-lookup"><span data-stu-id="14c6c-141">Follow the steps up to the point of adding packages.</span></span> <span data-ttu-id="14c6c-142">Kroky pro [publikovat balíček](#publishing-to-a-local-repository) jsou popsané dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="14c6c-142">The steps for [publishing a package](#publishing-to-a-local-repository) are covered later in this article.</span></span>

<span data-ttu-id="14c6c-143">Na základě sdílené složky úložiště souborů Ujistěte se, aby uživatelé měli oprávnění pro přístup ke sdílené složce.</span><span class="sxs-lookup"><span data-stu-id="14c6c-143">For a file share-based repository, make sure that your users have permissions to access the file share.</span></span>

## <a name="registering-a-local-repository"></a><span data-ttu-id="14c6c-144">Registrace místní úložiště</span><span class="sxs-lookup"><span data-stu-id="14c6c-144">Registering a local repository</span></span>

<span data-ttu-id="14c6c-145">Před použitím úložiště, je nutné jej zaregistrovat pomocí `Register-PSRepository` příkazu.</span><span class="sxs-lookup"><span data-stu-id="14c6c-145">Before a repository can be used, it must be registered using the `Register-PSRepository` command.</span></span>
<span data-ttu-id="14c6c-146">V příkladech níže **InstallationPolicy** je nastavena na *důvěryhodné*, za předpokladu, že důvěřujete vlastního úložiště.</span><span class="sxs-lookup"><span data-stu-id="14c6c-146">In the examples below, the **InstallationPolicy** is set to *Trusted*, on the assumption that you trust your own repository.</span></span>

```powershell
# Register a NuGet-based server
Register-PSRepository -Name LocalPSRepo -SourceLocation http://MyLocalNuget/Api/V2/ -ScriptSourceLocation http://MyLocalNuget/Api/V2 -InstallationPolicy Trusted

# Register a file share on my local machine
Register-PSRepository -Name LocalPSRepo -SourceLocation '\\localhost\PSRepoLocal\' -ScriptSourceLocation '\\localhost\PSRepoLocal\' -InstallationPolicy Trusted
```

<span data-ttu-id="14c6c-147">Poznamenejte si hodnotu rozdílu mezi způsob, jakým dva příkazy pracovat **ScriptSourceLocation**.</span><span class="sxs-lookup"><span data-stu-id="14c6c-147">Take note of the difference between how the two commands handle **ScriptSourceLocation**.</span></span> <span data-ttu-id="14c6c-148">Pro soubor úložiště založené na sdílenou složku **SourceLocation** a **ScriptSourceLocation** se musí shodovat.</span><span class="sxs-lookup"><span data-stu-id="14c6c-148">For a file share-based repositories, the **SourceLocation** and **ScriptSourceLocation** must match.</span></span> <span data-ttu-id="14c6c-149">Pro úložiště založeného na webu, musí být jiný, takže v tomto příkladu koncový znak "/" se přidá do **SourceLocation**.</span><span class="sxs-lookup"><span data-stu-id="14c6c-149">For a web-based repository, they must be different, so in this example a trailing "/" is added to the **SourceLocation**.</span></span>

<span data-ttu-id="14c6c-150">Pokud chcete nově vytvořenou PSRepository výchozí úložiště, musíte zrušit registraci jiných PSRepositories.</span><span class="sxs-lookup"><span data-stu-id="14c6c-150">If you want the newly created PSRepository to be the default repository, you must unregister all other PSRepositories.</span></span> <span data-ttu-id="14c6c-151">Příklad:</span><span class="sxs-lookup"><span data-stu-id="14c6c-151">For example:</span></span>

```powershell
Unregister-PSRepository -Name PSGallery
```

> [!NOTE]
> <span data-ttu-id="14c6c-152">Název úložiště 'PSGallery' je vyhrazený pro použití ve galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14c6c-152">The repository name 'PSGallery' is reserved for use by the PowerShell Gallery.</span></span> <span data-ttu-id="14c6c-153">Můžete zrušit registraci PSGallery, ale nemůže znovu použít název PSGallery jakéhokoli jiného úložiště.</span><span class="sxs-lookup"><span data-stu-id="14c6c-153">You can unregister PSGallery, but you cannot reuse the name PSGallery for any other repository.</span></span>

<span data-ttu-id="14c6c-154">Pokud je potřeba obnovit PSGallery, spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="14c6c-154">If you need to restore the PSGallery, run the following command:</span></span>

```powershell
Register-PSRepository -Default
```

## <a name="publishing-to-a-local-repository"></a><span data-ttu-id="14c6c-155">Publikování do místního úložiště</span><span class="sxs-lookup"><span data-stu-id="14c6c-155">Publishing to a local repository</span></span>

<span data-ttu-id="14c6c-156">Po zaregistrování místního PSRepository, můžete publikovat místní PSRepository.</span><span class="sxs-lookup"><span data-stu-id="14c6c-156">Once you've registered the local PSRepository, you can publish to your local PSRepository.</span></span> <span data-ttu-id="14c6c-157">Existují dva základní scénáře publikování: publikování vlastní modul a publikování modulu z PSGallery.</span><span class="sxs-lookup"><span data-stu-id="14c6c-157">There are two main publishing scenarios: publishing your own module and publishing a module from the PSGallery.</span></span>

### <a name="publishing-a-module-you-authored"></a><span data-ttu-id="14c6c-158">Publikování modul, který jste vytvořili</span><span class="sxs-lookup"><span data-stu-id="14c6c-158">Publishing a module you authored</span></span>

<span data-ttu-id="14c6c-159">Použití `Publish-Module` a `Publish-Script` publikovat modul Místní PSRepository stejným způsobem jako v galerii prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14c6c-159">Use `Publish-Module` and `Publish-Script` to publish your module to your local PSRepository the same way you do for the PowerShell Gallery.</span></span>

- <span data-ttu-id="14c6c-160">Zadejte umístění pro váš kód</span><span class="sxs-lookup"><span data-stu-id="14c6c-160">Specify the location for your code</span></span>
- <span data-ttu-id="14c6c-161">Zadejte klíč rozhraní API</span><span class="sxs-lookup"><span data-stu-id="14c6c-161">Supply an API key</span></span>
- <span data-ttu-id="14c6c-162">Zadejte název úložiště.</span><span class="sxs-lookup"><span data-stu-id="14c6c-162">Specify the repository name.</span></span> <span data-ttu-id="14c6c-163">Například `-PSRepository LocalPSRepo`.</span><span class="sxs-lookup"><span data-stu-id="14c6c-163">For example, `-PSRepository LocalPSRepo`</span></span>

> [!NOTE]
> <span data-ttu-id="14c6c-164">Musíte vytvořit účet na serveru NuGet a přihlaste se k vygenerování a uložit klíč rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="14c6c-164">You must create an account in the NuGet server, then sign in to generate and save the API key.</span></span>
> <span data-ttu-id="14c6c-165">Pro sdílenou složku použijte pro hodnotu NuGetApiKey jakýkoli neprázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="14c6c-165">For a file share, use any non-blank string for the NuGetApiKey value.</span></span>

<span data-ttu-id="14c6c-166">Příklady:</span><span class="sxs-lookup"><span data-stu-id="14c6c-166">Examples:</span></span>

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> <span data-ttu-id="14c6c-167">Abyste zajistili bezpečnost, klíče rozhraní API by neměl být pevně zakódovaný ve skriptech.</span><span class="sxs-lookup"><span data-stu-id="14c6c-167">To ensure security, API keys should not be hard-coded in scripts.</span></span> <span data-ttu-id="14c6c-168">Používejte systém zabezpečená správa klíčů.</span><span class="sxs-lookup"><span data-stu-id="14c6c-168">Use a secure key management system.</span></span>

### <a name="publishing-a-module-from-the-psgallery"></a><span data-ttu-id="14c6c-169">Publikování z PSGallery modulu</span><span class="sxs-lookup"><span data-stu-id="14c6c-169">Publishing a module from the PSGallery</span></span>

<span data-ttu-id="14c6c-170">K publikování modul z PSGallery a místní PSRepository, můžete použít rutinu balíček uložit-Package.</span><span class="sxs-lookup"><span data-stu-id="14c6c-170">To publish a module from the PSGallery to your local PSRepository, you can use the 'Save-Package' cmdlet.</span></span>

- <span data-ttu-id="14c6c-171">Zadejte název balíčku</span><span class="sxs-lookup"><span data-stu-id="14c6c-171">Specify the Name of the Package</span></span>
- <span data-ttu-id="14c6c-172">Jako poskytovatel zadat "NuGet.</span><span class="sxs-lookup"><span data-stu-id="14c6c-172">Specify 'NuGet' as the Provider</span></span>
- <span data-ttu-id="14c6c-173">Zadejte umístění PSGallery jako zdroj (https://www.powershellgallery.com/api/v2)</span><span class="sxs-lookup"><span data-stu-id="14c6c-173">Specify the PSGallery location as the source (https://www.powershellgallery.com/api/v2)</span></span>
- <span data-ttu-id="14c6c-174">Zadejte cestu do místního úložiště</span><span class="sxs-lookup"><span data-stu-id="14c6c-174">Specify the path to your local Repository</span></span>

<span data-ttu-id="14c6c-175">Příklad:</span><span class="sxs-lookup"><span data-stu-id="14c6c-175">Example:</span></span>

```powershell
# Publish from the PSGallery to your local Repository
Save-Package -Name 'PackageName' -Provider Nuget -Source https://www.powershellgallery.com/api/v2 -Path '\\localhost\PSRepoLocal\'
```

<span data-ttu-id="14c6c-176">Pokud vaše místní PSRepository založeného na webu, vyžaduje další krok, který používá nuget.exe k publikování.</span><span class="sxs-lookup"><span data-stu-id="14c6c-176">If your local PSRepository is web-based, it requires an additional step that uses nuget.exe to publish.</span></span>

<span data-ttu-id="14c6c-177">Viz dokumentace pro používání [nuget.exe][].</span><span class="sxs-lookup"><span data-stu-id="14c6c-177">See the documentation for using [nuget.exe][].</span></span>

## <a name="installing-powershellget-on-a-disconnected-system"></a><span data-ttu-id="14c6c-178">Instalace Správce balíčků PowerShellGet na odpojeném režimu</span><span class="sxs-lookup"><span data-stu-id="14c6c-178">Installing PowerShellGet on a disconnected system</span></span>

<span data-ttu-id="14c6c-179">Nasazení modulu PowerShellGet je obtížné v prostředích, která vyžadují systém odpojit od Internetu.</span><span class="sxs-lookup"><span data-stu-id="14c6c-179">Deploying PowerShellGet is difficult in environments that require systems to be disconnected from the internet.</span></span> <span data-ttu-id="14c6c-180">Správce balíčků PowerShellGet má spuštění procesu, který nainstaluje nejnovější verzi okamžiku, kdy se používá.</span><span class="sxs-lookup"><span data-stu-id="14c6c-180">PowerShellGet has a bootstrap process that installs the latest version the first time it's used.</span></span> <span data-ttu-id="14c6c-181">Modul OfflinePowerShellGetDeploy v galerii prostředí PowerShell obsahuje rutiny, které podporují tento proces spuštění.</span><span class="sxs-lookup"><span data-stu-id="14c6c-181">The OfflinePowerShellGetDeploy module in the PowerShell Gallery provides cmdlets that support this bootstrap process.</span></span>

<span data-ttu-id="14c6c-182">Ke spuštění v režimu offline nasazení, budete muset:</span><span class="sxs-lookup"><span data-stu-id="14c6c-182">To bootstrap an offline deployment, you need to:</span></span>

- <span data-ttu-id="14c6c-183">Stáhněte a nainstalujte systém OfflinePowerShellGetDeploy vašich připojených k Internetu a odpojených systémů</span><span class="sxs-lookup"><span data-stu-id="14c6c-183">Download and install the OfflinePowerShellGetDeploy your internet-connected system and your disconnected systems</span></span>
- <span data-ttu-id="14c6c-184">Stáhnout modul PowerShellGet a jeho závislosti na systému připojeného k Internetu pomocí `Save-PowerShellGetForOffline` rutiny</span><span class="sxs-lookup"><span data-stu-id="14c6c-184">Download PowerShellGet and its dependencies on the internet-connected system using the `Save-PowerShellGetForOffline` cmdlet</span></span>
- <span data-ttu-id="14c6c-185">Kopírovat PowerShellGet a jeho závislé součásti ze systému připojeného k Internetu do odpojeného systému</span><span class="sxs-lookup"><span data-stu-id="14c6c-185">Copy PowerShellGet and its dependencies from the internet-connected system to the disconnected system</span></span>
- <span data-ttu-id="14c6c-186">Použití `Install-PowerShellGetOffline` v odpojeném systému umístí modul PowerShellGet a jeho závislosti do správné složky</span><span class="sxs-lookup"><span data-stu-id="14c6c-186">Use the `Install-PowerShellGetOffline` on the disconnected system to place PowerShellGet and its dependencies into the proper folders</span></span>

<span data-ttu-id="14c6c-187">Následující příkazy použijte `Save-PowerShellGetForOffline` převést všechny součásti do složky `f:\OfflinePowerShellGet`</span><span class="sxs-lookup"><span data-stu-id="14c6c-187">The following commands use `Save-PowerShellGetForOffline` to put all the components into a folder `f:\OfflinePowerShellGet`</span></span>

```powershell
# Requires -RunAsAdministrator
#Download the OfflinePowerShellGetDeploy to a location that can be accessed
# by both the connected and disconnected systems.
Save-Module -Name OfflinePowerShellGetDeploy -Path 'F:\' -Repository PSGallery
Import-Module F:\OfflinePowerShellGetDeploy

# Put PowerShellGet somewhere locally
Save-PowerShellGetForOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

<span data-ttu-id="14c6c-188">V tomto okamžiku je třeba obsah `F:\OfflinePowerShellGet` odpojených systémů k dispozici.</span><span class="sxs-lookup"><span data-stu-id="14c6c-188">At this point, you must make the contents of `F:\OfflinePowerShellGet` available to your disconnected systems.</span></span> <span data-ttu-id="14c6c-189">Spustit `Install-PowerShellGetOffline` rutinu instalace Správce balíčků PowerShellGet v odpojeném systému.</span><span class="sxs-lookup"><span data-stu-id="14c6c-189">Run the `Install-PowerShellGetOffline` cmdlet to install PowerShellGet on the disconnected system.</span></span>

> [!NOTE]
> <span data-ttu-id="14c6c-190">Je důležité, nespouštějte PowerShellGet v relaci prostředí PowerShell před spuštěním těchto příkazů.</span><span class="sxs-lookup"><span data-stu-id="14c6c-190">It is important that you do not run PowerShellGet in the PowerShell session before running these commands.</span></span> <span data-ttu-id="14c6c-191">Jakmile správce balíčků PowerShellGet je načten do relace, komponenty se nedá aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="14c6c-191">Once PowerShellGet is loaded into the session, the components cannot be updated.</span></span> <span data-ttu-id="14c6c-192">Pokud spustíte Správce balíčků PowerShellGet omylem, ukončete a restartujte prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14c6c-192">If you do start PowerShellGet by mistake, exit and restart PowerShell.</span></span>

```powershell
Import-Module F:\OfflinePowerShellGetDeploy

Install-PowerShellGetOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

<span data-ttu-id="14c6c-193">Po spuštění těchto příkazů, jste připraveni publikovat PowerShellGet do místního úložiště.</span><span class="sxs-lookup"><span data-stu-id="14c6c-193">After running these commands, you are ready to publish PowerShellGet to your local repository.</span></span>

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'F:\OfflinePowershellGet' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'F:\OfflinePowerShellGet' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> <span data-ttu-id="14c6c-194">Abyste zajistili bezpečnost, klíče rozhraní API by neměl být pevně zakódovaný ve skriptech.</span><span class="sxs-lookup"><span data-stu-id="14c6c-194">To ensure security, API keys should not be hard-coded in scripts.</span></span> <span data-ttu-id="14c6c-195">Používejte systém zabezpečená správa klíčů.</span><span class="sxs-lookup"><span data-stu-id="14c6c-195">Use a secure key management system.</span></span>

<!-- external links -->
[OfflinePowerShellGetDeploy]: https://www.powershellgallery.com/packages/OfflinePowerShellGetDeploy/0.1.1
[Nuget.Server]: /nuget/hosting-packages/nuget-server
[nuget.exe]: /nuget/tools/nuget-exe-cli-reference

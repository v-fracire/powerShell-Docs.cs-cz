---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Kontrolní seznam při tvorbě prostředku
ms.openlocfilehash: 76d9fecca8618fcc178975465f45cda0d0e04064
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="resource-authoring-checklist"></a><span data-ttu-id="e5452-103">Kontrolní seznam při tvorbě prostředku</span><span class="sxs-lookup"><span data-stu-id="e5452-103">Resource authoring checklist</span></span>
<span data-ttu-id="e5452-104">Tento kontrolní seznam je seznam osvědčené postupy při vytváření nového prostředku DSC.</span><span class="sxs-lookup"><span data-stu-id="e5452-104">This checklist is a list of best practices when authoring a new DSC Resource.</span></span>
## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a><span data-ttu-id="e5452-105">Modul prostředků obsahuje soubor .psd1 a schema.mof pro každý prostředek</span><span class="sxs-lookup"><span data-stu-id="e5452-105">Resource module contains .psd1 file and schema.mof for every resource</span></span>
<span data-ttu-id="e5452-106">Zkontrolujte, zda prostředek má správnou strukturu a obsahuje všechny požadované soubory.</span><span class="sxs-lookup"><span data-stu-id="e5452-106">Check that your resource has correct structure and contains all required files.</span></span> <span data-ttu-id="e5452-107">Každý modul prostředků by měl obsahovat soubor .psd1 a každý jiný složené prostředků musí mít schema.mof souboru.</span><span class="sxs-lookup"><span data-stu-id="e5452-107">Every resource module should contain a .psd1 file and every non-composite resource should have schema.mof file.</span></span> <span data-ttu-id="e5452-108">Prostředky, které neobsahují schématu nebude uvedené podle **Get-DscResource** a uživatelé nebudou moci používat intellisense při psaní kódu pro tyto moduly (ISE) v.</span><span class="sxs-lookup"><span data-stu-id="e5452-108">Resources that do not contain schema will not be listed by **Get-DscResource** and users will not be able to use the intellisense when writing code against those modules in ISE.</span></span>
<span data-ttu-id="e5452-109">Strukturu adresáře pro prostředek xRemoteFile, která je součástí systému [xPSDesiredStateConfiguration prostředků modulu](https://github.com/PowerShell/xPSDesiredStateConfiguration), vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="e5452-109">The directory structure for xRemoteFile resource, which is part of the [xPSDesiredStateConfiguration resource module](https://github.com/PowerShell/xPSDesiredStateConfiguration), looks as follows:</span></span>


```
xPSDesiredStateConfiguration
    DSCResources
        MSFT_xRemoteFile
            MSFT_xRemoteFile.psm1
            MSFT_xRemoteFile.schema.mof
    Examples
        xRemoteFile_DownloadFile.ps1
    ResourceDesignerScripts
        GenerateXRemoteFileSchema.ps1
    Tests
        ResourceDesignerTests.ps1
    xPSDesiredStateConfiguration.psd1
```

## <a name="resource-and-schema-are-correct"></a><span data-ttu-id="e5452-110">Prostředek a schématu jsou správné ##</span><span class="sxs-lookup"><span data-stu-id="e5452-110">Resource and schema are correct##</span></span>
<span data-ttu-id="e5452-111">Ověření schématu zdroje (\*. schema.mof) souboru.</span><span class="sxs-lookup"><span data-stu-id="e5452-111">Verify the resource schema (\*.schema.mof) file.</span></span> <span data-ttu-id="e5452-112">Můžete použít [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) usnadňuje vývoj a testování schéma.</span><span class="sxs-lookup"><span data-stu-id="e5452-112">You can use the [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) to help develop and test your schema.</span></span>
<span data-ttu-id="e5452-113">Ujistěte se, že:</span><span class="sxs-lookup"><span data-stu-id="e5452-113">Make sure that:</span></span>
- <span data-ttu-id="e5452-114">Typy vlastností jsou správné (například nepoužívejte řetězec pro vlastnosti, které přijímají číselných hodnot, byste měli používat místo toho UInt32 nebo jiných číselnými typy)</span><span class="sxs-lookup"><span data-stu-id="e5452-114">Property types are correct (e.g. don’t use String for properties which accept numeric values, you should use UInt32 or other numeric types instead)</span></span>
- <span data-ttu-id="e5452-115">Vlastnost atributy jsou správně zadané jako: ([klíč], [vyžaduje], [zapisovat], [přečíst])</span><span class="sxs-lookup"><span data-stu-id="e5452-115">Property attributes are specified correctly as: ([key], [required], [write], [read])</span></span>
- <span data-ttu-id="e5452-116">Minimálně jeden parametr ve schématu musí být označeny jako [klíč]</span><span class="sxs-lookup"><span data-stu-id="e5452-116">At least one parameter in the schema has to be marked as [key]</span></span>
- <span data-ttu-id="e5452-117">[přečíst] vlastnost není existovat společně, spolu s případnými systému: [vyžaduje], [key], [zapsat.]</span><span class="sxs-lookup"><span data-stu-id="e5452-117">[read] property does not coexist together with any of: [required], [key], [write]</span></span>
- <span data-ttu-id="e5452-118">Pokud více kvalifikátory jsou zadaný – s výjimkou [čtení], pak [klíč] má přednost před</span><span class="sxs-lookup"><span data-stu-id="e5452-118">If multiple qualifiers are specified except [read], then [key] takes precedence</span></span>
- <span data-ttu-id="e5452-119">Pokud [zapsat.] a [vyžaduje] jsou zadaný, bude [vyžaduje] přednost</span><span class="sxs-lookup"><span data-stu-id="e5452-119">If [write] and [required] are specified, then [required] takes precedence</span></span>
- <span data-ttu-id="e5452-120">Je zadán chybu, kde je to vhodné</span><span class="sxs-lookup"><span data-stu-id="e5452-120">ValueMap is specified where appropriate</span></span>

<span data-ttu-id="e5452-121">Příklad:</span><span class="sxs-lookup"><span data-stu-id="e5452-121">Example:</span></span>
```
[Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
```

- <span data-ttu-id="e5452-122">Popisný název je zadán a potvrdí, k DSC zásady vytváření názvů</span><span class="sxs-lookup"><span data-stu-id="e5452-122">Friendly name is specified and confirms to DSC naming conventions</span></span>

<span data-ttu-id="e5452-123">Příklad: ```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```</span><span class="sxs-lookup"><span data-stu-id="e5452-123">Example: ```[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]```</span></span>

- <span data-ttu-id="e5452-124">Každé pole má výstižný popis.</span><span class="sxs-lookup"><span data-stu-id="e5452-124">Every field has meaningful description.</span></span> <span data-ttu-id="e5452-125">Úložiště GitHub prostředí PowerShell, jako má dobrými příklady [. schema.mof pro xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span><span class="sxs-lookup"><span data-stu-id="e5452-125">The PowerShell GitHub repository has good examples, such as [the .schema.mof for xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span></span>

<span data-ttu-id="e5452-126">Kromě toho byste měli používat **Test xDscResource** a **Test xDscSchema** rutiny z [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) automaticky ověření prostředků a schématu:</span><span class="sxs-lookup"><span data-stu-id="e5452-126">Additionally, you should use **Test-xDscResource** and **Test-xDscSchema** cmdlets from [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner/) to automatically verify the resource and schema:</span></span>
```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```
<span data-ttu-id="e5452-127">Příklad:</span><span class="sxs-lookup"><span data-stu-id="e5452-127">For example:</span></span>
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a><span data-ttu-id="e5452-128">Načte prostředek bez chyby</span><span class="sxs-lookup"><span data-stu-id="e5452-128">Resource loads without errors</span></span> ##
<span data-ttu-id="e5452-129">Zkontrolujte, zda modul prostředků mohou být úspěšně načteny.</span><span class="sxs-lookup"><span data-stu-id="e5452-129">Check whether the resource module can be successfully loaded.</span></span>
<span data-ttu-id="e5452-130">Toho lze dosáhnout ručně spuštěním `Import-Module <resource_module> -force ` a potvrzení, že nedošlo k žádným chybám, nebo pomocí zápis test automatizace.</span><span class="sxs-lookup"><span data-stu-id="e5452-130">This can be achieved manually, by running `Import-Module <resource_module> -force ` and confirming that no errors occurred, or by writing test automation.</span></span> <span data-ttu-id="e5452-131">V případě k tomu můžete následující strukturu v testovací případ:</span><span class="sxs-lookup"><span data-stu-id="e5452-131">In case of the latter, you can follow this structure in your test case:</span></span>
```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```
## <a name="resource-is-idempotent-in-the-positive-case"></a><span data-ttu-id="e5452-132">Prostředek je idempotent v případě, že kladné</span><span class="sxs-lookup"><span data-stu-id="e5452-132">Resource is idempotent in the positive case</span></span>
<span data-ttu-id="e5452-133">Mezi základní charakteristiky prostředků DSC je možné idempotenci.</span><span class="sxs-lookup"><span data-stu-id="e5452-133">One of the fundamental characteristics of DSC resources is be idempotence.</span></span> <span data-ttu-id="e5452-134">Znamená to, že použití konfigurace DSC, tento prostředek obsahující více než jednou. bude vždy dosažení stejného výsledku.</span><span class="sxs-lookup"><span data-stu-id="e5452-134">It means that applying a DSC configuration containing that resource multiple times will always achieve the same result.</span></span> <span data-ttu-id="e5452-135">Pokud například vytvoříme konfigurace, který obsahuje následující prostředek souboru:</span><span class="sxs-lookup"><span data-stu-id="e5452-135">For example, if we create a configuration which contains the following File resource:</span></span>
```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```
<span data-ttu-id="e5452-136">Po jeho použití poprvé, by se zobrazit test.txt soubor ve složce C:\test.</span><span class="sxs-lookup"><span data-stu-id="e5452-136">After applying it for the first time, file test.txt should appear in C:\test folder.</span></span> <span data-ttu-id="e5452-137">Při dalším spuštění stejnou konfiguraci nesmí však změnit stav počítače (například žádné kopie souboru test.txt by měl vytvořit).</span><span class="sxs-lookup"><span data-stu-id="e5452-137">However, subsequent runs of the same configuration should not change the state of the machine (e.g. no copies of the test.txt file should be created).</span></span>
<span data-ttu-id="e5452-138">Pro zajištění prostředek idempotent opakovaně můžete volat **Set-TargetResource** při testování prostředku přímo, nebo volejte **Start-DscConfiguration** více než jednou. při provádění testování koncové.</span><span class="sxs-lookup"><span data-stu-id="e5452-138">To ensure a resource is idempotent you can repeatedly call **Set-TargetResource** when testing the resource directly, or call **Start-DscConfiguration** multiple times when doing end to end testing.</span></span> <span data-ttu-id="e5452-139">Výsledek by měl být stejný po každé spuštění.</span><span class="sxs-lookup"><span data-stu-id="e5452-139">The result should be the same after every run.</span></span>


## <a name="test-user-modification-scenario"></a><span data-ttu-id="e5452-140">Scénáře úpravy uživatele testu</span><span class="sxs-lookup"><span data-stu-id="e5452-140">Test user modification scenario</span></span> ##
<span data-ttu-id="e5452-141">Změnou stavu počítače a pak znovu spustit DSC, můžete ověřit, která **Set-TargetResource** a **Test TargetResource** fungovat správně.</span><span class="sxs-lookup"><span data-stu-id="e5452-141">By changing the state of the machine and then rerunning DSC, you can verify that **Set-TargetResource** and **Test-TargetResource** function properly.</span></span> <span data-ttu-id="e5452-142">Zde jsou kroky, které byste měli vzít:</span><span class="sxs-lookup"><span data-stu-id="e5452-142">Here are steps you should take:</span></span>
1.  <span data-ttu-id="e5452-143">Začněte u prostředku není v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="e5452-143">Start with the resource not in the desired state.</span></span>
2.  <span data-ttu-id="e5452-144">Spuštění konfigurace pomocí vaší prostředků</span><span class="sxs-lookup"><span data-stu-id="e5452-144">Run configuration with your resource</span></span>
3.  <span data-ttu-id="e5452-145">Ověřte **Test DscConfiguration** vrátí hodnotu True.</span><span class="sxs-lookup"><span data-stu-id="e5452-145">Verify **Test-DscConfiguration** returns True</span></span>
4.  <span data-ttu-id="e5452-146">Upravit nakonfigurované položka, která má být mimo požadovaný stav</span><span class="sxs-lookup"><span data-stu-id="e5452-146">Modify the configured item to be out of the desired state</span></span>
5.  <span data-ttu-id="e5452-147">Ověřte **Test DscConfiguration** vrací hodnotu false, tady je příklad konkrétnější pomocí registru prostředků:</span><span class="sxs-lookup"><span data-stu-id="e5452-147">Verify **Test-DscConfiguration** returns false Here’s a more concrete example using Registry resource:</span></span>
1.  <span data-ttu-id="e5452-148">Spustit s klíčem registru není v požadovaném stavu</span><span class="sxs-lookup"><span data-stu-id="e5452-148">Start with registry key not in the desired state</span></span>
2.  <span data-ttu-id="e5452-149">Spustit **Start-DscConfiguration** s konfigurací a umístí jej v požadovaném stavu ověření předá.</span><span class="sxs-lookup"><span data-stu-id="e5452-149">Run **Start-DscConfiguration** with a configuration to put it in the desired state and verify it passes.</span></span>
3.  <span data-ttu-id="e5452-150">Spustit **Test DscConfiguration** a ověřte, vrátí hodnotu true</span><span class="sxs-lookup"><span data-stu-id="e5452-150">Run **Test-DscConfiguration** and verify it returns true</span></span>
4.  <span data-ttu-id="e5452-151">Změňte hodnotu klíče, aby není v požadovaném stavu</span><span class="sxs-lookup"><span data-stu-id="e5452-151">Modify the value of the key so that it is not in the desired state</span></span>
5.  <span data-ttu-id="e5452-152">Spustit **Test DscConfiguration** a ověřte, vrátí hodnotu false</span><span class="sxs-lookup"><span data-stu-id="e5452-152">Run **Test-DscConfiguration** and verify it returns false</span></span>
6.  <span data-ttu-id="e5452-153">Get-TargetResource funkce byla ověřena pomocí Get-DscConfiguration</span><span class="sxs-lookup"><span data-stu-id="e5452-153">Get-TargetResource functionality was verified using Get-DscConfiguration</span></span>

<span data-ttu-id="e5452-154">Get-TargetResource by měl vrátit podrobnosti o aktuálním stavem prostředku.</span><span class="sxs-lookup"><span data-stu-id="e5452-154">Get-TargetResource should return details of the current state of the resource.</span></span> <span data-ttu-id="e5452-155">Ujistěte se, že testovací volání Get-DscConfiguration po dokončení konfigurace a ověření, že výstupní správně odráží aktuální stav počítače.</span><span class="sxs-lookup"><span data-stu-id="e5452-155">Make sure to test it by calling Get-DscConfiguration after you apply the configuration and verifying that output correctly reflects the current state of the machine.</span></span> <span data-ttu-id="e5452-156">Je důležité k testování samostatně, protože všechny problémy v této oblasti se nezobrazí při volání metody DscConfiguration spuštění.</span><span class="sxs-lookup"><span data-stu-id="e5452-156">It's important to test it separately, since any issues in this area won't appear when calling Start-DscConfiguration.</span></span>

## <a name="call-getsettest-targetresource-functions-directly"></a><span data-ttu-id="e5452-157">Volání **Get/Set nebo Test-TargetResource** přímo funkce</span><span class="sxs-lookup"><span data-stu-id="e5452-157">Call **Get/Set/Test-TargetResource** functions directly</span></span> ##

<span data-ttu-id="e5452-158">Zajistěte, aby testování **Get/Set nebo Test-TargetResource** funkce implementované v prostředku přímé volání a ověření, že fungují podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="e5452-158">Make sure you test the **Get/Set/Test-TargetResource** functions implemented in your resource by calling them directly and verifying that they work as expected.</span></span>

## <a name="verify-end-to-end-using-start-dscconfiguration"></a><span data-ttu-id="e5452-159">Ověřit pomocí koncová **Start DscConfiguration**</span><span class="sxs-lookup"><span data-stu-id="e5452-159">Verify End to End using **Start-DscConfiguration**</span></span> ##

<span data-ttu-id="e5452-160">Testování **Get/Set nebo Test-TargetResource** funkcí podle přímé volání je důležité, ale ne všechny problémy budou zjištěny tímto způsobem.</span><span class="sxs-lookup"><span data-stu-id="e5452-160">Testing **Get/Set/Test-TargetResource** functions by calling them directly is important, but not all issues will be discovered this way.</span></span> <span data-ttu-id="e5452-161">Měli byste se zaměřit významnou část testování na pomocí **Start-DscConfiguration** nebo serveru pro vyžádání obsahu.</span><span class="sxs-lookup"><span data-stu-id="e5452-161">You should focus significant part of your testing on using **Start-DscConfiguration** or the pull server.</span></span> <span data-ttu-id="e5452-162">Ve skutečnosti to je, jak budou uživatelé používat k prostředku, a to tak není příliš nízko, násobek tohoto typu testů.</span><span class="sxs-lookup"><span data-stu-id="e5452-162">In fact, this is how users will use the resource, so don’t underestimate the significance of this type of tests.</span></span>
<span data-ttu-id="e5452-163">Možné typy problémů:</span><span class="sxs-lookup"><span data-stu-id="e5452-163">Possible types of issues:</span></span>
- <span data-ttu-id="e5452-164">Přihlašovací údaje nebo relace může chovat jinak, protože DSC agent běží jako služba.</span><span class="sxs-lookup"><span data-stu-id="e5452-164">Credential/Session may behave differently because the DSC agent runs as a service.</span></span>  <span data-ttu-id="e5452-165">Nezapomeňte otestovat všechny funkce, zde začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="e5452-165">Be sure to test any features here end to end.</span></span>
- <span data-ttu-id="e5452-166">Chyby výstupem **Start-DscConfiguration** může být jiný než ty, které zobrazí při volání metody **Set-TargetResource** funkce přímo.</span><span class="sxs-lookup"><span data-stu-id="e5452-166">Errors output by **Start-DscConfiguration** may be different than those displayed when calling the **Set-TargetResource** function directly.</span></span>

## <a name="test-compatability-on-all-dsc-supported-platforms"></a><span data-ttu-id="e5452-167">Test kompatibility na DSC všechny podporované platformy</span><span class="sxs-lookup"><span data-stu-id="e5452-167">Test compatability on all DSC supported platforms</span></span> ##
<span data-ttu-id="e5452-168">Prostředek by měly fungovat na všech platformách DSC podporované (Windows Server 2008 R2 a novější).</span><span class="sxs-lookup"><span data-stu-id="e5452-168">Resource should work on all DSC supported platforms (Windows Server 2008 R2 and newer).</span></span> <span data-ttu-id="e5452-169">Nainstalujte poslední verzi WMF (Windows Management Framework) v operačním systému získat nejnovější verzi DSC.</span><span class="sxs-lookup"><span data-stu-id="e5452-169">Install the latest WMF (Windows Management Framework) on your OS to get the latest version of DSC.</span></span> <span data-ttu-id="e5452-170">Pokud prostředek nefunguje na některé z těchto platforem záměrné, má být vrácen konkrétní chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="e5452-170">If your resource does not work on some of these platforms by design, a specific error message should be returned.</span></span> <span data-ttu-id="e5452-171">Taky se ujistěte, že prostředek ověří, zda jsou rutiny, ke kterému se připojujete na konkrétním počítači.</span><span class="sxs-lookup"><span data-stu-id="e5452-171">Also, make sure your resource checks whether cmdlets you are calling are present on particular machine.</span></span> <span data-ttu-id="e5452-172">Windows Server 2012 přidat velký počet nových rutin, které nejsou k dispozici v systému Windows Server 2008 R2, i s WMF nainstalována.</span><span class="sxs-lookup"><span data-stu-id="e5452-172">Windows Server 2012 added a large number of new cmdlets that are not available on Windows Server 2008R2, even with WMF installed.</span></span>

## <a name="verify-on-windows-client-if-applicable"></a><span data-ttu-id="e5452-173">Ověřte v klientovi Windows (pokud existuje)</span><span class="sxs-lookup"><span data-stu-id="e5452-173">Verify on Windows Client (if applicable)</span></span> ##
<span data-ttu-id="e5452-174">Jeden velmi běžné mezera testovací ověřuje prostředků pouze v serverových verzí systému Windows.</span><span class="sxs-lookup"><span data-stu-id="e5452-174">One very common test gap is verifying the resource only on server versions of Windows.</span></span> <span data-ttu-id="e5452-175">Mnoho prostředků jsou navrženy pro práci na SKU klienta, takže pokud je to pravda v váš případ, nezapomeňte otestovat ji na těchto platformách také.</span><span class="sxs-lookup"><span data-stu-id="e5452-175">Many resources are also designed to work on Client SKUs, so if that’s true in your case, don’t forget to test it on those platforms as well.</span></span>
## <a name="get-dscresource-lists-the-resource"></a><span data-ttu-id="e5452-176">Get-DSCResource uvádí prostředku</span><span class="sxs-lookup"><span data-stu-id="e5452-176">Get-DSCResource lists the resource</span></span> ##
<span data-ttu-id="e5452-177">Po nasazení modul, volání Get-DscResource by měl seznam prostředku ostatních v důsledku.</span><span class="sxs-lookup"><span data-stu-id="e5452-177">After deploying the module, calling Get-DscResource should list your resource among others as a result.</span></span> <span data-ttu-id="e5452-178">Pokud prostředek nelze najít v seznamu, ověřte, zda tento soubor schema.mof pro tento prostředek existuje.</span><span class="sxs-lookup"><span data-stu-id="e5452-178">If you can’t find your resource in the list, make sure that schema.mof file for that resource exists.</span></span>
## <a name="resource-module-contains-examples"></a><span data-ttu-id="e5452-179">Modul prostředků obsahuje příklady</span><span class="sxs-lookup"><span data-stu-id="e5452-179">Resource module contains examples</span></span> ##
<span data-ttu-id="e5452-180">Vytváření kvality příklady, které pomůže ostatním pochopit, jak ho použít.</span><span class="sxs-lookup"><span data-stu-id="e5452-180">Creating quality examples which will help others understand how to use it.</span></span> <span data-ttu-id="e5452-181">To je velmi důležitý, zejména od mnoha uživateli považovat za dokumentaci ukázkový kód.</span><span class="sxs-lookup"><span data-stu-id="e5452-181">This is crucial, especially since many users treat sample code as documentation.</span></span>
- <span data-ttu-id="e5452-182">Nejdřív musíte si ujasnit některé příklady, které budou zahrnuty s modulem – alespoň, by mělo zahrnovat nejdůležitější případy použití pro prostředek:</span><span class="sxs-lookup"><span data-stu-id="e5452-182">First, you should determine the examples that will be included with the module – at minimum, you should cover most important use cases for your resource:</span></span>
- <span data-ttu-id="e5452-183">Pokud modul obsahuje několik prostředků, které je potřeba spolupracují scénář začátku do konce, základní příklad začátku do konce v ideálním případě by první.</span><span class="sxs-lookup"><span data-stu-id="e5452-183">If your module contains several resources that need to work together for an end-to-end scenario, the basic end-to-end example would ideally be first.</span></span>
- <span data-ttu-id="e5452-184">Počáteční příklady by měl být velmi jednoduché – jak začít pracovat s vaše prostředky v malých spravovatelných blocích (např. k vytvoření nového virtuálního pevného disku)</span><span class="sxs-lookup"><span data-stu-id="e5452-184">The initial examples should be very simple -- how to get started with your resources in small manageable chunks (e.g. creating a new VHD)</span></span>
- <span data-ttu-id="e5452-185">Následující příklady by měl vytvářet na tyto příklady (např. vytvoření virtuálního počítače z disku VHD, odebrání virtuálního počítače, změny virtuálního počítače) a zobrazit pokročilé funkce (např. vytvoření virtuálního počítače s dynamickou pamětí)</span><span class="sxs-lookup"><span data-stu-id="e5452-185">Subsequent examples should build on those examples (e.g. creating a VM from a VHD, removing VM, modifying VM), and show advanced functionality (e.g. creating a VM with dynamic memory)</span></span>
- <span data-ttu-id="e5452-186">Příklad konfigurace by měly být parametrizovány (všech hodnot, které mají být předány do konfigurace jako parametry a měla by existovat žádné hodnoty pevně zakódované):</span><span class="sxs-lookup"><span data-stu-id="e5452-186">Example configurations should be parameterized (all values should be passed to the configuration as parameters and there should be no hardcoded values):</span></span>
```powershell
configuration Sample_xRemoteFile_DownloadFile
{
    param
    (
        [string[]] $nodeName = 'localhost',

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $destinationPath,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String] $uri,

        [String] $userAgent,

        [Hashtable] $headers
    )

    Import-DscResource -Name MSFT_xRemoteFile -ModuleName xPSDesiredStateConfiguration

    Node $nodeName
    {
        xRemoteFile DownloadFile
        {
            DestinationPath = $destinationPath
            Uri = $uri
            UserAgent = $userAgent
            Headers = $headers
        }
    }
}
```
- <span data-ttu-id="e5452-187">Je dobrým zvykem zahrnují (komentovaný out) příklad toho, jak volat konfigurace se skutečnými hodnotami na konci ukázkový skript.</span><span class="sxs-lookup"><span data-stu-id="e5452-187">It’s a good practice to include (commented out) example of how to call the configuration with the actual values at the end of the example script.</span></span>
<span data-ttu-id="e5452-188">Například v konfiguraci výše není nutně zřejmé, že je nejlepší způsob, jak určit UserAgent:</span><span class="sxs-lookup"><span data-stu-id="e5452-188">For example, in the configuration above it isn't neccessarily obvious that the best way to specify UserAgent is:</span></span>

<span data-ttu-id="e5452-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` V takovém případě komentář mohou objasnit zamýšlený provedení konfigurace:</span><span class="sxs-lookup"><span data-stu-id="e5452-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` In which case a comment can clarify the intended execution of the configuration:</span></span>
```
<#
Sample use (parameter values need to be changed according to your scenario):

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
-userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
#>
```
- <span data-ttu-id="e5452-190">Každý například zápisu krátký popis, která vysvětluje, co znamená a význam vlastností parametrů.</span><span class="sxs-lookup"><span data-stu-id="e5452-190">For each example, write a short description which explains what it does, and the meaning of the parameters.</span></span>
- <span data-ttu-id="e5452-191">Zajistěte, aby příklady zahrnují většině scénářů, které jsou důležité pro prostředek a pokud není nic chybí, ověřte, zda se všechny provést a uveďte počítač s požadovaným stavem.</span><span class="sxs-lookup"><span data-stu-id="e5452-191">Make sure examples cover most the important scenarios for your resource and if there’s nothing missing, verify that they all execute and put machine in the desired state.</span></span>

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a><span data-ttu-id="e5452-192">Chybové zprávy se dají snadno pochopit a pomáhají uživatelům řešit problémy</span><span class="sxs-lookup"><span data-stu-id="e5452-192">Error messages are easy to understand and help users solve problems</span></span> ##
<span data-ttu-id="e5452-193">By měla být funkční chybové zprávy:</span><span class="sxs-lookup"><span data-stu-id="e5452-193">Good error messages should be:</span></span>
- <span data-ttu-id="e5452-194">: Největších problém s chybové zprávy není, často neexistují, proto se ujistěte, že jsou dispozici.</span><span class="sxs-lookup"><span data-stu-id="e5452-194">There: The biggest problem with error messages is that they often don’t exist, so make sure they are there.</span></span>
- <span data-ttu-id="e5452-195">Snadno pochopitelné: lidské čitelný, ne skrytého chybové kódy</span><span class="sxs-lookup"><span data-stu-id="e5452-195">Easy to understand: Human readable, no obscure error codes</span></span>
- <span data-ttu-id="e5452-196">Přesné: Popisují, co je přesně tento problém</span><span class="sxs-lookup"><span data-stu-id="e5452-196">Precise: Describe what’s exactly the problem</span></span>
- <span data-ttu-id="e5452-197">Konstruktivní: Rady informace o vyřešení problému</span><span class="sxs-lookup"><span data-stu-id="e5452-197">Constructive: Advice how to fix the issue</span></span>
- <span data-ttu-id="e5452-198">Celkem: Nemáte viny uživatele nebo zajistěte, je zaregistrované chybný Ujistěte se, ověřte chyby ve scénářích koncová (pomocí **Start-DscConfiguration**), protože se mohou lišit od těch vrácená při spuštění funkce prostředků přímo.</span><span class="sxs-lookup"><span data-stu-id="e5452-198">Polite: Don’t blame user or make them feel bad Make sure you verify errors in End to End scenarios (using **Start-DscConfiguration**), because they may differ from those returned when running resource functions directly.</span></span>

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a><span data-ttu-id="e5452-199">Zprávy protokolu jsou snadno pochopit a informativní (včetně – podrobné nastavení, – protokoly trasování a ladění)</span><span class="sxs-lookup"><span data-stu-id="e5452-199">Log messages are easy to understand and informative (including –verbose, –debug and ETW logs)</span></span> ##
<span data-ttu-id="e5452-200">Zkontrolujte, zda jsou protokoly výstupem prostředkem snadno pochopit a zadejte hodnotu pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="e5452-200">Ensure that logs outputted by the resource are easy to understand and provide value to the user.</span></span> <span data-ttu-id="e5452-201">Prostředky by výstup všechny informace, které mohou být užitečné pro uživatele, ale další protokoly není vždy lepší.</span><span class="sxs-lookup"><span data-stu-id="e5452-201">Resources should output all information which might be helpful to the user, but more logs is not always better.</span></span> <span data-ttu-id="e5452-202">Měli byste vyhnout redundance a odesíláním dat, která ho nemá zadejte další hodnotu – nevytvářejte někdo projít stovky položky protokolu, aby bylo možné najít, co hledají.</span><span class="sxs-lookup"><span data-stu-id="e5452-202">You should avoid redundancy and outputting data which does not provide additional value – don’t make someone go through hundreds of log entries in order to find what they're looking for.</span></span> <span data-ttu-id="e5452-203">Samozřejmě žádné protokoly není přijatelného řešení tohoto problému buď.</span><span class="sxs-lookup"><span data-stu-id="e5452-203">Of course, no logs is not an acceptable solution for this problem either.</span></span>

<span data-ttu-id="e5452-204">Při testování, by také analyzovat podrobné a ladění protokoly (spuštěním **Start-DscConfiguration** s – podrobné a – ladění přepínače správně), stejně jako protokoly trasování událostí pro Windows.</span><span class="sxs-lookup"><span data-stu-id="e5452-204">When testing, you should also analyze verbose and debug logs (by running **Start-DscConfiguration** with –verbose and –debug switches appropriately), as well as ETW logs.</span></span> <span data-ttu-id="e5452-205">Chcete-li zobrazit protokoly trasování událostí pro Windows DSC, přejděte do prohlížeče událostí a otevřete následující složku: aplikací a konfigurace požadovaného stavu služby společnosti Microsoft - Windows -.</span><span class="sxs-lookup"><span data-stu-id="e5452-205">To see DSC ETW logs, go to Event Viewer and open the following folder: Applications and Services- Microsoft - Windows - Desired State Configuration.</span></span>  <span data-ttu-id="e5452-206">Ve výchozím nastavení existuje budou provozní kanál, ale zajistěte, aby povolíte analýzu a ladit kanály před spuštěním konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e5452-206">By default there will be Operational channel, but make sure you enable Analytic and Debug channels before running the configuration.</span></span>
<span data-ttu-id="e5452-207">Pokud chcete povolit kanály analýzy nebo ladění, můžete provést níže uvedený skript:</span><span class="sxs-lookup"><span data-stu-id="e5452-207">To enable Analytic/Debug channels, you can execute script below:</span></span>
```powershell
$statusEnabled = $true
# Use "Analytic" to enable Analytic channel
$eventLogFullName = "Microsoft-Windows-Dsc/Debug"
$commandToExecute = "wevtutil set-log $eventLogFullName /e:$statusEnabled /q:$statusEnabled   "
$log = New-Object System.Diagnostics.Eventing.Reader.EventLogConfiguration $eventLogFullName
if($statusEnabled -eq $log.IsEnabled)
{
    Write-Host -Verbose "The channel event log is already enabled"
    return
}
Invoke-Expression $commandToExecute
```
## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a><span data-ttu-id="e5452-208">Implementace prostředků neobsahuje pevně zakódované cesty</span><span class="sxs-lookup"><span data-stu-id="e5452-208">Resource implementation does not contain hardcoded paths</span></span> ##
<span data-ttu-id="e5452-209">Ujistěte se, neexistují žádné cesty pevně kódovaný v provádění prostředku, zvlášť pokud převzaly jazyka (en-us), nebo když se systémové proměnné, které lze použít.</span><span class="sxs-lookup"><span data-stu-id="e5452-209">Ensure there are no hardcoded paths in the resource implementation, particularly if they assume language (en-us), or when there are system variables that can be used.</span></span>
<span data-ttu-id="e5452-210">Pokud prostředek potřebovat přístup k určité cesty, pomocí proměnné prostředí místo hardcoding cesty, protože se mohou lišit na jiné počítače.</span><span class="sxs-lookup"><span data-stu-id="e5452-210">If your resource need to access specific paths, use environment variables instead of hardcoding the path, as it may differ on other machines.</span></span>

<span data-ttu-id="e5452-211">Příklad:</span><span class="sxs-lookup"><span data-stu-id="e5452-211">Example:</span></span>

<span data-ttu-id="e5452-212">Namísto:</span><span class="sxs-lookup"><span data-stu-id="e5452-212">Instead of:</span></span>
```
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
 ```
<span data-ttu-id="e5452-213">Můžete napsat:</span><span class="sxs-lookup"><span data-stu-id="e5452-213">You can write:</span></span>
```
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```
## <a name="resource-implementation-does-not-contain-user-information"></a><span data-ttu-id="e5452-214">Implementace prostředků neobsahuje informace o uživateli</span><span class="sxs-lookup"><span data-stu-id="e5452-214">Resource implementation does not contain user information</span></span> ##
<span data-ttu-id="e5452-215">Ujistěte se, že neexistují žádné e-mailu, informace o účtu nebo jména osob v kódu.</span><span class="sxs-lookup"><span data-stu-id="e5452-215">Make sure there are no email names, account information, or names of people in the code.</span></span>
## <a name="resource-was-tested-with-validinvalid-credentials"></a><span data-ttu-id="e5452-216">Prostředek byla testována s platnou nebo neplatná pověření</span><span class="sxs-lookup"><span data-stu-id="e5452-216">Resource was tested with valid/invalid credentials</span></span> ##
<span data-ttu-id="e5452-217">Pokud prostředek přijímá pověření jako parametr:</span><span class="sxs-lookup"><span data-stu-id="e5452-217">If your resource takes a credential as parameter:</span></span>
- <span data-ttu-id="e5452-218">Ověření funguje prostředků místní systém (nebo účet počítače pro vzdálené prostředky) nemá přístup.</span><span class="sxs-lookup"><span data-stu-id="e5452-218">Verify the resource works when Local System (or the computer account for remote resources) does not have access.</span></span>
- <span data-ttu-id="e5452-219">Ověřte prostředků funguje s pověření zadaná pro získáte nastavené a testování</span><span class="sxs-lookup"><span data-stu-id="e5452-219">Verify the resource works with a credential specified for Get, Set and Test</span></span>
- <span data-ttu-id="e5452-220">Pokud získá přístup k prostředku sdílené složky, otestujte všechny varianty, které potřebujete podporovat, jako například:</span><span class="sxs-lookup"><span data-stu-id="e5452-220">If your resource accesses shares, test all the variants you need to support, such as:</span></span>
  - <span data-ttu-id="e5452-221">Standardní windows sdílené složky.</span><span class="sxs-lookup"><span data-stu-id="e5452-221">Standard windows shares.</span></span>
  - <span data-ttu-id="e5452-222">Sdílené složky systému souborů DFS.</span><span class="sxs-lookup"><span data-stu-id="e5452-222">DFS shares.</span></span>
  - <span data-ttu-id="e5452-223">SAMBA sdílených složek (Pokud chcete podporovat Linux.)</span><span class="sxs-lookup"><span data-stu-id="e5452-223">SAMBA shares (if you want to support Linux.)</span></span>

## <a name="resource-does-not-require-interactive-input"></a><span data-ttu-id="e5452-224">Prostředek nepotřebuje interaktivní vstup</span><span class="sxs-lookup"><span data-stu-id="e5452-224">Resource does not require interactive input</span></span> ##
<span data-ttu-id="e5452-225">**Get/Set nebo Test-TargetResource** funkce budou automaticky spuštěny a nesmí počkejte uživatelský vstup v jakékoli fázi provádění (například byste neměli používat **Get-Credential** uvnitř tyto funkce).</span><span class="sxs-lookup"><span data-stu-id="e5452-225">**Get/Set/Test-TargetResource** functions should be executed automatically and must not wait for user’s input at any stage of execution (e.g. you should not use **Get-Credential** inside these functions).</span></span> <span data-ttu-id="e5452-226">Když musíte zadat uživatelský vstup, musí se předat do konfigurace jako parametr během fáze kompilace.</span><span class="sxs-lookup"><span data-stu-id="e5452-226">If you need to provide user’s input, you should pass it to the configuration as parameter during the compilation phase.</span></span>
## <a name="resource-functionality-was-thoroughly-tested"></a><span data-ttu-id="e5452-227">Funkce prostředků byla testována</span><span class="sxs-lookup"><span data-stu-id="e5452-227">Resource functionality was thoroughly tested</span></span> ##
<span data-ttu-id="e5452-228">Tento kontrolní seznam obsahuje položky, které jsou důležité má být testována nebo jsou často vynechán.</span><span class="sxs-lookup"><span data-stu-id="e5452-228">This checklist contains items which are important to be tested and/or are often missed.</span></span> <span data-ttu-id="e5452-229">Bude bunch testů, především funkční ty, které mají být specifické pro prostředek, testování a nejsou zde uvedeným.</span><span class="sxs-lookup"><span data-stu-id="e5452-229">There will be bunch of tests, mainly functional ones which will be specific to the resource you are testing and are not mentioned here.</span></span> <span data-ttu-id="e5452-230">Nezapomeňte záporné testovací případy.</span><span class="sxs-lookup"><span data-stu-id="e5452-230">Don’t forget about negative test cases.</span></span>
## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a><span data-ttu-id="e5452-231">Nejvhodnější: modul prostředků obsahuje složku testy s ResourceDesignerTests.ps1 skriptu</span><span class="sxs-lookup"><span data-stu-id="e5452-231">Best practice: Resource module contains Tests folder with ResourceDesignerTests.ps1 script</span></span> ##
<span data-ttu-id="e5452-232">Je vhodné vytvořit složku "testy" v modulu prostředků, vytvořte soubor ResourceDesignerTests.ps1 a přidejte testů pomocí **Test xDscResource** a **Test xDscSchema** pro všechny prostředky v zadané modul.</span><span class="sxs-lookup"><span data-stu-id="e5452-232">It’s a good practice to create folder “Tests” inside resource module, create ResourceDesignerTests.ps1 file and add tests using **Test-xDscResource** and **Test-xDscSchema** for all resources in given module.</span></span>
<span data-ttu-id="e5452-233">Tímto způsobem můžete rychle ověřit schémata všechny prostředky z daného moduly a nechcete, správností zkontrolujte před publikováním.</span><span class="sxs-lookup"><span data-stu-id="e5452-233">This way you can quickly validate schemas of all resources from the given modules and do a sanity check before publishing.</span></span>
<span data-ttu-id="e5452-234">Pro xRemoteFile může vypadat ResourceTests.ps1 stejně jednoduché jako:</span><span class="sxs-lookup"><span data-stu-id="e5452-234">For xRemoteFile, ResourceTests.ps1 could look as simple as:</span></span>
```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```
##<a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a><span data-ttu-id="e5452-235">Nejvhodnější: Složka prostředků obsahuje prostředků Návrháře skript pro generování schémat ##</span><span class="sxs-lookup"><span data-stu-id="e5452-235">Best practice: Resource folder contains resource designer script for generating schema##</span></span>
<span data-ttu-id="e5452-236">Všechny prostředky by měly obsahovat prostředků Návrháře skript, který generuje schéma mof prostředku.</span><span class="sxs-lookup"><span data-stu-id="e5452-236">Each resource should contain a resource designer script which generates a mof schema of the resource.</span></span> <span data-ttu-id="e5452-237">Tento soubor musí být umístěny v <ResourceName>\ResourceDesignerScripts a bude mít název generování<ResourceName>Schema.ps1 pro prostředek xRemoteFile tento soubor by být volána GenerateXRemoteFileSchema.ps1 a obsahovat:</span><span class="sxs-lookup"><span data-stu-id="e5452-237">This file should be placed in <ResourceName>\ResourceDesignerScripts and be named Generate<ResourceName>Schema.ps1 For xRemoteFile resource this file would be called GenerateXRemoteFileSchema.ps1 and contain:</span></span>
```powershell
$DestinationPath = New-xDscResourceProperty -Name DestinationPath -Type String -Attribute Key -Description 'Path under which downloaded or copied file should be accessible after operation.'
$Uri = New-xDscResourceProperty -Name Uri -Type String -Attribute Required -Description 'Uri of a file which should be copied or downloaded. This parameter supports HTTP and HTTPS values.'
$Headers = New-xDscResourceProperty -Name Headers -Type Hashtable[] -Attribute Write -Description 'Headers of the web request.'
$UserAgent = New-xDscResourceProperty -Name UserAgent -Type String -Attribute Write -Description 'User agent for the web request.'
$Ensure = New-xDscResourceProperty -Name Ensure -Type String -Attribute Read -ValidateSet "Present", "Absent" -Description 'Says whether DestinationPath exists on the machine'
$Credential = New-xDscResourceProperty -Name Credential -Type PSCredential -Attribute Write -Description 'Specifies a user account that has permission to send the request.'
$CertificateThumbprint = New-xDscResourceProperty -Name CertificateThumbprint -Type String -Attribute Write -Description 'Digital public key certificate that is used to send the request.'

New-xDscResource -Name MSFT_xRemoteFile -Property @($DestinationPath, $Uri, $Headers, $UserAgent, $Ensure, $Credential, $CertificateThumbprint) -ModuleName xPSDesiredStateConfiguration2 -FriendlyName xRemoteFile
```
## <a name="best-practice-resource-supports--whatif"></a><span data-ttu-id="e5452-238">Nejvhodnější: prostředek podporuje - whatif</span><span class="sxs-lookup"><span data-stu-id="e5452-238">Best practice: Resource supports -whatif</span></span> ##
<span data-ttu-id="e5452-239">Pokud prostředek provádí "nebezpečné" operace, je vhodné implementovat - whatif funkce.</span><span class="sxs-lookup"><span data-stu-id="e5452-239">If your resource is performing “dangerous” operations, it’s a good practice to implement -whatif functionality.</span></span> <span data-ttu-id="e5452-240">Po dokončení, zajistěte, aby whatif výstup správně popisuje operací, které by mohlo dojít, pokud byl proveden příkaz bez whatif přepínače.</span><span class="sxs-lookup"><span data-stu-id="e5452-240">After it’s done, make sure that whatif output correctly describes operations which would happen if command was executed without whatif switch.</span></span>
<span data-ttu-id="e5452-241">Také ověřte, že operace nepracuje (nebudou provedeny žádné změny stavu uzlu) Pokud je zadán přepínač – whatif.</span><span class="sxs-lookup"><span data-stu-id="e5452-241">Also, verify that operations does not execute (no changes to the node’s state are made) when –whatif switch is present.</span></span>
<span data-ttu-id="e5452-242">Předpokládejme například, že se testují souboru prostředků.</span><span class="sxs-lookup"><span data-stu-id="e5452-242">For example, let’s assume we are testing File resource.</span></span> <span data-ttu-id="e5452-243">Níže je jednoduchá konfigurace, který vytvoří soubor "test.txt" obsah "test":</span><span class="sxs-lookup"><span data-stu-id="e5452-243">Below is simple configuration which creates file “test.txt” with contents “test”:</span></span>
```powershell
configuration config
{
    node localhost
    {
        File file
        {
            Contents="test"
            DestinationPath="C:\test\test.txt"
        }
    }
}
config
```
<span data-ttu-id="e5452-244">Pokud jsme zkompilovat a potom spusťte konfigurace s přepínačem – whatif, výstup nám oznamuje přesně co by se stalo při jsme spuštění konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e5452-244">If we compile and then execute the configuration with the –whatif switch, the output is telling us exactly what would happen when we run the configuration.</span></span> <span data-ttu-id="e5452-245">Konfigurace samotného ale neprovedl (test.txt soubor nebyl vytvořen).</span><span class="sxs-lookup"><span data-stu-id="e5452-245">The configuration itself however was not executed (test.txt file was not created).</span></span>
```powershell
Start-DscConfiguration -path .\config -ComputerName localhost -wait -verbose -whatif
VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
SendConfigurationApply,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer CHARLESX1 with user sid
S-1-5-21-397955417-626881126-188441444-5179871.
What if: [X]: LCM:  [ Start  Set      ]
What if: [X]: LCM:  [ Start  Resource ]  [[File]file]
What if: [X]: LCM:  [ Start  Test     ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]: LCM:  [ End    Test     ]  [[File]file]  in 0.0270 seconds.
What if: [X]: LCM:  [ Start  Set      ]  [[File]file]
What if: [X]:                            [[File]file] The system cannot find the file specified.
What if: [X]:                            [[File]file] The related file/directory is: C:\test\test.txt.
What if: [X]:                            [C:\test\test.txt] Creating and writing contents and setting attributes.
What if: [X]: LCM:  [ End    Set      ]  [[File]file]  in 0.0180 seconds.
What if: [X]: LCM:  [ End    Resource ]  [[File]file]
What if: [X]: LCM:  [ End    Set      ]
VERBOSE: [X]: LCM:  [ End    Set      ]    in  0.1050 seconds.
VERBOSE: Operation 'Invoke CimMethod' complete.
```

<span data-ttu-id="e5452-246">Tento seznam není vyčerpávající, týká se však mnoho důležité problémy, které můžete došlo při navrhování, vývoj a testování prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="e5452-246">This list is not exhaustive, but it covers many important issues which can be encountered while designing, developing and testing DSC resources.</span></span>
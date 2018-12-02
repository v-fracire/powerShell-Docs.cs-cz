---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Kontrolní seznam při tvorbě prostředku
ms.openlocfilehash: 2b6e972776dba4ecc6fd1ab5c21361d653e1a469
ms.sourcegitcommit: e24525046dd37166b9d83eeecdc534726316f429
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/01/2018
ms.locfileid: "52742835"
---
# <a name="resource-authoring-checklist"></a><span data-ttu-id="b7749-103">Kontrolní seznam při tvorbě prostředku</span><span class="sxs-lookup"><span data-stu-id="b7749-103">Resource authoring checklist</span></span>

<span data-ttu-id="b7749-104">Tento kontrolní seznam je seznam osvědčených postupů při vytváření nového prostředku DSC.</span><span class="sxs-lookup"><span data-stu-id="b7749-104">This checklist is a list of best practices when authoring a new DSC Resource.</span></span>

## <a name="resource-module-contains-psd1-file-and-schemamof-for-every-resource"></a><span data-ttu-id="b7749-105">Modul prostředků obsahuje souboru .psd1 a schema.mof pro každý prostředek</span><span class="sxs-lookup"><span data-stu-id="b7749-105">Resource module contains .psd1 file and schema.mof for every resource</span></span>

<span data-ttu-id="b7749-106">Zkontrolujte, zda váš prostředek má správnou strukturu a obsahuje všechny požadované soubory.</span><span class="sxs-lookup"><span data-stu-id="b7749-106">Check that your resource has correct structure and contains all required files.</span></span> <span data-ttu-id="b7749-107">Každý modul prostředků by měl obsahovat souboru .psd1 a každý bez složený prostředek by měl mít schema.mof souboru.</span><span class="sxs-lookup"><span data-stu-id="b7749-107">Every resource module should contain a .psd1 file and every non-composite resource should have schema.mof file.</span></span> <span data-ttu-id="b7749-108">Prostředky, které neobsahují schématu nebude uvedené podle `Get-DscResource` a uživatelé nebudou moct používat technologii intellisense při psaní kódu pro tyto moduly v prostředí ISE.</span><span class="sxs-lookup"><span data-stu-id="b7749-108">Resources that do not contain schema will not be listed by `Get-DscResource` and users will not be able to use the intellisense when writing code against those modules in ISE.</span></span>
<span data-ttu-id="b7749-109">Adresářové struktury xRemoteFile prostředků, která je součástí sady [xPSDesiredStateConfiguration prostředků modulu](https://github.com/PowerShell/xPSDesiredStateConfiguration), vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="b7749-109">The directory structure for xRemoteFile resource, which is part of the [xPSDesiredStateConfiguration resource module](https://github.com/PowerShell/xPSDesiredStateConfiguration), looks as follows:</span></span>

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

## <a name="resource-and-schema-are-correct"></a><span data-ttu-id="b7749-110">Správnost prostředků a schématu</span><span class="sxs-lookup"><span data-stu-id="b7749-110">Resource and schema are correct</span></span>

<span data-ttu-id="b7749-111">Ověření schématu prostředků (\*. schema.mof) soubor.</span><span class="sxs-lookup"><span data-stu-id="b7749-111">Verify the resource schema (\*.schema.mof) file.</span></span> <span data-ttu-id="b7749-112">Můžete použít [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner) usnadňují vývoj a testování vašeho schématu.</span><span class="sxs-lookup"><span data-stu-id="b7749-112">You can use the [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner) to help develop and test your schema.</span></span>
<span data-ttu-id="b7749-113">Ujistěte se, že:</span><span class="sxs-lookup"><span data-stu-id="b7749-113">Make sure that:</span></span>

- <span data-ttu-id="b7749-114">Typy vlastností jsou správné (například nepoužívejte řetězec pro vlastnosti, které přijímají číselných hodnot, byste měli použít místo toho UInt32 nebo další číselné typy)</span><span class="sxs-lookup"><span data-stu-id="b7749-114">Property types are correct (e.g. don’t use String for properties which accept numeric values, you should use UInt32 or other numeric types instead)</span></span>
- <span data-ttu-id="b7749-115">Atributy vlastnosti jsou správně zadané jako: ([klíč], [povinné], [psaní], [pro čtení])</span><span class="sxs-lookup"><span data-stu-id="b7749-115">Property attributes are specified correctly as: ([key], [required], [write], [read])</span></span>
- <span data-ttu-id="b7749-116">Nejméně jeden parametr ve schématu musí být označený jako [klíč]</span><span class="sxs-lookup"><span data-stu-id="b7749-116">At least one parameter in the schema has to be marked as [key]</span></span>
- <span data-ttu-id="b7749-117">[pro čtení] vlastnost není existovat vedle sebe spolu s případnými z: [povinné], [key], [psaní]</span><span class="sxs-lookup"><span data-stu-id="b7749-117">[read] property does not coexist together with any of: [required], [key], [write]</span></span>
- <span data-ttu-id="b7749-118">Pokud více kvalifikátory jsou zadaný – s výjimkou [čtení], pak [klíč] má přednost před</span><span class="sxs-lookup"><span data-stu-id="b7749-118">If multiple qualifiers are specified except [read], then [key] takes precedence</span></span>
- <span data-ttu-id="b7749-119">Pokud [psaní] a [povinné] je zadán, pak [povinné] přednost</span><span class="sxs-lookup"><span data-stu-id="b7749-119">If [write] and [required] are specified, then [required] takes precedence</span></span>
- <span data-ttu-id="b7749-120">Je zadán chybu případně příkladu:</span><span class="sxs-lookup"><span data-stu-id="b7749-120">ValueMap is specified where appropriate Example:</span></span>

  ```
  [Read, ValueMap{"Present", "Absent"}, Values{"Present", "Absent"}, Description("Says whether DestinationPath exists on the machine")] String Ensure;
  ```

- <span data-ttu-id="b7749-121">Popisný název je zadán a potvrdí DSC zásady vytváření názvů pro</span><span class="sxs-lookup"><span data-stu-id="b7749-121">Friendly name is specified and confirms to DSC naming conventions</span></span>

  <span data-ttu-id="b7749-122">Příklad: `[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]`</span><span class="sxs-lookup"><span data-stu-id="b7749-122">Example: `[ClassVersion("1.0.0.0"), FriendlyName("xRemoteFile")]`</span></span>

- <span data-ttu-id="b7749-123">Každé pole má výstižný popis.</span><span class="sxs-lookup"><span data-stu-id="b7749-123">Every field has meaningful description.</span></span> <span data-ttu-id="b7749-124">Úložiště GitHub Powershellu má dobrými příklady, například [. schema.mof pro xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span><span class="sxs-lookup"><span data-stu-id="b7749-124">The PowerShell GitHub repository has good examples, such as [the .schema.mof for xRemoteFile](https://github.com/PowerShell/xPSDesiredStateConfiguration/blob/dev/DSCResources/MSFT_xRemoteFile/MSFT_xRemoteFile.schema.mof)</span></span>

<span data-ttu-id="b7749-125">Kromě toho byste měli použít **testovací xDscResource** a **testovací xDscSchema** rutiny z [Návrhář prostředků DSC](https://www.powershellgallery.com/packages/xDSCResourceDesigner) můžete si automaticky ověřit zdroj a schéma:</span><span class="sxs-lookup"><span data-stu-id="b7749-125">Additionally, you should use **Test-xDscResource** and **Test-xDscSchema** cmdlets from [DSC Resource Designer](https://www.powershellgallery.com/packages/xDSCResourceDesigner) to automatically verify the resource and schema:</span></span>

```
Test-xDscResource <Resource_folder>
Test-xDscSchema <Path_to_resource_schema_file>
```

<span data-ttu-id="b7749-126">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b7749-126">For example:</span></span>

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="resource-loads-without-errors"></a><span data-ttu-id="b7749-127">Prostředek načte bez chyb</span><span class="sxs-lookup"><span data-stu-id="b7749-127">Resource loads without errors</span></span>

<span data-ttu-id="b7749-128">Zkontrolujte, zda modul prostředků je možné úspěšně načíst.</span><span class="sxs-lookup"><span data-stu-id="b7749-128">Check whether the resource module can be successfully loaded.</span></span>
<span data-ttu-id="b7749-129">Toho lze dosáhnout ručně spuštěním `Import-Module <resource_module> -force` a potvrzení, že nedošlo k žádným chybám, nebo za zápis automatizace testů.</span><span class="sxs-lookup"><span data-stu-id="b7749-129">This can be achieved manually, by running `Import-Module <resource_module> -force` and confirming that no errors occurred, or by writing test automation.</span></span> <span data-ttu-id="b7749-130">V druhém případě můžete postupovat podle této struktuře ve svém testovacím případu:</span><span class="sxs-lookup"><span data-stu-id="b7749-130">In case of the latter, you can follow this structure in your test case:</span></span>

```powershell
$error = $null
Import-Module <resource_module> –force
If ($error.count –ne 0) {
    Throw “Module was not imported correctly. Errors returned: $error”
}
```

## <a name="resource-is-idempotent-in-the-positive-case"></a><span data-ttu-id="b7749-131">Prostředek je idempotentní v případě pozitivní</span><span class="sxs-lookup"><span data-stu-id="b7749-131">Resource is idempotent in the positive case</span></span>

<span data-ttu-id="b7749-132">Mezi základní charakteristiky prostředky DSC je idempotence.</span><span class="sxs-lookup"><span data-stu-id="b7749-132">One of the fundamental characteristics of DSC resources is idempotence.</span></span> <span data-ttu-id="b7749-133">Znamená to, že použití DSC konfigurace obsahující více než jednou tento prostředek se vždycky dosažení stejného výsledku.</span><span class="sxs-lookup"><span data-stu-id="b7749-133">It means that applying a DSC configuration containing that resource multiple times will always achieve the same result.</span></span> <span data-ttu-id="b7749-134">Pokud například vytvoříme konfigurace, která obsahuje následující prostředek souboru:</span><span class="sxs-lookup"><span data-stu-id="b7749-134">For example, if we create a configuration which contains the following File resource:</span></span>

```powershell
File file {
    DestinationPath = "C:\test\test.txt"
    Contents = "Sample text"
}
```

<span data-ttu-id="b7749-135">Po jeho použití poprvé souboru test.txt by se zobrazit v `C:\test` složky.</span><span class="sxs-lookup"><span data-stu-id="b7749-135">After applying it for the first time, file test.txt should appear in `C:\test` folder.</span></span> <span data-ttu-id="b7749-136">Ale při dalším spuštění se stejnou konfigurací by neměla změnit stav počítače (třeba žádná kopie `test.txt` by měl být vytvořen soubor).</span><span class="sxs-lookup"><span data-stu-id="b7749-136">However, subsequent runs of the same configuration should not change the state of the machine (e.g. no copies of the `test.txt` file should be created).</span></span>
<span data-ttu-id="b7749-137">K zajištění prostředek je idempotentní můžete opakovaně volat `Set-TargetResource` při testování prostředku přímo, nebo volat `Start-DscConfiguration` více než jednou při provádění testování začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="b7749-137">To ensure a resource is idempotent you can repeatedly call `Set-TargetResource` when testing the resource directly, or call `Start-DscConfiguration` multiple times when doing end to end testing.</span></span> <span data-ttu-id="b7749-138">Výsledek by měl být stejný po každé spuštění.</span><span class="sxs-lookup"><span data-stu-id="b7749-138">The result should be the same after every run.</span></span>

## <a name="test-user-modification-scenario"></a><span data-ttu-id="b7749-139">Testovací scénář úpravy uživatele</span><span class="sxs-lookup"><span data-stu-id="b7749-139">Test user modification scenario</span></span>

<span data-ttu-id="b7749-140">Změna stavu počítače a pak znovu spustíte DSC, můžete ověřit, že `Set-TargetResource` a `Test-TargetResource` fungovat správně.</span><span class="sxs-lookup"><span data-stu-id="b7749-140">By changing the state of the machine and then rerunning DSC, you can verify that `Set-TargetResource` and `Test-TargetResource` function properly.</span></span> <span data-ttu-id="b7749-141">Tady jsou kroky, které byste měli provést:</span><span class="sxs-lookup"><span data-stu-id="b7749-141">Here are steps you should take:</span></span>

1. <span data-ttu-id="b7749-142">Začněte s prostředku není v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="b7749-142">Start with the resource not in the desired state.</span></span>
2. <span data-ttu-id="b7749-143">Konfigurace spuštění s vaším prostředkem</span><span class="sxs-lookup"><span data-stu-id="b7749-143">Run configuration with your resource</span></span>
3. <span data-ttu-id="b7749-144">Ověřte `Test-DscConfiguration` vrátí hodnotu True</span><span class="sxs-lookup"><span data-stu-id="b7749-144">Verify `Test-DscConfiguration` returns True</span></span>
4. <span data-ttu-id="b7749-145">Upravit nakonfigurované položky, která má být z požadovaného stavu</span><span class="sxs-lookup"><span data-stu-id="b7749-145">Modify the configured item to be out of the desired state</span></span>
5. <span data-ttu-id="b7749-146">Ověřte `Test-DscConfiguration` vrátí hodnotu false</span><span class="sxs-lookup"><span data-stu-id="b7749-146">Verify `Test-DscConfiguration` returns false</span></span>

<span data-ttu-id="b7749-147">Zde je příklad konkrétnější pomocí registru prostředků:</span><span class="sxs-lookup"><span data-stu-id="b7749-147">Here’s a more concrete example using Registry resource:</span></span>

1. <span data-ttu-id="b7749-148">Spustit pomocí klíče registru není v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="b7749-148">Start with registry key not in the desired state</span></span>
2. <span data-ttu-id="b7749-149">Spustit `Start-DscConfiguration` s konfiguraci, kterou chcete vložit ho do požadovaného stavu a ověří, že předává.</span><span class="sxs-lookup"><span data-stu-id="b7749-149">Run `Start-DscConfiguration` with a configuration to put it in the desired state and verify it passes.</span></span>
3. <span data-ttu-id="b7749-150">Spustit `Test-DscConfiguration` a ověřit, vrátí hodnotu true</span><span class="sxs-lookup"><span data-stu-id="b7749-150">Run `Test-DscConfiguration` and verify it returns true</span></span>
4. <span data-ttu-id="b7749-151">Upravte hodnotu klíče, aby není v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="b7749-151">Modify the value of the key so that it is not in the desired state</span></span>
5. <span data-ttu-id="b7749-152">Spustit `Test-DscConfiguration` a ověřit, vrátí hodnotu false</span><span class="sxs-lookup"><span data-stu-id="b7749-152">Run `Test-DscConfiguration` and verify it returns false</span></span>
6. <span data-ttu-id="b7749-153">`Get-TargetResource` funkce se ověřila pomocí `Get-DscConfiguration`</span><span class="sxs-lookup"><span data-stu-id="b7749-153">`Get-TargetResource` functionality was verified using `Get-DscConfiguration`</span></span>

<span data-ttu-id="b7749-154">`Get-TargetResource` by měl vrátit podrobnosti o aktuálním stavem prostředku.</span><span class="sxs-lookup"><span data-stu-id="b7749-154">`Get-TargetResource` should return details of the current state of the resource.</span></span> <span data-ttu-id="b7749-155">Ujistěte se, že ho otestovat pomocí volání `Get-DscConfiguration` po použití konfigurace a ověření, který výstup správně odráží aktuální stav stroje.</span><span class="sxs-lookup"><span data-stu-id="b7749-155">Make sure to test it by calling `Get-DscConfiguration` after you apply the configuration and verifying that output correctly reflects the current state of the machine.</span></span> <span data-ttu-id="b7749-156">Je potřeba otestovat samostatně, protože všechny problémy v této oblasti se nezobrazí při volání metody `Start-DscConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="b7749-156">It's important to test it separately, since any issues in this area won't appear when calling `Start-DscConfiguration`.</span></span>

## <a name="call-getsettest-targetresource-functions-directly"></a><span data-ttu-id="b7749-157">Volání **Get/Set/Test-TargetResource** přímo funkce</span><span class="sxs-lookup"><span data-stu-id="b7749-157">Call **Get/Set/Test-TargetResource** functions directly</span></span>

<span data-ttu-id="b7749-158">Ujistěte se, že je otestovat **Get/Set/Test-TargetResource** funkce implementované ve svém prostředku přímého volání a ověření, že fungují podle očekávání.</span><span class="sxs-lookup"><span data-stu-id="b7749-158">Make sure you test the **Get/Set/Test-TargetResource** functions implemented in your resource by calling them directly and verifying that they work as expected.</span></span>

## <a name="verify-end-to-end-using-start-dscconfiguration"></a><span data-ttu-id="b7749-159">Ověření pomocí koncového **Start-DscConfiguration**</span><span class="sxs-lookup"><span data-stu-id="b7749-159">Verify End to End using **Start-DscConfiguration**</span></span>

<span data-ttu-id="b7749-160">Testování **Get/Set/Test-TargetResource** funkcí pomocí přímého volání je důležité, ale ne všechny problémy, bude zjištěno tímto způsobem.</span><span class="sxs-lookup"><span data-stu-id="b7749-160">Testing **Get/Set/Test-TargetResource** functions by calling them directly is important, but not all issues will be discovered this way.</span></span> <span data-ttu-id="b7749-161">Měli byste se zaměřit podstatnou část testování pomocí `Start-DscConfiguration` nebo serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="b7749-161">You should focus significant part of your testing on using `Start-DscConfiguration` or the pull server.</span></span> <span data-ttu-id="b7749-162">Ve skutečnosti to je, jak budou uživatelé používat prostředků, takže Nepodceňujte význam tohoto typu testy.</span><span class="sxs-lookup"><span data-stu-id="b7749-162">In fact, this is how users will use the resource, so don’t underestimate the significance of this type of tests.</span></span>
<span data-ttu-id="b7749-163">Možné typy problémů:</span><span class="sxs-lookup"><span data-stu-id="b7749-163">Possible types of issues:</span></span>

- <span data-ttu-id="b7749-164">Přihlašovací údaje nebo relace může chovat jinak, protože DSC agent běží jako služba.</span><span class="sxs-lookup"><span data-stu-id="b7749-164">Credential/Session may behave differently because the DSC agent runs as a service.</span></span>  <span data-ttu-id="b7749-165">Nezapomeňte otestovat tady žádné funkce začátku do konce.</span><span class="sxs-lookup"><span data-stu-id="b7749-165">Be sure to test any features here end to end.</span></span>
- <span data-ttu-id="b7749-166">Ve výstupu chyby `Start-DscConfiguration` může být jiný než ty, které zobrazí při volání `Set-TargetResource` fungovat přímo.</span><span class="sxs-lookup"><span data-stu-id="b7749-166">Errors output by `Start-DscConfiguration` may be different than those displayed when calling the `Set-TargetResource` function directly.</span></span>

## <a name="test-compatability-on-all-dsc-supported-platforms"></a><span data-ttu-id="b7749-167">Kompatibilita test na všechny DSC podporované platformy</span><span class="sxs-lookup"><span data-stu-id="b7749-167">Test compatability on all DSC supported platforms</span></span>

<span data-ttu-id="b7749-168">Prostředků by měly fungovat na všech platformách nepodporuje DSC (Windows Server 2008 R2 a novější).</span><span class="sxs-lookup"><span data-stu-id="b7749-168">Resource should work on all DSC supported platforms (Windows Server 2008 R2 and newer).</span></span> <span data-ttu-id="b7749-169">Nainstalujte nejnovější WMF (Windows Management Framework) na vašem operačním systému, abyste získali nejnovější verzi DSC.</span><span class="sxs-lookup"><span data-stu-id="b7749-169">Install the latest WMF (Windows Management Framework) on your OS to get the latest version of DSC.</span></span> <span data-ttu-id="b7749-170">Pokud váš prostředek nelze použít u některé z těchto platforem záměrné, má být vrácen určité chybové zprávě.</span><span class="sxs-lookup"><span data-stu-id="b7749-170">If your resource does not work on some of these platforms by design, a specific error message should be returned.</span></span> <span data-ttu-id="b7749-171">Také se ujistěte, že váš prostředek kontroluje, zda jsou rutiny, ke kterému se připojujete na konkrétním počítači.</span><span class="sxs-lookup"><span data-stu-id="b7749-171">Also, make sure your resource checks whether cmdlets you are calling are present on particular machine.</span></span> <span data-ttu-id="b7749-172">Windows Server 2012 přidali velký počet nové rutiny, které nejsou k dispozici na Windows Server 2008 R2, i při instalaci WMF.</span><span class="sxs-lookup"><span data-stu-id="b7749-172">Windows Server 2012 added a large number of new cmdlets that are not available on Windows Server 2008R2, even with WMF installed.</span></span>

## <a name="verify-on-windows-client-if-applicable"></a><span data-ttu-id="b7749-173">Ověřte v klientovi Windows (Pokud je k dispozici)</span><span class="sxs-lookup"><span data-stu-id="b7749-173">Verify on Windows Client (if applicable)</span></span>

<span data-ttu-id="b7749-174">Jednu mezeru velmi běžné testu se ověřuje se prostředek pouze v serverových verzí systému Windows.</span><span class="sxs-lookup"><span data-stu-id="b7749-174">One very common test gap is verifying the resource only on server versions of Windows.</span></span> <span data-ttu-id="b7749-175">Mnoho prostředků jsou také navrženy pro práci na SKU klienta, takže pokud je to váš případ true, nezapomeňte ji otestovat na těchto platformách.</span><span class="sxs-lookup"><span data-stu-id="b7749-175">Many resources are also designed to work on Client SKUs, so if that’s true in your case, don’t forget to test it on those platforms as well.</span></span>

## <a name="get-dscresource-lists-the-resource"></a><span data-ttu-id="b7749-176">Get-DSCResource uvádí prostředku</span><span class="sxs-lookup"><span data-stu-id="b7749-176">Get-DSCResource lists the resource</span></span>

<span data-ttu-id="b7749-177">Po nasazení modulu volání `Get-DscResource` váš prostředek mimo jiné díky tomu zveřejnit.</span><span class="sxs-lookup"><span data-stu-id="b7749-177">After deploying the module, calling `Get-DscResource` should list your resource among others as a result.</span></span> <span data-ttu-id="b7749-178">Pokud váš prostředek nejde najít v seznamu, ujistěte se, že tento soubor schema.mof pro daný prostředek existuje.</span><span class="sxs-lookup"><span data-stu-id="b7749-178">If you can’t find your resource in the list, make sure that schema.mof file for that resource exists.</span></span>

## <a name="resource-module-contains-examples"></a><span data-ttu-id="b7749-179">Modul prostředků obsahuje příklady</span><span class="sxs-lookup"><span data-stu-id="b7749-179">Resource module contains examples</span></span>

<span data-ttu-id="b7749-180">Vytváření kvalitní příklady, které pomůže ostatním pochopit, jak ho použít.</span><span class="sxs-lookup"><span data-stu-id="b7749-180">Creating quality examples which will help others understand how to use it.</span></span> <span data-ttu-id="b7749-181">Toto je zásadní, zejména, protože mnoho uživatelů považovat dokumentaci ukázkový kód.</span><span class="sxs-lookup"><span data-stu-id="b7749-181">This is crucial, especially since many users treat sample code as documentation.</span></span>

- <span data-ttu-id="b7749-182">Nejdřív byste měli určit příklady, které budou součástí modulu – minimálně, by mělo zahrnovat nejdůležitější případy použití pro prostředek:</span><span class="sxs-lookup"><span data-stu-id="b7749-182">First, you should determine the examples that will be included with the module – at minimum, you should cover most important use cases for your resource:</span></span>
- <span data-ttu-id="b7749-183">Pokud modul obsahuje několik prostředků, které je potřeba ve scénáři začátku do konce společně, základní příklad začátku do konce v ideálním případě by první.</span><span class="sxs-lookup"><span data-stu-id="b7749-183">If your module contains several resources that need to work together for an end-to-end scenario, the basic end-to-end example would ideally be first.</span></span>
- <span data-ttu-id="b7749-184">Počáteční příklady by měla být velmi jednoduché – jak začít pracovat s vašimi prostředky v malých spravovatelných blocích (třeba vytvoření nového virtuálního pevného disku)</span><span class="sxs-lookup"><span data-stu-id="b7749-184">The initial examples should be very simple -- how to get started with your resources in small manageable chunks (e.g. creating a new VHD)</span></span>
- <span data-ttu-id="b7749-185">Následující příklady by měl vytvářet v těchto příkladech (např. vytvoření virtuálního počítače z virtuálního pevného disku, odebrání virtuálního počítače, změna virtuálního počítače) a zobrazit pokročilé funkce (např. vytvoření virtuálního počítače s dynamickou pamětí)</span><span class="sxs-lookup"><span data-stu-id="b7749-185">Subsequent examples should build on those examples (e.g. creating a VM from a VHD, removing VM, modifying VM), and show advanced functionality (e.g. creating a VM with dynamic memory)</span></span>
- <span data-ttu-id="b7749-186">Příklad konfigurace by měly být parametrizovány (všechny hodnoty by měly být předány konfiguraci jako parametry a měl by existovat žádné hodnoty pevně zakódované):</span><span class="sxs-lookup"><span data-stu-id="b7749-186">Example configurations should be parameterized (all values should be passed to the configuration as parameters and there should be no hardcoded values):</span></span>

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

- <span data-ttu-id="b7749-187">Je dobrým zvykem zahrnout (komentovaný navýšení kapacity) příklad toho, jak volat konfigurace a skutečné hodnoty na konci ukázkový skript.</span><span class="sxs-lookup"><span data-stu-id="b7749-187">It’s a good practice to include (commented out) example of how to call the configuration with the actual values at the end of the example script.</span></span>
  <span data-ttu-id="b7749-188">Například ve výše uvedené konfigurace není nutně jasné, že je nejlepší způsob, jak určit UserAgent:</span><span class="sxs-lookup"><span data-stu-id="b7749-188">For example, in the configuration above it isn't necessarily obvious that the best way to specify UserAgent is:</span></span>

  <span data-ttu-id="b7749-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` Komentář v takovém případě můžete zpřehlednit zamýšlený provádění konfigurace:</span><span class="sxs-lookup"><span data-stu-id="b7749-189">`UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer` In which case a comment can clarify the intended execution of the configuration:</span></span>

  ```powershell
  <#
  Sample use (parameter values need to be changed according to your scenario):

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg"

  Sample_xRemoteFile_DownloadFile -destinationPath "$env:SystemDrive\fileName.jpg" -uri "http://www.contoso.com/image.jpg" `
  -userAgent [Microsoft.PowerShell.Commands.PSUserAgent]::InternetExplorer -headers @{"Accept-Language" = "en-US"}
  #>
  ```

- <span data-ttu-id="b7749-190">Pro každý příklad zápisu krátký popis, který vysvětluje, co to dělá a význam parametry.</span><span class="sxs-lookup"><span data-stu-id="b7749-190">For each example, write a short description which explains what it does, and the meaning of the parameters.</span></span>
- <span data-ttu-id="b7749-191">Ujistěte se, že příklady pokrývají většinu scénářů, které jsou důležité pro váš prostředek a pokud není nic nechybí, ověřte, že všechny spustit a změnit počítače v požadovaném stavu.</span><span class="sxs-lookup"><span data-stu-id="b7749-191">Make sure examples cover most the important scenarios for your resource and if there’s nothing missing, verify that they all execute and put machine in the desired state.</span></span>

## <a name="error-messages-are-easy-to-understand-and-help-users-solve-problems"></a><span data-ttu-id="b7749-192">Chybové zprávy jsou srozumitelné a pomáhají uživatelům řešit problémy</span><span class="sxs-lookup"><span data-stu-id="b7749-192">Error messages are easy to understand and help users solve problems</span></span>

<span data-ttu-id="b7749-193">By měl být dobrým chybové zprávy:</span><span class="sxs-lookup"><span data-stu-id="b7749-193">Good error messages should be:</span></span>

- <span data-ttu-id="b7749-194">: Největší problém s chybovými zprávami je, že často neexistují, proto se ujistěte, že jsou zde.</span><span class="sxs-lookup"><span data-stu-id="b7749-194">There: The biggest problem with error messages is that they often don’t exist, so make sure they are there.</span></span>
- <span data-ttu-id="b7749-195">Snadná na pochopení: lidské čitelný, ne skrytého chybové kódy</span><span class="sxs-lookup"><span data-stu-id="b7749-195">Easy to understand: Human readable, no obscure error codes</span></span>
- <span data-ttu-id="b7749-196">Přesné: Popisují, co je právě tento problém</span><span class="sxs-lookup"><span data-stu-id="b7749-196">Precise: Describe what’s exactly the problem</span></span>
- <span data-ttu-id="b7749-197">Konstruktivní: Pokyny k vyřešení problému</span><span class="sxs-lookup"><span data-stu-id="b7749-197">Constructive: Advice how to fix the issue</span></span>
- <span data-ttu-id="b7749-198">Zdvořilé: Nemáte blame uživatele nebo je pocit, že chybné</span><span class="sxs-lookup"><span data-stu-id="b7749-198">Polite: Don’t blame user or make them feel bad</span></span>

<span data-ttu-id="b7749-199">Ujistěte se, že ověříte chyby v komplexní scénáře (pomocí `Start-DscConfiguration`), protože se může lišit od těch vráceného po spuštění funkce resource přímo.</span><span class="sxs-lookup"><span data-stu-id="b7749-199">Make sure you verify errors in End to End scenarios (using `Start-DscConfiguration`), because they may differ from those returned when running resource functions directly.</span></span>

## <a name="log-messages-are-easy-to-understand-and-informative-including-verbose-debug-and-etw-logs"></a><span data-ttu-id="b7749-200">Zprávy protokolu jsou snadno pochopitelný a informativní (včetně – verbose, – ladění a protokoly trasování událostí pro Windows)</span><span class="sxs-lookup"><span data-stu-id="b7749-200">Log messages are easy to understand and informative (including –verbose, –debug and ETW logs)</span></span>

<span data-ttu-id="b7749-201">Zajistěte, aby byly protokoly výstupem prostředkem srozumitelné a zadejte hodnotu pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="b7749-201">Ensure that logs outputted by the resource are easy to understand and provide value to the user.</span></span> <span data-ttu-id="b7749-202">Prostředky by měly výstup všechny informace, které mohou být pro uživatele užitečné, ale další protokoly není vždy lepší.</span><span class="sxs-lookup"><span data-stu-id="b7749-202">Resources should output all information which might be helpful to the user, but more logs is not always better.</span></span> <span data-ttu-id="b7749-203">Měli byste vyhnout redundance a výstup dat, která ho nemá zvyšujících hodnotu – neprovádějte někdo projít stovky položek protokolu. Pokud chcete zjistit, co hledají.</span><span class="sxs-lookup"><span data-stu-id="b7749-203">You should avoid redundancy and outputting data which does not provide additional value – don’t make someone go through hundreds of log entries in order to find what they're looking for.</span></span> <span data-ttu-id="b7749-204">Samozřejmě žádné protokoly není přijatelná řešení tohoto problému buď.</span><span class="sxs-lookup"><span data-stu-id="b7749-204">Of course, no logs is not an acceptable solution for this problem either.</span></span>

<span data-ttu-id="b7749-205">Při testování, by měl také podrobné analýze a ladění protokoly (spuštěním `Start-DscConfiguration` s `–Verbose` a `–Debug` přepne odpovídajícím způsobem), stejně jako protokoly trasování událostí pro Windows.</span><span class="sxs-lookup"><span data-stu-id="b7749-205">When testing, you should also analyze verbose and debug logs (by running `Start-DscConfiguration` with `–Verbose` and `–Debug` switches appropriately), as well as ETW logs.</span></span> <span data-ttu-id="b7749-206">Pokud chcete zobrazit protokoly trasování událostí pro Windows DSC, přejděte do prohlížeče událostí a otevřete následující složku: aplikací a služeb společnosti Microsoft - Windows - Desired State Configuration.</span><span class="sxs-lookup"><span data-stu-id="b7749-206">To see DSC ETW logs, go to Event Viewer and open the following folder: Applications and Services- Microsoft - Windows - Desired State Configuration.</span></span>  <span data-ttu-id="b7749-207">Ve výchozím nastavení existuje budou provozní kanál, ale ujistěte se, že povolíte analytické a ladit kanály před spuštěním konfigurace.</span><span class="sxs-lookup"><span data-stu-id="b7749-207">By default there will be Operational channel, but make sure you enable Analytic and Debug channels before running the configuration.</span></span>
<span data-ttu-id="b7749-208">Povolení analýzy/Debug kanály, můžete spustit skript níže:</span><span class="sxs-lookup"><span data-stu-id="b7749-208">To enable Analytic/Debug channels, you can execute script below:</span></span>

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

## <a name="resource-implementation-does-not-contain-hardcoded-paths"></a><span data-ttu-id="b7749-209">Implementace prostředků neobsahuje pevně zakódované cesty</span><span class="sxs-lookup"><span data-stu-id="b7749-209">Resource implementation does not contain hardcoded paths</span></span>

<span data-ttu-id="b7749-210">Zkontrolujte v implementaci prostředku nejsou žádné pevně zakódované cesty, zejména v případě, že předpokládají jazyka (en-us), nebo když se systémové proměnné, které lze použít.</span><span class="sxs-lookup"><span data-stu-id="b7749-210">Ensure there are no hardcoded paths in the resource implementation, particularly if they assume language (en-us), or when there are system variables that can be used.</span></span>
<span data-ttu-id="b7749-211">Pokud váš prostředek potřebovat přístup ke konkrétní cesty, proměnné prostředí použít namísto hardcoding cestu, protože se může lišit na jiných počítačích.</span><span class="sxs-lookup"><span data-stu-id="b7749-211">If your resource need to access specific paths, use environment variables instead of hardcoding the path, as it may differ on other machines.</span></span>

<span data-ttu-id="b7749-212">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b7749-212">Example:</span></span>

<span data-ttu-id="b7749-213">Namísto:</span><span class="sxs-lookup"><span data-stu-id="b7749-213">Instead of:</span></span>

```powershell
$tempPath = "C:\Users\kkaczma\AppData\Local\Temp\MyResource"
$programFilesPath = "C:\Program Files (x86)"
```

<span data-ttu-id="b7749-214">Můžete psát:</span><span class="sxs-lookup"><span data-stu-id="b7749-214">You can write:</span></span>

```powershell
$tempPath = Join-Path $env:temp "MyResource"
$programFilesPath = ${env:ProgramFiles(x86)}
```

## <a name="resource-implementation-does-not-contain-user-information"></a><span data-ttu-id="b7749-215">Implementace prostředků neobsahuje informace o uživateli</span><span class="sxs-lookup"><span data-stu-id="b7749-215">Resource implementation does not contain user information</span></span>

<span data-ttu-id="b7749-216">Ujistěte se, že neexistují žádné názvy e-mailu, informace o účtu nebo jména osob v kódu.</span><span class="sxs-lookup"><span data-stu-id="b7749-216">Make sure there are no email names, account information, or names of people in the code.</span></span>

## <a name="resource-was-tested-with-validinvalid-credentials"></a><span data-ttu-id="b7749-217">Prostředek byl testován s přihlašovacími údaji platná nebo není platné</span><span class="sxs-lookup"><span data-stu-id="b7749-217">Resource was tested with valid/invalid credentials</span></span>

<span data-ttu-id="b7749-218">Pokud váš prostředek přijímá jako parametr přihlašovacích údajů:</span><span class="sxs-lookup"><span data-stu-id="b7749-218">If your resource takes a credential as parameter:</span></span>

- <span data-ttu-id="b7749-219">Při místní systém (nebo účet počítače pro vzdálené prostředky) nemá přístup zkontrolujte, jestli funguje prostředků.</span><span class="sxs-lookup"><span data-stu-id="b7749-219">Verify the resource works when Local System (or the computer account for remote resources) does not have access.</span></span>
- <span data-ttu-id="b7749-220">Zkontrolujte prostředek funguje s přihlašovacími údaji zadaný pro získání, nastavení a testování</span><span class="sxs-lookup"><span data-stu-id="b7749-220">Verify the resource works with a credential specified for Get, Set and Test</span></span>
- <span data-ttu-id="b7749-221">Pokud váš prostředek přistupuje ke sdílené složky, otestujte všechny varianty, které potřebujete pro podporu, jako například:</span><span class="sxs-lookup"><span data-stu-id="b7749-221">If your resource accesses shares, test all the variants you need to support, such as:</span></span>
  - <span data-ttu-id="b7749-222">Sdílené složky windows na úrovni Standard.</span><span class="sxs-lookup"><span data-stu-id="b7749-222">Standard windows shares.</span></span>
  - <span data-ttu-id="b7749-223">Sdílené složky systému souborů DFS.</span><span class="sxs-lookup"><span data-stu-id="b7749-223">DFS shares.</span></span>
  - <span data-ttu-id="b7749-224">SAMBA složek (Pokud chcete zajistit podporu Linuxu.)</span><span class="sxs-lookup"><span data-stu-id="b7749-224">SAMBA shares (if you want to support Linux.)</span></span>

## <a name="resource-does-not-require-interactive-input"></a><span data-ttu-id="b7749-225">Prostředek nepotřebuje interaktivní vstup</span><span class="sxs-lookup"><span data-stu-id="b7749-225">Resource does not require interactive input</span></span>

<span data-ttu-id="b7749-226">**Get/Set/Test-TargetResource** funkce by měla být spouštěny automaticky a nesmí čekat, až se uživatelovo zadání v jakékoli fázi spuštění (například byste neměli používat `Get-Credential` uvnitř těchto funkcí).</span><span class="sxs-lookup"><span data-stu-id="b7749-226">**Get/Set/Test-TargetResource** functions should be executed automatically and must not wait for user’s input at any stage of execution (e.g. you should not use `Get-Credential` inside these functions).</span></span> <span data-ttu-id="b7749-227">Pokud je třeba zadat uživatelský vstup, je třeba předat ho do konfigurace jako parametr během fáze kompilace.</span><span class="sxs-lookup"><span data-stu-id="b7749-227">If you need to provide user’s input, you should pass it to the configuration as parameter during the compilation phase.</span></span>

## <a name="resource-functionality-was-thoroughly-tested"></a><span data-ttu-id="b7749-228">Funkce prostředků byla důkladně otestována.</span><span class="sxs-lookup"><span data-stu-id="b7749-228">Resource functionality was thoroughly tested</span></span>

<span data-ttu-id="b7749-229">Tento kontrolní seznam obsahuje položky, které jsou důležité k testování a/nebo jsou často provedena.</span><span class="sxs-lookup"><span data-stu-id="b7749-229">This checklist contains items which are important to be tested and/or are often missed.</span></span> <span data-ttu-id="b7749-230">Bude existovat mnoho testů, hlavně funkční ty, které budou mít specifická pro prostředek, testování a nejsou zde uvedeny.</span><span class="sxs-lookup"><span data-stu-id="b7749-230">There will be bunch of tests, mainly functional ones which will be specific to the resource you are testing and are not mentioned here.</span></span> <span data-ttu-id="b7749-231">Nezapomeňte o záporné testovací případy.</span><span class="sxs-lookup"><span data-stu-id="b7749-231">Don’t forget about negative test cases.</span></span>

## <a name="best-practice-resource-module-contains-tests-folder-with-resourcedesignertestsps1-script"></a><span data-ttu-id="b7749-232">Osvědčený postup: modul prostředků obsahuje složku testy s ResourceDesignerTests.ps1 skriptu</span><span class="sxs-lookup"><span data-stu-id="b7749-232">Best practice: Resource module contains Tests folder with ResourceDesignerTests.ps1 script</span></span>

<span data-ttu-id="b7749-233">Je vhodné vytvořit složku "testy" uvnitř modulu prostředků, vytvořte `ResourceDesignerTests.ps1` a přidejte testy pomocí **testovací xDscResource** a **testovací xDscSchema** pro všechny prostředky v zadané modulu.</span><span class="sxs-lookup"><span data-stu-id="b7749-233">It’s a good practice to create folder “Tests” inside resource module, create `ResourceDesignerTests.ps1` file and add tests using **Test-xDscResource** and **Test-xDscSchema** for all resources in given module.</span></span>
<span data-ttu-id="b7749-234">Tímto způsobem můžete rychle ověřit schémata všechny prostředky z daného moduly a nechcete, zkontrolujte vhodnosti před publikováním.</span><span class="sxs-lookup"><span data-stu-id="b7749-234">This way you can quickly validate schemas of all resources from the given modules and do a sanity check before publishing.</span></span>
<span data-ttu-id="b7749-235">Pro xRemoteFile `ResourceTests.ps1` může vypadat stejně snadné jako:</span><span class="sxs-lookup"><span data-stu-id="b7749-235">For xRemoteFile, `ResourceTests.ps1` could look as simple as:</span></span>

```powershell
Test-xDscResource ..\DSCResources\MSFT_xRemoteFile
Test-xDscSchema ..\DSCResources\MSFT_xRemoteFile\MSFT_xRemoteFile.schema.mof
```

## <a name="best-practice-resource-folder-contains-resource-designer-script-for-generating-schema"></a><span data-ttu-id="b7749-236">Osvědčený postup: Složka prostředků obsahuje návrháře skript prostředků pro generování schématu</span><span class="sxs-lookup"><span data-stu-id="b7749-236">Best practice: Resource folder contains resource designer script for generating schema</span></span>

<span data-ttu-id="b7749-237">Každý prostředek by měl obsahovat návrháře skript prostředků, který generuje schématu mof prostředku.</span><span class="sxs-lookup"><span data-stu-id="b7749-237">Each resource should contain a resource designer script which generates a mof schema of the resource.</span></span> <span data-ttu-id="b7749-238">Tento soubor by měl být umístěn v `<ResourceName>\ResourceDesignerScripts` a bude mít název generovat `<ResourceName>Schema.ps1` xRemoteFile prostředků tento soubor bude označovat `GenerateXRemoteFileSchema.ps1` a obsahovat:</span><span class="sxs-lookup"><span data-stu-id="b7749-238">This file should be placed in `<ResourceName>\ResourceDesignerScripts` and be named Generate `<ResourceName>Schema.ps1` For xRemoteFile resource this file would be called `GenerateXRemoteFileSchema.ps1` and contain:</span></span>

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

## <a name="best-practice-resource-supports--whatif"></a><span data-ttu-id="b7749-239">Osvědčený postup: - WhatIf prostředek podporuje.</span><span class="sxs-lookup"><span data-stu-id="b7749-239">Best practice: Resource supports -WhatIf</span></span>

<span data-ttu-id="b7749-240">Pokud váš prostředek je provádění operací "nebezpečných", je vhodné provádět `-WhatIf` funkce.</span><span class="sxs-lookup"><span data-stu-id="b7749-240">If your resource is performing “dangerous” operations, it’s a good practice to implement `-WhatIf` functionality.</span></span> <span data-ttu-id="b7749-241">Po dokončení, ujistěte se, že `-WhatIf` výstup správně popisuje operace, které by mohlo dojít, pokud příkaz se provedl zcela bez `-WhatIf` přepnout.</span><span class="sxs-lookup"><span data-stu-id="b7749-241">After it’s done, make sure that `-WhatIf` output correctly describes operations which would happen if command was executed without `-WhatIf` switch.</span></span>
<span data-ttu-id="b7749-242">Ověřte také, že operace nespustí (nebudou provedeny žádné změny uzlu stavu) při `–WhatIf` přepínači je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="b7749-242">Also, verify that operations does not execute (no changes to the node’s state are made) when `–WhatIf` switch is present.</span></span>
<span data-ttu-id="b7749-243">Předpokládejme například, že se testují souboru prostředků.</span><span class="sxs-lookup"><span data-stu-id="b7749-243">For example, let’s assume we are testing File resource.</span></span> <span data-ttu-id="b7749-244">Níže je jednoduchý konfigurace, která vytvoří soubor `test.txt` s obsahem "test":</span><span class="sxs-lookup"><span data-stu-id="b7749-244">Below is simple configuration which creates file `test.txt` with contents “test”:</span></span>

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

<span data-ttu-id="b7749-245">Pokud jsme kompilovat a pak proveďte konfiguraci `-WhatIf` přepínače, výstup se dozvíme přesně co by mohlo dojít při konfiguraci zajišťuje každodenní provoz.</span><span class="sxs-lookup"><span data-stu-id="b7749-245">If we compile and then execute the configuration with the `-WhatIf` switch, the output is telling us exactly what would happen when we run the configuration.</span></span> <span data-ttu-id="b7749-246">V konfiguraci samotného ale neprovedl (`test.txt` soubor nebyl vytvořen).</span><span class="sxs-lookup"><span data-stu-id="b7749-246">The configuration itself however was not executed (`test.txt` file was not created).</span></span>

```powershell
Start-DscConfiguration -Path .\config -ComputerName localhost -Wait -Verbose -WhatIf
```

```output
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

<span data-ttu-id="b7749-247">Tento seznam není úplný, ale zahrnuje mnoho důležité problémy, které může dojít při navrhování, vývoj a testování prostředky DSC.</span><span class="sxs-lookup"><span data-stu-id="b7749-247">This list is not exhaustive, but it covers many important issues which can be encountered while designing, developing and testing DSC resources.</span></span>

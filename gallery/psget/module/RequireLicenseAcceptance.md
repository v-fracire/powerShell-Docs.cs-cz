---
ms.date: 2017-06-09
schema: 2.0.0
keywords: "Prostředí PowerShell"
title: RequireLicenseAcceptance
ms.openlocfilehash: 260ccc1ee52d09a640e88203c5644f20f9723d6f
ms.sourcegitcommit: cd66d4f49ea762a31887af2c72d087b219ddbe10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/11/2017
---
# <a name="modules-requiring-license-acceptance"></a><span data-ttu-id="4a7d9-103">Moduly, které vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="4a7d9-103">Modules Requiring License Acceptance</span></span>

## <a name="synopsis"></a><span data-ttu-id="4a7d9-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="4a7d9-104">SYNOPSIS</span></span>
<span data-ttu-id="4a7d9-105">Právní oddělení pro některé zdroje modulu vyžadují, zákazníci musí explicitně přijali licence před instalací jejich modul z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-105">Legal departments for some module publishers require that customers must explicitly accept the license before installing their module from PowerShell Gallery.</span></span> <span data-ttu-id="4a7d9-106">Pokud uživatel nainstaluje, aktualizace nebo uloží modulu pomocí PowerShellGet, zda přímo, nebo jako závislost pro jinou položku, a tento modul vyžaduje, aby uživatel souhlasit s licenci, uživatel musí označovat přijmou licence nebo se operace nezdaří.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-106">If a user installs, updates, or saves a module using PowerShellGet, whether directly or as a dependency for another item, and that module requires the user to agree to a license, the user must indicate they accept the license or the operation fails.</span></span>

## <a name="publish-requirements-for-modules"></a><span data-ttu-id="4a7d9-107">Publikování požadavky pro moduly</span><span class="sxs-lookup"><span data-stu-id="4a7d9-107">Publish Requirements for Modules</span></span>

<span data-ttu-id="4a7d9-108">Moduly, které chcete uživatelé musí přijmout licenční musí splnit následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="4a7d9-108">Modules that would like to require users to accept license should fulfill following requirements:</span></span>
    
- <span data-ttu-id="4a7d9-109">PSData oddíl manifestu modulu musí obsahovat RequireLicenseAcceptance = $True.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-109">PSData section of module manifest should include RequireLicenseAcceptance = $True.</span></span>
- <span data-ttu-id="4a7d9-110">Modul by měly obsahovat license.txt soubor v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-110">Module should contain license.txt file in root directory.</span></span>
- <span data-ttu-id="4a7d9-111">Modul manifestu by měl obsahovat identifikátor Uri licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-111">Module manifest should contain License Uri.</span></span>
- <span data-ttu-id="4a7d9-112">Modul je nutné ji publikovat pomocí PowerShellGet formátu verze 2.0 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-112">Module should be published with PowerShellGet Format Version 2.0 and above.</span></span>

## <a name="impact-on-installsaveupdate-module"></a><span data-ttu-id="4a7d9-113">Dopad na instalaci nebo uložit nebo aktualizace – modul</span><span class="sxs-lookup"><span data-stu-id="4a7d9-113">Impact on Install/Save/Update-Module</span></span>

- <span data-ttu-id="4a7d9-114">Instalovat nebo uložit nebo aktualizovat rutiny bude podporovat nový parametr – AcceptLicense, který se bude chovat, jako by uživatel viděli licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-114">Install/Save/Update cmdlets will support a new parameter –AcceptLicense that will behave as though the user saw the license.</span></span>
- <span data-ttu-id="4a7d9-115">Pokud má hodnotu True, RequiredLicenseAcceptance a není určena – AcceptLicense, uživatel bude vidět license.txt a zobrazí výzva s: &quot;přijímáte tyto licenční podmínky (Ano/Ne/YesToAll/NoToAll)&quot;.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-115">If RequiredLicenseAcceptance is True and –AcceptLicense is not specified, the user will be shown the license.txt, and prompted with: &quot;Do you accept these license terms (Yes/No/YesToAll/NoToAll)&quot;.</span></span>
  - <span data-ttu-id="4a7d9-116">Pokud licence byla přijata.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-116">If the license is accepted</span></span>
    - <span data-ttu-id="4a7d9-117">**Uložit-Module:** modul se zkopírují na uživatele & č. 39; s systému</span><span class="sxs-lookup"><span data-stu-id="4a7d9-117">**Save-Module:** the module will be copied to the user&#39;s system</span></span>
    - <span data-ttu-id="4a7d9-118">**Instalace modulu:** modul se zkopírují na uživatele & č. 39; s systému do správné složky (podle oboru)</span><span class="sxs-lookup"><span data-stu-id="4a7d9-118">**Install-Module:** the module will be copied to the user&#39;s system to the proper folder (based on scope)</span></span>
    - <span data-ttu-id="4a7d9-119">**Aktualizace modulu:** modul bude aktualizován.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-119">**Update-Module:** the module will be updated.</span></span>
  - <span data-ttu-id="4a7d9-120">Pokud bylo odmítnuto, licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-120">If the license is declined.</span></span> 
    - <span data-ttu-id="4a7d9-121">Operace bude zrušena.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-121">Operation will be cancelled.</span></span>
- <span data-ttu-id="4a7d9-122">Všechny rutiny zkontroluje metadata (requireLicenseAcceptance a verze formátu), s upozorněním, že se přijetí licence vyžaduje</span><span class="sxs-lookup"><span data-stu-id="4a7d9-122">All cmdlets will check for the metadata(requireLicenseAcceptance and Format Version) that says a license acceptance is required</span></span>
  - <span data-ttu-id="4a7d9-123">Pokud formát verze klienta je starší než 2.0, operace se nezdaří a požádat uživatele o aktualizaci klienta.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-123">If format version of client is older than 2.0, operation will fail and ask the user to update the client.</span></span>
  - <span data-ttu-id="4a7d9-124">Pokud modul byla publikována s formátu verze starší než 2.0, requireLicenseAcceptance příznak budou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-124">If module was published with format version older than 2.0, requireLicenseAcceptance flag will be ignored.</span></span>

    
 ## <a name="module-dependencies"></a><span data-ttu-id="4a7d9-125">Modul závislosti</span><span class="sxs-lookup"><span data-stu-id="4a7d9-125">Module Dependencies</span></span>
- <span data-ttu-id="4a7d9-126">Během instalace nebo uložit nebo aktualizace se bude vyžadovat operace, pokud modul závisí (něco jiného závisí na modulu) vyžaduje přijetí licence, pak chování přijetí licence (výše).</span><span class="sxs-lookup"><span data-stu-id="4a7d9-126">During Install/Save/Update operation, if a dependent module(something else depends on the module) requires license acceptance, then the license acceptance behavior (above) will be required.</span></span>
- <span data-ttu-id="4a7d9-127">Pokud verze modulu je již uveden v katalogu místní jako nainstalované v systému, by vyřazeno kontrola licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-127">If the module version is already listed in the local catalog as being installed on the system, we would bypass the license checking.</span></span>
- <span data-ttu-id="4a7d9-128">Během instalace nebo uložit nebo aktualizovat operace Pokud modul závisí vyžaduje licenci, a nedojde k přijetí licence, operace se nezdaří a postupovat podle normální procesů pro položku se nepodařilo instalovat nebo uložit nebo aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-128">During Install/Save/Update operation, if a dependent module requires a license, and the license acceptance does not occur, the operation will fail and follow normal processes for the item failed to install/save/update.</span></span>

 ## <a name="impact-on--force"></a><span data-ttu-id="4a7d9-129">Dopad na - Force</span><span class="sxs-lookup"><span data-stu-id="4a7d9-129">Impact on -Force</span></span>

<span data-ttu-id="4a7d9-130">Určení – Force není dostatečná tak, aby přijímal licenci.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-130">Specifying –Force is NOT sufficient to accept a license.</span></span> <span data-ttu-id="4a7d9-131">– AcceptLicense je vyžadována pro oprávnění k instalaci.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-131">–AcceptLicense is required for permission to install.</span></span> <span data-ttu-id="4a7d9-132">Pokud – Force, RequiredLicenseAcceptance má hodnotu True a – AcceptLicense není zadaný, se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-132">If –Force is specified, RequiredLicenseAcceptance is True, and –AcceptLicense is NOT specified, the operation will fail.</span></span>

## <a name="examples"></a><span data-ttu-id="4a7d9-133">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="4a7d9-133">EXAMPLES</span></span>

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a><span data-ttu-id="4a7d9-134">Příklad 1: Aktualizace modulu Manifest vyžadovat přijetí licence</span><span class="sxs-lookup"><span data-stu-id="4a7d9-134">Example 1: Update Module Manifest to require license acceptance</span></span>
```PowerShell
PS C:\> Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance

PrivateData = @{

    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable
    
 } # End of PrivateData hashtable
```
<span data-ttu-id="4a7d9-135">Tento příkaz aktualizuje souboru manifestu a nastavuje příznak RequireLicenseAcceptance na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-135">This command updates the manifest file and sets the RequireLicenseAcceptance flag to true.</span></span>
### <a name="example-2-install-module-requiring-license-acceptance"></a><span data-ttu-id="4a7d9-136">Příklad 2: Instalace modulu vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="4a7d9-136">Example 2: Install Module requiring license acceptance</span></span>
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 

```
<span data-ttu-id="4a7d9-137">Tento příkaz zobrazují informace o licenčních ze souboru license.txt a vyzývá uživatele k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-137">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="4a7d9-138">Příklad 3: Instalace modulu přijetí na vyžadují licence s - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="4a7d9-138">Example 3: Install Module requiring license acceptance with -AcceptLicense</span></span>
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```
<span data-ttu-id="4a7d9-139">Modul je nainstalován bez jakékoli výzvy tak, aby přijímal licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-139">Module is installed without any prompt to accept license.</span></span>

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a><span data-ttu-id="4a7d9-140">Příklad 4: Instalace modulu přijetí na vyžadují licence s parametrem - Force</span><span class="sxs-lookup"><span data-stu-id="4a7d9-140">Example 4: Install Module requiring license acceptance with -Force</span></span>
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance -Force
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="4a7d9-141">Příklad 5: Instalace modulu závislosti, které vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="4a7d9-141">Example 5: Install Module with dependencies requiring license acceptance</span></span>
<span data-ttu-id="4a7d9-142">Modul ModuleWithDependency závisí na modulu 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-142">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="4a7d9-143">Uživatel je vyzván k přijetí licenční.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-143">User is prompted to Accept License.</span></span>
```PowerShell
PS C:\> Install-Module -Name ModuleWithDependency

License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="4a7d9-144">Příklad 6: Instalace modulu se závislostmi vyžadovat přijetí licence a - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="4a7d9-144">Example 6: Install Module with dependencies requiring license acceptance and -AcceptLicense</span></span>
<span data-ttu-id="4a7d9-145">Modul ModuleWithDependency závisí na modulu 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-145">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="4a7d9-146">Uživatel není vyzvání k přijetí licence, jako jsou zadány - AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-146">User is not prompted to accept license as -AcceptLicense is specified.</span></span>
```PowerShell
PS C:\>  Install-Module -Name ModuleWithDependency -AcceptLicense
```
### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a><span data-ttu-id="4a7d9-147">Příklad 7: Instalace modulu nutnosti přijetí licence na klienta starší než PSGetFormatVersion 2.0</span><span class="sxs-lookup"><span data-stu-id="4a7d9-147">Example 7: Install module requiring license acceptance on a client older than PSGetFormatVersion 2.0</span></span>
```PowerShell
PS C:\windows\system32> Install-Module -Name ModuleRequireLicenseAcceptance

WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.

```
### <a name="example-8-save-module-requiring-license-acceptance"></a><span data-ttu-id="4a7d9-148">Příklad 8: Uložit modulu, které vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="4a7d9-148">Example 8: Save Module requiring license acceptance</span></span>
```PowerShell
PS C:\> Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```
<span data-ttu-id="4a7d9-149">Tento příkaz zobrazují informace o licenčních ze souboru license.txt a vyzývá uživatele k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-149">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="4a7d9-150">Příklad 9: Modul nutnosti přijetí licence s - AcceptLicense uložte</span><span class="sxs-lookup"><span data-stu-id="4a7d9-150">Example 9: Save Module requiring license acceptance with -AcceptLicense</span></span>
```PowerShell
PS C:\> Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```
<span data-ttu-id="4a7d9-151">Modul je uložit bez žádné výzva k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-151">Module is saved without any prompt to accept license.</span></span>

### <a name="example-10-update-module-requiring-license-acceptance"></a><span data-ttu-id="4a7d9-152">Příklad 10: Přijetí licence vyžadují aktualizace modulu</span><span class="sxs-lookup"><span data-stu-id="4a7d9-152">Example 10: Update Module requiring license acceptance</span></span>
```PowerShell
PS C:\> Update-Module -Name ModuleRequireLicenseAcceptance

License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): 
```
<span data-ttu-id="4a7d9-153">Tento příkaz zobrazují informace o licenčních ze souboru license.txt a vyzývá uživatele k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-153">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="4a7d9-154">Příklad 11: Aktualizace modulu přijetí na vyžadují licence s - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="4a7d9-154">Example 11: Update Module requiring license acceptance with -AcceptLicense</span></span>
```PowerShell
PS C:\> Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```
<span data-ttu-id="4a7d9-155">Modul se aktualizuje bez jakékoli výzvy tak, aby přijímal licence.</span><span class="sxs-lookup"><span data-stu-id="4a7d9-155">Module is updated without any prompt to accept license.</span></span>

## <a name="more-details"></a><span data-ttu-id="4a7d9-156">Další informace</span><span class="sxs-lookup"><span data-stu-id="4a7d9-156">More details</span></span>
### <a name="require-license-acceptance-for-scriptsscriptscriptrequirelicenseacceptancemd"></a>[<span data-ttu-id="4a7d9-157">Vyžadovat přijetí licence pro skripty</span><span class="sxs-lookup"><span data-stu-id="4a7d9-157">Require License Acceptance for Scripts</span></span>](../script/script_RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[<span data-ttu-id="4a7d9-158">Vyžadovat přijetí licence podporu na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="4a7d9-158">Require License Acceptance support on PowerShellGallery</span></span>](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[<span data-ttu-id="4a7d9-159">Vyžadovat přijetí licence na nasazení do služby Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4a7d9-159">Require License Acceptance on Deploy to Azure Automation</span></span>](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)

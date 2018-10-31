---
ms.date: 06/09/2017
schema: 2.0.0
keywords: prostředí PowerShell
title: Moduly vyžadující přijetí licence
ms.openlocfilehash: 369e32d5278a2e1bf1d3f2ae67f670c524b9f878
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002663"
---
# <a name="modules-requiring-license-acceptance"></a><span data-ttu-id="d8f2a-103">Moduly vyžadující přijetí licence</span><span class="sxs-lookup"><span data-stu-id="d8f2a-103">Modules Requiring License Acceptance</span></span>

## <a name="synopsis"></a><span data-ttu-id="d8f2a-104">SOUHRN</span><span class="sxs-lookup"><span data-stu-id="d8f2a-104">SYNOPSIS</span></span>

<span data-ttu-id="d8f2a-105">Právní oddělení pro některé zdroje modulu vyžadují, aby zákazníci musí explicitně přijměte licenci před instalací jejich modul z Galerie prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-105">Legal departments for some module publishers require that customers must explicitly accept the license before installing their module from PowerShell Gallery.</span></span> <span data-ttu-id="d8f2a-106">Pokud uživatel nainstaluje, aktualizuje nebo uloží modul použití modulu PowerShellGet, ať už přímo, nebo jako závislost jinému balíčku, a tento modul vyžaduje, aby uživatel vyjádření souhlasu s licencí, uživatel musí uvádět, přijměte licenci nebo se operace nezdaří.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-106">If a user installs, updates, or saves a module using PowerShellGet, whether directly or as a dependency for another package, and that module requires the user to agree to a license, the user must indicate they accept the license or the operation fails.</span></span>

## <a name="publish-requirements-for-modules"></a><span data-ttu-id="d8f2a-107">Publikování požadavky pro moduly</span><span class="sxs-lookup"><span data-stu-id="d8f2a-107">Publish Requirements for Modules</span></span>

<span data-ttu-id="d8f2a-108">Moduly, které chcete vyžadovat, aby uživatelé přijměte licenci na by měl splňovat následující požadavky:</span><span class="sxs-lookup"><span data-stu-id="d8f2a-108">Modules that would like to require users to accept license should fulfill following requirements:</span></span>

- <span data-ttu-id="d8f2a-109">PSData části manifestu modulu by měl obsahovat RequireLicenseAcceptance = $True.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-109">PSData section of module manifest should include RequireLicenseAcceptance = $True.</span></span>
- <span data-ttu-id="d8f2a-110">Modul by měl obsahovat soubor license.txt v kořenovém adresáři.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-110">Module should contain license.txt file in root directory.</span></span>
- <span data-ttu-id="d8f2a-111">Manifestu modulu musí obsahovat identifikátor Uri licence.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-111">Module manifest should contain License Uri.</span></span>
- <span data-ttu-id="d8f2a-112">Modul by se měly zveřejňovat pomocí Správce balíčků PowerShellGet formát verze 2.0 a vyšší.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-112">Module should be published with PowerShellGet Format Version 2.0 and above.</span></span>

## <a name="impact-on-installsaveupdate-module"></a><span data-ttu-id="d8f2a-113">Dopad na instalaci/Save/Update-Module</span><span class="sxs-lookup"><span data-stu-id="d8f2a-113">Impact on Install/Save/Update-Module</span></span>

- <span data-ttu-id="d8f2a-114">Instalace/Save/aktualizace rutin bude podporovat nový parametr – AcceptLicense, jako by uživatel viděli licence, které se bude chovat.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-114">Install/Save/Update cmdlets will support a new parameter –AcceptLicense that will behave as though the user saw the license.</span></span>
- <span data-ttu-id="d8f2a-115">Pokud RequiredLicenseAcceptance má hodnotu True a není určena – AcceptLicense, uživateli se zobrazí license.txt a zobrazí výzva s: &quot;přijímáte tyto licenční podmínky (Ano/Ne/YesToAll/NoToAll)&quot;.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-115">If RequiredLicenseAcceptance is True and –AcceptLicense is not specified, the user will be shown the license.txt, and prompted with: &quot;Do you accept these license terms (Yes/No/YesToAll/NoToAll)&quot;.</span></span>
  - <span data-ttu-id="d8f2a-116">Pokud je přijetí licence</span><span class="sxs-lookup"><span data-stu-id="d8f2a-116">If the license is accepted</span></span>
    - <span data-ttu-id="d8f2a-117">**Save-Module:** modul bude zkopírován do uživatel&#39;s systému</span><span class="sxs-lookup"><span data-stu-id="d8f2a-117">**Save-Module:** the module will be copied to the user&#39;s system</span></span>
    - <span data-ttu-id="d8f2a-118">**Install-Module:** modul bude zkopírován do uživatel&#39;systému s do správné složky (podle rozsahu)</span><span class="sxs-lookup"><span data-stu-id="d8f2a-118">**Install-Module:** the module will be copied to the user&#39;s system to the proper folder (based on scope)</span></span>
    - <span data-ttu-id="d8f2a-119">**Update-Module:** modul bude aktualizován.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-119">**Update-Module:** the module will be updated.</span></span>
  - <span data-ttu-id="d8f2a-120">Pokud licence, které bylo odmítnuto.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-120">If the license is declined.</span></span>
    - <span data-ttu-id="d8f2a-121">Operace se zrušila.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-121">Operation will be cancelled.</span></span>
    - <span data-ttu-id="d8f2a-122">Všechny rutiny bude vyhledávat metadata (requireLicenseAcceptance a verzi formátu), která uvádí, že je vyžadováno přijetí licence</span><span class="sxs-lookup"><span data-stu-id="d8f2a-122">All cmdlets will check for the metadata(requireLicenseAcceptance and Format Version) that says a license acceptance is required</span></span>
    - <span data-ttu-id="d8f2a-123">Pokud formát verze klienta je starší než 2.0, operace se nezdaří a požádat uživatele, aby také aktualizovat klienta sady.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-123">If format version of client is older than 2.0, operation will fail and ask the user to update the client.</span></span>
    - <span data-ttu-id="d8f2a-124">Pokud modul byl publikován s formát verze starší než 2.0, requireLicenseAcceptance příznak se bude ignorovat.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-124">If module was published with format version older than 2.0, requireLicenseAcceptance flag will be ignored.</span></span>

## <a name="module-dependencies"></a><span data-ttu-id="d8f2a-125">Závislostí modulů</span><span class="sxs-lookup"><span data-stu-id="d8f2a-125">Module Dependencies</span></span>

- <span data-ttu-id="d8f2a-126">Během instalace/Save/aktualizace se bude vyžadovat operace, pokud modul závisí (něco jiného závisí na modul) vyžaduje souhlas s podmínkami licence, pak chování přijetí licence (viz výše).</span><span class="sxs-lookup"><span data-stu-id="d8f2a-126">During Install/Save/Update operation, if a dependent module(something else depends on the module) requires license acceptance, then the license acceptance behavior (above) will be required.</span></span>
- <span data-ttu-id="d8f2a-127">Pokud verze modulu je již uveden v místního katalogu jako nainstalované v systému, jsme by obejít kontrolu licence.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-127">If the module version is already listed in the local catalog as being installed on the system, we would bypass the license checking.</span></span>
- <span data-ttu-id="d8f2a-128">Během instalace/uložit nebo aktualizovat Pokud závislé modul musí mít licenci, a nedojde k přijetí licence, operace se nezdaří a postupujte podle běžných procesů pro balíček se nepodařilo nainstalovat nebo uložit nebo aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-128">During Install/Save/Update operation, if a dependent module requires a license, and the license acceptance does not occur, the operation will fail and follow normal processes for the package failed to install/save/update.</span></span>

## <a name="impact-on--force"></a><span data-ttu-id="d8f2a-129">Dopad na - Force</span><span class="sxs-lookup"><span data-stu-id="d8f2a-129">Impact on -Force</span></span>

<span data-ttu-id="d8f2a-130">Určení `–Force` není dostatečná k přijměte licenci.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-130">Specifying `–Force` is NOT sufficient to accept a license.</span></span> <span data-ttu-id="d8f2a-131">`–AcceptLicense` je vyžadován pro oprávnění k instalaci.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-131">`–AcceptLicense` is required for permission to install.</span></span> <span data-ttu-id="d8f2a-132">Pokud `–Force` určena RequiredLicenseAcceptance má hodnotu True, a `–AcceptLicense` není zadán, operace se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-132">If `–Force` is specified, RequiredLicenseAcceptance is True, and `–AcceptLicense` is NOT specified, the operation will fail.</span></span>

## <a name="examples"></a><span data-ttu-id="d8f2a-133">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="d8f2a-133">EXAMPLES</span></span>

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a><span data-ttu-id="d8f2a-134">Příklad 1: Aktualizace modulu Manifest k vyžadování přijetí licence</span><span class="sxs-lookup"><span data-stu-id="d8f2a-134">Example 1: Update Module Manifest to require license acceptance</span></span>

```powershell
Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance -PrivateData @{
    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable

 } # End of PrivateData hashtable
```

<span data-ttu-id="d8f2a-135">Tento příkaz aktualizuje soubor manifestu a nastaví příznak RequireLicenseAcceptance na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-135">This command updates the manifest file and sets the RequireLicenseAcceptance flag to true.</span></span>

### <a name="example-2-install-module-requiring-license-acceptance"></a><span data-ttu-id="d8f2a-136">Příklad 2: Instalace modulu vyžadování přijetí licence</span><span class="sxs-lookup"><span data-stu-id="d8f2a-136">Example 2: Install Module requiring license acceptance</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```output
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

<span data-ttu-id="d8f2a-137">Tento příkaz zobrazí licenci ze souboru license.txt a vyzve uživatele k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-137">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="d8f2a-138">Příklad 3: Instalace modulu vyžaduje souhlas s podmínkami licence s - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="d8f2a-138">Example 3: Install Module requiring license acceptance with -AcceptLicense</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

<span data-ttu-id="d8f2a-139">Modul se nainstaluje bez libovolného řádku přijměte licenci.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-139">Module is installed without any prompt to accept license.</span></span>

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a><span data-ttu-id="d8f2a-140">Příklad 4: Instalace modulu vyžaduje souhlas s podmínkami licence s parametrem - Force</span><span class="sxs-lookup"><span data-stu-id="d8f2a-140">Example 4: Install Module requiring license acceptance with -Force</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -Force
```

```output
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="d8f2a-141">Příklad 5: Instalace modulu se závislostmi vyžadující přijetí licence</span><span class="sxs-lookup"><span data-stu-id="d8f2a-141">Example 5: Install Module with dependencies requiring license acceptance</span></span>

<span data-ttu-id="d8f2a-142">Modul ModuleWithDependency závisí na modulu "ModuleRequireLicenseAcceptance".</span><span class="sxs-lookup"><span data-stu-id="d8f2a-142">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="d8f2a-143">Uživatel je vyzván k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-143">User is prompted to Accept License.</span></span>

```powershell
Install-Module -Name ModuleWithDependency
```

```output
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

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="d8f2a-144">Příklad 6: Instalace modulu se závislostmi vyžadování přijetí licence a - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="d8f2a-144">Example 6: Install Module with dependencies requiring license acceptance and -AcceptLicense</span></span>

<span data-ttu-id="d8f2a-145">Modul ModuleWithDependency závisí na modulu "ModuleRequireLicenseAcceptance".</span><span class="sxs-lookup"><span data-stu-id="d8f2a-145">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="d8f2a-146">Uživatel není vyzván k uvedené - AcceptLicense přijměte licenci.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-146">User is not prompted to accept license as -AcceptLicense is specified.</span></span>

```powershell
Install-Module -Name ModuleWithDependency -AcceptLicense
```

### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a><span data-ttu-id="d8f2a-147">Příklad 7: Instalace modulu vyžadující přijetí licence u klienta starší než PSGetFormatVersion 2.0</span><span class="sxs-lookup"><span data-stu-id="d8f2a-147">Example 7: Install module requiring license acceptance on a client older than PSGetFormatVersion 2.0</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```output
WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.
```

### <a name="example-8-save-module-requiring-license-acceptance"></a><span data-ttu-id="d8f2a-148">Příklad 8: Modul vyžadující přijetí licence uložit</span><span class="sxs-lookup"><span data-stu-id="d8f2a-148">Example 8: Save Module requiring license acceptance</span></span>

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved
```

```output
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

<span data-ttu-id="d8f2a-149">Tento příkaz zobrazí licenci ze souboru license.txt a vyzve uživatele k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-149">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="d8f2a-150">Příklad 9: Modul vyžadující přijetí licence s - AcceptLicense uložte</span><span class="sxs-lookup"><span data-stu-id="d8f2a-150">Example 9: Save Module requiring license acceptance with -AcceptLicense</span></span>

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```

<span data-ttu-id="d8f2a-151">Modul se uloží bez jakékoli výzvy přijměte licenci.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-151">Module is saved without any prompt to accept license.</span></span>

### <a name="example-10-update-module-requiring-license-acceptance"></a><span data-ttu-id="d8f2a-152">Příklad 10: Aktualizace modulu vyžadování přijetí licence</span><span class="sxs-lookup"><span data-stu-id="d8f2a-152">Example 10: Update Module requiring license acceptance</span></span>

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance
```

```output
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

<span data-ttu-id="d8f2a-153">Tento příkaz zobrazí licenci ze souboru license.txt a vyzve uživatele k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-153">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="d8f2a-154">Příklad 11: Modul aktualizace vyžadující souhlas s podmínkami licence s - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="d8f2a-154">Example 11: Update Module requiring license acceptance with -AcceptLicense</span></span>

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

<span data-ttu-id="d8f2a-155">Modul se aktualizuje bez jakékoli výzvy přijměte licenci.</span><span class="sxs-lookup"><span data-stu-id="d8f2a-155">Module is updated without any prompt to accept license.</span></span>

## <a name="more-details"></a><span data-ttu-id="d8f2a-156">Další podrobnosti</span><span class="sxs-lookup"><span data-stu-id="d8f2a-156">More details</span></span>

[<span data-ttu-id="d8f2a-157">Vyžadování přijetí licence u skriptů</span><span class="sxs-lookup"><span data-stu-id="d8f2a-157">Require License Acceptance for Scripts</span></span>](./script-license-acceptance.md)

[<span data-ttu-id="d8f2a-158">Vyžadovat přijetí licence podpory na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="d8f2a-158">Require License Acceptance support on PowerShellGallery</span></span>](../how-to/working-with-packages/packages-that-require-license-acceptance.md)

[<span data-ttu-id="d8f2a-159">Vyžadování přijetí licence při nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="d8f2a-159">Require License Acceptance on Deploy to Azure Automation</span></span>](../how-to/working-with-packages/deploy-to-azure-automation.md)

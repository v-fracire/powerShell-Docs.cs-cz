---
ms.date: 06/09/2017
schema: 2.0.0
keywords: Prostředí PowerShell
title: Moduly vyžadující přijetí licence
ms.openlocfilehash: fe197ea271e18580a221ad4d5245b685bd81775b
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="modules-requiring-license-acceptance"></a>Moduly vyžadující přijetí licence

## <a name="synopsis"></a>STRUČNÝ OBSAH

Právní oddělení pro některé zdroje modulu vyžadují, zákazníci musí explicitně přijali licence před instalací jejich modul z Galerie prostředí PowerShell. Pokud uživatel nainstaluje, aktualizace nebo uloží modulu pomocí PowerShellGet, zda přímo, nebo jako závislost pro jinou položku, a tento modul vyžaduje, aby uživatel souhlasit s licenci, uživatel musí označovat přijmou licence nebo se operace nezdaří.

## <a name="publish-requirements-for-modules"></a>Publikování požadavky pro moduly

Moduly, které chcete uživatelé musí přijmout licenční musí splnit následující požadavky:

- PSData oddíl manifestu modulu musí obsahovat RequireLicenseAcceptance = $True.
- Modul by měly obsahovat license.txt soubor v kořenovém adresáři.
- Modul manifestu by měl obsahovat identifikátor Uri licence.
- Modul je nutné ji publikovat pomocí PowerShellGet formátu verze 2.0 a vyšší.

## <a name="impact-on-installsaveupdate-module"></a>Dopad na instalaci nebo uložit nebo aktualizace – modul

- Instalovat nebo uložit nebo aktualizovat rutiny bude podporovat nový parametr – AcceptLicense, který se bude chovat, jako by uživatel viděli licence.
- Pokud má hodnotu True, RequiredLicenseAcceptance a není určena – AcceptLicense, uživatel bude vidět license.txt a zobrazí výzva s: &quot;přijímáte tyto licenční podmínky (Ano/Ne/YesToAll/NoToAll)&quot;.
  - Pokud licence byla přijata.
    - **Uložit-Module:** modul se zkopírují na uživatele&#39;s systému
    - **Instalace modulu:** modul se zkopírují na uživatele&#39;s systému do správné složky (podle oboru)
    - **Aktualizace modulu:** modul bude aktualizován.
  - Pokud bylo odmítnuto, licence.
    - Operace bude zrušena.
- Všechny rutiny zkontroluje metadata (requireLicenseAcceptance a verze formátu), s upozorněním, že se přijetí licence vyžaduje
  - Pokud formát verze klienta je starší než 2.0, operace se nezdaří a požádat uživatele o aktualizaci klienta.
  - Pokud modul byla publikována s formátu verze starší než 2.0, requireLicenseAcceptance příznak budou ignorovány.


 ## <a name="module-dependencies"></a>Modul závislosti
- Během instalace nebo uložit nebo aktualizace se bude vyžadovat operace, pokud modul závisí (něco jiného závisí na modulu) vyžaduje přijetí licence, pak chování přijetí licence (výše).
- Pokud verze modulu je již uveden v katalogu místní jako nainstalované v systému, by vyřazeno kontrola licence.
- Během instalace nebo uložit nebo aktualizovat operace Pokud modul závisí vyžaduje licenci, a nedojde k přijetí licence, operace se nezdaří a postupovat podle normální procesů pro položku se nepodařilo instalovat nebo uložit nebo aktualizovat.

 ## <a name="impact-on--force"></a>Dopad na - Force

Určení – Force není dostatečná tak, aby přijímal licenci. – AcceptLicense je vyžadována pro oprávnění k instalaci. Pokud – Force, RequiredLicenseAcceptance má hodnotu True a – AcceptLicense není zadaný, se nezdaří.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a>Příklad 1: Aktualizace modulu Manifest vyžadovat přijetí licence

```PowerShell
PS> Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance

PrivateData = @{

    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable

 } # End of PrivateData hashtable
```

Tento příkaz aktualizuje souboru manifestu a nastavuje příznak RequireLicenseAcceptance na hodnotu true.

### <a name="example-2-install-module-requiring-license-acceptance"></a>Příklad 2: Instalace modulu vyžadují přijetí licence

```PowerShell
PS> Install-Module -Name ModuleRequireLicenseAcceptance

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

Tento příkaz zobrazují informace o licenčních ze souboru license.txt a vyzývá uživatele k přijetí licence.

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a>Příklad 3: Instalace modulu přijetí na vyžadují licence s - AcceptLicense

```PowerShell
PS> Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

Modul je nainstalován bez jakékoli výzvy tak, aby přijímal licence.

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a>Příklad 4: Instalace modulu přijetí na vyžadují licence s parametrem - Force

```PowerShell
PS> Install-Module -Name ModuleRequireLicenseAcceptance -Force
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a>Příklad 5: Instalace modulu závislosti, které vyžadují přijetí licence

Modul ModuleWithDependency závisí na modulu 'ModuleRequireLicenseAcceptance'. Uživatel je vyzván k přijetí licenční.

```PowerShell
PS> Install-Module -Name ModuleWithDependency

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

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Příklad 6: Instalace modulu se závislostmi vyžadovat přijetí licence a - AcceptLicense

Modul ModuleWithDependency závisí na modulu 'ModuleRequireLicenseAcceptance'. Uživatel není vyzvání k přijetí licence, jako jsou zadány - AcceptLicense.

```PowerShell
PS>  Install-Module -Name ModuleWithDependency -AcceptLicense
```

### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a>Příklad 7: Instalace modulu nutnosti přijetí licence na klienta starší než PSGetFormatVersion 2.0

```PowerShell
PS C:\windows\system32> Install-Module -Name ModuleRequireLicenseAcceptance

WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.

```

### <a name="example-8-save-module-requiring-license-acceptance"></a>Příklad 8: Uložit modulu, které vyžadují přijetí licence

```PowerShell
PS> Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved

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

Tento příkaz zobrazují informace o licenčních ze souboru license.txt a vyzývá uživatele k přijetí licence.

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a>Příklad 9: Modul nutnosti přijetí licence s - AcceptLicense uložte

```PowerShell
PS> Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```

Modul je uložit bez žádné výzva k přijetí licence.

### <a name="example-10-update-module-requiring-license-acceptance"></a>Příklad 10: Přijetí licence vyžadují aktualizace modulu

```PowerShell
PS> Update-Module -Name ModuleRequireLicenseAcceptance

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

Tento příkaz zobrazují informace o licenčních ze souboru license.txt a vyzývá uživatele k přijetí licence.

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a>Příklad 11: Aktualizace modulu přijetí na vyžadují licence s - AcceptLicense

```PowerShell
PS> Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

Modul se aktualizuje bez jakékoli výzvy tak, aby přijímal licence.

## <a name="more-details"></a>Další informace

### <a name="require-license-acceptance-for-scriptsscript-license-acceptancemd"></a>[Vyžadování přijetí licence u skriptů](./script-license-acceptance.md)

### <a name="require-license-acceptance-support-on-powershellgalleryhow-toworking-with-itemsitems-that-require-license-acceptancemd"></a>[Vyžadovat přijetí licence podporu na PowerShellGallery](../how-to/working-with-items/items-that-require-license-acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationhow-toworking-with-itemsdeploy-to-azure-automationmd"></a>[Vyžadování přijetí licence při nasazení ve službě Azure Automation](../how-to/working-with-items/deploy-to-azure-automation.md)
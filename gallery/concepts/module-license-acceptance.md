---
ms.date: 06/09/2017
schema: 2.0.0
keywords: prostředí PowerShell
title: Moduly vyžadující přijetí licence
ms.openlocfilehash: 93f92f6e83bcf18a40c3d89eb39a154e16ca5063
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893106"
---
# <a name="modules-requiring-license-acceptance"></a>Moduly vyžadující přijetí licence

## <a name="synopsis"></a>SOUHRN

Právní oddělení pro některé zdroje modulu vyžadují, aby zákazníci musí explicitně přijměte licenci před instalací jejich modul z Galerie prostředí PowerShell. Pokud uživatel nainstaluje, aktualizuje nebo uloží modul použití modulu PowerShellGet, ať už přímo, nebo jako závislost pro jinou položku, a tento modul vyžaduje, aby uživatel vyjádření souhlasu s licencí, uživatel musí uvádět, přijměte licenci nebo se operace nezdaří.

## <a name="publish-requirements-for-modules"></a>Publikování požadavky pro moduly

Moduly, které chcete vyžadovat, aby uživatelé přijměte licenci na by měl splňovat následující požadavky:

- PSData části manifestu modulu by měl obsahovat RequireLicenseAcceptance = $True.
- Modul by měl obsahovat soubor license.txt v kořenovém adresáři.
- Manifestu modulu musí obsahovat identifikátor Uri licence.
- Modul by se měly zveřejňovat pomocí Správce balíčků PowerShellGet formát verze 2.0 a vyšší.

## <a name="impact-on-installsaveupdate-module"></a>Dopad na instalaci/Save/Update-Module

- Instalace/Save/aktualizace rutin bude podporovat nový parametr – AcceptLicense, jako by uživatel viděli licence, které se bude chovat.
- Pokud RequiredLicenseAcceptance má hodnotu True a není určena – AcceptLicense, uživateli se zobrazí license.txt a zobrazí výzva s: &quot;přijímáte tyto licenční podmínky (Ano/Ne/YesToAll/NoToAll)&quot;.
  - Pokud je přijetí licence
    - **Save-Module:** modul bude zkopírován do uživatel&#39;s systému
    - **Install-Module:** modul bude zkopírován do uživatel&#39;systému s do správné složky (podle rozsahu)
    - **Update-Module:** modul bude aktualizován.
  - Pokud licence, které bylo odmítnuto.
    - Operace se zrušila.
    - Všechny rutiny bude vyhledávat metadata (requireLicenseAcceptance a verzi formátu), která uvádí, že je vyžadováno přijetí licence
    - Pokud formát verze klienta je starší než 2.0, operace se nezdaří a požádat uživatele, aby také aktualizovat klienta sady.
    - Pokud modul byl publikován s formát verze starší než 2.0, requireLicenseAcceptance příznak se bude ignorovat.

## <a name="module-dependencies"></a>Závislostí modulů

- Během instalace/Save/aktualizace se bude vyžadovat operace, pokud modul závisí (něco jiného závisí na modul) vyžaduje souhlas s podmínkami licence, pak chování přijetí licence (viz výše).
- Pokud verze modulu je již uveden v místního katalogu jako nainstalované v systému, jsme by obejít kontrolu licence.
- Během instalace/uložit nebo aktualizovat Pokud závislé modul musí mít licenci, a nedojde k přijetí licence, operace se nezdaří a postupujte podle běžných procesů pro položku se nepodařilo nainstalovat nebo uložit nebo aktualizovat.

## <a name="impact-on--force"></a>Dopad na - Force

Určení `–Force` není dostatečná k přijměte licenci. `–AcceptLicense` je vyžadován pro oprávnění k instalaci. Pokud `–Force` určena RequiredLicenseAcceptance má hodnotu True, a `–AcceptLicense` není zadán, operace se nezdaří.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a>Příklad 1: Aktualizace modulu Manifest k vyžadování přijetí licence

```powershell
Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance -PrivateData @{
    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable

 } # End of PrivateData hashtable
```

Tento příkaz aktualizuje soubor manifestu a nastaví příznak RequireLicenseAcceptance na hodnotu true.

### <a name="example-2-install-module-requiring-license-acceptance"></a>Příklad 2: Instalace modulu vyžadování přijetí licence

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

Tento příkaz zobrazí licenci ze souboru license.txt a vyzve uživatele k přijetí licence.

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a>Příklad 3: Instalace modulu vyžaduje souhlas s podmínkami licence s - AcceptLicense

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

Modul se nainstaluje bez libovolného řádku přijměte licenci.

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a>Příklad 4: Instalace modulu vyžaduje souhlas s podmínkami licence s parametrem - Force

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

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a>Příklad 5: Instalace modulu se závislostmi vyžadující přijetí licence

Modul ModuleWithDependency závisí na modulu "ModuleRequireLicenseAcceptance". Uživatel je vyzván k přijetí licence.

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

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Příklad 6: Instalace modulu se závislostmi vyžadování přijetí licence a - AcceptLicense

Modul ModuleWithDependency závisí na modulu "ModuleRequireLicenseAcceptance". Uživatel není vyzván k uvedené - AcceptLicense přijměte licenci.

```powershell
Install-Module -Name ModuleWithDependency -AcceptLicense
```

### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a>Příklad 7: Instalace modulu vyžadující přijetí licence u klienta starší než PSGetFormatVersion 2.0

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```output
WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.
```

### <a name="example-8-save-module-requiring-license-acceptance"></a>Příklad 8: Modul vyžadující přijetí licence uložit

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

Tento příkaz zobrazí licenci ze souboru license.txt a vyzve uživatele k přijetí licence.

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a>Příklad 9: Modul vyžadující přijetí licence s - AcceptLicense uložte

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```

Modul se uloží bez jakékoli výzvy přijměte licenci.

### <a name="example-10-update-module-requiring-license-acceptance"></a>Příklad 10: Aktualizace modulu vyžadování přijetí licence

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

Tento příkaz zobrazí licenci ze souboru license.txt a vyzve uživatele k přijetí licence.

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a>Příklad 11: Modul aktualizace vyžadující souhlas s podmínkami licence s - AcceptLicense

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

Modul se aktualizuje bez jakékoli výzvy přijměte licenci.

## <a name="more-details"></a>Další podrobnosti

[Vyžadování přijetí licence u skriptů](./script-license-acceptance.md)

[Vyžadovat přijetí licence podpory na PowerShellGallery](../how-to/working-with-items/items-that-require-license-acceptance.md)

[Vyžadování přijetí licence při nasazení ve službě Azure Automation](../how-to/working-with-items/deploy-to-azure-automation.md)
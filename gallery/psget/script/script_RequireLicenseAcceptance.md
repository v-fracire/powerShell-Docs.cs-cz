---
ms.date: 06/09/2017
schema: 2.0.0
keywords: Prostředí PowerShell
title: RequireLicenseAcceptanceScript
ms.openlocfilehash: 4a2dc39c2b6c380fb4ca94f9fd071ed9cdb35049
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="requiring-license-acceptance-for-scripts"></a>Pro skripty, které vyžadují přijetí licence

Přijetí licence není podporována pro skripty. Ale pokud skript závisí na modul, který vyžaduje přijetí licence je podporován.

Skript commands(Install-Script/Save-Script/Update-Script) podporují nový parametr - AcceptLicense, který se chová, jako by uživatel viděli licence. Pokud není zadán - AcceptLicense; Uživatel se zobrazí license.txt pro závislé modul a vyzvání k přijetí licence.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>Příklad 1: Instalační skript se závislostmi, které vyžadují přijetí licence
Skript ScriptRequireLicenseAcceptance závisí na modulu 'ModuleRequireLicenseAcceptance'. Uživatel je vyzván k přijetí licenční.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Příklad 2: Instalační skript se závislostmi vyžadovat přijetí licence a - AcceptLicense
Skript ScriptRequireLicenseAcceptance závisí na modulu 'ModuleRequireLicenseAcceptance'. Uživatel není vyzvání k přijetí licence, jako jsou zadány - AcceptLicense.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>Další informace
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[Vyžadovat přijetí licence podporu pro moduly](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[Vyžadovat přijetí licence podporu na PowerShellGallery](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[Vyžadování přijetí licence při nasazení ve službě Azure Automation](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)
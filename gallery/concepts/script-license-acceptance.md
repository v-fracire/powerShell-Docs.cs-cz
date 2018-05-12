---
ms.date: 06/09/2017
schema: 2.0.0
keywords: Prostředí PowerShell
title: Pro skripty, které vyžadují přijetí licence
ms.openlocfilehash: 6374c8c8536dd0c8f27580a5b8895b8db18424f9
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="requiring-license-acceptance-for-scripts"></a>Pro skripty, které vyžadují přijetí licence

Přijetí licence není podporována pro skripty. Ale pokud skript závisí na modul, který vyžaduje přijetí licence je podporován.

Skript commands(Install-Script/Save-Script/Update-Script) podporují nový parametr - AcceptLicense, který se chová, jako by uživatel viděli licence. Pokud není zadán - AcceptLicense; Uživatel se zobrazí license.txt pro závislé modul a vyzvání k přijetí licence.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>Příklad 1: Instalační skript se závislostmi, které vyžadují přijetí licence

Skript ScriptRequireLicenseAcceptance závisí na modulu 'ModuleRequireLicenseAcceptance'. Uživatel je vyzván k přijetí licenční.

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance

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
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>Další informace

- [Vyžadovat přijetí licence podporu pro moduly](module-license-acceptance.md)
- [Vyžadovat přijetí licence podporu na PowerShellGallery](../how-to/working-with-items/items-that-require-license-acceptance.md)
- [Vyžadování přijetí licence při nasazení ve službě Azure Automation](../how-to/working-with-items/deploy-to-azure-automation.md)
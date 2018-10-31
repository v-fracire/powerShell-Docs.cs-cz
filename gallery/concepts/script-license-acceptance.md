---
ms.date: 06/09/2017
schema: 2.0.0
keywords: prostředí PowerShell
title: Vyžadování přijetí licence u skriptů
ms.openlocfilehash: e7101eb6a480dd87965b7b9be9d49583042b603f
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002578"
---
# <a name="requiring-license-acceptance-for-scripts"></a>Vyžadování přijetí licence u skriptů

Přijetí licence u skriptů nepodporuje. Scénář, ve kterém se skript závisí na modul, který vyžaduje souhlas s podmínkami licence je však podporováno.

Skript commands(Install-Script/Save-Script/Update-Script) podporují nový parametr - AcceptLicense, který se chová jako by uživatel viděli licence. Pokud není zadán - AcceptLicense; Uživatel se zobrazí license.txt závislé modulu a vyzván k přijetí licence.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>Příklad 1: Instalační skript se závislostmi vyžadující přijetí licence

Skript ScriptRequireLicenseAcceptance závisí na modulu "ModuleRequireLicenseAcceptance". Uživatel je vyzván k přijetí licence.

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>Příklad 2: Instalační skript se závislostmi vyžadování přijetí licence a - AcceptLicense

Skript ScriptRequireLicenseAcceptance závisí na modulu "ModuleRequireLicenseAcceptance". Uživatel není vyzván k uvedené - AcceptLicense přijměte licenci.

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>Další podrobnosti

- [Vyžadovat přijetí licence podporu pro moduly](module-license-acceptance.md)
- [Vyžadovat přijetí licence podpory na PowerShellGallery](../how-to/working-with-packages/packages-that-require-license-acceptance.md)
- [Vyžadování přijetí licence při nasazení ve službě Azure Automation](../how-to/working-with-packages/deploy-to-azure-automation.md)

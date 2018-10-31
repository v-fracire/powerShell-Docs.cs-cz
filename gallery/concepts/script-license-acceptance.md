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
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="b9c1e-103">Vyžadování přijetí licence u skriptů</span><span class="sxs-lookup"><span data-stu-id="b9c1e-103">Requiring license acceptance for scripts</span></span>

<span data-ttu-id="b9c1e-104">Přijetí licence u skriptů nepodporuje.</span><span class="sxs-lookup"><span data-stu-id="b9c1e-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="b9c1e-105">Scénář, ve kterém se skript závisí na modul, který vyžaduje souhlas s podmínkami licence je však podporováno.</span><span class="sxs-lookup"><span data-stu-id="b9c1e-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="b9c1e-106">Skript commands(Install-Script/Save-Script/Update-Script) podporují nový parametr - AcceptLicense, který se chová jako by uživatel viděli licence.</span><span class="sxs-lookup"><span data-stu-id="b9c1e-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="b9c1e-107">Pokud není zadán - AcceptLicense; Uživatel se zobrazí license.txt závislé modulu a vyzván k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="b9c1e-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="b9c1e-108">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="b9c1e-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="b9c1e-109">Příklad 1: Instalační skript se závislostmi vyžadující přijetí licence</span><span class="sxs-lookup"><span data-stu-id="b9c1e-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>

<span data-ttu-id="b9c1e-110">Skript ScriptRequireLicenseAcceptance závisí na modulu "ModuleRequireLicenseAcceptance".</span><span class="sxs-lookup"><span data-stu-id="b9c1e-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="b9c1e-111">Uživatel je vyzván k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="b9c1e-111">User is prompted to Accept License.</span></span>

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="b9c1e-112">Příklad 2: Instalační skript se závislostmi vyžadování přijetí licence a - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="b9c1e-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>

<span data-ttu-id="b9c1e-113">Skript ScriptRequireLicenseAcceptance závisí na modulu "ModuleRequireLicenseAcceptance".</span><span class="sxs-lookup"><span data-stu-id="b9c1e-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="b9c1e-114">Uživatel není vyzván k uvedené - AcceptLicense přijměte licenci.</span><span class="sxs-lookup"><span data-stu-id="b9c1e-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="b9c1e-115">Další podrobnosti</span><span class="sxs-lookup"><span data-stu-id="b9c1e-115">More details</span></span>

- [<span data-ttu-id="b9c1e-116">Vyžadovat přijetí licence podporu pro moduly</span><span class="sxs-lookup"><span data-stu-id="b9c1e-116">Require License Acceptance support for Modules</span></span>](module-license-acceptance.md)
- [<span data-ttu-id="b9c1e-117">Vyžadovat přijetí licence podpory na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="b9c1e-117">Require License Acceptance support on PowerShellGallery</span></span>](../how-to/working-with-packages/packages-that-require-license-acceptance.md)
- [<span data-ttu-id="b9c1e-118">Vyžadování přijetí licence při nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b9c1e-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../how-to/working-with-packages/deploy-to-azure-automation.md)

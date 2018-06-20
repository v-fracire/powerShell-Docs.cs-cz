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
ms.locfileid: "34048754"
---
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="7d521-103">Pro skripty, které vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="7d521-103">Requiring license acceptance for scripts</span></span>

<span data-ttu-id="7d521-104">Přijetí licence není podporována pro skripty.</span><span class="sxs-lookup"><span data-stu-id="7d521-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="7d521-105">Ale pokud skript závisí na modul, který vyžaduje přijetí licence je podporován.</span><span class="sxs-lookup"><span data-stu-id="7d521-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="7d521-106">Skript commands(Install-Script/Save-Script/Update-Script) podporují nový parametr - AcceptLicense, který se chová, jako by uživatel viděli licence.</span><span class="sxs-lookup"><span data-stu-id="7d521-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="7d521-107">Pokud není zadán - AcceptLicense; Uživatel se zobrazí license.txt pro závislé modul a vyzvání k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="7d521-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="7d521-108">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="7d521-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="7d521-109">Příklad 1: Instalační skript se závislostmi, které vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="7d521-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>

<span data-ttu-id="7d521-110">Skript ScriptRequireLicenseAcceptance závisí na modulu 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="7d521-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="7d521-111">Uživatel je vyzván k přijetí licenční.</span><span class="sxs-lookup"><span data-stu-id="7d521-111">User is prompted to Accept License.</span></span>

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="7d521-112">Příklad 2: Instalační skript se závislostmi vyžadovat přijetí licence a - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="7d521-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>

<span data-ttu-id="7d521-113">Skript ScriptRequireLicenseAcceptance závisí na modulu 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="7d521-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="7d521-114">Uživatel není vyzvání k přijetí licence, jako jsou zadány - AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="7d521-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="7d521-115">Další informace</span><span class="sxs-lookup"><span data-stu-id="7d521-115">More details</span></span>

- [<span data-ttu-id="7d521-116">Vyžadovat přijetí licence podporu pro moduly</span><span class="sxs-lookup"><span data-stu-id="7d521-116">Require License Acceptance support for Modules</span></span>](module-license-acceptance.md)
- [<span data-ttu-id="7d521-117">Vyžadovat přijetí licence podporu na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="7d521-117">Require License Acceptance support on PowerShellGallery</span></span>](../how-to/working-with-items/items-that-require-license-acceptance.md)
- [<span data-ttu-id="7d521-118">Vyžadování přijetí licence při nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7d521-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../how-to/working-with-items/deploy-to-azure-automation.md)
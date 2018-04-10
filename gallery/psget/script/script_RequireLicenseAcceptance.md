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
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="6b27f-103">Pro skripty, které vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="6b27f-103">Requiring License Acceptance for Scripts</span></span>

<span data-ttu-id="6b27f-104">Přijetí licence není podporována pro skripty.</span><span class="sxs-lookup"><span data-stu-id="6b27f-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="6b27f-105">Ale pokud skript závisí na modul, který vyžaduje přijetí licence je podporován.</span><span class="sxs-lookup"><span data-stu-id="6b27f-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="6b27f-106">Skript commands(Install-Script/Save-Script/Update-Script) podporují nový parametr - AcceptLicense, který se chová, jako by uživatel viděli licence.</span><span class="sxs-lookup"><span data-stu-id="6b27f-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="6b27f-107">Pokud není zadán - AcceptLicense; Uživatel se zobrazí license.txt pro závislé modul a vyzvání k přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="6b27f-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="6b27f-108">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="6b27f-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="6b27f-109">Příklad 1: Instalační skript se závislostmi, které vyžadují přijetí licence</span><span class="sxs-lookup"><span data-stu-id="6b27f-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>
<span data-ttu-id="6b27f-110">Skript ScriptRequireLicenseAcceptance závisí na modulu 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="6b27f-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="6b27f-111">Uživatel je vyzván k přijetí licenční.</span><span class="sxs-lookup"><span data-stu-id="6b27f-111">User is prompted to Accept License.</span></span>
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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="6b27f-112">Příklad 2: Instalační skript se závislostmi vyžadovat přijetí licence a - AcceptLicense</span><span class="sxs-lookup"><span data-stu-id="6b27f-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>
<span data-ttu-id="6b27f-113">Skript ScriptRequireLicenseAcceptance závisí na modulu 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="6b27f-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="6b27f-114">Uživatel není vyzvání k přijetí licence, jako jsou zadány - AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="6b27f-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="6b27f-115">Další informace</span><span class="sxs-lookup"><span data-stu-id="6b27f-115">More details</span></span>
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[<span data-ttu-id="6b27f-116">Vyžadovat přijetí licence podporu pro moduly</span><span class="sxs-lookup"><span data-stu-id="6b27f-116">Require License Acceptance support for Modules</span></span>](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[<span data-ttu-id="6b27f-117">Vyžadovat přijetí licence podporu na PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="6b27f-117">Require License Acceptance support on PowerShellGallery</span></span>](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[<span data-ttu-id="6b27f-118">Vyžadování přijetí licence při nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="6b27f-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)
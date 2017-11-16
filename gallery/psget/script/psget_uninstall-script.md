---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Odinstalujte skriptu
ms.openlocfilehash: 7973524cf9268d629b5375f0726fe70164bdeddb
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="uninstall-script"></a><span data-ttu-id="52c57-103">Odinstalujte skriptu</span><span class="sxs-lookup"><span data-stu-id="52c57-103">Uninstall-Script</span></span>

<span data-ttu-id="52c57-104">Soubor skriptu, která byla nainstalována pomocí PowerShellGet odinstaluje.</span><span class="sxs-lookup"><span data-stu-id="52c57-104">Uninstalls a script file which was installed using PowerShellGet.</span></span>

## <a name="description"></a><span data-ttu-id="52c57-105">Popis</span><span class="sxs-lookup"><span data-stu-id="52c57-105">Description</span></span>

<span data-ttu-id="52c57-106">Odinstalační skript rutiny odinstaluje zadaný skript soubory, které byly nainstalovány z úložiště online.</span><span class="sxs-lookup"><span data-stu-id="52c57-106">The Uninstall-Script cmdlet uninstalls the specified script files which were installed from the online repository.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="52c57-107">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="52c57-107">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Uninstall-Script -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="52c57-108">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="52c57-108">Cmdlet online help reference</span></span>

[<span data-ttu-id="52c57-109">Odinstalujte skriptu</span><span class="sxs-lookup"><span data-stu-id="52c57-109">Uninstall-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619789)

## <a name="example-commands"></a><span data-ttu-id="52c57-110">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="52c57-110">Example commands</span></span>

```powershell
Get-InstalledScript | Uninstall-Script -WhatIf
What if: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Required-Script3'".
What if: Performing the operation "Uninstall-Script" on target "Version '1.0' of script 'Demo-Script'".
What if: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Fabrikam-Script'".
What if: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Fabrikam-ServerScript'".
What if: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Required-Script1'".
What if: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Required-Script2'".
What if: Performing the operation "Uninstall-Script" on target "Version '2.0' of script 'Script-WithDependencies2'".

Uninstall-Script Required-Script1 -WhatIf -RequiredVersion 2.5
What if: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Required-Script1'".

Uninstall-Script Required-Script1 -WhatIf -MinimumVersion 2.0 -MaximumVersion 3.0
What if: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Required-Script1'".

Get-InstalledScript -Name Script-WithDependencies2 | Uninstall-Script -WhatIf
What if: Performing the operation "Uninstall-Script" on target "Version '2.0' of script 'Script-WithDependencies2'".

Get-InstalledScript -Name Script-WithDependencies2 | Uninstall-Script -Confirm
Confirm
Are you sure you want to perform this action?
Performing the operation "Uninstall-Script" on target "Version '2.0' of script 'Script-WithDependencies2'".
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"): N

Uninstall-Script Required-Script1 -RequiredVersion 2.5 -Verbose
VERBOSE: Performing the operation "Uninstall-Script" on target "Version '2.5' of script 'Required-Script1'".
VERBOSE: Successfully uninstalled the script 'Required-Script1' from script base 'C:\Users\manikb\Documents\WindowsPowerShell\Scripts'.

# Get-InstalledScript should not return the Required-Script1
Get-InstalledScript Required-Script1
PackageManagement\Get-Package : No match was found for the specified search criteria and script names 'Required-Script1'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:3142 char:9
+ PackageManagement\Get-Package @PSBoundParameters | Microsoft. ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : ObjectNotFound: (Microsoft.Power...lets.GetPackage:GetPackage) [Get-Package], Exception
+ FullyQualifiedErrorId : NoMatchFound,Microsoft.PowerShell.PackageManagement.Cmdlets.GetPackage
```


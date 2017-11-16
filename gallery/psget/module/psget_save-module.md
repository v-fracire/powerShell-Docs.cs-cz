---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Uložit – modul"
ms.openlocfilehash: 296c5c5ffc6f1e12da0162237e562b13b3679110
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="save-module"></a><span data-ttu-id="db01c-103">Uložit – modul</span><span class="sxs-lookup"><span data-stu-id="db01c-103">Save-Module</span></span>

<span data-ttu-id="db01c-104">Uloží modul místně bez nutnosti její instalace.</span><span class="sxs-lookup"><span data-stu-id="db01c-104">Saves a module locally without installing it.</span></span>

## <a name="description"></a><span data-ttu-id="db01c-105">Popis</span><span class="sxs-lookup"><span data-stu-id="db01c-105">Description</span></span>

<span data-ttu-id="db01c-106">Rutina modulu uložit uloží modul místně z zadané úložiště pro kontroly.</span><span class="sxs-lookup"><span data-stu-id="db01c-106">The Save-Module cmdlet saves a module locally from the specified repository for inspection.</span></span> <span data-ttu-id="db01c-107">Modul není nainstalován.</span><span class="sxs-lookup"><span data-stu-id="db01c-107">The module is not installed.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="db01c-108">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="db01c-108">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Save-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="db01c-109">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="db01c-109">Cmdlet online help reference</span></span>

[<span data-ttu-id="db01c-110">Uložit – modul</span><span class="sxs-lookup"><span data-stu-id="db01c-110">Save-Module</span></span>](http://go.microsoft.com/fwlink/?LinkId=531351)

## <a name="example-commands"></a><span data-ttu-id="db01c-111">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="db01c-111">Example commands</span></span>

```powershell
Save-Module -Repository MSPSGallery -Name ModuleWithDependencies2 -Path C:\MySavedModuleLocation
dir C:\MySavedModuleLocation

Directory: C:\MySavedModuleLocation

Mode LastWriteTime Length Name
---- ------------- ------ ----
d----- 4/21/2015 5:40 PM ModuleWithDependencies2
d----- 4/21/2015 5:40 PM NestedRequiredModule1
d----- 4/21/2015 5:40 PM NestedRequiredModule2
d----- 4/21/2015 5:40 PM NestedRequiredModule3
d----- 4/21/2015 5:40 PM RequiredModule1
d----- 4/21/2015 5:40 PM RequiredModule2
d----- 4/21/2015 5:40 PM RequiredModule3


# Find a command and save its module
# This command finds the specified command, and then passes it to Save-Module to save it to the C:\temp folder.
Find-Command -Name "Get-NestedRequiredModule4" -Repository "INT" | Save-Module -Path "C:\temp\" -Verbose


# Save the role capability modules by piping the Find-RoleCapability output to Save-Module cmdlet.
Find-RoleCapability -Name Maintenance,MyJeaRole | Save-Module -Path C:\MyModulesPath

```


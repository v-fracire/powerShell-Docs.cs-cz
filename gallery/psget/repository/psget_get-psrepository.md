---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Get-PSRepository
ms.openlocfilehash: 96f87428312c233757aa5fcae405a192aadff385
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="get-psrepository"></a><span data-ttu-id="ae622-103">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="ae622-103">Get-PSRepository</span></span>

<span data-ttu-id="ae622-104">Získá registrované úložiště na počítači.</span><span class="sxs-lookup"><span data-stu-id="ae622-104">Gets the registered repositories on a computer.</span></span>

## <a name="description"></a><span data-ttu-id="ae622-105">Popis</span><span class="sxs-lookup"><span data-stu-id="ae622-105">Description</span></span>

<span data-ttu-id="ae622-106">Rutinu Get-PSRepository získá úložiště modulu prostředí PowerShell, které jsou registrovány pro aktuálního uživatele v počítači.</span><span class="sxs-lookup"><span data-stu-id="ae622-106">The Get-PSRepository cmdlet gets PowerShell module repositories that are registered for the current user on a computer.</span></span>

<span data-ttu-id="ae622-107">Pro každý registrovaný úložiště vrátí Get-PSRepository PSRepository objekt, který lze volitelně přesměrovat Unregister-PSRepository pro zrušení registrace registrované úložiště.</span><span class="sxs-lookup"><span data-stu-id="ae622-107">For each registered repository, Get-PSRepository returns a PSRepository object which can optionally be piped to Unregister-PSRepository for unregistering a registered repository.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="ae622-108">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="ae622-108">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Get-PSRepository -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="ae622-109">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="ae622-109">Cmdlet online help reference</span></span>

[<span data-ttu-id="ae622-110">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="ae622-110">Get-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517127)

## <a name="example-commands"></a><span data-ttu-id="ae622-111">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="ae622-111">Example commands</span></span>

```powershell

# Properties of Get-PSRepository returned object
Get-PSRepository PSGallery | Format-List * -Force

Name                      : PSGallery
SourceLocation            : https://www.powershellgallery.com/api/v2/
Trusted                   : False
Registered                : True
InstallationPolicy        : Untrusted
PackageManagementProvider : NuGet
PublishLocation           : https://www.powershellgallery.com/api/v2/package/
ScriptSourceLocation      : https://www.powershellgallery.com/api/v2/items/psscript/
ScriptPublishLocation     : https://www.powershellgallery.com/api/v2/package/
ProviderOptions           : {}

# Get all registered repositories
Get-PSRepository

# Get a specific registered repository
Get-PSRepository PSGallery

Name                      InstallationPolicy   SourceLocation
----                      ------------------   --------------
PSGallery                 Untrusted            https://www.powershellgallery.com/api/v2/

# Get registered repository with wildcards
Get-PSRepository *Gallery*

```


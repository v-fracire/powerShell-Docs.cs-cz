---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: Get-PSRepository
ms.openlocfilehash: 97279a8ed0087c835fb924991484959cd7237016
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="get-psrepository"></a><span data-ttu-id="080af-103">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="080af-103">Get-PSRepository</span></span>

<span data-ttu-id="080af-104">Získá registrované úložiště na počítači.</span><span class="sxs-lookup"><span data-stu-id="080af-104">Gets the registered repositories on a computer.</span></span>

## <a name="description"></a><span data-ttu-id="080af-105">Popis</span><span class="sxs-lookup"><span data-stu-id="080af-105">Description</span></span>

<span data-ttu-id="080af-106">Rutinu Get-PSRepository získá úložiště modulu prostředí PowerShell, které jsou registrovány pro aktuálního uživatele v počítači.</span><span class="sxs-lookup"><span data-stu-id="080af-106">The Get-PSRepository cmdlet gets PowerShell module repositories that are registered for the current user on a computer.</span></span>

<span data-ttu-id="080af-107">Pro každý registrovaný úložiště vrátí Get-PSRepository PSRepository objekt, který lze volitelně přesměrovat Unregister-PSRepository pro zrušení registrace registrované úložiště.</span><span class="sxs-lookup"><span data-stu-id="080af-107">For each registered repository, Get-PSRepository returns a PSRepository object which can optionally be piped to Unregister-PSRepository for unregistering a registered repository.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="080af-108">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="080af-108">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Get-PSRepository -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="080af-109">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="080af-109">Cmdlet online help reference</span></span>

[<span data-ttu-id="080af-110">Get-PSRepository</span><span class="sxs-lookup"><span data-stu-id="080af-110">Get-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517127)

## <a name="example-commands"></a><span data-ttu-id="080af-111">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="080af-111">Example commands</span></span>

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
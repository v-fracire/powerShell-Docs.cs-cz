---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: "Zrušit registraci PSRepository"
ms.openlocfilehash: 91380210f262208fce39d596bd6c2ad05a819fbf
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="unregister-psrepository"></a><span data-ttu-id="f1f9f-103">Zrušit registraci PSRepository</span><span class="sxs-lookup"><span data-stu-id="f1f9f-103">Unregister-PSRepository</span></span>

<span data-ttu-id="f1f9f-104">Zruší registraci úložiště.</span><span class="sxs-lookup"><span data-stu-id="f1f9f-104">Unregisters a repository.</span></span>

## <a name="description"></a><span data-ttu-id="f1f9f-105">Popis</span><span class="sxs-lookup"><span data-stu-id="f1f9f-105">Description</span></span>

<span data-ttu-id="f1f9f-106">Rutinu Unregister-PSRepository zruší registraci úložiště pro aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="f1f9f-106">The Unregister-PSRepository cmdlet unregisters a repository for the current user.</span></span>
- <span data-ttu-id="f1f9f-107">Zrušení registrace a opakovanou registraci PSGallery úložiště je povolena pro organizace a odpojí scénáře.</span><span class="sxs-lookup"><span data-stu-id="f1f9f-107">Unregistration and re-registration of the PSGallery repository is allowed for an enterprise and disconnected scenarios.</span></span>
- <span data-ttu-id="f1f9f-108">Uživatelé mohou registrovat znovu PSGallery jednoduše spuštěním`Register-PSRepository -Default`</span><span class="sxs-lookup"><span data-stu-id="f1f9f-108">Users can re-register the PSGallery by simply running `Register-PSRepository -Default`</span></span>
- <span data-ttu-id="f1f9f-109">Vzhledem k tomu, že výchozí nastavení je PSGallery publikovat úložiště v modulu publikování a publikovat skript rutiny, bude vyvolána chyba, pokud PSGallery není k dispozici v seznamu registrovaných úložiště.</span><span class="sxs-lookup"><span data-stu-id="f1f9f-109">Since PSGallery is the default publish repository in Publish-Module and Publish-Script cmdlets, an error will be thrown if PSGallery is not available in the registered repository list.</span></span>

## <a name="cmdlet-syntax"></a><span data-ttu-id="f1f9f-110">Syntaxe rutin</span><span class="sxs-lookup"><span data-stu-id="f1f9f-110">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="f1f9f-111">Referenční informace o rutinách online nápovědy</span><span class="sxs-lookup"><span data-stu-id="f1f9f-111">Cmdlet online help reference</span></span>

[<span data-ttu-id="f1f9f-112">Zrušit registraci PSRepository</span><span class="sxs-lookup"><span data-stu-id="f1f9f-112">Unregister-PSRepository</span></span>](http://go.microsoft.com/fwlink/?LinkID=517130)

## <a name="example-commands"></a><span data-ttu-id="f1f9f-113">Příklady příkazů</span><span class="sxs-lookup"><span data-stu-id="f1f9f-113">Example commands</span></span>

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### <a name="unregistration-and-re-registration-of-the-psgallery-repository-is-allowed-for-an-enterprise-and-disconnected-scenarios"></a><span data-ttu-id="f1f9f-114">Zrušení registrace a opakovanou registraci PSGallery úložiště je povolena pro organizace a odpojí scénáře.</span><span class="sxs-lookup"><span data-stu-id="f1f9f-114">Unregistration and re-registration of the PSGallery repository is allowed for an enterprise and disconnected scenarios.</span></span>
```powershell

# Unregister PSGallery repository
Unregister-PSRepository PSGallery

# Publish-Module throws an error when PSGallery is not a registered repository
Publish-Module -Name MyModule
publish-module : Unable to find repository 'PSGallery'. Use Get-PSRepository to see all available repositories. Try again after specifying a valid repository name. You can use 'Register-PSRepository -Default' to register the PSGallery repository.
At line:1 char:1
+ publish-module -name mymodule
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (PSGallery:String) [Publish-Module], ArgumentException
    + FullyQualifiedErrorId : PSGalleryNotFound,Publish-Module

# Re-register PSGallery repository
Register-PSRepository -Default
```

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
# <a name="unregister-psrepository"></a>Zrušit registraci PSRepository

Zruší registraci úložiště.

## <a name="description"></a>Popis

Rutinu Unregister-PSRepository zruší registraci úložiště pro aktuálního uživatele.
- Zrušení registrace a opakovanou registraci PSGallery úložiště je povolena pro organizace a odpojí scénáře.
- Uživatelé mohou registrovat znovu PSGallery jednoduše spuštěním`Register-PSRepository -Default`
- Vzhledem k tomu, že výchozí nastavení je PSGallery publikovat úložiště v modulu publikování a publikovat skript rutiny, bude vyvolána chyba, pokud PSGallery není k dispozici v seznamu registrovaných úložiště.

## <a name="cmdlet-syntax"></a>Syntaxe rutin

```powershell
Get-Command -Name Unregister-PSRepository -Module PowerShellGet -Syntax
```
## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Zrušit registraci PSRepository](http://go.microsoft.com/fwlink/?LinkID=517130)

## <a name="example-commands"></a>Příklady příkazů

```powershell
Unregister-PSRepository -Name "MyPrivateGallery"

Get-PSRepository exp | Unregister-PSRepository
```

### <a name="unregistration-and-re-registration-of-the-psgallery-repository-is-allowed-for-an-enterprise-and-disconnected-scenarios"></a>Zrušení registrace a opakovanou registraci PSGallery úložiště je povolena pro organizace a odpojí scénáře.
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


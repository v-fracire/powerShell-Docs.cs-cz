---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: Aktualizace modulu
ms.openlocfilehash: 343c296dad2a3df35f13393b3796a1d484f5f535
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="update-module"></a>Aktualizace modulu

Stáhne a nainstaluje nejnovější verzi zadané moduly z online galerie do místního počítače.

## <a name="description"></a>Popis

Rutinu Update-Module nainstaluje na novější verzi modul prostředí Windows PowerShell, který byl nainstalován z online galerie spuštěním instalace modulu v místním počítači.

Ve výchozím nastavení je nainstalovaná nejnovější verze zadaný modul k dispozici v online galerie, pokud nezadáte požadovaná verze. Modul existující, nainstalované můžete aktualizovat tak, že zadáte název modulu; Aktualizace modulu vyhledá $env: PSModulePath pro modul, který chcete aktualizovat.

Spuštění aktualizace modul bez názvu parametru aktualizuje všechny moduly, které mohou být aktualizovány na místním počítači.

### <a name="notes"></a>Poznámky

- Tato rutina se spustí v prostředí Windows PowerShell 3.0 nebo novější verze prostředí Windows PowerShell na Windows 7 nebo Windows 2008 R2 a pozdějších verzích Windows.
- Pokud modul, který můžete určit pomocí parametru název nebyl nainstalován pomocí instalace modulu, dojde k chybě. Aktualizace modulu lze spustit jen u moduly, které jste nainstalovali z online galerie spuštěním instalace modulu.
- Pokud aktualizace modul se pokusí aktualizovat binární soubory, které se používají, aktualizace modulu vrátí chybu, která identifikuje procesy problém a informuje uživatele, zopakujte akci aktualizace modulu po ukončení procesů.
- PowerShell 5.0 nebo novější verze Pokud aktualizace modulu aktualizuje modul, přidá nejnovější (nebo zadaný) verzi modulu, takže starší a novějších verzí teď-souběžného ve stejném adresáři. Je užitečné k vyslovení tak a k zobrazení příkladu výstupu z těchto příkazů.


## <a name="cmdlet-syntax"></a>Syntaxe rutin
```powershell
Get-Command -Name Update-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>Referenční informace o rutinách online nápovědy

[Aktualizace modulu](http://go.microsoft.com/fwlink/?LinkID=398576)


## <a name="example-commands"></a>Příklady příkazů

```powershell
PS C:\\windows\\system32> Update-Module -Name ContosoServer -RequiredVersion 1.5
PS C:\\windows\\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.0
PS C:\\windows\\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
PS C:\\windows\\system32> Update-Module -Name ContosoServer
PS C:\\windows\\system32> Get-Module -ListAvailable -Name ContosoServer | Format-List Name,Version,ModuleBase
Name : ContosoServer
Version : 2.8.1
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.8.1
Name : ContosoServer
Version : 2.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\2.0
Name : ContosoServer
Version : 1.5
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.5
Name : ContosoServer
Version : 1.0
ModuleBase : C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoServer\\1.0
PS C:\\windows\\system32> Get-InstalledModule
Version Name Repository Description
------- ---- ---------- -----------
1.0 ContosoServer MSPSGallery ContosoServer module
1.5 ContosoServer MSPSGallery ContosoServer module
2.0 ContosoServer MSPSGallery ContosoServer module
2.8.1 ContosoServer MSPSGallery ContosoServer module
```


###  <a name="update-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a>Aktualizace modulu TestDepWithNestedRequiredModules1 se závislostmi.
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -AllVersions

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module

Update-Module -Name TestDepWithNestedRequiredModules1 -RequiredVersion 2.0
Get-InstalledModule

Version    Name                                Repository  Description
-------    ----                                ----------  -----------
1.0        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
2.5        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
1.0        RequiredModule1                     LocalRepo   RequiredModule1 module
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module
2.5        RequiredModule3                     LocalRepo   RequiredModule3 module
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
2.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module
```


---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 91b60a22580dcb8eae245f45e202710812522a64
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="powershellget-cmdlets-for-module-management"></a>PowerShellGet rutiny pro správu modulu

- [Najít DscResource](https://technet.microsoft.com/en-us/library/mt654006.aspx)
- [Najít – modul](https://technet.microsoft.com/en-us/library/dn807167.aspx)
- [Najít skriptu](https://technet.microsoft.com/en-us/library/mt654001.aspx)
- [Get-InstalledModule](https://technet.microsoft.com/en-us/library/mt653990.aspx)
- [Get-InstalledScript](https://technet.microsoft.com/en-us/library/mt653994.aspx)
- [Get-PSRepository](https://technet.microsoft.com/en-us/library/dn807170.aspx)
- [Instalace modulu](https://technet.microsoft.com/en-us/library/dn807162.aspx)
- [Instalační skript](https://technet.microsoft.com/en-us/library/mt653998.aspx)
- [Nové ScriptFileInfo](https://technet.microsoft.com/en-us/library/mt653995.aspx)
- [Publikování modulu](https://technet.microsoft.com/en-us/library/dn807163.aspx)
- [Publikování skriptu](https://technet.microsoft.com/en-us/library/mt654003.aspx)
- [Registrace PSRepository](https://technet.microsoft.com/en-us/library/dn807168.aspx)
- [Uložit – modul](https://technet.microsoft.com/en-us/library/mt653992.aspx)
- [Uložení skriptu](https://technet.microsoft.com/en-us/library/mt654004.aspx)
- [Set-PSRepository](https://technet.microsoft.com/en-us/library/dn807165.aspx)
- [Test ScriptFileInfo](https://technet.microsoft.com/en-us/library/mt654005.aspx)
- [Odinstalujte modul](https://technet.microsoft.com/en-us/library/mt653996.aspx)
- [Odinstalujte skriptu](https://technet.microsoft.com/en-us/library/mt653989.aspx)
- [Aktualizace modulu](https://technet.microsoft.com/en-us/library/dn807166.aspx)
- [Aktualizace ModuleManifest](https://technet.microsoft.com/en-us/library/mt654002.aspx)
- [Skript aktualizace](https://technet.microsoft.com/en-us/library/mt653997.aspx)
- [Aktualizace ScriptFileInfo](https://technet.microsoft.com/en-us/library/mt653991.aspx)
- [Zrušit registraci PSRepository](https://technet.microsoft.com/en-us/library/dn807161.aspx)

## <a name="module-dependency-installation-support-get-installedmodule-and-uninstall-module-cmdlets"></a>Podpora instalace modulu závislostí, Get-InstalledModule a odinstalace modulu rutiny
- Přidat modul závislosti naplnění v rutině modulu publikovat. Seznamy RequiredModules a NestedModules PSModuleInfo se používají při přípravě seznamu závislostí modulu k publikování.
- Přidání závislostí instalace podpora rutiny Install-Module a aktualizace modulu. Modul závislosti jsou nainstalované a aktualizovat ve výchozím nastavení.
- Přidat parametrem - IncludeDependencies do rutiny modulu najít zahrnout modulu závislosti ve výsledcích.
- Přidaná podpora - MaximumVersion na Najít modulu modulu instalace a aktualizace modulu rutiny.
- Přidání nové Get-InstalledModule a odinstalace modulu rutiny.

## <a name="powershellget-cmdlets-demo-with-module-dependencies-support"></a>Ukázkové rutiny PowerShellGet modulu závislosti podporují:

### <a name="ensure-that-module-dependencies-are-available-on-the-repository"></a>Ujistěte se, že modul závislosti jsou k dispozici v úložišti:
```powershell
Find-Module -Repository LocalRepo -Name RequiredModule1,RequiredModule2,RequiredModule3,NestedRequiredModule1,NestedRequiredModule2,NestedRequiredModule3 | Sort-Object -Property Name

Version    Name                     Repository    Description                  
-------    ----                     ----------    -----------                  
2.5        NestedRequiredModule1    LocalRepo     NestedRequiredModule1 module 
2.5        NestedRequiredModule2    LocalRepo     NestedRequiredModule2 module 
2.0        NestedRequiredModule3    LocalRepo     NestedRequiredModule3 module 
2.5        RequiredModule1          LocalRepo     RequiredModule1 module  
2.5        RequiredModule2          LocalRepo     RequiredModule2 module  
2.0        RequiredModule3          LocalRepo     RequiredModule3 module
```

### <a name="create-a-module-with-dependencies-that-are-specified-in-the-requiredmodules-and-nestedmodules-properties-of-its-module-manifest"></a>Vytvoření modulu s závislosti, které jsou určené ve vlastnostech RequiredModules a NestedModules jeho manifestu modulu.
```powershell
$RequiredModules = @('RequiredModule1',
                     @{ModuleName = 'RequiredModule2'; ModuleVersion = '1.5'; },
                     @{ModuleName = 'RequiredModule3'; RequiredVersion = '2.0'; })

$NestedRequiredModules = @('TestDepWithNestedRequiredModules1.psm1', 'NestedRequiredModule1',
                            @{ModuleName = 'NestedRequiredModule2'; ModuleVersion = '1.5'; },
                            @{ModuleName = 'NestedRequiredModule3'; RequiredVersion = '2.0'; })

New-ModuleManifest -Path 'C:\Program Files\WindowsPowerShell\Modules\TestDepWithNestedRequiredModules1\TestDepWithNestedRequiredModules1.psd1' `
-NestedModules $NestedRequiredModules -RequiredModules $RequiredModules -ModuleVersion "1.0" -Description "TestDepWithNestedRequiredModules1 module"
```

###  <a name="publish-two-versions-10-and-20-of-the-testdepwithnestedrequiredmodules1-module-with-dependencies-to-the-repository"></a>Publikování dvě verze (**"1.0"** a **"2.0"**) modulu TestDepWithNestedRequiredModules1 se závislostmi do úložiště.
```powershell
Publish-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -NuGetApiKey "MyNuGet-ApiKey-For-LocalRepo"
```

###  <a name="find-the-testdepwithnestedrequiredmodules1-module-with-its-dependencies-by-specifying--includedependencies"></a>Zadáním - IncludeDependencies najít modul TestDepWithNestedRequiredModules1 s jeho závislé součásti.
```powershell
Find-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo –IncludeDependencies -MaximumVersion "1.0"

Version    Name                                Repository  Description 
-------    ----                                ----------  -----------  
1.0        TestDepWithNestedRequiredModules1   LocalRepo   TestDepWithNestedRequiredModules1 module  
2.5        RequiredModule1                     LocalRepo   RequiredModule1 module      
2.5        RequiredModule2                     LocalRepo   RequiredModule2 module      
2.0        RequiredModule3                     LocalRepo   RequiredModule3 module      
2.5        NestedRequiredModule1               LocalRepo   NestedRequiredModule1 module
2.5        NestedRequiredModule2               LocalRepo   NestedRequiredModule2 module
2.0        NestedRequiredModule3               LocalRepo   NestedRequiredModule3 module
``` 

### <a name="use-find-module-metadata-to-find-the-module-dependencies"></a>Metadata modulu najít slouží k vyhledání modulu závislosti.
```powershell
$psgetModuleInfo = Find-Module -Repository MSPSGallery -Name ModuleWithDependencies2
$psgetModuleInfo.Dependencies.ModuleName

RequiredModule1
RequiredModule2
RequiredModule3
NestedRequiredModule1
NestedRequiredModule2
NestedRequiredModule3

$psgetModuleInfo.Dependencies

Name Value
---- -----
ModuleName RequiredModule1
CanonicalId PowerShellGet:RequiredModule1/#http://psget/psGallery/api/v2/

ModuleName RequiredModule2
ModuleVersion 2.0
CanonicalId PowerShellGet:RequiredModule2/2.0#http://psget/psGallery/api/v2/

ModuleName RequiredModule3
RequiredVersion 2.5
CanonicalId PowerShellGet:RequiredModule3/2.5#http://psget/psGallery/api/v2/

ModuleName NestedRequiredModule1
CanonicalId PowerShellGet:NestedRequiredModule1/#http://psget/psGallery/api/v2/

ModuleName NestedRequiredModule2
ModuleVersion 2.0
CanonicalId PowerShellGet:NestedRequiredModule2/2.0#http://psget/psGallery/api/v2/

ModuleName NestedRequiredModule3
RequiredVersion 2.5
CanonicalId PowerShellGet:NestedRequiredModule3/2.5#http://psget/psGallery/api/v2/
```

###  <a name="install-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a>Nainstalujte modul TestDepWithNestedRequiredModules1 se závislostmi.
```powershell
Install-Module -Name TestDepWithNestedRequiredModules1 -Repository LocalRepo -RequiredVersion "1.0"
Get-InstalledModule

Version    Name                    Repository   Description                 
-------    ----                    ----------   -----------                 
1.0        NestedRequiredModule1   LocalRepo    NestedRequiredModule1 module
2.5        NestedRequiredModule2   LocalRepo    NestedRequiredModule2 module
2.0        NestedRequiredModule3   LocalRepo    NestedRequiredModule3 module
1.0        RequiredModule1         LocalRepo    RequiredModule1 module      
2.5        RequiredModule2                    LocalRepo    RequiredModule2 module 
2.0        RequiredModule3                    LocalRepo    RequiredModule3 module 
1.0        TestDepWithNestedRequiredModules1  LocalRepo    TestDepWithNestedRequiredModules1 module
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

###  <a name="run-the-uninstall-module-cmdlet-to-uninstall-a-module-that-you-installed-by-using-powershellget"></a>Spusťte rutinu Uninstall-Module odinstalovat modul, který jste nainstalovali pomocí PowerShellGet.
Pokud ostatní moduly závisí na modul, který chcete odstranit, PowerShellGet vrátí chybu.
```powershell
Get-InstalledModule -Name RequiredModule1 | Uninstall-Module

PackageManagement\Uninstall-Package : The module 'RequiredModule1' of version '2.5' in module base folder 'C:\Program Files\WindowsPowerShell\Modules\RequiredModule1\2.5' cannot be uninstalled, because one or more other modules 'ModuleWithDependencies2' are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'RequiredModule1'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\PSGet.psm1:1303 char:25
+ ... $null = PackageManagement\\Uninstall-Package @PSBoundParameters
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Package], Exception
+ FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.UninstallPackage
```

## <a name="save-module-cmdlet"></a>Rutinu modulu uložit
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
```

## <a name="update-modulemanifest-cmdlet"></a>Rutina aktualizace ModuleManifest
Tato nová rutina se používá k aktualizace manifest souboru s hodnotami vstupní vlastnost nápovědy. Všechny parametry, které nemá testovací ModuleManifest trvá.

Zjistíme, že mnoho modulu autoři chtěli zadejte "\*" exportovaný hodnoty, jako je například FunctionsToExport, CmdletsToExport, atd. Při publikování modulu v galerii prostředí PowerShell, neurčené funkce a příkazy se nenaplní správně do galerie. Proto doporučujeme aktualizace modulu autoři jejich manifesty s správné hodnoty.

Pokud máte moduly, které byly exportovány vlastnosti, naplní aktualizace ModuleManifest zadaný soubor manifestu informace z exportovaných funkcí, rutin, proměnné atd:
```powershell
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'

#(Other properties removed here for Simplicity…)

# Functions to export from this module
FunctionsToExport = '*'
# Cmdlets to export from this module
CmdletsToExport = '*'
# Variables to export from this module
VariablesToExport = '*'
# Aliases to export from this module
AliasesToExport = '*'
}
```

Po aktualizaci ModuleManifest:
```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
Get-Content -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1"
#
# Module manifest for module 'NewManifest'
#
# Generated by: author name
#
# Generated on: 11/13/2015
#
@{
# Script module or binary module file associated with this manifest.
# RootModule = ''
# Version number of this module.
ModuleVersion = '2.5'
# ID used to uniquely identify this module
GUID = '610e5c5b-dc42-4eaa-8511-ebfb44066d5e'
# Functions to export from this module
FunctionsToExport = 'Get-FooFn Get-FooWF'
# Cmdlets to export from this module
CmdletsToExport = 'Test-PSGetTestCmdlet'
}
```

Pro každý modul existují také pole metadat, které jsou s ním spojená. Aby bylo možné zobrazit metadata správně na PowrShell galerie, můžete aktualizace ModuleManifest k naplnění těchto polí v rámci PrivateData.
```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1" -Tags "Tag1" -LicenseUri "http://license.com" -ProjectUri "http://project.com" -IconUri "http://icon.com" -ReleaseNotes "Test module"
```
Zatřiďovací tabulky PrivateData ze souboru manifestu šablony má následující vlastnosti:
```powershell
# Private data to pass to the module specified in RootModule/ModuleToProcess. This may also contain a PSData hashtable with additional module metadata used by PowerShell.
PrivateData = @{
    PSData = @{
        # Tags applied to this module. These help with module discovery in online galleries.
        # Tags = @()

        # A URL to the license for this module.
        # LicenseUri = ''
    
        # A URL to the main website for this project.
        # ProjectUri = ''
        
        # A URL to an icon representing this module.
        # IconUri = ''
        
        # ReleaseNotes of this module
        # ReleaseNotes = ''
        
        # External dependent modules of this module
        # ExternalModuleDependencies = ''
    } # End of PSData hashtable
} # End of PrivateData hashtable
```
***Poznámka:*** DscResourcesToExport je podporován pouze na nejnovější rozhraní PowerShell verze 5.0. Jsme nebude možné aktualizovat pole, pokud běží na předchozí verze prostředí PowerShell.


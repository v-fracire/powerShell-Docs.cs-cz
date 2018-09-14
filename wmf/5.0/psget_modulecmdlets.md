---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 29b11e8b11f27fc5be60ea8c5cd56138326b3998
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522818"
---
# <a name="powershellget-cmdlets-for-module-management"></a>Rutiny správce balíčků PowerShellGet pro správu modulů

- [Find-DscResource](https://technet.microsoft.com/library/mt654006.aspx)
- [Find-Module](https://technet.microsoft.com/library/dn807167.aspx)
- [Find-Script](https://technet.microsoft.com/library/mt654001.aspx)
- [Get-InstalledModule](https://technet.microsoft.com/library/mt653990.aspx)
- [Get-InstalledScript](https://technet.microsoft.com/library/mt653994.aspx)
- [Get-PSRepository](https://technet.microsoft.com/library/dn807170.aspx)
- [Install-Module](https://technet.microsoft.com/library/dn807162.aspx)
- [Install-Script](https://technet.microsoft.com/library/mt653998.aspx)
- [New-ScriptFileInfo](https://technet.microsoft.com/library/mt653995.aspx)
- [Publish-Module](https://technet.microsoft.com/library/dn807163.aspx)
- [Publish-Script](https://technet.microsoft.com/library/mt654003.aspx)
- [Register-PSRepository](https://technet.microsoft.com/library/dn807168.aspx)
- [Save-Module](https://technet.microsoft.com/library/mt653992.aspx)
- [Save-Script](https://technet.microsoft.com/library/mt654004.aspx)
- [Set-PSRepository](https://technet.microsoft.com/library/dn807165.aspx)
- [Test-ScriptFileInfo](https://technet.microsoft.com/library/mt654005.aspx)
- [Odinstalujte modul](https://technet.microsoft.com/library/mt653996.aspx)
- [Odinstalace Script](https://technet.microsoft.com/library/mt653989.aspx)
- [Aktualizace modulu](https://technet.microsoft.com/library/dn807166.aspx)
- [Update-ModuleManifest](https://technet.microsoft.com/library/mt654002.aspx)
- [Update-Script](https://technet.microsoft.com/library/mt653997.aspx)
- [Update-ScriptFileInfo](https://technet.microsoft.com/library/mt653991.aspx)
- [Zrušit registraci PSRepository](https://technet.microsoft.com/library/dn807161.aspx)

## <a name="module-dependency-installation-support-get-installedmodule-and-uninstall-module-cmdlets"></a>Podpora instalace závislostí modulů, Get-InstalledModule a rutiny Uninstall-Module
- Naplnění závislosti modulu do rutiny Publish-Module. RequiredModules a NestedModules seznamů PSModuleInfo se používají při přípravě seznam závislostí modulu má být publikován.
- Podpora instalace přidání závislostí v rutiny Install-Module a aktualizace modulu. Závislosti modulu jsou nainstalovány a aktualizovány ve výchozím nastavení.
- Přidat parametr - IncludeDependencies do rutiny Find-Module zahrnout závislostí modulů ve výsledcích.
- Přidání podpory - MaximumVersion na Find-Module, Install-Module a rutiny Update-Module.
- Přidání nových Get-InstalledModule a odinstalovat modul rutin.

## <a name="powershellget-cmdlets-demo-with-module-dependencies-support"></a>Ukázkový rutiny PowerShellGet s závislosti modulu podporovat:

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

### <a name="create-a-module-with-dependencies-that-are-specified-in-the-requiredmodules-and-nestedmodules-properties-of-its-module-manifest"></a>Vytvoření modulu se závislostmi, které jsou určené ve vlastnostech RequiredModules a NestedModules manifestu modulu.
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

###  <a name="find-the-testdepwithnestedrequiredmodules1-module-with-its-dependencies-by-specifying--includedependencies"></a>Zadáním - IncludeDependencies se najdete modul TestDepWithNestedRequiredModules1 její závislosti.
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

### <a name="use-find-module-metadata-to-find-the-module-dependencies"></a>Find-Module metadata použijte k vyhledání závislostí modulů.
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

###  <a name="install-the-testdepwithnestedrequiredmodules1-module-with-dependencies"></a>Instalace modulu TestDepWithNestedRequiredModules1 se závislostmi.
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

###  <a name="run-the-uninstall-module-cmdlet-to-uninstall-a-module-that-you-installed-by-using-powershellget"></a>Spusťte rutinu Uninstall-Module k odinstalaci modulu, který jste nainstalovali pomocí Správce balíčků PowerShellGet.
Pokud jakýkoli modul závisí na modul, který chcete odstranit, Správce balíčků PowerShellGet vyvolá chybu.
```powershell
Get-InstalledModule -Name RequiredModule1 | Uninstall-Module

PackageManagement\Uninstall-Package : The module 'RequiredModule1' of version '2.5' in module base folder 'C:\Program Files\WindowsPowerShell\Modules\RequiredModule1\2.5' cannot be uninstalled, because one or more other modules 'ModuleWithDependencies2' are dependent on this module. Uninstall the modules that depend on this module before uninstalling module 'RequiredModule1'.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\PSGet.psm1:1303 char:25
+ ... $null = PackageManagement\\Uninstall-Package @PSBoundParameters
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : InvalidOperation: (Microsoft.Power...ninstallPackage:UninstallPackage) [Uninstall-Package], Exception
+ FullyQualifiedErrorId : UnableToUninstallAsOtherModulesNeedThisModule,Uninstall-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.UninstallPackage
```

## <a name="save-module-cmdlet"></a>Rutina Save-Module
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

## <a name="update-modulemanifest-cmdlet"></a>Rutina Update-ModuleManifest
Tato nová rutina slouží ke snadnější aktualizace hodnoty vstupní vlastnosti souboru manifestu. Všechny parametry, které provádí Test ModuleManifest trvá.

Zjistíme, že velké množství autoři modulu chtěli "\*" v exportovaných hodnot, jako je například FunctionsToExport CmdletsToExport, atd. Během publikování modulu galerii prostředí PowerShell, příkazy a neurčené funkce nebudou naplněné, správně do galerie. Proto doporučujeme aktualizovat autoři modulu svých manifestech s odpovídajícími hodnotami.

Pokud máte moduly, které jste exportovali vlastnosti aktualizace ModuleManifest vyplní zadaný soubor manifestu s informacemi z exportovaných funkcí, rutiny, proměnné atd:
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

Pro každý modul existují také pole metadat, které jsou s ním spojená. Aby bylo možné správně zobrazit metadata v galerii PowrShell, můžete použít aktualizace ModuleManifest k naplnění těchto polí v rámci PrivateData.
```powershell
Update-ModuleManifest -Path "C:\Temp\PSGTEST-TestPackageMetadata\2.5\PSGTEST-TestPackageMetadata.psd1" -Tags "Tag1" -LicenseUri "http://license.com" -ProjectUri "http://project.com" -IconUri "http://icon.com" -ReleaseNotes "Test module"
```
Zatřiďovací tabulka PrivateData ze souboru manifestu šablony má následující vlastnosti:
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
***Poznámka:*** DscResourcesToExport je podporována pouze na nejnovější PowerShell verze 5.0. Společnost Microsoft nebude možné aktualizovat pole, pokud používáte předchozí verzi prostředí PowerShell.

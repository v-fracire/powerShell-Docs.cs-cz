---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Psaní vlastních prostředků DSC s MOF
ms.openlocfilehash: 2dcdeb49b50e23bc8b9d87293ebb8d8ec5e7b57d
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403646"
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a>Psaní vlastních prostředků DSC s MOF

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

V tomto tématu jsme se definovat schéma pro vlastní prostředek Windows PowerShell Desired State Configuration (DSC) v souboru MOF a implementovat prostředek v souboru skriptu Windows Powershellu. Tento vlastní prostředek je pro vytváření a udržování webu.

## <a name="creating-the-mof-schema"></a>Vytváří se schéma MOF

Schéma definuje vlastnosti prostředku, který se dá nakonfigurovat pomocí skriptu konfigurace DSC.

### <a name="folder-structure-for-a-mof-resource"></a>Struktura složek pro prostředek MOF

Pokud chcete implementovat vlastní prostředek DSC se schématem MOF, vytvořte následující strukturu složek. Schéma MOF je definována v souboru Demo_IISWebsite.schema.mof a skript prostředků je definována v Demo_IISWebsite.psm1. Volitelně můžete vytvořit soubor manifestu (psd1) modulu.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

Mějte na paměti, že je potřeba vytvořit složku s názvem DSCResources nejvyšší úrovně ve složce, a že složku pro každý zdroj musí mít stejný název jako prostředek.

### <a name="the-contents-of-the-mof-file"></a>Obsah souboru MOF

Tady je příklad souboru MOF, který lze použít pro vlastní web prostředků. Postupujte podle tohoto příkladu, uložit toto schéma do souboru a soubor *Demo_IISWebsite.schema.mof*.

```
[ClassVersion("1.0.0"), FriendlyName("Website")]
class Demo_IISWebsite : OMI_BaseResource
{
  [Key] string Name;
  [Required] string PhysicalPath;
  [write,ValueMap{"Present", "Absent"},Values{"Present", "Absent"}] string Ensure;
  [write,ValueMap{"Started","Stopped"},Values{"Started", "Stopped"}] string State;
  [write] string Protocol[];
  [write] string BindingInfo[];
  [write] string ApplicationPool;
  [read] string ID;
};
```

Mějte na paměti následující skutečnosti související předchozí kód:

* `FriendlyName` Definuje název, který můžete použít k odkazování na tento vlastní prostředek ve skriptech konfigurace DSC. V tomto příkladu `Website` popisný název odpovídá `Archive` pro integrované prostředek Archive.
* Můžete definovat pro váš vlastní prostředek musí být odvozen od třídy `OMI_BaseResource`.
* Kvalifikátor typu `[Key]`na vlastnost indikuje, že tato vlastnost bude jedinečným způsobem identifikovat instanci zdroje. Alespoň jeden `[Key]` vlastnost je povinná.
* `[Required]` Kvalifikátor označuje, že tato vlastnost je vyžadovaná (musí být zadána hodnota v konfigurační skript, který používá tento prostředek).
* `[write]` Kvalifikátor označuje, že tato vlastnost je volitelná, při použití vlastního prostředku ve skriptu konfigurace. `[read]` Kvalifikátor označuje, že vlastnost nejde zadat konfigurace a je jenom ke generování sestav.
* `Values` omezí hodnoty, které je možné přiřadit k vlastnosti do seznamu hodnot definovaných v `ValueMap`. Další informace najdete v tématu [chybu a hodnota kvalifikátory](/windows/desktop/WmiSdk/value-map).
* Volá se, včetně vlastnost `Ensure` hodnotami `Present` a `Absent` v prostředku se doporučuje jako způsob, jak udržovat v jednotném stylu s integrované prostředky DSC.
* Název souboru schématu pro vlastní prostředek následujícím způsobem: `classname.schema.mof`, kde `classname` je identifikátor, který následuje `class` – klíčové slovo v definici schématu.

### <a name="writing-the-resource-script"></a>Psaní skriptu prostředků

Skript prostředků implementuje logiku prostředku. V tomto modulu musí obsahovat tři funkce volané **Get-TargetResource**, **Set-TargetResource**, a **testovací TargetResource**. Všechny tři funkce musí být sada parametrů je stejný jako sadu vlastnosti definované ve schématu MOF, který jste vytvořili pro váš prostředek. V tomto dokumentu touto sadou vlastností se označuje jako "vlastnosti prostředku." Tyto tři funkce v souboru s názvem Store <ResourceName>.psm1. V následujícím příkladu jsou funkce uloženy v souboru s názvem Demo_IISWebsite.psm1.

> **Poznámka:**: Při spuštění stejný konfigurační skript pro váš prostředek více než jednou, mělo by se zobrazit žádné chyby a prostředku by měla zůstat v stejného stavu jako po spuštění skriptu. Jak toho dosáhnout, ujistěte se, že vaše **Get-TargetResource** a **TargetResource testovací** funkce nechte beze změny prostředku a tohoto volání **Set-TargetResource**více než jednou v uvedeném pořadí s stejný parametr hodnoty je vždy ekvivalentní k vyvolání jednou fungovat.

V **Get-TargetResource** funkce implementace, použít hodnoty vlastností klíče prostředků, které jsou k dispozici jako parametry a zkontrolujte stav instance zadaného prostředku. Tato funkce musí vracet zatřiďovací tabulku, která jsou uvedeny vlastnosti prostředků jako klíče a skutečné hodnoty těchto vlastností jako odpovídající hodnoty. Následující kód obsahuje příklad.

```powershell
# DSC uses the Get-TargetResource function to fetch the status of the resource instance specified in the parameters for the target machine
function Get-TargetResource
{
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

        $getTargetResourceResult = $null;

        <# Insert logic that uses the mandatory parameter values to get the website and assign it to a variable called $Website #>
        <# Set $ensureResult to "Present" if the requested website exists and to "Absent" otherwise #>

        # Add all Website properties to the hash table
        # This simple example assumes that $Website is not null
        $getTargetResourceResult = @{
                                      Name = $Website.Name;
                                        Ensure = $ensureResult;
                                        PhysicalPath = $Website.physicalPath;
                                        State = $Website.state;
                                        ID = $Website.id;
                                        ApplicationPool = $Website.applicationPool;
                                        Protocol = $Website.bindings.Collection.protocol;
                                        Binding = $Website.bindings.Collection.bindingInformation;
                                    }

        $getTargetResourceResult;
}
```

V závislosti na hodnoty, které jsou určené pro vlastnosti prostředku v konfigurační skript **Set-TargetResource** musíte udělat jednu z následujících akcí:

* Vytvoření nového webu
* Aktualizace existujícího webu
* Odstranit existující web

Následující příklad ukazuje to.

```powershell
# The Set-TargetResource function is used to create, delete or configure a website on the target machine.
function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

    <# If Ensure is set to "Present" and the website specified in the mandatory input parameters does not exist, then create it using the specified parameter values #>
    <# Else, if Ensure is set to "Present" and the website does exist, then update its properties to match the values provided in the non-mandatory parameter values #>
    <# Else, if Ensure is set to "Absent" and the website does not exist, then do nothing #>
    <# Else, if Ensure is set to "Absent" and the website does exist, then delete the website #>
}
```

Nakonec **testovací TargetResource** funkce musí přebírat stejný parametr nastavit jako **Get-TargetResource** a **Set-TargetResource**. Ve vaší implementaci **testovací TargetResource**, zkontrolujte stav instance prostředku, který je zadán v klíčových parametrů. Pokud skutečný stav instance prostředku neodpovídá hodnoty zadané v sadu parametrů, vrátí **$false**. V opačném případě vrátí **$true**.

Následující kód implementuje **testovací TargetResource** funkce.

```powershell
function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[parameter(Mandatory = $true)]
[System.String]
$Name,

[parameter(Mandatory = $true)]
[System.String]
$PhysicalPath,

[ValidateSet("Started","Stopped")]
[System.String]
$State,

[System.String[]]
$Protocol,

[System.String[]]
$BindingData,

[System.String]
$ApplicationPool
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


#Include logic to
$result = [System.Boolean]
#Add logic to test whether the website is present and its status mathes the supplied parameter values. If it does, return true. If it does not, return false.
$result
}
```

**Poznámka:**: Pro snadnější ladění, použijte **Write-Verbose** rutiny ve vaší implementaci předchozí tři funkce.
>Tato rutina zapíše text do proudu podrobnou zprávu.
>Ve výchozím nastavení, se nezobrazí datový proud podrobnou zprávu, ale je můžete zobrazit tak, že změníte hodnotu **$VerbosePreference** proměnné nebo s použitím **Verbose** parametrů v rutinách DSC = nový.

### <a name="creating-the-module-manifest"></a>Vytváření manifestu modulu

Nakonec použijte **New-ModuleManifest** rutiny k definování <ResourceName>souboru .psd1 pro modul vlastních prostředků. Při vyvolání Tato rutina odkazovat na soubor skriptu modulů (.psm1), je popsáno v předchozí části. Zahrnout **Get-TargetResource**, **Set-TargetResource**, a **testovací TargetResource** v seznamu funkcí pro export. Tady je příklad souboru manifestu.

```powershell
# Module manifest for module 'Demo.IIS.Website'
#
# Generated on: 1/10/2013
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '6AB5ED33-E923-41d8-A3A4-5ADDA2B301DE'

# Author of this module
Author = 'Contoso'

# Company or vendor of this module
CompanyName = 'Contoso'

# Copyright statement for this module
Copyright = 'Contoso. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This Module is used to support the creation and configuration of IIS Websites through Get, Set and Test API on the DSC managed nodes.'

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '4.0'

# Minimum version of the common language runtime (CLR) required by this module
CLRVersion = '4.0'

# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @("WebAdministration")

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @("Demo_IISWebsite.psm1")

# Functions to export from this module
FunctionsToExport = @("Get-TargetResource", "Set-TargetResource", "Test-TargetResource")

# Cmdlets to export from this module
#CmdletsToExport = '*'

# HelpInfo URI of this module
# HelpInfoURI = ''
}
```

## <a name="supporting-psdscrunascredential"></a>Podpora PsDscRunAsCredential

>**Poznámka:** **PsDscRunAsCredential** je podporován v Powershellu 5.0 a novějším.

**PsDscRunAsCredential** vlastnost lze použít v [konfigurací DSC](../configurations/configurations.md) prostředků bloku k určení, prostředku by měl být spuštěny pod zadanou sadu přihlašovacích údajů.
Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](../configurations/runAsUser.md).

Pro přístup k uživatelský kontext z v rámci vlastní prostředek, můžete použít automatické proměnné `$PsDscContext`.

Například následující kód by zápisu uživatelský kontext, ve kterém prostředek běží podrobné výstupního datového proudu:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

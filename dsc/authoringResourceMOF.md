---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Psaní vlastních prostředků DSC s MOF"
ms.openlocfilehash: 58d6ba3995d3d6dea2787cfa347e0b1386bc40af
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a>Psaní vlastních prostředků DSC s MOF

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

V tomto tématu jsme bude definovat schéma pro vlastní prostředek požadovaného stavu aplikace Windows PowerShell (DSC) v souboru MOF a implementovat prostředku v souboru skriptu prostředí Windows PowerShell. Tento vlastní prostředek je pro vytváření a údržbu webu.

## <a name="creating-the-mof-schema"></a>Vytvoření schématu MOF

Schéma definuje vlastnosti prostředku nakonfigurovaný pomocí skriptu, který konfigurace DSC.

### <a name="folder-structure-for-a-mof-resource"></a>Struktura složek pro prostředek MOF

Chcete-li implementovat vlastní prostředek DSC se schématem, MOF, vytvořte následující strukturu složek. Schéma MOF je definována v souboru Demo_IISWebsite.schema.mof a skriptu prostředků je definována v Demo_IISWebsite.psm1. Volitelně můžete vytvořit soubor manifestu (psd1) modulu.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

Všimněte si, že je potřeba vytvořit složku s názvem DSCResources ve složce nejvyšší úrovně a že složka pro každý prostředek, musí mít stejný název jako prostředek.

### <a name="the-contents-of-the-mof-file"></a>Obsah souboru MOF

Následuje příklad MOF souboru, který lze použít pro prostředek vlastní web. Postup popsaný v tomto příkladu, uložit toto schéma do souboru a volání soubor *Demo_IISWebsite.schema.mof*.

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

Vezměte na vědomí následující skutečnosti související předchozí kód:

* `FriendlyName`Definuje název, který slouží k odkazování na tento vlastní prostředek DSC konfigurační skripty. V tomto příkladu `Website` je ekvivalentní popisný název `Archive` pro předdefinované prostředek archivu.
* Třída definujete pro vlastní prostředek musí být odvozeny od `OMI_BaseResource`.
* Kvalifikátor typu `[Key]`na vlastnost značí, že tato vlastnost jednoznačné identifikaci instance prostředku. Alespoň jeden `[Key]` vlastnost je povinná.
* `[Required]` Kvalifikátor označuje, že tato vlastnost je vyžadovaná (musí být zadaná hodnota v konfigurační skript, který používá tento prostředek).
* `[write]` Kvalifikátor označuje, že tato vlastnost je volitelná, při použití vlastního prostředku v konfigurační skript. `[read]` Kvalifikátor označuje, že vlastnost nelze nastavit konfigurace a je pouze pro účely vytváření sestav.
* `Values`omezuje hodnoty, které lze přiřadit k vlastnosti do seznamu hodnot definovaných v `ValueMap`. Další informace najdete v tématu [chybu a hodnota kvalifikátory](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).
* Včetně vlastnost volá `Ensure` s hodnotami `Present` a `Absent` v prostředku se doporučuje jako způsob, jak udržovat konzistentní styl s integrovanou prostředky DSC.
* Název souboru schématu pro vlastní prostředek následujícím způsobem: `classname.schema.mof`, kde `classname` je identifikátor, který následuje `class` – klíčové slovo v vaší definice schématu.

### <a name="writing-the-resource-script"></a>Psaní skriptu prostředků

Skript prostředků implementuje logiku prostředku. V tomto modulu musí obsahovat tři funkce volané **Get-TargetResource**, **Set-TargetResource**, a **Test TargetResource**. Všechny tři funkce vyžaduje sadu parametrů, který je stejný jako sada vlastností, definovaná ve schématu MOF, který jste vytvořili pro prostředek. V tomto dokumentu tato sada vlastností se označuje jako "vlastností prostředku." Úložiště volá tyto tři funkce v souboru <ResourceName>.psm1. V následujícím příkladu funkce jsou uloženy v souboru s názvem Demo_IISWebsite.psm1.

> **Poznámka:**: Když spustíte stejný konfigurační skript na prostředku více než jednou, mělo by se zobrazit žádné chyby a prostředek by měla zůstat v stejného stavu jako jednou spouštění skriptu. K tomu, ujistěte se, že vaše **Get-TargetResource** a **Test TargetResource** funkce nechte beze změny prostředek a že vyvolání **Set-TargetResource**více než jednou v sekvenci s parametrem stejné hodnoty se vždy rovná ho po vyvolání funkce.

V **Get-TargetResource** funkce implementace, použijte vlastnost hodnoty klíče prostředků, které jsou k dispozici jako parametry a zkontrolujte stav instance zadaný prostředek. Tato funkce musí vracet zatřiďovací tabulka, která jsou uvedeny vlastnosti prostředků jako klíče a skutečné hodnoty těchto vlastností jako odpovídající hodnoty. Následující kód představuje příklad.

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
* Aktualizovat existující web
* Odstraňte existující web

Následující příklad znázorňuje to.

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

Nakonec **Test TargetResource** funkce vyžaduje parametr stejné nastavení jako **Get-TargetResource** a **Set-TargetResource**. V implementaci **Test TargetResource**, zkontrolujte stav instance prostředku, který je uveden v parametrech klíče. Pokud skutečný stav instance prostředku neodpovídá hodnot zadaných v sadě parametrů, vrátí **$false**. V opačném vraťte **$true**.

Následující kód implementuje **Test TargetResource** funkce.

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

**Poznámka:**: pro snazší ladění, použijte **Write-Verbose** rutiny v implementaci předchozí tři funkce. 
>Tato rutina zapíše text do proudu podrobnou zprávu. 
>Ve výchozím nastavení, se nezobrazí datový proud podrobné zprávy, ale můžete ji zobrazit tak, že změníte hodnotu **$VerbosePreference** proměnné nebo pomocí **podrobné** parametr rutiny DSC = nový.

### <a name="creating-the-module-manifest"></a>Vytvoření manifestu modulu

Nakonec použijte **New-ModuleManifest** rutiny k definování <ResourceName>.psd1 soubor pro vaše vlastní prostředek modul. Při vyvolání této rutiny, odkazovat na soubor skriptu (.psm1) modul popsané v předchozí části. Zahrnout **Get-TargetResource**, **Set-TargetResource**, a **Test TargetResource** v seznamu funkcí pro export. Následuje příklad souboru manifestu.

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

>**Poznámka:** **PsDscRunAsCredential** je podporována v prostředí PowerShell 5.0 nebo novější.

**PsDscRunAsCredential** vlastnost lze použít v [konfigurace DSC](configurations.md) prostředků bloku určí prostředek by měl být spuštění pod zadanou sadu přihlašovacích údajů.
Další informace najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).

Pro přístup k kontext uživatele z v rámci vlastní prostředek, můžete použít automatické proměnné `$PsDscContext`.

Například následující kód zapíše kontextu uživatele, pod kterým běží prostředku do datového proudu podrobný výstup:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```





---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředky DSC
ms.openlocfilehash: 1f77b5e6630a2e3de6e1d1a05638f94d2df039ae
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046687"
---
# <a name="dsc-resources"></a>Prostředky DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Desired State Configuration (DSC) prostředky poskytují stavební bloky pro konfiguraci DSC. Prostředek zveřejňuje vlastnosti, které může být nakonfigurovaný (schéma) a obsahuje funkce skript Powershellu, která volá místní Configuration Manageru (LCM) aby ",".

Zdroj lze modelovat něco jako obecné jako soubor, nebo co nastavení serveru služby IIS.  Skupiny jako prostředky jsou zkombinované v modulu DSC, která slouží k uspořádání všechny požadované soubory v strukturu, která je přenosná a zahrnuje jejich metadata k určení, jak jsou prostředky určena pro použití.

Každý prostředek má * schéma, které určuje nutné k využití prostředků v syntaxi [konfigurace](../configurations/configurations.md). Schéma zdroje lze definovat takto:

- **"Schema.Mof"** souboru: Definujte většinu prostředků jejich *schématu* v "schema.mof soubor, pomocí [Managed Object Format](/windows/desktop/wmisdk/managed-object-format--mof-).
- **"\<Název prostředku\>. schema.psm1"** souboru: [Složené prostředky](../configurations/compositeConfigs.md) definovat jejich *schématu* v "<ResourceName>. schema.psm1" soubor pomocí [bloku parametrů](/powershell/module/microsoft.powershell.core/about/about_functions?view=powershell-6#functions-with-parameters).
- **"\<Název prostředku\>.psm1"** souboru: Třídy založené na prostředky DSC definovat jejich *schématu* v definici třídy. Syntaxe položky jsou označené jako vlastnosti třídy. Další informace najdete v tématu [about_Classes](/powershell/module/psdesiredstateconfiguration/about/about_classes_and_dsc).

Pokud chcete načíst syntaxe pro prostředek DSC, použijte [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) rutinu s `-Syntax` parametru. Toto použití je podobný používání [Get-Command](/powershell/module/microsoft.powershell.core/get-command) s `-Syntax` parametr zobrazíte Syntaxe rutin. Šablona použitá pro blok prostředků pro prostředek, který zadáte se zobrazí výstup, který se zobrazí.

```powershell
Get-DscResource -Syntax Service
```

Který se zobrazí výstup by měl vypadat přibližně ve výstupu níže, i když tento prostředek syntaxe může v budoucnu změnit. Syntaxe rutin, jako jsou *klíče* viděli v hranatých závorkách jsou volitelné. Typy určete typ dat, který očekává, že každý klíč.

> [!NOTE]
> **Ujistěte se, že** klíč je volitelný, protože výchozí hodnota "K dispozici".

```output
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

V konfiguraci **služby** prostředků bloku může vypadat třeba takto k **Ujistěte se, že** , na kterém běží služba zařazování tisku.

> [!NOTE]
> Před použitím zdroje v konfiguraci, je nutné naimportovat pomocí [Import-DSCResource](../configurations/import-dscresource.md).

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }
    }
}
```

Konfigurace může obsahovat více instancí stejného typu prostředku. Každá instance musí mít jedinečné názvy. V následujícím příkladu druhý **služby** prostředků bloku se přidá do konfigurace služby "DHCP".

```powershell
Configuration TestConfig
{
    # It is best practice to always directly import resources, even if the resource is a built-in resource.
    Import-DSCResource -Name Service
    Node localhost
    {
        # The name of this resource block, can be anything you choose, as long as it is of type [String] as indicated by the schema.
        Service "Spooler:Running"
        {
            Name = "Spooler"
            State = "Running"
        }

        # To configure a second service resource block, add another Service resource block and use a unique name.
        Service "DHCP:Running"
        {
            Name = "DHCP"
            State = "Running"
        }
    }
}
```

> [!NOTE]
> Od v Powershellu 5.0, byl přidán technologie intellisense pro DSC. Tato nová funkce umožňuje používat \<kartu\> a \<kombinace kláves Ctrl + mezerník\> pro automatické dokončování názvů klíčů.

![Prostředek Tab k dokončování příkazů](../media/resource-tabcompletion.png)

## <a name="built-in-resources"></a>Integrované prostředky

Kromě komunitní zdroje jsou integrované prostředky pro Windows, prostředky pro Linux a prostředky pro závislost mezi uzly. Výše uvedené kroky můžete použít k určení syntaxe těchto prostředků a jejich použití. Na stránkách, které slouží tyto prostředky byly archivovány v rámci **odkaz**.

Integrované prostředky pro Windows

* [Prostředek Archive](../reference/resources/windows/archiveResource.md)
* [Prostředek Environment](../reference/resources/windows/environmentResource.md)
* [Prostředek File](../reference/resources/windows/fileResource.md)
* [Prostředek Group](../reference/resources/windows/groupResource.md)
* [Prostředek GroupSet](../reference/resources/windows/groupSetResource.md)
* [Prostředek Log](../reference/resources/windows/logResource.md)
* [Prostředek Package](../reference/resources/windows/packageResource.md)
* [Prostředek ProcessSet](../reference/resources/windows/ProcessSetResource.md)
* [Prostředek Registry](../reference/resources/windows/registryResource.md)
* [Prostředek Script](../reference/resources/windows/scriptResource.md)
* [Prostředek Service](../reference/resources/windows/serviceResource.md)
* [Prostředek ServiceSet](../reference/resources/windows/serviceSetResource.md)
* [Prostředek User](../reference/resources/windows/userResource.md)
* [Prostředek WindowsFeature](../reference/resources/windows/windowsFeatureResource.md)
* [Prostředek WindowsFeatureSet](../reference/resources/windows/windowsFeatureSetResource.md)
* [Prostředek WindowsOptionalFeature](../reference/resources/windows/windowsOptionalFeatureResource.md)
* [Prostředek WindowsOptionalFeatureSet](../reference/resources/windows/windowsOptionalFeatureSetResource.md)
* [WindowsPackageCabResource prostředků](../reference/resources/windows/windowsPackageCabResource.md)
* [Prostředek WindowsProcess](../reference/resources/windows/windowsProcessResource.md)

[Závislost mezi uzly](../configurations/crossNodeDependencies.md) prostředky

* [WaitForAll prostředků](../reference/resources/windows/waitForAllResource.md)
* [WaitForSome prostředků](../reference/resources/windows/waitForSomeResource.md)
* [WaitForAny prostředků](../reference/resources/windows/waitForAnyResource.md)

Balíček správy prostředků

* [PackageManagement prostředků](../reference/resources/packagemanagement/PackageManagementDscResource.md)
* [PackageManagementSource prostředků](../reference/resources/packagemanagement/PackageManagementSourceDscResource.md)

Prostředky pro Linux

* [Prostředek Linux Archive](../reference/resources/linux/lnxArchiveResource.md)
* [Zdroje prostředí Linux](../reference/resources/linux/lnxEnvironmentResource.md)
* [Linux FileLine prostředků](../reference/resources/linux/lnxFileLineResource.md)
* [Linuxový soubor prostředků](../reference/resources/linux/lnxFileResource.md)
* [Linuxové skupiny prostředků](../reference/resources/linux/lnxGroupResource.md)
* [Prostředek Linux Package](../reference/resources/linux/lnxPackageResource.md)
* [Prostředek Linux Script](../reference/resources/linux/lnxScriptResource.md)
* [Prostředek služby Linux](../reference/resources/linux/lnxServiceResource.md)
* [Linux SshAuthorizedKeys prostředků](../reference/resources/linux/lnxSshAuthorizedKeysResource.md)
* [Prostředek uživatele Linuxu](../reference/resources/linux/lnxUserResource.md)

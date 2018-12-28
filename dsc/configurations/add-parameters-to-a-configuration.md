---
ms.date: 12/12/2018
keywords: DSC, powershell, zdroj, galerie, instalační program
title: Přidání parametrů ke konfiguraci
ms.openlocfilehash: 15213404f0cdd6416baf1f83af91b8f5279cc97f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403725"
---
# <a name="add-parameters-to-a-configuration"></a>Přidání parametrů ke konfiguraci

Funkce, jako jsou [konfigurace](configurations.md) může být parametrizován umožňující dynamičtějších konfigurace na základě uživatelského zadání. Postup je podobný jako postup popsaný v [funkce s parametry](/powershell/module/microsoft.powershell.core/about/about_functions).

Tento příklad začíná základní konfigurace, který konfiguruje službu "Zařazování" k "Spuštěna".

```powershell
Configuration TestConfig
{
    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}
```

## <a name="built-in-configuration-parameters"></a>Integrované parametry konfigurace

Na rozdíl od funkce však [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) atribut přidá žádné funkce. Kromě [společné parametry](/powershell/module/microsoft.powershell.core/about/about_commonparameters), konfigurace můžete použít také následující předdefinované parametrů, aniž by bylo potřeba jejich definování.

|Parametr  |Popis  |
|---------|---------|
|`-InstanceName`|Použít při definování [složené konfigurace](compositeconfigs.md)|
|`-DependsOn`|Použít při definování [složené konfigurace](compositeconfigs.md)|
|`-PSDSCRunAsCredential`|Použít při definování [složené konfigurace](compositeconfigs.md)|
|`-ConfigurationData`|Sloužící k předávání v strukturované [konfigurační Data](configData.md) pro použití v konfiguraci.|
|`-OutputPath`|Umožňuje určit, kde vaše "\<computername\>MOF" soubor bude zkompilována.|

## <a name="adding-your-own-parameters-to-configurations"></a>Přidání vlastní parametry konfigurace

Kromě předdefinovaných parametry můžete také přidat vlastní parametry do vaší konfigurace. Blok parametrů přejde přímo uvnitř deklarace konfigurace, stejně jako funkce. Blok parametr konfigurace by měla být mimo všechny **uzel** deklarace a výše žádné *importovat* příkazy. Přidáním parametrů můžete provést konfiguraci robustní a dynamické.

```powershell
Configuration TestConfig
{
    param
    (

    )
```

### <a name="add-a-computername-parameter"></a>Přidat parametr ComputerName

První parametr, můžete přidat je `-Computername` parametrů, takže můžete dynamicky kompilovat soubor "MOF" pro všechny `-Computername` předáte do vaší konfigurace. Podobně jako funkce můžete také definovat výchozí hodnotu v případě, že uživatel nepředáte hodnotu `-ComputerName`

```powershell
param
(
    [String]
    $ComputerName="localhost"
)
```

V rámci konfigurace, můžete pak určit váš `-ComputerName` parametr při definování vašeho uzlu bloku.

```powershell
Node $ComputerName
{

}
```

### <a name="calling-your-configuration-with-parameters"></a>Konfigurace s parametry volání

Po přidání parametrů do vaší konfigurace, můžete je použít stejným způsobem, jako byste to pomocí rutiny.

```powershell
TestConfig -ComputerName "server01"
```

### <a name="compiling-multiple-mof-files"></a>Kompilování více soubory MOF

Blok uzel můžete také přijmout čárkou oddělený seznam názvů počítačů a bude generovat soubory ".mof" pro každý. Spustíte podle následujícího příkladu lze generovat soubory ".mof" pro všechny počítače, které jsou předány `-ComputerName` parametru.

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ComputerName="localhost"
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}

TestConfig -ComputerName "server01", "server02", "server03"
```

## <a name="advanced-parameters-in-configurations"></a>Pokročilé parametry v konfiguracích

Kromě `-ComputerName` parametr, můžeme přidat parametry pro název služby a stav. Následující příklad přidá parametr blok s `-ServiceName` parametr a použije ho a dynamicky tak definovat **služby** prostředků bloku. Přidá také `-State` parametrů a dynamicky tak definovat **stavu** v **služby** prostředků bloku.

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ServiceName,

        [String]
        $State,

        [String]
        $ComputerName="localhost"
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

> [!NOTE]
> Ve více scénářích advacned, může mít více smysl přesunout dynamických dat do strukturované [konfigurační Data](configData.md).

Příklad konfigurace nyní přijímá dynamickou `$ServiceName`, ale pokud není zadaná, kompilaci za následek chybu. Můžete přidat výchozí hodnotu jako v tomto příkladu.

```powershell
[String]
$ServiceName="Spooler"
```

V tomto případě však smysl další jednoduše nutí uživatele zadat hodnotu `$ServiceName` parametru. `parameter` Atribut umožňuje přidat další ověření a kanál podpory vaší konfigurace parametrů.

Nad všechny deklarace parametru přidejte `parameter` bloku atributu stejně jako v následujícím příkladu.

```powershell
[parameter()]
[String]
$ServiceName
```

Lze zadat argumenty u každého `parameter` atribut pro řízení aspektů definovaný parametr. Následující příklad provede `$ServiceName` **povinné** parametru.

```powershell
[parameter(Mandatory)]
[String]
$ServiceName
```

Pro `$State` parametr, rádi bychom zabrání uživateli v zadávání hodnoty mimo sadu předdefinovaných (jako je spuštění, zastavení) `ValidationSet*`atributu by zabrání uživateli v zadávání hodnoty mimo sadu předdefinovaných (jako je spuštění, Zastavit). Následující příklad přidá `ValidationSet` atribut `$State` parametru. Protože jsme nechcete, aby `$State` parametr **povinné**, budeme muset přidat výchozí hodnotu pro něj.

```powershell
[ValidateSet("Running", "Stopped")]
[String]
$State="Running"
```

> [!NOTE]
> Není potřeba zadat `parameter` atribut při použití `validation` atribut.

Další informace o `parameter` a atributů ověření v [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters.md).

## <a name="fully-parameterized-configuration"></a>Plně parametry konfigurace

Teď máme parametry konfigurace, která vynutí, aby uživatel zadal `-InstanceName`, `-ServiceName`a ověří `-State` parametru.

```powershell
Configuration TestConfig
{
    param
    (
        [parameter(Mandatory)]
        [String]
        $ServiceName,

        [ValidateSet("Running","Stopped")]
        [String]
        $State="Running",

        [String]
        $ComputerName="localhost",
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

## <a name="see-also"></a>Viz taky

- [Zápis nápovědy ke konfiguracím DSC](configHelp.md)
- [Dynamická konfigurace](flow-control-in-configurations.md)
- [Použití konfiguračních dat ve vašich konfiguracích](configData.md)
- [Samostatná data pro konfiguraci a prostředí](separatingEnvData.md)

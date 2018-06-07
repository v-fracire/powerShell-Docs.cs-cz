---
ms.date: 06/20/2018
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: PackageManagement prostředek DSC
ms.openlocfilehash: 3d52934b130d59acee4d7f8a92da2c743c1eb305
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753783"
---
# <a name="dsc-packagemanagement-resource"></a>PackageManagement prostředek DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, 5.1 prostředí Windows PowerShell

**PackageManagement** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků správy balíčků na cílový uzel. Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.

> [!IMPORTANT]
> **PackageManagement** modulu by měla být minimálně verze 1.1.7.0 následující vlastnost informace správné.

## <a name="syntax"></a>Syntaxe

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [AdditionalParameters = [HashTable]]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [MaximumVersion = [string]]
    [MinimumVersion = [string]]
    [ProviderName = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [RequiredVersion = [string]]
    [Source = [string]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Název| Určuje název balíčku, který má být nainstalována nebo odinstalována.|
| Další_parametry| Zprostředkovatel konkrétní zatřiďovací tabulku parametrů, které by byly předány `Get-Package -AdditionalArguments`. Například pro zprostředkovatele NuGet můžete předat další parametry, jako je Cílová_cesta.|
| Ujistěte se| Určuje, zda balíček má být nainstalována nebo odinstalována.|
| MaximumVersion|Určuje maximální povolený verze balíčku, který chcete najít. Pokud tento parametr nepřidáte, prostředek vyhledá nejvyšší dostupné verze balíčku.|
| MinimumVersion|Určuje minimální povolená verzi balíčku, který chcete najít. Pokud tento parametr je nemůžete přidat, prostředek vyhledá nejvyšší dostupné verze balíčku, který také splňuje všechny maximální zadaná verze určeného _MaximumVersion_ parametr.|
| ProviderName| Určuje název zprostředkovatele balíček do které chcete obor vyhledávání balíčku. Název zprostředkovatele balíček můžete získat spuštěním `Get-PackageProvider` rutiny.|
| RequiredVersion| Určuje přesnou verzi balíčku, který chcete nainstalovat. Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje na nejnovější dostupnou verzi balíčku, který také splňuje všechny maximální verze zadaná v _MaximumVersion_ parametr.|
| Zdroj| Určuje název zdroje balíčku, které lze nalézt balíček. To může být identifikátor URI nebo zdroj zaregistrována `Register-PackageSource` nebo prostředek PackageManagementSource DSC.|
| SourceCredential | Určuje uživatelský účet, který má práva pro instalaci balíčku pro zadaný balíček zprostředkovatele nebo zdroje.|

## <a name="additional-parameters"></a>Další parametry

V následující tabulce je uveden seznam možností pro vlastnost Další_parametry.
|  Parametr  | Popis   |
|---|---|
| Cílová_cesta| Používá zprostředkovatele například předdefinované zprostředkovatele Nuget. Určuje umístění souboru, kam chcete balíček, který má být nainstalován.|
| InstallationPolicy| Používá zprostředkovatele například předdefinované zprostředkovatele Nuget. Určuje, zda je důvěryhodné zdroje balíčku. Jeden z: "Nedůvěryhodná", "Důvěryhodné".|

## <a name="example"></a>Příklad

Tento příklad nainstaluje **JQuery** balíček NuGet a **GistProvider** pomocí modulu prostředí PowerShell **PackageManagement** prostředek DSC. Tento příklad nejprve zajišťuje zdroje požadovaný balíček jsou k dispozici, pak definuje očekávaný stav **JQuery** a **GistProvider** balíčky (NuGet a prostředí PowerShell, v uvedeném pořadí).

```powershell
Configuration PackageTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagementSource PSGallery
    {
        Ensure      = "Present"
        Name        = "psgallery"
        ProviderName= "PowerShellGet"
        SourceLocation   = "https://www.powershellgallery.com/api/v2/"
        InstallationPolicy ="Trusted"
    }

    PackageManagement NugetPackage
    {
        Ensure               = "Present"
        Name                 = "JQuery"
        AdditionalParameters = "$env:HomeDrive\nuget"
        RequiredVersion      = "2.0.1"
        DependsOn            = "[PackageManagementSource]SourceRepository"
    }

    PackageManagement PSModule
    {
        Ensure               = "Present"
        Name                 = "gistprovider"
        Source               = "PSGallery"
        DependsOn            = "[PackageManagementSource]PSGallery"
    }
}
```
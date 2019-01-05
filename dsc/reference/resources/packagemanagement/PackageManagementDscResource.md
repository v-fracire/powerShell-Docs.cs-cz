---
ms.date: 06/20/2018
keywords: DSC, powershell, konfigurace, instalační program
title: PackageManagement prostředků DSC
ms.openlocfilehash: 18cbbfe0715c82dcfdf4a5fb6ee36ee814e43d3b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048159"
---
# <a name="dsc-packagemanagement-resource"></a>PackageManagement prostředků DSC

Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, prostředí Windows PowerShell 5.1

**PackageManagement** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčku správy balíčků na cílový uzel. Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z [ http://PowerShellGallery.com ](http://PowerShellGallery.com).

> [!IMPORTANT]
> **PackageManagement** modul by měl být dlouhý aspoň verzi 1.1.7.0 pro následující vlastnost informace správné.

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

| Vlastnost | Popis |
| --- | --- |
| Name| Určuje název balíčku, který má být nainstalována nebo odinstalována.|
| Další_parametry| Zprostředkovatel konkrétní zatřiďovací tabulku parametrů, které by byly předány `Get-Package -AdditionalArguments`. Například pro zprostředkovatele NuGet můžete předat další parametry, jako je DestinationPath.|
| Zkontrolujte| Určuje, zda balíček nainstalovat nebo odinstalovat.|
| MaximumVersion|Určuje maximální povolenou verzi balíčku, který má být nalezena. Pokud nemůžete přidat tento parametr, vyhledá prostředek nejvyšší dostupnou verzi balíčku.|
| MinimumVersion|Určuje minimální povolenou verzi balíčku, který má být nalezena. Pokud nemůžete přidat tento parametr, prostředek vyhledá nejvyšší dostupnou verzi balíčku, který také splňuje všechny maximální zadaná verze určená _MaximumVersion_ parametru.|
| ProviderName| Určuje název zprostředkovatele balíček do kterého chcete omezit rozsah hledání balíčku. Názvy balíčků zprostředkovatele můžete získat spuštěním `Get-PackageProvider` rutiny.|
| RequiredVersion| Určuje přesnou verzi balíčku, který chcete nainstalovat. Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje na nejnovější dostupnou verzi balíčku, který také splňuje všechny maximální verze určená _MaximumVersion_ parametru.|
| Zdroj| Určuje název zdroje balíčku, kde můžete najít balíček. Může to být buď identifikátor URI nebo zdroj zaregistrovaného `Register-PackageSource` nebo prostředek DSC PackageManagementSource.|
| SourceCredential | Určuje uživatelský účet, který má oprávnění k instalaci balíčku pro zadaný balíček poskytovatele nebo zdroj.|

## <a name="additional-parameters"></a>Další parametry

V následující tabulce jsou uvedeny možnosti pro vlastnost Další_parametry.

| Parametr | Popis |
| --- | --- |
| DestinationPath| Použít poskytovatelé jako je předdefinovaný poskytovatel Nuget. Určuje umístění souboru, kam chcete balíček nainstalovat.|
| InstallationPolicy| Použít poskytovatelé jako je předdefinovaný poskytovatel Nuget. Určuje, zda důvěřujete zdroje balíčku. Jeden z: `Untrusted`, `Trusted`.|

## <a name="example"></a>Příklad

Tento příklad nainstaluje **JQuery** balíčku NuGet a **GistProvider** pomocí modulu PowerShell **PackageManagement** prostředků DSC. V tomto příkladu nejdřív zajišťuje zdroje požadovaný balíček jsou k dispozici, pak určuje očekávaný stav **JQuery** a **GistProvider** balíčky (NuGet a prostředí PowerShell, v uvedeném pořadí).

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
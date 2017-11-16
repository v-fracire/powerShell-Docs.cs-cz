---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "PackageManagement prostředek DSC"
ms.openlocfilehash: a984fbf5db561a696d89b60dde8b92096c6e4924
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-packagemanagement-resource"></a>PackageManagement prostředek DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**PackageManagement** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků správy balíčků na cílový uzel. Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.

## <a name="syntax"></a>Syntaxe

```
PackageManagement [string] #ResourceName
{
    Name = [string]
    [ Source = [string] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ RequiredVersion = [string] ]
    [ MinimumVersion = [string] ]
    [ MaximumVersion = [string] ]
    [ SourceCredential = [PSCredential] ]
    [ ProviderName = [string] ]
    [ AdditionalParameters = [Microsoft.Management.Infrastructure.CimInstance[]] ]
}
```

## <a name="properties"></a>Properties
|  Vlastnost  |  Popis   | 
|---|---| 
| Název| Určuje název balíčku, který má být nainstalována nebo odinstalována.| 
| Zdroj| Určuje název zdroje balíčku, které lze nalézt balíček. To může být identifikátor URI nebo zdroj zaregistrována Register-PackageSource nebo PackageManagementSource DSC prostředek. Prostředek DSC MSFT_PackageManagementSource taky moct registrovat zdroj balíčku.| 
| Ujistěte se| Určuje, zda balíček má být nainstalována nebo odinstalována.| 
| RequiredVersion| Určuje přesnou verzi balíčku, který chcete nainstalovat. Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje na nejnovější dostupnou verzi balíčku, který splňuje všechny maximální verze zadaná v parametru MaximumVersion rovněž.| 
| MinimumVersion| Určuje minimální povolená verzi balíčku, který chcete nainstalovat. Pokud tento parametr, tento intalls prostředků DSC nejvyšší dostupné verze balíčku, který splňuje všechny maximální zadaná verze zadané parametrem MaximumVersion rovněž nepřidávejte.| 
| MaximumVersion| Určuje maximální povolený verze balíčku, který chcete nainstalovat. Pokud tento parametr nezadáte, tento prostředek DSC nainstaluje nejvyšší číslované dostupná verze balíčku.| 
| SourceCredential | Určuje uživatelský účet, který má práva pro instalaci balíčku pro zadaný balíček zprostředkovatele nebo zdroje.| 
| ProviderName| Určuje název zprostředkovatele balíček do které chcete obor vyhledávání balíčku. Název zprostředkovatele balíček můžete získat spuštěním rutiny Get-PackageProvider.| 
| Další_parametry| Zprostředkovatel konkrétní parametry, které jsou předány jako zatřiďovací tabulky. Například pro zprostředkovatele NuGet můžete předat další parametry, jako je Cílová_cesta.| 

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
        SourceUri   = "http://nuget.org/api/v2/"   
        InstallationPolicy ="Trusted" 
    }    
    
    PackageManagementSource PSGallery 
    { 
        Ensure      = "Present" 
        Name        = "psgallery" 
        ProviderName= "PowerShellGet" 
        SourceUri   = "https://www.powershellgallery.com/api/v2/"   
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


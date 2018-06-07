---
ms.date: 06/20/2018
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: PackageManagementSource prostředek DSC
ms.openlocfilehash: 5d049b05c387cafe27edb202d569852b10852dce
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/04/2018
ms.locfileid: "34753766"
---
# <a name="dsc-packagemanagementsource-resource"></a>PackageManagementSource prostředek DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, 5.1 prostředí Windows PowerShell

**PackageManagementSource** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro zaregistrovat nebo zrušit registraci zdroje správy balíčků na cílový uzel. **Balíček správy zdroje registrované tímto způsobem je zaregistrovaný v kontextu systému, použít účet System nebo modul DSC.** Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.

> [!IMPORTANT]
> **PackageManagement** modulu by měla být minimálně verze 1.1.7.0 následující vlastnost informace správné.

## <a name="syntax"></a>Syntaxe

```
PackageManagementSource [String] #ResourceName
{
    Name = [string]
    ProviderName = [string]
    SourceLocation = [string]
    [DependsOn = [string[]]]
    [Ensure = [string]{ Absent | Present }]
    [InstallationPolicy = [string]{ Trusted | Untrusted }]
    [PsDscRunAsCredential = [PSCredential]]
    [SourceCredential = [PSCredential]]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Název| Určuje název zdroje balíčku, který má být zaregistrován nebo zrušit její registraci v systému.|
| ProviderName| Určuje název zprostředkovatele OneGet, pomocí kterého můžete Interoperabilita s zdroji balíčku.|
| SourceLocation| Určuje identifikátor URI zdroje balíčku.|
| Ujistěte se| Určuje, zda zdroj balíčku má být zaregistrován nebo zrušit její registraci.|
| InstallationPolicy| Používá zprostředkovatele například předdefinované zprostředkovatele Nuget. Určuje, zda je důvěryhodné zdroje balíčku. Jeden z: "Nedůvěryhodná", "Důvěryhodné".|
| SourceCredential| Poskytuje přístup k balíčku na vzdáleného zdroje.|

## <a name="example"></a>Příklad

Zaregistruje v tomto příkladu http://nuget.org zdroje balíčku pomocí **PackageManagementSource** prostředek DSC.

```powershell
Configuration PackageManagementSourceTest
{
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present"
        Name        = "MyNuget"
        ProviderName= "Nuget"
        SourceLocation   = "http://nuget.org/api/v2/"
        InstallationPolicy ="Trusted"
    }
}
```
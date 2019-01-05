---
ms.date: 06/20/2018
keywords: DSC, powershell, konfigurace, instalační program
title: PackageManagementSource prostředků DSC
ms.openlocfilehash: e51b5318288bef458567dd4b58d17caaea3ed69b
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048113"
---
# <a name="dsc-packagemanagementsource-resource"></a>PackageManagementSource prostředků DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0, prostředí Windows PowerShell 5.1

**PackageManagementSource** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zaregistrovat nebo zrušit registraci balíčku správy zdrojů na cílový uzel. **Balíček správy zdrojů zaregistrovaných tímto způsobem jsou registrovány v kontextu systému, použít systémový účet nebo modulem DSC.** Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.

> [!IMPORTANT]
> **PackageManagement** modul by měl být dlouhý aspoň verzi 1.1.7.0 pro následující vlastnost informace správné.

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
| Name| Určuje název balíčku zdroj, který má být registrováno nebo Odregistrováno ve vašem systému.|
| ProviderName| Určuje název zprostředkovatel oneget pro balíčky, pomocí kterého můžete zprostředkovatele komunikace s objekty zdroji balíčku.|
| SourceLocation| Určuje identifikátor URI zdroje balíčku.|
| Zkontrolujte| Určuje, zda zdroj balíčku registrováno nebo odregistrováno.|
| InstallationPolicy| Použít poskytovatelé jako je předdefinovaný poskytovatel Nuget. Určuje, zda důvěřujete zdroje balíčku. Jedna z: "Nedůvěryhodné", "důvěryhodné".|
| SourceCredential| Poskytuje přístup k balíčku na vzdáleného zdroje.|

## <a name="example"></a>Příklad

Registruje v tomto příkladu http://nuget.org pomocí zdroje balíčku **PackageManagementSource** prostředků DSC.

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
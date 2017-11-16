---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "PackageManagementSource prostředek DSC"
ms.openlocfilehash: 80d157aff5bf7685a797baaf6a26215f02473096
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-packagemanagementsource-resource"></a>PackageManagementSource prostředek DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**PackageManagementSource** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro zaregistrovat nebo zrušit registraci zdroje správy balíčků na cílový uzel. **Balíček správy zdroje registrované tímto způsobem je zaregistrovaný v kontextu systému, použít účet System nebo modul DSC.** Vyžaduje tento prostředek **PackageManagement** modulu, k dispozici z http://PowerShellGallery.com.

## <a name="syntax"></a>Syntaxe

```
PSModule [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ InstallationPolicy = [string] ]
    [ ProviderName = [string] ]
    [ SourceUri = [string] ]
    [ SourceCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Properties
|  Vlastnost  |  Popis   | 
|---|---| 
| Název| Určuje název zdroje balíčku, který má být zaregistrován nebo zrušit její registraci v systému.| 
| Ujistěte se| Určuje, zda zdroj balíčku má být zaregistrován nebo zrušit její registraci.| 
| InstallationPolicy| Určuje, zda je zdroj balíčku důvěryhodný. Jeden z: "Nedůvěryhodná", "Důvěryhodné".| 
| ProviderName| Určuje název zprostředkovatele OneGet, pomocí kterého můžete Interoperabilita s zdroji balíčku.| 
| SourceUri| Určuje identifikátor URI zdroje balíčku.| 
| SourceCredential| Poskytuje přístup k balíčku na vzdáleného zdroje.| 

## <a name="example"></a>Příklad

Tento příklad zaregistruje zdrojový balíček http://nuget.org pomocí **PackageManagementSource** prostředek DSC.

```powershell
Configuration PackageManagementSourceTest
{    
    PackageManagementSource SourceRepository
    {
        Ensure      = "Present" 
        Name        = "MyNuget" 
        ProviderName= "Nuget" 
        SourceUri   = "http://nuget.org/api/v2/"   
        InstallationPolicy ="Trusted" 
    }
}
```


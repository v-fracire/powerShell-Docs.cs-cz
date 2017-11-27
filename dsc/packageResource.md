---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC balíček"
ms.openlocfilehash: f7bcbd387db422037614feee7c4a00d93b3cec4e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-package-resource"></a>Prostředek DSC balíček

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**Balíček** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků, například balíčků Instalační služby systému Windows a setup.exe, na cílový uzel.

## <a name="syntax"></a>Syntaxe

```
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ ReturnCode = [UInt32[]] ]
}
```

## <a name="properties"></a>Properties
|  Vlastnost  |  Popis   | 
|---|---| 
| Název| Určuje název balíčku, pro které chcete zajistit určitý stav.| 
| Cesta| Určuje cestu, na kterém se nachází balíček.| 
| productId| Určuje ID produktu, který jedinečně identifikuje balíčku.| 
| Argumenty| Zobrazí řetězec argumenty, které se předá do balíčku přesně tak, jak zadat.| 
| přihlašovací údaje| Poskytuje přístup k balíčku na vzdáleného zdroje. Tato vlastnost se používá k instalaci balíčku. Balíček je vždy nainstalován v místním systému.| 
| Ujistěte se| Určuje, zda je nainstalován balíček. Nastavením této vlastnosti "Chybí" zajistěte, aby byl že balíček není nainstalovaný (nebo má být balíček odinstalován, je-li nainstalován). Nastavte tak, aby "Prezentovat" (výchozí hodnota) ujistěte se, že je balíček nainstalován.| 
| LogPath| Určuje úplnou cestu, kam chcete zprostředkovatele, který má uložit soubor protokolu instalace a odinstalace balíčku.| 
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba **ResourceName** a její typ je **ResourceType**, syntaxe pro používání této vlastnosti je ' DependsOn = "[ Typ prostředku] ResourceName"".| 
| ReturnCode| Označuje očekávaný návratový kód. Pokud skutečnou návratový kód neodpovídá očekávané hodnotě zadané tady že konfigurace vrátí chybu.| 

## <a name="example"></a>Příklad

Tento příklad spustí instalační program MSI, který se nachází v zadané cestě a má zadaný produkt ID.

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    } 
}
```


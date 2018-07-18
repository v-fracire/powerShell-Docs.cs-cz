---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC balíček
ms.openlocfilehash: 3046ba7d57776a996a0b917348a0e863db6cd0c8
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093799"
---
# <a name="dsc-package-resource"></a>Prostředek DSC balíček

> Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**Balíčku** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků, jako jsou například balíčky Instalační služby systému Windows a setup.exe, na cílový uzel.

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
| Cesta| Určuje cestu, kde se nachází balíček.|
| productId| Určuje ID produktu, který jednoznačně identifikuje balíček.|
| Argumenty| Seznam argumentů, které se předají do balíčku přesně tak, jak zadat řetězec.|
| Přihlašovací údaje| Poskytuje přístup k balíčku na vzdáleného zdroje. Tato vlastnost se používá k instalaci balíčku. Balíček je vždy nainstalován v místním systému.|
| Zkontrolujte| Určuje, zda je nainstalován balíček. Nastavte tuto vlastnost na "Chybí" Ujistěte se, že balíček není nainstalovaný, (nebo odinstalovat balíček, je-li nainstalován). Nastavte tak, aby "Předložit" (výchozí hodnota) ujistěte se, že je balíček nainstalován.|
| LogPath| Určuje úplnou cestu, kam chcete poskytovatele za účelem uložení souboru protokolu instalace nebo odinstalace balíčku.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je "DependsOn ="[ ResourceName ResourceType]"".|
| ReturnCode| Označuje očekávaný návratový kód. Pokud skutečný návratový kód neodpovídá očekávané hodnotě. k dispozici tady, že konfiguraci, vrátí se chyba.|

## <a name="example"></a>Příklad

Tento příklad se spustí instalační program MSI, který se nachází v zadané cestě a má zadaný kód product ID.

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
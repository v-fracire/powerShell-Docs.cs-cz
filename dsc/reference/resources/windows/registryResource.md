---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Registry DSC
ms.openlocfilehash: e0ae1a4a27edc08c4e6ccd47786426917eb1ccb4
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048161"
---
# <a name="dsc-registry-resource"></a>Prostředek Registry DSC

_Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_

**Registru** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě klíčů registru a hodnoty na cílový uzel.

## <a name="syntax"></a>Syntaxe

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Present | Absent }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a>Properties

| Vlastnost | Popis |
| --- | --- |
| Klávesa| Označuje cestu klíče registru, pro které chcete zajistit určitý stav. Tato cesta musí obsahovat hive.|
| Název hodnoty| Určuje název hodnoty registru. Přidání nebo odebrání určitého klíče registru, zadejte tuto vlastnost jako prázdný řetězec bez předchozího určení ValueType nebo data. Chcete-li upravit nebo odebrat výchozí hodnota klíče registru, tuto vlastnost zadávejte jako prázdný řetězec při zadávání také ValueType nebo data.|
| Zkontrolujte| Označuje, zda existují klíče a hodnoty. Aby bylo zajištěno, že dělají, nastavte tuto vlastnost na "K dispozici". Aby bylo zajištěno, že neexistují, nastavte vlastnost na "Chybí". Výchozí hodnota je "K dispozici".|
| Force| Pokud zadaný klíč registru je k dispozici, **platnost** přepíšete novou hodnotou. Pokud se odstranění klíče registru s podklíčích, musí se jednat **$true** |
| Hex| Označuje, pokud se data vyjadřují v šestnáctkovém formátu. Je-li zadána, data hodnotu DWORD/QWORD se zobrazují v šestnáctkovém formátu. Není platný pro jiné typy. Výchozí hodnota je **$false**.|
| DependsOn| Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Data| Data pro hodnotu registru.|
| ValueType| Určuje typ hodnoty. Podporované typy jsou: Řetězce (REG_SZ), binární soubor (REG binární soubor), Dword 32 bitů (REG_DWORD), Qword 64-bit (REG_QWORD), víceřetězcovou (REG_MULTI_SZ), Rozšiřitelná řetězcová (REG_EXPAND_SZ) |

## <a name="example"></a>Příklad

Tento příklad zajistí, že klíč s názvem "ExampleKey" je k dispozici v **HKEY\_místní\_počítač** hive.

```powershell
Configuration RegistryTest
{
    Registry RegistryExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Key         = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
        ValueName   = "TestValue"
        ValueData   = "TestData"
    }
}
```

> [!NOTE]
> Změna nastavení v registru `HKEY\CURRENT\USER` hive vyžaduje, že konfigurace spouští pomocí přihlašovacích údajů uživatele, nikoli jako systém. Můžete použít **PsDscRunAsCredential** vlastnosti a určit přihlašovací údaje uživatele pro danou konfiguraci. Příklad najdete v tématu [DSC spuštěná s pověřeními uživatele](../../../configurations/runAsUser.md).

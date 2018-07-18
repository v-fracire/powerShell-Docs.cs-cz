---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Registry DSC
ms.openlocfilehash: b77710d7a6fc599949e78c17af309ad88a1a0872
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093581"
---
# <a name="dsc-registry-resource"></a>Prostředek Registry DSC

> Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

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

|  Vlastnost  |  Popis   |
|---|---|
| Klávesa| Označuje cestu klíče registru, pro které chcete zajistit určitý stav. Tato cesta musí obsahovat hive.|
| Název hodnoty| Určuje název hodnoty registru. Přidání nebo odebrání určitého klíče registru, zadejte tuto vlastnost jako prázdný řetězec bez předchozího určení ValueType nebo data. Chcete-li upravit nebo odebrat výchozí hodnota klíče registru, tuto vlastnost zadávejte jako prázdný řetězec při zadávání také ValueType nebo data.|
| Zkontrolujte| Označuje, zda existují klíče a hodnoty. Aby bylo zajištěno, že dělají, nastavte tuto vlastnost na "K dispozici". Aby bylo zajištěno, že neexistují, nastavte vlastnost na "Chybí". Výchozí hodnota je "K dispozici".|
| Force| Pokud zadaný klíč registru je k dispozici, **platnost** přepíšete novou hodnotou. Pokud se odstranění klíče registru s podklíčích, musí se jednat **$true** |
| Hex| Označuje, pokud se data vyjadřují v šestnáctkovém formátu. Je-li zadána, data hodnotu DWORD/QWORD se zobrazují v šestnáctkovém formátu. Není platný pro jiné typy. Výchozí hodnota je **$false**.|
| DependsOn| Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.|
| Data| Data pro hodnotu registru.|
| ValueType| Určuje typ hodnoty. Podporované typy jsou: řetězce (REG_SZ), binární soubor (REG binární soubor), Dword 32 bitů (REG_DWORD), Qword 64-bit (REG_QWORD), víceřetězcovou (REG_MULTI_SZ), Rozšiřitelná řetězcová (REG_EXPAND_SZ) |

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
> Změna nastavení v registru **HKEY\_aktuální\_uživatele** hive vyžaduje, že konfigurace spouští pomocí přihlašovacích údajů uživatele, nikoli jako systém. Můžete použít **PsDscRunAsCredential** vlastnosti a určit přihlašovací údaje uživatele pro danou konfiguraci. Příklad najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).
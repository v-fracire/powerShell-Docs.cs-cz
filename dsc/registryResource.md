---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC registru"
ms.openlocfilehash: 1e73e4275c0d9db5d8fac7641514ea8190f719ca
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-registry-resource"></a>Prostředek DSC registru

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

**Registru** prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro správu klíčů registru a hodnoty na cílový uzel.

## <a name="syntax"></a>Syntaxe

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Enable | Disable }  ]
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
| Klávesa| Určuje cestu klíč registru, pro které chcete zajistit určitý stav. Tato cesta musí obsahovat podregistr.| 
| ValueName| Určuje název hodnoty registru. Chcete-li přidat nebo odebrat klíč registru, zadejte tuto vlastnost jako prázdný řetězec bez zadání ValueType nebo data. Změnit nebo odebrat výchozí hodnota klíče registru, zadejte tuto vlastnost při zadávání také ValueType nebo data jako prázdný řetězec.| 
| Ujistěte se| Určuje, zda existují klíč a hodnotu. Aby se zajistilo, že udělají, nastavte tuto vlastnost na "Dispozici". Aby se zajistilo, že neexistují, nastavte vlastnost na "Chybí". Výchozí hodnota je "Dispozici".| 
| Force| Pokud zadaný klíč registru existuje, __Force__ přepíše s novou hodnotou. Pokud odstraníte klíč registru s podklíče, musí se jednat __$true__| 
| Hex| Označuje, pokud budou data vyjádřeny v šestnáctkovém formátu. -Li zadána, data hodnotu DWORD nebo QWORD jsou zobrazena v šestnáctkovém formátu. Pro jiné typy není platná. Výchozí hodnota je __$false__.| 
| dependsOn| Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.| 
| ValueData| Data pro hodnotu registru.| 
| ValueType| Označuje typ hodnoty. Podporované typy jsou: 
<ul><li>Řetězec (REG_SZ)</li>


<li>Binární (REG binární)</li>


<li>DWORD 32-bit (REG_DWORD)</li>


<li>Qword 64-bit (REG_QWORD)</li>


<li>Víceřetězcovou (REG_MULTI_SZ)</li>


<li>Rozšíření řetězce (REG_EXPAND_SZ)</li></ul>

## <a name="example"></a>Příklad
Tento příklad zajišťuje, že klíč s názvem "ExampleKey" součástí **HKEY\_místní\_počítač** hive.
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

>**Poznámka:** Změna nastavení registru **HKEY\_aktuální\_uživatele** hive vyžaduje, že konfigurace bude spuštěna s pověřeními uživatele, nikoli jako systém.
>Můžete použít **PsDscRunAsCredential** vlastnosti a určit přihlašovací údaje uživatele pro danou konfiguraci. Příklad, naleznete v části [DSC spuštěná s pověřeními uživatele](runAsUser.md)




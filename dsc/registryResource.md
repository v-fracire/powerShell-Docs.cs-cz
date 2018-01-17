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
# <a name="dsc-registry-resource"></a><span data-ttu-id="2b055-103">Prostředek DSC registru</span><span class="sxs-lookup"><span data-stu-id="2b055-103">DSC Registry Resource</span></span>

> <span data-ttu-id="2b055-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="2b055-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="2b055-105">**Registru** prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro správu klíčů registru a hodnoty na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="2b055-105">The **Registry** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage registry keys and values on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="2b055-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2b055-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="2b055-107">Properties</span><span class="sxs-lookup"><span data-stu-id="2b055-107">Properties</span></span>
|  <span data-ttu-id="2b055-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="2b055-108">Property</span></span>  |  <span data-ttu-id="2b055-109">Popis</span><span class="sxs-lookup"><span data-stu-id="2b055-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="2b055-110">Klávesa</span><span class="sxs-lookup"><span data-stu-id="2b055-110">Key</span></span>| <span data-ttu-id="2b055-111">Určuje cestu klíč registru, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="2b055-111">Indicates the path of the registry key for which you want to ensure a specific state.</span></span> <span data-ttu-id="2b055-112">Tato cesta musí obsahovat podregistr.</span><span class="sxs-lookup"><span data-stu-id="2b055-112">This path must include the hive.</span></span>| 
| <span data-ttu-id="2b055-113">ValueName</span><span class="sxs-lookup"><span data-stu-id="2b055-113">ValueName</span></span>| <span data-ttu-id="2b055-114">Určuje název hodnoty registru.</span><span class="sxs-lookup"><span data-stu-id="2b055-114">Indicates the name of the registry value.</span></span> <span data-ttu-id="2b055-115">Chcete-li přidat nebo odebrat klíč registru, zadejte tuto vlastnost jako prázdný řetězec bez zadání ValueType nebo data.</span><span class="sxs-lookup"><span data-stu-id="2b055-115">To add or remove a registry key, specify this property as an empty string without specifying ValueType or ValueData.</span></span> <span data-ttu-id="2b055-116">Změnit nebo odebrat výchozí hodnota klíče registru, zadejte tuto vlastnost při zadávání také ValueType nebo data jako prázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="2b055-116">To modify or remove the default value of a registry key, specify this property as an empty string while also specifying ValueType or ValueData.</span></span>| 
| <span data-ttu-id="2b055-117">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="2b055-117">Ensure</span></span>| <span data-ttu-id="2b055-118">Určuje, zda existují klíč a hodnotu.</span><span class="sxs-lookup"><span data-stu-id="2b055-118">Indicates if the key and value exist.</span></span> <span data-ttu-id="2b055-119">Aby se zajistilo, že udělají, nastavte tuto vlastnost na "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="2b055-119">To ensure that they do, set this property to "Present".</span></span> <span data-ttu-id="2b055-120">Aby se zajistilo, že neexistují, nastavte vlastnost na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="2b055-120">To ensure that they do not exist, set the property to "Absent".</span></span> <span data-ttu-id="2b055-121">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="2b055-121">The default value is "Present".</span></span>| 
| <span data-ttu-id="2b055-122">Force</span><span class="sxs-lookup"><span data-stu-id="2b055-122">Force</span></span>| <span data-ttu-id="2b055-123">Pokud zadaný klíč registru existuje, __Force__ přepíše s novou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="2b055-123">If the specified registry key is present, __Force__ overwrites it with the new value.</span></span> <span data-ttu-id="2b055-124">Pokud odstraníte klíč registru s podklíče, musí se jednat __$true__</span><span class="sxs-lookup"><span data-stu-id="2b055-124">If deleting a registry key with subkeys, this needs to be __$true__</span></span>| 
| <span data-ttu-id="2b055-125">Hex</span><span class="sxs-lookup"><span data-stu-id="2b055-125">Hex</span></span>| <span data-ttu-id="2b055-126">Označuje, pokud budou data vyjádřeny v šestnáctkovém formátu.</span><span class="sxs-lookup"><span data-stu-id="2b055-126">Indicates if data will be expressed in hexadecimal format.</span></span> <span data-ttu-id="2b055-127">-Li zadána, data hodnotu DWORD nebo QWORD jsou zobrazena v šestnáctkovém formátu.</span><span class="sxs-lookup"><span data-stu-id="2b055-127">If specified, the DWORD/QWORD value data is presented in hexadecimal format.</span></span> <span data-ttu-id="2b055-128">Pro jiné typy není platná.</span><span class="sxs-lookup"><span data-stu-id="2b055-128">Not valid for other types.</span></span> <span data-ttu-id="2b055-129">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="2b055-129">The default value is __$false__.</span></span>| 
| <span data-ttu-id="2b055-130">dependsOn</span><span class="sxs-lookup"><span data-stu-id="2b055-130">DependsOn</span></span>| <span data-ttu-id="2b055-131">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="2b055-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="2b055-132">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="2b055-132">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="2b055-133">ValueData</span><span class="sxs-lookup"><span data-stu-id="2b055-133">ValueData</span></span>| <span data-ttu-id="2b055-134">Data pro hodnotu registru.</span><span class="sxs-lookup"><span data-stu-id="2b055-134">The data for the registry value.</span></span>| 
| <span data-ttu-id="2b055-135">ValueType</span><span class="sxs-lookup"><span data-stu-id="2b055-135">ValueType</span></span>| <span data-ttu-id="2b055-136">Označuje typ hodnoty.</span><span class="sxs-lookup"><span data-stu-id="2b055-136">Indicates the type of the value.</span></span> <span data-ttu-id="2b055-137">Podporované typy jsou:</span><span class="sxs-lookup"><span data-stu-id="2b055-137">The supported types are:</span></span> 
<ul><li><span data-ttu-id="2b055-138">Řetězec (REG_SZ)</span><span class="sxs-lookup"><span data-stu-id="2b055-138">String (REG_SZ)</span></span></li>


<li><span data-ttu-id="2b055-139">Binární (REG binární)</span><span class="sxs-lookup"><span data-stu-id="2b055-139">Binary (REG-BINARY)</span></span></li>


<li><span data-ttu-id="2b055-140">DWORD 32-bit (REG_DWORD)</span><span class="sxs-lookup"><span data-stu-id="2b055-140">Dword 32-bit (REG_DWORD)</span></span></li>


<li><span data-ttu-id="2b055-141">Qword 64-bit (REG_QWORD)</span><span class="sxs-lookup"><span data-stu-id="2b055-141">Qword 64-bit (REG_QWORD)</span></span></li>


<li><span data-ttu-id="2b055-142">Víceřetězcovou (REG_MULTI_SZ)</span><span class="sxs-lookup"><span data-stu-id="2b055-142">Multi-string (REG_MULTI_SZ)</span></span></li>


<li><span data-ttu-id="2b055-143">Rozšíření řetězce (REG_EXPAND_SZ)</span><span class="sxs-lookup"><span data-stu-id="2b055-143">Expandable string (REG_EXPAND_SZ)</span></span></li></ul>

## <a name="example"></a><span data-ttu-id="2b055-144">Příklad</span><span class="sxs-lookup"><span data-stu-id="2b055-144">Example</span></span>
<span data-ttu-id="2b055-145">Tento příklad zajišťuje, že klíč s názvem "ExampleKey" součástí **HKEY\_místní\_počítač** hive.</span><span class="sxs-lookup"><span data-stu-id="2b055-145">This example ensures that a key named "ExampleKey" is present in the **HKEY\_LOCAL\_MACHINE** hive.</span></span>
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

><span data-ttu-id="2b055-146">**Poznámka:** Změna nastavení registru **HKEY\_aktuální\_uživatele** hive vyžaduje, že konfigurace bude spuštěna s pověřeními uživatele, nikoli jako systém.</span><span class="sxs-lookup"><span data-stu-id="2b055-146">**Note:** Changing a registry setting in the **HKEY\_CURRENT\_USER** hive requires that the configuration runs with user credentials, rather than as the system.</span></span>
><span data-ttu-id="2b055-147">Můžete použít **PsDscRunAsCredential** vlastnosti a určit přihlašovací údaje uživatele pro danou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="2b055-147">You can use the **PsDscRunAsCredential** property to specify user credentials for the configuration.</span></span> <span data-ttu-id="2b055-148">Příklad, naleznete v části [DSC spuštěná s pověřeními uživatele](runAsUser.md)</span><span class="sxs-lookup"><span data-stu-id="2b055-148">For an example, see [Running DSC with user credentials](runAsUser.md)</span></span>




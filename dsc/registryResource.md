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
# <a name="dsc-registry-resource"></a><span data-ttu-id="b6b38-103">Prostředek Registry DSC</span><span class="sxs-lookup"><span data-stu-id="b6b38-103">DSC Registry Resource</span></span>

> <span data-ttu-id="b6b38-104">Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b6b38-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b6b38-105">**Registru** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě klíčů registru a hodnoty na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="b6b38-105">The **Registry** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage registry keys and values on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="b6b38-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b6b38-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="b6b38-107">Properties</span><span class="sxs-lookup"><span data-stu-id="b6b38-107">Properties</span></span>

|  <span data-ttu-id="b6b38-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="b6b38-108">Property</span></span>  |  <span data-ttu-id="b6b38-109">Popis</span><span class="sxs-lookup"><span data-stu-id="b6b38-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="b6b38-110">Klávesa</span><span class="sxs-lookup"><span data-stu-id="b6b38-110">Key</span></span>| <span data-ttu-id="b6b38-111">Označuje cestu klíče registru, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="b6b38-111">Indicates the path of the registry key for which you want to ensure a specific state.</span></span> <span data-ttu-id="b6b38-112">Tato cesta musí obsahovat hive.</span><span class="sxs-lookup"><span data-stu-id="b6b38-112">This path must include the hive.</span></span>|
| <span data-ttu-id="b6b38-113">Název hodnoty</span><span class="sxs-lookup"><span data-stu-id="b6b38-113">ValueName</span></span>| <span data-ttu-id="b6b38-114">Určuje název hodnoty registru.</span><span class="sxs-lookup"><span data-stu-id="b6b38-114">Indicates the name of the registry value.</span></span> <span data-ttu-id="b6b38-115">Přidání nebo odebrání určitého klíče registru, zadejte tuto vlastnost jako prázdný řetězec bez předchozího určení ValueType nebo data.</span><span class="sxs-lookup"><span data-stu-id="b6b38-115">To add or remove a registry key, specify this property as an empty string without specifying ValueType or ValueData.</span></span> <span data-ttu-id="b6b38-116">Chcete-li upravit nebo odebrat výchozí hodnota klíče registru, tuto vlastnost zadávejte jako prázdný řetězec při zadávání také ValueType nebo data.</span><span class="sxs-lookup"><span data-stu-id="b6b38-116">To modify or remove the default value of a registry key, specify this property as an empty string while also specifying ValueType or ValueData.</span></span>|
| <span data-ttu-id="b6b38-117">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="b6b38-117">Ensure</span></span>| <span data-ttu-id="b6b38-118">Označuje, zda existují klíče a hodnoty.</span><span class="sxs-lookup"><span data-stu-id="b6b38-118">Indicates if the key and value exist.</span></span> <span data-ttu-id="b6b38-119">Aby bylo zajištěno, že dělají, nastavte tuto vlastnost na "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="b6b38-119">To ensure that they do, set this property to "Present".</span></span> <span data-ttu-id="b6b38-120">Aby bylo zajištěno, že neexistují, nastavte vlastnost na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="b6b38-120">To ensure that they do not exist, set the property to "Absent".</span></span> <span data-ttu-id="b6b38-121">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="b6b38-121">The default value is "Present".</span></span>|
| <span data-ttu-id="b6b38-122">Force</span><span class="sxs-lookup"><span data-stu-id="b6b38-122">Force</span></span>| <span data-ttu-id="b6b38-123">Pokud zadaný klíč registru je k dispozici, **platnost** přepíšete novou hodnotou.</span><span class="sxs-lookup"><span data-stu-id="b6b38-123">If the specified registry key is present, **Force** overwrites it with the new value.</span></span> <span data-ttu-id="b6b38-124">Pokud se odstranění klíče registru s podklíčích, musí se jednat **$true**</span><span class="sxs-lookup"><span data-stu-id="b6b38-124">If deleting a registry key with subkeys, this needs to be **$true**</span></span> |
| <span data-ttu-id="b6b38-125">Hex</span><span class="sxs-lookup"><span data-stu-id="b6b38-125">Hex</span></span>| <span data-ttu-id="b6b38-126">Označuje, pokud se data vyjadřují v šestnáctkovém formátu.</span><span class="sxs-lookup"><span data-stu-id="b6b38-126">Indicates if data will be expressed in hexadecimal format.</span></span> <span data-ttu-id="b6b38-127">Je-li zadána, data hodnotu DWORD/QWORD se zobrazují v šestnáctkovém formátu.</span><span class="sxs-lookup"><span data-stu-id="b6b38-127">If specified, the DWORD/QWORD value data is presented in hexadecimal format.</span></span> <span data-ttu-id="b6b38-128">Není platný pro jiné typy.</span><span class="sxs-lookup"><span data-stu-id="b6b38-128">Not valid for other types.</span></span> <span data-ttu-id="b6b38-129">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="b6b38-129">The default value is **$false**.</span></span>|
| <span data-ttu-id="b6b38-130">DependsOn</span><span class="sxs-lookup"><span data-stu-id="b6b38-130">DependsOn</span></span>| <span data-ttu-id="b6b38-131">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="b6b38-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="b6b38-132">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="b6b38-132">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="b6b38-133">Data</span><span class="sxs-lookup"><span data-stu-id="b6b38-133">ValueData</span></span>| <span data-ttu-id="b6b38-134">Data pro hodnotu registru.</span><span class="sxs-lookup"><span data-stu-id="b6b38-134">The data for the registry value.</span></span>|
| <span data-ttu-id="b6b38-135">ValueType</span><span class="sxs-lookup"><span data-stu-id="b6b38-135">ValueType</span></span>| <span data-ttu-id="b6b38-136">Určuje typ hodnoty.</span><span class="sxs-lookup"><span data-stu-id="b6b38-136">Indicates the type of the value.</span></span> <span data-ttu-id="b6b38-137">Podporované typy jsou: řetězce (REG_SZ), binární soubor (REG binární soubor), Dword 32 bitů (REG_DWORD), Qword 64-bit (REG_QWORD), víceřetězcovou (REG_MULTI_SZ), Rozšiřitelná řetězcová (REG_EXPAND_SZ)</span><span class="sxs-lookup"><span data-stu-id="b6b38-137">The supported types are: String (REG_SZ), Binary (REG-BINARY), Dword 32-bit (REG_DWORD), Qword 64-bit (REG_QWORD), Multi-string (REG_MULTI_SZ), Expandable string (REG_EXPAND_SZ)</span></span> |

## <a name="example"></a><span data-ttu-id="b6b38-138">Příklad</span><span class="sxs-lookup"><span data-stu-id="b6b38-138">Example</span></span>

<span data-ttu-id="b6b38-139">Tento příklad zajistí, že klíč s názvem "ExampleKey" je k dispozici v **HKEY\_místní\_počítač** hive.</span><span class="sxs-lookup"><span data-stu-id="b6b38-139">This example ensures that a key named "ExampleKey" is present in the **HKEY\_LOCAL\_MACHINE** hive.</span></span>

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
> <span data-ttu-id="b6b38-140">Změna nastavení v registru **HKEY\_aktuální\_uživatele** hive vyžaduje, že konfigurace spouští pomocí přihlašovacích údajů uživatele, nikoli jako systém.</span><span class="sxs-lookup"><span data-stu-id="b6b38-140">Changing a registry setting in the **HKEY\_CURRENT\_USER** hive requires that the configuration runs with user credentials, rather than as the system.</span></span> <span data-ttu-id="b6b38-141">Můžete použít **PsDscRunAsCredential** vlastnosti a určit přihlašovací údaje uživatele pro danou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="b6b38-141">You can use the **PsDscRunAsCredential** property to specify user credentials for the configuration.</span></span> <span data-ttu-id="b6b38-142">Příklad najdete v tématu [DSC spuštěná s pověřeními uživatele](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="b6b38-142">For an example, see [Running DSC with user credentials](runAsUser.md).</span></span>
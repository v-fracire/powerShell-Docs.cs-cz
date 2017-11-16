---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC prostředí"
ms.openlocfilehash: 7c98798fa0e8fc865798ea30530e41ac87b2dadc
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-environment-resource"></a><span data-ttu-id="240e7-103">Prostředek DSC prostředí</span><span class="sxs-lookup"><span data-stu-id="240e7-103">DSC Environment Resource</span></span>

> <span data-ttu-id="240e7-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="240e7-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="240e7-105">__Prostředí__ prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě systémových proměnných prostředí.</span><span class="sxs-lookup"><span data-stu-id="240e7-105">The __Environment__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage system environment variables.</span></span>

## <a name="syntax"></a><span data-ttu-id="240e7-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="240e7-106">Syntax</span></span>
``` mof
Environment [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Path = [bool] ]
    [ DependsOn = [string[]] ]
    [ Value = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="240e7-107">Properties</span><span class="sxs-lookup"><span data-stu-id="240e7-107">Properties</span></span>

|  <span data-ttu-id="240e7-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="240e7-108">Property</span></span>  |  <span data-ttu-id="240e7-109">Popis</span><span class="sxs-lookup"><span data-stu-id="240e7-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="240e7-110">Název</span><span class="sxs-lookup"><span data-stu-id="240e7-110">Name</span></span>| <span data-ttu-id="240e7-111">Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="240e7-111">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="240e7-112">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="240e7-112">Ensure</span></span>| <span data-ttu-id="240e7-113">Určuje, jestli existuje proměnné.</span><span class="sxs-lookup"><span data-stu-id="240e7-113">Indicates if a variable exists.</span></span> <span data-ttu-id="240e7-114">Tuto vlastnost nastavit na __přítomen__ vytvoření proměnné prostředí, pokud neexistuje nebo k zajištění, že jeho hodnota odpovídá, co je zajišťováno prostřednictvím __hodnotu__ vlastnost Pokud proměnnou již existuje.</span><span class="sxs-lookup"><span data-stu-id="240e7-114">Set this property to __Present__ to create the environment variable if it does not exist or to ensure that its value matches what is provided through the __Value__ property if the variable already exists.</span></span> <span data-ttu-id="240e7-115">Nastavte ji na __chybí__ odstranit proměnnou, pokud existuje.</span><span class="sxs-lookup"><span data-stu-id="240e7-115">Set it to __Absent__ to delete the variable if it exists.</span></span>| 
| <span data-ttu-id="240e7-116">Cesta</span><span class="sxs-lookup"><span data-stu-id="240e7-116">Path</span></span>| <span data-ttu-id="240e7-117">Definuje proměnnou prostředí, který je konfigurován.</span><span class="sxs-lookup"><span data-stu-id="240e7-117">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="240e7-118">Tuto vlastnost nastavit na __$true__ -li proměnná __cesta__ proměnné; v opačném nastavte ji na __$false__.</span><span class="sxs-lookup"><span data-stu-id="240e7-118">Set this property to __$true__ if the variable is the __Path__ variable; otherwise, set it to __$false__.</span></span> <span data-ttu-id="240e7-119">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="240e7-119">The default is __$false__.</span></span> <span data-ttu-id="240e7-120">Pokud je proměnná konfigurován __cesta__ proměnné, hodnota poskytnutá prostřednictvím __hodnotu__ vlastnost bude připojeno k stávající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="240e7-120">If the variable being configured is the __Path__ variable, the value provided through the __Value__ property will be appended to the existing value.</span></span>| 
| <span data-ttu-id="240e7-121">dependsOn</span><span class="sxs-lookup"><span data-stu-id="240e7-121">DependsOn</span></span> | <span data-ttu-id="240e7-122">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="240e7-122">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="240e7-123">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="240e7-123">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="240e7-124">Hodnota</span><span class="sxs-lookup"><span data-stu-id="240e7-124">Value</span></span>| <span data-ttu-id="240e7-125">Hodnota pro přiřazení k proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="240e7-125">The value to assign to the environment variable.</span></span>| 

## <a name="example"></a><span data-ttu-id="240e7-126">Příklad</span><span class="sxs-lookup"><span data-stu-id="240e7-126">Example</span></span>

<span data-ttu-id="240e7-127">Následující příklad zajišťuje, že __TestEnvironmentVariable__ existuje a má hodnotu __Testovací_hodnota__.</span><span class="sxs-lookup"><span data-stu-id="240e7-127">The following example ensures that __TestEnvironmentVariable__ is present and it has the value __TestValue__.</span></span> <span data-ttu-id="240e7-128">Pokud není přítomen, vytvoří se.</span><span class="sxs-lookup"><span data-stu-id="240e7-128">If it is not present, it creates it.</span></span>

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```


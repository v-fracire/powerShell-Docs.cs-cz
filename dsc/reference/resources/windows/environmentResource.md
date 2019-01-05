---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC prostředí
ms.openlocfilehash: 2bc1600a9df32538d59efa712569b12fa9e3beee
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048131"
---
# <a name="dsc-environment-resource"></a><span data-ttu-id="3079a-103">Prostředek DSC prostředí</span><span class="sxs-lookup"><span data-stu-id="3079a-103">DSC Environment Resource</span></span>

> <span data-ttu-id="3079a-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3079a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="3079a-105">__Prostředí__ prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě seznamu proměnných prostředí systému.</span><span class="sxs-lookup"><span data-stu-id="3079a-105">The __Environment__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage system environment variables.</span></span>

## <a name="syntax"></a><span data-ttu-id="3079a-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="3079a-106">Syntax</span></span>
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

## <a name="properties"></a><span data-ttu-id="3079a-107">Properties</span><span class="sxs-lookup"><span data-stu-id="3079a-107">Properties</span></span>

|  <span data-ttu-id="3079a-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="3079a-108">Property</span></span>  |  <span data-ttu-id="3079a-109">Popis</span><span class="sxs-lookup"><span data-stu-id="3079a-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="3079a-110">Name</span><span class="sxs-lookup"><span data-stu-id="3079a-110">Name</span></span>| <span data-ttu-id="3079a-111">Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="3079a-111">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="3079a-112">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="3079a-112">Ensure</span></span>| <span data-ttu-id="3079a-113">Určuje, jestli existuje proměnná.</span><span class="sxs-lookup"><span data-stu-id="3079a-113">Indicates if a variable exists.</span></span> <span data-ttu-id="3079a-114">Tuto vlastnost nastavte na __k dispozici__ vytvořit proměnnou prostředí, pokud neexistuje nebo k zajištění, že její hodnota odpovídá, co je poskytována prostřednictvím __hodnotu__ vlastnost, pokud je proměnná už existuje.</span><span class="sxs-lookup"><span data-stu-id="3079a-114">Set this property to __Present__ to create the environment variable if it does not exist or to ensure that its value matches what is provided through the __Value__ property if the variable already exists.</span></span> <span data-ttu-id="3079a-115">Nastavte ho na __chybí__ odstranit proměnnou, pokud existuje.</span><span class="sxs-lookup"><span data-stu-id="3079a-115">Set it to __Absent__ to delete the variable if it exists.</span></span>|
| <span data-ttu-id="3079a-116">Cesta</span><span class="sxs-lookup"><span data-stu-id="3079a-116">Path</span></span>| <span data-ttu-id="3079a-117">Definuje proměnnou prostředí, který je konfigurován.</span><span class="sxs-lookup"><span data-stu-id="3079a-117">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="3079a-118">Tuto vlastnost nastavte na __$true__ Pokud je proměnná __cesta__ proměnné; v opačném případě nastavte ho na __$false__.</span><span class="sxs-lookup"><span data-stu-id="3079a-118">Set this property to __$true__ if the variable is the __Path__ variable; otherwise, set it to __$false__.</span></span> <span data-ttu-id="3079a-119">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="3079a-119">The default is __$false__.</span></span> <span data-ttu-id="3079a-120">Pokud je proměnná, která se právě nastavuje __cesta__ proměnné, hodnota poskytnutá prostřednictvím __hodnotu__ vlastnost se připojí k existující hodnotu.</span><span class="sxs-lookup"><span data-stu-id="3079a-120">If the variable being configured is the __Path__ variable, the value provided through the __Value__ property will be appended to the existing value.</span></span>|
| <span data-ttu-id="3079a-121">DependsOn</span><span class="sxs-lookup"><span data-stu-id="3079a-121">DependsOn</span></span> | <span data-ttu-id="3079a-122">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="3079a-122">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="3079a-123">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="3079a-123">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="3079a-124">Hodnota</span><span class="sxs-lookup"><span data-stu-id="3079a-124">Value</span></span>| <span data-ttu-id="3079a-125">Hodnota, kterou chcete přiřadit k proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="3079a-125">The value to assign to the environment variable.</span></span>|

## <a name="example"></a><span data-ttu-id="3079a-126">Příklad</span><span class="sxs-lookup"><span data-stu-id="3079a-126">Example</span></span>

<span data-ttu-id="3079a-127">Následující příklad zajistí, že __TestEnvironmentVariable__ existuje a má hodnotu __Testovaci_Hodnota__.</span><span class="sxs-lookup"><span data-stu-id="3079a-127">The following example ensures that __TestEnvironmentVariable__ is present and it has the value __TestValue__.</span></span> <span data-ttu-id="3079a-128">Pokud tam není, vytvoří se.</span><span class="sxs-lookup"><span data-stu-id="3079a-128">If it is not present, it creates it.</span></span>

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```
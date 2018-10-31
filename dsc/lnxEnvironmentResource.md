---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxEnvironment
ms.openlocfilehash: 763ec560faa6adaf42aef3c21c9045be95f780bc
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225977"
---
# <a name="dsc-for-linux-nxenvironment-resource"></a><span data-ttu-id="891e0-103">DSC pro Linux prostředek nxEnvironment</span><span class="sxs-lookup"><span data-stu-id="891e0-103">DSC for Linux nxEnvironment Resource</span></span>

<span data-ttu-id="891e0-104">**NxEnvironment** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě seznamu proměnných prostředí systému v systému Linux uzlu.</span><span class="sxs-lookup"><span data-stu-id="891e0-104">The **nxEnvironment** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage system environment variables on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="891e0-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="891e0-105">Syntax</span></span>

```
nxEnvironment <string> #ResourceName
{
    Name = <string>
    [ Value = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Path = <bool> }
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="891e0-106">Properties</span><span class="sxs-lookup"><span data-stu-id="891e0-106">Properties</span></span>

|  <span data-ttu-id="891e0-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="891e0-107">Property</span></span> |  <span data-ttu-id="891e0-108">Popis</span><span class="sxs-lookup"><span data-stu-id="891e0-108">Description</span></span> |
|---|---|
| <span data-ttu-id="891e0-109">Název</span><span class="sxs-lookup"><span data-stu-id="891e0-109">Name</span></span>| <span data-ttu-id="891e0-110">Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="891e0-110">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="891e0-111">Hodnota</span><span class="sxs-lookup"><span data-stu-id="891e0-111">Value</span></span>| <span data-ttu-id="891e0-112">Hodnota, kterou chcete přiřadit k proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="891e0-112">The value to assign to the environment variable.</span></span>|
| <span data-ttu-id="891e0-113">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="891e0-113">Ensure</span></span>| <span data-ttu-id="891e0-114">Určuje, jestli se má zkontrolovat, zda existuje proměnná.</span><span class="sxs-lookup"><span data-stu-id="891e0-114">Determines whether to check if the variable exists.</span></span> <span data-ttu-id="891e0-115">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že existuje proměnná.</span><span class="sxs-lookup"><span data-stu-id="891e0-115">Set this property to "Present" to ensure the variable exists.</span></span> <span data-ttu-id="891e0-116">Nastavte ho na "Chybí" Ujistěte se, že proměnná neexistuje.</span><span class="sxs-lookup"><span data-stu-id="891e0-116">Set it to "Absent" to ensure the variable does not exist.</span></span> <span data-ttu-id="891e0-117">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="891e0-117">The default value is "Present".</span></span>|
| <span data-ttu-id="891e0-118">Cesta</span><span class="sxs-lookup"><span data-stu-id="891e0-118">Path</span></span>| <span data-ttu-id="891e0-119">Definuje proměnnou prostředí, který je konfigurován.</span><span class="sxs-lookup"><span data-stu-id="891e0-119">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="891e0-120">Tuto vlastnost nastavte na **$true** Pokud je proměnná **cesta** proměnné; v opačném případě nastavte ho na **$false**.</span><span class="sxs-lookup"><span data-stu-id="891e0-120">Set this property to **$true** if the variable is the **Path** variable; otherwise, set it to **$false**.</span></span> <span data-ttu-id="891e0-121">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="891e0-121">The default is **$false**.</span></span> <span data-ttu-id="891e0-122">Pokud je proměnná, která se právě nastavuje **cesta** proměnné, hodnota poskytnutá prostřednictvím **hodnotu** vlastnost se připojí k existující hodnotu.</span><span class="sxs-lookup"><span data-stu-id="891e0-122">If the variable being configured is the **Path** variable, the value provided through the **Value** property will be appended to the existing value.</span></span>|
| <span data-ttu-id="891e0-123">DependsOn</span><span class="sxs-lookup"><span data-stu-id="891e0-123">DependsOn</span></span> | <span data-ttu-id="891e0-124">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="891e0-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="891e0-125">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="891e0-125">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="891e0-126">Další informace</span><span class="sxs-lookup"><span data-stu-id="891e0-126">Additional Information</span></span>

* <span data-ttu-id="891e0-127">Pokud **cesta** chybí nebo je nastavena na **$false**, proměnné prostředí jsou spravovány v `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="891e0-127">If **Path** is absent or set to **$false**, environment variables are managed in `/etc/environment`.</span></span> <span data-ttu-id="891e0-128">Programů nebo skriptů můžou vyžadovat konfiguraci ke zdroji `/etc/environment` souboru pro přístup k proměnným spravovaném prostředí.</span><span class="sxs-lookup"><span data-stu-id="891e0-128">Your programs or scripts may require configuration to source the `/etc/environment` file to access the managed environment variables.</span></span>
* <span data-ttu-id="891e0-129">Pokud **cesta** je nastavena na **$true**, proměnné prostředí se spravuje v souboru `/etc/profile.d/DSCenvironment.sh`.</span><span class="sxs-lookup"><span data-stu-id="891e0-129">If **Path** is set to **$true**, the environment variable is managed in the file `/etc/profile.d/DSCenvironment.sh`.</span></span> <span data-ttu-id="891e0-130">Tento soubor bude vytvořen, pokud neexistuje.</span><span class="sxs-lookup"><span data-stu-id="891e0-130">This file will be created if it does not exist.</span></span> <span data-ttu-id="891e0-131">Pokud **Ujistěte se, že** je nastavena na "Chybí" a **cesta** je nastavena na **$true**, existující proměnné prostředí pouze se odebere z `/etc/profile.d/DSCenvironment.sh` a ne z jiných souborů.</span><span class="sxs-lookup"><span data-stu-id="891e0-131">If **Ensure** is set to "Absent" and **Path** is set to **$true**, an existing environment variable will only be removed from `/etc/profile.d/DSCenvironment.sh` and not from other files.</span></span>

## <a name="example"></a><span data-ttu-id="891e0-132">Příklad</span><span class="sxs-lookup"><span data-stu-id="891e0-132">Example</span></span>

<span data-ttu-id="891e0-133">Následující příklad ukazuje způsob použití **nxEnvironment** prostředků zajistit, aby **TestEnvironmentVariable** je k dispozici a má hodnotu "Test-Value".</span><span class="sxs-lookup"><span data-stu-id="891e0-133">The following example shows how to use the **nxEnvironment** resource to ensure that **TestEnvironmentVariable** is present and has the value "Test-Value".</span></span> <span data-ttu-id="891e0-134">Pokud **TestEnvironmentVariable** není k dispozici, bude vytvořen.</span><span class="sxs-lookup"><span data-stu-id="891e0-134">If **TestEnvironmentVariable** is not present, it will be created.</span></span>

```
Import-DSCResource -Module nx


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```
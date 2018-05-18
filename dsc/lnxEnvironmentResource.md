---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: DSC pro Linux nxEnvironment prostředků
ms.openlocfilehash: 3c9f39760e0fba7fac060f29f9e808a3a434401f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-for-linux-nxenvironment-resource"></a><span data-ttu-id="e6c4f-103">DSC pro Linux nxEnvironment prostředků</span><span class="sxs-lookup"><span data-stu-id="e6c4f-103">DSC for Linux nxEnvironment Resource</span></span>

<span data-ttu-id="e6c4f-104">**NxEnvironment** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro ke správě seznamu proměnných prostředí systému Linux uzlu.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-104">The **nxEnvironment** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage system environment variables on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="e6c4f-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e6c4f-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="e6c4f-106">Properties</span><span class="sxs-lookup"><span data-stu-id="e6c4f-106">Properties</span></span>

|  <span data-ttu-id="e6c4f-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e6c4f-107">Property</span></span> |  <span data-ttu-id="e6c4f-108">Popis</span><span class="sxs-lookup"><span data-stu-id="e6c4f-108">Description</span></span> |
|---|---|
| <span data-ttu-id="e6c4f-109">Název</span><span class="sxs-lookup"><span data-stu-id="e6c4f-109">Name</span></span>| <span data-ttu-id="e6c4f-110">Určuje název proměnné prostředí, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-110">Indicates the name of the environment variable for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="e6c4f-111">Hodnota</span><span class="sxs-lookup"><span data-stu-id="e6c4f-111">Value</span></span>| <span data-ttu-id="e6c4f-112">Hodnota pro přiřazení k proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-112">The value to assign to the environment variable.</span></span>|
| <span data-ttu-id="e6c4f-113">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="e6c4f-113">Ensure</span></span>| <span data-ttu-id="e6c4f-114">Určuje, jestli se má zkontrolovat, zda existuje proměnnou.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-114">Determines whether to check if the variable exists.</span></span> <span data-ttu-id="e6c4f-115">Nastavením této vlastnosti "Přítomen" Ujistěte se, že existuje proměnnou.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-115">Set this property to "Present" to ensure the variable exists.</span></span> <span data-ttu-id="e6c4f-116">Nastavte ji na "Chybí" Ujistěte se, že proměnná neexistuje.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-116">Set it to "Absent" to ensure the variable does not exist.</span></span> <span data-ttu-id="e6c4f-117">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="e6c4f-117">The default value is "Present".</span></span>|
| <span data-ttu-id="e6c4f-118">Cesta</span><span class="sxs-lookup"><span data-stu-id="e6c4f-118">Path</span></span>| <span data-ttu-id="e6c4f-119">Definuje proměnnou prostředí, který je konfigurován.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-119">Defines the environment variable that is being configured.</span></span> <span data-ttu-id="e6c4f-120">Tuto vlastnost nastavit na **$true** -li proměnná **cesta** proměnné; v opačném nastavte ji na **$false**.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-120">Set this property to **$true** if the variable is the **Path** variable; otherwise, set it to **$false**.</span></span> <span data-ttu-id="e6c4f-121">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-121">The default is **$false**.</span></span> <span data-ttu-id="e6c4f-122">Pokud je proměnná konfigurován **cesta** proměnné, hodnota poskytnutá prostřednictvím **hodnotu** vlastnost bude připojeno k stávající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-122">If the variable being configured is the **Path** variable, the value provided through the **Value** property will be appended to the existing value.</span></span>|
| <span data-ttu-id="e6c4f-123">dependsOn</span><span class="sxs-lookup"><span data-stu-id="e6c4f-123">DependsOn</span></span> | <span data-ttu-id="e6c4f-124">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="e6c4f-125">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-125">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="e6c4f-126">Další informace</span><span class="sxs-lookup"><span data-stu-id="e6c4f-126">Additional Information</span></span>

* <span data-ttu-id="e6c4f-127">Pokud **cesta** chybí nebo je nastavena na **$false**, proměnné prostředí se spravují v `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-127">If **Path** is absent or set to **$false**, environment variables are managed in `/etc/environment`.</span></span> <span data-ttu-id="e6c4f-128">Programy nebo skripty může vyžadovat konfiguraci ke zdroji `/etc/environment` souboru pro přístup k proměnným spravovaném prostředí.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-128">Your programs or scripts may require configuration to source the `/etc/environment` file to access the managed environment variables.</span></span>
* <span data-ttu-id="e6c4f-129">Pokud **cesta** je nastaven na **$true**, proměnná prostředí je spravován v souboru `/etc/profile.d/DSCenvironment.sh`.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-129">If **Path** is set to **$true**, the environment variable is managed in the file `/etc/profile.d/DSCenvironment.sh`.</span></span> <span data-ttu-id="e6c4f-130">Tento soubor bude vytvořen, pokud neexistuje.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-130">This file will be created if it does not exist.</span></span> <span data-ttu-id="e6c4f-131">Pokud **zajistěte, aby** je nastaven na "Chybí" a **cesta** je nastaven na **$true**, existující proměnné prostředí se jenom odeberou z `/etc/profile.d/DSCenvironment.sh` a nikoli z jiné soubory.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-131">If **Ensure** is set to "Absent" and **Path** is set to **$true**, an existing environment variable will only be removed from `/etc/profile.d/DSCenvironment.sh` and not from other files.</span></span>

## <a name="example"></a><span data-ttu-id="e6c4f-132">Příklad</span><span class="sxs-lookup"><span data-stu-id="e6c4f-132">Example</span></span>

<span data-ttu-id="e6c4f-133">Následující příklad ukazuje, jak používat **nxEnvironment** prostředků zajistit, aby **TestEnvironmentVariable** je k dispozici a má hodnotu "Test-hodnota".</span><span class="sxs-lookup"><span data-stu-id="e6c4f-133">The following example shows how to use the **nxEnvironment** resource to ensure that **TestEnvironmentVariable** is present and has the value "Test-Value".</span></span> <span data-ttu-id="e6c4f-134">Pokud **TestEnvironmentVariable** nejsou k dispozici, bude vytvořen.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-134">If **TestEnvironmentVariable** is not present, it will be created.</span></span>

```
Import-DSCResource -Module nx


nxEnvironment EnvironmentExample
{
    Ensure = “Present”
    Name = “TestEnvironmentVariable”
    Value = “TestValue”
}
```
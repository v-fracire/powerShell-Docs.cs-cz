---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxPackage prostředků"
ms.openlocfilehash: 11019b1cd12f23b0b498b7cb9a06e02c46c3c279
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxpackage-resource"></a><span data-ttu-id="60a58-103">DSC pro Linux nxPackage prostředků</span><span class="sxs-lookup"><span data-stu-id="60a58-103">DSC for Linux nxPackage Resource</span></span>

<span data-ttu-id="60a58-104">**NxPackage** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě balíčků na uzlu Linux.</span><span class="sxs-lookup"><span data-stu-id="60a58-104">The **nxPackage** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage packages on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="60a58-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="60a58-105">Syntax</span></span>

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]
    
}
```

## <a name="properties"></a><span data-ttu-id="60a58-106">Properties</span><span class="sxs-lookup"><span data-stu-id="60a58-106">Properties</span></span>

|  <span data-ttu-id="60a58-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="60a58-107">Property</span></span> |  <span data-ttu-id="60a58-108">Popis</span><span class="sxs-lookup"><span data-stu-id="60a58-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="60a58-109">Název</span><span class="sxs-lookup"><span data-stu-id="60a58-109">Name</span></span>| <span data-ttu-id="60a58-110">Název balíčku, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="60a58-110">The name of the package for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="60a58-111">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="60a58-111">Ensure</span></span>| <span data-ttu-id="60a58-112">Určuje, jestli se má zkontrolovat, zda balíček existuje.</span><span class="sxs-lookup"><span data-stu-id="60a58-112">Determines whether to check if the package exists.</span></span> <span data-ttu-id="60a58-113">Nastavením této vlastnosti "Přítomen" zajistěte, aby byl že balíček existuje.</span><span class="sxs-lookup"><span data-stu-id="60a58-113">Set this property to "Present" to ensure the package exists.</span></span> <span data-ttu-id="60a58-114">Nastavte ji na "Chybí" zajistěte, aby byl že balíček neexistuje.</span><span class="sxs-lookup"><span data-stu-id="60a58-114">Set it to "Absent" to ensure the package does not exist.</span></span> <span data-ttu-id="60a58-115">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="60a58-115">The default value is "Present".</span></span>|  
| <span data-ttu-id="60a58-116">PackageManager</span><span class="sxs-lookup"><span data-stu-id="60a58-116">PackageManager</span></span>| <span data-ttu-id="60a58-117">Podporované hodnoty jsou "yum", "výstižný" a "zypper".</span><span class="sxs-lookup"><span data-stu-id="60a58-117">Supported values are "yum", "apt", and "zypper".</span></span> <span data-ttu-id="60a58-118">Určuje Správce balíčků, které chcete použít při instalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="60a58-118">Specifies the package manager to use when installing packages.</span></span> <span data-ttu-id="60a58-119">Pokud **FilePath** je zadán, že zadaná cesta se použije k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="60a58-119">If **FilePath** is specified, the provided path will be used to install the package.</span></span> <span data-ttu-id="60a58-120">Správce balíčků, jinak hodnota použije k instalaci balíčku z předem nakonfigurovaná úložiště.</span><span class="sxs-lookup"><span data-stu-id="60a58-120">Otherwise, a Package Manager will be used to install the package from a pre-configured repository.</span></span> <span data-ttu-id="60a58-121">Pokud ani **PackageManager** ani **FilePath** součástí jsou výchozí Správce balíčků pro systém, který se použije.</span><span class="sxs-lookup"><span data-stu-id="60a58-121">If neither **PackageManager** nor **FilePath** are provided, the default package manager for the system will be used.</span></span>| 
| <span data-ttu-id="60a58-122">Cesta k souboru</span><span class="sxs-lookup"><span data-stu-id="60a58-122">FilePath</span></span>| <span data-ttu-id="60a58-123">Cesta k souboru, ve kterém se nachází balíček</span><span class="sxs-lookup"><span data-stu-id="60a58-123">The file path where the package resides</span></span>| 
| <span data-ttu-id="60a58-124">PackageGroup</span><span class="sxs-lookup"><span data-stu-id="60a58-124">PackageGroup</span></span>| <span data-ttu-id="60a58-125">Pokud **$true**, **název** musí být název skupiny balíček pro použití s **PackageManager**.</span><span class="sxs-lookup"><span data-stu-id="60a58-125">If **$true**, the **Name** is expected to be the name of a package group for use with a **PackageManager**.</span></span> <span data-ttu-id="60a58-126">**PacakgeGroup** není platný při poskytování **FilePath**.</span><span class="sxs-lookup"><span data-stu-id="60a58-126">**PacakgeGroup** is not valid when providing a **FilePath**.</span></span>| 
| <span data-ttu-id="60a58-127">Argumenty</span><span class="sxs-lookup"><span data-stu-id="60a58-127">Arguments</span></span>| <span data-ttu-id="60a58-128">Řetězec argumenty, které se předá do balíčku přesně tak, jak zadat.</span><span class="sxs-lookup"><span data-stu-id="60a58-128">A string of arguments that will be passed to the package exactly as provided.</span></span>| 
| <span data-ttu-id="60a58-129">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="60a58-129">ReturnCode</span></span>| <span data-ttu-id="60a58-130">Očekávaný návratový kód.</span><span class="sxs-lookup"><span data-stu-id="60a58-130">The expected return code.</span></span> <span data-ttu-id="60a58-131">Pokud skutečnou návratový kód neodpovídá očekávané hodnotě zadané tady že konfigurace vrátí chybu.</span><span class="sxs-lookup"><span data-stu-id="60a58-131">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>| 
| <span data-ttu-id="60a58-132">dependsOn</span><span class="sxs-lookup"><span data-stu-id="60a58-132">DependsOn</span></span> | <span data-ttu-id="60a58-133">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="60a58-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="60a58-134">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="60a58-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="60a58-135">Příklad</span><span class="sxs-lookup"><span data-stu-id="60a58-135">Example</span></span>

<span data-ttu-id="60a58-136">Následující příklad zajistí, že balíček s názvem "httpd" je nainstalovat na počítač se systémem Linux, pomocí Správce balíčků "Yum".</span><span class="sxs-lookup"><span data-stu-id="60a58-136">The following example ensures that the package named "httpd" is installed on a Linux computer, using the “Yum” package manager.</span></span>

```
Import-DSCResource -Module nx 

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```


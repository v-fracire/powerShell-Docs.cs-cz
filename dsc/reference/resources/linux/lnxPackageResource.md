---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxPackage
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048130"
---
# <a name="dsc-for-linux-nxpackage-resource"></a><span data-ttu-id="d7f42-103">DSC pro Linux prostředek nxPackage</span><span class="sxs-lookup"><span data-stu-id="d7f42-103">DSC for Linux nxPackage Resource</span></span>

<span data-ttu-id="d7f42-104">**NxPackage** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě balíčků na uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="d7f42-104">The **nxPackage** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage packages on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="d7f42-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d7f42-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="d7f42-106">Properties</span><span class="sxs-lookup"><span data-stu-id="d7f42-106">Properties</span></span>

|  <span data-ttu-id="d7f42-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="d7f42-107">Property</span></span> |  <span data-ttu-id="d7f42-108">Popis</span><span class="sxs-lookup"><span data-stu-id="d7f42-108">Description</span></span> |
|---|---|
| <span data-ttu-id="d7f42-109">Name</span><span class="sxs-lookup"><span data-stu-id="d7f42-109">Name</span></span>| <span data-ttu-id="d7f42-110">Název balíčku, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="d7f42-110">The name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="d7f42-111">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="d7f42-111">Ensure</span></span>| <span data-ttu-id="d7f42-112">Určuje, jestli se má zkontrolovat, zda balíček existuje.</span><span class="sxs-lookup"><span data-stu-id="d7f42-112">Determines whether to check if the package exists.</span></span> <span data-ttu-id="d7f42-113">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že balíček existuje.</span><span class="sxs-lookup"><span data-stu-id="d7f42-113">Set this property to "Present" to ensure the package exists.</span></span> <span data-ttu-id="d7f42-114">Nastavte ho na "Chybí" Ujistěte se, že balíček neexistuje.</span><span class="sxs-lookup"><span data-stu-id="d7f42-114">Set it to "Absent" to ensure the package does not exist.</span></span> <span data-ttu-id="d7f42-115">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="d7f42-115">The default value is "Present".</span></span>|
| <span data-ttu-id="d7f42-116">PackageManager</span><span class="sxs-lookup"><span data-stu-id="d7f42-116">PackageManager</span></span>| <span data-ttu-id="d7f42-117">Podporované hodnoty jsou "yumu", "apt" a "zypperu".</span><span class="sxs-lookup"><span data-stu-id="d7f42-117">Supported values are "yum", "apt", and "zypper".</span></span> <span data-ttu-id="d7f42-118">Určuje Správce balíčků pro použití při instalaci balíčků.</span><span class="sxs-lookup"><span data-stu-id="d7f42-118">Specifies the package manager to use when installing packages.</span></span> <span data-ttu-id="d7f42-119">Pokud **FilePath** není zadán, použije se zadaná cesta k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="d7f42-119">If **FilePath** is specified, the provided path will be used to install the package.</span></span> <span data-ttu-id="d7f42-120">V opačném případě se použije k instalaci balíčku z předem nakonfigurované úložiště Správce balíčků.</span><span class="sxs-lookup"><span data-stu-id="d7f42-120">Otherwise, a Package Manager will be used to install the package from a pre-configured repository.</span></span> <span data-ttu-id="d7f42-121">Pokud ani **PackageManager** ani **FilePath** jsou k dispozici, výchozí Správce balíčků pro systém, který se použije.</span><span class="sxs-lookup"><span data-stu-id="d7f42-121">If neither **PackageManager** nor **FilePath** are provided, the default package manager for the system will be used.</span></span>|
| <span data-ttu-id="d7f42-122">Cesta k souboru</span><span class="sxs-lookup"><span data-stu-id="d7f42-122">FilePath</span></span>| <span data-ttu-id="d7f42-123">Cesta k souboru, ve které se nachází balíček</span><span class="sxs-lookup"><span data-stu-id="d7f42-123">The file path where the package resides</span></span>|
| <span data-ttu-id="d7f42-124">PackageGroup</span><span class="sxs-lookup"><span data-stu-id="d7f42-124">PackageGroup</span></span>| <span data-ttu-id="d7f42-125">Pokud **$true**, **název** očekává se název skupiny balíčku pro použití se službou **PackageManager**.</span><span class="sxs-lookup"><span data-stu-id="d7f42-125">If **$true**, the **Name** is expected to be the name of a package group for use with a **PackageManager**.</span></span> <span data-ttu-id="d7f42-126">**PacakgeGroup** není platný při zadávání **FilePath**.</span><span class="sxs-lookup"><span data-stu-id="d7f42-126">**PacakgeGroup** is not valid when providing a **FilePath**.</span></span>|
| <span data-ttu-id="d7f42-127">Argumenty</span><span class="sxs-lookup"><span data-stu-id="d7f42-127">Arguments</span></span>| <span data-ttu-id="d7f42-128">Řetězec s argumenty, které budou předány do balíčku přesně tak, jak je uvedeno.</span><span class="sxs-lookup"><span data-stu-id="d7f42-128">A string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="d7f42-129">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="d7f42-129">ReturnCode</span></span>| <span data-ttu-id="d7f42-130">Očekávaný návratový kód.</span><span class="sxs-lookup"><span data-stu-id="d7f42-130">The expected return code.</span></span> <span data-ttu-id="d7f42-131">Pokud skutečný návratový kód neodpovídá očekávané hodnotě. k dispozici tady, že konfiguraci, vrátí se chyba.</span><span class="sxs-lookup"><span data-stu-id="d7f42-131">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|
| <span data-ttu-id="d7f42-132">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d7f42-132">DependsOn</span></span> | <span data-ttu-id="d7f42-133">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="d7f42-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d7f42-134">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d7f42-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="d7f42-135">Příklad</span><span class="sxs-lookup"><span data-stu-id="d7f42-135">Example</span></span>

<span data-ttu-id="d7f42-136">Následující příklad zajistí, že je nainstalován balíček s názvem "httpd" na počítači s Linuxem pomocí Správce balíčků "Yumu".</span><span class="sxs-lookup"><span data-stu-id="d7f42-136">The following example ensures that the package named "httpd" is installed on a Linux computer, using the “Yum” package manager.</span></span>

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
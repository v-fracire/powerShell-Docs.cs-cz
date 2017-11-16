---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxFileLine prostředků"
ms.openlocfilehash: bde42bbe217fc9acf5a3f2ee0136d30e2b5f2415
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxfileline-resource"></a><span data-ttu-id="efa6d-103">DSC pro Linux nxFileLine prostředků</span><span class="sxs-lookup"><span data-stu-id="efa6d-103">DSC for Linux nxFileLine Resource</span></span>

<span data-ttu-id="efa6d-104">**NxFileLine** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro ke správě řádky v konfiguračním souboru na uzlu Linux.</span><span class="sxs-lookup"><span data-stu-id="efa6d-104">The **nxFileLine** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage lines within a configuration file on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="efa6d-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="efa6d-105">Syntax</span></span>

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="efa6d-106">Properties</span><span class="sxs-lookup"><span data-stu-id="efa6d-106">Properties</span></span>

|  <span data-ttu-id="efa6d-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="efa6d-107">Property</span></span> |  <span data-ttu-id="efa6d-108">Popis</span><span class="sxs-lookup"><span data-stu-id="efa6d-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="efa6d-109">Cesta k souboru</span><span class="sxs-lookup"><span data-stu-id="efa6d-109">FilePath</span></span>| <span data-ttu-id="efa6d-110">Úplná cesta k souboru ke správě řádků v na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="efa6d-110">The full path to the file to manage lines in on the target node.</span></span>| 
| <span data-ttu-id="efa6d-111">ContainsLine</span><span class="sxs-lookup"><span data-stu-id="efa6d-111">ContainsLine</span></span>| <span data-ttu-id="efa6d-112">Řádek zajistit existuje v souboru.</span><span class="sxs-lookup"><span data-stu-id="efa6d-112">A line to ensure exists in the file.</span></span> <span data-ttu-id="efa6d-113">Tento řádek bude připojen k souboru, pokud neexistuje v souboru.</span><span class="sxs-lookup"><span data-stu-id="efa6d-113">This line will be appended to the file if it does not exist in the file.</span></span> <span data-ttu-id="efa6d-114">**ContainsLine** je povinná, ale můžete nastavit na prázdný řetězec ("ContainsLine =".) Pokud není nutné.</span><span class="sxs-lookup"><span data-stu-id="efa6d-114">**ContainsLine** is mandatory, but can be set to an empty string (`ContainsLine = ‘’`\`) if it is not needed.</span></span>| 
| <span data-ttu-id="efa6d-115">DoesNotContainPattern</span><span class="sxs-lookup"><span data-stu-id="efa6d-115">DoesNotContainPattern</span></span>| <span data-ttu-id="efa6d-116">Vzor regulárního výrazu řádky, které by neměly existovat v souboru.</span><span class="sxs-lookup"><span data-stu-id="efa6d-116">A regular expression pattern for lines that should not exist in the file.</span></span> <span data-ttu-id="efa6d-117">Pro všechny řádky, které existují v souboru odpovídající regulárnímu výrazu se odeberou ze souboru na řádku.</span><span class="sxs-lookup"><span data-stu-id="efa6d-117">For any lines that exist in the file that match this regular expression, the line will be removed from the file.</span></span>| 
| <span data-ttu-id="efa6d-118">dependsOn</span><span class="sxs-lookup"><span data-stu-id="efa6d-118">DependsOn</span></span> | <span data-ttu-id="efa6d-119">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="efa6d-119">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="efa6d-120">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="efa6d-120">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="efa6d-121">Příklad</span><span class="sxs-lookup"><span data-stu-id="efa6d-121">Example</span></span>

<span data-ttu-id="efa6d-122">Tento příklad ukazuje, jak pomocí **nxFileLine** prostředků ke konfiguraci `/etc/sudoers` souboru zajistit, aby uživatel: monuser nakonfigurovaný tak, aby není requiretty.</span><span class="sxs-lookup"><span data-stu-id="efa6d-122">This example demonstrates using the **nxFileLine** resource to configure the `/etc/sudoers` file, ensuring that the user: monuser is configured to not requiretty.</span></span>

```
Import-DSCResource -Module nx 

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
} 
```

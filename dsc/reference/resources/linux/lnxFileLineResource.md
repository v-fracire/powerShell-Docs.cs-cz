---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxFileLine
ms.openlocfilehash: 6a91db25638b09659adfabcec78f91bcb2e69dd9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048111"
---
# <a name="dsc-for-linux-nxfileline-resource"></a><span data-ttu-id="a9bb6-103">DSC pro Linux prostředek nxFileLine</span><span class="sxs-lookup"><span data-stu-id="a9bb6-103">DSC for Linux nxFileLine Resource</span></span>

<span data-ttu-id="a9bb6-104">**NxFileLine** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě řádky v konfiguračním souboru v systému Linux uzlu.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-104">The **nxFileLine** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage lines within a configuration file on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="a9bb6-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a9bb6-105">Syntax</span></span>

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="a9bb6-106">Properties</span><span class="sxs-lookup"><span data-stu-id="a9bb6-106">Properties</span></span>

|  <span data-ttu-id="a9bb6-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a9bb6-107">Property</span></span> |  <span data-ttu-id="a9bb6-108">Popis</span><span class="sxs-lookup"><span data-stu-id="a9bb6-108">Description</span></span> |
|---|---|
| <span data-ttu-id="a9bb6-109">Cesta k souboru</span><span class="sxs-lookup"><span data-stu-id="a9bb6-109">FilePath</span></span>| <span data-ttu-id="a9bb6-110">Úplná cesta k souboru, který má spravovat řádky v na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-110">The full path to the file to manage lines in on the target node.</span></span>|
| <span data-ttu-id="a9bb6-111">ContainsLine</span><span class="sxs-lookup"><span data-stu-id="a9bb6-111">ContainsLine</span></span>| <span data-ttu-id="a9bb6-112">Řádek zajistit existuje v souboru.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-112">A line to ensure exists in the file.</span></span> <span data-ttu-id="a9bb6-113">Tento řádek bude připojen k souboru, pokud neexistuje v souboru.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-113">This line will be appended to the file if it does not exist in the file.</span></span> <span data-ttu-id="a9bb6-114">**ContainsLine** je povinná, ale lze nastavit na prázdný řetězec (`ContainsLine = ""`) Pokud není potřeba.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-114">**ContainsLine** is mandatory, but can be set to an empty string (`ContainsLine = ""`) if it is not needed.</span></span>|
| <span data-ttu-id="a9bb6-115">DoesNotContainPattern</span><span class="sxs-lookup"><span data-stu-id="a9bb6-115">DoesNotContainPattern</span></span>| <span data-ttu-id="a9bb6-116">Vzor regulárního výrazu pro řádky, které by neměly existovat v souboru.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-116">A regular expression pattern for lines that should not exist in the file.</span></span> <span data-ttu-id="a9bb6-117">Pro všechny řádky, které existují v souboru, které odpovídají tento regulární výraz se odebere ze souboru řádek.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-117">For any lines that exist in the file that match this regular expression, the line will be removed from the file.</span></span>|
| <span data-ttu-id="a9bb6-118">DependsOn</span><span class="sxs-lookup"><span data-stu-id="a9bb6-118">DependsOn</span></span> | <span data-ttu-id="a9bb6-119">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-119">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a9bb6-120">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-120">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="a9bb6-121">Příklad</span><span class="sxs-lookup"><span data-stu-id="a9bb6-121">Example</span></span>

<span data-ttu-id="a9bb6-122">Tento příklad ukazuje použití **nxFileLine** prostředků ke konfiguraci `/etc/sudoers` souboru zajistit, aby uživatel: monuser nastavená na Ne requiretty.</span><span class="sxs-lookup"><span data-stu-id="a9bb6-122">This example demonstrates using the **nxFileLine** resource to configure the `/etc/sudoers` file, ensuring that the user: monuser is configured to not requiretty.</span></span>

```powershell
Import-DscResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```
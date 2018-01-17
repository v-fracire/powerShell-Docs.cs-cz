---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "WaitForAny prostředek DSC"
ms.openlocfilehash: 795c005c67c196ef9afb08af790fe2a1695392ec
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="42cea-103">WaitForAny prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="42cea-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="42cea-104">Platí pro: 5.1 a novějším se prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="42cea-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="42cea-105">**WaitForSome** prostředků konfigurace požadovaného stavu (DSC) lze použít v rámci bloku uzlu v [konfigurace DSC](configurations.md) určete závislosti na konfiguraci na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="42cea-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="42cea-106">Tento prostředek úspěšná, pokud Pokud prostředek určeného **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly, který je definovaný v **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="42cea-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="42cea-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="42cea-107">Syntax</span></span>

```
WaitForAny [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ] 
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="42cea-108">Properties</span><span class="sxs-lookup"><span data-stu-id="42cea-108">Properties</span></span>

|  <span data-ttu-id="42cea-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="42cea-109">Property</span></span>  |  <span data-ttu-id="42cea-110">Popis</span><span class="sxs-lookup"><span data-stu-id="42cea-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="42cea-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="42cea-111">ResourceName</span></span>| <span data-ttu-id="42cea-112">Název prostředku závislý na.</span><span class="sxs-lookup"><span data-stu-id="42cea-112">The resource name to depend on.</span></span>| 
| <span data-ttu-id="42cea-113">NodeName</span><span class="sxs-lookup"><span data-stu-id="42cea-113">NodeName</span></span>| <span data-ttu-id="42cea-114">Cílové uzly závislý na prostředku.</span><span class="sxs-lookup"><span data-stu-id="42cea-114">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="42cea-115">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="42cea-115">RetryIntervalSec</span></span>| <span data-ttu-id="42cea-116">Počet sekund, než se budete pokoušet.</span><span class="sxs-lookup"><span data-stu-id="42cea-116">The number of seconds before retrying.</span></span> <span data-ttu-id="42cea-117">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="42cea-117">Minimum is 1.</span></span>| 
| <span data-ttu-id="42cea-118">retryCount</span><span class="sxs-lookup"><span data-stu-id="42cea-118">RetryCount</span></span>| <span data-ttu-id="42cea-119">Maximální počet pokusů o opakování.</span><span class="sxs-lookup"><span data-stu-id="42cea-119">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="42cea-120">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="42cea-120">ThrottleLimit</span></span>| <span data-ttu-id="42cea-121">Počet počítačů pro připojení současně.</span><span class="sxs-lookup"><span data-stu-id="42cea-121">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="42cea-122">Výchozí hodnota je výchozí pro nové cimsession.</span><span class="sxs-lookup"><span data-stu-id="42cea-122">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="42cea-123">dependsOn</span><span class="sxs-lookup"><span data-stu-id="42cea-123">DependsOn</span></span> | <span data-ttu-id="42cea-124">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="42cea-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="42cea-125">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="42cea-125">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="42cea-126">Příklad</span><span class="sxs-lookup"><span data-stu-id="42cea-126">Example</span></span>

<span data-ttu-id="42cea-127">Příklad toho, jak používat tento prostředek, naleznete v části [určení závislostí mezi uzly](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="42cea-127">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>


---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "WaitForAny prostředek DSC"
ms.openlocfilehash: 43922dbcccb6d06d7d9edfcf16ce4eb107e9d4e6
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="a4686-103">WaitForAny prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="a4686-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="a4686-104">Platí pro: 5.1 a novějším se prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4686-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="a4686-105">**WaitForSome** prostředků konfigurace požadovaného stavu (DSC) lze použít v rámci bloku uzlu v [konfigurace DSC](configurations.md) určete závislosti na konfiguraci na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="a4686-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="a4686-106">Tento prostředek úspěšná, pokud Pokud prostředek určeného **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly, který je definovaný v **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="a4686-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="a4686-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a4686-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="a4686-108">Properties</span><span class="sxs-lookup"><span data-stu-id="a4686-108">Properties</span></span>

|  <span data-ttu-id="a4686-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a4686-109">Property</span></span>  |  <span data-ttu-id="a4686-110">Popis</span><span class="sxs-lookup"><span data-stu-id="a4686-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="a4686-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="a4686-111">ResourceName</span></span>| <span data-ttu-id="a4686-112">Název prostředku závislý na.</span><span class="sxs-lookup"><span data-stu-id="a4686-112">The resource name to depend on.</span></span> <span data-ttu-id="a4686-113">Pokud tento prostředek patří do jiné konfigurace, formátu názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="a4686-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>| 
| <span data-ttu-id="a4686-114">NodeName</span><span class="sxs-lookup"><span data-stu-id="a4686-114">NodeName</span></span>| <span data-ttu-id="a4686-115">Cílové uzly závislý na prostředku.</span><span class="sxs-lookup"><span data-stu-id="a4686-115">The target nodes of the resource to depend on.</span></span>| 
| <span data-ttu-id="a4686-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="a4686-116">RetryIntervalSec</span></span>| <span data-ttu-id="a4686-117">Počet sekund, než se budete pokoušet.</span><span class="sxs-lookup"><span data-stu-id="a4686-117">The number of seconds before retrying.</span></span> <span data-ttu-id="a4686-118">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="a4686-118">Minimum is 1.</span></span>| 
| <span data-ttu-id="a4686-119">retryCount</span><span class="sxs-lookup"><span data-stu-id="a4686-119">RetryCount</span></span>| <span data-ttu-id="a4686-120">Maximální počet pokusů o opakování.</span><span class="sxs-lookup"><span data-stu-id="a4686-120">The maximum number of times to retry.</span></span>| 
| <span data-ttu-id="a4686-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="a4686-121">ThrottleLimit</span></span>| <span data-ttu-id="a4686-122">Počet počítačů pro připojení současně.</span><span class="sxs-lookup"><span data-stu-id="a4686-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="a4686-123">Výchozí hodnota je výchozí pro nové cimsession.</span><span class="sxs-lookup"><span data-stu-id="a4686-123">Default is new-cimsession default.</span></span>| 
| <span data-ttu-id="a4686-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a4686-124">DependsOn</span></span> | <span data-ttu-id="a4686-125">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="a4686-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a4686-126">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a4686-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="a4686-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="a4686-127">Example</span></span>

<span data-ttu-id="a4686-128">Příklad toho, jak používat tento prostředek, naleznete v části [určení závislostí mezi uzly](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="a4686-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>


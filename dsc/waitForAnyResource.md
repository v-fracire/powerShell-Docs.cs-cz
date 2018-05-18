---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: WaitForAny prostředek DSC
ms.openlocfilehash: c9700c908f8601db85f9c922445969a34b59d453
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="8355a-103">WaitForAny prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="8355a-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="8355a-104">Platí pro: 5.1 a novějším se prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="8355a-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="8355a-105">**WaitForSome** prostředků konfigurace požadovaného stavu (DSC) lze použít v rámci bloku uzlu v [konfigurace DSC](configurations.md) určete závislosti na konfiguraci na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="8355a-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="8355a-106">Tento prostředek úspěšná, pokud Pokud prostředek určeného **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly, který je definovaný v **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="8355a-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="8355a-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="8355a-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="8355a-108">Properties</span><span class="sxs-lookup"><span data-stu-id="8355a-108">Properties</span></span>

|  <span data-ttu-id="8355a-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="8355a-109">Property</span></span>  |  <span data-ttu-id="8355a-110">Popis</span><span class="sxs-lookup"><span data-stu-id="8355a-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="8355a-111">resourceName</span><span class="sxs-lookup"><span data-stu-id="8355a-111">ResourceName</span></span>| <span data-ttu-id="8355a-112">Název prostředku závislý na.</span><span class="sxs-lookup"><span data-stu-id="8355a-112">The resource name to depend on.</span></span> <span data-ttu-id="8355a-113">Pokud tento prostředek patří do jiné konfigurace, formátu názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="8355a-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="8355a-114">nodeName</span><span class="sxs-lookup"><span data-stu-id="8355a-114">NodeName</span></span>| <span data-ttu-id="8355a-115">Cílové uzly závislý na prostředku.</span><span class="sxs-lookup"><span data-stu-id="8355a-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="8355a-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="8355a-116">RetryIntervalSec</span></span>| <span data-ttu-id="8355a-117">Počet sekund, než se budete pokoušet.</span><span class="sxs-lookup"><span data-stu-id="8355a-117">The number of seconds before retrying.</span></span> <span data-ttu-id="8355a-118">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="8355a-118">Minimum is 1.</span></span>|
| <span data-ttu-id="8355a-119">retryCount</span><span class="sxs-lookup"><span data-stu-id="8355a-119">RetryCount</span></span>| <span data-ttu-id="8355a-120">Maximální počet pokusů o opakování.</span><span class="sxs-lookup"><span data-stu-id="8355a-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="8355a-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="8355a-121">ThrottleLimit</span></span>| <span data-ttu-id="8355a-122">Počet počítačů pro připojení současně.</span><span class="sxs-lookup"><span data-stu-id="8355a-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="8355a-123">Výchozí hodnota je výchozí pro nové cimsession.</span><span class="sxs-lookup"><span data-stu-id="8355a-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="8355a-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="8355a-124">DependsOn</span></span> | <span data-ttu-id="8355a-125">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="8355a-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="8355a-126">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="8355a-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="8355a-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="8355a-127">Example</span></span>

<span data-ttu-id="8355a-128">Příklad toho, jak používat tento prostředek, naleznete v části [určení závislostí mezi uzly](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="8355a-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>
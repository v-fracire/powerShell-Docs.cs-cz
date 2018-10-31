---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: WaitForAll prostředků DSC
ms.openlocfilehash: 367f95caaa71ebec9c8e0a7c31fa5c0f5be27945
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226096"
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="68997-103">WaitForAll prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="68997-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="68997-104">Platí pro: 5.0 a novější se prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="68997-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="68997-105">**WaitForAll** Desired State Configuration (DSC) prostředku se dá použít v bloku uzlu v [konfigurace DSC](configurations.md) postup určení závislostí pro konfigurací na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="68997-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="68997-106">Tento prostředek proběhne úspěšně, pokud zadaný prostředek podle **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly podle **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="68997-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="68997-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="68997-107">Syntax</span></span>

```
WaitForAll [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ]
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="68997-108">Properties</span><span class="sxs-lookup"><span data-stu-id="68997-108">Properties</span></span>

|  <span data-ttu-id="68997-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="68997-109">Property</span></span>  |  <span data-ttu-id="68997-110">Popis</span><span class="sxs-lookup"><span data-stu-id="68997-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="68997-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="68997-111">ResourceName</span></span>| <span data-ttu-id="68997-112">Název prostředku, aby závisely na.</span><span class="sxs-lookup"><span data-stu-id="68997-112">The resource name to depend on.</span></span> <span data-ttu-id="68997-113">Pokud tento prostředek patří do jiné konfigurace, formátování názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="68997-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="68997-114">NodeName</span><span class="sxs-lookup"><span data-stu-id="68997-114">NodeName</span></span>| <span data-ttu-id="68997-115">Cílové uzly jsou závislé na prostředku.</span><span class="sxs-lookup"><span data-stu-id="68997-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="68997-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="68997-116">RetryIntervalSec</span></span>| <span data-ttu-id="68997-117">Počet sekund, než to zkusíte znovu.</span><span class="sxs-lookup"><span data-stu-id="68997-117">The number of seconds before retrying.</span></span> <span data-ttu-id="68997-118">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="68997-118">Minimum is 1.</span></span>|
| <span data-ttu-id="68997-119">retryCount</span><span class="sxs-lookup"><span data-stu-id="68997-119">RetryCount</span></span>| <span data-ttu-id="68997-120">Maximální počet pokusů o zopakování.</span><span class="sxs-lookup"><span data-stu-id="68997-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="68997-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="68997-121">ThrottleLimit</span></span>| <span data-ttu-id="68997-122">Počet počítačů současně připojit.</span><span class="sxs-lookup"><span data-stu-id="68997-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="68997-123">Výchozí hodnota je nový cimsession výchozí.</span><span class="sxs-lookup"><span data-stu-id="68997-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="68997-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="68997-124">DependsOn</span></span> | <span data-ttu-id="68997-125">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="68997-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="68997-126">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="68997-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="68997-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="68997-127">Example</span></span>

<span data-ttu-id="68997-128">Příklad toho, jak používat tento prostředek, naleznete v tématu [určení závislostí mezi uzly](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="68997-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>
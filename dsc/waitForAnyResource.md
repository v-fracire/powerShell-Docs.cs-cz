---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: WaitForAny prostředků DSC
ms.openlocfilehash: 39100f0fc52092c54bbecab55e3ef3dfabb4c70e
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226045"
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="9d9a4-103">WaitForAny prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="9d9a4-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="9d9a4-104">Platí pro: 5.1 a novější se prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d9a4-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="9d9a4-105">**WaitForSome** Desired State Configuration (DSC) prostředku se dá použít v bloku uzlu v [konfigurace DSC](configurations.md) postup určení závislostí pro konfigurací na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="9d9a4-106">Tento prostředek proběhne úspěšně, pokud zadaný prostředek podle **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly podle **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="9d9a4-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9d9a4-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="9d9a4-108">Properties</span><span class="sxs-lookup"><span data-stu-id="9d9a4-108">Properties</span></span>

|  <span data-ttu-id="9d9a4-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="9d9a4-109">Property</span></span>  |  <span data-ttu-id="9d9a4-110">Popis</span><span class="sxs-lookup"><span data-stu-id="9d9a4-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="9d9a4-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="9d9a4-111">ResourceName</span></span>| <span data-ttu-id="9d9a4-112">Název prostředku, aby závisely na.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-112">The resource name to depend on.</span></span> <span data-ttu-id="9d9a4-113">Pokud tento prostředek patří do jiné konfigurace, formátování názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="9d9a4-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="9d9a4-114">NodeName</span><span class="sxs-lookup"><span data-stu-id="9d9a4-114">NodeName</span></span>| <span data-ttu-id="9d9a4-115">Cílové uzly jsou závislé na prostředku.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="9d9a4-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="9d9a4-116">RetryIntervalSec</span></span>| <span data-ttu-id="9d9a4-117">Počet sekund, než to zkusíte znovu.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-117">The number of seconds before retrying.</span></span> <span data-ttu-id="9d9a4-118">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-118">Minimum is 1.</span></span>|
| <span data-ttu-id="9d9a4-119">retryCount</span><span class="sxs-lookup"><span data-stu-id="9d9a4-119">RetryCount</span></span>| <span data-ttu-id="9d9a4-120">Maximální počet pokusů o zopakování.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="9d9a4-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="9d9a4-121">ThrottleLimit</span></span>| <span data-ttu-id="9d9a4-122">Počet počítačů současně připojit.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="9d9a4-123">Výchozí hodnota je nový cimsession výchozí.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="9d9a4-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="9d9a4-124">DependsOn</span></span> | <span data-ttu-id="9d9a4-125">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9d9a4-126">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="9d9a4-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="9d9a4-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="9d9a4-127">Example</span></span>

<span data-ttu-id="9d9a4-128">Příklad toho, jak používat tento prostředek, naleznete v tématu [určení závislostí mezi uzly](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="9d9a4-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>
---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: WaitForAll prostředků DSC
ms.openlocfilehash: 1e891f1aecbdbe641973669f71f22664ad8ea16c
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048144"
---
# <a name="dsc-waitforall-resource"></a><span data-ttu-id="75679-103">WaitForAll prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="75679-103">DSC WaitForAll Resource</span></span>

> <span data-ttu-id="75679-104">Platí pro: Prostředí Windows PowerShell 5.0 a novější</span><span class="sxs-lookup"><span data-stu-id="75679-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="75679-105">**WaitForAll** Desired State Configuration (DSC) prostředku se dá použít v bloku uzlu v [konfigurace DSC](../../../configurations/configurations.md) postup určení závislostí pro konfigurací na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="75679-105">The **WaitForAll** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="75679-106">Tento prostředek proběhne úspěšně, pokud zadaný prostředek podle **ResourceName** vlastnost je v požadovaném stavu na všechny cílové uzly podle **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="75679-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on all target nodes defined in the **NodeName** property.</span></span>

## <a name="syntax"></a><span data-ttu-id="75679-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="75679-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="75679-108">Properties</span><span class="sxs-lookup"><span data-stu-id="75679-108">Properties</span></span>

|  <span data-ttu-id="75679-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="75679-109">Property</span></span>  |  <span data-ttu-id="75679-110">Popis</span><span class="sxs-lookup"><span data-stu-id="75679-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="75679-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="75679-111">ResourceName</span></span>| <span data-ttu-id="75679-112">Název prostředku, aby závisely na.</span><span class="sxs-lookup"><span data-stu-id="75679-112">The resource name to depend on.</span></span> <span data-ttu-id="75679-113">Pokud tento prostředek patří do jiné konfigurace, formátování názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="75679-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="75679-114">NodeName</span><span class="sxs-lookup"><span data-stu-id="75679-114">NodeName</span></span>| <span data-ttu-id="75679-115">Cílové uzly jsou závislé na prostředku.</span><span class="sxs-lookup"><span data-stu-id="75679-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="75679-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="75679-116">RetryIntervalSec</span></span>| <span data-ttu-id="75679-117">Počet sekund, než to zkusíte znovu.</span><span class="sxs-lookup"><span data-stu-id="75679-117">The number of seconds before retrying.</span></span> <span data-ttu-id="75679-118">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="75679-118">Minimum is 1.</span></span>|
| <span data-ttu-id="75679-119">retryCount</span><span class="sxs-lookup"><span data-stu-id="75679-119">RetryCount</span></span>| <span data-ttu-id="75679-120">Maximální počet pokusů o zopakování.</span><span class="sxs-lookup"><span data-stu-id="75679-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="75679-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="75679-121">ThrottleLimit</span></span>| <span data-ttu-id="75679-122">Počet počítačů současně připojit.</span><span class="sxs-lookup"><span data-stu-id="75679-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="75679-123">Výchozí hodnota je nový cimsession výchozí.</span><span class="sxs-lookup"><span data-stu-id="75679-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="75679-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="75679-124">DependsOn</span></span> | <span data-ttu-id="75679-125">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="75679-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="75679-126">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="75679-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="75679-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="75679-127">Example</span></span>

<span data-ttu-id="75679-128">Příklad toho, jak používat tento prostředek, naleznete v tématu [určení závislostí mezi uzly](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="75679-128">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>

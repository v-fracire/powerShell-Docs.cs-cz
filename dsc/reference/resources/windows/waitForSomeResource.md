---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: WaitForSome prostředků DSC
ms.openlocfilehash: 906375a8fcf9b87d4b7487e63e6fae3f05b86d0d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048117"
---
# <a name="dsc-waitforsome-resource"></a><span data-ttu-id="3fffa-103">WaitForSome prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="3fffa-103">DSC WaitForSome Resource</span></span>

> <span data-ttu-id="3fffa-104">Platí pro: Prostředí Windows PowerShell 5.0 a novější</span><span class="sxs-lookup"><span data-stu-id="3fffa-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="3fffa-105">**WaitForAny** Desired State Configuration (DSC) prostředku se dá použít v bloku uzlu v [konfigurace DSC](../../../configurations/configurations.md) postup určení závislostí pro konfigurací na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="3fffa-105">The **WaitForAny** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="3fffa-106">Tento prostředek proběhne úspěšně, pokud zadaný prostředek podle **ResourceName** vlastnost je v požadovaném stavu na minimální počet uzlů (určená **NodeCount**) definované **NodeName**  vlastnost.</span><span class="sxs-lookup"><span data-stu-id="3fffa-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="3fffa-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="3fffa-107">Syntax</span></span>

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

## <a name="properties"></a><span data-ttu-id="3fffa-108">Properties</span><span class="sxs-lookup"><span data-stu-id="3fffa-108">Properties</span></span>

|  <span data-ttu-id="3fffa-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="3fffa-109">Property</span></span>  |  <span data-ttu-id="3fffa-110">Popis</span><span class="sxs-lookup"><span data-stu-id="3fffa-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="3fffa-111">NodeCount</span><span class="sxs-lookup"><span data-stu-id="3fffa-111">NodeCount</span></span>| <span data-ttu-id="3fffa-112">Minimální počet uzlů, které musí být v požadovaném stavu pro tento prostředek proběhla úspěšně.</span><span class="sxs-lookup"><span data-stu-id="3fffa-112">The minimum number of nodes that must be in the desired state for this resource to succeed.</span></span>|
| <span data-ttu-id="3fffa-113">NodeName</span><span class="sxs-lookup"><span data-stu-id="3fffa-113">NodeName</span></span>| <span data-ttu-id="3fffa-114">Cílové uzly jsou závislé na prostředku.</span><span class="sxs-lookup"><span data-stu-id="3fffa-114">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="3fffa-115">ResourceName</span><span class="sxs-lookup"><span data-stu-id="3fffa-115">ResourceName</span></span>| <span data-ttu-id="3fffa-116">Název prostředku, aby závisely na.</span><span class="sxs-lookup"><span data-stu-id="3fffa-116">The resource name to depend on.</span></span> <span data-ttu-id="3fffa-117">Pokud tento prostředek patří do jiné konfigurace, formátování názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="3fffa-117">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="3fffa-118">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="3fffa-118">RetryIntervalSec</span></span>| <span data-ttu-id="3fffa-119">Počet sekund, než to zkusíte znovu.</span><span class="sxs-lookup"><span data-stu-id="3fffa-119">The number of seconds before retrying.</span></span> <span data-ttu-id="3fffa-120">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="3fffa-120">Minimum is 1.</span></span>|
| <span data-ttu-id="3fffa-121">retryCount</span><span class="sxs-lookup"><span data-stu-id="3fffa-121">RetryCount</span></span>| <span data-ttu-id="3fffa-122">Maximální počet pokusů o zopakování.</span><span class="sxs-lookup"><span data-stu-id="3fffa-122">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="3fffa-123">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="3fffa-123">ThrottleLimit</span></span>| <span data-ttu-id="3fffa-124">Počet počítačů současně připojit.</span><span class="sxs-lookup"><span data-stu-id="3fffa-124">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="3fffa-125">Výchozí hodnota je nový cimsession výchozí.</span><span class="sxs-lookup"><span data-stu-id="3fffa-125">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="3fffa-126">DependsOn</span><span class="sxs-lookup"><span data-stu-id="3fffa-126">DependsOn</span></span> | <span data-ttu-id="3fffa-127">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="3fffa-127">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="3fffa-128">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="3fffa-128">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="3fffa-129">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="3fffa-129">PsDscRunAsCredential</span></span> | <span data-ttu-id="3fffa-130">Zobrazit [DSC pomocí uživatelských přihlašovacích údajů](https://docs.microsoft.com/powershell/dsc/runasuser)</span><span class="sxs-lookup"><span data-stu-id="3fffa-130">See [Using DSC with User Credentials](https://docs.microsoft.com/powershell/dsc/runasuser)</span></span> |

## <a name="example"></a><span data-ttu-id="3fffa-131">Příklad</span><span class="sxs-lookup"><span data-stu-id="3fffa-131">Example</span></span>

<span data-ttu-id="3fffa-132">Příklad toho, jak používat tento prostředek, naleznete v tématu [určení závislostí mezi uzly](../../../configurations/crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="3fffa-132">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>

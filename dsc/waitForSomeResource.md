---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: WaitForSome prostředek DSC
ms.openlocfilehash: 08a5b96bee0b1b4475470e0d857dca79dee2b02e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-waitforsome-resource"></a><span data-ttu-id="a3a85-103">WaitForSome prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="a3a85-103">DSC WaitForSome Resource</span></span>

> <span data-ttu-id="a3a85-104">Platí pro: 5.0 a novější se prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3a85-104">Applies To: Windows PowerShell 5.0 and later</span></span>

<span data-ttu-id="a3a85-105">**WaitForAny** prostředků konfigurace požadovaného stavu (DSC) lze použít v rámci bloku uzlu v [konfigurace DSC](configurations.md) určete závislosti na konfiguraci na jiných uzlech.</span><span class="sxs-lookup"><span data-stu-id="a3a85-105">The **WaitForAny** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="a3a85-106">Tento prostředek úspěšná, pokud prostředek určeného **ResourceName** vlastnost je v požadovaném stavu na minimální počet uzlů (zadáno v **NodeCount**) definované **NodeName**  vlastnost.</span><span class="sxs-lookup"><span data-stu-id="a3a85-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="a3a85-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a3a85-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="a3a85-108">Properties</span><span class="sxs-lookup"><span data-stu-id="a3a85-108">Properties</span></span>

|  <span data-ttu-id="a3a85-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a3a85-109">Property</span></span>  |  <span data-ttu-id="a3a85-110">Popis</span><span class="sxs-lookup"><span data-stu-id="a3a85-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="a3a85-111">NodeCount</span><span class="sxs-lookup"><span data-stu-id="a3a85-111">NodeCount</span></span>| <span data-ttu-id="a3a85-112">Minimální počet uzlů, které musí být v požadovaném stavu pro tento prostředek proběhla úspěšně.</span><span class="sxs-lookup"><span data-stu-id="a3a85-112">The minimum number of nodes that must be in the desired state for this resource to succeed.</span></span>|
| <span data-ttu-id="a3a85-113">nodeName</span><span class="sxs-lookup"><span data-stu-id="a3a85-113">NodeName</span></span>| <span data-ttu-id="a3a85-114">Cílové uzly závislý na prostředku.</span><span class="sxs-lookup"><span data-stu-id="a3a85-114">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="a3a85-115">resourceName</span><span class="sxs-lookup"><span data-stu-id="a3a85-115">ResourceName</span></span>| <span data-ttu-id="a3a85-116">Název prostředku závislý na.</span><span class="sxs-lookup"><span data-stu-id="a3a85-116">The resource name to depend on.</span></span> <span data-ttu-id="a3a85-117">Pokud tento prostředek patří do jiné konfigurace, formátu názvu jako "[__ResourceType__]__ResourceName__:: [__ConfigurationName__]:: [ __ConfigurationName__] "</span><span class="sxs-lookup"><span data-stu-id="a3a85-117">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="a3a85-118">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="a3a85-118">RetryIntervalSec</span></span>| <span data-ttu-id="a3a85-119">Počet sekund, než se budete pokoušet.</span><span class="sxs-lookup"><span data-stu-id="a3a85-119">The number of seconds before retrying.</span></span> <span data-ttu-id="a3a85-120">Minimální hodnota je 1.</span><span class="sxs-lookup"><span data-stu-id="a3a85-120">Minimum is 1.</span></span>|
| <span data-ttu-id="a3a85-121">retryCount</span><span class="sxs-lookup"><span data-stu-id="a3a85-121">RetryCount</span></span>| <span data-ttu-id="a3a85-122">Maximální počet pokusů o opakování.</span><span class="sxs-lookup"><span data-stu-id="a3a85-122">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="a3a85-123">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="a3a85-123">ThrottleLimit</span></span>| <span data-ttu-id="a3a85-124">Počet počítačů pro připojení současně.</span><span class="sxs-lookup"><span data-stu-id="a3a85-124">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="a3a85-125">Výchozí hodnota je výchozí pro nové cimsession.</span><span class="sxs-lookup"><span data-stu-id="a3a85-125">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="a3a85-126">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a3a85-126">DependsOn</span></span> | <span data-ttu-id="a3a85-127">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="a3a85-127">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a3a85-128">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a3a85-128">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="a3a85-129">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="a3a85-129">PsDscRunAsCredential</span></span> | <span data-ttu-id="a3a85-130">V tématu [DSC pomocí uživatelských přihlašovacích údajů](https://docs.microsoft.com/powershell/dsc/runasuser)</span><span class="sxs-lookup"><span data-stu-id="a3a85-130">See [Using DSC with User Credentials](https://docs.microsoft.com/powershell/dsc/runasuser)</span></span> |


## <a name="example"></a><span data-ttu-id="a3a85-131">Příklad</span><span class="sxs-lookup"><span data-stu-id="a3a85-131">Example</span></span>

<span data-ttu-id="a3a85-132">Příklad toho, jak používat tento prostředek, naleznete v části [určení závislostí mezi uzly](crossNodeDependencies.md)</span><span class="sxs-lookup"><span data-stu-id="a3a85-132">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>
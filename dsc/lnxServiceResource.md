---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxService prostředků"
ms.openlocfilehash: be9f1f090eacc38bcdb77e53020d559bab72c156
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxservice-resource"></a><span data-ttu-id="95690-103">DSC pro Linux nxService prostředků</span><span class="sxs-lookup"><span data-stu-id="95690-103">DSC for Linux nxService Resource</span></span>

<span data-ttu-id="95690-104">**NxService** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě služeb v uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="95690-104">The **nxService** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="95690-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="95690-105">Syntax</span></span>

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd }  ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="95690-106">Properties</span><span class="sxs-lookup"><span data-stu-id="95690-106">Properties</span></span>
|  <span data-ttu-id="95690-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="95690-107">Property</span></span> |  <span data-ttu-id="95690-108">Popis</span><span class="sxs-lookup"><span data-stu-id="95690-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="95690-109">Název</span><span class="sxs-lookup"><span data-stu-id="95690-109">Name</span></span>| <span data-ttu-id="95690-110">Název služby nebo démon ke konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="95690-110">The name of the service/daemon to configure.</span></span>| 
| <span data-ttu-id="95690-111">Řadiče</span><span class="sxs-lookup"><span data-stu-id="95690-111">Controller</span></span>| <span data-ttu-id="95690-112">Typ řadiče služby použít při konfiguraci služby.</span><span class="sxs-lookup"><span data-stu-id="95690-112">The type of service controller to use when configuring the service.</span></span>| 
| <span data-ttu-id="95690-113">Povoleno</span><span class="sxs-lookup"><span data-stu-id="95690-113">Enabled</span></span>| <span data-ttu-id="95690-114">Určuje, zda byla služba spuštěna při spuštění.</span><span class="sxs-lookup"><span data-stu-id="95690-114">Indicates whether the service starts on boot.</span></span>| 
| <span data-ttu-id="95690-115">Stav</span><span class="sxs-lookup"><span data-stu-id="95690-115">State</span></span>| <span data-ttu-id="95690-116">Určuje, zda je služba spuštěná.</span><span class="sxs-lookup"><span data-stu-id="95690-116">Indicates whether the service is running.</span></span> <span data-ttu-id="95690-117">Nastavením této vlastnosti "Stopped" zajistit, že služba není spuštěná.</span><span class="sxs-lookup"><span data-stu-id="95690-117">Set this property to "Stopped" to ensure that the service is not running.</span></span> <span data-ttu-id="95690-118">Nastavte ji na "Spuštěný" zajistit, že služba není spuštěná.</span><span class="sxs-lookup"><span data-stu-id="95690-118">Set it to "Running" to ensure that the service is not running.</span></span>| 
| <span data-ttu-id="95690-119">dependsOn</span><span class="sxs-lookup"><span data-stu-id="95690-119">DependsOn</span></span> | <span data-ttu-id="95690-120">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="95690-120">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="95690-121">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="95690-121">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 


## <a name="additional-information"></a><span data-ttu-id="95690-122">Další informace</span><span class="sxs-lookup"><span data-stu-id="95690-122">Additional Information</span></span>

<span data-ttu-id="95690-123">**NxService** prostředků nebude vytvořit definici služby nebo skriptu pro službu, pokud neexistuje.</span><span class="sxs-lookup"><span data-stu-id="95690-123">The **nxService** resource will not create a service definition or script for the service if it does not exist.</span></span> <span data-ttu-id="95690-124">Můžete použít prostředí PowerShell konfigurace požadovaného stavu **nxFile** prostředků prostředků ke správě existence nebo obsah souboru definice služby nebo skriptu.</span><span class="sxs-lookup"><span data-stu-id="95690-124">You can use the PowerShell Desired State Configuration **nxFile** Resource resource to manage the existence or contents of the service definition file or script.</span></span>

## <a name="example"></a><span data-ttu-id="95690-125">Příklad</span><span class="sxs-lookup"><span data-stu-id="95690-125">Example</span></span>

<span data-ttu-id="95690-126">Následující příklad ukazuje konfiguraci služby "httpd" (pro serveru Apache HTTP Server), zaregistrována **SystemD** řadič služby.</span><span class="sxs-lookup"><span data-stu-id="95690-126">The following example shows configuration of the “httpd” service (for Apache HTTP Server), registered with the **SystemD** service controller.</span></span>

```
Import-DSCResource -Module nx 

Node $node {
#Apache Service
nxService ApacheService 
{
Name = "httpd"
State = "running"
Enabled = $true
Controller = "systemd"
}
}
```


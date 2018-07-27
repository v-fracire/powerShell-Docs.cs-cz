---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxService
ms.openlocfilehash: fe8043995205649378725f2ab0a78e19313739c9
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267775"
---
# <a name="dsc-for-linux-nxservice-resource"></a><span data-ttu-id="0d437-103">DSC pro Linux prostředek nxService</span><span class="sxs-lookup"><span data-stu-id="0d437-103">DSC for Linux nxService Resource</span></span>

<span data-ttu-id="0d437-104">**NxService** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě služeb na uzlech systému Linux.</span><span class="sxs-lookup"><span data-stu-id="0d437-104">The **nxService** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="0d437-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0d437-105">Syntax</span></span>

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd } ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a><span data-ttu-id="0d437-106">Properties</span><span class="sxs-lookup"><span data-stu-id="0d437-106">Properties</span></span>

| <span data-ttu-id="0d437-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0d437-107">Property</span></span> | <span data-ttu-id="0d437-108">Popis</span><span class="sxs-lookup"><span data-stu-id="0d437-108">Description</span></span> |
|---|---|
| <span data-ttu-id="0d437-109">Název</span><span class="sxs-lookup"><span data-stu-id="0d437-109">Name</span></span>| <span data-ttu-id="0d437-110">Název služby/démona ke konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="0d437-110">The name of the service/daemon to configure.</span></span>|
| <span data-ttu-id="0d437-111">Kontroler</span><span class="sxs-lookup"><span data-stu-id="0d437-111">Controller</span></span>| <span data-ttu-id="0d437-112">Typ služby řadiče pro použití při konfiguraci služby.</span><span class="sxs-lookup"><span data-stu-id="0d437-112">The type of service controller to use when configuring the service.</span></span>|
| <span data-ttu-id="0d437-113">Povoleno</span><span class="sxs-lookup"><span data-stu-id="0d437-113">Enabled</span></span>| <span data-ttu-id="0d437-114">Určuje, zda bude služba spuštěna při spuštění.</span><span class="sxs-lookup"><span data-stu-id="0d437-114">Indicates whether the service starts on boot.</span></span>|
| <span data-ttu-id="0d437-115">Stav</span><span class="sxs-lookup"><span data-stu-id="0d437-115">State</span></span>| <span data-ttu-id="0d437-116">Určuje, zda je služba spuštěna.</span><span class="sxs-lookup"><span data-stu-id="0d437-116">Indicates whether the service is running.</span></span> <span data-ttu-id="0d437-117">Nastavte tuto vlastnost na "Stopped" Ujistěte se, že služba není spuštěná.</span><span class="sxs-lookup"><span data-stu-id="0d437-117">Set this property to "Stopped" to ensure that the service is not running.</span></span> <span data-ttu-id="0d437-118">Nastavte na "Spuštěno" Ujistěte se, že služba není spuštěná.</span><span class="sxs-lookup"><span data-stu-id="0d437-118">Set it to "Running" to ensure that the service is not running.</span></span>|
| <span data-ttu-id="0d437-119">DependsOn</span><span class="sxs-lookup"><span data-stu-id="0d437-119">DependsOn</span></span> | <span data-ttu-id="0d437-120">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="0d437-120">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="0d437-121">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="0d437-121">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="0d437-122">Další informace</span><span class="sxs-lookup"><span data-stu-id="0d437-122">Additional Information</span></span>

<span data-ttu-id="0d437-123">**NxService** prostředek nebude vytvořit definice nebo skript pro službu, pokud neexistuje.</span><span class="sxs-lookup"><span data-stu-id="0d437-123">The **nxService** resource will not create a service definition or script for the service if it does not exist.</span></span> <span data-ttu-id="0d437-124">Můžete použít PowerShell Desired State Configuration **nxFile** prostředky ke správě existenci nebo obsah definičního souboru služby nebo skriptu.</span><span class="sxs-lookup"><span data-stu-id="0d437-124">You can use the PowerShell Desired State Configuration **nxFile** Resource resource to manage the existence or contents of the service definition file or script.</span></span>

## <a name="example"></a><span data-ttu-id="0d437-125">Příklad</span><span class="sxs-lookup"><span data-stu-id="0d437-125">Example</span></span>

<span data-ttu-id="0d437-126">Následující příklad ukazuje konfiguraci služby "httpd" (v případě serveru Apache HTTP Server), zaregistrované **SystemD** řadič služby.</span><span class="sxs-lookup"><span data-stu-id="0d437-126">The following example shows configuration of the 'httpd' service (for Apache HTTP Server), registered with the **SystemD** service controller.</span></span>

```powershell
Import-DSCResource -Module nx

Node $node {
    #Apache Service
    nxService ApacheService {
        Name = 'httpd'
        State = 'running'
        Enabled = $true
        Controller = 'systemd'
    }
}
```
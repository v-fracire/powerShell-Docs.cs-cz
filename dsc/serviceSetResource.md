---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "ServiceSet prostředek DSC"
ms.openlocfilehash: 2488dda5212ccb717f7fd5d59ad62ec135ad13d5
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="dsc-serviceset-resource"></a><span data-ttu-id="ebb18-103">ServiceSet prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="ebb18-103">DSC ServiceSet Resource</span></span>

> <span data-ttu-id="ebb18-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ebb18-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="ebb18-105">**ServiceSet** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě služeb na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="ebb18-105">The **ServiceSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span> <span data-ttu-id="ebb18-106">Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [služby prostředků](serviceResource.md) u každé služby zadaný v `Name` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="ebb18-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [Service resource](serviceResource.md) for each service specified in the `Name` property.</span></span>

<span data-ttu-id="ebb18-107">Pokud chcete nakonfigurovat několik služeb do stejného stavu, použijte tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="ebb18-107">Use this resource when you want to configure a number of services to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="ebb18-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ebb18-108">Syntax</span></span>

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a><span data-ttu-id="ebb18-109">Properties</span><span class="sxs-lookup"><span data-stu-id="ebb18-109">Properties</span></span>

|  <span data-ttu-id="ebb18-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ebb18-110">Property</span></span>  |  <span data-ttu-id="ebb18-111">Popis</span><span class="sxs-lookup"><span data-stu-id="ebb18-111">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="ebb18-112">Název</span><span class="sxs-lookup"><span data-stu-id="ebb18-112">Name</span></span>| <span data-ttu-id="ebb18-113">Určuje názvy služeb.</span><span class="sxs-lookup"><span data-stu-id="ebb18-113">Indicates the service names.</span></span> <span data-ttu-id="ebb18-114">Všimněte si, že v některých případech je to jiné názvy zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ebb18-114">Note that sometimes this is different from the display names.</span></span> <span data-ttu-id="ebb18-115">Můžete získat seznam služeb a jejich aktuální stav s [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="ebb18-115">You can get a list of the services and their current state with the [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) cmdlet.</span></span>|
| <span data-ttu-id="ebb18-116">StartupType</span><span class="sxs-lookup"><span data-stu-id="ebb18-116">StartupType</span></span>| <span data-ttu-id="ebb18-117">Označuje typ spuštění služby.</span><span class="sxs-lookup"><span data-stu-id="ebb18-117">Indicates the startup type for the service.</span></span> <span data-ttu-id="ebb18-118">Jsou hodnoty, které jsou povoleny pro tuto vlastnost: **automatické**, **zakázané**, a **ruční**</span><span class="sxs-lookup"><span data-stu-id="ebb18-118">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|  
| <span data-ttu-id="ebb18-119">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="ebb18-119">BuiltInAccount</span></span>| <span data-ttu-id="ebb18-120">Určuje účet přihlášení, který chcete použít pro služby.</span><span class="sxs-lookup"><span data-stu-id="ebb18-120">Indicates the sign-in account to use for the services.</span></span> <span data-ttu-id="ebb18-121">Jsou hodnoty, které jsou povoleny pro tuto vlastnost: **LocalService**, **LocalSystem**, a **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="ebb18-121">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>| 
| <span data-ttu-id="ebb18-122">Stav</span><span class="sxs-lookup"><span data-stu-id="ebb18-122">State</span></span>| <span data-ttu-id="ebb18-123">Označuje stav chcete zajistit pro služby: **Zastaveno** nebo **systémem**.</span><span class="sxs-lookup"><span data-stu-id="ebb18-123">Indicates the state you want to ensure for the services: **Stopped** or **Running**.</span></span>| 
| <span data-ttu-id="ebb18-124">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="ebb18-124">Ensure</span></span>| <span data-ttu-id="ebb18-125">Udává, zda existuje služeb v systému.</span><span class="sxs-lookup"><span data-stu-id="ebb18-125">Indicates whether the services exist on the system.</span></span> <span data-ttu-id="ebb18-126">Tuto vlastnost nastavit na **chybí** zajistit, že služby nejsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="ebb18-126">Set this property to **Absent** to ensure that the services do not exist.</span></span> <span data-ttu-id="ebb18-127">Jeho nastavení na hodnotu **přítomen** (výchozí hodnota) zajišťuje, že existují cíl služby.</span><span class="sxs-lookup"><span data-stu-id="ebb18-127">Setting it to **Present** (the default value) ensures that target services exist.</span></span>|
| <span data-ttu-id="ebb18-128">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="ebb18-128">Credential</span></span>| <span data-ttu-id="ebb18-129">Určuje pověření pro účet, který prostředek služby budou spouštěny pod.</span><span class="sxs-lookup"><span data-stu-id="ebb18-129">Indicates credentials for the account that the service resource will run under.</span></span> <span data-ttu-id="ebb18-130">Tato vlastnost a **BuiltinAccount** vlastnost nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="ebb18-130">This property and the **BuiltinAccount** property cannot be used together.</span></span>| 
| <span data-ttu-id="ebb18-131">dependsOn</span><span class="sxs-lookup"><span data-stu-id="ebb18-131">DependsOn</span></span>| <span data-ttu-id="ebb18-132">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="ebb18-132">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="ebb18-133">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba *ResourceName* a její typ je *ResourceType*, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="ebb18-133">For example, if the ID of the resource configuration script block that you want to run first is *ResourceName* and its type is *ResourceType*, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 



## <a name="example"></a><span data-ttu-id="ebb18-134">Příklad</span><span class="sxs-lookup"><span data-stu-id="ebb18-134">Example</span></span>

<span data-ttu-id="ebb18-135">Následující konfigurace spuštění služby "Windows Audio" a "Služby Vzdálená plocha".</span><span class="sxs-lookup"><span data-stu-id="ebb18-135">The following configuration starts the "Windows Audio" and "Remote Desktop Services" services.</span></span>

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```


---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Serviceset DSC
ms.openlocfilehash: 5694c2abc5c0caf0098670b629af464b35125583
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048120"
---
# <a name="dsc-serviceset-resource"></a><span data-ttu-id="0eb81-103">Prostředek Serviceset DSC</span><span class="sxs-lookup"><span data-stu-id="0eb81-103">DSC ServiceSet Resource</span></span>

> <span data-ttu-id="0eb81-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0eb81-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="0eb81-105">**ServiceSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě služeb na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="0eb81-105">The **ServiceSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span> <span data-ttu-id="0eb81-106">Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [služeb resource](serviceResource.md) pro každou službu podle `Name` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="0eb81-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [Service resource](serviceResource.md) for each service specified in the `Name` property.</span></span>

<span data-ttu-id="0eb81-107">Pokud chcete provést konfiguraci celé řady služeb do stejného stavu, použijte tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="0eb81-107">Use this resource when you want to configure a number of services to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="0eb81-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0eb81-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="0eb81-109">Properties</span><span class="sxs-lookup"><span data-stu-id="0eb81-109">Properties</span></span>

|  <span data-ttu-id="0eb81-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0eb81-110">Property</span></span>  |  <span data-ttu-id="0eb81-111">Popis</span><span class="sxs-lookup"><span data-stu-id="0eb81-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="0eb81-112">Name</span><span class="sxs-lookup"><span data-stu-id="0eb81-112">Name</span></span>| <span data-ttu-id="0eb81-113">Určuje názvy služeb.</span><span class="sxs-lookup"><span data-stu-id="0eb81-113">Indicates the service names.</span></span> <span data-ttu-id="0eb81-114">Všimněte si, že někdy se liší od zobrazované názvy.</span><span class="sxs-lookup"><span data-stu-id="0eb81-114">Note that sometimes this is different from the display names.</span></span> <span data-ttu-id="0eb81-115">Můžete získat seznam služeb a jejich aktuální stav s [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0eb81-115">You can get a list of the services and their current state with the [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) cmdlet.</span></span>|
| <span data-ttu-id="0eb81-116">Typ spuštění</span><span class="sxs-lookup"><span data-stu-id="0eb81-116">StartupType</span></span>| <span data-ttu-id="0eb81-117">Určuje typ spouštění služby.</span><span class="sxs-lookup"><span data-stu-id="0eb81-117">Indicates the startup type for the service.</span></span> <span data-ttu-id="0eb81-118">Hodnoty, které jsou pro tuto vlastnost povolena jsou: **Automatické**, **zakázané**, a **ruční**</span><span class="sxs-lookup"><span data-stu-id="0eb81-118">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="0eb81-119">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="0eb81-119">BuiltInAccount</span></span>| <span data-ttu-id="0eb81-120">Určuje přihlašovací účet, který chcete použít pro služby.</span><span class="sxs-lookup"><span data-stu-id="0eb81-120">Indicates the sign-in account to use for the services.</span></span> <span data-ttu-id="0eb81-121">Hodnoty, které jsou pro tuto vlastnost povolena jsou: **LocalService**, **LocalSystem**, a **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="0eb81-121">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="0eb81-122">Stav</span><span class="sxs-lookup"><span data-stu-id="0eb81-122">State</span></span>| <span data-ttu-id="0eb81-123">Označuje stavu, ve kterém chcete zajistit služby: **Zastavit** nebo **systémem**.</span><span class="sxs-lookup"><span data-stu-id="0eb81-123">Indicates the state you want to ensure for the services: **Stopped** or **Running**.</span></span>|
| <span data-ttu-id="0eb81-124">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="0eb81-124">Ensure</span></span>| <span data-ttu-id="0eb81-125">Určuje, zda služby existovat v systému.</span><span class="sxs-lookup"><span data-stu-id="0eb81-125">Indicates whether the services exist on the system.</span></span> <span data-ttu-id="0eb81-126">Tuto vlastnost nastavte na **chybí** zajistit, že služby neexistuje.</span><span class="sxs-lookup"><span data-stu-id="0eb81-126">Set this property to **Absent** to ensure that the services do not exist.</span></span> <span data-ttu-id="0eb81-127">Nastavení na **k dispozici** (výchozí hodnota) zajišťuje, že existují cílové služby.</span><span class="sxs-lookup"><span data-stu-id="0eb81-127">Setting it to **Present** (the default value) ensures that target services exist.</span></span>|
| <span data-ttu-id="0eb81-128">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="0eb81-128">Credential</span></span>| <span data-ttu-id="0eb81-129">Určuje přihlašovací údaje pro účet, pod kterými poběží prostředek služby.</span><span class="sxs-lookup"><span data-stu-id="0eb81-129">Indicates credentials for the account that the service resource will run under.</span></span> <span data-ttu-id="0eb81-130">Tato vlastnost a **BuiltinAccount** vlastnost nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="0eb81-130">This property and the **BuiltinAccount** property cannot be used together.</span></span>|
| <span data-ttu-id="0eb81-131">DependsOn</span><span class="sxs-lookup"><span data-stu-id="0eb81-131">DependsOn</span></span>| <span data-ttu-id="0eb81-132">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="0eb81-132">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="0eb81-133">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba *ResourceName* a jejím typem je *ResourceType*, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="0eb81-133">For example, if the ID of the resource configuration script block that you want to run first is *ResourceName* and its type is *ResourceType*, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|



## <a name="example"></a><span data-ttu-id="0eb81-134">Příklad</span><span class="sxs-lookup"><span data-stu-id="0eb81-134">Example</span></span>

<span data-ttu-id="0eb81-135">Následující konfigurace spuštění služby "Windows zvuku" a "Služby Vzdálená plocha".</span><span class="sxs-lookup"><span data-stu-id="0eb81-135">The following configuration starts the "Windows Audio" and "Remote Desktop Services" services.</span></span>

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

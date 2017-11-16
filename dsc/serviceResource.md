---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC služby"
ms.openlocfilehash: 611729e5d971ebaf15ac947454cffadc6797927b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-service-resource"></a><span data-ttu-id="fb63a-103">Prostředek DSC služby</span><span class="sxs-lookup"><span data-stu-id="fb63a-103">DSC Service Resource</span></span>

> <span data-ttu-id="fb63a-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="fb63a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="fb63a-105">**Služby** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě služeb na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="fb63a-105">The **Service** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="fb63a-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="fb63a-106">Syntax</span></span>

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="fb63a-107">Properties</span><span class="sxs-lookup"><span data-stu-id="fb63a-107">Properties</span></span>

|  <span data-ttu-id="fb63a-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fb63a-108">Property</span></span>  |  <span data-ttu-id="fb63a-109">Popis</span><span class="sxs-lookup"><span data-stu-id="fb63a-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="fb63a-110">Název</span><span class="sxs-lookup"><span data-stu-id="fb63a-110">Name</span></span>| <span data-ttu-id="fb63a-111">Určuje název služby.</span><span class="sxs-lookup"><span data-stu-id="fb63a-111">Indicates the service name.</span></span> <span data-ttu-id="fb63a-112">Všimněte si, že v některých případech se to neliší od zobrazovaný název.</span><span class="sxs-lookup"><span data-stu-id="fb63a-112">Note that sometimes this is different from the display name.</span></span> <span data-ttu-id="fb63a-113">Můžete získat seznam služeb a jejich aktuálního stavu pomocí rutiny Get-Service.</span><span class="sxs-lookup"><span data-stu-id="fb63a-113">You can get a list of the services and their current state with the Get-Service cmdlet.</span></span>| 
| <span data-ttu-id="fb63a-114">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="fb63a-114">BuiltInAccount</span></span>| <span data-ttu-id="fb63a-115">Určuje účet přihlášení, který chcete použít pro službu.</span><span class="sxs-lookup"><span data-stu-id="fb63a-115">Indicates the sign-in account to use for the service.</span></span> <span data-ttu-id="fb63a-116">Jsou hodnoty, které jsou povoleny pro tuto vlastnost: **LocalService**, **LocalSystem**, a **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="fb63a-116">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>| 
| <span data-ttu-id="fb63a-117">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="fb63a-117">Credential</span></span>| <span data-ttu-id="fb63a-118">Určuje pověření pro účet, který služba bude spuštěna pod.</span><span class="sxs-lookup"><span data-stu-id="fb63a-118">Indicates credentials for the account that the service will run under.</span></span> <span data-ttu-id="fb63a-119">Tato vlastnost a __BuiltinAccount__ vlastnost nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="fb63a-119">This property and the __BuiltinAccount__ property cannot be used together.</span></span>| 
| <span data-ttu-id="fb63a-120">dependsOn</span><span class="sxs-lookup"><span data-stu-id="fb63a-120">DependsOn</span></span>| <span data-ttu-id="fb63a-121">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="fb63a-121">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="fb63a-122">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="fb63a-122">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="fb63a-123">StartupType</span><span class="sxs-lookup"><span data-stu-id="fb63a-123">StartupType</span></span>| <span data-ttu-id="fb63a-124">Označuje typ spuštění služby.</span><span class="sxs-lookup"><span data-stu-id="fb63a-124">Indicates the startup type for the service.</span></span> <span data-ttu-id="fb63a-125">Jsou hodnoty, které jsou povoleny pro tuto vlastnost: **automatické**, **zakázané**, a **ruční**</span><span class="sxs-lookup"><span data-stu-id="fb63a-125">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>| 
| <span data-ttu-id="fb63a-126">Stav</span><span class="sxs-lookup"><span data-stu-id="fb63a-126">State</span></span>| <span data-ttu-id="fb63a-127">Označuje stav, který chcete pro službu zajistit.</span><span class="sxs-lookup"><span data-stu-id="fb63a-127">Indicates the state you want to ensure for the service.</span></span>| 
| <span data-ttu-id="fb63a-128">Popis</span><span class="sxs-lookup"><span data-stu-id="fb63a-128">Description</span></span> | <span data-ttu-id="fb63a-129">Určuje popis cílovou službu.</span><span class="sxs-lookup"><span data-stu-id="fb63a-129">Indicates the description of the target service.</span></span>| 
| <span data-ttu-id="fb63a-130">DisplayName</span><span class="sxs-lookup"><span data-stu-id="fb63a-130">DisplayName</span></span> | <span data-ttu-id="fb63a-131">Určuje zobrazovaný název cílové služby.</span><span class="sxs-lookup"><span data-stu-id="fb63a-131">Indicates the display name of the target service.</span></span>| 
| <span data-ttu-id="fb63a-132">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="fb63a-132">Ensure</span></span> | <span data-ttu-id="fb63a-133">Určuje, zda cílová služba existuje v systému.</span><span class="sxs-lookup"><span data-stu-id="fb63a-133">Indicates whether the target service exists on the system.</span></span> <span data-ttu-id="fb63a-134">Tuto vlastnost nastavit na **chybí** zajistit, že cílová služba neexistuje.</span><span class="sxs-lookup"><span data-stu-id="fb63a-134">Set this property to **Absent** to ensure that the target service does not exist.</span></span> <span data-ttu-id="fb63a-135">Jeho nastavení na hodnotu **přítomen** (výchozí hodnota) zajišťuje, že cílová služba existuje.</span><span class="sxs-lookup"><span data-stu-id="fb63a-135">Setting it to **Present** (the default value) ensures that target service exists.</span></span>|
| <span data-ttu-id="fb63a-136">Cesta</span><span class="sxs-lookup"><span data-stu-id="fb63a-136">Path</span></span> | <span data-ttu-id="fb63a-137">Určuje cestu k binárnímu souboru pro novou službu.</span><span class="sxs-lookup"><span data-stu-id="fb63a-137">Indicates the path to the binary file for a new service.</span></span>| 

## <a name="example"></a><span data-ttu-id="fb63a-138">Příklad</span><span class="sxs-lookup"><span data-stu-id="fb63a-138">Example</span></span>

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```


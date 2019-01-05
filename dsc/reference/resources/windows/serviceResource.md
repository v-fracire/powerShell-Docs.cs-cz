---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC služby
ms.openlocfilehash: 09571bd0eaa428e7d0bb7a533d6ad1c0c936e2cf
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048115"
---
# <a name="dsc-service-resource"></a><span data-ttu-id="7c259-103">Prostředek DSC služby</span><span class="sxs-lookup"><span data-stu-id="7c259-103">DSC Service Resource</span></span>

> <span data-ttu-id="7c259-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7c259-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="7c259-105">**Služby** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě služeb na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="7c259-105">The **Service** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="7c259-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="7c259-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="7c259-107">Properties</span><span class="sxs-lookup"><span data-stu-id="7c259-107">Properties</span></span>

|  <span data-ttu-id="7c259-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="7c259-108">Property</span></span>  |  <span data-ttu-id="7c259-109">Popis</span><span class="sxs-lookup"><span data-stu-id="7c259-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="7c259-110">Name</span><span class="sxs-lookup"><span data-stu-id="7c259-110">Name</span></span>| <span data-ttu-id="7c259-111">Určuje název služby.</span><span class="sxs-lookup"><span data-stu-id="7c259-111">Indicates the service name.</span></span> <span data-ttu-id="7c259-112">Všimněte si, že někdy se liší od zobrazovaný název.</span><span class="sxs-lookup"><span data-stu-id="7c259-112">Note that sometimes this is different from the display name.</span></span> <span data-ttu-id="7c259-113">Můžete získat seznam služeb a jejich aktuální stav pomocí rutiny Get-Service.</span><span class="sxs-lookup"><span data-stu-id="7c259-113">You can get a list of the services and their current state with the Get-Service cmdlet.</span></span>|
| <span data-ttu-id="7c259-114">BuiltInAccount</span><span class="sxs-lookup"><span data-stu-id="7c259-114">BuiltInAccount</span></span>| <span data-ttu-id="7c259-115">Určuje přihlašovací účet, který chcete použít pro službu.</span><span class="sxs-lookup"><span data-stu-id="7c259-115">Indicates the sign-in account to use for the service.</span></span> <span data-ttu-id="7c259-116">Hodnoty, které jsou pro tuto vlastnost povolena jsou: **LocalService**, **LocalSystem**, a **NetworkService**.</span><span class="sxs-lookup"><span data-stu-id="7c259-116">The values that are allowed for this property are: **LocalService**, **LocalSystem**, and **NetworkService**.</span></span>|
| <span data-ttu-id="7c259-117">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="7c259-117">Credential</span></span>| <span data-ttu-id="7c259-118">Určuje přihlašovací údaje pro účet, který bude tato služba spuštěna pod.</span><span class="sxs-lookup"><span data-stu-id="7c259-118">Indicates credentials for the account that the service will run under.</span></span> <span data-ttu-id="7c259-119">Tato vlastnost a __BuiltinAccount__ vlastnost nelze použít společně.</span><span class="sxs-lookup"><span data-stu-id="7c259-119">This property and the __BuiltinAccount__ property cannot be used together.</span></span>|
| <span data-ttu-id="7c259-120">DependsOn</span><span class="sxs-lookup"><span data-stu-id="7c259-120">DependsOn</span></span>| <span data-ttu-id="7c259-121">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="7c259-121">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7c259-122">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="7c259-122">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="7c259-123">Typ spuštění</span><span class="sxs-lookup"><span data-stu-id="7c259-123">StartupType</span></span>| <span data-ttu-id="7c259-124">Určuje typ spouštění služby.</span><span class="sxs-lookup"><span data-stu-id="7c259-124">Indicates the startup type for the service.</span></span> <span data-ttu-id="7c259-125">Hodnoty, které jsou pro tuto vlastnost povolena jsou: **Automatické**, **zakázané**, a **ruční**</span><span class="sxs-lookup"><span data-stu-id="7c259-125">The values that are allowed for this property are: **Automatic**, **Disabled**, and **Manual**</span></span>|
| <span data-ttu-id="7c259-126">Stav</span><span class="sxs-lookup"><span data-stu-id="7c259-126">State</span></span>| <span data-ttu-id="7c259-127">Označuje stavu, ve kterém chcete zajistit pro službu.</span><span class="sxs-lookup"><span data-stu-id="7c259-127">Indicates the state you want to ensure for the service.</span></span>|
| <span data-ttu-id="7c259-128">Popis</span><span class="sxs-lookup"><span data-stu-id="7c259-128">Description</span></span> | <span data-ttu-id="7c259-129">Určuje popis cílové služby.</span><span class="sxs-lookup"><span data-stu-id="7c259-129">Indicates the description of the target service.</span></span>|
| <span data-ttu-id="7c259-130">DisplayName</span><span class="sxs-lookup"><span data-stu-id="7c259-130">DisplayName</span></span> | <span data-ttu-id="7c259-131">Určuje zobrazovaný název cílové služby.</span><span class="sxs-lookup"><span data-stu-id="7c259-131">Indicates the display name of the target service.</span></span>|
| <span data-ttu-id="7c259-132">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="7c259-132">Ensure</span></span> | <span data-ttu-id="7c259-133">Určuje, zda cílová služba existuje v systému.</span><span class="sxs-lookup"><span data-stu-id="7c259-133">Indicates whether the target service exists on the system.</span></span> <span data-ttu-id="7c259-134">Tuto vlastnost nastavte na **chybí** zajistit, že cílová služba neexistuje.</span><span class="sxs-lookup"><span data-stu-id="7c259-134">Set this property to **Absent** to ensure that the target service does not exist.</span></span> <span data-ttu-id="7c259-135">Nastavení na **k dispozici** (výchozí hodnota) zajišťuje, že cílová služba existuje.</span><span class="sxs-lookup"><span data-stu-id="7c259-135">Setting it to **Present** (the default value) ensures that target service exists.</span></span>|
| <span data-ttu-id="7c259-136">Cesta</span><span class="sxs-lookup"><span data-stu-id="7c259-136">Path</span></span> | <span data-ttu-id="7c259-137">Určuje cestu k binárnímu souboru pro novou službu.</span><span class="sxs-lookup"><span data-stu-id="7c259-137">Indicates the path to the binary file for a new service.</span></span>|

## <a name="example"></a><span data-ttu-id="7c259-138">Příklad</span><span class="sxs-lookup"><span data-stu-id="7c259-138">Example</span></span>

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
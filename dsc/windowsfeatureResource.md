---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC WindowsFeature"
ms.openlocfilehash: b4f50cb9ee172600b1811175e9cf67f6a7ed2d55
ms.sourcegitcommit: cd5a1f054cbf9eb95c5242a995f9741e031ddb24
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2017
---
# <a name="dsc-windowsfeature-resource"></a><span data-ttu-id="b672f-103">Prostředek DSC WindowsFeature</span><span class="sxs-lookup"><span data-stu-id="b672f-103">DSC WindowsFeature Resource</span></span>

> <span data-ttu-id="b672f-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b672f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b672f-105">**WindowsFeature** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že role a funkce se přidají nebo odeberou na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="b672f-105">The **WindowsFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="b672f-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b672f-106">Syntax</span></span>

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="b672f-107">Properties</span><span class="sxs-lookup"><span data-stu-id="b672f-107">Properties</span></span>

|  <span data-ttu-id="b672f-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="b672f-108">Property</span></span>  |  <span data-ttu-id="b672f-109">Popis</span><span class="sxs-lookup"><span data-stu-id="b672f-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="b672f-110">Název</span><span class="sxs-lookup"><span data-stu-id="b672f-110">Name</span></span>| <span data-ttu-id="b672f-111">Určuje název role nebo funkce, které chcete zajistit přidat nebo odebrat.</span><span class="sxs-lookup"><span data-stu-id="b672f-111">Indicates the name of the role or feature that you want to ensure is added or removed.</span></span> <span data-ttu-id="b672f-112">Je to stejné jako __název__ vlastnost z [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) rutiny a nikoli zobrazovaný název role nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="b672f-112">This is the same as the __Name__ property from the [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) cmdlet, and not the display name of the role or feature.</span></span>| 
| <span data-ttu-id="b672f-113">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="b672f-113">Credential</span></span>| <span data-ttu-id="b672f-114">Určuje pověření, které můžete přidat nebo odebrat roli nebo funkci.</span><span class="sxs-lookup"><span data-stu-id="b672f-114">Indicates the credentials to use to add or remove the role or feature.</span></span>| 
| <span data-ttu-id="b672f-115">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="b672f-115">Ensure</span></span>| <span data-ttu-id="b672f-116">Označuje, pokud je přidána role nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="b672f-116">Indicates if the role or feature is added.</span></span> <span data-ttu-id="b672f-117">K zajištění, že je role nebo funkce přidané, nastavte tuto vlastnost "Přítomen" se ujistěte, že je odebrán roli nebo funkci, nastavte vlastnost na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="b672f-117">To ensure that the role or feature is added, set this property to "Present" To ensure that the role or feature is removed, set the property to "Absent".</span></span>| 
| <span data-ttu-id="b672f-118">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="b672f-118">IncludeAllSubFeature</span></span>| <span data-ttu-id="b672f-119">Tuto vlastnost nastavit na __$true__ zajistit stav všechny požadované položky se stavem funkci zadáte pomocí __název__ vlastnost.</span><span class="sxs-lookup"><span data-stu-id="b672f-119">Set this property to __$true__ to ensure the state of all required subfeatures with the state of the feature you specify with the __Name__ property.</span></span>| 
| <span data-ttu-id="b672f-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="b672f-120">LogPath</span></span>| <span data-ttu-id="b672f-121">Určuje cestu k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.</span><span class="sxs-lookup"><span data-stu-id="b672f-121">Indicates the path to a log file where you want the resource provider to log the operation.</span></span>| 
| <span data-ttu-id="b672f-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="b672f-122">DependsOn</span></span>| <span data-ttu-id="b672f-123">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="b672f-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="b672f-124">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="b672f-124">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="b672f-125">Zdroj</span><span class="sxs-lookup"><span data-stu-id="b672f-125">Source</span></span>| <span data-ttu-id="b672f-126">Určuje umístění zdrojového souboru pro instalaci, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="b672f-126">Indicates the location of the source file to use for installation, if necessary.</span></span>| 

## <a name="example"></a><span data-ttu-id="b672f-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="b672f-127">Example</span></span>
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present" 
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature  
}
```


---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek WindowsFeature DSC
ms.openlocfilehash: 7a57f4b2797ab3bb202aea8b2543d1e3f14074e9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048153"
---
# <a name="dsc-windowsfeature-resource"></a><span data-ttu-id="250bc-103">Prostředek WindowsFeature DSC</span><span class="sxs-lookup"><span data-stu-id="250bc-103">DSC WindowsFeature Resource</span></span>

> <span data-ttu-id="250bc-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="250bc-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="250bc-105">**WindowsFeature** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že role a funkce přidávají a odebírají na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="250bc-105">The **WindowsFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="250bc-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="250bc-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="250bc-107">Properties</span><span class="sxs-lookup"><span data-stu-id="250bc-107">Properties</span></span>

|  <span data-ttu-id="250bc-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="250bc-108">Property</span></span>  |  <span data-ttu-id="250bc-109">Popis</span><span class="sxs-lookup"><span data-stu-id="250bc-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="250bc-110">Name</span><span class="sxs-lookup"><span data-stu-id="250bc-110">Name</span></span>| <span data-ttu-id="250bc-111">Určuje název role nebo funkce, které chcete zajistit přidá nebo odebere.</span><span class="sxs-lookup"><span data-stu-id="250bc-111">Indicates the name of the role or feature that you want to ensure is added or removed.</span></span> <span data-ttu-id="250bc-112">To je stejný jako __název__ vlastnost z [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) rutiny a nikoli zobrazovaný název role nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="250bc-112">This is the same as the __Name__ property from the [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) cmdlet, and not the display name of the role or feature.</span></span>|
| <span data-ttu-id="250bc-113">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="250bc-113">Credential</span></span>| <span data-ttu-id="250bc-114">Určuje pověření, které slouží k přidání nebo odebrání role nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="250bc-114">Indicates the credentials to use to add or remove the role or feature.</span></span>|
| <span data-ttu-id="250bc-115">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="250bc-115">Ensure</span></span>| <span data-ttu-id="250bc-116">Označuje, pokud je přidána role nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="250bc-116">Indicates if the role or feature is added.</span></span> <span data-ttu-id="250bc-117">K zajištění, že role nebo funkce je přidána, nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že se odebere roli nebo funkci, nastavte vlastnost na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="250bc-117">To ensure that the role or feature is added, set this property to "Present" To ensure that the role or feature is removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="250bc-118">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="250bc-118">IncludeAllSubFeature</span></span>| <span data-ttu-id="250bc-119">Tuto vlastnost nastavte na __$true__ zajistit stav všech požadovaných tyto položky se stavem funkci zadáte __název__ vlastnost.</span><span class="sxs-lookup"><span data-stu-id="250bc-119">Set this property to __$true__ to ensure the state of all required subfeatures with the state of the feature you specify with the __Name__ property.</span></span>|
| <span data-ttu-id="250bc-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="250bc-120">LogPath</span></span>| <span data-ttu-id="250bc-121">Určuje cestu k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.</span><span class="sxs-lookup"><span data-stu-id="250bc-121">Indicates the path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="250bc-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="250bc-122">DependsOn</span></span>| <span data-ttu-id="250bc-123">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="250bc-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="250bc-124">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="250bc-124">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="250bc-125">Zdroj</span><span class="sxs-lookup"><span data-stu-id="250bc-125">Source</span></span>| <span data-ttu-id="250bc-126">Určuje umístění zdrojového souboru pro použití pro instalaci, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="250bc-126">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="250bc-127">Příklad</span><span class="sxs-lookup"><span data-stu-id="250bc-127">Example</span></span>
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present"
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature
}
```
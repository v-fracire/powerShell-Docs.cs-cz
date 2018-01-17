---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "WindowsOptionalFeatureSet prostředek DSC"
ms.openlocfilehash: 6912e5cf92f23058342bc566bd66dc4be3357a30
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a><span data-ttu-id="54711-103">WindowsOptionalFeatureSet prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="54711-103">DSC WindowsOptionalFeatureSet Resource</span></span>

> <span data-ttu-id="54711-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="54711-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="54711-105">**WindowsOptionalFeatureSet** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že jsou na cílový uzel povolené volitelné funkce.</span><span class="sxs-lookup"><span data-stu-id="54711-105">The **WindowsOptionalFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span> <span data-ttu-id="54711-106">Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [WindowsOptionalFeature prostředků](windowsOptionalFeatureResource.md) pro každou funkci zadaný v `Name` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="54711-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsOptionalFeature resource](windowsOptionalFeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="54711-107">Pokud chcete nakonfigurovat počet volitelné funkce systému Windows do stejného stavu, použijte tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="54711-107">Use this resource when you want to configure a number of Windows optional features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="54711-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="54711-108">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ] 
    [ RemoveFilesOnDisable = [bool] ]  
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a><span data-ttu-id="54711-109">Properties</span><span class="sxs-lookup"><span data-stu-id="54711-109">Properties</span></span>

|  <span data-ttu-id="54711-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="54711-110">Property</span></span>  |  <span data-ttu-id="54711-111">Popis</span><span class="sxs-lookup"><span data-stu-id="54711-111">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="54711-112">Název</span><span class="sxs-lookup"><span data-stu-id="54711-112">Name</span></span>| <span data-ttu-id="54711-113">Určuje název funkce, které chcete zajistit jsou zapnutá nebo vypnutá.</span><span class="sxs-lookup"><span data-stu-id="54711-113">Indicates the name of the features that you want to ensure are enabled or disabled.</span></span>| 
| <span data-ttu-id="54711-114">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="54711-114">Ensure</span></span>| <span data-ttu-id="54711-115">Určuje, jestli jsou povolené funkce.</span><span class="sxs-lookup"><span data-stu-id="54711-115">Specifies whether the features are enabled.</span></span> <span data-ttu-id="54711-116">K zajištění, že funkce jsou povolené, nastavte tuto vlastnost možnost povolit"k zajištění, že jsou zakázány funkce, nastavte vlastnost na"Zakázat".</span><span class="sxs-lookup"><span data-stu-id="54711-116">To ensure that the features are enabled, set this property to "Enable" To ensure that the features are disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="54711-117">Zdroj</span><span class="sxs-lookup"><span data-stu-id="54711-117">Source</span></span>| <span data-ttu-id="54711-118">Není implementováno.</span><span class="sxs-lookup"><span data-stu-id="54711-118">Not implemented.</span></span>|
| <span data-ttu-id="54711-119">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="54711-119">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="54711-120">Určuje, zda DISM kontaktuje Windows Update (WU) při vyhledávání pro zdrojové soubory k povolení funkce.</span><span class="sxs-lookup"><span data-stu-id="54711-120">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable features.</span></span> <span data-ttu-id="54711-121">Pokud $true, DISM nebude kontaktovat služby WU.</span><span class="sxs-lookup"><span data-stu-id="54711-121">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="54711-122">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="54711-122">RemoveFilesOnDisable</span></span>| <span data-ttu-id="54711-123">Nastavte na **$true** odebrat všechny soubory spojené s funkcí, když jsou zakázány (to znamená, když **zajistěte, aby** je nastaven na "Chybí").</span><span class="sxs-lookup"><span data-stu-id="54711-123">Set to **$true** to remove all files associated with the features when they are disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="54711-124">ÚroveňProtokolu</span><span class="sxs-lookup"><span data-stu-id="54711-124">LogLevel</span></span>| <span data-ttu-id="54711-125">Maximální úroveň výstupu zobrazeného v protokolech.</span><span class="sxs-lookup"><span data-stu-id="54711-125">The maximum output level shown in the logs.</span></span> <span data-ttu-id="54711-126">Možné hodnoty jsou: "ErrorsOnly" (jsou protokolovány pouze chyby), "ErrorsAndWarning" (chyby a upozornění přihlášení) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění přihlášeni).</span><span class="sxs-lookup"><span data-stu-id="54711-126">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="54711-127">LogPath</span><span class="sxs-lookup"><span data-stu-id="54711-127">LogPath</span></span>| <span data-ttu-id="54711-128">Cesta k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.</span><span class="sxs-lookup"><span data-stu-id="54711-128">The path to a log file where you want the resource provider to log the operation.</span></span>| 
| <span data-ttu-id="54711-129">dependsOn</span><span class="sxs-lookup"><span data-stu-id="54711-129">DependsOn</span></span>| <span data-ttu-id="54711-130">Určuje, že konfigurace jiný prostředek musí spustit předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="54711-130">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="54711-131">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="54711-131">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
 




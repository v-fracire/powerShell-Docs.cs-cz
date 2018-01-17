---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC WindowsOptionalFeature"
ms.openlocfilehash: d9b8cc316255f06d2de71fedc47ce4472cc8b382
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-windowsoptionalfeature-resource"></a><span data-ttu-id="a46ac-103">Prostředek DSC WindowsOptionalFeature</span><span class="sxs-lookup"><span data-stu-id="a46ac-103">DSC WindowsOptionalFeature Resource</span></span>

> <span data-ttu-id="a46ac-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a46ac-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="a46ac-105">**WindowsOptionalFeature** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že jsou na cílový uzel povolené volitelné funkce.</span><span class="sxs-lookup"><span data-stu-id="a46ac-105">The **WindowsOptionalFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="a46ac-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a46ac-106">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a><span data-ttu-id="a46ac-107">Properties</span><span class="sxs-lookup"><span data-stu-id="a46ac-107">Properties</span></span>

|  <span data-ttu-id="a46ac-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a46ac-108">Property</span></span>  |  <span data-ttu-id="a46ac-109">Popis</span><span class="sxs-lookup"><span data-stu-id="a46ac-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="a46ac-110">Název</span><span class="sxs-lookup"><span data-stu-id="a46ac-110">Name</span></span>| <span data-ttu-id="a46ac-111">Určuje název funkce, které chcete zajistit povolený nebo zakázaný.</span><span class="sxs-lookup"><span data-stu-id="a46ac-111">Indicates the name of the feature that you want to ensure is enabled or disabled.</span></span>| 
| <span data-ttu-id="a46ac-112">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="a46ac-112">Ensure</span></span>| <span data-ttu-id="a46ac-113">Určuje, zda je povolena funkce.</span><span class="sxs-lookup"><span data-stu-id="a46ac-113">Specifies whether the feature is enabled.</span></span> <span data-ttu-id="a46ac-114">K zajištění, že tato funkce je povoleno, nastavte tuto vlastnost možnost povolit"k zajištění, že tato funkce je zakázaná, nastavte vlastnost na"Zakázat".</span><span class="sxs-lookup"><span data-stu-id="a46ac-114">To ensure that the feature is enabled, set this property to "Enable" To ensure that the feature is disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="a46ac-115">Zdroj</span><span class="sxs-lookup"><span data-stu-id="a46ac-115">Source</span></span>| <span data-ttu-id="a46ac-116">Není implementováno.</span><span class="sxs-lookup"><span data-stu-id="a46ac-116">Not implemented.</span></span>|
| <span data-ttu-id="a46ac-117">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="a46ac-117">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="a46ac-118">Určuje, zda DISM kontaktuje Windows Update (WU) při vyhledávání pro zdrojové soubory pro povolení funkce.</span><span class="sxs-lookup"><span data-stu-id="a46ac-118">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable a feature.</span></span> <span data-ttu-id="a46ac-119">Pokud $true, DISM nebude kontaktovat služby WU.</span><span class="sxs-lookup"><span data-stu-id="a46ac-119">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="a46ac-120">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="a46ac-120">RemoveFilesOnDisable</span></span>| <span data-ttu-id="a46ac-121">Nastavte na **$true** odebere všechny soubory přidružené k této funkci, pokud je zakázán (to znamená, když **zajistěte, aby** je nastaven na "Chybí").</span><span class="sxs-lookup"><span data-stu-id="a46ac-121">Set to **$true** to remove all files associated with the feature when it is disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="a46ac-122">ÚroveňProtokolu</span><span class="sxs-lookup"><span data-stu-id="a46ac-122">LogLevel</span></span>| <span data-ttu-id="a46ac-123">Maximální úroveň výstupu zobrazeného v protokolech.</span><span class="sxs-lookup"><span data-stu-id="a46ac-123">The maximum output level shown in the logs.</span></span> <span data-ttu-id="a46ac-124">Možné hodnoty jsou: "ErrorsOnly" (jsou protokolovány pouze chyby), "ErrorsAndWarning" (chyby a upozornění přihlášení) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění přihlášeni).</span><span class="sxs-lookup"><span data-stu-id="a46ac-124">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="a46ac-125">LogPath</span><span class="sxs-lookup"><span data-stu-id="a46ac-125">LogPath</span></span>| <span data-ttu-id="a46ac-126">Cesta k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.</span><span class="sxs-lookup"><span data-stu-id="a46ac-126">The path to a log file where you want the resource provider to log the operation.</span></span>| 
| <span data-ttu-id="a46ac-127">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a46ac-127">DependsOn</span></span>| <span data-ttu-id="a46ac-128">Určuje, že konfigurace jiný prostředek musí spustit předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="a46ac-128">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a46ac-129">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a46ac-129">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
 




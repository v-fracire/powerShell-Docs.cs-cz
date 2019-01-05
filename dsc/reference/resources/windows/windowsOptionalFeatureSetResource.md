---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowsoptionalfeatureset DSC
ms.openlocfilehash: c27d026e01bbb443a82112e37f1d199fb3482e49
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048133"
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a><span data-ttu-id="ab372-103">Prostředek Windowsoptionalfeatureset DSC</span><span class="sxs-lookup"><span data-stu-id="ab372-103">DSC WindowsOptionalFeatureSet Resource</span></span>

> <span data-ttu-id="ab372-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ab372-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="ab372-105">**WindowsOptionalFeatureSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že na cílový uzel je povolené volitelné funkce.</span><span class="sxs-lookup"><span data-stu-id="ab372-105">The **WindowsOptionalFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>
<span data-ttu-id="ab372-106">Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [prostředek WindowsOptionalFeature](windowsOptionalFeatureResource.md) pro každou součást podle `Name` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="ab372-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [WindowsOptionalFeature resource](windowsOptionalFeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="ab372-107">Pokud chcete nakonfigurovat několik volitelných funkcí Windows do stejného stavu, použijte tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="ab372-107">Use this resource when you want to configure a number of Windows optional features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="ab372-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ab372-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="ab372-109">Properties</span><span class="sxs-lookup"><span data-stu-id="ab372-109">Properties</span></span>

|  <span data-ttu-id="ab372-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ab372-110">Property</span></span>  |  <span data-ttu-id="ab372-111">Popis</span><span class="sxs-lookup"><span data-stu-id="ab372-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="ab372-112">Name</span><span class="sxs-lookup"><span data-stu-id="ab372-112">Name</span></span>| <span data-ttu-id="ab372-113">Určuje název funkce, které chcete zajistit jsou zapnutá nebo vypnutá.</span><span class="sxs-lookup"><span data-stu-id="ab372-113">Indicates the name of the features that you want to ensure are enabled or disabled.</span></span>|
| <span data-ttu-id="ab372-114">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="ab372-114">Ensure</span></span>| <span data-ttu-id="ab372-115">Určuje, zda jsou povoleny funkce.</span><span class="sxs-lookup"><span data-stu-id="ab372-115">Specifies whether the features are enabled.</span></span> <span data-ttu-id="ab372-116">K zajištění, že funkce jsou povolené, nastavte tuto vlastnost na "Zapnout" Ujistěte se, že funkce je zakázáno, nastavte vlastnost na "Zakázat".</span><span class="sxs-lookup"><span data-stu-id="ab372-116">To ensure that the features are enabled, set this property to "Enable" To ensure that the features are disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="ab372-117">Zdroj</span><span class="sxs-lookup"><span data-stu-id="ab372-117">Source</span></span>| <span data-ttu-id="ab372-118">Není implementováno.</span><span class="sxs-lookup"><span data-stu-id="ab372-118">Not implemented.</span></span>|
| <span data-ttu-id="ab372-119">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="ab372-119">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="ab372-120">Určuje, zda DISM kontaktuje Windows Update (WU) při hledání pro zdrojové soubory k povolení funkcí.</span><span class="sxs-lookup"><span data-stu-id="ab372-120">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable features.</span></span> <span data-ttu-id="ab372-121">Pokud $true, DISM nekontaktuje WU.</span><span class="sxs-lookup"><span data-stu-id="ab372-121">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="ab372-122">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="ab372-122">RemoveFilesOnDisable</span></span>| <span data-ttu-id="ab372-123">Nastavte na **$true** odebrat všechny soubory spojené s funkcemi, když jsou zakázány (to znamená, když **Ujistěte se, že** je nastavena na "Chybí").</span><span class="sxs-lookup"><span data-stu-id="ab372-123">Set to **$true** to remove all files associated with the features when they are disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="ab372-124">ÚroveňProtokolu</span><span class="sxs-lookup"><span data-stu-id="ab372-124">LogLevel</span></span>| <span data-ttu-id="ab372-125">Maximální úroveň výstupu zobrazeného v protokolech.</span><span class="sxs-lookup"><span data-stu-id="ab372-125">The maximum output level shown in the logs.</span></span> <span data-ttu-id="ab372-126">Přípustné hodnoty jsou: "ErrorsOnly" (pouze chyby se protokolují), "ErrorsAndWarning" (chyby a upozornění se protokolují) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění jsou protokolovány).</span><span class="sxs-lookup"><span data-stu-id="ab372-126">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="ab372-127">LogPath</span><span class="sxs-lookup"><span data-stu-id="ab372-127">LogPath</span></span>| <span data-ttu-id="ab372-128">Cesta k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.</span><span class="sxs-lookup"><span data-stu-id="ab372-128">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="ab372-129">DependsOn</span><span class="sxs-lookup"><span data-stu-id="ab372-129">DependsOn</span></span>| <span data-ttu-id="ab372-130">Určuje, že konfigurace jiný prostředek musí spustit před konfigurací tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="ab372-130">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="ab372-131">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="ab372-131">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

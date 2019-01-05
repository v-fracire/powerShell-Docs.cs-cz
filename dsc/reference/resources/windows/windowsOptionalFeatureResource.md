---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek WindowsOptionalFeature DSC
ms.openlocfilehash: 390caefd2ad190afc651b22ed1beb5cf1d604527
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048147"
---
# <a name="dsc-windowsoptionalfeature-resource"></a><span data-ttu-id="d7148-103">Prostředek WindowsOptionalFeature DSC</span><span class="sxs-lookup"><span data-stu-id="d7148-103">DSC WindowsOptionalFeature Resource</span></span>

> <span data-ttu-id="d7148-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d7148-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="d7148-105">**WindowsOptionalFeature** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že na cílový uzel je povolené volitelné funkce.</span><span class="sxs-lookup"><span data-stu-id="d7148-105">The **WindowsOptionalFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="d7148-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="d7148-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="d7148-107">Properties</span><span class="sxs-lookup"><span data-stu-id="d7148-107">Properties</span></span>

|  <span data-ttu-id="d7148-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="d7148-108">Property</span></span>  |  <span data-ttu-id="d7148-109">Popis</span><span class="sxs-lookup"><span data-stu-id="d7148-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="d7148-110">Name</span><span class="sxs-lookup"><span data-stu-id="d7148-110">Name</span></span>| <span data-ttu-id="d7148-111">Určuje název funkce, která budete muset zajistit, aby povolený nebo zakázaný.</span><span class="sxs-lookup"><span data-stu-id="d7148-111">Indicates the name of the feature that you want to ensure is enabled or disabled.</span></span>|
| <span data-ttu-id="d7148-112">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="d7148-112">Ensure</span></span>| <span data-ttu-id="d7148-113">Určuje, zda je povolena funkce.</span><span class="sxs-lookup"><span data-stu-id="d7148-113">Specifies whether the feature is enabled.</span></span> <span data-ttu-id="d7148-114">K zajištění, že funkce je povolená, nastavte tuto vlastnost na "Zapnout" Ujistěte se, že je zakázaná, nastavte vlastnost na "Zakázat".</span><span class="sxs-lookup"><span data-stu-id="d7148-114">To ensure that the feature is enabled, set this property to "Enable" To ensure that the feature is disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="d7148-115">Zdroj</span><span class="sxs-lookup"><span data-stu-id="d7148-115">Source</span></span>| <span data-ttu-id="d7148-116">Není implementováno.</span><span class="sxs-lookup"><span data-stu-id="d7148-116">Not implemented.</span></span>|
| <span data-ttu-id="d7148-117">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="d7148-117">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="d7148-118">Určuje, zda DISM kontaktuje Windows Update (WU) při hledání pro zdrojové soubory pro povolení funkce.</span><span class="sxs-lookup"><span data-stu-id="d7148-118">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable a feature.</span></span> <span data-ttu-id="d7148-119">Pokud $true, DISM nekontaktuje WU.</span><span class="sxs-lookup"><span data-stu-id="d7148-119">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="d7148-120">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="d7148-120">RemoveFilesOnDisable</span></span>| <span data-ttu-id="d7148-121">Nastavte na **$true** odebrat všechny soubory přidružené k této funkci, když je zakázaný (to znamená, když **Ujistěte se, že** je nastavena na "Chybí").</span><span class="sxs-lookup"><span data-stu-id="d7148-121">Set to **$true** to remove all files associated with the feature when it is disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="d7148-122">ÚroveňProtokolu</span><span class="sxs-lookup"><span data-stu-id="d7148-122">LogLevel</span></span>| <span data-ttu-id="d7148-123">Maximální úroveň výstupu zobrazeného v protokolech.</span><span class="sxs-lookup"><span data-stu-id="d7148-123">The maximum output level shown in the logs.</span></span> <span data-ttu-id="d7148-124">Přípustné hodnoty jsou: "ErrorsOnly" (pouze chyby se protokolují), "ErrorsAndWarning" (chyby a upozornění se protokolují) a "ErrorsAndWarningAndInformation" (chyby, upozornění a informace o ladění jsou protokolovány).</span><span class="sxs-lookup"><span data-stu-id="d7148-124">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="d7148-125">LogPath</span><span class="sxs-lookup"><span data-stu-id="d7148-125">LogPath</span></span>| <span data-ttu-id="d7148-126">Cesta k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.</span><span class="sxs-lookup"><span data-stu-id="d7148-126">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="d7148-127">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d7148-127">DependsOn</span></span>| <span data-ttu-id="d7148-128">Určuje, že konfigurace jiný prostředek musí spustit před konfigurací tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="d7148-128">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d7148-129">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d7148-129">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
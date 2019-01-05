---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC balíček
ms.openlocfilehash: 9285df71a303c9a53dd50d450272575a64e962e7
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048129"
---
# <a name="dsc-package-resource"></a><span data-ttu-id="e5ae4-103">Prostředek DSC balíček</span><span class="sxs-lookup"><span data-stu-id="e5ae4-103">DSC Package Resource</span></span>

<span data-ttu-id="e5ae4-104">_Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="e5ae4-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="e5ae4-105">**Balíčku** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků, jako jsou například balíčky Instalační služby systému Windows a setup.exe, na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-105">The **Package** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall packages, such as Windows Installer and setup.exe packages, on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="e5ae4-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="e5ae4-106">Syntax</span></span>

```
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ ReturnCode = [UInt32[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="e5ae4-107">Properties</span><span class="sxs-lookup"><span data-stu-id="e5ae4-107">Properties</span></span>

| <span data-ttu-id="e5ae4-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="e5ae4-108">Property</span></span> | <span data-ttu-id="e5ae4-109">Popis</span><span class="sxs-lookup"><span data-stu-id="e5ae4-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e5ae4-110">Name</span><span class="sxs-lookup"><span data-stu-id="e5ae4-110">Name</span></span>| <span data-ttu-id="e5ae4-111">Určuje název balíčku, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-111">Indicates the name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="e5ae4-112">Cesta</span><span class="sxs-lookup"><span data-stu-id="e5ae4-112">Path</span></span>| <span data-ttu-id="e5ae4-113">Určuje cestu, kde se nachází balíček.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-113">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="e5ae4-114">productId</span><span class="sxs-lookup"><span data-stu-id="e5ae4-114">ProductId</span></span>| <span data-ttu-id="e5ae4-115">Určuje ID produktu, který jednoznačně identifikuje balíček.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-115">Indicates the product ID that uniquely identifies the package.</span></span>|
| <span data-ttu-id="e5ae4-116">Argumenty</span><span class="sxs-lookup"><span data-stu-id="e5ae4-116">Arguments</span></span>| <span data-ttu-id="e5ae4-117">Seznam argumentů, které se předají do balíčku přesně tak, jak zadat řetězec.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-117">Lists a string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="e5ae4-118">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="e5ae4-118">Credential</span></span>| <span data-ttu-id="e5ae4-119">Poskytuje přístup k balíčku na vzdáleného zdroje.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-119">Provides access to the package on a remote source.</span></span> <span data-ttu-id="e5ae4-120">Tato vlastnost se používá k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-120">This property is not used to install the package.</span></span> <span data-ttu-id="e5ae4-121">Balíček je vždy nainstalován v místním systému.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-121">The package is always installed on the local system.</span></span>|
| <span data-ttu-id="e5ae4-122">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="e5ae4-122">Ensure</span></span>| <span data-ttu-id="e5ae4-123">Určuje, zda je nainstalován balíček.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-123">Indicates if the package is installed.</span></span> <span data-ttu-id="e5ae4-124">Nastavte tuto vlastnost na "Chybí" Ujistěte se, že balíček není nainstalovaný, (nebo odinstalovat balíček, je-li nainstalován).</span><span class="sxs-lookup"><span data-stu-id="e5ae4-124">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="e5ae4-125">Nastavte tak, aby "Předložit" (výchozí hodnota) ujistěte se, že je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-125">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="e5ae4-126">LogPath</span><span class="sxs-lookup"><span data-stu-id="e5ae4-126">LogPath</span></span>| <span data-ttu-id="e5ae4-127">Určuje úplnou cestu, kam chcete poskytovatele za účelem uložení souboru protokolu instalace nebo odinstalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-127">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="e5ae4-128">DependsOn</span><span class="sxs-lookup"><span data-stu-id="e5ae4-128">DependsOn</span></span> | <span data-ttu-id="e5ae4-129">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-129">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="e5ae4-130">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-130">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="e5ae4-131">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="e5ae4-131">ReturnCode</span></span>| <span data-ttu-id="e5ae4-132">Označuje očekávaný návratový kód.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-132">Indicates the expected return code.</span></span> <span data-ttu-id="e5ae4-133">Pokud skutečný návratový kód neodpovídá očekávané hodnotě. k dispozici tady, že konfiguraci, vrátí se chyba.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-133">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|

## <a name="example"></a><span data-ttu-id="e5ae4-134">Příklad</span><span class="sxs-lookup"><span data-stu-id="e5ae4-134">Example</span></span>

<span data-ttu-id="e5ae4-135">Tento příklad se spustí instalační program MSI, který se nachází v zadané cestě a má zadaný kód product ID.</span><span class="sxs-lookup"><span data-stu-id="e5ae4-135">This example runs the .msi installer that is located at the specified path and has the specified product ID.</span></span>

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    }
}
```
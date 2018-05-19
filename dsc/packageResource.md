---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC balíček
ms.openlocfilehash: 16f7f1b8fa7b84bcfdeb09fdc46db9c93113e70c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-package-resource"></a><span data-ttu-id="c817a-103">Prostředek DSC balíček</span><span class="sxs-lookup"><span data-stu-id="c817a-103">DSC Package Resource</span></span>

> <span data-ttu-id="c817a-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="c817a-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="c817a-105">**Balíček** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků, například balíčků Instalační služby systému Windows a setup.exe, na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="c817a-105">The **Package** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall packages, such as Windows Installer and setup.exe packages, on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="c817a-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="c817a-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="c817a-107">Properties</span><span class="sxs-lookup"><span data-stu-id="c817a-107">Properties</span></span>
|  <span data-ttu-id="c817a-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="c817a-108">Property</span></span>  |  <span data-ttu-id="c817a-109">Popis</span><span class="sxs-lookup"><span data-stu-id="c817a-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="c817a-110">Název</span><span class="sxs-lookup"><span data-stu-id="c817a-110">Name</span></span>| <span data-ttu-id="c817a-111">Určuje název balíčku, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="c817a-111">Indicates the name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="c817a-112">Cesta</span><span class="sxs-lookup"><span data-stu-id="c817a-112">Path</span></span>| <span data-ttu-id="c817a-113">Určuje cestu, na kterém se nachází balíček.</span><span class="sxs-lookup"><span data-stu-id="c817a-113">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="c817a-114">productId</span><span class="sxs-lookup"><span data-stu-id="c817a-114">ProductId</span></span>| <span data-ttu-id="c817a-115">Určuje ID produktu, který jedinečně identifikuje balíčku.</span><span class="sxs-lookup"><span data-stu-id="c817a-115">Indicates the product ID that uniquely identifies the package.</span></span>|
| <span data-ttu-id="c817a-116">Argumenty</span><span class="sxs-lookup"><span data-stu-id="c817a-116">Arguments</span></span>| <span data-ttu-id="c817a-117">Zobrazí řetězec argumenty, které se předá do balíčku přesně tak, jak zadat.</span><span class="sxs-lookup"><span data-stu-id="c817a-117">Lists a string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="c817a-118">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="c817a-118">Credential</span></span>| <span data-ttu-id="c817a-119">Poskytuje přístup k balíčku na vzdáleného zdroje.</span><span class="sxs-lookup"><span data-stu-id="c817a-119">Provides access to the package on a remote source.</span></span> <span data-ttu-id="c817a-120">Tato vlastnost se používá k instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="c817a-120">This property is not used to install the package.</span></span> <span data-ttu-id="c817a-121">Balíček je vždy nainstalován v místním systému.</span><span class="sxs-lookup"><span data-stu-id="c817a-121">The package is always installed on the local system.</span></span>|
| <span data-ttu-id="c817a-122">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="c817a-122">Ensure</span></span>| <span data-ttu-id="c817a-123">Určuje, zda je nainstalován balíček.</span><span class="sxs-lookup"><span data-stu-id="c817a-123">Indicates if the package is installed.</span></span> <span data-ttu-id="c817a-124">Nastavením této vlastnosti "Chybí" zajistěte, aby byl že balíček není nainstalovaný (nebo má být balíček odinstalován, je-li nainstalován).</span><span class="sxs-lookup"><span data-stu-id="c817a-124">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="c817a-125">Nastavte tak, aby "Prezentovat" (výchozí hodnota) ujistěte se, že je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="c817a-125">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="c817a-126">LogPath</span><span class="sxs-lookup"><span data-stu-id="c817a-126">LogPath</span></span>| <span data-ttu-id="c817a-127">Určuje úplnou cestu, kam chcete zprostředkovatele, který má uložit soubor protokolu instalace a odinstalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="c817a-127">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="c817a-128">dependsOn</span><span class="sxs-lookup"><span data-stu-id="c817a-128">DependsOn</span></span> | <span data-ttu-id="c817a-129">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="c817a-129">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="c817a-130">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba **ResourceName** a její typ je **ResourceType**, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="c817a-130">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|
| <span data-ttu-id="c817a-131">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="c817a-131">ReturnCode</span></span>| <span data-ttu-id="c817a-132">Označuje očekávaný návratový kód.</span><span class="sxs-lookup"><span data-stu-id="c817a-132">Indicates the expected return code.</span></span> <span data-ttu-id="c817a-133">Pokud skutečnou návratový kód neodpovídá očekávané hodnotě zadané tady že konfigurace vrátí chybu.</span><span class="sxs-lookup"><span data-stu-id="c817a-133">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|

## <a name="example"></a><span data-ttu-id="c817a-134">Příklad</span><span class="sxs-lookup"><span data-stu-id="c817a-134">Example</span></span>

<span data-ttu-id="c817a-135">Tento příklad spustí instalační program MSI, který se nachází v zadané cestě a má zadaný produkt ID.</span><span class="sxs-lookup"><span data-stu-id="c817a-135">This example runs the .msi installer that is located at the specified path and has the specified product ID.</span></span>

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
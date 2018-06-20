---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: WindowsPackageCab prostředek DSC
ms.openlocfilehash: 8c4de193c8ea787dd125436f86aa0b5eafdb1509
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190345"
---
# <a name="dsc-windowspackagecab-resource"></a><span data-ttu-id="9a9bb-103">WindowsPackageCab prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="9a9bb-103">DSC WindowsPackageCab Resource</span></span>

> <span data-ttu-id="9a9bb-104">Platí pro: 5.1 a novějším se prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a9bb-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="9a9bb-105">**WindowsPackageCab** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků souboru CAB systému Windows na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-105">The **WindowsPackageCab** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Windows cabinet (.cab) packages on a target node.</span></span>

<span data-ttu-id="9a9bb-106">Cílový uzel musí mít nainstalován modul PowerShell nástroje DISM.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-106">The target node must have the DISM PowerShell module installed.</span></span> <span data-ttu-id="9a9bb-107">Informace najdete v tématu [pomocí nástroje DISM v prostředí Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span><span class="sxs-lookup"><span data-stu-id="9a9bb-107">For information, see [Use DISM in Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span></span>


## <a name="syntax"></a><span data-ttu-id="9a9bb-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9a9bb-108">Syntax</span></span>

```
{
    Name = [string]
    Ensure = [string] { Absent | Present }
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="9a9bb-109">Properties</span><span class="sxs-lookup"><span data-stu-id="9a9bb-109">Properties</span></span>

|  <span data-ttu-id="9a9bb-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="9a9bb-110">Property</span></span>  |  <span data-ttu-id="9a9bb-111">Popis</span><span class="sxs-lookup"><span data-stu-id="9a9bb-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="9a9bb-112">Název</span><span class="sxs-lookup"><span data-stu-id="9a9bb-112">Name</span></span>| <span data-ttu-id="9a9bb-113">Určuje název balíčku pro chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-113">Indicates the name of the package for you want to ensure a specific state.</span></span>|
| <span data-ttu-id="9a9bb-114">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="9a9bb-114">Ensure</span></span>| <span data-ttu-id="9a9bb-115">Určuje, zda je nainstalován balíček.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-115">Indicates if the package is installed.</span></span> <span data-ttu-id="9a9bb-116">Nastavením této vlastnosti "Chybí" zajistěte, aby byl že balíček není nainstalovaný (nebo má být balíček odinstalován, je-li nainstalován).</span><span class="sxs-lookup"><span data-stu-id="9a9bb-116">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="9a9bb-117">Nastavte tak, aby "Prezentovat" (výchozí hodnota) ujistěte se, že je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-117">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="9a9bb-118">Cesta</span><span class="sxs-lookup"><span data-stu-id="9a9bb-118">Path</span></span>| <span data-ttu-id="9a9bb-119">Určuje cestu, na kterém se nachází balíček.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-119">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="9a9bb-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="9a9bb-120">LogPath</span></span>| <span data-ttu-id="9a9bb-121">Určuje úplnou cestu, kam chcete zprostředkovatele, který má uložit soubor protokolu instalace a odinstalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-121">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="9a9bb-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="9a9bb-122">DependsOn</span></span> | <span data-ttu-id="9a9bb-123">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="9a9bb-124">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba **ResourceName** a její typ je **ResourceType**, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="9a9bb-124">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example"></a><span data-ttu-id="9a9bb-125">Příklad</span><span class="sxs-lookup"><span data-stu-id="9a9bb-125">Example</span></span>

<span data-ttu-id="9a9bb-126">Následující příklad konfigurace použije vstupní parametry a zajistí, že soubor .cab do určeného `$Name` parametr je nainstalovaná.</span><span class="sxs-lookup"><span data-stu-id="9a9bb-126">The following example configuration takes input parameters, and ensures that the .cab file specified by the `$Name` parameter is installed.</span></span>

```powershell
Configuration Sample_WindowsPackageCab
{
    param
    (
        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $Name,

        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $SourcePath,

        [Parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $LogPath
    )

    Import-DscResource -ModuleName 'PSDscResources'

    WindowsPackageCab WindowsPackageCab1
    {
        Name = $Name
        Ensure = 'Present'
        SourcePath = $SourcePath
        LogPath = $LogPath
    }
}
```
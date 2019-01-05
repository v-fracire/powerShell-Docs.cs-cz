---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowspackagecab DSC
ms.openlocfilehash: 035944e7ca5c7469250c48a19b79f2f2d5d38e9a
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048126"
---
# <a name="dsc-windowspackagecab-resource"></a><span data-ttu-id="a5eb4-103">Prostředek Windowspackagecab DSC</span><span class="sxs-lookup"><span data-stu-id="a5eb4-103">DSC WindowsPackageCab Resource</span></span>

> <span data-ttu-id="a5eb4-104">Platí pro: Prostředí Windows PowerShell 5.1 a novější</span><span class="sxs-lookup"><span data-stu-id="a5eb4-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="a5eb4-105">**WindowsPackageCab** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků Windows soubor CAB (.cab) na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-105">The **WindowsPackageCab** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Windows cabinet (.cab) packages on a target node.</span></span>

<span data-ttu-id="a5eb4-106">Cílový uzel musí mít nainstalovaný modul PowerShell nástroje DISM.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-106">The target node must have the DISM PowerShell module installed.</span></span> <span data-ttu-id="a5eb4-107">Informace najdete v tématu [pomocí nástroje DISM prostředí Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span><span class="sxs-lookup"><span data-stu-id="a5eb4-107">For information, see [Use DISM in Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span></span>


## <a name="syntax"></a><span data-ttu-id="a5eb4-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a5eb4-108">Syntax</span></span>

```
{
    Name = [string]
    Ensure = [string] { Absent | Present }
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="a5eb4-109">Properties</span><span class="sxs-lookup"><span data-stu-id="a5eb4-109">Properties</span></span>

|  <span data-ttu-id="a5eb4-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a5eb4-110">Property</span></span>  |  <span data-ttu-id="a5eb4-111">Popis</span><span class="sxs-lookup"><span data-stu-id="a5eb4-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="a5eb4-112">Name</span><span class="sxs-lookup"><span data-stu-id="a5eb4-112">Name</span></span>| <span data-ttu-id="a5eb4-113">Určuje název balíčku pro budete muset zajistit, aby určitý stav.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-113">Indicates the name of the package for you want to ensure a specific state.</span></span>|
| <span data-ttu-id="a5eb4-114">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="a5eb4-114">Ensure</span></span>| <span data-ttu-id="a5eb4-115">Určuje, zda je nainstalován balíček.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-115">Indicates if the package is installed.</span></span> <span data-ttu-id="a5eb4-116">Nastavte tuto vlastnost na "Chybí" Ujistěte se, že balíček není nainstalovaný, (nebo odinstalovat balíček, je-li nainstalován).</span><span class="sxs-lookup"><span data-stu-id="a5eb4-116">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="a5eb4-117">Nastavte tak, aby "Předložit" (výchozí hodnota) ujistěte se, že je balíček nainstalován.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-117">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="a5eb4-118">Cesta</span><span class="sxs-lookup"><span data-stu-id="a5eb4-118">Path</span></span>| <span data-ttu-id="a5eb4-119">Určuje cestu, kde se nachází balíček.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-119">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="a5eb4-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="a5eb4-120">LogPath</span></span>| <span data-ttu-id="a5eb4-121">Určuje úplnou cestu, kam chcete poskytovatele za účelem uložení souboru protokolu instalace nebo odinstalace balíčku.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-121">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="a5eb4-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="a5eb4-122">DependsOn</span></span> | <span data-ttu-id="a5eb4-123">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a5eb4-124">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je "DependsOn ="[ ResourceName ResourceType]"".</span><span class="sxs-lookup"><span data-stu-id="a5eb4-124">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example"></a><span data-ttu-id="a5eb4-125">Příklad</span><span class="sxs-lookup"><span data-stu-id="a5eb4-125">Example</span></span>

<span data-ttu-id="a5eb4-126">Následující příklad konfigurace vstupní parametry a zajistí, že soubor .cab určené `$Name` parametr je nainstalována.</span><span class="sxs-lookup"><span data-stu-id="a5eb4-126">The following example configuration takes input parameters, and ensures that the .cab file specified by the `$Name` parameter is installed.</span></span>

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
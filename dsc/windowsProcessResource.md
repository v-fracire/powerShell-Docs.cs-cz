---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "WindowsProcess prostředek DSC"
ms.openlocfilehash: ec77209637d574a0e530f4cce283e1ad98701cdb
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="1ef52-103">WindowsProcess prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="1ef52-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="1ef52-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1ef52-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="1ef52-105">**WindowsProcess** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="1ef52-105">The **WindowsProcess** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="1ef52-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="1ef52-106">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="1ef52-107">Properties</span><span class="sxs-lookup"><span data-stu-id="1ef52-107">Properties</span></span>
|  <span data-ttu-id="1ef52-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="1ef52-108">Property</span></span>  |  <span data-ttu-id="1ef52-109">Popis</span><span class="sxs-lookup"><span data-stu-id="1ef52-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="1ef52-110">Argumenty</span><span class="sxs-lookup"><span data-stu-id="1ef52-110">Arguments</span></span>| <span data-ttu-id="1ef52-111">Určuje řetězec argumenty předání do procesu jako-je.</span><span class="sxs-lookup"><span data-stu-id="1ef52-111">Indicates a string of arguments to pass to the process as-is.</span></span> <span data-ttu-id="1ef52-112">Pokud potřebujete předání několik argumentů, uložili je na tento řetězec.</span><span class="sxs-lookup"><span data-stu-id="1ef52-112">If you need to pass several arguments, put them all in this string.</span></span>| 
| <span data-ttu-id="1ef52-113">Cesta</span><span class="sxs-lookup"><span data-stu-id="1ef52-113">Path</span></span>| <span data-ttu-id="1ef52-114">Cesta ke spustitelnému souboru procesu.</span><span class="sxs-lookup"><span data-stu-id="1ef52-114">The path to the process executable.</span></span> <span data-ttu-id="1ef52-115">Pokud název souboru nebo spustitelný soubor (není plně kvalifikovanou cestu), prostředek DSC hledat prostředí **cesta** proměnné (`$env:Path`) najít spustitelný soubor.</span><span class="sxs-lookup"><span data-stu-id="1ef52-115">If this the file name of the executable (not the fully qualified path), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the executable file.</span></span> <span data-ttu-id="1ef52-116">Pokud je hodnota této vlastnosti plně kvalifikovanou cestu, nebude používat DSC **cesta** proměnné prostředí se najít soubor a vyvolá chybu, pokud cesta neexistuje.</span><span class="sxs-lookup"><span data-stu-id="1ef52-116">If the value of this property is a fully qualified path, DSC will not use the **Path** environment variable to find the file, and will throw an error if the path does not exist.</span></span> <span data-ttu-id="1ef52-117">Relativní cesty nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="1ef52-117">Relative paths are not allowed.</span></span>| 
| <span data-ttu-id="1ef52-118">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="1ef52-118">Credential</span></span>| <span data-ttu-id="1ef52-119">Určuje pověření ke spuštění procesu.</span><span class="sxs-lookup"><span data-stu-id="1ef52-119">Indicates the credentials for starting the process.</span></span>| 
| <span data-ttu-id="1ef52-120">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="1ef52-120">Ensure</span></span>| <span data-ttu-id="1ef52-121">Označuje, pokud proces existuje.</span><span class="sxs-lookup"><span data-stu-id="1ef52-121">Indicates if the process exists.</span></span> <span data-ttu-id="1ef52-122">Nastavením této vlastnosti "Přítomen" Zkontrolujte, zda existuje proces.</span><span class="sxs-lookup"><span data-stu-id="1ef52-122">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="1ef52-123">V opačném případě ji nastavte na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="1ef52-123">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="1ef52-124">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="1ef52-124">The default is "Present".</span></span>| 
| <span data-ttu-id="1ef52-125">dependsOn</span><span class="sxs-lookup"><span data-stu-id="1ef52-125">DependsOn</span></span> | <span data-ttu-id="1ef52-126">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="1ef52-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="1ef52-127">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="1ef52-127">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\` .</span></span>| 
| <span data-ttu-id="1ef52-128">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="1ef52-128">StandardErrorPath</span></span>| <span data-ttu-id="1ef52-129">Určuje, cesta k adresáři pro zápis standardní chybu.</span><span class="sxs-lookup"><span data-stu-id="1ef52-129">Indicates the directory path to write the standard error.</span></span> <span data-ttu-id="1ef52-130">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="1ef52-130">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="1ef52-131">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="1ef52-131">StandardInputPath</span></span>| <span data-ttu-id="1ef52-132">Určuje standardní vstupní umístění.</span><span class="sxs-lookup"><span data-stu-id="1ef52-132">Indicates the standard input location.</span></span>| 
| <span data-ttu-id="1ef52-133">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="1ef52-133">StandardOutputPath</span></span>| <span data-ttu-id="1ef52-134">Určuje umístění pro zápis ve standardním výstupu.</span><span class="sxs-lookup"><span data-stu-id="1ef52-134">Indicates the location to write the standard output.</span></span> <span data-ttu-id="1ef52-135">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="1ef52-135">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="1ef52-136">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="1ef52-136">WorkingDirectory</span></span>| <span data-ttu-id="1ef52-137">Určuje umístění, které se použije jako aktuální pracovní adresář pro proces.</span><span class="sxs-lookup"><span data-stu-id="1ef52-137">Indicates the location that will be used as the current working directory for the process.</span></span>| 


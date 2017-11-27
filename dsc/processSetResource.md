---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "ProcessSet prostředek DSC"
ms.openlocfilehash: b713d1a9c34eab6966de4f342991ead32c19df5d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="6b099-103">WindowsProcess prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="6b099-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="6b099-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6b099-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="6b099-105">**ProcessSet** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="6b099-105">The **ProcessSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span> <span data-ttu-id="6b099-106">Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [WindowsProcess prostředků](windowsProcessResource.md) pro každou skupinu zadaný v `GroupName` parametr.</span><span class="sxs-lookup"><span data-stu-id="6b099-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsProcess resource](windowsProcessResource.md) for each group specified in the `GroupName` parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="6b099-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="6b099-107">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ StandardOutputPath = [string] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]   
    [ WorkingDirectory = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="6b099-108">Properties</span><span class="sxs-lookup"><span data-stu-id="6b099-108">Properties</span></span>
|  <span data-ttu-id="6b099-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="6b099-109">Property</span></span>  |  <span data-ttu-id="6b099-110">Popis</span><span class="sxs-lookup"><span data-stu-id="6b099-110">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="6b099-111">Argumenty</span><span class="sxs-lookup"><span data-stu-id="6b099-111">Arguments</span></span>| <span data-ttu-id="6b099-112">Řetězec, který obsahuje argumenty, které mají být předána do procesu jako-je.</span><span class="sxs-lookup"><span data-stu-id="6b099-112">A string that contains arguments to pass to the process as-is.</span></span> <span data-ttu-id="6b099-113">Pokud potřebujete předání několik argumentů, uložili je na tento řetězec.</span><span class="sxs-lookup"><span data-stu-id="6b099-113">If you need to pass several arguments, put them all in this string.</span></span>| 
| <span data-ttu-id="6b099-114">Cesta</span><span class="sxs-lookup"><span data-stu-id="6b099-114">Path</span></span>| <span data-ttu-id="6b099-115">Cesty k procesu spustitelné soubory.</span><span class="sxs-lookup"><span data-stu-id="6b099-115">The paths to the process executables.</span></span> <span data-ttu-id="6b099-116">Pokud jsou názvy spustitelné soubory (plně kvalifikovaný cest), prostředek DSC hledat prostředí **cesta** proměnné (`$env:Path`) k vyhledání soubory.</span><span class="sxs-lookup"><span data-stu-id="6b099-116">If these are the names of the executable files (not fully qualified paths), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the files.</span></span> <span data-ttu-id="6b099-117">Pokud jsou hodnoty této vlastnosti úplné cesty, nebude používat DSC **cesta** proměnnou prostředí nalézt soubory a vyvolá chybu, pokud neexistuje žádné cesty.</span><span class="sxs-lookup"><span data-stu-id="6b099-117">If the values of this property are fully qualified paths, DSC will not use the **Path** environment variable to find the files, and will throw an error if any of the paths do not exist.</span></span> <span data-ttu-id="6b099-118">Relativní cesty nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="6b099-118">Relative paths are not allowed.</span></span>| 
| <span data-ttu-id="6b099-119">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="6b099-119">Credential</span></span>| <span data-ttu-id="6b099-120">Určuje pověření ke spuštění procesu.</span><span class="sxs-lookup"><span data-stu-id="6b099-120">Indicates the credentials for starting the process.</span></span>| 
| <span data-ttu-id="6b099-121">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="6b099-121">Ensure</span></span>| <span data-ttu-id="6b099-122">Určuje, zda existuje procesy.</span><span class="sxs-lookup"><span data-stu-id="6b099-122">Specifies whether the processes exists.</span></span> <span data-ttu-id="6b099-123">Nastavením této vlastnosti "Přítomen" Zkontrolujte, zda existuje proces.</span><span class="sxs-lookup"><span data-stu-id="6b099-123">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="6b099-124">V opačném případě ji nastavte na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="6b099-124">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="6b099-125">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="6b099-125">The default is "Present".</span></span>| 
| <span data-ttu-id="6b099-126">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="6b099-126">StandardErrorPath</span></span>| <span data-ttu-id="6b099-127">Cesta, do které procesy standardní Chyba zápisu.</span><span class="sxs-lookup"><span data-stu-id="6b099-127">The path to which the processes write standard error.</span></span> <span data-ttu-id="6b099-128">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="6b099-128">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="6b099-129">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="6b099-129">StandardInputPath</span></span>| <span data-ttu-id="6b099-130">Datový proud, ze kterého přijímá proces standardní vstup.</span><span class="sxs-lookup"><span data-stu-id="6b099-130">The stream from which the process receives standard input.</span></span>| 
| <span data-ttu-id="6b099-131">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="6b099-131">StandardOutputPath</span></span>| <span data-ttu-id="6b099-132">Cesta souboru, do které procesy zápisu standardní výstup.</span><span class="sxs-lookup"><span data-stu-id="6b099-132">The path of the file to which the processes write standard output.</span></span> <span data-ttu-id="6b099-133">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="6b099-133">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="6b099-134">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="6b099-134">WorkingDirectory</span></span>| <span data-ttu-id="6b099-135">Umístění použít jako aktuální pracovní adresář pro procesy.</span><span class="sxs-lookup"><span data-stu-id="6b099-135">The location used as the current working directory for the processes.</span></span>| 
| <span data-ttu-id="6b099-136">dependsOn</span><span class="sxs-lookup"><span data-stu-id="6b099-136">DependsOn</span></span> | <span data-ttu-id="6b099-137">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="6b099-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="6b099-138">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba **ResourceName** a její typ je **_ResourceType**, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="6b099-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **_ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`\` .</span></span>| 


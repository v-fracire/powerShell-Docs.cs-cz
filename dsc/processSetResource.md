---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Processset DSC
ms.openlocfilehash: 33000786a9e17e11168b5e08c3bcfcacf3af2611
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268010"
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="b3879-103">Prostředek Windowsprocess DSC</span><span class="sxs-lookup"><span data-stu-id="b3879-103">DSC WindowsProcess Resource</span></span>

<span data-ttu-id="b3879-104">_Platí pro: Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="b3879-104">_Applies To: Windows PowerShell 5.0_</span></span>

<span data-ttu-id="b3879-105">**ProcessSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="b3879-105">The **ProcessSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span> <span data-ttu-id="b3879-106">Tento prostředek je [složený prostředek](authoringResourceComposite.md) , která volá [prostředek windowsprocess](windowsProcessResource.md) pro každou skupinu podle `GroupName` parametru.</span><span class="sxs-lookup"><span data-stu-id="b3879-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsProcess resource](windowsProcessResource.md) for each group specified in the `GroupName` parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="b3879-107">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b3879-107">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="b3879-108">Properties</span><span class="sxs-lookup"><span data-stu-id="b3879-108">Properties</span></span>

| <span data-ttu-id="b3879-109">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="b3879-109">Property</span></span> | <span data-ttu-id="b3879-110">Popis</span><span class="sxs-lookup"><span data-stu-id="b3879-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b3879-111">Argumenty</span><span class="sxs-lookup"><span data-stu-id="b3879-111">Arguments</span></span>| <span data-ttu-id="b3879-112">Řetězec, který obsahuje argumenty budou předány procesu jako-je.</span><span class="sxs-lookup"><span data-stu-id="b3879-112">A string that contains arguments to pass to the process as-is.</span></span> <span data-ttu-id="b3879-113">Pokud je potřeba předat několik argumentů, vytvořte z nich všechny v tomto řetězci.</span><span class="sxs-lookup"><span data-stu-id="b3879-113">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="b3879-114">Cesta</span><span class="sxs-lookup"><span data-stu-id="b3879-114">Path</span></span>| <span data-ttu-id="b3879-115">Cesty pro spustitelné soubory procesu.</span><span class="sxs-lookup"><span data-stu-id="b3879-115">The paths to the process executables.</span></span> <span data-ttu-id="b3879-116">Pokud se jedná se o názvy spustitelných souborů (plně kvalifikovanou cestou), prostředek DSC bude hledat prostředí **cesta** proměnné (`$env:Path`) k vyhledání souborů.</span><span class="sxs-lookup"><span data-stu-id="b3879-116">If these are the names of the executable files (not fully qualified paths), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the files.</span></span> <span data-ttu-id="b3879-117">Pokud jsou hodnoty této vlastnosti plně kvalifikovanou cestou, nebudeme je používat DSC **cesta** proměnnou prostředí k vyhledání souborů a vyvolá chybu, pokud neexistuje žádné cesty.</span><span class="sxs-lookup"><span data-stu-id="b3879-117">If the values of this property are fully qualified paths, DSC will not use the **Path** environment variable to find the files, and will throw an error if any of the paths do not exist.</span></span> <span data-ttu-id="b3879-118">Relativní cesty nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="b3879-118">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="b3879-119">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="b3879-119">Credential</span></span>| <span data-ttu-id="b3879-120">Určuje přihlašovací údaje pro spuštění procesu.</span><span class="sxs-lookup"><span data-stu-id="b3879-120">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="b3879-121">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="b3879-121">Ensure</span></span>| <span data-ttu-id="b3879-122">Určuje, zda existuje procesy.</span><span class="sxs-lookup"><span data-stu-id="b3879-122">Specifies whether the processes exists.</span></span> <span data-ttu-id="b3879-123">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že proces existuje.</span><span class="sxs-lookup"><span data-stu-id="b3879-123">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="b3879-124">Jinak ji nastavte na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="b3879-124">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="b3879-125">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="b3879-125">The default is "Present".</span></span>|
| <span data-ttu-id="b3879-126">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="b3879-126">StandardErrorPath</span></span>| <span data-ttu-id="b3879-127">Cesta, ke kterému procesy standardní Chyba zápisu.</span><span class="sxs-lookup"><span data-stu-id="b3879-127">The path to which the processes write standard error.</span></span> <span data-ttu-id="b3879-128">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="b3879-128">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="b3879-129">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="b3879-129">StandardInputPath</span></span>| <span data-ttu-id="b3879-130">Datový proud, ze kterého proces obdrží standardní vstup.</span><span class="sxs-lookup"><span data-stu-id="b3879-130">The stream from which the process receives standard input.</span></span>|
| <span data-ttu-id="b3879-131">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="b3879-131">StandardOutputPath</span></span>| <span data-ttu-id="b3879-132">Cestu k souboru, ke kterému procesy, které zapisují standardní výstup.</span><span class="sxs-lookup"><span data-stu-id="b3879-132">The path of the file to which the processes write standard output.</span></span> <span data-ttu-id="b3879-133">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="b3879-133">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="b3879-134">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="b3879-134">WorkingDirectory</span></span>| <span data-ttu-id="b3879-135">Umístění použité jako aktuální pracovní adresář pro procesy.</span><span class="sxs-lookup"><span data-stu-id="b3879-135">The location used as the current working directory for the processes.</span></span>|
| <span data-ttu-id="b3879-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="b3879-136">DependsOn</span></span> | <span data-ttu-id="b3879-137">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="b3879-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="b3879-138">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **_ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"` .</span><span class="sxs-lookup"><span data-stu-id="b3879-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **_ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"` .</span></span>|
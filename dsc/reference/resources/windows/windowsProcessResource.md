---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowsprocess DSC
ms.openlocfilehash: cee93ab283ded407d6e032161125aa6d6ac98827
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048152"
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="ead9e-103">Prostředek Windowsprocess DSC</span><span class="sxs-lookup"><span data-stu-id="ead9e-103">DSC WindowsProcess Resource</span></span>

<span data-ttu-id="ead9e-104">_Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="ead9e-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="ead9e-105">**WindowsProcess** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro konfiguraci procesů na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="ead9e-105">The **WindowsProcess** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="ead9e-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ead9e-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="ead9e-107">Properties</span><span class="sxs-lookup"><span data-stu-id="ead9e-107">Properties</span></span>

| <span data-ttu-id="ead9e-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ead9e-108">Property</span></span> | <span data-ttu-id="ead9e-109">Popis</span><span class="sxs-lookup"><span data-stu-id="ead9e-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ead9e-110">Argumenty</span><span class="sxs-lookup"><span data-stu-id="ead9e-110">Arguments</span></span>| <span data-ttu-id="ead9e-111">Určuje řetězec argumenty budou předány procesu jako-je.</span><span class="sxs-lookup"><span data-stu-id="ead9e-111">Indicates a string of arguments to pass to the process as-is.</span></span> <span data-ttu-id="ead9e-112">Pokud je potřeba předat několik argumentů, vytvořte z nich všechny v tomto řetězci.</span><span class="sxs-lookup"><span data-stu-id="ead9e-112">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="ead9e-113">Cesta</span><span class="sxs-lookup"><span data-stu-id="ead9e-113">Path</span></span>| <span data-ttu-id="ead9e-114">Cesta ke spustitelnému souboru procesu.</span><span class="sxs-lookup"><span data-stu-id="ead9e-114">The path to the process executable.</span></span> <span data-ttu-id="ead9e-115">Pokud tento soubor název spustitelného souboru (není plně kvalifikovanou cestu), prostředek DSC bude hledat prostředí **cesta** proměnné (`$env:Path`) spustitelný soubor se nenašel.</span><span class="sxs-lookup"><span data-stu-id="ead9e-115">If this the file name of the executable (not the fully qualified path), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the executable file.</span></span> <span data-ttu-id="ead9e-116">Pokud je hodnota této vlastnosti plně kvalifikovanou cestu, nebudeme je používat DSC **cesta** proměnnou prostředí, aby našli požadovaný soubor a vyvolá chybu, pokud cesta neexistuje.</span><span class="sxs-lookup"><span data-stu-id="ead9e-116">If the value of this property is a fully qualified path, DSC will not use the **Path** environment variable to find the file, and will throw an error if the path does not exist.</span></span> <span data-ttu-id="ead9e-117">Relativní cesty nejsou povoleny.</span><span class="sxs-lookup"><span data-stu-id="ead9e-117">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="ead9e-118">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="ead9e-118">Credential</span></span>| <span data-ttu-id="ead9e-119">Určuje přihlašovací údaje pro spuštění procesu.</span><span class="sxs-lookup"><span data-stu-id="ead9e-119">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="ead9e-120">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="ead9e-120">Ensure</span></span>| <span data-ttu-id="ead9e-121">Určuje, jestli proces existuje.</span><span class="sxs-lookup"><span data-stu-id="ead9e-121">Indicates if the process exists.</span></span> <span data-ttu-id="ead9e-122">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že proces existuje.</span><span class="sxs-lookup"><span data-stu-id="ead9e-122">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="ead9e-123">Jinak ji nastavte na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="ead9e-123">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="ead9e-124">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="ead9e-124">The default is "Present".</span></span>|
| <span data-ttu-id="ead9e-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="ead9e-125">DependsOn</span></span> | <span data-ttu-id="ead9e-126">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="ead9e-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="ead9e-127">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"` .</span><span class="sxs-lookup"><span data-stu-id="ead9e-127">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"` .</span></span>|
| <span data-ttu-id="ead9e-128">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="ead9e-128">StandardErrorPath</span></span>| <span data-ttu-id="ead9e-129">Určuje cestu k adresáři zapsat standardní chybu.</span><span class="sxs-lookup"><span data-stu-id="ead9e-129">Indicates the directory path to write the standard error.</span></span> <span data-ttu-id="ead9e-130">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="ead9e-130">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="ead9e-131">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="ead9e-131">StandardInputPath</span></span>| <span data-ttu-id="ead9e-132">Označuje standardní vstupní umístění.</span><span class="sxs-lookup"><span data-stu-id="ead9e-132">Indicates the standard input location.</span></span>|
| <span data-ttu-id="ead9e-133">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="ead9e-133">StandardOutputPath</span></span>| <span data-ttu-id="ead9e-134">Určuje umístění pro zápis ve standardním výstupu.</span><span class="sxs-lookup"><span data-stu-id="ead9e-134">Indicates the location to write the standard output.</span></span> <span data-ttu-id="ead9e-135">Všechny existující soubory budou přepsány.</span><span class="sxs-lookup"><span data-stu-id="ead9e-135">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="ead9e-136">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="ead9e-136">WorkingDirectory</span></span>| <span data-ttu-id="ead9e-137">Určuje umístění, které se použije jako aktuální pracovní adresář pro proces.</span><span class="sxs-lookup"><span data-stu-id="ead9e-137">Indicates the location that will be used as the current working directory for the process.</span></span>|
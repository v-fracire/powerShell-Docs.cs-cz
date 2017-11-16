---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "WindowsFeatureSet prostředek DSC"
ms.openlocfilehash: 3cdabc36ef35c2bf912ac54393fe40024a8e8bc0
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-windowsfeatureset-resource"></a><span data-ttu-id="a2a21-103">WindowsFeatureSet prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="a2a21-103">DSC WindowsFeatureSet Resource</span></span>

> <span data-ttu-id="a2a21-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a2a21-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="a2a21-105">**WindowsFeatureSet** prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro Ujistěte se, že role a funkce se přidají nebo odeberou na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="a2a21-105">The **WindowsFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>
<span data-ttu-id="a2a21-106">Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [WindowsFeature prostředků](windowsfeatureResource.md) pro každou funkci zadaný v `Name` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="a2a21-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsFeature resource](windowsfeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="a2a21-107">Pokud chcete konfigurovat řadu funkcí systému Windows do stejného stavu, použijte tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="a2a21-107">Use this resource when you want to configure a number of Windows Features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="a2a21-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a2a21-108">Syntax</span></span>

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]] 
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a><span data-ttu-id="a2a21-109">Properties</span><span class="sxs-lookup"><span data-stu-id="a2a21-109">Properties</span></span>

|  <span data-ttu-id="a2a21-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a2a21-110">Property</span></span>  |  <span data-ttu-id="a2a21-111">Popis</span><span class="sxs-lookup"><span data-stu-id="a2a21-111">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="a2a21-112">Název</span><span class="sxs-lookup"><span data-stu-id="a2a21-112">Name</span></span>| <span data-ttu-id="a2a21-113">Názvy rolí nebo funkcí, které chcete zajistit přidání nebo odebrání.</span><span class="sxs-lookup"><span data-stu-id="a2a21-113">The names of the roles or features that you want to ensure are added or removed.</span></span> <span data-ttu-id="a2a21-114">Je to stejné jako **název** vlastnost [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) rutiny a ne zobrazovaným názvem rolí nebo funkcí.</span><span class="sxs-lookup"><span data-stu-id="a2a21-114">This is the same as the **Name** property of the [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet, and not the display name of the roles or features.</span></span>| 
| <span data-ttu-id="a2a21-115">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="a2a21-115">Credential</span></span>| <span data-ttu-id="a2a21-116">Pověření, který se má použít k přidání nebo odebrání rolí nebo funkcí.</span><span class="sxs-lookup"><span data-stu-id="a2a21-116">The credentials to use to add or remove the roles or features.</span></span>| 
| <span data-ttu-id="a2a21-117">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="a2a21-117">Ensure</span></span>| <span data-ttu-id="a2a21-118">Určuje, zda jsou přidány rolí nebo funkcí.</span><span class="sxs-lookup"><span data-stu-id="a2a21-118">Indicates whether the roles or features are added.</span></span> <span data-ttu-id="a2a21-119">Zajistit, že role nebo funkce jsou přidané, nastavte tuto vlastnost "Přítomen" zajistit, že jsou odebrány rolí nebo funkcí, nastavte vlastnost na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="a2a21-119">To ensure that the roles or features are added, set this property to "Present" To ensure that the roles or features are removed, set the property to "Absent".</span></span>| 
| <span data-ttu-id="a2a21-120">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="a2a21-120">IncludeAllSubFeature</span></span>| <span data-ttu-id="a2a21-121">Tuto vlastnost nastavit na **$true** zahrnout všechny požadované jejích s funkcí, které zadáte pomocí **název** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="a2a21-121">Set this property to **$true** to include all required subfeatures with of the features you specify with the **Name** property.</span></span>| 
| <span data-ttu-id="a2a21-122">LogPath</span><span class="sxs-lookup"><span data-stu-id="a2a21-122">LogPath</span></span>| <span data-ttu-id="a2a21-123">Cesta k souboru protokolu, kam chcete poskytovatele prostředků do protokolu operaci.</span><span class="sxs-lookup"><span data-stu-id="a2a21-123">The path to a log file where you want the resource provider to log the operation.</span></span>| 
| <span data-ttu-id="a2a21-124">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a2a21-124">DependsOn</span></span>| <span data-ttu-id="a2a21-125">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="a2a21-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a2a21-126">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a2a21-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 
| <span data-ttu-id="a2a21-127">Zdroj</span><span class="sxs-lookup"><span data-stu-id="a2a21-127">Source</span></span>| <span data-ttu-id="a2a21-128">Určuje umístění zdrojového souboru pro instalaci, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="a2a21-128">Indicates the location of the source file to use for installation, if necessary.</span></span>| 

## <a name="example"></a><span data-ttu-id="a2a21-129">Příklad</span><span class="sxs-lookup"><span data-stu-id="a2a21-129">Example</span></span>

<span data-ttu-id="a2a21-130">Následující konfigurace zajišťuje, že **Webový Server** (IIS) a **SMTP Server** funkce a všechny podfunkce jednotlivých, jsou nainstalované.</span><span class="sxs-lookup"><span data-stu-id="a2a21-130">The following configuration ensures that the **Web-Server** (IIS) and **SMTP Server** features, and all subfeatures of each, are installed.</span></span>

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        } 
    }
}
```


---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowsfeatureset DSC
ms.openlocfilehash: 8b7c7e72dd58459bd19cb723e5790a82841515c0
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048116"
---
# <a name="dsc-windowsfeatureset-resource"></a><span data-ttu-id="b261f-103">Prostředek Windowsfeatureset DSC</span><span class="sxs-lookup"><span data-stu-id="b261f-103">DSC WindowsFeatureSet Resource</span></span>

> <span data-ttu-id="b261f-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b261f-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="b261f-105">**WindowsFeatureSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zajištění, že role a funkce přidávají a odebírají na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="b261f-105">The **WindowsFeatureSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that roles and features are added or removed on a target node.</span></span>
<span data-ttu-id="b261f-106">Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [prostředek WindowsFeature](windowsfeatureResource.md) pro každou součást podle `Name` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="b261f-106">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [WindowsFeature resource](windowsfeatureResource.md) for each feature specified in the `Name` property.</span></span>

<span data-ttu-id="b261f-107">Pokud chcete konfigurovat řadu funkcí Windows do stejného stavu, použijte tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="b261f-107">Use this resource when you want to configure a number of Windows Features to the same state.</span></span>

## <a name="syntax"></a><span data-ttu-id="b261f-108">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b261f-108">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="b261f-109">Properties</span><span class="sxs-lookup"><span data-stu-id="b261f-109">Properties</span></span>

|  <span data-ttu-id="b261f-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="b261f-110">Property</span></span>  |  <span data-ttu-id="b261f-111">Popis</span><span class="sxs-lookup"><span data-stu-id="b261f-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="b261f-112">Name</span><span class="sxs-lookup"><span data-stu-id="b261f-112">Name</span></span>| <span data-ttu-id="b261f-113">Názvy rolí nebo funkcí, které chcete zajistit přidávají a odebírají.</span><span class="sxs-lookup"><span data-stu-id="b261f-113">The names of the roles or features that you want to ensure are added or removed.</span></span> <span data-ttu-id="b261f-114">To je stejný jako **název** vlastnost [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) rutiny a ne zobrazovaným názvem rolí nebo funkcí.</span><span class="sxs-lookup"><span data-stu-id="b261f-114">This is the same as the **Name** property of the [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet, and not the display name of the roles or features.</span></span>|
| <span data-ttu-id="b261f-115">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="b261f-115">Credential</span></span>| <span data-ttu-id="b261f-116">Pověření, které slouží k přidání nebo odebrání rolí nebo funkcí.</span><span class="sxs-lookup"><span data-stu-id="b261f-116">The credentials to use to add or remove the roles or features.</span></span>|
| <span data-ttu-id="b261f-117">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="b261f-117">Ensure</span></span>| <span data-ttu-id="b261f-118">Označuje, zda jsou přidány role nebo funkce.</span><span class="sxs-lookup"><span data-stu-id="b261f-118">Indicates whether the roles or features are added.</span></span> <span data-ttu-id="b261f-119">K zajištění, že role nebo funkce přidání, nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že role nebo funkce, jsou odebrány, nastavte vlastnost na "Chybí".</span><span class="sxs-lookup"><span data-stu-id="b261f-119">To ensure that the roles or features are added, set this property to "Present" To ensure that the roles or features are removed, set the property to "Absent".</span></span>|
| <span data-ttu-id="b261f-120">IncludeAllSubFeature</span><span class="sxs-lookup"><span data-stu-id="b261f-120">IncludeAllSubFeature</span></span>| <span data-ttu-id="b261f-121">Tuto vlastnost nastavte na **$true** zahrnout všechny požadované podfunkce s funkcí, které zadáte **název** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="b261f-121">Set this property to **$true** to include all required subfeatures with of the features you specify with the **Name** property.</span></span>|
| <span data-ttu-id="b261f-122">LogPath</span><span class="sxs-lookup"><span data-stu-id="b261f-122">LogPath</span></span>| <span data-ttu-id="b261f-123">Cesta k souboru protokolu, ve kterém chcete protokolovat operace poskytovatele prostředků.</span><span class="sxs-lookup"><span data-stu-id="b261f-123">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="b261f-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="b261f-124">DependsOn</span></span>| <span data-ttu-id="b261f-125">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="b261f-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="b261f-126">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="b261f-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="b261f-127">Zdroj</span><span class="sxs-lookup"><span data-stu-id="b261f-127">Source</span></span>| <span data-ttu-id="b261f-128">Určuje umístění zdrojového souboru pro použití pro instalaci, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="b261f-128">Indicates the location of the source file to use for installation, if necessary.</span></span>|

## <a name="example"></a><span data-ttu-id="b261f-129">Příklad</span><span class="sxs-lookup"><span data-stu-id="b261f-129">Example</span></span>

<span data-ttu-id="b261f-130">Následující konfigurace zajistí, že **Webový Server** (IIS) a **SMTP Server** funkce a všechny podfunkce jednotlivých, jsou nainstalované.</span><span class="sxs-lookup"><span data-stu-id="b261f-130">The following configuration ensures that the **Web-Server** (IIS) and **SMTP Server** features, and all subfeatures of each, are installed.</span></span>

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

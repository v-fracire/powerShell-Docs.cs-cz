---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: ab49a0ae10f9ad32966944a1dcf8125619bde141
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="new-built-in-dsc-resources"></a><span data-ttu-id="f0393-102">Nové vestavěné prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f0393-102">New built-in DSC resources</span></span>

<span data-ttu-id="f0393-103">WMF 5.0 RTM má 4 nové prostředky DSC:</span><span class="sxs-lookup"><span data-stu-id="f0393-103">WMF 5.0 RTM has 4 new DSC resources:</span></span> 
* <span data-ttu-id="f0393-104">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="f0393-104">WindowsFeatureSet</span></span>
* <span data-ttu-id="f0393-105">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="f0393-105">WindowsOptionalFeatureSet</span></span>
* <span data-ttu-id="f0393-106">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="f0393-106">ServiceSet</span></span>
* <span data-ttu-id="f0393-107">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="f0393-107">ProcessSet</span></span> 

<span data-ttu-id="f0393-108">Tyto zdroje poskytují snadný způsob, jak nakonfigurovat více instancí pomocí volání jednoho zdroje.</span><span class="sxs-lookup"><span data-stu-id="f0393-108">These resources provide an easy way to configure multiple instances using a single resource call.</span></span>

## <a name="windowsfeatureset"></a><span data-ttu-id="f0393-109">WindowsFeatureSet</span><span class="sxs-lookup"><span data-stu-id="f0393-109">WindowsFeatureSet</span></span>

```powershell
# Get the syntax of WindowsFeatureSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name WindowsFeatureSet -Syntax

WindowsFeatureSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Name = [String[]]
    [Ensure = [String]]
    [Source = [String]]
    [IncludeAllSubFeature = [Boolean]]
    [Credential = [PSCredential]]
    [LogPath = [String]]
}
```

## <a name="windowsoptionalfeatureset"></a><span data-ttu-id="f0393-110">WindowsOptionalFeatureSet</span><span class="sxs-lookup"><span data-stu-id="f0393-110">WindowsOptionalFeatureSet</span></span> 

```powershell
# Get the syntax of WindowsOptionalFeatureSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name WindowsOptionalFeatureSet -Syntax

WindowsOptionalFeatureSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Name = [String[]]
    Ensure = [String]
    [Source = [String[]]]
    [RemoveFilesOnDisable = [Boolean]]
    [LogPath = [String]]
    [NoWindowsUpdateCheck = [Boolean]]
    [LogLevel = [String]]
}
```

## <a name="serviceset"></a><span data-ttu-id="f0393-111">ServiceSet</span><span class="sxs-lookup"><span data-stu-id="f0393-111">ServiceSet</span></span> 

```powershell
# Get the syntax of ServiceSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name ServiceSet -Syntax

ServiceSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Name = [String[]]
    [StartupType = [String]]
    [BuiltInAccount = [String]]
    [State = [String]]
    [Ensure = [String]]
    [Credential = [PSCredential]]
}
```

## <a name="processset"></a><span data-ttu-id="f0393-112">ProcessSet</span><span class="sxs-lookup"><span data-stu-id="f0393-112">ProcessSet</span></span> 

```powershell
# Get the syntax of ProcessSet resource
Get-DscResource -Module psdesiredstateconfiguration -Name ProcessSet -Syntax

ProcessSet [String] #ResourceName
{
    [DependsOn = [String[]]]
    Path = [String[]]
    [Credential = [PSCredential]]
    [Ensure = [String]]
    [StandardOutputPath = [String]]
    [StandardErrorPath = [String]]
    [StandardInputPath = [String]]
    [WorkingDirectory = [String]]
}
```


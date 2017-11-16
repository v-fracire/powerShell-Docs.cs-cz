---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC protokolu"
ms.openlocfilehash: 72c9c5a9b8e2a4ed4ce43cfd792572ce95b502b3
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-log-resource"></a><span data-ttu-id="ce694-103">Prostředek DSC protokolu</span><span class="sxs-lookup"><span data-stu-id="ce694-103">DSC Log Resource</span></span> 

> <span data-ttu-id="ce694-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ce694-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="ce694-105">__Protokolu__ prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro zápis zpráv do protokolu událostí stavu Microsoft-Windows-požadovaná konfigurace nebo analýzu.</span><span class="sxs-lookup"><span data-stu-id="ce694-105">The __Log__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

<span data-ttu-id="ce694-106">Poznámka: Ve výchozím nastavení pouze v provozních protokolech DSC jsou povolené.</span><span class="sxs-lookup"><span data-stu-id="ce694-106">NOTE: By default only the Operational logs for DSC are enabled.</span></span>
<span data-ttu-id="ce694-107">Před analytické protokolu bude k dispozici nebo viditelná, musí být povolena.</span><span class="sxs-lookup"><span data-stu-id="ce694-107">Before the Analytic log will be available or visible, it must be enabled.</span></span>
<span data-ttu-id="ce694-108">Najdete v následujícím článku.</span><span class="sxs-lookup"><span data-stu-id="ce694-108">See the following article.</span></span>

[<span data-ttu-id="ce694-109">Kde jsou protokoly událostí DSC?</span><span class="sxs-lookup"><span data-stu-id="ce694-109">Where are DSC Event Logs?</span></span>](https://msdn.microsoft.com/en-us/powershell/dsc/troubleshooting#where-are-dsc-event-logs)

## <a name="properties"></a><span data-ttu-id="ce694-110">Properties</span><span class="sxs-lookup"><span data-stu-id="ce694-110">Properties</span></span>
|  <span data-ttu-id="ce694-111">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ce694-111">Property</span></span>  |  <span data-ttu-id="ce694-112">Popis</span><span class="sxs-lookup"><span data-stu-id="ce694-112">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="ce694-113">Zpráva</span><span class="sxs-lookup"><span data-stu-id="ce694-113">Message</span></span>| <span data-ttu-id="ce694-114">Určuje zprávu, kterou chcete zapisovat do protokolu událostí Microsoft-Windows-Desired stav konfigurace nebo analýzu.</span><span class="sxs-lookup"><span data-stu-id="ce694-114">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>| 
| <span data-ttu-id="ce694-115">dependsOn</span><span class="sxs-lookup"><span data-stu-id="ce694-115">DependsOn</span></span> | <span data-ttu-id="ce694-116">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než získá zapsat tuto zprávu protokolu.</span><span class="sxs-lookup"><span data-stu-id="ce694-116">Indicates that the configuration of another resource must run before this log message gets written.</span></span> <span data-ttu-id="ce694-117">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="ce694-117">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="example"></a><span data-ttu-id="ce694-118">Příklad</span><span class="sxs-lookup"><span data-stu-id="ce694-118">Example</span></span>

<span data-ttu-id="ce694-119">Následující příklad ukazuje, jak chcete zahrnout zprávy v protokolu událostí Microsoft-Windows-Desired stav konfigurace nebo analýzu.</span><span class="sxs-lookup"><span data-stu-id="ce694-119">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> <span data-ttu-id="ce694-120">**Poznámka:**: Pokud spustíte [Test DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) se tento prostředek nakonfigurován, bude vždy vrátí **$false**.</span><span class="sxs-lookup"><span data-stu-id="ce694-120">**Note**: if you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

```powershell 
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost

    {
        Log LogExample
        {
            Message = "This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log."
        }
    }
}
```

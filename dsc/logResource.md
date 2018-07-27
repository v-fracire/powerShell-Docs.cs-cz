---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Log
ms.openlocfilehash: 50fd6cd31ba426108830fcf124a767318060a95d
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268428"
---
# <a name="dsc-log-resource"></a><span data-ttu-id="f2cb1-103">Prostředek DSC Log</span><span class="sxs-lookup"><span data-stu-id="f2cb1-103">DSC Log Resource</span></span>

<span data-ttu-id="f2cb1-104">_Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="f2cb1-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="f2cb1-105">__Protokolu__ prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zápis zpráv do protokolu událostí Microsoft-Windows-Desired State Configuration / analýzy.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-105">The __Log__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

> [!NOTE]
> <span data-ttu-id="f2cb1-106">Ve výchozím nastavení jsou povoleny pouze v provozních protokolech DSC.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-106">By default only the Operational logs for DSC are enabled.</span></span> <span data-ttu-id="f2cb1-107">Předtím, než v analytickém protokolu bude k dispozici nebo viditelné, musí být povolena.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-107">Before the Analytic log will be available or visible, it must be enabled.</span></span> <span data-ttu-id="f2cb1-108">Další informace najdete v tématu [kde jsou protokoly událostí DSC?](troubleshooting.md#where-are-dsc-event-logs).</span><span class="sxs-lookup"><span data-stu-id="f2cb1-108">For more information, see [Where are DSC Event Logs?](troubleshooting.md#where-are-dsc-event-logs).</span></span>

## <a name="properties"></a><span data-ttu-id="f2cb1-109">Properties</span><span class="sxs-lookup"><span data-stu-id="f2cb1-109">Properties</span></span>

| <span data-ttu-id="f2cb1-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="f2cb1-110">Property</span></span> | <span data-ttu-id="f2cb1-111">Popis</span><span class="sxs-lookup"><span data-stu-id="f2cb1-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f2cb1-112">Zpráva</span><span class="sxs-lookup"><span data-stu-id="f2cb1-112">Message</span></span>| <span data-ttu-id="f2cb1-113">Určuje zprávu, kterou chcete zapisovat do protokolu událostí stavu Microsoft-Windows-Desired konfigurace/analýzy.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-113">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>|
| <span data-ttu-id="f2cb1-114">DependsOn</span><span class="sxs-lookup"><span data-stu-id="f2cb1-114">DependsOn</span></span> | <span data-ttu-id="f2cb1-115">Označuje, že konfigurace jiný prostředek musí spustit před napsané tuto zprávu protokolu.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-115">Indicates that the configuration of another resource must run before this log message gets written.</span></span> <span data-ttu-id="f2cb1-116">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = '[ResourceType]ResourceName'`.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-116">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = '[ResourceType]ResourceName'`.</span></span>|

## <a name="example"></a><span data-ttu-id="f2cb1-117">Příklad</span><span class="sxs-lookup"><span data-stu-id="f2cb1-117">Example</span></span>

<span data-ttu-id="f2cb1-118">Následující příklad ukazuje, jak zahrnout zprávy v protokolu událostí stavu Microsoft-Windows-Desired konfigurace/analýzy.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-118">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> [!NOTE]
> <span data-ttu-id="f2cb1-119">Pokud spustíte [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) se tento prostředek nakonfigurován, bude vždy vrátí **$false**.</span><span class="sxs-lookup"><span data-stu-id="f2cb1-119">If you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Log LogExample
        {
            Message = 'This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log.'
        }
    }
}
```
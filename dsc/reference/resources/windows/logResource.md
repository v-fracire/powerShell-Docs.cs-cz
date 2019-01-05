---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC Log
ms.openlocfilehash: 1f94a2d847a4ef63f81e2fb83d1a0f76f5677b09
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048140"
---
# <a name="dsc-log-resource"></a><span data-ttu-id="fc6d2-103">Prostředek DSC Log</span><span class="sxs-lookup"><span data-stu-id="fc6d2-103">DSC Log Resource</span></span>

> <span data-ttu-id="fc6d2-104">_Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="fc6d2-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="fc6d2-105">__Protokolu__ prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro zápis zpráv do protokolu událostí Microsoft-Windows-Desired State Configuration / analýzy.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-105">The __Log__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

```
Syntax

Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
}
```

> [!NOTE]
> <span data-ttu-id="fc6d2-106">Ve výchozím nastavení jsou povoleny pouze v provozních protokolech DSC.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-106">By default only the Operational logs for DSC are enabled.</span></span> <span data-ttu-id="fc6d2-107">Předtím, než v analytickém protokolu bude k dispozici nebo viditelné, musí být povolena.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-107">Before the Analytic log will be available or visible, it must be enabled.</span></span> <span data-ttu-id="fc6d2-108">Další informace najdete v tématu [kde jsou protokoly událostí DSC?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).</span><span class="sxs-lookup"><span data-stu-id="fc6d2-108">For more information, see [Where are DSC Event Logs?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).</span></span>

## <a name="properties"></a><span data-ttu-id="fc6d2-109">Properties</span><span class="sxs-lookup"><span data-stu-id="fc6d2-109">Properties</span></span>

| <span data-ttu-id="fc6d2-110">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="fc6d2-110">Property</span></span> | <span data-ttu-id="fc6d2-111">Popis</span><span class="sxs-lookup"><span data-stu-id="fc6d2-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fc6d2-112">Zpráva</span><span class="sxs-lookup"><span data-stu-id="fc6d2-112">Message</span></span>| <span data-ttu-id="fc6d2-113">Určuje zprávu, kterou chcete zapisovat do protokolu událostí stavu Microsoft-Windows-Desired konfigurace/analýzy.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-113">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>|
| <span data-ttu-id="fc6d2-114">DependsOn</span><span class="sxs-lookup"><span data-stu-id="fc6d2-114">DependsOn</span></span> | <span data-ttu-id="fc6d2-115">Označuje, že konfigurace jiný prostředek musí spustit před napsané tuto zprávu protokolu.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-115">Indicates that the configuration of another resource must run before this log message gets written.</span></span> <span data-ttu-id="fc6d2-116">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je `DependsOn = '[ResourceType]ResourceName'`.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-116">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = '[ResourceType]ResourceName'`.</span></span>|

## <a name="example"></a><span data-ttu-id="fc6d2-117">Příklad</span><span class="sxs-lookup"><span data-stu-id="fc6d2-117">Example</span></span>

<span data-ttu-id="fc6d2-118">Následující příklad ukazuje, jak zahrnout zprávy v protokolu událostí stavu Microsoft-Windows-Desired konfigurace/analýzy.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-118">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> [!NOTE]
> <span data-ttu-id="fc6d2-119">Pokud spustíte [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) se tento prostředek nakonfigurován, bude vždy vrátí **$false**.</span><span class="sxs-lookup"><span data-stu-id="fc6d2-119">If you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

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

---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Podmíněné příkazy a smyčky v konfiguracích
ms.openlocfilehash: 0073d94d28afbb45bb635442129a6cddde4c805a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403665"
---
# <a name="conditional-statements-and-loops-in-configurations"></a><span data-ttu-id="49961-103">Podmíněné příkazy a smyčky v konfiguracích</span><span class="sxs-lookup"><span data-stu-id="49961-103">Conditional statements and loops in Configurations</span></span>

<span data-ttu-id="49961-104">Můžete provést vaše [konfigurace](configurations.md) dynamičtějších pomocí klíčových slov řízení toku prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49961-104">You can make your [Configurations](configurations.md) more dynamic using PowerShell flow-control keywords.</span></span> <span data-ttu-id="49961-105">Tento článek vám ukáže, jak provést konfiguraci dynamičtějších můžete podmíněné příkazy a smyčky.</span><span class="sxs-lookup"><span data-stu-id="49961-105">This article will show you how you can use conditional statements, and loops to make your Configurations more dynamic.</span></span> <span data-ttu-id="49961-106">Kombinování podmíněné a smyčky s [parametry](add-parameters-to-a-configuration.md) a [konfigurační Data](configData.md) vám umožní větší flexibility a kontroly, při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="49961-106">Combining conditional and loops with [parameters](add-parameters-to-a-configuration.md) and [Configuration Data](configData.md) allows you more flexibility and control when compiling your Configurations.</span></span>

<span data-ttu-id="49961-107">Stejně jako funkce nebo blok skriptu můžete použít libovolný jazyk prostředí PowerShell v rámci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="49961-107">Just like a Function or a Script Block, you can use any PowerShell language within a Configuration.</span></span> <span data-ttu-id="49961-108">Příkazy, které můžete použít se vyhodnotí pouze při volání konfiguraci pro kompilaci ".mof".</span><span class="sxs-lookup"><span data-stu-id="49961-108">The statements you use will only be evaluated when you call your Configuration to compile a ".mof" file.</span></span> <span data-ttu-id="49961-109">Následující příklady ukazují jednoduché scénáře k předvedení konceptů.</span><span class="sxs-lookup"><span data-stu-id="49961-109">The examples below show simple scenarios to demonstrate concepts.</span></span> <span data-ttu-id="49961-110">Podmíněné výrazy jsou smyčky se častěji používají s parametry a konfigurační Data.</span><span class="sxs-lookup"><span data-stu-id="49961-110">Conditionals are loops are more often used with parameters and Configuration Data.</span></span>

<span data-ttu-id="49961-111">V tomto jednoduchém příkladu **služby** prostředků bloku načte aktuální stav služby v době kompilace k vygenerování souboru ".mof", který udržuje jeho aktuální stav.</span><span class="sxs-lookup"><span data-stu-id="49961-111">In this simple example, the **Service** resource block retrieves the current state of a service at compile time to generate a ".mof" file that maintains its current state.</span></span>

> [!NOTE]
> <span data-ttu-id="49961-112">Pomocí dynamických prostředků bloků se vyřizuje efektivitu technologie Intellisense.</span><span class="sxs-lookup"><span data-stu-id="49961-112">Using dynamic Resource blocks will preempt the effectiveness of Intellisense.</span></span> <span data-ttu-id="49961-113">Analyzátor Powershellu nelze určit, pokud zadané hodnoty jsou přijatelné, dokud je zkompilován konfigurace.</span><span class="sxs-lookup"><span data-stu-id="49961-113">The PowerShell parser cannot determine if the values specified are acceptable until the Configuration is compiled.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Service Spooler
        {
            Name = "Spooler"
            State = $(Get-Service -Name 'spooler').Status
            StartType = $(Get-Service -Name 'spooler').StartType
        }
    }
}
```

<span data-ttu-id="49961-114">Kromě toho můžete vytvořit **služby** blokovat prostředků pro každou službu na aktuálním počítači pomocí `foreach` smyčky.</span><span class="sxs-lookup"><span data-stu-id="49961-114">Additionally, you could create a **Service** block resource for every service on the current machine, using a `foreach` loop.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration
    Node localhost
    {
        Foreach ($service in $(Get-Service))
        {
            Service $service.Name
            {
                Name = $service.Name
                State = $service.Status
                StartType = $service.StartType
            }
        }
    }
}
```

<span data-ttu-id="49961-115">Můžete také pouze vytvořit konfigurace pro počítače, které jsou online, pomocí jednoduchého `if` příkazu.</span><span class="sxs-lookup"><span data-stu-id="49961-115">You could also only create configurations for machines that are online, by using a simple `if` statement.</span></span>

```powershell
Configuration ServiceState
{
    # It is best practice to explicitly import any resources used in your Configurations.
    Import-DSCResource -Name Service -Module PSDesiredStateConfiguration

    Foreach ($computer in @('Server01', 'Server02', 'Server03'))
    {
        if (Test-Connection -ComputerName $computer)
        {
            Node $computer
            {
                Service "Spooler"
                {
                    Name = "Spooler"
                    State = "Started"
                }
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="49961-116">Dynamický prostředek bloků v odkazu na výše uvedené příklady aktuálního počítače.</span><span class="sxs-lookup"><span data-stu-id="49961-116">The dynamic resource blocks in the above examples reference the current machine.</span></span> <span data-ttu-id="49961-117">V tomto případě, že bude vytváření konfiguraci na počítači, není cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="49961-117">In this instance, that would be the machine you are authoring the Configuration on, not the target Node.</span></span>

<!---
Mention Get-DSCConfigurationFromSystem
-->

## <a name="summary"></a><span data-ttu-id="49961-118">Souhrn</span><span class="sxs-lookup"><span data-stu-id="49961-118">Summary</span></span>

<span data-ttu-id="49961-119">Stručně řečeno můžete použít libovolný jazyk prostředí PowerShell v rámci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="49961-119">In summary, you can use any PowerShell language within a Configuration.</span></span>

<span data-ttu-id="49961-120">Zahrnuje to takové věci, jako jsou:</span><span class="sxs-lookup"><span data-stu-id="49961-120">This includes things like:</span></span>

- <span data-ttu-id="49961-121">Vlastní objekty</span><span class="sxs-lookup"><span data-stu-id="49961-121">Custom Objects</span></span>
- <span data-ttu-id="49961-122">Zatřiďovací tabulky</span><span class="sxs-lookup"><span data-stu-id="49961-122">Hashtables</span></span>
- <span data-ttu-id="49961-123">Zacházení s řetězci</span><span class="sxs-lookup"><span data-stu-id="49961-123">String manipulation</span></span>
- <span data-ttu-id="49961-124">Vzdálená komunikace</span><span class="sxs-lookup"><span data-stu-id="49961-124">Remoting</span></span>
- <span data-ttu-id="49961-125">Rozhraní WMI a CIM</span><span class="sxs-lookup"><span data-stu-id="49961-125">WMI and CIM</span></span>
- <span data-ttu-id="49961-126">Objekty Active Directory</span><span class="sxs-lookup"><span data-stu-id="49961-126">ActiveDirectory objects</span></span>
- <span data-ttu-id="49961-127">a další...</span><span class="sxs-lookup"><span data-stu-id="49961-127">and more...</span></span>

<span data-ttu-id="49961-128">Jakýkoli kód Powershellu definované v konfiguraci se vyhodnotí době kompilace, ale můžete také umístit kód ve skriptu, který obsahuje konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="49961-128">Any PowerShell code defined in a Configuration will be evaluated a compile time, but you can also place code in the script containing your Configuration.</span></span> <span data-ttu-id="49961-129">Veškerý kód mimo blok konfigurace se spustí při importu vaší konfigurace.</span><span class="sxs-lookup"><span data-stu-id="49961-129">Any code outside of the Configuration block will be executed when you import your Configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="49961-130">Viz taky</span><span class="sxs-lookup"><span data-stu-id="49961-130">See also</span></span>

- [<span data-ttu-id="49961-131">Přidání parametrů ke konfiguraci</span><span class="sxs-lookup"><span data-stu-id="49961-131">Add parameters to a Configuration</span></span>](add-parameters-to-a-configuration.md)
- [<span data-ttu-id="49961-132">Samostatný konfigurační data z konfigurace</span><span class="sxs-lookup"><span data-stu-id="49961-132">Separate Configuration data from Configurations</span></span>](configData.md)

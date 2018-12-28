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
# <a name="conditional-statements-and-loops-in-configurations"></a>Podmíněné příkazy a smyčky v konfiguracích

Můžete provést vaše [konfigurace](configurations.md) dynamičtějších pomocí klíčových slov řízení toku prostředí PowerShell. Tento článek vám ukáže, jak provést konfiguraci dynamičtějších můžete podmíněné příkazy a smyčky. Kombinování podmíněné a smyčky s [parametry](add-parameters-to-a-configuration.md) a [konfigurační Data](configData.md) vám umožní větší flexibility a kontroly, při kompilaci konfigurace.

Stejně jako funkce nebo blok skriptu můžete použít libovolný jazyk prostředí PowerShell v rámci konfigurace. Příkazy, které můžete použít se vyhodnotí pouze při volání konfiguraci pro kompilaci ".mof". Následující příklady ukazují jednoduché scénáře k předvedení konceptů. Podmíněné výrazy jsou smyčky se častěji používají s parametry a konfigurační Data.

V tomto jednoduchém příkladu **služby** prostředků bloku načte aktuální stav služby v době kompilace k vygenerování souboru ".mof", který udržuje jeho aktuální stav.

> [!NOTE]
> Pomocí dynamických prostředků bloků se vyřizuje efektivitu technologie Intellisense. Analyzátor Powershellu nelze určit, pokud zadané hodnoty jsou přijatelné, dokud je zkompilován konfigurace.

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

Kromě toho můžete vytvořit **služby** blokovat prostředků pro každou službu na aktuálním počítači pomocí `foreach` smyčky.

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

Můžete také pouze vytvořit konfigurace pro počítače, které jsou online, pomocí jednoduchého `if` příkazu.

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
> Dynamický prostředek bloků v odkazu na výše uvedené příklady aktuálního počítače. V tomto případě, že bude vytváření konfiguraci na počítači, není cílový uzel.

<!---
Mention Get-DSCConfigurationFromSystem
-->

## <a name="summary"></a>Souhrn

Stručně řečeno můžete použít libovolný jazyk prostředí PowerShell v rámci konfigurace.

Zahrnuje to takové věci, jako jsou:

- Vlastní objekty
- Zatřiďovací tabulky
- Zacházení s řetězci
- Vzdálená komunikace
- Rozhraní WMI a CIM
- Objekty Active Directory
- a další...

Jakýkoli kód Powershellu definované v konfiguraci se vyhodnotí době kompilace, ale můžete také umístit kód ve skriptu, který obsahuje konfiguraci. Veškerý kód mimo blok konfigurace se spustí při importu vaší konfigurace.

## <a name="see-also"></a>Viz taky

- [Přidání parametrů ke konfiguraci](add-parameters-to-a-configuration.md)
- [Samostatný konfigurační data z konfigurace](configData.md)

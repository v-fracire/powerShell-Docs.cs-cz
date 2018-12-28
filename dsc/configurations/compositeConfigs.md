---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Vnořování konfigurací
ms.openlocfilehash: 54162cd72d2d1e7773e3be636bfa681329854498
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403656"
---
# <a name="nesting-dsc-configurations"></a>Vnořování konfigurací DSC

Vnořené konfigurace (také nazývané složené configuration) je konfigurace, která je volána v rámci jiné konfigurace, jako by šlo prostředku.
Obě konfigurace musí být definován ve stejném souboru.

Podívejme se na jednoduchý příklad:

```powershell
Configuration FileConfig
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
       {
           SourcePath = $CopyFrom
           DestinationPath = $CopyTo
           Ensure = 'Present'
       }

}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

V tomto příkladu `FileConfig` používá dva povinné parametry **CopyFrom –** a **CopyTo**, které se používají jako hodnoty **SourcePath** a  **DestinationPath** vlastnosti `File` prostředků bloku.
`NestedConfig` Konfigurace volání `FileConfig` jako by šlo prostředku.
Vlastnosti `NestedConfig` bloku prostředků (**CopyFrom –** a **CopyTo**) jsou parametry `FileConfig` konfigurace.

## <a name="see-also"></a>Viz také

- [Složené prostředky – pomocí konfigurace DSC jako prostředek](../resources/authoringResourceComposite.md)
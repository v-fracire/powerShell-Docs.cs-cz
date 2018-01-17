---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Konfigurace vnoření"
ms.openlocfilehash: 89badda86707a129909b1c3cc3f79afa0b5f5df6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="nesting-dsc-configurations"></a>Vnoření konfigurace DSC

Vnořené konfigurace (také nazývané složené configuration) je konfigurace, která je volána v rámci jiné konfigurace, jako by šlo prostředku.
Obě konfigurace musí být definovaný ve stejném souboru.

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

V tomto příkladu `FileConfig` přebírá dva povinné parametry, **CopyFrom –** a **CopyTo**, které se používají jako hodnoty **SourcePath** a  **Cílová_cesta** vlastnosti v `File` prostředků bloku. `NestedConfig` Konfigurace volání `FileConfig` jako by šlo prostředku.
Vlastnosti v `NestedConfig` bloku prostředků (**CopyFrom –** a **CopyTo**) jsou parametry `FileConfig` konfigurace.

## <a name="see-also"></a>Viz také

- [Složené prostředků – pomocí konfigurace DSC jako prostředek](authoringResourceComposite.md)


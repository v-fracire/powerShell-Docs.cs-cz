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
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="2b30c-103">Vnořování konfigurací DSC</span><span class="sxs-lookup"><span data-stu-id="2b30c-103">Nesting DSC configurations</span></span>

<span data-ttu-id="2b30c-104">Vnořené konfigurace (také nazývané složené configuration) je konfigurace, která je volána v rámci jiné konfigurace, jako by šlo prostředku.</span><span class="sxs-lookup"><span data-stu-id="2b30c-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="2b30c-105">Obě konfigurace musí být definován ve stejném souboru.</span><span class="sxs-lookup"><span data-stu-id="2b30c-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="2b30c-106">Podívejme se na jednoduchý příklad:</span><span class="sxs-lookup"><span data-stu-id="2b30c-106">Let's look at a simple example:</span></span>

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

<span data-ttu-id="2b30c-107">V tomto příkladu `FileConfig` používá dva povinné parametry **CopyFrom –** a **CopyTo**, které se používají jako hodnoty **SourcePath** a  **DestinationPath** vlastnosti `File` prostředků bloku.</span><span class="sxs-lookup"><span data-stu-id="2b30c-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span>
<span data-ttu-id="2b30c-108">`NestedConfig` Konfigurace volání `FileConfig` jako by šlo prostředku.</span><span class="sxs-lookup"><span data-stu-id="2b30c-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="2b30c-109">Vlastnosti `NestedConfig` bloku prostředků (**CopyFrom –** a **CopyTo**) jsou parametry `FileConfig` konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2b30c-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="2b30c-110">Viz také</span><span class="sxs-lookup"><span data-stu-id="2b30c-110">See Also</span></span>

- [<span data-ttu-id="2b30c-111">Složené prostředky – pomocí konfigurace DSC jako prostředek</span><span class="sxs-lookup"><span data-stu-id="2b30c-111">Composite resources--Using a DSC configuration as a resource</span></span>](../resources/authoringResourceComposite.md)
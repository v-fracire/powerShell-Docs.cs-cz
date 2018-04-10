---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Vnořování konfigurací
ms.openlocfilehash: 9c6dbce462f7481e5714039a95ae85f85be0072e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="1e8cf-103">Vnoření konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="1e8cf-103">Nesting DSC configurations</span></span>

<span data-ttu-id="1e8cf-104">Vnořené konfigurace (také nazývané složené configuration) je konfigurace, která je volána v rámci jiné konfigurace, jako by šlo prostředku.</span><span class="sxs-lookup"><span data-stu-id="1e8cf-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="1e8cf-105">Obě konfigurace musí být definovaný ve stejném souboru.</span><span class="sxs-lookup"><span data-stu-id="1e8cf-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="1e8cf-106">Podívejme se na jednoduchý příklad:</span><span class="sxs-lookup"><span data-stu-id="1e8cf-106">Let's look at a simple example:</span></span>

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

<span data-ttu-id="1e8cf-107">V tomto příkladu `FileConfig` přebírá dva povinné parametry, **CopyFrom –** a **CopyTo**, které se používají jako hodnoty **SourcePath** a  **Cílová_cesta** vlastnosti v `File` prostředků bloku.</span><span class="sxs-lookup"><span data-stu-id="1e8cf-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span>
<span data-ttu-id="1e8cf-108">`NestedConfig` Konfigurace volání `FileConfig` jako by šlo prostředku.</span><span class="sxs-lookup"><span data-stu-id="1e8cf-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="1e8cf-109">Vlastnosti v `NestedConfig` bloku prostředků (**CopyFrom –** a **CopyTo**) jsou parametry `FileConfig` konfigurace.</span><span class="sxs-lookup"><span data-stu-id="1e8cf-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="1e8cf-110">Viz také</span><span class="sxs-lookup"><span data-stu-id="1e8cf-110">See Also</span></span>

- [<span data-ttu-id="1e8cf-111">Složené prostředků – pomocí konfigurace DSC jako prostředek</span><span class="sxs-lookup"><span data-stu-id="1e8cf-111">Composite resources--Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
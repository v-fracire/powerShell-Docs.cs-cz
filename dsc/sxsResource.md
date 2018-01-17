---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Pomocí prostředků s více verzemi"
ms.openlocfilehash: 8bd8b1dab9418c6d8cf64cd682c527a7f039cdb4
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="using-resources-with-multiple-versions"></a><span data-ttu-id="f8d65-103">Pomocí prostředků s více verzemi</span><span class="sxs-lookup"><span data-stu-id="f8d65-103">Using resources with multiple versions</span></span>

> <span data-ttu-id="f8d65-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f8d65-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="f8d65-105">V prostředí PowerShell 5.0 prostředky DSC může mít několik verzí a verzí lze nainstalovat počítače-souběžného.</span><span class="sxs-lookup"><span data-stu-id="f8d65-105">In PowerShell 5.0, DSC resources can have multiple versions, and versions can be installed on a computer side-by-side.</span></span> <span data-ttu-id="f8d65-106">Tato možnost je implementovaná tak, že více verzí modul prostředků, které jsou obsaženy ve stejné složce modulu.</span><span class="sxs-lookup"><span data-stu-id="f8d65-106">This is implemented by having multiple versions of a resource module that are contained in the same module folder.</span></span>

## <a name="installing-multiple-resource-versions-side-by-side"></a><span data-ttu-id="f8d65-107">Instalace více prostředků verze-souběžného</span><span class="sxs-lookup"><span data-stu-id="f8d65-107">Installing multiple resource versions side-by-side</span></span>

<span data-ttu-id="f8d65-108">Můžete použít **MinimumVersion**, **MaximumVersion**, a **RequiredVersion** parametry [instalace modulu](https://technet.microsoft.com/en-us/library/dn807162.aspx) rutina k zadání která verze modulu k instalaci.</span><span class="sxs-lookup"><span data-stu-id="f8d65-108">You can use the **MinimumVersion**, **MaximumVersion**, and **RequiredVersion** parameters of the [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx) cmdlet to specify which version of a module to install.</span></span> <span data-ttu-id="f8d65-109">Volání metody **instalace modulu** bez zadání verze nainstaluje nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="f8d65-109">Calling **Install-Module** without specifying a version installs the most recent version.</span></span>

<span data-ttu-id="f8d65-110">Například existuje více verzí **xFailOverCluster** modulu, z nichž každý obsahuje **xCluster** odstraňovaného prostředku.</span><span class="sxs-lookup"><span data-stu-id="f8d65-110">For example, there are multiple versions of the **xFailOverCluster** module, each of which contains an **xCluster** resouce.</span></span> <span data-ttu-id="f8d65-111">Výsledek volání **instalace modulu** bez zadání verze číslo je následující:</span><span class="sxs-lookup"><span data-stu-id="f8d65-111">The result of calling **Install-Module** without specifying the version number is as follows:</span></span>

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

<span data-ttu-id="f8d65-112">Teď, když zavoláte **instalace modulu** znovu, ale zadat **RequiredVersion** z 1.1.0.0, výsledkem následující:</span><span class="sxs-lookup"><span data-stu-id="f8d65-112">Now, if you call **Install-Module** again, but specify a **RequiredVersion** of 1.1.0.0, it results in the following:</span></span>

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster -RequiredVersion 1.1
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a><span data-ttu-id="f8d65-113">Určení verze prostředků v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="f8d65-113">Specifying a resource version in a configuration</span></span>

<span data-ttu-id="f8d65-114">Pokud máte několik prostředků nainstalovat do počítače, musíte zadat verzi prostředku při použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f8d65-114">If you have multiple resources installed on a computer, you must specify the version of that resource when you use it in a configuration.</span></span> <span data-ttu-id="f8d65-115">To uděláte tak, že zadáte **ModuleVersion** parametr **Import DscResource** – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="f8d65-115">You do this by specifying the **ModuleVersion** parameter of the **Import-DscResource** keyword.</span></span> <span data-ttu-id="f8d65-116">Pokud se vám nepodaří zadejte verzi modul prostředků prostředků, které máte více než jeden nainstalovanou verzi, konfiguraci, vygeneruje se chyba.</span><span class="sxs-lookup"><span data-stu-id="f8d65-116">If you fail to specify the version of a resource module of a resource of which you have more than one version installed, the configuration generates an error.</span></span>

<span data-ttu-id="f8d65-117">Následující konfigurace ukazuje, jak určit verzi prostředek, který volání:</span><span class="sxs-lookup"><span data-stu-id="f8d65-117">The following configuration shows how to specify the version of the resource to call:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}     
```

><span data-ttu-id="f8d65-118">Poznámka: Verze modulu parametru importu DscResource není k dispozici v prostředí PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="f8d65-118">Note: The ModuleVersion parameter of Import-DscResource is not available in PowerShell 4.0.</span></span> <span data-ttu-id="f8d65-119">V prostředí PowerShell 4.0 můžete zadat verze modulu pomocí předání parametru ModuleName Import DscResource objekt specifikace modulu.</span><span class="sxs-lookup"><span data-stu-id="f8d65-119">In PowerShell 4.0, you can specify a module version by passing a module specification object to the ModuleName parameter of Import-DscResource.</span></span> <span data-ttu-id="f8d65-120">Objekt specifikace modulu je zatřiďovací tabulka, která obsahuje název modulu a RequiredVersion klíče.</span><span class="sxs-lookup"><span data-stu-id="f8d65-120">A module specification object is a hash table that contains ModuleName and RequiredVersion  keys.</span></span> <span data-ttu-id="f8d65-121">Příklad:</span><span class="sxs-lookup"><span data-stu-id="f8d65-121">For example:</span></span>

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}     
```

<span data-ttu-id="f8d65-122">To bude fungovat i v prostředí PowerShell 5.0, ale doporučuje se použít **ModuleVersion** parametr.</span><span class="sxs-lookup"><span data-stu-id="f8d65-122">This will also work in PowerShell 5.0, but it is recommended that you use the **ModuleVersion** parameter.</span></span>

## <a name="see-also"></a><span data-ttu-id="f8d65-123">Viz taky</span><span class="sxs-lookup"><span data-stu-id="f8d65-123">See also</span></span>
* [<span data-ttu-id="f8d65-124">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="f8d65-124">DSC Configurations</span></span>](configurations.md)
* [<span data-ttu-id="f8d65-125">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="f8d65-125">DSC Resources</span></span>](resources.md)


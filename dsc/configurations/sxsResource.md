---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Importovat konkrétní verzi nainstalovaného prostředků
ms.openlocfilehash: 5ed81e11aa67eb6590d958647f48a33b1b5f1c0e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403638"
---
# <a name="import-a-specific-version-of-an-installed-resource"></a><span data-ttu-id="eb922-103">Importovat konkrétní verzi nainstalovaného prostředků</span><span class="sxs-lookup"><span data-stu-id="eb922-103">Import a specific version of an installed resource</span></span>

> <span data-ttu-id="eb922-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="eb922-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="eb922-105">V Powershellu 5.0 může být samostatných verzí prostředků DSC nainstalovány v počítači vedle sebe.</span><span class="sxs-lookup"><span data-stu-id="eb922-105">In PowerShell 5.0, separate versions of DSC resources can be installed on a computer side by side.</span></span> <span data-ttu-id="eb922-106">Modul prostředků můžete ukládat samostatné verze prostředku ve verzi s názvem složky.</span><span class="sxs-lookup"><span data-stu-id="eb922-106">A resource module can store separate versions of a resource in version named folders.</span></span>

## <a name="installing-separate-resource-versions-side-by-side"></a><span data-ttu-id="eb922-107">Instalace samostatného prostředku verzí vedle sebe</span><span class="sxs-lookup"><span data-stu-id="eb922-107">Installing separate resource versions side by side</span></span>

<span data-ttu-id="eb922-108">Můžete použít **MinimumVersion**, **MaximumVersion**, a **RequiredVersion** parametry [Install-Module](/powershell/module/PowershellGet/Install-Module) rutina k zadání kterou verzi modulu pro instalaci.</span><span class="sxs-lookup"><span data-stu-id="eb922-108">You can use the **MinimumVersion**, **MaximumVersion**, and **RequiredVersion** parameters of the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to specify which version of a module to install.</span></span> <span data-ttu-id="eb922-109">Volání **Install-Module** bez zadání verze nainstaluje nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="eb922-109">Calling **Install-Module** without specifying a version installs the most recent version.</span></span>

<span data-ttu-id="eb922-110">Například existuje více verzí **xFailOverCluster** modulu, z nichž každý obsahuje **xCluster** prostředků.</span><span class="sxs-lookup"><span data-stu-id="eb922-110">For example, there are multiple versions of the **xFailOverCluster** module, each of which contains an **xCluster** resource.</span></span> <span data-ttu-id="eb922-111">Volání **Install-Module** bez zadání verze číslo nainstaluje nejnovější verzi modulu.</span><span class="sxs-lookup"><span data-stu-id="eb922-111">Calling **Install-Module** without specifying the version number installs the most recent version of the module.</span></span>

```powershell
PS> Install-Module xFailOverCluster
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

<span data-ttu-id="eb922-112">Pokud chcete nainstalovat konkrétní verzi modulu, zadejte **RequiredVersion** z 1.1.0.0.</span><span class="sxs-lookup"><span data-stu-id="eb922-112">To install a specific version of a module, specify a **RequiredVersion** of 1.1.0.0.</span></span> <span data-ttu-id="eb922-113">Tím se nainstaluje zadaná verze s nainstalovanou verzí.</span><span class="sxs-lookup"><span data-stu-id="eb922-113">This installs the specified version side by side with the installed version.</span></span>

```powershell
PS> Install-Module xFailOverCluster -RequiredVersion 1.1
```

<span data-ttu-id="eb922-114">Nyní, uvidíte oba uvedenou verzi modulu při použití `Get-DSCResource`.</span><span class="sxs-lookup"><span data-stu-id="eb922-114">Now, you see both version of the module listed when you use `Get-DSCResource`.</span></span>

```powershell
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a><span data-ttu-id="eb922-115">Určení verze prostředků v konfiguraci</span><span class="sxs-lookup"><span data-stu-id="eb922-115">Specifying a resource version in a configuration</span></span>

<span data-ttu-id="eb922-116">Pokud máte samostatný prostředek verze nainstalované na počítači, musíte zadat verzi tohoto prostředku, při použití v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="eb922-116">If you have separate resource versions installed on a computer, you must specify the version of that resource when you use it in a configuration.</span></span> <span data-ttu-id="eb922-117">To provedete tak, že zadáte **ModuleVersion** parametr **Import-DscResource** – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="eb922-117">You do this by specifying the **ModuleVersion** parameter of the **Import-DscResource** keyword.</span></span> <span data-ttu-id="eb922-118">Pokud k určení verze modulu prostředků prostředku, které mají více než jedna verze nainstalovaná, kterou konfigurace generuje chybu.</span><span class="sxs-lookup"><span data-stu-id="eb922-118">If you fail to specify the version of a resource module of a resource of which you have more than one version installed, the configuration generates an error.</span></span>

<span data-ttu-id="eb922-119">Následující konfigurace ukazuje, jak určit verzi prostředku pro volání:</span><span class="sxs-lookup"><span data-stu-id="eb922-119">The following configuration shows how to specify the version of the resource to call:</span></span>

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

><span data-ttu-id="eb922-120">Poznámka: Parametr verze modulu Import-DscResource není k dispozici v Powershellu 4.0.</span><span class="sxs-lookup"><span data-stu-id="eb922-120">Note: The ModuleVersion parameter of Import-DscResource is not available in PowerShell 4.0.</span></span> <span data-ttu-id="eb922-121">V Powershellu 4.0 můžete určit verzi modulu předáním objektu modulu specifikace parametru ModuleName Import-DscResource.</span><span class="sxs-lookup"><span data-stu-id="eb922-121">In PowerShell 4.0, you can specify a module version by passing a module specification object to the ModuleName parameter of Import-DscResource.</span></span> <span data-ttu-id="eb922-122">Objekt modulu specifikace je zatřiďovací tabulku, která obsahuje název modulu a RequiredVersion klíče.</span><span class="sxs-lookup"><span data-stu-id="eb922-122">A module specification object is a hash table that contains ModuleName and RequiredVersion  keys.</span></span> <span data-ttu-id="eb922-123">Příklad:</span><span class="sxs-lookup"><span data-stu-id="eb922-123">For example:</span></span>

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

<span data-ttu-id="eb922-124">To bude fungovat i v Powershellu 5.0, ale doporučuje se, že používáte **ModuleVersion** parametru.</span><span class="sxs-lookup"><span data-stu-id="eb922-124">This will also work in PowerShell 5.0, but it is recommended that you use the **ModuleVersion** parameter.</span></span>

## <a name="see-also"></a><span data-ttu-id="eb922-125">Viz taky</span><span class="sxs-lookup"><span data-stu-id="eb922-125">See also</span></span>

- [<span data-ttu-id="eb922-126">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="eb922-126">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="eb922-127">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="eb922-127">DSC Resources</span></span>](../resources/resources.md)

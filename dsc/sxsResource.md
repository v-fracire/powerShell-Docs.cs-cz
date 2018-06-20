---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Použití různých verzí prostředků
ms.openlocfilehash: 6400d6506106657ba28fa1f9c83d9f8ee1c93ba3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187006"
---
# <a name="using-resources-with-multiple-versions"></a>Použití různých verzí prostředků

> Platí pro: Prostředí Windows PowerShell 5.0

V prostředí PowerShell 5.0 prostředky DSC může mít několik verzí a verzí lze nainstalovat počítače-souběžného. Tato možnost je implementovaná tak, že více verzí modul prostředků, které jsou obsaženy ve stejné složce modulu.

## <a name="installing-multiple-resource-versions-side-by-side"></a>Instalace více prostředků verze-souběžného

Můžete použít **MinimumVersion**, **MaximumVersion**, a **RequiredVersion** parametry [instalace modulu](https://technet.microsoft.com/library/dn807162.aspx) rutina k zadání která verze modulu k instalaci. Volání metody **instalace modulu** bez zadání verze nainstaluje nejnovější verzi.

Například existuje více verzí **xFailOverCluster** modulu, z nichž každý obsahuje **xCluster** odstraňovaného prostředku. Výsledek volání **instalace modulu** bez zadání verze číslo je následující:

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

Teď, když zavoláte **instalace modulu** znovu, ale zadat **RequiredVersion** z 1.1.0.0, výsledkem následující:

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster -RequiredVersion 1.1
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a>Určení verze prostředků v konfiguraci

Pokud máte několik prostředků nainstalovat do počítače, musíte zadat verzi prostředku při použití v konfiguraci. To uděláte tak, že zadáte **ModuleVersion** parametr **Import DscResource** – klíčové slovo. Pokud se vám nepodaří zadejte verzi modul prostředků prostředků, které máte více než jeden nainstalovanou verzi, konfiguraci, vygeneruje se chyba.

Následující konfigurace ukazuje, jak určit verzi prostředek, který volání:

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

>Poznámka: Verze modulu parametru importu DscResource není k dispozici v prostředí PowerShell 4.0. V prostředí PowerShell 4.0 můžete zadat verze modulu pomocí předání parametru ModuleName Import DscResource objekt specifikace modulu. Objekt specifikace modulu je zatřiďovací tabulka, která obsahuje název modulu a RequiredVersion klíče. Příklad:

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

To bude fungovat i v prostředí PowerShell 5.0, ale doporučuje se použít **ModuleVersion** parametr.

## <a name="see-also"></a>Viz taky
* [Konfigurace DSC](configurations.md)
* [Prostředky DSC](resources.md)
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
# <a name="import-a-specific-version-of-an-installed-resource"></a>Importovat konkrétní verzi nainstalovaného prostředků

> Platí pro: Windows PowerShell 5.0

V Powershellu 5.0 může být samostatných verzí prostředků DSC nainstalovány v počítači vedle sebe. Modul prostředků můžete ukládat samostatné verze prostředku ve verzi s názvem složky.

## <a name="installing-separate-resource-versions-side-by-side"></a>Instalace samostatného prostředku verzí vedle sebe

Můžete použít **MinimumVersion**, **MaximumVersion**, a **RequiredVersion** parametry [Install-Module](/powershell/module/PowershellGet/Install-Module) rutina k zadání kterou verzi modulu pro instalaci. Volání **Install-Module** bez zadání verze nainstaluje nejnovější verzi.

Například existuje více verzí **xFailOverCluster** modulu, z nichž každý obsahuje **xCluster** prostředků. Volání **Install-Module** bez zadání verze číslo nainstaluje nejnovější verzi modulu.

```powershell
PS> Install-Module xFailOverCluster
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

Pokud chcete nainstalovat konkrétní verzi modulu, zadejte **RequiredVersion** z 1.1.0.0. Tím se nainstaluje zadaná verze s nainstalovanou verzí.

```powershell
PS> Install-Module xFailOverCluster -RequiredVersion 1.1
```

Nyní, uvidíte oba uvedenou verzi modulu při použití `Get-DSCResource`.

```powershell
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a>Určení verze prostředků v konfiguraci

Pokud máte samostatný prostředek verze nainstalované na počítači, musíte zadat verzi tohoto prostředku, při použití v konfiguraci. To provedete tak, že zadáte **ModuleVersion** parametr **Import-DscResource** – klíčové slovo. Pokud k určení verze modulu prostředků prostředku, které mají více než jedna verze nainstalovaná, kterou konfigurace generuje chybu.

Následující konfigurace ukazuje, jak určit verzi prostředku pro volání:

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

>Poznámka: Parametr verze modulu Import-DscResource není k dispozici v Powershellu 4.0. V Powershellu 4.0 můžete určit verzi modulu předáním objektu modulu specifikace parametru ModuleName Import-DscResource. Objekt modulu specifikace je zatřiďovací tabulku, která obsahuje název modulu a RequiredVersion klíče. Příklad:

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

To bude fungovat i v Powershellu 5.0, ale doporučuje se, že používáte **ModuleVersion** parametru.

## <a name="see-also"></a>Viz taky

- [Konfigurace DSC](configurations.md)
- [Prostředky DSC](../resources/resources.md)

---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Určení závislostí mezi uzly
ms.openlocfilehash: 1bdfbd9f8a94809d6bf410eff525e1c877fb6aad
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403636"
---
# <a name="specifying-cross-node-dependencies"></a>Určení závislostí mezi uzly

> Platí pro: Windows PowerShell 5.0

DSC poskytuje zvláštní prostředky **WaitForAll**, **WaitForAny**, a **WaitForSome** , který lze použít v konfiguracích postup určení závislostí pro konfigurací na jiné uzly. Chování těchto prostředků je následující:

- **WaitForAll**: Úspěšná, pokud zadaný prostředek je v požadovaném stavu na všechny cílové uzly podle **NodeName** vlastnost.
- **WaitForAny**: Úspěšná, pokud zadaný prostředek je v požadovaném stavu na nejméně jednom cílové uzly podle **NodeName** vlastnost.
- **WaitForSome**: Určuje **NodeCount** vlastnost kromě **NodeName** vlastnost. Prostředek proběhne úspěšně, pokud prostředek je v požadovaném stavu na minimální počet uzlů (určená **NodeCount**) definované **NodeName** vlastnost.

## <a name="syntax"></a>Syntaxe

**WaitForAll** a **WaitForAny** prostředky sdílet stejnou syntaxi. Nahraďte \<ResourceType\> v níže uvedeném příkladu s jedním **WaitForAny** nebo **WaitForAll**.
Podobně jako **DependsOn** – klíčové slovo, budete muset formátování názvu jako "ResourceName [ResourceType]". Pokud prostředek patří do samostatné [konfigurace](configurations.md), zahrnout **ConfigurationName** do formátovaného řetězce "[ResourceType] ResourceName:: [ConfigurationName]:: [ConfigurationName]". **NodeName** je počítač nebo uzlu, na kterém by měl čekat aktuální prostředek.

```
<ResourceType> [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential]]
    [ RetryCount = [Uint32] ]
    [ RetryIntervalSec = [Uint64] ]
    [ ThrottleLimit = [Uint32]]
}
```

**WaitForSome** prostředek má podobné syntaxi v příkladu výše, ale přidá **NodeCount** klíč. **NodeCount** označuje aktuální prostředek by měl čekat na počtu uzlů.

```
WaitForSome [String] #ResourceName
{
    NodeCount = [UInt32]
    NodeName = [string[]]
    ResourceName = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
    [RetryCount = [UInt32]]
    [RetryIntervalSec = [UInt64]]
    [ThrottleLimit = [UInt32]]
}
```

Všechny **WaitForXXXX** sdílet následující syntaxe klíče.

|  Vlastnost |  Popis || RetryIntervalSec | Počet sekund, než to zkusíte znovu. Minimální hodnota je 1. | | RetryCount | Maximální počet pokusů o zopakování. | | ThrottleLimit | Počet počítačů současně připojit. Výchozí hodnota je `New-CimSession` výchozí. | | DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Další informace najdete v tématu [DependsOn](resource-depends-on.md)|| PsDscRunAsCredential | Zobrazit [DSC pomocí uživatelských přihlašovacích údajů](./runAsUser.md) |


## <a name="using-waitforxxxx-resources"></a>Použití WaitForXXXX prostředků

Každý **WaitForXXXX** prostředků čeká na dokončení pro zadaný uzel zadané prostředky. Jiné prostředky ve stejné konfigurace lze poté *závisí na* **WaitForXXXX** prostředků pomocí **DependsOn** klíč.

Například v následující konfiguraci cílový uzel je čekání **xADDomain** prostředků k dokončení **MyDC** uzel s maximálně 30 opakování, v 15sekundových intervalech, než Cílový uzel může připojit k doméně.

```powershell
Configuration JoinDomain
{
    Import-DscResource -Module xComputerManagement, xActiveDirectory

    Node myDC
    {
        WindowsFeature InstallAD
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xADDomain NewDomain
        {
            DomainName = 'Contoso.com'
            DomainAdministratorCredential = (Get-Credential)
            SafemodeAdministratorPassword = (Get-Credential)
            DatabasePath = "C:\Windows\NTDS"
            LogPath = "C:\Windows\NTDS"
            SysvolPath = "C:\Windows\Sysvol"
        }
    }

    Node myDomainJoinedServer
    {
        WaitForAll DC
        {
            ResourceName      = '[xADDomain]NewDomain'
            NodeName          = 'MyDC'
            RetryIntervalSec  = 15
            RetryCount        = 30
        }

        xComputer JoinDomain
        {
            Name             = 'myPC'
            DomainName       = 'Contoso.com'
            Credential       = (Get-Credential)
            DependsOn        ='[WaitForAll]DC'
        }
    }
}
```

Při kompilaci konfigurace jsou generovány dva soubory ".mof". Oba soubory ".mof" platí pro cílové uzly pomocí [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny

>**Poznámka:** Ve výchozím nastavení WaitForXXX prostředky zkuste jednou a dojde k selhání. I když to není potřeba, obvykle můžete zadat **RetryCount** a **RetryIntervalSec**.

## <a name="see-also"></a>Viz také

- [Konfigurace DSC](configurations.md)
- [Využívat závislosti prostředků](resource-depends-on.md)
- [Prostředky DSC](../resources/resources.md)
- [Konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md)

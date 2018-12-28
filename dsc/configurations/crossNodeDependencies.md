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
# <a name="specifying-cross-node-dependencies"></a><span data-ttu-id="076df-103">Určení závislostí mezi uzly</span><span class="sxs-lookup"><span data-stu-id="076df-103">Specifying cross-node dependencies</span></span>

> <span data-ttu-id="076df-104">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="076df-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="076df-105">DSC poskytuje zvláštní prostředky **WaitForAll**, **WaitForAny**, a **WaitForSome** , který lze použít v konfiguracích postup určení závislostí pro konfigurací na jiné uzly.</span><span class="sxs-lookup"><span data-stu-id="076df-105">DSC provides special resources, **WaitForAll**, **WaitForAny**, and **WaitForSome** that can be used in configurations to specify dependencies on configurations on other nodes.</span></span> <span data-ttu-id="076df-106">Chování těchto prostředků je následující:</span><span class="sxs-lookup"><span data-stu-id="076df-106">The behavior of these resources is as follows:</span></span>

- <span data-ttu-id="076df-107">**WaitForAll**: Úspěšná, pokud zadaný prostředek je v požadovaném stavu na všechny cílové uzly podle **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="076df-107">**WaitForAll**: Succeeds if the specified resource is in the desired state on all target nodes defined in the **NodeName** property.</span></span>
- <span data-ttu-id="076df-108">**WaitForAny**: Úspěšná, pokud zadaný prostředek je v požadovaném stavu na nejméně jednom cílové uzly podle **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="076df-108">**WaitForAny**: Succeeds if the specified resource is in the desired state on at least one of the target nodes defined in the **NodeName** property.</span></span>
- <span data-ttu-id="076df-109">**WaitForSome**: Určuje **NodeCount** vlastnost kromě **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="076df-109">**WaitForSome**: Specifies a **NodeCount** property in addition to a **NodeName** property.</span></span> <span data-ttu-id="076df-110">Prostředek proběhne úspěšně, pokud prostředek je v požadovaném stavu na minimální počet uzlů (určená **NodeCount**) definované **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="076df-110">The resource succeeds if the resource is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>

## <a name="syntax"></a><span data-ttu-id="076df-111">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="076df-111">Syntax</span></span>

<span data-ttu-id="076df-112">**WaitForAll** a **WaitForAny** prostředky sdílet stejnou syntaxi.</span><span class="sxs-lookup"><span data-stu-id="076df-112">The **WaitForAll** and **WaitForAny** resources share the same syntax.</span></span> <span data-ttu-id="076df-113">Nahraďte \<ResourceType\> v níže uvedeném příkladu s jedním **WaitForAny** nebo **WaitForAll**.</span><span class="sxs-lookup"><span data-stu-id="076df-113">Replace \<ResourceType\> in the example below with either **WaitForAny** or **WaitForAll**.</span></span>
<span data-ttu-id="076df-114">Podobně jako **DependsOn** – klíčové slovo, budete muset formátování názvu jako "ResourceName [ResourceType]".</span><span class="sxs-lookup"><span data-stu-id="076df-114">Like the **DependsOn** keyword, you will need to format the name as "[ResourceType]ResourceName".</span></span> <span data-ttu-id="076df-115">Pokud prostředek patří do samostatné [konfigurace](configurations.md), zahrnout **ConfigurationName** do formátovaného řetězce "[ResourceType] ResourceName:: [ConfigurationName]:: [ConfigurationName]".</span><span class="sxs-lookup"><span data-stu-id="076df-115">If the resource belongs to a separate [Configuration](configurations.md), include the **ConfigurationName** in the formatted string "[ResourceType]ResourceName::[ConfigurationName]::[ConfigurationName]".</span></span> <span data-ttu-id="076df-116">**NodeName** je počítač nebo uzlu, na kterém by měl čekat aktuální prostředek.</span><span class="sxs-lookup"><span data-stu-id="076df-116">The **NodeName** is the computer, or Node, on which the current resource should wait.</span></span>

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

<span data-ttu-id="076df-117">**WaitForSome** prostředek má podobné syntaxi v příkladu výše, ale přidá **NodeCount** klíč.</span><span class="sxs-lookup"><span data-stu-id="076df-117">The **WaitForSome** resource has a similar syntax to the example above, but adds the **NodeCount** key.</span></span> <span data-ttu-id="076df-118">**NodeCount** označuje aktuální prostředek by měl čekat na počtu uzlů.</span><span class="sxs-lookup"><span data-stu-id="076df-118">The **NodeCount** indicates how many Nodes the current resource should wait on.</span></span>

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

<span data-ttu-id="076df-119">Všechny **WaitForXXXX** sdílet následující syntaxe klíče.</span><span class="sxs-lookup"><span data-stu-id="076df-119">All **WaitForXXXX** share the following syntax keys.</span></span>

<span data-ttu-id="076df-120">|  Vlastnost |  Popis || RetryIntervalSec | Počet sekund, než to zkusíte znovu.</span><span class="sxs-lookup"><span data-stu-id="076df-120">|  Property  |  Description   | | RetryIntervalSec| The number of seconds before retrying.</span></span> <span data-ttu-id="076df-121">Minimální hodnota je 1. | | RetryCount | Maximální počet pokusů o zopakování. | | ThrottleLimit | Počet počítačů současně připojit.</span><span class="sxs-lookup"><span data-stu-id="076df-121">Minimum is 1.| | RetryCount| The maximum number of times to retry.| | ThrottleLimit| Number of machines to connect simultaneously.</span></span> <span data-ttu-id="076df-122">Výchozí hodnota je `New-CimSession` výchozí. | | DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="076df-122">Default is `New-CimSession` default.| | DependsOn | Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="076df-123">Další informace najdete v tématu [DependsOn](resource-depends-on.md)|| PsDscRunAsCredential | Zobrazit [DSC pomocí uživatelských přihlašovacích údajů](./runAsUser.md) |</span><span class="sxs-lookup"><span data-stu-id="076df-123">For more information, see [DependsOn](resource-depends-on.md)| | PsDscRunAsCredential | See [Using DSC with User Credentials](./runAsUser.md) |</span></span>


## <a name="using-waitforxxxx-resources"></a><span data-ttu-id="076df-124">Použití WaitForXXXX prostředků</span><span class="sxs-lookup"><span data-stu-id="076df-124">Using WaitForXXXX resources</span></span>

<span data-ttu-id="076df-125">Každý **WaitForXXXX** prostředků čeká na dokončení pro zadaný uzel zadané prostředky.</span><span class="sxs-lookup"><span data-stu-id="076df-125">Each **WaitForXXXX** resource waits for the specified resources to complete on the specified Node.</span></span> <span data-ttu-id="076df-126">Jiné prostředky ve stejné konfigurace lze poté *závisí na* **WaitForXXXX** prostředků pomocí **DependsOn** klíč.</span><span class="sxs-lookup"><span data-stu-id="076df-126">Other resources in the same Configuration can then *depend on* the **WaitForXXXX** resource using the **DependsOn** key.</span></span>

<span data-ttu-id="076df-127">Například v následující konfiguraci cílový uzel je čekání **xADDomain** prostředků k dokončení **MyDC** uzel s maximálně 30 opakování, v 15sekundových intervalech, než Cílový uzel může připojit k doméně.</span><span class="sxs-lookup"><span data-stu-id="076df-127">For example, in the following configuration, the target node is waiting for the **xADDomain** resource to finish on the **MyDC** node with maximum number of 30 retries, at 15-second intervals, before the target node can join the domain.</span></span>

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

<span data-ttu-id="076df-128">Při kompilaci konfigurace jsou generovány dva soubory ".mof".</span><span class="sxs-lookup"><span data-stu-id="076df-128">When you compile the Configuration, two ".mof" files are generated.</span></span> <span data-ttu-id="076df-129">Oba soubory ".mof" platí pro cílové uzly pomocí [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny</span><span class="sxs-lookup"><span data-stu-id="076df-129">Apply both ".mof" files to the target Nodes using the [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet</span></span>

><span data-ttu-id="076df-130">**Poznámka:** Ve výchozím nastavení WaitForXXX prostředky zkuste jednou a dojde k selhání.</span><span class="sxs-lookup"><span data-stu-id="076df-130">**Note:** By default the WaitForXXX resources try one time and then fail.</span></span> <span data-ttu-id="076df-131">I když to není potřeba, obvykle můžete zadat **RetryCount** a **RetryIntervalSec**.</span><span class="sxs-lookup"><span data-stu-id="076df-131">Although it is not required, you will typically want to specify a **RetryCount** and **RetryIntervalSec**.</span></span>

## <a name="see-also"></a><span data-ttu-id="076df-132">Viz také</span><span class="sxs-lookup"><span data-stu-id="076df-132">See Also</span></span>

- [<span data-ttu-id="076df-133">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="076df-133">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="076df-134">Využívat závislosti prostředků</span><span class="sxs-lookup"><span data-stu-id="076df-134">Use Resource Dependencies</span></span>](resource-depends-on.md)
- [<span data-ttu-id="076df-135">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="076df-135">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="076df-136">Konfigurace Local Configuration Manageru</span><span class="sxs-lookup"><span data-stu-id="076df-136">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)

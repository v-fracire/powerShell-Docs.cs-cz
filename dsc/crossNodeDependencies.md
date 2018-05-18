---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Určení závislostí mezi uzly
ms.openlocfilehash: c1802d6baa1f2b3449603e0374a83e213abf598e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="specifying-cross-node-dependencies"></a><span data-ttu-id="1d296-103">Určení závislostí mezi uzly</span><span class="sxs-lookup"><span data-stu-id="1d296-103">Specifying cross-node dependencies</span></span>

> <span data-ttu-id="1d296-104">Platí pro: Prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1d296-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="1d296-105">DSC poskytuje speciální prostředky **WaitForAll**, **WaitForAny**, a **WaitForSome** který lze použít v konfiguracích k určení závislostí na konfigurace na dalších uzly.</span><span class="sxs-lookup"><span data-stu-id="1d296-105">DSC provides special resources, **WaitForAll**, **WaitForAny**, and **WaitForSome** that can be used in configurations to specify dependencies on configurations on other nodes.</span></span> <span data-ttu-id="1d296-106">Chování těchto prostředků je následující:</span><span class="sxs-lookup"><span data-stu-id="1d296-106">The behavior of these resources is as follows:</span></span>

* <span data-ttu-id="1d296-107">**WaitForAll**: úspěšná, pokud je zadaný prostředek s požadovaným stavem na všechny cílové uzly, které jsou definované v **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1d296-107">**WaitForAll**: Succeeds if the specified resource is in the desired state on all target nodes defined in the **NodeName** property.</span></span>
* <span data-ttu-id="1d296-108">**WaitForAny**: úspěšná, pokud je zadaný prostředek s požadovaným stavem na alespoň jeden z cílových uzlů definované v **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1d296-108">**WaitForAny**: Succeeds if the specified resource is in the desired state on at least one of the target nodes defined in the **NodeName** property.</span></span>
* <span data-ttu-id="1d296-109">**WaitForSome**: Určuje **NodeCount** vlastnost kromě **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1d296-109">**WaitForSome**: Specifies a **NodeCount** property in addition to a **NodeName** property.</span></span> <span data-ttu-id="1d296-110">Prostředek úspěšné, pokud je v požadovaném stavu na minimální počet uzlů (zadáno v **NodeCount**) definované **NodeName** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="1d296-110">The resource succeeds if the resource is in the desired state on a minimum number of nodes (specified by **NodeCount**) defined by the **NodeName** property.</span></span>

## <a name="using-waitforxxxx-resources"></a><span data-ttu-id="1d296-111">Pomocí WaitForXXXX prostředků</span><span class="sxs-lookup"><span data-stu-id="1d296-111">Using WaitForXXXX resources</span></span>

<span data-ttu-id="1d296-112">Použít **WaitForXXXX** prostředky, vytvořit blok prostředků tohoto typu prostředků, které určuje prostředek DSC a uzly pro čekání.</span><span class="sxs-lookup"><span data-stu-id="1d296-112">To use the **WaitForXXXX** resources, you create a resource block of that resource type that specifies the DSC resource and node(s) to wait for.</span></span> <span data-ttu-id="1d296-113">Pak použijete **DependsOn** blokuje vlastnost v jiných prostředků ve vaší konfiguraci čekat podmínky uvedené v **WaitForXXXX** uzlu proběhla úspěšně.</span><span class="sxs-lookup"><span data-stu-id="1d296-113">You then use the **DependsOn** property in any other resource blocks in your configuration to wait for the conditions specified in the **WaitForXXXX** node to succeed.</span></span>

<span data-ttu-id="1d296-114">Například v následující konfiguraci cílový uzel čeká **xADDomain** prostředků na dokončení na **MyDC** uzel s maximálně 30 opakování, v intervalech 15 sekund, než Cílový uzel můžete připojit k doméně.</span><span class="sxs-lookup"><span data-stu-id="1d296-114">For example, in the following configuration, the target node is waiting for the **xADDomain** resource to finish on the **MyDC** node with maximum number of 30 retries, at 15-second intervals, before the target node can join the domain.</span></span>

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

><span data-ttu-id="1d296-115">**Poznámka:** ve výchozím nastavení WaitForXXX prostředky zkuste jednou a pak neúspěšné.</span><span class="sxs-lookup"><span data-stu-id="1d296-115">**Note:** By default the WaitForXXX resources try one time and then fail.</span></span> <span data-ttu-id="1d296-116">I když to není nutné, obvykle můžete zadat interval opakování a počet.</span><span class="sxs-lookup"><span data-stu-id="1d296-116">Although it is not required, you will typically want to specify a retry interval and count.</span></span>

## <a name="see-also"></a><span data-ttu-id="1d296-117">Viz také</span><span class="sxs-lookup"><span data-stu-id="1d296-117">See Also</span></span>
* [<span data-ttu-id="1d296-118">Konfigurace DSC</span><span class="sxs-lookup"><span data-stu-id="1d296-118">DSC Configurations</span></span>](configurations.md)
* [<span data-ttu-id="1d296-119">Prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="1d296-119">DSC Resources</span></span>](resources.md)
* [<span data-ttu-id="1d296-120">Konfigurace správce místní konfigurace</span><span class="sxs-lookup"><span data-stu-id="1d296-120">Configuring The Local Configuration Manager</span></span>](metaConfig.md)
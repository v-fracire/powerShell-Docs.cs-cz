---
ms.date: 03/15/2018
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Použití platformy DSC v Microsoft Azure
ms.openlocfilehash: 5b0d577e1fecdeac38c2c5f8e955a2d23b1eb707
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="using-dsc-on-microsoft-azure"></a><span data-ttu-id="db0fd-103">Použití platformy DSC v Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="db0fd-103">Using DSC on Microsoft Azure</span></span>

<span data-ttu-id="db0fd-104">Požadovaná stav konfigurace (DSC) se podporuje v Microsoft Azure prostřednictvím [obslužná rutina rozšíření konfigurace požadovaného stavu Azure](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) a pomocí [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span><span class="sxs-lookup"><span data-stu-id="db0fd-104">Desired State Configuration (DSC) is supported in Microsoft Azure through the [Azure Desired State Configuration extension handler](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) and through [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span></span>

## <a name="azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="db0fd-105">Stavu Azure požadovaná konfigurace rozšíření obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="db0fd-105">Azure Desired State Configuration extension handler</span></span>

<span data-ttu-id="db0fd-106">Rozšíření Azure DSC umožňuje virtuální počítače hostované v Microsoft Azure a spravovat pomocí DSC.</span><span class="sxs-lookup"><span data-stu-id="db0fd-106">The Azure DSC extension allows VMs hosted in Microsoft Azure to be managed with DSC.</span></span>
<span data-ttu-id="db0fd-107">Další informace najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="db0fd-107">For more information, see the following topics:</span></span>

- [<span data-ttu-id="db0fd-108">Stavu Azure požadovaná konfigurace rozšíření obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="db0fd-108">Azure Desired State Configuration extension handler</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview)
- [<span data-ttu-id="db0fd-109">Windows VMSS a konfigurace požadovaného stavu pomocí šablon Azure Resource Manageru</span><span class="sxs-lookup"><span data-stu-id="db0fd-109">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-template)
- [<span data-ttu-id="db0fd-110">Předání přihlašovacích údajů k obslužné rutině rozšíření Azure DSC</span><span class="sxs-lookup"><span data-stu-id="db0fd-110">Passing credentials to the Azure DSC extension handler</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-credentials)
- [<span data-ttu-id="db0fd-111">Historie stavu Azure požadovaná konfigurace rozšíření</span><span class="sxs-lookup"><span data-stu-id="db0fd-111">Azure Desired State Configuration extension history</span></span>](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a><span data-ttu-id="db0fd-112">Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="db0fd-112">Azure Automation DSC</span></span>

<span data-ttu-id="db0fd-113">[Služba Azure Automation](https://azure.microsoft.com/services/automation/) vám umožní spravovat konfigurace DSC, prostředky a spravované uzly z v rámci Azure.</span><span class="sxs-lookup"><span data-stu-id="db0fd-113">The [Azure Automation service](https://azure.microsoft.com/services/automation/) allows you to manage DSC configurations, resources, and managed nodes from within Azure.</span></span> <span data-ttu-id="db0fd-114">Další informace najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="db0fd-114">For more information, see the following topics:</span></span>

- [<span data-ttu-id="db0fd-115">Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="db0fd-115">Azure Automation DSC</span></span>](/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="db0fd-116">Začínáme s Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="db0fd-116">Getting started with Azure Automation DSC</span></span>](/azure/automation/automation-dsc-getting-started)
- [<span data-ttu-id="db0fd-117">Registrace počítačů pro správu Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="db0fd-117">Onboarding machines for management by Azure Automation DSC</span></span>](/azure/automation/automation-dsc-onboarding)
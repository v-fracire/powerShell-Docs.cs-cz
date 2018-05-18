---
ms.date: 03/15/2018
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Použití platformy DSC v Microsoft Azure
ms.openlocfilehash: d35488c3f66895e930eaa84360f3d3ec9d74e9c7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="using-dsc-on-microsoft-azure"></a><span data-ttu-id="ea2ae-103">Použití platformy DSC v Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ea2ae-103">Using DSC on Microsoft Azure</span></span>

<span data-ttu-id="ea2ae-104">Požadovaná stav konfigurace (DSC) se podporuje v Microsoft Azure prostřednictvím [obslužná rutina rozšíření konfigurace požadovaného stavu Azure](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) a pomocí [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span><span class="sxs-lookup"><span data-stu-id="ea2ae-104">Desired State Configuration (DSC) is supported in Microsoft Azure through the [Azure Desired State Configuration extension handler](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) and through [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span></span>

## <a name="azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="ea2ae-105">Stavu Azure požadovaná konfigurace rozšíření obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="ea2ae-105">Azure Desired State Configuration extension handler</span></span>

<span data-ttu-id="ea2ae-106">Rozšíření Azure DSC umožňuje virtuální počítače hostované v Microsoft Azure a spravovat pomocí DSC.</span><span class="sxs-lookup"><span data-stu-id="ea2ae-106">The Azure DSC extension allows VMs hosted in Microsoft Azure to be managed with DSC.</span></span>
<span data-ttu-id="ea2ae-107">Další informace najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="ea2ae-107">For more information, see the following topics:</span></span>

- [<span data-ttu-id="ea2ae-108">Stavu Azure požadovaná konfigurace rozšíření obslužné rutiny</span><span class="sxs-lookup"><span data-stu-id="ea2ae-108">Azure Desired State Configuration extension handler</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview)
- [<span data-ttu-id="ea2ae-109">Windows VMSS a konfigurace požadovaného stavu pomocí šablon Azure Resource Manageru</span><span class="sxs-lookup"><span data-stu-id="ea2ae-109">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-template)
- [<span data-ttu-id="ea2ae-110">Předání přihlašovacích údajů k obslužné rutině rozšíření Azure DSC</span><span class="sxs-lookup"><span data-stu-id="ea2ae-110">Passing credentials to the Azure DSC extension handler</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-credentials)
- [<span data-ttu-id="ea2ae-111">Historie stavu Azure požadovaná konfigurace rozšíření</span><span class="sxs-lookup"><span data-stu-id="ea2ae-111">Azure Desired State Configuration extension history</span></span>](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a><span data-ttu-id="ea2ae-112">Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ea2ae-112">Azure Automation DSC</span></span>

<span data-ttu-id="ea2ae-113">[Služba Azure Automation](https://azure.microsoft.com/services/automation/) vám umožní spravovat konfigurace DSC, prostředky a spravované uzly z v rámci Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ae-113">The [Azure Automation service](https://azure.microsoft.com/services/automation/) allows you to manage DSC configurations, resources, and managed nodes from within Azure.</span></span> <span data-ttu-id="ea2ae-114">Další informace najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="ea2ae-114">For more information, see the following topics:</span></span>

- [<span data-ttu-id="ea2ae-115">Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ea2ae-115">Azure Automation DSC</span></span>](/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="ea2ae-116">Začínáme s Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ea2ae-116">Getting started with Azure Automation DSC</span></span>](/azure/automation/automation-dsc-getting-started)
- [<span data-ttu-id="ea2ae-117">Registrace počítačů pro správu Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="ea2ae-117">Onboarding machines for management by Azure Automation DSC</span></span>](/azure/automation/automation-dsc-onboarding)
---
ms.date: 03/15/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Použití platformy DSC v Microsoft Azure
ms.openlocfilehash: 54a317a415ff12c3d270897f414cba88716f0728
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403626"
---
# <a name="using-dsc-on-microsoft-azure"></a><span data-ttu-id="abcc1-103">Použití platformy DSC v Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="abcc1-103">Using DSC on Microsoft Azure</span></span>

<span data-ttu-id="abcc1-104">Desired State Configuration (DSC) se podporuje v Microsoft Azure prostřednictvím [obslužná rutina rozšíření Azure Desired State Configuration](/azure/virtual-machines/extensions/dsc-overview) a přes [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span><span class="sxs-lookup"><span data-stu-id="abcc1-104">Desired State Configuration (DSC) is supported in Microsoft Azure through the [Azure Desired State Configuration extension handler](/azure/virtual-machines/extensions/dsc-overview) and through [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span></span>

## <a name="azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="abcc1-105">Obslužná rutina rozšíření Azure Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="abcc1-105">Azure Desired State Configuration extension handler</span></span>

<span data-ttu-id="abcc1-106">Rozšíření DSC Azure umožňuje virtuální počítače hostované v Microsoft Azure a spravovat pomocí DSC.</span><span class="sxs-lookup"><span data-stu-id="abcc1-106">The Azure DSC extension allows VMs hosted in Microsoft Azure to be managed with DSC.</span></span>
<span data-ttu-id="abcc1-107">Další informace najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="abcc1-107">For more information, see the following topics:</span></span>

- [<span data-ttu-id="abcc1-108">Obslužná rutina rozšíření Azure Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="abcc1-108">Azure Desired State Configuration extension handler</span></span>](/azure/virtual-machines/extensions/dsc-overview)
- [<span data-ttu-id="abcc1-109">Windows VMSS a Desired State Configuration pomocí šablon Azure Resource Manageru</span><span class="sxs-lookup"><span data-stu-id="abcc1-109">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>](/azure/virtual-machines/extensions/dsc-template)
- [<span data-ttu-id="abcc1-110">Předávání přihlašovacích údajů do obslužné rutiny rozšíření DSC Azure</span><span class="sxs-lookup"><span data-stu-id="abcc1-110">Passing credentials to the Azure DSC extension handler</span></span>](/azure/virtual-machines/extensions/dsc-credentials)
- [<span data-ttu-id="abcc1-111">Historie rozšíření Azure Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="abcc1-111">Azure Desired State Configuration extension history</span></span>](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a><span data-ttu-id="abcc1-112">Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="abcc1-112">Azure Automation DSC</span></span>

<span data-ttu-id="abcc1-113">[Služby Azure Automation](https://azure.microsoft.com/en-us/services/automation/) vám umožní spravovat konfigurace DSC, prostředky a spravované uzly z v rámci Azure.</span><span class="sxs-lookup"><span data-stu-id="abcc1-113">The [Azure Automation service](https://azure.microsoft.com/en-us/services/automation/) allows you to manage DSC configurations, resources, and managed nodes from within Azure.</span></span> <span data-ttu-id="abcc1-114">Další informace najdete v těchto tématech:</span><span class="sxs-lookup"><span data-stu-id="abcc1-114">For more information, see the following topics:</span></span>

- [<span data-ttu-id="abcc1-115">Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="abcc1-115">Azure Automation DSC</span></span>](/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="abcc1-116">Začínáme s Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="abcc1-116">Getting started with Azure Automation DSC</span></span>](/azure/automation/automation-dsc-getting-started)
- [<span data-ttu-id="abcc1-117">Připojování počítačů pro správu pomocí Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="abcc1-117">Onboarding machines for management by Azure Automation DSC</span></span>](/azure/automation/automation-dsc-onboarding)
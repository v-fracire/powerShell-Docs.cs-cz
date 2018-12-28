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
# <a name="using-dsc-on-microsoft-azure"></a>Použití platformy DSC v Microsoft Azure

Desired State Configuration (DSC) se podporuje v Microsoft Azure prostřednictvím [obslužná rutina rozšíření Azure Desired State Configuration](/azure/virtual-machines/extensions/dsc-overview) a přes [Azure Automation DSC](/azure/automation/automation-dsc-overview).

## <a name="azure-desired-state-configuration-extension-handler"></a>Obslužná rutina rozšíření Azure Desired State Configuration

Rozšíření DSC Azure umožňuje virtuální počítače hostované v Microsoft Azure a spravovat pomocí DSC.
Další informace najdete v těchto tématech:

- [Obslužná rutina rozšíření Azure Desired State Configuration](/azure/virtual-machines/extensions/dsc-overview)
- [Windows VMSS a Desired State Configuration pomocí šablon Azure Resource Manageru](/azure/virtual-machines/extensions/dsc-template)
- [Předávání přihlašovacích údajů do obslužné rutiny rozšíření DSC Azure](/azure/virtual-machines/extensions/dsc-credentials)
- [Historie rozšíření Azure Desired State Configuration](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a>Azure Automation DSC

[Služby Azure Automation](https://azure.microsoft.com/en-us/services/automation/) vám umožní spravovat konfigurace DSC, prostředky a spravované uzly z v rámci Azure. Další informace najdete v těchto tématech:

- [Azure Automation DSC](/azure/automation/automation-dsc-overview)
- [Začínáme s Azure Automation DSC](/azure/automation/automation-dsc-getting-started)
- [Připojování počítačů pro správu pomocí Azure Automation DSC](/azure/automation/automation-dsc-onboarding)
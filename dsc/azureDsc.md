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
# <a name="using-dsc-on-microsoft-azure"></a>Použití platformy DSC v Microsoft Azure

Požadovaná stav konfigurace (DSC) se podporuje v Microsoft Azure prostřednictvím [obslužná rutina rozšíření konfigurace požadovaného stavu Azure](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) a pomocí [Azure Automation DSC](/azure/automation/automation-dsc-overview).

## <a name="azure-desired-state-configuration-extension-handler"></a>Stavu Azure požadovaná konfigurace rozšíření obslužné rutiny

Rozšíření Azure DSC umožňuje virtuální počítače hostované v Microsoft Azure a spravovat pomocí DSC.
Další informace najdete v těchto tématech:

- [Stavu Azure požadovaná konfigurace rozšíření obslužné rutiny](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview)
- [Windows VMSS a konfigurace požadovaného stavu pomocí šablon Azure Resource Manageru](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-template)
- [Předání přihlašovacích údajů k obslužné rutině rozšíření Azure DSC](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-credentials)
- [Historie stavu Azure požadovaná konfigurace rozšíření](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a>Azure Automation DSC.

[Služba Azure Automation](https://azure.microsoft.com/services/automation/) vám umožní spravovat konfigurace DSC, prostředky a spravované uzly z v rámci Azure. Další informace najdete v těchto tématech:

- [Azure Automation DSC](/azure/automation/automation-dsc-overview)
- [Začínáme s Azure Automation DSC.](/azure/automation/automation-dsc-getting-started)
- [Registrace počítačů pro správu Azure Automation DSC.](/azure/automation/automation-dsc-onboarding)
---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Nasazení ve službě Azure Automation
ms.openlocfilehash: dc382b1cf3ceaa787f54c555d01e6bd9ba70e680
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004008"
---
# <a name="deploy-to-azure-automation"></a>Nasazení ve službě Azure Automation

Nasazení do služby Azure Automation tlačítko na stránce s podrobnostmi balíčku se nasadit balíček z Galerie prostředí PowerShell pro Azure Automation.

![Nasazení do služby Azure Automation tlačítko](../../Images/DeployToAzureAutomationButton.png)

Po kliknutí na to vás přesměrují na portálu pro správu Azure, kde můžete přihlásit pomocí přihlašovacích údajů svého účtu Azure.
Pokud balíček obsahuje závislosti, všechny závislosti se nasadí i do Azure Automation.

> [!WARNING]
> Pokud ještě neexistuje stejného balíčku a verze ve vašem účtu Automation, přepíše ho znovu nasadíte z Galerie prostředí PowerShell balíček ve vašem účtu Automation.

Pokud provádíte nasazení modulu, zobrazí se v části moduly Azure Automation.  Pokud provádíte nasazení skriptu, se zobrazí v části Runbooky Azure Automation.

Nasazení do služby Azure Automation tlačítka je možné zakázat tak, že přidáte značku AzureAutomationNotSupported metadata balíčků.

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a>Vyžadování přijetí licence při nasazení ve službě Azure Automation

Pokud se nasazuje do Azure Automation modul vyžaduje souhlas s podmínkami licence, uživatelské rozhraní portálu se zobrazí o tom, že ustanovení o právním omezení ' Tento modul vyžaduje souhlas s podmínkami licence. Kliknutím na OK, abyste přijali licenční podmínky. "

![Nasazení do Azure Automation vyžaduje souhlas s podmínkami licence](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a>Další podrobnosti

- [Vyžadování přijetí licence v modulu PowerShellGet](../../concepts/module-license-acceptance.md)
- [Vyžadování přijetí licence v galerii prostředí PowerShell](packages-that-require-license-acceptance.md)
- [Web Azure Automation](http://azure.microsoft.com/services/automation/)

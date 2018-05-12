---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Nasazení ve službě Azure Automation
ms.openlocfilehash: 1efdc289228d3a6962302d12ccf44143ce63a806
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="deploy-to-azure-automation"></a>Nasazení ve službě Azure Automation

Nasadit do Azure Automation tlačítko na stránce podrobností položky nasadí položky z Galerie prostředí PowerShell pro Azure Automation.

![Nasazení do služby Azure Automation tlačítko](../../Images/DeployToAzureAutomationButton.png)

Při kliknutí na, přesměruje je na portálu Azure Management Portal, kde můžete přihlásit pomocí svých přihlašovacích údajů účtu Azure.
Pokud položka obsahuje závislosti, všechny závislosti bude nasazení také do Azure Automation.

> [!WARNING]
> Pokud stejné položky a verzí již existují v účtu Automation, znovu nasazení z Galerie Powershellu přepíše položky v účtu Automation.

Pokud nasadíte modul, se zobrazí v části moduly Azure Automation.  Pokud nasadíte skriptu, zobrazí se v části sady Runbook automatizace Azure.

Nasadit do Azure Automation tlačítko lze zakázat pomocí přidání značka AzureAutomationNotSupported na metadata položky.

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a>Vyžadování přijetí licence při nasazení ve službě Azure Automation

Pokud modul nasazení pro Azure Automation vyžaduje přijetí licence, portál uživatelského rozhraní se zobrazí právní omezení o tom, že se tento modul vyžaduje přijetí licence. Klepnutím na OK přijímáte licenční podmínky. "

![Nasazení do Azure Automation vyžaduje přijetí licence](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a>Další informace

- [Vyžadovat přijetí licence v PowerShellGet](../../concepts/module-license-acceptance.md)
- [Vyžadovat přijetí licence v galerii prostředí PowerShell](items-that-require-license-acceptance.md)
- [Webové stránky Azure Automation.](http://azure.microsoft.com/services/automation/)

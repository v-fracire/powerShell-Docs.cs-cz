---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: psgallery_deploy_to_azure_automation
ms.openlocfilehash: 8da4eabead6a419dc0c01c74335c06bf8be25d0c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
<a name="deploy-to-azure-automation"></a>Nasazení ve službě Azure Automation
===========================

Nasadit do Azure Automation tlačítko na stránce podrobností položky nasadí položky z Galerie prostředí PowerShell pro Azure Automation.

![Nasazení do služby Azure Automation tlačítko](Images/DeployToAzureAutomationButton.png)

Při kliknutí na, přesměruje je na portálu Azure Management Portal, kde můžete přihlásit pomocí svých přihlašovacích údajů účtu Azure.
Pokud položka obsahuje závislosti, všechny závislosti bude nasazení také do Azure Automation.

Upozornění: Pokud stejné položky a verzí již existují v účtu Automation, znovu nasazení z Galerie Powershellu přepíše položky v účtu Automation.

Pokud nasadíte modul, se zobrazí v části moduly Azure Automation.  Pokud nasadíte skriptu, zobrazí se v části sady Runbook automatizace Azure.

Nasadit do Azure Automation tlačítko lze zakázat pomocí přidání značka AzureAutomationNotSupported na metadata položky.

Další informace o Azure Automation, najdete v článku na webu Azure Automation [web Azure Automation](http://azure.microsoft.com/services/automation/).
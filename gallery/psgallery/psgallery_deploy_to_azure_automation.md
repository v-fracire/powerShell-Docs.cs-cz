---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_deploy_to_azure_automation
ms.openlocfilehash: 91f48fb43d7fb099e34ce5d3b3b632e3cb119d64
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
<a name="deploy-to-azure-automation"></a>Nasazení do služby Azure Automation
===========================

Nasadit do Azure Automation tlačítko na stránce podrobností položky nasadí položky z Galerie prostředí PowerShell pro Azure Automation.

![Nasazení do služby Azure Automation tlačítko](Images/DeployToAzureAutomationButton.png)

Při kliknutí na, přesměruje je na portálu Azure Management Portal, kde můžete přihlásit pomocí svých přihlašovacích údajů účtu Azure.
Pokud položka obsahuje závislosti, všechny závislosti bude nasazení také do Azure Automation.

Upozornění: Pokud stejné položky a verzí již existují v účtu Automation, znovu nasazení z Galerie Powershellu přepíše položky v účtu Automation.

Pokud nasadíte modul, se zobrazí v části moduly Azure Automation.  Pokud nasadíte skriptu, zobrazí se v části sady Runbook automatizace Azure.

Nasadit do Azure Automation tlačítko lze zakázat pomocí přidání značka AzureAutomationNotSupported na metadata položky.

Další informace o Azure Automation, najdete v článku na webu Azure Automation [web Azure Automation](http://azure.microsoft.com/en-us/services/automation/).


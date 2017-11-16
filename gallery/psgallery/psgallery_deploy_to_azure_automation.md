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
<a name="deploy-to-azure-automation"></a><span data-ttu-id="38d2a-103">Nasazení do služby Azure Automation</span><span class="sxs-lookup"><span data-stu-id="38d2a-103">Deploy to Azure Automation</span></span>
===========================

<span data-ttu-id="38d2a-104">Nasadit do Azure Automation tlačítko na stránce podrobností položky nasadí položky z Galerie prostředí PowerShell pro Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="38d2a-104">The Deploy to Azure Automation button on the item details page will deploy the item from the PowerShell Gallery to Azure Automation.</span></span>

![Nasazení do služby Azure Automation tlačítko](Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="38d2a-106">Při kliknutí na, přesměruje je na portálu Azure Management Portal, kde můžete přihlásit pomocí svých přihlašovacích údajů účtu Azure.</span><span class="sxs-lookup"><span data-stu-id="38d2a-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="38d2a-107">Pokud položka obsahuje závislosti, všechny závislosti bude nasazení také do Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="38d2a-107">If the item includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

<span data-ttu-id="38d2a-108">Upozornění: Pokud stejné položky a verzí již existují v účtu Automation, znovu nasazení z Galerie Powershellu přepíše položky v účtu Automation.</span><span class="sxs-lookup"><span data-stu-id="38d2a-108">WARNING:  If the same item and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the item in your Automation account.</span></span>

<span data-ttu-id="38d2a-109">Pokud nasadíte modul, se zobrazí v části moduly Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="38d2a-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="38d2a-110">Pokud nasadíte skriptu, zobrazí se v části sady Runbook automatizace Azure.</span><span class="sxs-lookup"><span data-stu-id="38d2a-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="38d2a-111">Nasadit do Azure Automation tlačítko lze zakázat pomocí přidání značka AzureAutomationNotSupported na metadata položky.</span><span class="sxs-lookup"><span data-stu-id="38d2a-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the item metadata.</span></span>

<span data-ttu-id="38d2a-112">Další informace o Azure Automation, najdete v článku na webu Azure Automation [web Azure Automation](http://azure.microsoft.com/en-us/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="38d2a-112">To learn more about Azure Automation, see the Azure Automation website [Azure Automation website](http://azure.microsoft.com/en-us/services/automation/).</span></span>

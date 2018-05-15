---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Nasazení ve službě Azure Automation
ms.openlocfilehash: 1efdc289228d3a6962302d12ccf44143ce63a806
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="deploy-to-azure-automation"></a><span data-ttu-id="14023-103">Nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="14023-103">Deploy to Azure Automation</span></span>

<span data-ttu-id="14023-104">Nasadit do Azure Automation tlačítko na stránce podrobností položky nasadí položky z Galerie prostředí PowerShell pro Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="14023-104">The Deploy to Azure Automation button on the item details page will deploy the item from the PowerShell Gallery to Azure Automation.</span></span>

![Nasazení do služby Azure Automation tlačítko](../../Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="14023-106">Při kliknutí na, přesměruje je na portálu Azure Management Portal, kde můžete přihlásit pomocí svých přihlašovacích údajů účtu Azure.</span><span class="sxs-lookup"><span data-stu-id="14023-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="14023-107">Pokud položka obsahuje závislosti, všechny závislosti bude nasazení také do Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="14023-107">If the item includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

> [!WARNING]
> <span data-ttu-id="14023-108">Pokud stejné položky a verzí již existují v účtu Automation, znovu nasazení z Galerie Powershellu přepíše položky v účtu Automation.</span><span class="sxs-lookup"><span data-stu-id="14023-108">If the same item and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the item in your Automation account.</span></span>

<span data-ttu-id="14023-109">Pokud nasadíte modul, se zobrazí v části moduly Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="14023-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="14023-110">Pokud nasadíte skriptu, zobrazí se v části sady Runbook automatizace Azure.</span><span class="sxs-lookup"><span data-stu-id="14023-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="14023-111">Nasadit do Azure Automation tlačítko lze zakázat pomocí přidání značka AzureAutomationNotSupported na metadata položky.</span><span class="sxs-lookup"><span data-stu-id="14023-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the item metadata.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="14023-112">Vyžadování přijetí licence při nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="14023-112">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="14023-113">Pokud modul nasazení pro Azure Automation vyžaduje přijetí licence, portál uživatelského rozhraní se zobrazí právní omezení o tom, že se tento modul vyžaduje přijetí licence.</span><span class="sxs-lookup"><span data-stu-id="14023-113">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="14023-114">Klepnutím na OK přijímáte licenční podmínky. "</span><span class="sxs-lookup"><span data-stu-id="14023-114">By clicking OK, you are accepting license terms.'</span></span>

![Nasazení do Azure Automation vyžaduje přijetí licence](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="14023-116">Další informace</span><span class="sxs-lookup"><span data-stu-id="14023-116">More details</span></span>

- [<span data-ttu-id="14023-117">Vyžadovat přijetí licence v PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="14023-117">Require License Acceptance in PowerShellGet</span></span>](../../concepts/module-license-acceptance.md)
- [<span data-ttu-id="14023-118">Vyžadovat přijetí licence v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="14023-118">Require License Acceptance in PowerShell Gallery</span></span>](items-that-require-license-acceptance.md)
- [<span data-ttu-id="14023-119">Webové stránky Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="14023-119">Azure Automation website</span></span>](http://azure.microsoft.com/services/automation/)

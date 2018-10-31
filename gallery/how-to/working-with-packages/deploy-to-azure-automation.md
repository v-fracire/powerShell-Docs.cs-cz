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
# <a name="deploy-to-azure-automation"></a><span data-ttu-id="da8cc-103">Nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="da8cc-103">Deploy to Azure Automation</span></span>

<span data-ttu-id="da8cc-104">Nasazení do služby Azure Automation tlačítko na stránce s podrobnostmi balíčku se nasadit balíček z Galerie prostředí PowerShell pro Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="da8cc-104">The Deploy to Azure Automation button on the package details page will deploy the package from the PowerShell Gallery to Azure Automation.</span></span>

![Nasazení do služby Azure Automation tlačítko](../../Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="da8cc-106">Po kliknutí na to vás přesměrují na portálu pro správu Azure, kde můžete přihlásit pomocí přihlašovacích údajů svého účtu Azure.</span><span class="sxs-lookup"><span data-stu-id="da8cc-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="da8cc-107">Pokud balíček obsahuje závislosti, všechny závislosti se nasadí i do Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="da8cc-107">If the package includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

> [!WARNING]
> <span data-ttu-id="da8cc-108">Pokud ještě neexistuje stejného balíčku a verze ve vašem účtu Automation, přepíše ho znovu nasadíte z Galerie prostředí PowerShell balíček ve vašem účtu Automation.</span><span class="sxs-lookup"><span data-stu-id="da8cc-108">If the same package and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the package in your Automation account.</span></span>

<span data-ttu-id="da8cc-109">Pokud provádíte nasazení modulu, zobrazí se v části moduly Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="da8cc-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="da8cc-110">Pokud provádíte nasazení skriptu, se zobrazí v části Runbooky Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="da8cc-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="da8cc-111">Nasazení do služby Azure Automation tlačítka je možné zakázat tak, že přidáte značku AzureAutomationNotSupported metadata balíčků.</span><span class="sxs-lookup"><span data-stu-id="da8cc-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the package metadata.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="da8cc-112">Vyžadování přijetí licence při nasazení ve službě Azure Automation</span><span class="sxs-lookup"><span data-stu-id="da8cc-112">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="da8cc-113">Pokud se nasazuje do Azure Automation modul vyžaduje souhlas s podmínkami licence, uživatelské rozhraní portálu se zobrazí o tom, že ustanovení o právním omezení ' Tento modul vyžaduje souhlas s podmínkami licence.</span><span class="sxs-lookup"><span data-stu-id="da8cc-113">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="da8cc-114">Kliknutím na OK, abyste přijali licenční podmínky. "</span><span class="sxs-lookup"><span data-stu-id="da8cc-114">By clicking OK, you are accepting license terms.'</span></span>

![Nasazení do Azure Automation vyžaduje souhlas s podmínkami licence](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="da8cc-116">Další podrobnosti</span><span class="sxs-lookup"><span data-stu-id="da8cc-116">More details</span></span>

- [<span data-ttu-id="da8cc-117">Vyžadování přijetí licence v modulu PowerShellGet</span><span class="sxs-lookup"><span data-stu-id="da8cc-117">Require License Acceptance in PowerShellGet</span></span>](../../concepts/module-license-acceptance.md)
- [<span data-ttu-id="da8cc-118">Vyžadování přijetí licence v galerii prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="da8cc-118">Require License Acceptance in PowerShell Gallery</span></span>](packages-that-require-license-acceptance.md)
- [<span data-ttu-id="da8cc-119">Web Azure Automation</span><span class="sxs-lookup"><span data-stu-id="da8cc-119">Azure Automation website</span></span>](http://azure.microsoft.com/services/automation/)

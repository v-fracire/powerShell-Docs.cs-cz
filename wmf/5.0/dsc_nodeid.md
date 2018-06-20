---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 6c036c2d8f97e559d20dd3ac40133fa06f5dab08
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188281"
---
# <a name="separation-of-node-and-configuration-ids"></a><span data-ttu-id="5796f-102">Oddělení ID uzlu od ID konfigurace</span><span class="sxs-lookup"><span data-stu-id="5796f-102">Separation of Node and Configuration IDs</span></span>

## <a name="overview"></a><span data-ttu-id="5796f-103">Přehled</span><span class="sxs-lookup"><span data-stu-id="5796f-103">Overview</span></span>

<span data-ttu-id="5796f-104">Aby bylo možné poskytnout více flexibilní a efektivní prostředí při používání DSC v režimu pro vyžádání obsahu, jsme přidali celou řadu funkcí v této verzi.</span><span class="sxs-lookup"><span data-stu-id="5796f-104">In order to provide a more flexible and streamlined experience when using DSC in Pull mode, we have added a number of features in this release.</span></span> <span data-ttu-id="5796f-105">Tyto funkce jsou určeny k umožňují flexibilně snadno nastavit a nasadit konfigurace napříč několika uzly, i když stále sledování stavu a vytváření sestav informace pro každý uzel zvlášť.</span><span class="sxs-lookup"><span data-stu-id="5796f-105">These features are intended to allow you to have the flexibility to easily setup and deploy configurations across multiple nodes, while still tracking status and reporting information for each node individually.</span></span>
<span data-ttu-id="5796f-106">Tyto funkce jsou následující:</span><span class="sxs-lookup"><span data-stu-id="5796f-106">These features are as follows:</span></span>

* <span data-ttu-id="5796f-107">Název konfigurace, které identifikuje konfigurace pro počítač.</span><span class="sxs-lookup"><span data-stu-id="5796f-107">A configuration name which identifies the configuration for a computer.</span></span> <span data-ttu-id="5796f-108">Tento název může být sdílen více cílové uzly</span><span class="sxs-lookup"><span data-stu-id="5796f-108">This name can be shared by multiple target nodes</span></span>
* <span data-ttu-id="5796f-109">ID agenta, které jedinečně identifikují jeden uzel</span><span class="sxs-lookup"><span data-stu-id="5796f-109">An agent ID which uniquely identifies a single node</span></span>
* <span data-ttu-id="5796f-110">Registrace krok, který dochází pouze při prvním cílový uzel připojuje k serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="5796f-110">A registration step which only occurs the first time a target node connects to a pull server</span></span>

<span data-ttu-id="5796f-111">**Poznámka:** tyto funkce a funkce byly přidány a nenahrazují stávající funkce pro vyžádání obsahu a koncepty.</span><span class="sxs-lookup"><span data-stu-id="5796f-111">**Note:** These features and functionality have been added and do not replace the existing pull features and concepts.</span></span> <span data-ttu-id="5796f-112">Můžete použít tyto nové funkce nebo starší k novému serveru vyžádané replikace přesouvání v této verzi.</span><span class="sxs-lookup"><span data-stu-id="5796f-112">You can use these new features or the older ones with the new pull server shipping in this release.</span></span>

<span data-ttu-id="5796f-113">Další informace najdete v tématu [nastavení vyžadování klienta pomocí názvy konfigurace](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span><span class="sxs-lookup"><span data-stu-id="5796f-113">For more information, see [Setting up a pull client using configuration names](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span></span>

---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 5b9eea1c90bfd5a8cee3897d832bf7775a750308
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="separation-of-node-and-configuration-ids"></a><span data-ttu-id="54b5d-102">Oddělení uzlu a konfigurace ID</span><span class="sxs-lookup"><span data-stu-id="54b5d-102">Separation of Node and Configuration IDs</span></span>

## <a name="overview"></a><span data-ttu-id="54b5d-103">Přehled</span><span class="sxs-lookup"><span data-stu-id="54b5d-103">Overview</span></span>

<span data-ttu-id="54b5d-104">Aby bylo možné poskytnout více flexibilní a efektivní prostředí při používání DSC v režimu pro vyžádání obsahu, jsme přidali celou řadu funkcí v této verzi.</span><span class="sxs-lookup"><span data-stu-id="54b5d-104">In order to provide a more flexible and streamlined experience when using DSC in Pull mode, we have added a number of features in this release.</span></span> <span data-ttu-id="54b5d-105">Tyto funkce jsou určeny k umožňují flexibilně snadno nastavit a nasadit konfigurace napříč několika uzly, i když stále sledování stavu a vytváření sestav informace pro každý uzel zvlášť.</span><span class="sxs-lookup"><span data-stu-id="54b5d-105">These features are intended to allow you to have the flexibility to easily setup and deploy configurations across multiple nodes, while still tracking status and reporting information for each node individually.</span></span> <span data-ttu-id="54b5d-106">Tyto funkce jsou následující:</span><span class="sxs-lookup"><span data-stu-id="54b5d-106">These features are as follows:</span></span>

* <span data-ttu-id="54b5d-107">Název konfigurace, které identifikuje konfigurace pro počítač.</span><span class="sxs-lookup"><span data-stu-id="54b5d-107">A configuration name which identifies the configuration for a computer.</span></span> <span data-ttu-id="54b5d-108">Tento název může být sdílen více cílové uzly</span><span class="sxs-lookup"><span data-stu-id="54b5d-108">This name can be shared by multiple target nodes</span></span> 
* <span data-ttu-id="54b5d-109">ID agenta, které jedinečně identifikují jeden uzel</span><span class="sxs-lookup"><span data-stu-id="54b5d-109">An agent ID which uniquely identifies a single node</span></span>
* <span data-ttu-id="54b5d-110">Registrace krok, který dochází pouze při prvním cílový uzel připojuje k serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="54b5d-110">A registration step which only occurs the first time a target node connects to a pull server</span></span>

<span data-ttu-id="54b5d-111">**Poznámka:** tyto funkce a funkce byly přidány a nenahrazují stávající funkce pro vyžádání obsahu a koncepty.</span><span class="sxs-lookup"><span data-stu-id="54b5d-111">**Note:** These features and functionality have been added and do not replace the existing pull features and concepts.</span></span> <span data-ttu-id="54b5d-112">Můžete použít tyto nové funkce nebo starší k novému serveru vyžádané replikace přesouvání v této verzi.</span><span class="sxs-lookup"><span data-stu-id="54b5d-112">You can use these new features or the older ones with the new pull server shipping in this release.</span></span>

<span data-ttu-id="54b5d-113">Další informace najdete v tématu [nastavení vyžadování klienta pomocí názvy konfigurace](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span><span class="sxs-lookup"><span data-stu-id="54b5d-113">For more information, see [Setting up a pull client using configuration names](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span></span>

